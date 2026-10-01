> **Solo facilitatore** · [indice](../README.md) · ← [02 · Runbook](02-runbook.md) · [05 · Piani B](05-piani-b.md) →

# Come condurre le due ore

Il tuo lavoro qui non è spiegare: è **osservare e sbloccare**. Parli quattordici
minuti in tutto, e la domanda che fai a tutti, sempre la stessa, è **«cosa ti
sta bloccando?»**, non «come va», perché a «come va» rispondono tutti bene.

> Le basi le hanno fatte a casa, nel workshop 1. Se cominci a rispiegare cos'è
> una skill, hai perso il pomeriggio e annoiato chi il compito l'aveva fatto.

---

## Team, ruoli, repo del team — 10′ (tuoi: 6′)

**Cosa dire**, in tre minuti:

Cosa si costruisce oggi, come sono divise le due ore, e i ruoli. Sui ruoli
fermati mezzo minuto, perché è una cosa che nessuno indovina:

> «La T sta per **track**, filone di lavoro. T1 backend, T2 sito, T3
> backoffice. T0 ha il numero zero perché non ha un track suo: non scrive
> funzionalità, tiene il contratto e mergia. Ritroverete le sigle nei nomi dei
> branch e nei TODO, quindi teneteli a mente.»

Poi consegna i fogli dei tavoli e **stai zitto**. Gira fra i banchi e guarda gli
schermi.

**Il controllo che salta sempre**

Il repo del team. Qualcuno continua a lavorare sulla copia scaricata a casa e se ne accorge
solo quando prova a pushare. Tavolo per tavolo:

- [ ] il repo del team esiste
- [ ] gli altri tre sono collaborator **e hanno clonato il repo del team**
- [ ] ognuno sa qual è il suo ticket
- [ ] `npm run dev` risponde su tutti e quattro i portatili

**Se qualcuno non ha fatto il workshop 1**

Non fermare la sala. Mettilo in coppia con qualcuno che l'ha fatto e digli che
recupera stasera: le skill nel repo ci sono comunque, e il plugin glielo installi
in due minuti. Il piano B lungo è in [05](05-piani-b.md).

---

## Il kickoff — 8′

L'unico discorso lungo della giornata. Tre punti, in quest'ordine.

**1. Il problema vero non è il codice.**

> «Fra un'ora avrete tre pezzi scritti da tre persone che non si sono viste. O
> si incastrano, o avete tre pezzi bellissimi e niente che funziona. Tutto
> quello che facciamo nei prossimi venticinque minuti serve solo a quello.»

**2. Il contratto.** Apri `src/contracts/trips.ts` sul proiettore e scorrilo.
Fermati sul pezzo che non si aspettano:

> «Il contratto non sono solo i path degli endpoint. C'è dentro la forma esatta
> di ogni risposta e di ogni errore, 404 compresi. Sapete perché? Perché chi fa
> il sito e chi fa il backoffice scrivono oggi contro API che non esistono
> ancora. Se la forma degli errori non è nel contratto, ognuno se la inventa, e
> lo scoprite al merge.»

Questo è il concetto più prezioso della giornata ed è quello che si portano al
lavoro. Non correre.

**3. Le tre regole**, sulla lavagna, dove restano per due ore.

Poi una riga sulla pianificazione:

> «Venticinque minuti, **un solo computer acceso per team**. Gli altri tre
> guardano e contestano.»

---

## Pianificazione — 25′

**Il segnale numero uno:** il tavolo dove stanno già scrivendo codice. Fermali.

> «Chiudi l'editor. Se in venticinque minuti producete un piano buono, l'ora e
> mezza dopo fila. Se ne producete uno mediocre, nessuna velocità di scrittura
> ve lo recupera.»

**Il segnale numero due:** il tavolo silenzioso dove parla solo il Contract
Owner. Chiedi tu qualcosa direttamente a T2 o T3: fra dieci minuti devono
lavorare contro API che non esistono, e se il contratto non l'hanno capito
adesso, lo scoprite tutti dopo.

**Cosa deve esserci nel piano, quando passi a controllare**

- la tabella dei file, senza sovrapposizioni
- le dipendenze fra track e come si va avanti senza aspettare
- la decisione che hanno preso sull'ambiguità della story

