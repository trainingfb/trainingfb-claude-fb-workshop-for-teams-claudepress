# Fogli da stampare — uno per tavolo

Stampa cinque copie, compila i nomi a mano la sera prima, e mettili sui
tavoli prima che entrino. Serve a far trovare il proprio posto senza
organizzare niente a voce.

---

<br>

# TEAM ___

## Chi fa cosa

**La T sta per track**, filone di lavoro. `T0` ha il numero zero perché non ha
un track suo: non scrive funzionalità, tiene il contratto e mergia.

| | Ruolo | Nome | Possiede questi file |
|---|---|---|---|
| **T0** | Contract Owner | ____________________ | `src/contracts/**` · `src/components/**` · `CLAUDE.md` · `.claude/**` |
| **T1** | Backend + docs | ____________________ | `src/app/api/**` · `src/server/**` · `docs/api.md` |
| **T2** | Frontend · sito | ____________________ | `src/app/pacchetti/**` · `src/app/page.tsx` |
| **T3** | Frontend · backoffice | ____________________ | `src/app/admin/**` |

**Tocchi solo i file della tua riga.** Se ti serve toccare quelli di un altro,
fermati e dillo: è materiale per il merge, non una cosa da risolvere in
silenzio.

<br>

## Le tre regole

1. **Tocchi solo i file del tuo ticket**
2. **PR aperta entro 20 minuti**, anche in draft, anche se non fa ancora niente
3. **`/adversarial-review`** prima di chiedere la review a un umano

<br>

## L'ordine

```
T0 apre la PR #0 e la mergia SUBITO
                 │
        ┌────────┼────────┐
        ▼        ▼        ▼
       T1       T2       T3
    backend    sito   backoffice
        └────────┼────────┘
                 ▼
    T0 mergia man mano, non alla fine
```

<br>

## Il vostro fork

```
Repo del team:  ________________________________

Branch:  <ruolo>/<cosa>      es.  t1/create-package
```

<br>

## Prima di ogni commit

```bash
npm run check
```

Se non passa, non si committa.

<br>

## Le skill che avete già

| | |
|---|---|
| `/contract-check` | prima di ogni commit |
| `/adversarial-review` | prima della review umana |
| `/new-endpoint` | T1 |
| `/new-page` | T2 e T3 |
| `/new-form` | T3 e T2 |
| `/pr-review` | T0 |
| `/commit` · `/pr` | dal plugin del workshop 1 |

Sono nel repo del team. **Se una non fa quello che vi serve, modificatela.**

<br>

## Quando sei bloccato

Il tuo ticket ha una sezione **Escape hatch**: dice cosa fare quando il pezzo
di un altro non è ancora pronto. Non aspettare mai più di cinque minuti — vai
lì e continua con un finto.

<br>

## Gli orari

| | |
|---|---|
| Pianificazione insieme, un solo PC | fino alle ______ |
| PR #0 mergiata, tutti `git pull` | ______ |
| Lavoro parallelo | fino alle ______ |
| Stop alle feature, solo integrazione | ______ |
| Demo — 2 minuti | ______ |
