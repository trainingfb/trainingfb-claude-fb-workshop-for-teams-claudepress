> **Passo 3 · T2 · 15-20 minuti · da solo**
> ← [02 · Ci si allinea](02-si-allinea.md) · [indice](README.md) · prossimo → [04 · Si chiude](04-si-chiude.md)

> **Da qui lavori da solo. Leggi solo questo file: gli altri due sono di altre persone.**

# T2 · CMS, l'elenco

Consegni la tabella dei post del backoffice e l'eliminazione.

> **Intanto:** T1 costruisce il sito pubblico, T3 il form. Il link *Modifica* della tua tabella porta a una pagina di T3: mettilo lo stesso, anche se per ora dà 404.

---

## Passo 1 · Il tuo branch

Nel terminale:

```bash
git checkout main && git pull
git checkout -b t2/cms-elenco
```

---

## Passo 2 · Guarda cosa ti torna l'API

**Com'è fatto un post** — i nomi dei campi sono quelli del tipo `Post` del contratto:

```bash
curl -s localhost:3000/api/posts/po-001
```

Dovrebbe restituirti un JSON con la struttura dei post.

**Cosa ti torna la rotta della tua tabella**, slug e stato di ognuno:

```bash
curl -s localhost:3000/api/posts | grep -oE '"id":"[^"]*"|"slug":"[^"]*"|"status":"[a-z]*"' | paste - - -
```

```
"id":"po-006"   "slug":"scrivere-una-skill-che-usi-davvero"        "status":"draft"
"id":"po-005"   "slug":"il-contratto-prima-del-codice"             "status":"published"
"id":"po-004"   "slug":"una-regola-si-scrive-dopo-aver-sbagliato"  "status":"draft"
"id":"po-003"   "slug":"niente-database-e-una-scelta"              "status":"published"
"id":"po-002"   "slug":"chi-possiede-quale-file"                   "status":"draft"
"id":"po-001"   "slug":"benvenuti-su-claudepress"                  "status":"published"
```

**Verifica**

- [ ] sei post, tre `draft` e tre `published`

L'`id` è quello che ti serve: il link *Modifica* va a `ROUTES.adminPost(id)` e l'eliminazione chiama `API_ROUTES.post(id)`.

Qui arrivano **tutti** i post, bozze comprese: è giusto, la tua tabella le deve mostrare. La home di T1 chiama la stessa rotta con `?status=published` e ne vede tre.

---

## Passo 3 · La tabella

