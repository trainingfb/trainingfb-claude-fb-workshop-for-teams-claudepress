> **Da qui lavori da solo. Leggi solo questo file: gli altri due sono di altre persone.**

DURATA: 15-20 MINUTI

# T1 · Il sito

Consegni la home e la pagina del post: è quello che si vede per primo nella demo.

> **Intanto:** T2 costruisce la tabella del CMS, T3 il form di creazione e modifica. Nessuno dei due tocca i tuoi file, e tu non tocchi i loro.

---

## Passo 1 · Il tuo branch

```bash
git checkout main && git pull
git checkout -b t1/sito
```

---

## Passo 2 · Guarda cosa ti torna l'API

Prima di scrivere la prima riga, un minuto che te ne fa risparmiare dieci.

**Com'è fatto un post** — i nomi dei campi sono quelli del tipo `Post` del contratto:

Avvia in un terminale questo comando e guarda la risposta:

```bash
curl -s localhost:3000/api/posts/po-001
```

**Quanti e di che tipo** te ne torna la rotta che userai in home:

```bash
curl -s "localhost:3000/api/posts?status=published" \ | grep -oE '"id":"[^"]*"|"slug":"[^"]*"|"status":"[a-z]*"' | paste - - -
```

```
"id":"po-005"   "slug":"il-contratto-prima-del-codice"   "status":"published"
"id":"po-003"   "slug":"niente-database-e-una-scelta"    "status":"published"
"id":"po-001"   "slug":"benvenuti-su-claudepress"        "status":"published"
```

**Verifica**

- [ ] tre righe, tutte `published`

Lo `slug` è quello che userai negli URL (`ROUTES.post(slug)`), l'`id` non ti serve: è roba del backoffice.

Le bozze non compaiono: **è il filtro che fa l'API**, non lo devi fare tu. Se togli `?status=published` ne tornano sei.

---

## Passo 3 · La home

**Prompt** — usa `/new-page`, la skill che hai scritto tu nelle [fondamenta](01-T1-fondamenta.md):

```
/new-page la home del blog in src/app/page.tsx: elenco dei post pubblicati,
dal più recente, ognuno con PostCard che linka a ROUTES.post(slug).
Se non ce ne sono, EmptyState con un messaggio in italiano.
```

Poi apri <http://localhost:3000> e guarda.

**Verifica manuale**

- [ ] vedi i tre post pubblicati del seed
- [ ] **non** vedi le bozze
- [ ] cliccando un post vai su `/posts/<slug>` — per ora è 404, la scrivi al passo dopo

Se la home è vuota o mostra le bozze, controlla che la fetch punti a `API_ROUTES.publishedPosts`, passi da `apiUrl()` e abbia `cache: "no-store"`.

Lancia su terminale: 

```bash
npm run check
```

E committa. Puoi usare la skill `/commit` che trovi nella cartella `.claude`
```bash
/commit
```


---

## Passo 4 · Apri la PR — adesso, non alla fine

La home funziona: basta così per aprirla, il resto lo aggiungi dopo.

**Cos'è una pull request.** È una richiesta di portare il tuo branch dentro `main`: una pagina su GitHub che mostra cosa hai cambiato e dove gli altri due possono guardare e commentare. **Aprirla non mergia niente** — il merge è un momento separato, e oggi lo farete insieme alla fine.

**Perché adesso e non quando hai finito.** Una PR in *draft* è il modo più economico di far vedere agli altri dove sei arrivato. Se hai preso una strada sbagliata, lo scopri adesso invece che alle cinque.

### 1. Controlla di aver committato

Su un terminale:

```bash
git status
```

Deve essere pulito. Se no, `/commit` — anche quella è già nel repo — e poi riprova.

### 2. Manda il branch su GitHub e apri la PR

Su claude code:

```bash
/pr
```

È una delle skill che trovi già nel repo: controlla che `npm run check` passi, fa il push e apre la PR in draft, con titolo e descrizione scritti leggendo il tuo diff.

A mano, se preferisci vedere i comandi:

```bash
git push -u origin t1/sito
gh pr create --draft --title "<titolo>" --body "<due righe su cosa fa>"
```

### 3. Apri il link che ti stampa

Nel terminale dovresti vedere il link alla PR. Aprilo.
Sulla pagina della PR, la scheda **Files changed** mostra tutto quello che hai toccato. Guardala una volta: **ci sono solo file tuoi?** Se compare roba di un altro track o dell'area condivisa, fermati e dillo, prima che diventi un problema di tutti.

### 4. Da qui in poi non serve riaprirla

Ogni commit che pushi su questo branch finisce **nella stessa PR**, da solo:

```bash
/commit
git push
```

> *Draft* vuol dire «non è finita, non mergiatela». Quando il tuo pezzo è a posto la sposti in *Ready for review* con il bottone sulla pagina — oppure lo dici e basta, tanto i merge li fate insieme, tutti allo stesso schermo.

**Verifica manuale**

- [ ] la PR è aperta, in draft
- [ ] in **Files changed** ci sono solo file tuoi

---

## Passo 5 · La pagina del post

**Prompt:**

```
/new-page il dettaglio in src/app/posts/[slug]/page.tsx: carica il post con
API_ROUTES.postBySlug(slug) e mostra titolo, autore, data e contenuto.
Se l'API risponde 404, chiama notFound().
```

**Verifica manuale**

- [ ] apri un post dalla home e lo leggi. Ad es. http://localhost:3000/posts/il-contratto-prima-del-codice

Su terminale:

```bash
npm run check
```


In claude:

```bash
/commit
```

---

## Passo 6 · La pagina "non esiste"

**Prompt:**

```
Scrivi src/app/posts/[slug]/not-found.tsx: un messaggio in italiano che dice
che il post non esiste, e un link alla home. Usa EmptyState.
```

