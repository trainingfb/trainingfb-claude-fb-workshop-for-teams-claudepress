> **Passo 2 · 10-20 minuti · insieme**
> ← 01 · Fondamenta: [T1](01-T1-fondamenta.md) · [T2](01-T2-fondamenta.md) · [T3](01-T3-fondamenta.md) · [indice](README.md) · prossimo → 03 · [T1 Sito](03-T1-sito.md) · [T2 Elenco](03-T2-cms-elenco.md) · [T3 Form](03-T3-cms-form.md)

> **Stop. Si ritorna tutti e tre allo stesso tavolo, e poi ci si divide per davvero.**

# Ci si allinea — lo stile, e il controllo prima di dividersi

Tre passi: prendete il lavoro degli altri due, date un'identità visiva ai sei componenti, e controllate che non manchi niente a nessuno.

| | Chi | Cosa |
|---|---|---|
| **1** | tutti e tre | il `git pull` con dentro il lavoro degli altri |
| **2** | uno solo | la vetrina dei sei componenti, e la skill di design |
| **3** | tutti e tre | il controllo che siate allineati |

**Si comincia quando hanno pushato tutti e tre**, componenti e strumento. Se qualcuno è indietro, aspettatelo: da qui in poi si va avanti insieme.

---

## Passo 1 · Prendete il lavoro degli altri due (TUTTI SUI LORO PC)

Tutti e tre, ognuno sul suo portatile:

```bash
git pull
npm run check
```

Adesso in `src/components/ui/` ci sono **tutti e sei** i componenti, non solo i vostri, e in `.claude/` ci sono i tre strumenti che vi siete scritti: due skill e un subagent.

**Verifica**

- [ ] i sei file esistono in `src/components/ui/` su tutti e tre i portatili
- [ ] `npm run check` passa
- [ ] nessuno ha toccato `src/contracts/`

---

## Passo 2 · La skill di design (SOLO UN MEMBRO DEL TEAM)

Da qui in poi fatelo su un portatile solo, con gli altri due che guardano: sono sei file, ci vogliono due minuti.

Qui usate una skill che **non avete scritto voi**: è un mestiere che non è il vostro, e non ha senso passare dieci minuti a metterlo per iscritto.

> Tre frontender, due ore, nessun designer. Il risultato funziona ed è brutto. Non perché siete scarsi: il gusto visivo non è una procedura che ripetete, è un mestiere.

### a. La vetrina: guardate i componenti prima dello stile

Finora i sei componenti non li ha visti nessuno: nessuna pagina li usa ancora, e sul sito ci sono solo i segnaposto. Prima di dargli uno stile, fateveli mostrare tutti in una pagina sola: così fra cinque minuti vedete anche **cosa cambia**, non solo il diff.

**Prompt:**

```
Crea src/app/vetrina/page.tsx: una pagina di prova che mostra i sei
componenti di src/components/ui/, uno sotto l'altro, ognuno con un
titoletto con il suo nome.
- È un client component ("use client", con il commento che dice perché):
  Input vuole onChange e Button onClick, che una pagina server non può passare.
- Dati finti scritti nella pagina, nessuna fetch.
- PostCard: due card con dati inventati.
- StatusBadge: uno published e uno draft.
- Button: le tre varianti, più uno disabled.
- Field con dentro Input: uno normale, uno multiline, uno con errore.
- EmptyState: con e senza description.
Usa i componenti così come sono, con i props del contratto. Non modificarli.
```

Aprite <http://localhost:3000/vetrina>, e guardatela bene: è il **prima**.

> La vetrina è nell'area **condivisa** del `CLAUDE.md`, come i componenti: resta nel progetto fino alla demo, e da qui in poi si congela con loro.

**Committatela subito**, da sola:

```bash
npm run check
git add src/app/vetrina/
git commit -m "chore: add UI showcase page"
git pull --rebase
git push origin main
```

Va committata adesso, prima di installare la skill: al punto d controllerete che la skill abbia toccato solo i componenti, e una vetrina non committata sarebbe una riga in più da spiegare.

### b. Installatela — **una persona sola**

Dalla radice del progetto, cioè dentro `claudepress/` (nel terminale, non dentro Claude Code):

```bash
npx skills add anthropics/skills@frontend-design -y
```

È la skill `frontend-design` di Anthropic: serve a produrre interfacce con un'identità, invece del solito grigio-con-bordino che esce di default. Il `-y` evita la domanda «per quali agent la installo?»: la mette in un posto solo e la collega a Claude Code.

