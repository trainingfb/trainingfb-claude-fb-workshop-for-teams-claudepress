> **Solo facilitatore** · [indice](../README.md) · ← [03 · Guida](03-guida.md) · [06 · Fogli](06-fogli-da-stampare.md) →

# Piani B

## Finiscono i limiti di utilizzo

Venti persone su account Pro: qualcuno li finisce, quasi sempre il più bravo,
perché è quello che ha macinato di più. Il rischio adesso è più alto di prima,
perché arrivano avendo già consumato un paio d'ore nel workshop 1.

- **Prevenzione, da dire al kickoff:** state su Sonnet, tenete Opus per i
  momenti in cui vi serve ragionare. E usate plan mode: un piano corretto una
  volta costa molto meno di tre implementazioni sbagliate.
- **Cura:** chi resta a secco si sposta in coppia sul portatile di un compagno
  di team. Non è un ripiego triste — il pair programming in quella fase
  funziona bene.
- Tieni comunque i tuoi due account di riserva pronti.

## La rete cede

Dev server e Claude Code girano in locale: si perdono solo i push e
le PR. Si continua a lavorare e si pusha quando torna.

Se non torna: la demo si fa dal portatile del Contract Owner, con i branch
mergiati in locale. Funziona, e diventa anche un aneddoto.

## Un team resta indietro

Non dare una mano a scrivere codice: **riduci l'ambito**. Vai al tavolo e di'
tu quale storia tagliare — di solito S4, le richieste nel backoffice.

Un team che consegna due storie funzionanti fa una demo migliore di uno che ne
consegna quattro rotte, e lo capiscono subito quando lo vedono.

## Una persona è bloccata da venti minuti

È sempre lo stesso problema: sta aspettando il pezzo di un altro. Mandala
all'**escape hatch** del suo ticket — sono scritti apposta, e nessuno li legge
finché non glielo dici tu.

Se aspetta T1, il fallback locale del suo ticket è scritto apposta: nove volte
su dieci non l'ha letto.

## Il Contract Owner si mette a scrivere codice

Succede sempre, di solito verso metà. Riportalo al suo ruolo con una domanda
sola:

> «Chi sta mergiando mentre tu scrivi?»

## Un team ha modificato il contratto a lavori iniziati

Fermali subito e fai contare quante persone stanno lavorando su quella base.
Poi: o si annulla la modifica, o si mergia **adesso** e tutti fanno `git pull`
prima di scrivere un'altra riga. Non c'è una terza opzione, e lasciarla aperta
significa perdere il pomeriggio.

## Il setup non è stato fatto

Con due ore non c'è margine: chi installa Node in aula ha già perso metà
giornata. Mettilo in coppia sul portatile di un compagno di team e fallo
lavorare da lì. Non fermare gli altri diciassette.

## Qualcuno non ha fatto il workshop 1

Succederà, mettilo in conto: uno o due su venti.

**Non rispiegare le basi alla sala.** Il danno vero non è il loro, è aver
annoiato i diciotto che il compito l'avevano fatto.

Cosa fare, in ordine:

1. Installagli il plugin `git`, sono due minuti: senza, oggi apre le PR
   a mano.
2. Mettilo in un ruolo dove il traino di un compagno pesa di meno. **T2 o T3**,
   mai T0, e mai T1 da cui dipendono gli altri due.
3. Digli di aprire `.claude/skills/` e leggere la sua skill di ruolo. Tre
   minuti, e recupera l'ottanta per cento di quello che gli serve oggi.
4. Il resto lo fa stasera.

## Sei in ritardo di venti minuti

Con due ore il margine è poco, quindi accorgitene presto. Nell'ordine, cosa
tagliare:

1. la **demo** scende a un minuto a team, e tieni solo la prima e la terza
   domanda
2. l'**integrazione** si accorcia: si accetta che `main` abbia una storia fuori,
   e si dice in demo
3. il **lavoro parallelo** si riduce di cinque minuti, non di più

Cosa **non** tagliare mai: la **pianificazione** e il **kickoff**. Se tagli
quelli, la parte in team non produce niente e la giornata non ha una conclusione
da mostrare.

E non recuperare mai tempo saltando il controllo sulla PR #0: è l'unica cosa
che, se salta, non si recupera più.
