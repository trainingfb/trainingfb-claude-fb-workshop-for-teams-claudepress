> **Solo facilitatore** · [indice](../README.md) · [02 · Runbook](02-runbook.md) →

# Messaggi pronti

Da copiare e incollare. Le date e i link sono da sostituire.

La formazione è in due pezzi: il **workshop 1** lo fanno da soli a casa, il
**workshop 2** è la giornata in aula. Questi messaggi servono a far arrivare
tutti con il primo già fatto, che è l'unica cosa che fa stare la seconda parte
dentro le due ore.

---

## T-10 giorni — il workshop 1

Il messaggio più importante di tutti. Mandalo con abbondanza di anticipo: due
ore di lavoro non si incastrano in una sera qualsiasi.

> Ciao a tutti 👋
>
> Fra due settimane ci vediamo per il workshop in aula, che sarà **tutto
> pratico**: lavoreremo in squadre da quattro sulla stessa codebase, in
> parallelo, e alla fine ognuno mostra cosa ha consegnato.
>
> Perché funzioni, le basi vanno fatte prima. Vi mando il **workshop 1**: un
> percorso da fare **da soli**, con i vostri tempi, circa due ore spezzabili
> come volete.
>
> <URL-REPO-WORKSHOP-1>
>
> Si parte dal `README.md` e si va in ordine. Alla fine avrete costruito una
> skill, un agente e un plugin vostro, e saprete scrivere le regole di un
> progetto. In aula si parte da lì.
>
> **Due cose:**
> - c'è un `npm run verifica` che vi dice da soli a che punto siete, usatelo
> - se vi bloccate più di dieci minuti, **scrivetemi**: sono qui. Ditemi a che
>   passo siete e incollate quello che vedete
>
> Restate su **Sonnet**: gli esercizi sono tarati per finire in fretta e non vi
> serve altro. Se bruciate i limiti lì, arrivate in aula senza.

---

## T-7 giorni — il setup della giornata

> Ciao 👋 due cose in vista di <data>.
>
> **1.** Come va il workshop 1? Se non l'avete ancora cominciato, questo è il
> momento: dopo diventa una corsa.
>
> **2.** Il setup del progetto su cui lavoreremo in aula. Dieci minuti adesso,
> perché il giorno stesso non c'è tempo: sono due ore e sono tutte di lavoro.
>
> **Serve:** Node 24 · git · [GitHub CLI](https://cli.github.com) autenticata
> (`gh auth login`) · Claude Code con un account **Pro o Max** attivo · il
> vostro editor.
>
> ```
> git clone <URL-REPO> claudetrips
> cd claudetrips
> npm install
> ./scripts/check-setup.sh
> ```
>
> Lo script vi dice verde/rosso riga per riga. **Se esce qualcosa in rosso,
> incollate qui l'output**: lo sistemiamo prima.
>
> Se è tutto verde e il workshop 1 è finito, rispondete con un 👍.

---

## T-3 giorni — il promemoria mirato

Non mandarlo al gruppo: manda un privato solo a chi non ha risposto. Sono
sempre gli stessi quattro o cinque, e sono quelli che in aula bloccano il
tavolo.

> Ciao <nome>, non ho visto il tuo 👍 — sei riuscito a fare il workshop 1 e il
> check di setup? Se ti sei bloccato da qualche parte scrivimi dove, che in
> cinque minuti lo sistemiamo. Sono due ore scarse e ci tengo che <data> tu
> parta insieme agli altri invece di rincorrere.

---

## La mattina — il messaggio nel canale

> Buongiorno! Repo: <URL>
>
> Se non l'avete ancora fatto: `npm install` e `./scripts/check-setup.sh`.
> Wifi: `<rete>` / `<password>`
>
> Controllate anche di avere il plugin del workshop 1:
> ```
> claude plugin list
> ```
> Se non c'è, installatelo adesso: sono due minuti e oggi aprirete una pull
> request tre o quattro volte.
>
> Usate **Sonnet**, non Opus. Due ore di lavoro fitto e i limiti finiscono
> prima di quanto pensiate. Opus tenetelo per i momenti in cui vi serve
> ragionare, non per scrivere una route handler.

---

## Dopo — il follow-up dello stesso giorno

Mandalo la sera stessa, non il giorno dopo: la sera se lo leggono ancora.

> Grazie a tutti, bella giornata 🙏
>
> Tutto quello che avete costruito:
> - i cinque repo dei team con le PR mergiate: <link>
> - le skill che avete modificato durante la giornata: <link>
> - il materiale, se volete rileggerlo: `workshop/README.md`
>
> Le tre cose da portarsi a lunedì, in ordine di quanto costano poco:
> 1. un `CLAUDE.md` nel vostro progetto vero, con tre regole verificabili
> 2. il plugin che avete costruito nel workshop 1: installatelo nei repo dove
>    lavorate davvero, `commit` e `pr` funzionano ovunque
> 3. il contratto prima del codice, anche quando lavorate da soli
>
> Una domanda sola, e mi interessa davvero la risposta: **cosa avete provato a
> rifare al lavoro questa settimana?** Scrivetemelo qui anche fra dieci giorni.
