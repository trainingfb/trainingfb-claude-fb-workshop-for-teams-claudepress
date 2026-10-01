> **Di nuovo tutti e tre insieme, su un portatile solo, sullo schermo grande.**

# Si chiude — insieme

Un portatile solo sullo schermo grande, gli altri due a portata di mano. 
**Alla tastiera va chi se la sente**, e meglio se non è chi ha guidato stamattina in [`00-si-parte.md`](00-si-parte.md): nell'arco della giornata la tastiera passa di mano, e chi guida impara più in fretta degli altri due.

> Non serve che sia una persona in particolare: le skill e il subagent `smoke-test` ce li avete tutti e tre da stamattina, arrivati con il `git pull` dell'allineamento, e al repo del team siete tutti collaboratori. Chi guida lancia i comandi perché ha la tastiera, non perché possiede qualcosa.

---

## Passo 1 · Le regole che avete imparato

Ognuno dice la sua, e ne ha una: quella che ha corretto a mano più di una volta, oppure il vincolo che si è ritrovato a ripetere in ogni prompt. **Se lo ripeti ogni volta, non è un'istruzione: è una regola**, e il posto delle regole è il `CLAUDE.md`.

Prima, sul portatile guida, mettetevi su `main`: le regole vanno lì, non sul branch di chi ha la tastiera, altrimenti finiscono dentro la sua PR invece che nel progetto.

```bash
git checkout main && git pull
```

Poi aprite il `CLAUDE.md`, sezione *«Regole aggiunte dal team»*, e scrivetele adesso. Una riga ciascuna, **specifica**.

Così:

```md
Le pagine del sito fanno fetch con `cache: "no-store"`. Senza, un post creato nel backoffice non compare in home e sembra un bug delle API.
```

Non così:

```md
Attenzione alla cache.
```

La differenza è che la prima si può seguire e la seconda no.

E si committa subito, su `main`:

```bash
git add CLAUDE.md
git commit -m "docs: team rules"
git push origin main
```

**Verifica**

- [ ] almeno una regola scritta, nata da un errore vero
- [ ] committata su `main`, non su un branch

> Se la sezione è ancora vuota, non insistete con la domanda: **riaprite i prompt di oggi** e cercate una frase che compare in più di uno — «testi in italiano», `cache: "no-store"`, «le rotte da `API_ROUTES`», «usa `Field` e `Input`». Quelle frasi sono regole travestite da istruzioni: le avete ripetute a mano tutto il giorno perché non erano scritte dove Claude le legge da solo.

---

## Passo 2 · L'ultima skill, e la scrivete adesso

La domanda del passo prima aveva anche un'altra risposta, e questa ce l'avete tutti e tre uguale: **cosa avete fatto a mano, con le dita, più volte oggi?**

```bash
npm run check
git add …
git commit -m "…"
git push
```

Quattro, cinque, otto volte a testa. E non è una regola: una regola è una cosa che Claude deve **sapere**, questa è una cosa che Claude può **fare**. Roba che rifate uguale ogni volta, con dei passi in ordine: è la definizione di skill.

> Metà del lavoro ce l'avete già: `/commit` lancia il check, si ferma se fallisce e scrive il messaggio leggendo il diff. Quello che avete ripetuto a mano ogni volta è il `git push` subito dopo — ed è anche quello che qualcuno si è dimenticato, visto che a fine track è servito un `git status -sb` per scoprirlo.

Sul portatile guida, sempre su `main`, creare una skill con il seguente prompt:

**Prompt:**

```
Leggi @.claude/skills/commit/SKILL.md: è l'esempio della forma che voglio, e
fa già metà del lavoro.

Scrivi .claude/skills/ship/SKILL.md, la skill che porta il lavoro finito da
locale a remoto in un colpo:
1. lancia npm run check e SI FERMA se fallisce, riportando l'errore com'è
2. guarda git status --short e git diff, e committa con un messaggio
   conventional commit scritto leggendo il diff
3. fa git push sul branch corrente
4. chiude dicendo il messaggio usato e su quale branch ha pushato

Se il push viene rifiutato non forzare: riporta l'errore e fermati.
Nel description metti i trigger: manda su, pusha il lavoro, chiudi il pezzo.
Massimo trenta righe. Procedura numerata, non descrizione.
```

