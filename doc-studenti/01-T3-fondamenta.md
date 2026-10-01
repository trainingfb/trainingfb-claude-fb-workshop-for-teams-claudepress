DURATA: 10-20 MINUTI

> **Ognuno sul suo  portatile, ma restate allo stesso tavolo: è ancora lavoro di squadra.**

# T3 · Le fondamenta

Due cose, in quest'ordine: **il tuo componente**, poi **il tuo strumento**, la skill `/new-form`, che è la più lunga dei tre. Quando li hai pushati tutti e due, ci si rivede in [`02-si-allinea.md`](02-si-allinea.md).

> **Intanto:** T1 scrive `PostCard`, `EmptyState` e `Input` più la skill `/new-page`, T2 scrive `StatusBadge` e `Button` più il subagent `smoke-test`. Nessuno dei due tocca i tuoi file.

Obiettivo della mattina: **quando comincerete a lavorare da soli, non dovrà mancare niente a nessuno.**

> Se sei in ritardo, sfora sul componente: un componente brutto si sistema dopo, uno strumento che non hai scritto non lo userai mai.

---

## Passo 1 · Il tuo componente

| Componente | Chi lo userà |
|---|---|
| `Field.tsx` | tu |

**Ne hai uno solo** perché al passo 2 scrivi la skill più lunga dei tre.

Gli altri due componenti che ti serviranno nel form — **`Input` e `Button`** — non li scrivi tu: `Input` lo scrive T1, che non lo userà mai, e `Button` lo scrive T2. Ti arrivano con il `git pull` dell'allineamento, e nel frattempo ti basta la loro firma nel contratto. **È il punto di tutta la giornata**: scrivi contro una firma, non contro il codice di qualcun altro.

Nel repo ci sono già tre skill pronte: **`/new-component`**, che fa esattamente questo, più **`/commit`** e **`/pr`** che userete tutto il giorno. Aprile adesso, sono tre minuti — `/new-component` ti serve anche come modello al passo 2.

**Soluzione / Prompt:**

```
/new-component Field
```

La skill va a leggere `FieldProps` nel contratto, scrive il file, e lancia `npm run check` da sola. Se ti dice che una firma non esiste, **non inventarla**: il contratto è quello.

Le due regole: **le firme sono quelle del contratto**, e i componenti **ricevono props e rendono markup** — niente fetch, niente logica di dominio.

Da un altro terminale avviare:

```bash
npm run check
```

Se ci sono errori chiedi a Claude di risolverli.

### Committa e pusha subito

Non aspettare di aver finito anche lo strumento: il tuo componente serve agli altri due.

```bash
git add src/components/ui/
git commit -m "feat: shared UI components"
git pull --rebase
git push origin main
```

Se `git push` ti rifiuta perché nel frattempo ha pushato un altro, rifai `git pull --rebase` e ripusha: state toccando file diversi, quindi non ci sono conflitti veri.

**Verifica**

- [ ] `Field.tsx` è in `src/components/ui/`
- [ ] `npm run check` passa
- [ ] non hai toccato `src/contracts/`
- [ ] committato e pushato

---

## Passo 2 · Il tuo strumento — la skill `/new-form`

**Cosa stai per fare:** scriverti una skill tua.

Una skill è una procedura scritta in un file: la scrivi una volta, e da lì in poi la lanci con un comando invece di rispiegare a Claude come si fa. `/new-component`, che hai appena usato, è esattamente questo — l'ha scritta qualcun altro per te.

La tua si chiama **`/new-form`** e ti serve a scrivere il form del backoffice: il pezzo più lungo della giornata, con dentro la validazione, gli errori sotto ai campi giusti, il bottone che si disabilita durante l'invio.

**La lanci una volta sola**, ma il form che ne esce lo useranno **tutte e due le tue pagine**, creazione e modifica. Il guadagno non è rilanciarla dieci volte: è che quelle sette regole le scrivi adesso, con calma, invece di rispiegarle a Claude in mezzo al codice fra un'ora. Per questo è la skill più lunga dei tre, e per questo hai un componente solo da scrivere.

**Ne scrivi una sola.** Gli altri due stanno scrivendo la loro, e ve le scambiate col `git pull` dell'allineamento.

Tre cose da fare, in ordine:

1. copia il prompt qui sotto e mandalo: Claude scrive `.claude/skills/new-form/SKILL.md` prendendo a modello `/new-component`
2. apri il file e rileggilo
3. **taglia** quello che è di troppo: più una skill è lunga, meno farà quello che credi

**Prompt:**

```
Leggi @.claude/skills/new-component/SKILL.md: è l'esempio della forma che voglio.

Scrivi .claude/skills/new-form/SKILL.md. La skill deve produrre un form che:
- è "use client", con una riga di commento che dice perché
- usa SEMPRE Field e Input, importati da @/components/ui/Field e
  @/components/ui/Input: nessun <input> o <textarea> scritto a mano, altrimenti
  resta fuori dall'identità visiva del progetto
- valida con postInputSchema di @src/contracts/blog.ts, mai con controlli scritti a mano
- mostra ogni errore dentro il Field del campo giusto, mai in cima alla pagina
- dopo la risposta del server, se è un ApiError con code "validation_error",
  legge error.fields e mette quei messaggi negli stessi Field
- disabilita il bottone durante l'invio: niente doppio invio
- funziona sia in creazione (POST) sia in modifica (PATCH), con valori iniziali opzionali

Nel description metti i trigger: nuovo form, il form di creazione, il modulo del post.
Massimo trenta righe. Procedura numerata, non descrizione.
```

### Committa e pusha

```bash
git add .claude/
git commit -m "chore: add new-form skill"
git pull --rebase
git push origin main
```

Gli altri due stanno scrivendo file diversi dentro `.claude/`, quindi anche qui nessun conflitto vero.

**Verifica**
Non serve al momento avviare questa skill. La userei dopo. Comunque verifica i seguenti punti:

- [ ] `.claude/skills/new-form/SKILL.md` esiste, ed è sotto le trenta righe
- [ ] committato e pushato

---

## Fatto

- [ ] il tuo componente è su `main`
- [ ] la tua skill è su `main`

Appena hanno pushato anche gli altri due, tutti e tre insieme: [`02-si-allinea.md`](02-si-allinea.md).
