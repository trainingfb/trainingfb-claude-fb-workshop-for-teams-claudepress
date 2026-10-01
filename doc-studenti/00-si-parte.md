> **Passo 0 · 15-20 minuti · insieme, un portatile solo**
> [indice](README.md) · prossimo → 01 · Fondamenta: [T1](01-T1-fondamenta.md) · [T2](01-T2-fondamenta.md) · [T3](01-T3-fondamenta.md)

> **Tutti e tre allo stesso tavolo, ma alla tastiera uno solo.** Questo file si fa su un portatile solo: si clona in tre soltanto all'ultimo passo.

# Si parte — chi siamo e cosa abbiamo deciso

Sei passi per mettervi d'accordo: il repo del team, chi fa cosa, il contratto, le tre decisioni che valgono per tutti. Poi ognuno si porta a casa il progetto già deciso.

**Qui non si scrive ancora codice.** Si scrive nei file dopo, uno per ruolo, e ci arrivate quando queste sei caselle sono spuntate.

> **Scegliete chi guida.** Uno dei tre apre il suo portatile, e da qui al Passo 5 si lavora solo su quello: gli altri due guardano lo schermo e dicono la loro. Non conta chi sia — conta che sia **uno solo**, o vi ritrovate un conflitto su `main` prima ancora di aver scritto una riga di codice.

---

## Passo 1 · Il repo del team

**Lo fa chi guida.** Le altre due persone guardano.

Si scarica solo il progetto, senza la documentazione del workshop, in una **cartella nuova** (non in quella clonata a casa):

```bash
npx degit trainingfb/trainingfb-claude-fb-workshop-for-teams-claudepress/repo-claudepress claudepress
cd claudepress
```

> `degit` scarica una cartella da GitHub senza la sua storia git: quello che hai adesso è solo codice, non ancora un repo.

Adesso ne fai un repo, e lo pubblichi sul tuo profilo GitHub:

> Al posto di `<NUMERO-TAVOLO>` metti il numero scritto sul foglietto del vostro tavolo, senza `< >`: per esempio `claudepress-team-3`.

> IMPORTANTE: `-b main` serve perché su alcuni computer git chiama il primo branch `master`, e al Passo 5 si pusha su `main`.


```bash
git init -b main
git add .
git commit -m "chore: start from claudepress scaffold"
gh repo create claudepress-team-<NUMERO-TAVOLO> --public --source=. --remote=origin --push
```


Poi, sempre chi guida, su GitHub: **Settings → Collaborators**, e aggiungi gli altri due.

**Verifica**

- [ ] il repo `claudepress-team-<NUMERO-TAVOLO>` è su `https://github.com/[YOUR-GITHUB-USERNAME]?tab=repositories` (sostituisci `[YOUR-GITHUB-USERNAME]` con il tuo username di GitHub)
- [ ] dentro c'è il progetto, con un solo commit
- [ ] gli altri due hanno ricevuto e accettato l'invito

---

## Passo 2 · Chi guida installa

**Solo il portatile guida.** Il progetto ce l'hai già: l'hai appena creato tu, nella cartella `claudepress`. Gli altri due non clonano ancora: lo faranno al Passo 6, quando il repo avrà già dentro le vostre decisioni.

```bash
npm install
npm run dev
```

Apri <http://localhost:3000>: vedi una pagina che dice che il sito non è ancora stato scritto. **È giusto.**

Poi, in un altro terminale:

```bash
npm run check
```

> `npm run check` lancia in sequenza il typecheck di TypeScript e ESLint, senza avviare nulla. È il controllo che rifarete prima di ogni commit: se passa adesso, su un progetto ancora vuoto, sapete che quando fallirà più tardi la colpa è del codice appena scritto e non dell'installazione.

**Verifica**

- [ ] il progetto gira su `localhost:3000`
- [ ] `npm run check` passa
- [ ] `git status` è pulito — se non lo è, fermatevi e guardate cosa è cambiato
  > Per buttare via tutte le modifiche e tornare al progetto appena scaricato: `git restore . && git clean -fd`

---

