> **Passo 3 · T3 · 15-20 minuti · da solo**
> ← [02 · Ci si allinea](02-si-allinea.md) · [indice](../README.md) · prossimo → [04 · Si chiude](04-si-chiude.md)

> **Da qui lavori da solo. Leggi solo questo file: gli altri due sono di altre persone.**

# T3 · CMS, il form

Consegni la creazione e la modifica dei post. È il pezzo più lungo della giornata.

**Non partire dalle pagine: parti dal form.** Le due pagine, dopo, sono dieci minuti in tutto.

> **Intanto:** T1 costruisce il sito pubblico, T2 la tabella del CMS. Il link *Modifica* della sua tabella punta alla tua pagina `/admin/posts/[id]`: finché non la scrivi dà 404, ed è normale.

---

## Passo 1 · Il tuo branch

Nel terminale:

```bash
git checkout main && git pull
git checkout -b t3/cms-form
```

---

## Passo 2 · Guarda cosa rifiuta l'API

Manda apposta un titolo troppo corto:

```bash
curl -s -X POST localhost:3000/api/posts -H 'content-type: application/json' -d '{"title":"ab","excerpt":"","content":"x","author":"io","status":"draft"}'
```

Guarda la risposta: dentro `error.fields` c'è la mappa **campo → messaggio**. È quella che userai per mettere gli errori sotto ai campi giusti.

**Verifica**

- [ ] hai visto la forma di `ApiError` con `fields`

---

## Passo 3 · Il form

Il pezzo grosso. Lo scrivi una volta sola e serve a tutte e due le pagine.

**Prompt** — usa `/new-form`, la skill che hai scritto tu nelle [fondamenta](01-T3-fondamenta.md):

```
/new-form Scrivi src/app/admin/posts/new/page.tsx: server component, titolo "Nuovo post",
e crea un componente src/app/admin/_components/PostForm.tsx.
Il form ha i seguenti campi:
titolo, sommario, contenuto (multiline), autore, stato.
Usa Field e Input, importati da @/components/ui/Field e @/components/ui/Input,
per tutti i campi di testo.
Per lo stato usa due Button, "Bozza" e "Pubblicato", con quello attivo evidenziato:
sono due soli valori, non serve un select.
Riceve valori iniziali opzionali e un id opzionale: senza id fa POST su
API_ROUTES.posts, con id fa PATCH su API_ROUTES.post(id).
A salvataggio riuscito porta a ROUTES.adminPosts.
Tutte le etichette e i messaggi in italiano.
```

---

## Passo 4 · Provalo subito

Apri <http://localhost:3000/admin/posts/new> e prova questi tre casi:

**Verifica manuale**

- [ ] salvo con il titolo di due caratteri → l'errore compare **sotto al campo titolo**, non in cima
- [ ] salvo con tutto giusto → il post viene creato e finisco su `/admin/posts`
- [ ] clicco *Salva* due volte in fretta → **non** si creano due post

Se l'errore compare in cima alla pagina invece che sotto al campo, è il momento di sistemare la skill `/new-form`: la userai ancora.

### Il post c'è davvero?

A schermo sei finito su `/admin/posts`, ma quell'elenco è un segnaposto: lo sta scrivendo T2 e sul tuo branch non mostra ancora niente. Quindi il tuo post vallo a vedere **dove vive davvero**, nei dati:

```bash
curl -s localhost:3000/api/posts | grep -oE '"id":"[^"]*"|"title":"[^"]*"|"status":"[a-z]*"' | paste - - -
```

L'API torna i post **dal più recente**, quindi il tuo è la **prima riga**: il titolo e lo stato sono quelli che hai scritto tu, l'`id` l'ha generato il server.

**Verifica manuale**

- [ ] la prima riga ha il titolo che hai appena inserito
- [ ] lo `status` è quello che hai scelto, `draft` o `published`
- [ ] l'`id` non l'hai scritto tu: lo assegna il server

> Se a schermo il post «si crea» ma qui non compare, il form non sta chiamando l'API: sta solo aggiornando lo stato di React. È l'errore più difficile da vedere a occhio, e il più facile da vedere con questo `curl`.

Su terminale:

```bash
npm run check
```

In Claude Code:

```bash
/commit
```
---

## Passo 5 · Apri la PR — adesso, non alla fine

Il form salva: basta così per aprirla, la pagina di modifica la aggiungi dopo.

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

A mano, se preferisci vedere i comandi:

```bash
git push -u origin t3/cms-form
gh pr create --draft --title "<titolo>" --body "<due righe su cosa fa>"
```

### 3. Apri il link che ti stampa

Sulla pagina della PR, la scheda **Files changed** mostra tutto quello che hai toccato. Guardala una volta: **ci sono solo file tuoi?** Se compare roba di un altro track o dell'area condivisa, fermati e dillo, prima che diventi un problema di tutti.

### 4. Da qui in poi non serve riaprirla

Ogni commit che pushi su questo branch finisce **nella stessa PR**, da solo:

In Claude Code:

```bash
/commit
```

Su terminale:

```bash
git push
```


> *Draft* vuol dire «non è finita, non mergiatela». Quando il tuo pezzo è a posto la sposti in *Ready for review* con il bottone sulla pagina — oppure lo dici e basta, tanto i merge li fate insieme, tutti allo stesso schermo.

**Verifica manuale**

- [ ] la PR è aperta, in draft
- [ ] in **Files changed** ci sono solo file tuoi

