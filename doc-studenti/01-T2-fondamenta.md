> **Passo 1 · T2 · 10-20 minuti · allo stesso tavolo**
> ← [00 · Si parte](00-si-parte.md) · [indice](README.md) · prossimo → [02 · Ci si allinea](02-si-allinea.md)

> **Ognuno sul suo portatile, ma restate allo stesso tavolo: è ancora lavoro di squadra.**

# T2 · Le fondamenta

## Passo 1 · I tuoi componenti

| Componente | Chi lo userà |
|---|---|
| `StatusBadge.tsx` | tu |
| `Button.tsx` | tu e T3 |

`Button` lo scrivi tu e lo userà anche T3 nel suo form: è il contratto che tiene insieme le due cose, non un accordo a voce.

Nel repo ci sono già tre skill pronte: **`/new-component`**, per creare nuovi componenti, più **`/commit`** e **`/pr`** che userete tutto il giorno. Aprile adesso, sono tre minuti — `/new-component` ti serve anche come modello al passo 2.

**Soluzione / Prompt** — comincia dal primo:

```
/new-component StatusBadge
```

La skill va a leggere `StatusBadgeProps` nel contratto, scrive il file, e lancia `npm run check` da sola. Se ti dice che una firma non esiste, **non inventarla**: il contratto è quello.

Le due regole: **le firme sono quelle del contratto**, e i componenti **ricevono props e rendono markup** — niente fetch, niente logica di dominio.

Apri il file che è uscito e guardalo: è la forma che deve avere anche l'altro.

Adesso **fai la stessa cosa per `Button`** — è la stessa skill, cambia solo il nome.

**Soluzione / Prompt:**

```
/new-component Button
```

La sua firma è `ButtonProps`, nello stesso contratto. Attenzione a questo: `Button` lo userà anche T3 nel suo form, quindi è il componente su cui non puoi inventarti niente.

Da un altro terminale avviare:

```bash
npm run check
```

Se ci sono errori chiedi a Claude di risolverli.

### Committa e pusha subito

Non aspettare di aver finito tutta la sezione: i tuoi componenti servono agli altri due.

```bash
git add src/components/ui/
git commit -m "feat: shared UI components"
git pull --rebase
git push origin main
```

> `git pull --rebase` scarica quello che hanno pushato gli altri e rimette il tuo commit in cima: la storia resta lineare, senza commit «Merge branch…».

Se `git push` ti rifiuta perché nel frattempo ha pushato un altro, rifai `git pull --rebase` e ripusha: state toccando file diversi, quindi non ci sono conflitti veri.

**Verifica**

- [ ] `StatusBadge.tsx` e `Button.tsx` sono in `src/components/ui/`
- [ ] `npm run check` passa
- [ ] non hai toccato `src/contracts/`
- [ ] committato e pushato

---

## Passo 2 · Il tuo subagent `smoke-test`

**Cosa stai per fare:** scrivere un agente, che poi usa tutto il team.

Il tuo si chiama **`smoke-test`** e fa una cosa sola: chiama tutte le pagine del sito e ti dice quali rispondono e quali no.

**Lo userete tutti e tre**: ognuno alla fine del suo track, per controllare di non aver rotto niente, e poi tutti insieme a fine giornata sul progetto mergiato — è quello il momento in cui, se è tutto verde, avete finito davvero. Tu puoi rilanciarlo quando vuoi, dopo ogni pagina: costa un comando. 

**È un subagent, non una skill**, e la differenza è tutta qui: esegue un lavoro in background, cinque o sei `curl` di fila, e gira in una sessione separata: a te torna solo il verdetto! Una skill invece è una procedura che esegue Claude nella tua sessione, come `/new-component` che hai appena usato due volte.

Tre cose da fare, in ordine:

1. copia il prompt qui sotto e mandalo: Claude scrive `.claude/agents/smoke-test.md`
2. apri il file e rileggilo
3. **taglia** quello che è di troppo: più una procedura è lunga, meno farà quello che credi

**Prompt:**

```
Leggi @.claude/skills/new-component/SKILL.md: è l'esempio del livello di
dettaglio che voglio.

Scrivi .claude/agents/smoke-test.md, un subagent in sola lettura.
Frontmatter: name smoke-test, una description che dica che verifica che tutte
le pagine rispondano, e tools: Bash — nessuno strumento di scrittura.

Con il dev server attivo su localhost:3000, fa una curl su ognuna di queste
rotte e riporta il codice HTTP:
  /
  /admin/posts
  /admin/posts/new
  /admin/posts/po-001
  /api/posts
  /api/posts?status=published
Poi prende il primo slug da /api/posts?status=published e prova anche
/posts/<slug>.

Risponde con una tabella, una riga per rotta: rotta e codice.
Chiude con una riga sola: TUTTO OK, oppure l'elenco delle rotte che non
rispondono 200.
Non avviare il dev server: se non risponde niente, dillo e basta.
```

**Provalo subito**, ma assicurati che `npm run dev` sia attivo in un altro terminale. Il sito dev'essere visibile

**Prompt:**

```
Usa il subagent smoke-test
```

Adesso deve risponderti più o meno così:

```
| Rotta                                 | Codice |
|---------------------------------------|--------|
| /                                     | 200    |
| /admin/posts                          | 200    |
| /admin/posts/new                      | 200    |
| /admin/posts/po-001                   | 404    |
| /api/posts                            | 200    |
| /api/posts?status=published           | 200    |
| /posts/il-contratto-prima-del-codice  | 404    |

Non rispondono 200: /admin/posts/po-001, /posts/il-contratto-prima-del-codice
```

**I due 404 sono il risultato giusto**, non un errore tuo: sono le due pagine che nel progetto non esistono ancora.

| Rotta in 404 | La pagina che manca | Chi la scrive |
|---|---|---|
| `/posts/<slug>` | `src/app/posts/[slug]/page.tsx`, il dettaglio di un post | T1 |
| `/admin/posts/po-001` | `src/app/admin/posts/[id]/page.tsx`, la modifica di un post | T3 |

Le altre rispondono 200 perché le pagine segnaposto e le API ci sono già. Fra un'ora la tabella sarà tutta a 200, e sarà la prova che avete finito.

> La grafica della tabella può cambiare (bordi, ordine delle righe, la riga finale scritta in un altro modo): conta che i codici siano questi.

### Committa e pusha

```bash
git add .claude/
git commit -m "chore: add smoke-test agent"
git pull --rebase
git push origin main
```

Gli altri due stanno scrivendo file diversi dentro `.claude/`, quindi anche qui nessun conflitto vero.

**Verifica**

- [ ] `.claude/agents/smoke-test.md` esiste, ed è sotto le trenta righe
- [ ] l'hai provato una volta e risponde nel formato giusto
- [ ] committato e pushato

---

## Fatto

- [ ] i tuoi due componenti sono su `main`
- [ ] il tuo subagent è su `main`, provato

Appena hanno pushato anche gli altri due, tutti e tre insieme: [`02-si-allinea.md`](02-si-allinea.md).


---

# AIUTA I TUOI COLLEGHI

Se hai finito prima degli altri, dai una mano ai tuoi colleghi