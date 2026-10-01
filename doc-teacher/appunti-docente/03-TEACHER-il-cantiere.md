# Il cantiere, e le quattro categorie — note per me

Perché la giornata è in tre fasi invece che in tre track paralleli dall'inizio, e cosa dire mentre montano i loro strumenti (skill e subagent).

## Perché il cantiere esiste

La prima versione di questo workshop aveva un ruolo che teneva contratto e componenti e mergiava le PR. Sulla carta funziona; in pratica **quel ruolo è un collo di bottiglia**: finché i componenti condivisi non esistono, gli altri due lavorano contro un `TODO` e scoprono al merge se avevano indovinato.

La fase 1 toglie il problema alla radice: **le fondamenta le costruiscono tutti e tre, prima che qualcuno cominci il suo pezzo.** Quando parte la fase 2 non manca niente a nessuno, e nessuno deve aspettare il vicino.

Il costo c'è ed è onesto: quaranta minuti su centoventi non sono codice della propria feature. Si recuperano tutti nella fase 2, perché nessuno si ferma.

| | | |
|---|---|---|
| 0–10 | setup | ruoli, repo del team, clone |
| **10–50** | **fase 1 · il cantiere** | insieme |
| **50–95** | **fase 2 · il proprio pezzo** | da soli |
| **95–115** | **fase 3 · rimettere insieme** | insieme |
| 115–120 | demo | |

## Il punto da far passare nella fase 1

Non è «Claude Code ha quattro feature». È che ci sono **quattro posti diversi dove mettere la stessa conoscenza**, e sbagliare posto si paga.

| | Quando | Cosa costa |
|---|---|---|
| **Regola** | vale sempre, non la invochi | sta nel contesto a ogni messaggio |
| **Skill** | una procedura che rifai uguale | solo quando la usi |
| **Subagent** | un lavoro che deleghi | contesto suo, ti torna un verdetto |
| **Skill esterna** | un mestiere che non è il tuo | niente: è già scritta |

L'errore tipico è mettere tutto nel `CLAUDE.md`: funziona per due settimane, poi il file è lungo trecento righe, nessuno lo legge e Claude ne ignora metà. La regola pratica da dire a voce: **se serve solo quando fai una cosa specifica, non è una regola, è una skill.**

## Perché uno strumento a testa

Tre persone × tre strumenti = novanta minuti su centoventi. Assurdo.

Il criterio di selezione è uno solo: **si ripaga entro le due ore?**

| | Strumento | Usi nella sessione |
|---|---|---|
| T1 | skill `/new-page` | 2: la home e il dettaglio |
| T3 | skill `/new-form` | 1, ma è il pezzo più lungo della giornata |
| T2 | subagent `smoke-test` | 4: una a testa a fine track, più quella finale in tre |

Il subagent è andato al T2 perché è il track più corto dei tre: così i carichi si pareggiano. E serve a tutti e tre, non a lui: è l'esempio che uno strumento può essere scritto da uno e usato dalla squadra.

## La quarta categoria, e perché è la più difficile da spiegare

Le prime tre hanno in comune che **la conoscenza è loro**: il progetto, la procedura, il lavoro da delegare. La skill esterna è l'unica in cui la conoscenza non ce l'hanno — e senza un caso concreto resta astratta.

Il caso concreto è il design. Tre frontender, due ore, nessun designer: il risultato funziona ed è brutto. Non è bravura, è che **il gusto visivo non è una procedura che ripeti, è un mestiere.** Le prime tre categorie lì non servono: non è una regola del progetto, non è una procedura tua, non è un lavoro da delegare a un contesto separato. È roba che qualcun altro ha già scritto meglio di te.

**La lancia una persona sola, sui sei componenti, alla fine della fase 1**, nel momento in cui i tre si riallineano prima di dividersi. È il momento giusto per due ragioni: i sei componenti sono appena arrivati tutti con un `git pull`, e i props sono già congelati dal contratto, quindi il rischio che rompa qualcosa è minimo. Se la lanciassero in tre, alle cinque ci sarebbero tre linguaggi visivi nella stessa app — ed è l'argomento più facile da dimostrare di tutta la giornata: basta guardare lo schermo.

**Si installa in sala, ma la scarica una persona sola**: `npx skills add anthropics/skills@frontend-design -y` installa dentro il progetto (il `-y` salta la domanda sugli agent), quindi al commit dell'allineamento ce l'hanno tutti e tre. A casa fanno solo `npx --yes skills --version`, per scaldare la cache di npx e non scaricare quindici volte la stessa cosa sul wifi della conferenza.

## Le regole nascono in fase 3, e questo va annunciato in fase 1

Il `CLAUDE.md` arriva nel repo con le cose non negoziabili e con una sezione vuota, *«Regole aggiunte dal team»*. In fase 1 la si lascia vuota **apposta**, e va detto perché: una regola scritta prima di sbagliare è un'opinione, scritta dopo è una cicatrice.

In fase 2 non chiedo niente: hanno prompt già pronti e starebbero a guardare il soffitto. La domanda la faccio io all'inizio della fase 3, quando sono di nuovo insieme, e i primi cinque minuti sono per scrivere le regole nel `CLAUDE.md`.

**Obiettivo minimo: una regola per team, nata da un errore vero.** Le tre che di solito emergono:

1. la fetch senza `cache: "no-store"` — il post creato non compare in home
2. `"use client"` messo in cima a una pagina che non ne ha bisogno
3. un `any` o un `@ts-ignore` per far tacere il compilatore alle 16:50

Se nessuno inciampa, in fase 3 non insisto con *«cosa avete ripetuto?»*: faccio riaprire i prompt della giornata e cercare una frase che torna in più di uno — «testi in italiano», `cache: "no-store"`, le rotte da `API_ROUTES`. Quelle sono regole travestite da istruzioni, ripetute a mano tutto il giorno perché non stavano dove Claude le legge da solo.

## Cosa può andare storto

- **La fase 1 sfora.** È il rischio numero uno, perché sono quattro cose in quaranta minuti con tre persone che si parlano. Il timer è mio, non loro: a 50 si passa alla fase 2 anche se un componente è brutto. Si sistema dopo.
- **Scrivono skill lunghe.** Dieci minuti sono pochi apposta. Se qualcuno arriva a ottanta righe, quella skill non verrà usata: fategliela tagliare.
- **Il subagent risponde con tre paragrafi.** Il formato di risposta va imposto nel prompt, altrimenti non risparmia niente rispetto a leggere il diff.
- **La skill di design rinomina una prop del contratto.** Succede. Si tiene lo stile e si rimettono i nomi. Se succede, è un ottimo momento da far vedere a tutti invece che da nascondere: è il motivo per cui le firme stanno nel contratto e non nella testa di chi ha scritto il componente.
- **Nessuno usa quello che ha scritto.** È il fallimento vero. A metà fase 2 passo e chiedo: *«l'hai usata?»*. Se la risposta è no, o la skill è sbagliata o il momento per invocarla non è chiaro, e in entrambi i casi si sistema in due minuti.

## La frase con cui chiudo il blocco

Gli strumenti non li scrivi prima di conoscere il problema, e non li scrivi dopo aver finito. Li scrivi **al terzo giro**, quando ti accorgi che stai rifacendo la stessa cosa. Oggi il terzo giro arriva in un pomeriggio, e per questo si vede.