## Passo 3 · Scegliete i tre ruoli

**A voce, tutti e tre.** Nessuno tocca la tastiera: servono solo i nomi, da scrivere nel `CLAUDE.md` al Passo 5.

Ci sono tre track, di peso simile, e **nessuno dipende dagli altri due**.

| | Track | Cosa consegna | Il suo file |
|---|---|---|---|
| **T1** | Sito | home e pagina del post | [`03-T1-sito.md`](03-T1-sito.md) |
| **T2** | CMS, elenco | tabella dei post ed eliminazione | [`03-T2-cms-elenco.md`](03-T2-cms-elenco.md) |
| **T3** | CMS, form | creazione e modifica | [`03-T3-cms-form.md`](03-T3-cms-form.md) |

Come sceglierli, in due minuti e non in dieci:

- **T3** è il pezzo più lungo. Prendilo se i form non ti spaventano.
- **T2** è il più corto, e in cambio scrive lo strumento — un subagent — che alla fine serve a tutti e tre.
- **T1** è quello che si vede per primo nella demo.

Il ruolo non c'entra con chi guida adesso: chi ha creato il repo può essere T1, T2 o T3.

**Verifica**

- [ ] ognuno sa se è T1, T2 o T3

---

## Passo 4 · Guardate il contratto, insieme

Da qui in avanti tenete il progetto **aperto nell'editor** — VS Code, Cursor, WebStorm, quello che usate. Dalla cartella `claudepress` potete ad esempio aprire l'editor con

```bash
code .    #  visual studio code
webstorm . # webstorm
agy-ide .  # antigravity
```

Serve per due cose: l'albero dei file a sinistra, per vedere cosa c'è e cosa cambia (fra poco toccate il `CLAUDE.md`), e il **terminale integrato** (*Terminal → New Terminal*), da cui lanciate `claude` senza saltare da una finestra all'altra.

> Il `npm run dev` del Passo 2 lasciatelo dov'è, gira per conto suo tutto il giorno.
Oppure killate il processo (CTRL/CMD + C) e avviatelo in un terminale del vostro IDE.

Poi, in un altro terminale dell'editor avviate Claude:

```bash
claude
```

**Prompt:**

```
Leggi @src/contracts/blog.ts e spiegami in dieci righe cosa contiene:
i tipi, gli schemi zod, le rotte e le firme dei componenti.
Non scrivere codice.
```

È l'unico file che importate tutti e tre. **Adesso si può discutere**, finché siete seduti insieme. Fra mezz'ora no.

**Verifica**

- [ ] sapete che esistono `Post`, `postInputSchema`, `ApiError`, `API_ROUTES`, `ROUTES` e i `…Props`

---

## Passo 5 · Le tre decisioni, e il `CLAUDE.md`

Stesso portatile, stessa sessione `claude` del passo prima. Si decide in tre, scrive uno solo.

### a. Decidete, a voce — 3 minuti

Tre cose sono rimaste aperte apposta:

1. `content` è **testo semplice** o **markdown**?
2. In `/admin/posts` l'ordinamento è per **data di modifica** o per **titolo**?
3. Cancellare un post **chiede conferma** o no?

Non sono decisioni grosse: tre minuti, non dieci. Quello che decidete vale per tutti e tre da adesso in poi.

### b. Scrivetele nel `CLAUDE.md`

**È lì che vanno**, non su un foglio e non nella chat: è il file che Claude legge a ogni messaggio, quindi una decisione scritta lì la rispetta da sola.

Il file è già nel repo, ed è un `CLAUDE.md` normale di progetto. Ha dentro quattro **`TODO`**: sono i punti in cui deve intervenire il team. Cercateli — tre si risolvono adesso, uno alla fine della giornata.

**Soluzione - Prompt:**

