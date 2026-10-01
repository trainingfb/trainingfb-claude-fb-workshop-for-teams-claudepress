<!--
Slide per il blocco "Il cantiere" — 7 minuti, all'inizio della fase 1. Separatore: `---`. Funziona con Marp, Slidev e reveal.js. I commenti HTML sono note per chi parla. Versione lunga: 08-TEACHER-regole-skill-agenti.md -->

# Il cantiere

Quaranta minuti in tre,<br>prima che qualcuno scriva una pagina.

---

## La prima versione aveva un capo

Uno teneva il contratto e i componenti.
Gli altri due lavoravano contro un `TODO`.

**Quel ruolo era un collo di bottiglia.**

<!-- E si scopriva al merge se avevi indovinato. -->

---

## Tre fasi

| | | |
|---|---|---|
| **1 · il cantiere** | 40′ | **insieme** |
| **2 · il tuo pezzo** | 45′ | da soli |
| **3 · rimettere insieme** | 20′ | **insieme** |

Quando parte la fase 2, **non manca niente a nessuno.**

<!-- Il costo è onesto: 40 minuti su 120 non sono la tua feature. Si recuperano nella fase 2, perché nessuno si ferma. -->

---

## Quaranta minuti, quattro cose

| | |
|---|---|
| **10′** | le tre decisioni · il `CLAUDE.md` |
| **15′** | i sei componenti, tre-due-uno |
| **10′** | il proprio strumento |
| **5′** | ci si allinea · la skill di design |

---

## Quattro posti dove mettere la conoscenza

| | Quando | Cosa costa |
|---|---|---|
| **Regola** | vale sempre, non la invochi | il contesto, a **ogni** messaggio |
| **Skill** | una procedura che rifai uguale | solo quando la usi |
| **Subagent** | un lavoro che deleghi | contesto suo, non sporca il tuo |
| **Skill esterna** | un mestiere che non è il tuo | niente: è già scritta |

<!-- Non è "Claude Code ha quattro feature". È che sbagliare posto si paga. -->

---

## Il posto sbagliato si paga

Mettere tutto nel `CLAUDE.md` funziona **per due settimane.**

Poi il file è lungo trecento righe, nessuno lo legge,
e Claude ne ignora metà.

<!-- Chiedere: chi ha un CLAUDE.md più lungo di una schermata? Di solito si alzano le mani. -->

---

## Il test, quattro domande

**Se lo dimentica se non glielo ripeto ogni volta?** → regola

**Lo rifaccio identico tre volte oggi?** → skill mia

**Mi riempirebbe il contesto di roba che non voglio leggere?** → subagent

**È un mestiere che non è il mio?** → skill esterna, e non la scrivo

---

## Uno strumento a testa

Non tre a testa. Tre × tre = novanta minuti su centoventi.

| | Strumento | Volte che lo usi oggi |
|---|---|---|
| **T1** | skill `/new-page` | 2: home e dettaglio |
| **T3** | skill `/new-form` | 1, il pezzo più lungo |
| **T2** | subagent `smoke-test` | 4, da tutti e tre |

**Il criterio è se ti ripaga entro oggi: in tempo, o in errori che non fai.**

<!-- Il subagent è del T2 perché è il track più corto: così i carichi si pareggiano. E serve a tutti e tre.
     Sul caso di T3, se qualcuno lo nota: la lancia una volta sola, e si ripaga lo stesso perché gli fa
     scrivere le sette regole del form prima e con calma, invece che a pezzi in mezzo al codice. -->

---

## Le due righe che fanno il subagent

```md
---
tools: Bash, Read, Grep
---

Rispondi in massimo dieci righe, in questa forma:
  VERDETTO: mergiabile | da sistemare | bloccato
```

`tools:` senza strumenti di scrittura. E il **formato di risposta imposto.**

Un subagent che risponde con tre paragrafi non vi fa risparmiare niente.

---

## Le prime tre hanno una cosa in comune

La conoscenza **è vostra.**

Il progetto. La procedura. Il lavoro da delegare.

---

## La quarta è l'opposto

# Tre frontender.<br>Due ore.<br>Nessun designer.

Il risultato funziona **ed è brutto.**

<!-- Non perché sono scarsi. Perché il gusto visivo non è una procedura che ripeti: è un mestiere. E un mestiere non si scrive in dieci minuti. -->

---

## Quindi non la scrivete

Non è una regola del progetto.
Non è una procedura vostra.
Non è un lavoro da delegare a un contesto separato.

**È roba che qualcun altro ha già scritto meglio di voi.**

---

## La lancia una persona sola

Su tutti e sei i componenti, adesso che esistono
e che i props sono già congelati dal contratto.

Se la lanciate in tre,
alle cinque avete **tre linguaggi visivi** nella stessa app.

<!-- E si vede in demo. È l'argomento più facile da dimostrare di tutta la giornata: basta guardare lo schermo. -->

---

## È brava, e non conosce il vostro contratto

Può rinominare una prop e rompere due branch in un colpo.

1. Solo su `src/components/ui/**` e `layout.tsx`
2. Le firme **non si toccano**: se le cambia, tenete lo stile e rimettete i nomi
3. Guardate il diff prima di committare

---

## Le regole restano vuote

Nel vostro `CLAUDE.md` c'è una sezione:

### «Regole aggiunte dal team»

Oggi in fase 1 **non la scrivete.**

---

## Una regola si scrive dopo aver sbagliato

Prima di sbagliare è **un'opinione.**

Dopo è **una cicatrice** — e si vede, perché è specifica:

> Le pagine del sito fanno fetch con `cache: "no-store"`.
> Senza, un post creato nel backoffice non compare in home
> e sembra un bug delle API.

<!-- In fase 3 le scriviamo insieme: o quello che hanno corretto a mano più volte, o una frase che torna in più prompt della giornata. Obiettivo minimo: una regola per team, che si possa seguire. -->

---

## Gli strumenti si scrivono al terzo giro

Non prima di conoscere il problema.

Non dopo aver finito.

**Al terzo giro**, quando ti accorgi che stai rifacendo la stessa cosa.

Oggi il terzo giro arriva in un pomeriggio.
