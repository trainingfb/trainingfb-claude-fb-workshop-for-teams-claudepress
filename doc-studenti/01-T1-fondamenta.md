> **Passo 1 · T1 · 10-20 minuti · allo stesso tavolo**
> ← [00 · Si parte](00-si-parte.md) · [indice](README.md) · prossimo → [02 · Ci si allinea](02-si-allinea.md)

> **Ognuno sul suo portatile, ma restate allo stesso tavolo: è ancora lavoro di squadra.**

# T1 · Le fondamenta

Due cose, in quest'ordine: **i tuoi tre componenti**, poi **il tuo strumento**, la skill `/new-page`. Quando li hai pushati tutti e due, ci si rivede in [`02-si-allinea.md`](02-si-allinea.md).

> **Intanto:** T2 scrive `StatusBadge` e `Button` più il subagent `smoke-test`, T3 scrive `Field` più la skill `/new-form`. Nessuno dei due tocca i tuoi file.

Obiettivo: **quando comincerete a lavorare da soli, non dovrà mancare niente a nessuno.**

> Se sei in ritardo, sfora sui componenti: un componente brutto si sistema dopo, uno strumento che non hai scritto non lo userai mai.

---

## Passo 1 · I tuoi componenti

Sono tre, uno in più degli altri: T3 ne ha uno solo perché scrive la skill più lunga dei tre.

| Componente | Chi lo userà |
|---|---|
| `PostCard.tsx` | tu |
| `EmptyState.tsx` | tu e T2 |
| `Input.tsx` | **solo T3** |

Guarda la terza riga: **`Input` lo scrivi tu, e non lo userai mai.** È la dimostrazione più pulita del perché esiste il contratto — scrivi contro una firma per qualcun altro, e al merge si incastra.

`Input` sta qui e non dentro il form di T3 per un motivo pratico: **la skill di design che lanciate all'allineamento passa solo su `src/components/ui/`.** Se i campi di testo stessero nel form, sarebbero l'unica cosa dell'applicazione a restare grezza — proprio nella schermata da cui parte la demo.

Nel repo ci sono già tre skill pronte: **`/new-component`**, che fa esattamente questo, più **`/commit`** e **`/pr`** che userete tutto il giorno. Aprile adesso, sono tre minuti — `/new-component` ti serve anche come modello al passo 2.

**Soluzione / Prompt** — comincia dal primo:

```
/new-component PostCard
```

La skill va a leggere `PostCardProps` nel contratto, scrive il file, e lancia `npm run check` da sola. Se ti dice che una firma non esiste, **non inventarla**: il contratto è quello.

Le due regole: **le firme sono quelle del contratto**, e i componenti **ricevono props e rendono markup** — niente fetch, niente logica di dominio.

Apri il file che è uscito e guardalo: è la forma che devono avere anche gli altri due.

Adesso **fai la stessa cosa per gli altri due**, uno alla volta — è la stessa skill, cambia solo il nome.

**Soluzione / Prompt:**

```
/new-component EmptyState
```

```
/new-component Input
```

> IMPORTANTE: conferma l'utilizzo di 'use client' se richiesto


Le loro firme sono `EmptyStateProps` e `InputProps`, nello stesso contratto. Se una delle due non ti torna, rileggi `src/contracts/blog.ts` invece di aggiustare il componente.

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

- [ ] `PostCard.tsx`, `EmptyState.tsx` e `Input.tsx` sono in `src/components/ui/`
- [ ] `npm run check` passa
- [ ] non hai toccato `src/contracts/`
- [ ] committato e pushato

---

## Passo 2 · Il tuo strumento — la skill `/new-page`

**Cosa stai per fare:** scriverti una skill tua.

Una skill è una procedura scritta in un file: la scrivi una volta, e da lì in poi la lanci con un comando invece di rispiegare a Claude come si fa. `/new-component`, che hai appena usato tre volte, è esattamente questo — l'ha scritta qualcun altro per te.

La tua si chiama **`/new-page`** e ti serve a scrivere una pagina del sito pubblico che **carica dati da un'API**: nel repo quelle pagine esistono già, ma sono segnaposto vuoti, e tocca a te riempirle.

**La userai due volte oggi**: per la home e per la pagina del singolo post. Sono i due pezzi più lunghi del tuo pomeriggio, e la seconda volta ti costa un prompt di una riga — è lì che si ripaga il quarto d'ora che ci metti adesso.

> La terza pagina che scriverai, quella del «post non esiste», **non** la farai con la skill: non carica niente, e una skill usata dove non serve è solo un giro più lungo.

**Ne scrivi una sola, non tre.** Gli altri due stanno scrivendo la loro, e ve le scambiate col `git pull` dell'allineamento.

Tre cose da fare, in ordine:

1. copia il prompt qui sotto e mandalo: Claude scrive `.claude/skills/new-page/SKILL.md` prendendo a modello `/new-component`
2. apri il file e rileggilo
3. **taglia** quello che è di troppo: più una skill è lunga, meno farà quello che credi

**Prompt:**

```
Leggi @.claude/skills/new-component/SKILL.md: è l'esempio della forma che voglio.

Scrivi .claude/skills/new-page/SKILL.md. La skill deve produrre una pagina del
sito pubblico che:
- è un server component, senza "use client"
- carica i dati con fetch(apiUrl(API_ROUTES.x), { cache: "no-store" }), tutto
  da @src/contracts/blog.ts: mai un path relativo, mai un URL scritto a mano
- gestisce tre casi: dati presenti, elenco vuoto con EmptyState, fetch fallita
- se la risorsa non esiste chiama notFound(), non ritorna null

Nel description metti i trigger: nuova pagina, crea la home, la pagina del post.
Massimo trenta righe. Procedura numerata, non descrizione.
```

### Committa e pusha

```bash
git add .claude/
git commit -m "chore: add new-page skill"
git pull --rebase
git push origin main
```

Gli altri due stanno scrivendo file diversi dentro `.claude/`, quindi anche qui nessun conflitto vero.

**Verifica**

- [ ] `.claude/skills/new-page/SKILL.md` esiste, ed è sotto le trenta righe
- [ ] committato e pushato

---

## Fatto

- [ ] i tuoi tre componenti sono su `main`
- [ ] la tua skill è su `main`

Appena hanno pushato anche gli altri due, tutti e tre insieme: [`02-si-allinea.md`](02-si-allinea.md).
