> **Solo facilitatore** · [indice](../README.md) · ← [01 · Messaggi](01-messaggi.md) · [03 · Guida](03-guida.md) →

# Runbook — la timeline

20 persone, **due ore**, 5 team da 4. Questa è solo la sequenza: il **cosa
dire** sta in [03](03-guida.md), i **piani B** in [05](05-piani-b.md), la
**preparazione** in [00](00-preparazione.md).

> Le basi arrivano dal workshop 1, fatto da loro a casa. Qui non si spiega più
> cos'è una skill, cos'è `CLAUDE.md` o come funziona il plan mode. Se qualcuno
> non l'ha fatto, il piano B è in [05](05-piani-b.md).

## Colpo d'occhio

| Ora | Step | Cosa | Chi parla |
|---|---|---|---|
| **0:00 – 0:10** | [01](../../workshop-2-team/workshop/01-il-tuo-team.md) | Team, ruoli, fork, cloni | tu 6′ |
| 0:10 – 0:18 | [02](../../workshop-2-team/workshop/02-la-story.md) | Kickoff: la story e il contratto | tu 8′ |
| 0:18 – 0:43 | [03](../../workshop-2-team/workshop/03-la-pianificazione.md) | Pianificazione, **un solo PC** | loro |
| 0:43 – 0:48 | — | PR #0 mergiata, tutti `git pull` | tu |
| 0:48 – 1:33 | [05](../../workshop-2-team/workshop/05-lavorare-in-parallelo.md) | Lavoro parallelo | loro |
| 1:33 – 1:48 | [06](../../workshop-2-team/workshop/06-integrazione-e-demo.md) | Integrazione, `main` verde | loro |
| 1:48 – 1:58 | [06](../../workshop-2-team/workshop/06-integrazione-e-demo.md) | Demo, 2 minuti a team | loro |
| 1:58 – 2:00 | — | Chiusura | tu |

Parli per quattordici minuti in tutto. Il resto lo fanno loro, ed è il punto.

## I controlli che non si saltano

| Quando | Controllo | Se è no |
|---|---|---|
| 0:08 | Tutti hanno clonato **il fork**, non l'originale | si riclona, sono due minuti |
| 0:08 | Tutti hanno `npm run dev` che risponde | coppia con il vicino, non si aspetta |
| 0:43 | Tutti e cinque i team hanno mergiato la PR #0 | **non si va avanti** |
| 0:58 | T2 e T3 non stanno aspettando T1 | mandali all'escape hatch del ticket |
| 1:08 | Tutti hanno una PR aperta | quel team non finirà |
| 1:23 | T0 ha già mergiato qualcosa | fallo mergiare adesso |

Il controllo delle 0:43 è l'unico davvero bloccante: se un team parte senza il
contratto in `main`, i suoi tre track divergono da subito e il merge finale non
si recupera in un'ora.

## Le tre regole sulla lavagna

Scritte prima che entrino, restano lì per due ore.

1. **Tocchi solo i file del tuo ticket**
2. **PR aperta entro 20 minuti**, anche in draft
3. **`/adversarial-review`** prima della review umana

## Cosa è cambiato rispetto alla versione da quattro ore

Le prime due ore, cioè regole, plan mode, la propria skill e lo skill swap, sono
diventate il **workshop 1**, che fanno da soli a casa su un'altra codebase. Qui
resta solo il lavoro in team.

Due conseguenze pratiche:

- Le sei skill del progetto sono **già nel repo**, in `.claude/skills/`. Nessuno
  le scrive più il giorno stesso, e questo è il motivo per cui il lavoro
  parallelo sta in 45 minuti.
- Il setup si fa a casa, non in aula. Se lo fai fare lì, perdi un quarto della
  giornata.

## Dopo

Il giorno stesso, nel canale: il repo con le PR mergiate dei cinque team, le
skill che hanno modificato, il link ai materiali. Il testo pronto è in
[`01-messaggi.md`](01-messaggi.md#dopo--il-follow-up-dello-stesso-giorno).
