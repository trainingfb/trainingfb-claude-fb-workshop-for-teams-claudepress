DURATA: 10-20 MINUTI

> **Ognuno sul suo portatile, ma restate allo stesso tavolo: è ancora lavoro di squadra.**

# T2 · Le fondamenta

Due cose, in quest'ordine: **i tuoi due componenti**, poi **il tuo strumento**, il subagent `smoke-test` — l'unico dei tre a servire a tutta la squadra. Quando li hai pushati tutti e due, ci si rivede in [`02-si-allinea.md`](02-si-allinea.md).

> **Intanto:** T1 scrive `PostCard`, `EmptyState` e `Input` più la skill `/new-page`, T3 scrive `Field` più la skill `/new-form`. Nessuno dei due tocca i tuoi file.

Obiettivo della mattina: **quando comincerete a lavorare da soli, non dovrà mancare niente a nessuno.**

> Se sei in ritardo, sfora sui componenti: un componente brutto si sistema dopo, uno strumento che non hai scritto non lo userai mai.

---

## Passo 1 · I tuoi componenti

| Componente | Chi lo userà |
|---|---|
| `StatusBadge.tsx` | tu |
| `Button.tsx` | tu e T3 |

`Button` lo scrivi tu e lo userà anche T3 nel suo form: è il contratto che tiene insieme le due cose, non un accordo a voce.

Nel repo ci sono già tre skill pronte: **`/new-component`**, che fa esattamente questo, più **`/commit`** e **`/pr`** che userete tutto il giorno. Aprile adesso, sono tre minuti — `/new-component` ti serve anche come modello al passo 2.

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

Non aspettare di aver finito anche lo strumento: i tuoi componenti servono agli altri due.

```bash
git add src/components/ui/
git commit -m "feat: shared UI components"
git pull --rebase
git push origin main
```

Se `git push` ti rifiuta perché nel frattempo ha pushato un altro, rifai `git pull --rebase` e ripusha: state toccando file diversi, quindi non ci sono conflitti veri.

**Verifica**

- [ ] `StatusBadge.tsx` e `Button.tsx` sono in `src/components/ui/`
- [ ] `npm run check` passa
- [ ] non hai toccato `src/contracts/`
- [ ] committato e pushato

---

## Passo 2 · Il tuo strumento — il subagent `smoke-test`

**Cosa stai per fare:** scriverti uno strumento tuo, che poi usa tutta la squadra.

Il tuo si chiama **`smoke-test`** e fa una cosa sola: chiama tutte le pagine del sito e ti dice quali rispondono e quali no.

**Lo userete tutti e tre**: ognuno alla fine del suo track, per controllare di non aver rotto niente, e poi tutti insieme a fine giornata sul progetto mergiato — è quello il momento in cui, se è tutto verde, avete finito davvero. Tu puoi rilanciarlo quando vuoi, dopo ogni pagina: costa un comando. Il tuo track è il più corto: questo è il pezzo che dai alla squadra in cambio.

**È un subagent, non una skill**, e la differenza è tutta qui: fa un lavoro rumoroso — cinque o sei `curl` di fila — che gira in una sessione separata, e a te torna solo il verdetto. Una skill invece è una procedura che esegue Claude nella tua sessione, come `/new-component` che hai appena usato due volte.

**Ne scrivi uno solo.** Gli altri due stanno scrivendo il loro, e ve li scambiate col `git pull` dell'allineamento.

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

**Provalo subito**, con `npm run dev` attivo in un altro terminale.

**Prompt:**

```
Usa il subagent smoke-test
```

Adesso deve dirti che `/`, `/admin/posts`, `/admin/posts/new` e le due API rispondono 200 — le pagine sono i segnaposto — e che `/posts/<slug>` e `/admin/posts/po-001` non rispondono, perché quelle due pagine non le ha ancora scritte nessuno. **È il risultato giusto**: fra un'ora saranno tutte verdi, e sarà la prova che avete finito.

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