Se manca la tabella dei file, il merge finale sarà un disastro. Falla scrivere
prima di andartene dal tavolo.

---

## PR #0 — 5′

**Controllo secco, tavolo per tavolo: la PR #0 è mergiata?**

Non andare oltre finché tutti e cinque i team non l'hanno mergiata. Se un team
parte con basi diverse, i suoi tre track divergono da subito e il merge finale
non succede.

---

## Lavoro parallelo — 45′

Tre checkpoint, gridati per tutta la sala.

| Quando | Cosa gridi | Perché |
|---|---|---|
| **+10′** | «T2, T3: state aspettando qualcuno?» | la risposta giusta è «no, ho il fallback». Se aspettano T1, non hanno letto l'escape hatch |
| **+20′** | «Tutti hanno una PR aperta?» | anche vuota. Zero PR a venti minuti = quel team non finisce |
| **+35′** | «T0, cosa hai già mergiato?» | se risponde «niente, mergio alla fine», il team è in pericolo |

Nel mezzo giri e fai **quella** domanda, a ognuno.

**Cose da non fare**

- Non mettere le mani sulla tastiera. Se li sblocchi tu, il team impara che c'è
  sempre qualcuno che sblocca.
- Non rispondere a domande di dominio, tipo «una richiesta su un pacchetto tolto
  dal sito si vede?». Rimandali al piano: quella decisione l'hanno presa loro, o
  dovevano prenderla.
- Non correggere il codice di nessuno. Al massimo indica il ticket.

**Le domande che ti faranno**

*«Posso toccare un file che non è mio?»*
No. Scrivilo nella PR come punto di merge e parlane con il T0.

*«La skill `/new-endpoint` non fa esattamente quello che voglio.»*
Allora modificala: è nel repo del team, è vostra. È esattamente quello che hanno
imparato a fare nel workshop 1, e qui hanno il primo motivo vero per farlo.

*«L'adversarial review mi ha trovato sette problemi, li sistemo tutti?»*
No. Rispondi a tutti nella PR, sistema quelli che ti convincono. Rifiutarne
qualcuno è parte dell'esercizio.

*«Non sono pratico di git, come apro la PR?»*
Mandalo a [`_02-se-qualcosa-va-storto.md`](../doc-studenti/_02-se-qualcosa-va-storto.md) e alla skill `/pr` del progetto invece di spiegarglielo:
è scritto per questo, e tu devi restare disponibile per gli altri diciannove.
Per i merge, i tre casi con i comandi sono in [`02-si-allinea.md`](../doc-studenti/02-si-allinea.md).

*«Ho finito il mio ticket, cosa faccio?»*
Vai dal T0. Quasi sempre la risposta è: fai la review della PR di un altro. Mai:
aggiungi una feature che non era prevista.

---

## Integrazione — 15′

Annuncio a voce alta: **«da adesso niente feature nuove. Solo far funzionare
quello che c'è.»**

È il momento in cui qualcuno perde la testa perché il main non è verde. Il tuo
lavoro qui è dire cosa **non** fare: niente refactor, niente «già che ci sono»,
niente «sistemo io il pezzo di un altro». Una storia che manca si lascia fuori
dalla demo e si dice.

---

## Demo — 10′

Due minuti a team, cronometrati davvero. Le tre domande sono sempre le stesse:

1. mostrate la story che funziona
2. una decisione che avete preso e che la story non aveva deciso
3. una cosa che rifareste diversa

**La terza è quella da cui esce il valore, ed è quella che tagliano se li lasci
correre.** Se un team la salta, richiamala tu prima di passare al successivo.

---

## Chiusura — 2′

Non riassumere quello che hanno fatto: l'hanno fatto loro, lo sanno. Chiudi
sulle tre cose che si portano a lunedì:

1. **Il contratto viene prima del codice.**
2. **Il parallelismo si progetta assegnando i file**, non coordinandosi meglio.
3. **Una PR aperta presto vale più di una PR perfetta tardi.**

E, se ti serve una frase per finire:

> «Stamattina avete imparato a dire a Claude cosa conta nel vostro progetto.
> Oggi avete scoperto che è la stessa identica cosa che serve per far lavorare
> insieme quattro persone. Solo che adesso non c'è più la scusa del tempo.»
