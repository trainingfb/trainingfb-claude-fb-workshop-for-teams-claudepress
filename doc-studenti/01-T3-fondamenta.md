> **Passo 1 · T3 · 10-20 minuti · allo stesso tavolo**
> ← [00 · Si parte](00-si-parte.md) · [indice](README.md) · prossimo → [02 · Ci si allinea](02-si-allinea.md)

> **Ognuno sul suo  portatile, ma restate allo stesso tavolo: è ancora lavoro di squadra.**

# T3 · Le fondamenta

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

> `git pull --rebase` scarica quello che hanno pushato gli altri e rimette il tuo commit in cima: la storia resta lineare, senza commit «Merge branch…».

Se `git push` ti rifiuta perché nel frattempo ha pushato un altro, rifai `git pull --rebase` e ripusha: state toccando file diversi, quindi non ci sono conflitti veri.

**Verifica**

- [ ] `Field.tsx` è in `src/components/ui/`
- [ ] `npm run check` passa
- [ ] non hai toccato `src/contracts/`
- [ ] committato e pushato

---

## Passo 2 · Il tuo strumento — la skill `/new-form`

**Cosa stai per fare:** scriverti una skill tua.

> **Qui scrivi solo la skill, non il form.** `Input` e `Button` ancora non li hai, e non ti servono: la skill li nomina e basta. Il form lo scrivi in [`03-T3-cms-form.md`](03-T3-cms-form.md), quando ti saranno arrivati con il `git pull`.

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
- usa SEMPRE Field, Input e Button, importati da @/components/ui/Field,
  @/components/ui/Input e @/components/ui/Button: nessun <input>, <textarea> o
  <button> scritto a mano, altrimenti resta fuori dall'identità visiva del progetto
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


---

# AIUTA I TUOI COLLEGHI

Se hai finito prima degli altri, dai una mano ai tuoi colleghi