---

## Passo 6 · La pagina di modifica

Questa è la pagina che si aprirà quando si clicca su Modifica della lista.
La lista non è ancora visibile perché la sta creando un tuo collega.

**Prompt:**

```
Scrivi src/app/admin/posts/[id]/page.tsx: server component, carica il post con
apiUrl(API_ROUTES.post(id)) e cache "no-store", e passa i valori a PostForm
insieme all'id. Se l'API risponde 404, chiama notFound().
```

**Verifica manuale**

- [ ] apro <http://localhost:3000/admin/posts/po-001> e il form è **precompilato** — il link *Modifica* nella tabella di T2 lo vedrai dopo il merge
- [ ] cambio il titolo, salvo, e `curl -s localhost:3000/api/posts/po-001` mostra il titolo nuovo

Su Terminale:

```bash
npm run check
```

In Claude Code:

```bash
/commit
```

---

## Passo 7 · Il controllo prima di chiudere

Lancia il subagent che ha scritto T2: dopo il `git pull` delle fondamenta ce l'avete tutti e tre. Serve il dev server attivo.

**Prompt:**

```
Usa il subagent smoke-test
```

Poi, a mano:

**Verifica**

- [ ] creo un post `published` e compare in `curl -s "localhost:3000/api/posts?status=published"`: è la rotta della home di T1
- [ ] creo un post `draft` e in quel `curl` **non** compare
- [ ] modifico un titolo e `curl -s localhost:3000/api/posts/<id>` lo mostra: è quello che leggerà l'elenco di T2
- [ ] titolo di due caratteri → errore sotto al campo titolo
- [ ] doppio clic su *Salva* → nessun doppione
- [ ] `npm run check` passa
- [ ] hai toccato solo `src/app/admin/posts/new/`, `[id]/` e `_components/`

La home di T1 e la tabella di T2 le vedrai con il tuo form dentro solo dopo il merge, in [`04-si-chiude.md`](04-si-chiude.md): sul tuo branch sono ancora segnaposto, ed è normale.

Hai il pezzo più lungo: se arrivi qui in tempo, hai già vinto. Se ti avanza, i bonus sono qui sotto.

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

Sono tutti **dentro `PostForm.tsx`** o nelle tue due pagine: non tocchi il contratto, i componenti condivisi né la tabella di T2.

Prendine **uno alla volta**, e committa fra uno e l'altro.

### Una PR sola, o due?

**I bonus vanno sullo stesso branch e nella stessa PR.** La tua prima PR non è ancora mergiata: un secondo branch partirebbe da un `main` che non contiene il tuo lavoro, e la seconda PR mostrerebbe due volte le stesse cose. È la trappola classica di chi apre PR a catena.

Quindi, per ogni bonus:

```bash
/commit
git push
```

e finisce nella PR che hai già aperto.

I merge si fanno tutti insieme alla fine, in [`04-si-chiude.md`](04-si-chiude.md): fino ad allora il tuo lavoro sta tutto lì dentro.

### Bonus 1 · Il contatore dei caratteri

Il contratto dà al sommario un massimo di 200 caratteri. Dirlo dopo aver salvato è tardi.

**Prompt:**

```
In src/app/admin/_components/PostForm.tsx aggiungi sotto al campo sommario un
contatore "128 / 200".
Diventa rosso quando si supera il limite, e in quel caso il bottone di salvataggio
è disabilitato.
Il 200 non scriverlo a mano: prendilo da postInputSchema di @src/contracts/blog.ts.
```

L'ultima riga è il punto: **il limite vive nel contratto**, e se un giorno cambia lì, il contatore si aggiorna da solo.

**Verifica manuale**

- [ ] scrivo nel sommario e il contatore sale
- [ ] supero i 200 → diventa rosso e non posso salvare
- [ ] torno sotto → posso salvare di nuovo

### Bonus 2 · «Hai modifiche non salvate»

Se chiudi la pagina con il form sporco, perdi tutto e non te lo dice nessuno.


**Prompt:**

```
In PostForm.tsx tieni traccia di se il form è stato modificato rispetto ai valori
iniziali. Se lo è, avvisa prima che l'utente lasci la pagina.
Dopo un salvataggio riuscito l'avviso non deve più comparire.
```

**Verifica**

Apri un form che contiene dei dati (ad es. http://localhost:3000/admin/posts/po-001) e fai una modifica ad un testo.
Prima di salvare prova a refreshare la pagina o a cliccare sui pulsanti del browser BACK o FORWARD.
Sarai avvisato con un alert.


### Bonus 3 · L'anteprima

Accanto al form, una colonna che mostra come verrà il post: titolo, autore, e il testo. Si aggiorna mentre scrivi. Su schermo stretto va sotto invece che a fianco.

È il bonus che si vede meglio in demo, ed è anche il più lungo: prendilo solo se sei davvero in anticipo.

**Prompt**

INVENTALO TU

### Bonus 4 · Salva da tastiera

`Cmd+S` su Mac, `Ctrl+S` su Windows, salvano il form invece di aprire il salvataggio del browser. Tre righe, e chi scrive molto te ne è grato.


**Prompt**

INVENTALO TU

---

## Fine
Ricordati di committare `/commit` e pushare `git push`

Hai finito il tuo track, che era il più lungo. Ci si rivede tutti e tre in [`04-si-chiude.md`](04-si-chiude.md): le regole, i merge e la demo.