Poi fatela vedere alla sessione:

```
/reload-skills
```

**E provatela subito sul primo lavoro che avete a portata di mano: sé stessa.**

```
/ship
```

Se funziona, avete appena committato e pushato la skill **usando la skill**. Se si ferma al check, si è fermata dove doveva.

Se vi chiede su quale branch committarlo, rispondete su `main`.


**Verifica**

- [ ] `.claude/skills/ship/SKILL.md` esiste, sotto le trenta righe
- [ ] compare in `/skills`
- [ ] l'avete usata almeno una volta, e il commit è su `main`

> Siete in ritardo? **Saltate ai merge e tornate qui dopo la demo.** Questa è l'unica parte della chiusura che si può rimandare senza perdere niente: il codice è già tutto nelle PR.

---

## Passo 3 · I merge, una PR alla volta

Per ogni PR, prima di mergiare, guardate **quali file tocca** — non il diff riga per riga. I branch degli altri due non sono su questo portatile, quindi si chiede a GitHub:

```bash
gh pr list  # i numeri delle tre PR. Premi `Q` per uscire.
gh pr diff <numero> --name-only
```

Poi:

1. confrontate i path con la tabella «Aree di proprietà» del `CLAUDE.md`
2. se compare qualcosa dell'area condivisa — `src/contracts/`, `src/components/ui/`, `CLAUDE.md` — o di un altro track, **si sistema adesso**, davanti a tutti

### Come si sistema

Quasi sempre è un file salvato per sbaglio, e si rimette com'era. Lo fa **chi ha aperto quella PR, sul suo portatile**: il branch è solo lì.

```bash
git checkout <il-tuo-branch>
git fetch origin
git checkout origin/main -- <il file>     # ricopia QUEL file dalla versione di main
npm run check
/commit
git push
```

L'ultimo comando non cambia branch, nonostante il nome: il `--` vuol dire «prendi da `origin/main` solo questo file e mettilo qui». Tu resti sul tuo branch e tutto il resto del tuo lavoro non viene toccato.

Adesso quel file sul tuo branch è identico a quello di `main`, e siccome una PR mostra solo le differenze rispetto a `main`, **sparisce dalla PR**: rifate `gh pr diff <numero> --name-only` e quel path non c'è più.

L'unica eccezione è se quella modifica **serve davvero** — senza, il suo codice non gira. Allora si tiene, la si legge a voce, e quella PR si mergia per prima. **Nel dubbio, rimettete il file com'era.**

### Come si mergia

Le PR sono in **draft**, e una draft non si mergia: prima va segnata pronta.

```bash
gh pr ready 1                               # la toglie da draft
gh pr merge 1 --squash --delete-branch      # mergia e cancella il branch
```

Dal browser è la stessa cosa: *Ready for review* → *Squash and merge* → *Delete branch*.

- **`--squash`** mette tutto il lavoro di quel branch in **un commit solo** su `main`. La storia resta leggibile: tre commit, uno per persona, invece di quaranta.
- **`--delete-branch`** cancella il branch su GitHub. Quello locale resta: lo cancellate dopo, o mai, non cambia niente.

Ripetete questo processo per le altre due PR rimanenti.

Chiunque dei tre può mergiare: siete tutti collaborator del repo del team.

### Se GitHub dice che una PR ha conflitti

Non dovrebbe succedere: le tre aree sono disgiunte, e GitHub mergia da solo una PR dopo l'altra. Se succede, è quasi sempre un file dell'area condivisa che qualcuno ha toccato e non doveva — e lo avete già visto con `gh pr diff`.

Il conflitto si risolve **adesso**, in tre davanti allo stesso schermo: è il momento migliore della giornata per farlo. Poi GitHub si accorge da solo che la PR è mergiabile, e si ricomincia con quella successiva.

Chi ha aperto quella PR riapre il suo portatile e porta dentro `main`:

```bash
git checkout main && git pull
git checkout <il-tuo-branch>
git merge main
```