**Apri nel browser:**

```
http://localhost:3000/posts/non-esiste
```

**Verifica manuale**

- [ ] vedi la tua pagina, non una pagina bianca né l'errore di Next


Su terminale:

```bash
npm run check
```


In claude:

```bash
/commit
```

---

## Passo 7 · Il controllo prima di chiudere

Lancia il subagent che ha scritto T2: dopo il `git pull` delle fondamenta ce l'avete tutti e tre. Serve il dev server attivo.

**Prompt:**

In claude code:

```
Usa il subagent smoke-test
```

Poi, a mano:

**Verifica**

- [ ] la home elenca solo i `published`, dal più recente
- [ ] le bozze non si vedono da nessuna parte nel sito
- [ ] uno slug inesistente dà la tua 404
- [ ] `npm run check` passa
- [ ] hai toccato solo `src/app/page.tsx` e `src/app/posts/**`

Se hai finito e gli altri due no, **non stare fermo e non andare ad aiutare dentro i loro file**: prendi un bonus qui sotto.

### Prima di alzarti dal tuo track

Il tuo lavoro deve essere **su GitHub**, non solo sul tuo portatile: fra poco si mergia dalle PR, e quello che è rimasto qui non entra da nessuna parte.

```bash
git status -sb
```

Se la prima riga dice `[ahead …]`, hai commit non pushati:

```bash
git push
```

Se invece elenca dei file, committa prima con `/commit` e poi pusha.

**La PR resta in draft, e resta una sola.** Non mergiarla adesso e non aprirne una seconda: i merge si fanno tutti insieme in [`04-si-chiude.md`](04-si-chiude.md), dove la si segna pronta con `gh pr ready`. Se hai altro da aggiungere, anche dopo la pausa, va nello stesso branch: `/commit` e `git push`, e finisce da solo nella PR che hai già aperto.

**Verifica**

- [ ] `git status -sb` non dice `ahead` e non elenca file
- [ ] sulla pagina della PR, in *Commits*, c'è il tuo ultimo commit
- [ ] la PR è ancora in **draft**

---

## Passo 8 · I bonus, se ti avanza tempo

Prendine **uno alla volta**, e committa fra uno e l'altro: se suona la fine, quello che hai finito è già dentro.

### Una PR sola, o due?

**I bonus vanno sullo stesso branch e nella stessa PR.** La tua prima PR non è ancora mergiata: un secondo branch partirebbe da un `main` che non contiene il tuo lavoro, e la seconda PR mostrerebbe due volte le stesse cose. È la trappola classica di chi apre PR a catena.

Quindi, per ogni bonus:

In claude Code:

```bash
/commit
```

Su Terminale:

```bash
git push
```


e finisce nella PR che hai già aperto.

I merge si fanno tutti insieme alla fine, in [`04-si-chiude.md`](04-si-chiude.md): fino ad allora il tuo lavoro sta tutto lì dentro.

### Bonus 1 · Una pagina contatti

Una rotta nuova, `/contatti`, con un form che **non chiama nessuna API**: alla conferma mostra un messaggio e basta. È il modo più veloce di aggiungere una pagina vera senza dipendere da niente.

**Prompt:**

```
Crea src/app/contatti/page.tsx e src/app/contatti/ContactForm.tsx.

La pagina è un server component con titolo e una riga di introduzione.
Il form è "use client", con una riga di commento che dice perché, e ha tre
campi: nome, email, messaggio.

Alla conferma NON chiama nessuna API: valida i campi lato client e, se sono
validi, nasconde il form e mostra al suo posto un messaggio di conferma in
italiano. Se non lo sono, mostra l'errore sotto al campo sbagliato.

Usa Field, Input e Button, importati da @/components/ui/Field, @/components/ui/Input
e @/components/ui/Button. Testi in italiano, Tailwind.
```

#### Aggiungi un messaggio di conferma

Un messaggio nella pagina e non un `alert()`: l'alert blocca tutto, non si può stilare, e in demo si vede male.

Poi aggiungi il link **dalla tua home**, in fondo — non dal `layout.tsx`, che è condiviso e congelato.

**Prompt**

```
Inserisci un pulsante "Scrivici" nella home page, in fondo, che porta alla pagina /contatti.
```

**Verifica manuale**

- [ ] `/contatti` si apre e il form si compila
- [ ] mando vuoto → vedo gli errori sotto ai campi
- [ ] mando compilato → il form sparisce e compare la conferma
- [ ] dalla home ci arrivo con un click

### Bonus 2 · La data in italiano

`12 marzo 2026` invece di `2026-03-12T08:00:00.000Z`. Tocca solo le tue due pagine.

**Prompt:**

```
Scrivi src/app/posts/formatDate.ts: una funzione che prende una stringa ISO e
torna la data in italiano, per esempio "12 marzo 2026". Usa Intl.DateTimeFormat
con locale it-IT, niente librerie.
Poi usala nella home e nella pagina del post.
```

### Bonus 3 · Il tempo di lettura

«3 minuti di lettura» sotto al titolo del post: parole diviso 200, arrotondato per eccesso, minimo 1. Sta tutto dentro `src/app/posts/[slug]/page.tsx`.

### Bonus 4 · Gli stati di caricamento

Un `loading.tsx` per la home e uno per la pagina del post, con uno scheletro grigio al posto del contenuto. Su localhost si vedono per un istante, ma sono due file di tre righe e in demo fanno la differenza fra «funziona» e «è finito».

---

## Fine

Ricordati di committare `/commit` e pushare `git push`


Hai finito il tuo track. Ci si rivede tutti e tre in [`04-si-chiude.md`](04-si-chiude.md): le regole, i merge e la demo.