```
Apri @CLAUDE.md.

Nella sezione "Decisioni di progetto" sostituisci i tre "da decidere" con:
- content: testo
- ordinamento in /admin/posts: titolo
- conferma prima di cancellare: no

Nella sezione "Skill di design" scrivi il nome della skill che useremo:

frontend-design

Nella tabella "Aree di proprietà" sostituisci i TODO della colonna
Responsabile con questi nomi:
- Sito pubblico: <NOME UTENTE 1> 
- Backoffice, elenco: <NOME UTENTE 2> 
- Backoffice, editor: <NOME UTENTE 3> 

Togli i commenti TODO delle tre sezioni che hai compilato. Lascia quello
di "Regole aggiunte dal team" e non toccare il resto del file.
```

Le tre righe fra `< >` sono le vostre decisioni: mettete quelle, non l'esempio.

> **Il quarto `TODO`, quello delle «Regole aggiunte dal team», non si tocca adesso.** Si risolve alla fine della giornata: una regola scritta prima di sbagliare è un'opinione.

### c. Committate e pushate

In un altro terminale avviare i seguenti comandi:

```bash
npm run check
git add CLAUDE.md
git commit -m "docs: team decisions and area owners"
git push origin main
```

**Verifica**

- [ ] le tre decisioni sono nel `CLAUDE.md`, al posto dei «da decidere»
- [ ] la colonna «Responsabile» ha tre nomi al posto dei `TODO`
- [ ] il `TODO` delle «Regole aggiunte dal team» è ancora lì
- [ ] su GitHub, nella pagina del repo del team, il `CLAUDE.md` è quello aggiornato

---

## Passo 6 · Adesso clonano gli altri due

**Chi guida non fa niente: ce l'ha già.** Gli altri due, ognuno sul proprio portatile, in una **cartella nuova**:

```bash
git clone <URL-DEL-REPO-DEL-TEAM> claudepress
cd claudepress
npm install
npm run dev
```

Poi, in un altro terminale:

```bash
npm run check
```

Poi aprite anche voi il progetto nell'editor (`code .` dalla cartella `claudepress`): da qui in avanti ci lavorate dentro.

> Clonate solo ora il repo (e non prima), così vi arriverà un progetto che ha già dentro le tre decisioni e i tre responsabili: nessun `git pull` di allineamento, e nessuno che parte con un `CLAUDE.md` vecchio.

**Verifica**

- [ ] tutti e tre avete il progetto che gira su `localhost:3000`
- [ ] `npm run check` passa su tutti e tre i portatili
- [ ] `git status` è pulito su tutti e tre
- [ ] aprite il `CLAUDE.md`: le tre decisioni e i tre nomi ci sono

> Se su un portatile non parte, fermatevi qui e sistematelo. Andare avanti in due e recuperare dopo non funziona mai.

---

## Come siete messi adesso

Da qui in avanti ognuno lavora con **tre terminali aperti**, tutti nella cartella `claudepress` e tutti dentro l'editor:

| | Cosa ci gira | Quanto resta aperto |
|---|---|---|
| **1** | `npm run dev` | tutto il giorno, non lo tocchi più |
| **2** | `claude` | tutto il giorno |
| **3** | i comandi a mano: `git`, `npm run check` | è quello che usi e basta |

Il terzo serve perché gli altri due sono occupati: il dev server scrive di continuo, e in quello di Claude non si digitano comandi.

---

## Fatto

- [ ] il repo del team esiste e siete tutti e tre collaboratori
- [ ] ognuno sa se è T1, T2 o T3
- [ ] avete letto il contratto insieme
- [ ] le tre decisioni e i tre responsabili sono nel `CLAUDE.md`, committati e pushati
- [ ] tutti e tre avete il progetto che gira e `npm run check` che passa
- [ ] ognuno ha i suoi tre terminali aperti

Avanti: adesso ognuno apre **il file del suo ruolo**, sul suo portatile.

| | |
|---|---|
| **T1** | [`01-T1-fondamenta.md`](01-T1-fondamenta.md) |
| **T2** | [`01-T2-fondamenta.md`](01-T2-fondamenta.md) |
| **T3** | [`01-T3-fondamenta.md`](01-T3-fondamenta.md) |

Sono ancora fondamenta comuni, quindi **restate allo stesso tavolo**: ci si ritrova tutti e tre in [`02-si-allinea.md`](02-si-allinea.md).