Crea la pagina del CMS per la tabella (l'elenco) dei post

**Prompt:**

```
Leggi @src/contracts/blog.ts.
Scrivi src/app/admin/posts/page.tsx: server component, carica
apiUrl(API_ROUTES.posts) con cache "no-store", e rende una tabella con titolo,
autore, data, StatusBadge, un link Modifica verso ROUTES.adminPost(id) e un
bottone Elimina. In cima alla tabella un link "Nuovo post" verso
ROUTES.adminPostNew.
Ordina per data di modifica.
Se non ci sono post usa EmptyState. Tutti i testi in italiano.
```

> Se ti viene comunicata un'incoerenza sull'ordinamento e Claude ti fa una domanda, prendi tu una decisione.

Apri <http://localhost:3000/admin/posts>. Apri anche <http://localhost:3000/admin>: ti porta a `/admin/posts`. Quel redirect è già scritto in `src/app/admin/page.tsx`, ed è nella tua area.

**Verifica manuale**

- [ ] vedi tutti e sei i post del seed
- [ ] le bozze hanno un badge diverso dai pubblicati
- [ ] c'è il link *Nuovo post* — per ora dà il segnaposto di T3
- [ ] `/admin` porta a `/admin/posts`

Su terminale

```bash
npm run check
```

In Claude Code:
```bash
/commit
```

---

## Passo 4 · Apri la PR — adesso, non alla fine

La tabella si vede: basta così per aprirla, l'eliminazione la aggiungi dopo.

**Cos'è una pull request.** È una richiesta di portare il tuo branch dentro `main`: una pagina su GitHub che mostra cosa hai cambiato e dove gli altri due possono guardare e commentare. **Aprirla non mergia niente** — il merge è un momento separato, e oggi lo farete insieme alla fine.

**Perché adesso e non quando hai finito.** Una PR in *draft* è il modo più economico di far vedere agli altri dove sei arrivato. Se hai preso una strada sbagliata, lo scopri adesso invece che alle cinque.

### 1. Controlla di aver committato

Nel terminale:

```bash
git status
```

Deve essere pulito. Se no, `/commit` — anche quella è già nel repo — e poi riprova.

### 2. Manda il branch su GitHub e apri la PR

In Claude Code:

```bash
/pr
```

È una delle skill che trovi già nel repo: controlla che `npm run check` passi, fa il push e apre la PR in draft, con titolo e descrizione scritti leggendo il tuo diff.

Se preferisci farla a mano invece di usare la skill `/pr`, questi sono i comandi:

```bash
git push -u origin t2/cms-elenco
gh pr create --draft --title "<titolo>" --body "<due righe su cosa fa>"
```

### 3. Apri il link che ti stampa

Sulla pagina della PR, la scheda **Files changed** mostra tutto quello che hai toccato. Guardala una volta: **ci sono solo file tuoi?** Se compare roba di un altro track o dell'area condivisa, fermati e dillo, prima che diventi un problema di tutti.

### 4. Da qui in poi non serve riaprirla

Ogni commit che pushi su questo branch finisce **nella stessa PR**, da solo:

```bash
/commit
git push
```

> *Draft* vuol dire «non è finita, non mergiatela». Lo faremo dopo.

**Verifica manuale**

- [ ] la PR è aperta, in draft
- [ ] in **Files changed** ci sono solo file tuoi

---

## Passo 5 · L'eliminazione di un post

Devi effettuare questo step solo se non vedi un pulsante ELIMINA nell'area admin.
Se invece è presente e ti permette di eliminare un post, allora non serve farlo

È l'unico pezzo interattivo che hai, quindi isolalo: **la pagina resta server**, il bottone diventa client.
(è una dinamica di NextJS. Non preoccuparti se non è chiaro)

NOTA: questo step potrebbe esser già stato effettuato in automatico dallo step #3.
Quindi verifica prima che il pulsante ELIMINA funzioni e in tal caso non serve che metti in pratica questo step.


**Prompt:**

```
Scrivi src/app/admin/posts/_list/DeletePostButton.tsx, un client component con una riga
di commento che dice perché è client.
Riceve l'id del post, chiama DELETE su API_ROUTES.post(id), e a risposta ok aggiorna l'elenco con router.refresh().
Durante la chiamata il bottone resta disabilitato.
Usa Button con variant "danger".
Poi usalo in ogni riga della tabella in page.tsx.
```

Se il team ha deciso che la cancellazione chiede conferma, aggiungilo — **senza `window.confirm`**, che blocca tutto.

**Verifica manuale**

- [ ] cancello un post e sparisce **senza ricaricare la pagina a mano**
- [ ] cliccando due volte in fretta non parte due volte

```bash
npm run check
/commit
```

---

## Passo 6 · Il controllo prima di chiudere

Lancia il tuo subagent. Serve il dev server attivo.

**Prompt:**

```
Usa il subagent smoke-test
```

> Le tue rotte devono rispondere 200. `/posts/<slug>` e `/admin/posts/<id>` invece daranno ancora **404**: sono le pagine di T1 e T3, stanno sui loro branch e arrivano su `main` solo con i merge di [`04-si-chiude.md`](04-si-chiude.md). Tutte a 200 le vedrete lì.

Poi, a mano:

**Verifica**

- [ ] l'elenco mostra bozze e pubblicati, distinguibili con `StatusBadge`
- [ ] l'ordinamento è quello deciso insieme, non un altro
- [ ] *Modifica* porta a `/admin/posts/<id>` anche se T3 non ha finito
- [ ] `npm run check` passa
- [ ] hai toccato solo `src/app/admin/page.tsx`, `src/app/admin/posts/page.tsx` e `src/app/admin/posts/_list/`

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

# Bonus

## Passo 7 · I bonus, se ti avanza tempo

Sei probabilmente quello che finisce prima, quindi questi te li ho pensati apposta. 
Prendine **uno alla volta**, e committa fra uno e l'altro.

### Una PR sola, o due?

**I bonus vanno sullo stesso branch e nella stessa PR.** La tua prima PR non è ancora mergiata: un secondo branch partirebbe da un `main` che non contiene il tuo lavoro, e la seconda PR mostrerebbe due volte le stesse cose. È la trappola classica di chi apre PR a catena.

Quindi, per ogni bonus:

Nel terminale

In Claude Code:

```bash
/commit
```

```bash
git push
```

e finisce nella PR che hai già aperto.

I merge si fanno tutti insieme alla fine, in [`04-si-chiude.md`](04-si-chiude.md): fino ad allora il tuo lavoro sta tutto lì dentro.

### Bonus 1 · Pubblica e riporta in bozza

Il pezzo che manca davvero: dalla tabella, cambiare stato senza aprire il form (che è compito di T3 e non ancora pronto).

**Soluzione / Prompt:**

```
Scrivi src/app/admin/posts/_list/StatusToggle.tsx, un client component con una
riga di commento che dice perché è client.

Riceve id e status del post. Mostra un bottone: "Pubblica" se lo stato è draft,
"Riporta in bozza" se è published.
Al click fa PATCH su API_ROUTES.post(id) mandando solo { status: <il nuovo> },
poi router.refresh().
Durante la chiamata resta disabilitato.
Usa Button con variant "secondary". Poi usalo in ogni riga della tabella.
```

**Verifica manuale**

- [ ] pubblico una bozza dalla tabella e il badge cambia
- [ ] quello stesso post compare in `curl -s "localhost:3000/api/posts?status=published"` — è la rotta della home di T1, che vedrai dopo il merge
- [ ] lo riporto in bozza e da quel `curl` sparisce

Ricordati di committare con `/commit`

### Bonus 2 · Il filtro per stato

Tre link in cima alla tabella — *Tutti · Bozze · Pubblicati* — che filtrano.

**Soluzione / Prompt:**

```
In src/app/admin/posts/page.tsx leggi il searchParam "status".
Se vale draft o published, filtra l'elenco; altrimenti mostrali tutti.
Aggiungi in cima tre Link: Tutti (/admin/posts), Bozze (?status=draft),
Pubblicati (?status=published), con quello attivo evidenziato.
La pagina resta un server component.
```

Ricordati di committare con `/commit`


### Bonus 3 · Il riepilogo in testa

Una riga sopra la tabella coni totali: «6 post — 3 pubblicati, 3 bozze». 

**Prompt**

INVENTALO TU : )


### Bonus 4 · Ordina per titolo

Rendi cliccabile l'intestazione della colonna *Titolo*: al click aggiunge `?sort=title`, e la pagina si riordina. Sempre `searchParam`, sempre server component.


**Prompt**

INVENTALO TU : )

---

## Fine

Ricordati di committare `/commit` e pushare `git push`


Hai finito il tuo track. Ci si rivede tutti e tre in [`04-si-chiude.md`](04-si-chiude.md): le regole, i merge e la demo.
