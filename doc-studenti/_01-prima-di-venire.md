> **Tutto quello che c'è da fare e da sapere prima del workshop. Mezz'ora, a casa.**
> [← indice](README.md)

# Prima di venire

Questo file si legge **una volta sola, a casa**. In sala non ti servirà: lì c'è il percorso, che ti dice passo per passo cosa fare.

L'unico altro file che ti servirà è [`_02-se-qualcosa-va-storto.md`](_02-se-qualcosa-va-storto.md), e solo quando qualcosa si rompe.

> **Le basi si danno per fatte.** Qui non si spiega più cos'è una skill o un subagent: si scrivono. Se è la prima volta che ne senti parlare, guarda il materiale del workshop sulle basi prima di venire.

---

# 1. Cosa costruiamo

Un blog con il suo CMS. Il sito pubblico legge, il backoffice scrive, e i due pezzi li costruiscono persone diverse nello stesso momento.

- Una home con l'elenco dei post pubblicati.
- La pagina di un singolo post.
- Un backoffice dove si creano, si modificano e si cancellano i post.

## In tre, in tre momenti

| | |
|---|---|
| **Insieme, si parte** | le decisioni, il `CLAUDE.md`, i sei componenti condivisi, gli strumenti (skill e subagent) |
| **Ognuno il suo pezzo** | nessuno aspetta nessuno, perché le fondamenta ci sono già |
| **Insieme, si chiude** | le regole imparate, i merge, la demo |

| | Track | Cosa consegna |
|---|---|---|
| **T1** | Sito pubblico | la home e la pagina del post |
| **T2** | Backoffice, elenco | la tabella dei post e l'eliminazione |
| **T3** | Backoffice, form | creazione e modifica |

---

---

# 2. Il setup

Qui non si spiega più cos'è una regola di progetto, una skill o un subagent: si usano e si scrivono. Se è la prima volta che ne senti parlare, guarda il materiale del workshop sulle basi prima di venire — sono due ore da solo.

## Un account GitHub

**Ogni partecipante deve avere il suo account GitHub.** In sala lavorerai in un team: uno crea il repo del team, gli altri vengono aggiunti come collaboratori, e ognuno fa push e apre pull request con il proprio account. Se non ce l'hai, crealo su [github.com/signup](https://github.com/signup) prima di venire, e confermalo dalla mail.

## Cosa deve esserci sul tuo portatile

```bash
node --version        # 22 o superiore
git --version
gh --version          # GitHub CLI, serve per creare il repo del team e le PR
claude --version      # Claude Code
```

Se `gh` non è configurato: `gh auth login`, con il tuo account GitHub.

## La skill di design: scaldare il comando

Durante il workshop userete una skill esterna, `frontend-design` di Anthropic. **Non installarla adesso**: si installa dentro il progetto, e il progetto vero lo clonerete in sala.

Quello che serve fare a casa è solo assicurarsi che il comando funzioni, perché sul wifi di una conferenza scaricarlo per la prima volta è il modo migliore per perdere dieci minuti:

```bash
npx --yes skills --version
```

Deve stampare un numero di versione. La prima volta scarica qualche megabyte: è proprio quello che vogliamo togliere di mezzo stasera.

## Il progetto

```bash
npx degit trainingfb/trainingfb-claude-fb-workshop-for-teams-claudepress/repo-claudepress claudepress-workshop
cd claudepress-workshop
npm install
npm run dev
```

> Questa copia serve solo a controllare il setup. In sala chi guida ne scaricherà una nuova per creare il repo del **team**, e gli altri lo cloneranno: è lì che lavorerete tutto il giorno.

Apri <http://localhost:3000> e clicca anche su **Backoffice**: su tutte e due vedi una pagina che dice che quel pezzo non è ancora stato scritto, e quale prompt provare. **È giusto così**: sono i segnaposto che sostituirai tu. Quello che c'è e quello che non c'è è spiegato più sotto, in «Cosa trovi nel repo».

Poi:

```bash
npm run check
```

Deve passare. Se non passa sul progetto appena scaricato, scrivilo in chat prima del workshop: è un problema mio, non tuo.

## La checklist del setup

**Verifica**

- [ ] un account GitHub tuo, confermato
- [ ] Node 22+, `git`, `gh` autenticato, Claude Code
- [ ] `npx --yes skills --version` stampa un numero
- [ ] progetto scaricato, `npm install` fatto, `npm run dev` che parte
- [ ] `npm run check` che passa

Fatto questo, restano da leggere le due sezioni qui sotto — dieci minuti — e domani non perdi tempo.

---

# Cosa trovi nel repo