**Qui `git merge` si ferma** e ti elenca i file in conflitto. Apriteli: dentro trovate i due pezzi marcati con `<<<<<<<`, `=======` e `>>>>>>>`. Tenete quello giusto, togliete i marcatori, salvate. Se non siete sicuri di quale sia quello giusto, vale la regola di sempre: **è di chi possiede il file** secondo la tabella «Aree di proprietà».

Se non sapete come fare potete chiedere direttamente a Claude Code di risolvere i conflitti.

Poi si chiude il merge e si pusha:

```bash
npm run check
git status                  # deve elencare solo i file del conflitto
git add -A
git commit --no-edit        # chiude il merge, con il messaggio che git ha già preparato
git push
```

Due comandi che sembrano di troppo e non lo sono: **`git status`** perché `git add -A` prende tutto quello che trova, e vuoi sapere cosa sta prendendo; **`--no-edit`** perché senza si apre l'editor dei messaggi, che su un portatile appena configurato è `vim`, e sono tre minuti persi a cercare come si esce.

> Se invece `git merge main` **non** si ferma, git ha già fatto tutto da solo: il commit di merge c'è già, e ti basta `npm run check` e `git push`.


**Verifica**

- [ ] tre PR mergiate
- [ ] `grep -rn "TODO(" src/` non trova più niente: i segnaposto sono stati tutti sostituiti

---

## Passo 4 · La prova su `main`

```bash
git checkout main && git pull
npm run check
npm run build
npm run dev          # in un altro terminale: resta attivo
```

Poi, con il dev server attivo, il subagent `smoke-test` su tutto il progetto mergiato:

**Prompt:**

```
Usa il subagent smoke-test
```

**Verifica**

- [ ] `check` passa
- [ ] `build` passa
- [ ] **tutte le rotte rispondono 200** — comprese `/posts/<slug>` e `/admin/posts/po-001`, che stamattina non rispondevano
- [ ] dalla tabella clicco *Modifica* e il form è precompilato — è la prima volta che i pezzi di T2 e T3 si incontrano
- [ ] creo un post dal backoffice e compare in home — T3 e T1

Questa è la riga che dice che avete finito. Se una rotta è rossa, lo scoprite adesso e non durante la demo.

Se `build` si rompe qui e non si rompeva sui branch, è quasi sempre un import di un file che non è stato mergiato: guardate l'errore, non tirate a indovinare.

---

## Passo 5 · La demo

Si fa **sul portatile guida**: è l'unico su cui gira il progetto intero, appena mergiato e pullato. Sugli altri due c'è ancora solo il proprio pezzo. Chi parla non conta — conta che tutti e tre vedano il proprio lavoro dentro quello degli altri.

Serve il dev server attivo e il browser sullo schermo grande. Il giro è questo, in quest'ordine.

### Il sito — `localhost:3000`

| Cosa fai | Cosa dimostra |
|---|---|
| apri la **home** | l'elenco dei post pubblicati, con `PostCard` |
| **clicchi un titolo** | la pagina del post: contenuto, autore, data |
| scrivi a mano `/posts/non-esiste` | la pagina «non esiste», non un errore di Next |

### Il backoffice — `/admin/posts`

| Cosa fai | Cosa dimostra |
|---|---|
| apri la **tabella** | tutti i post, bozze comprese, con lo `StatusBadge` |
| **Nuovo post** → compili → salvi come *pubblicato* | il form valida, salva, e ti riporta in tabella |
| torni in **home** | **il post appena creato c'è.** È il primo giro completo: backoffice → API → sito |
| **Nuovo post** → salvi come **bozza** | in tabella c'è, **in home no** |
| **Modifica** su un post | il form si apre **già compilato** — il link è di T2, la pagina è di T3, e fino a mezz'ora fa dava 404 |
| cambi il titolo, salvi | la tabella mostra il titolo nuovo |
| **Elimina** | la riga sparisce |

La frase da dire ad alta voce, mentre lo fate, è sempre quella:

> Creo un post nel backoffice, lo vedo comparire in home, lo apro.
>
> Lo creo come bozza, e in home non compare.

Due minuti in tutto. Se una schermata è rossa non improvvisate una scusa: ditelo, e dite in quale delle tre aree sta — tanto lo `smoke-test` del passo prima l'ha già scritto.