Compaiono tre cose nel repo:

```
.claude/skills/frontend-design      la skill per Claude Code
.agents/skills/frontend-design/     skill universale (per altri agent)
skills-lock.json                    versione e hash, come un package-lock
```

**Non è un'installazione globale: è dentro il progetto.** Per questo la fa una persona sola: agli altri due arriva con un `git pull`, senza installarla ognuno per conto suo.

Poi **fatela vedere alla sessione di Claude Code che hai già aperta**: una sessione avviata prima dell'installazione non sa che la skill esiste.

```
/reload-skills
```

Rilegge le skill dal disco senza chiudere niente. In alternativa esci e rilancia `claude`, che fa lo stesso ma ti fa ripartire da capo.

**Committa e pusha adesso, prima di lanciarla:**

```bash
git add -A
git commit -m "chore: add frontend-design skill"
git pull --rebase
git push origin main
```

Due commit separati e non uno solo, per un motivo pratico: fra due minuti dovrete leggere il diff di quello che la skill ha cambiato. Se l'installazione è già committata, in quel diff restano **solo** i vostri componenti — altrimenti ci trovate dentro anche `.agents/`, il symlink e `skills-lock.json`, e il controllo diventa illeggibile.

### c. Lanciatela — la stessa persona, su tutti e sei i componenti



Prima controlla che ci sia davvero:

```
/skills
```

Elenca le skill disponibili: `frontend-design` deve comparire. Se non c'è, non hai fatto `/reload-skills` — rifallo adesso, perché il prompt qui sotto la chiama per nome e senza di lei Claude improvvisa.

Se la lanciate in tre, ognuno sui suoi, uscite da qui con **tre linguaggi visivi** nella stessa app. Per questo il `git pull` del passo 1 viene prima: la skill deve vedere i sei componenti tutti insieme.

**Prompt:**

```
Usa la skill frontend-design su src/components/ui/, src/app/layout.tsx e
src/app/globals.css.
Dai a ClaudePress un'identità visiva coerente: tipografia, colori, spaziature.
Non cambiare i nomi dei props: sono definiti nel contratto.
Non toccare nessun altro file.
```

### d. Guardate il diff in tre

Una skill esterna è brava e **non conosce il vostro contratto**: può rinominare props, spostare file, riscrivere cose che non sono sue. Questo è l'unico momento della giornata in cui vale la pena leggere un diff riga per riga — e visto che avete committato i componenti prima, avete un punto a cui tornare.

**1. Quali file ha toccato**

```bash
git status --short
```

Vi aspettate solo roba dentro `src/components/ui/`, `src/app/layout.tsx` e `src/app/globals.css` — la vetrina e i file dell'installazione non ci sono più, li avete committati ai punti a e b. **Qualsiasi altra riga è un problema**, e si risolve al punto 4.

**2. Quanto ha cambiato**

```bash
git diff --stat
```

> Esci dalla modalità `diff` premendo `Q`

Una riga per file, con quante righe dentro e fuori. Serve a farsi un'idea in tre secondi: cinquanta righe cambiate in `PostCard.tsx` sono plausibili, trecento no.

**3. Il diff vero, un file alla volta**

```bash
git diff src/components/ui/PostCard.tsx
```

Si scorre con le frecce, si esce con `q`. 

**Cosa state cercando**, in ordine di gravità:

- **un prop rinominato** — `title` diventato `heading`, `href` diventato `link`. È il danno peggiore perché rompe il codice che scriverete fra dieci minuti
- **un componente nuovo** che non è nel contratto, o un file spostato
- **un import di una libreria** che non c'è in `package.json`
- **testi in inglese** al posto di quelli in italiano

**4. Se ha toccato qualcosa che non doveva**

Si butta quel file e basta, senza discutere:

```bash
git restore src/app/page.tsx        # torna com'era
```

**Caso diverso: il file vi piace, ma dentro ha rinominato un prop.** Qui non si butta niente — `git restore` vi riporterebbe indietro anche tutto lo stile. Correggete a mano il nome, e tenete il resto:

```tsx
// il contratto dice title, la skill ha scritto heading
export function PostCard({ heading, href }: PostCardProps)   // ✗
export function PostCard({ title, href }: PostCardProps)     // ✓ rimesso a mano
```

Sono due secondi, e vi tenete il lavoro buono: colori, spaziature e tipografia restano quelli che ha scritto lei.