```
claudepress/
├── CLAUDE.md                          🔨 le regole + quattro TODO da compilare
│
├── .claude/
│   ├── skills/
│   │   ├── new-component/             ✅ la usate e la copiate: è il modello
│   │   ├── commit/                    ✅ /commit — check, messaggio, commit
│   │   └── pr/                        ✅ /pr — push e pull request in draft
│   └── agents/                        ⬜ vuota — ci va smoke-test
│
├── src/
│   ├── contracts/blog.ts              🔒 il contratto — si legge, non si tocca
│   ├── data/posts.seed.json           🔒 sei post: tre pubblicati, tre bozze
│   ├── server/                        🔒 store in memoria, slug, errori HTTP
│   │
│   ├── app/
│   │   ├── layout.tsx · globals.css   🔨 minimi, li sistemate insieme
│   │   ├── page.tsx                   ⬜ segnaposto — T1
│   │   ├── posts/                     ⬜ vuota — T1
│   │   ├── admin/
│   │   │   ├── page.tsx               ✅ redirect, già scritto — area di T2
│   │   │   └── posts/
│   │   │       ├── page.tsx           ⬜ segnaposto — T2
│   │   │       └── new/page.tsx       ⬜ segnaposto — T3
│   │   └── api/posts/                 ✅ tutte le API, già scritte
│   │
│   └── components/ui/                 ⬜ vuota — sei componenti, li scrivete insieme
```

| | |
|---|---|
| ✅ | c'è, funziona, ti serve |
| 🔒 | c'è e **non si tocca** |
| 🔨 | c'è ma è minimo: lo sistemate insieme |
| ⬜ | lo scrivi tu. Dove c'è già un file, è un segnaposto da sostituire |

**Chi possiede cosa** è scritto nel `CLAUDE.md` del progetto, tabella «Aree di proprietà». All'inizio ci scriverete i vostri nomi.

> Le istruzioni del workshop **non stanno dentro il progetto**: sono questo materiale, a parte. Il repo su cui lavori è un progetto vero e va letto come tale — compreso il blocco in inglese in cima al `CLAUDE.md`, che scrive Next da solo a ogni `npm run dev` e che non va toccato.

## Le tre cose che non si toccano, e perché

**`src/contracts/blog.ts`** — tipi, schemi zod, rotte, firme dei componenti. È l'unico file che importate tutti e tre. Si discute all'inizio, finché siete seduti insieme; da lì in poi è congelato.

**`src/app/api/posts/**`** — tutte e sette le rotte, già scritte, con validazione e la forma `ApiError` su ogni errore, 404 compresi. Oggi siete tre frontender: scrivere endpoint non è il punto della giornata.

**`src/server/`** — lo store in memoria. **Non c'è un database, ed è una scelta**: zero setup, zero credenziali, zero rete, e i dati di ognuno sono i suoi. Riavvii il dev server e i post tornano quelli del seed: è giusto così.

## Le API in trenta secondi

Con `npm run dev` attivo, da un altro terminale:

```bash
# com'è fatto un post
curl -s localhost:3000/api/posts/po-001

# tutti: sei, tre bozze e tre pubblicati
curl -s localhost:3000/api/posts \
  | grep -oE '"id":"[^"]*"|"slug":"[^"]*"|"status":"[a-z]*"' | paste - - -

# la forma dell'errore
curl -s localhost:3000/api/posts/non-esiste
```

Fallo prima di scrivere la prima pagina: cinque minuti guadagnati. L'elenco completo delle rotte è nel `README.md` del progetto, i tipi in `src/contracts/blog.ts`.

## I comandi

```bash
npm run dev          # dev server su :3000
npm run check        # typecheck + lint  ← prima di ogni commit
npm run build
```

---

# Il perimetro

## Cosa non si fa, nemmeno se avanza tempo

Login e utenti · upload di immagini · editor rich text · ricerca · paginazione · commenti · categorie e tag · pubblicazione programmata · SEO e metadati · anteprima della bozza · **database**.

Questa lista è la sezione più utile del documento: è quella che, quando siete a metà e vi sentite bravi, vi impedisce di mettervi a fare la ricerca full-text invece di finire quello che avete promesso.

## Le tre cose ancora da decidere

Non le ha decise nessuno apposta. **Le decidete voi all'inizio**, insieme, e finiscono nel `CLAUDE.md`:

1. `content` è **testo semplice** o **markdown**? Cambia come lo rende T1.
2. In `/admin/posts` l'ordinamento è per **data di modifica** o per **titolo**?
3. Cancellare un post **chiede conferma**, o si cancella e basta?

## La demo, in una frase

> Creo un post nel backoffice, lo vedo comparire in home, lo apro.

Se un lavoro non serve a questa frase, oggi non si fa.