**5. Il controllo automatico**

```bash
npm run check
```

Questo è il vostro paracadute: i componenti sono tipizzati con i `…Props` del contratto, quindi **se ha rinominato un prop il typecheck esplode qui**. Se `check` passa e il diff è pulito, avete finito.

**6. Ricaricate la vetrina**

Riaprite <http://localhost:3000/vetrina>: è lo stesso codice di prima, con l'identità visiva nuova. Questo è il **dopo**. Se un componente è rotto o illeggibile lo vedete qui, adesso, e non fra un'ora dentro una pagina vera.

### Poi committa — sempre la stessa persona

```bash
git add -A
git commit -m "style: visual identity for shared components"
git pull --rebase
git push origin main
```

E gli altri due: `git pull`.

**Verifica**

- [ ] il diff tocca solo `src/components/ui/`, `src/app/layout.tsx` e `src/app/globals.css`
- [ ] i props sono ancora quelli di `blog.ts`
- [ ] `npm run check` passa
- [ ] `/vetrina` mostra i sei componenti, con lo stile nuovo

---

## Passo 3 · L'allineamento, e poi ci si divide (TUTTI)

Avete committato lungo la strada, un pezzo alla volta. Adesso il controllo finale, **tutti e tre**:

```bash
git pull
git status          # deve essere pulito
npm run check       # deve passare
git log --oneline -10
```

Nel log dovete vedere gli stessi commit su tutti e tre i portatili: il `CLAUDE.md`, i tre commit dei componenti, i tre degli strumenti, la vetrina, l'installazione della skill di design e lo stile. Nove in tutto.

Poi **riavviate Claude Code**, tutti e tre: le skill e il subagent degli altri sono arrivati con il `git pull`, e una sessione aperta prima non li vede.

**Verifica**

- [ ] `git status` è pulito su tutti e tre
- [ ] `npm run check` passa su tutti e tre
- [ ] `git log` mostra le stesse righe su tutti e tre
- [ ] Claude Code riavviato, e `/new-page`, `/new-form` e il subagent `smoke-test` ci sono su tutti e tre


---

# IN CASO DI PROBLEMI

Se a qualcuno manca un commit si sistema adesso, in dieci secondi. Se lo scoprite fra un'ora, avrà scritto una pagina contro un componente che non esiste.

### Se il `git log` non torna

Sul portatile a cui manca qualcosa, prima capite **di cosa si tratta**:

```bash
git status -sb
```

La prima riga dice tutto, e i casi sono tre:

**1. `## main...origin/main [ahead 1]` — hai committato ma non pushato.** È il caso più comune: il tuo lavoro ce l'hai solo tu.

```bash
git pull --rebase
git push origin main
```

**2. `## main...origin/main [behind 2]` — ti mancano i commit degli altri.**

```bash
git pull
```

**3. Sotto la prima riga compaiono file (`M`, `??`) — non hai proprio committato.**

```bash
git add -A
git commit -m "feat: shared UI components"    # o il messaggio giusto per quello che hai fatto
git pull --rebase
git push origin main
```

Poi **gli altri due rifanno `git pull`**, e tutti e tre ricontrollate:

```bash
git log --oneline -10
npm run check
```

> Se il `git pull --rebase` si ferma dicendo *CONFLICT*, non improvvisate in tre voci: fermatevi, guardate insieme quale file è, e tenete la versione di chi quel file lo possiede secondo la tabella «Aree di proprietà» del `CLAUDE.md`.

---

## Da adesso

Quello che avete costruito è **congelato**: contratto, componenti, layout, `CLAUDE.md`. Se lavorando da solo ti serve cambiarne uno, **non farlo**: annotatelo, e se ne parla quando vi rimettete insieme.

E ricordate il perimetro, perché è adesso che si comincia a sforare:

> Niente login, upload di immagini, editor rich text, ricerca, paginazione, commenti, categorie, SEO, database. **Nemmeno se avanza tempo.**

La misura di oggi è una frase sola:

> Creo un post nel backoffice, lo vedo comparire in home, lo apro.

Ognuno apre il suo file e va avanti da solo:

| | |
|---|---|
| **T1** | [`03-T1-sito.md`](03-T1-sito.md) |
| **T2** | [`03-T2-cms-elenco.md`](03-T2-cms-elenco.md) |
| **T3** | [`03-T3-cms-form.md`](03-T3-cms-form.md) |

Ci si rivede in [`04-si-chiude.md`](04-si-chiude.md).
