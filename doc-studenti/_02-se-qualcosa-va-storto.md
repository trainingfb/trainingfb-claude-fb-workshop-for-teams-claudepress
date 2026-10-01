> **Da aprire quando serve.**
> [← indice](_README.md)

# Se qualcosa va storto

Non ha un posto nella sequenza: si apre quando serve.

| | Cosa succede davvero |
|---|---|
| **«Ho creato il post e in home non c'è»** | manca `cache: "no-store"` sulla fetch. **Non è un bug delle API**: è la cache di Next |
| **«La pagina dice *Failed to parse URL*»** | una fetch con path relativo dentro un server component. L'URL si costruisce con `apiUrl(API_ROUTES.x)` del contratto |
| **«I post sono tornati quelli di prima»** | hai riavviato il dev server. Lo store è in memoria e riparte dal seed: è giusto così |
| **«Il componente che mi serve non esiste»** | non dovrebbe succedere dopo la fase 1. Se succede, `// TODO(Tx):` e vai avanti: non aspettare |
| **«Mi serve un file di un altro track»** | fermati. Non toccarlo: annotalo e se ne parla in fase 3. È materiale per il merge |
| **«Ho toccato per sbaglio un file di un altro»** | dillo subito invece di cancellare di nascosto. Costa trenta secondi adesso e venti minuti dopo |
| **«Il contratto mi sembra sbagliato»** | in fase 1 si discute, dopo no. Se è la fase 2, aggiralo e portalo in fase 3 |
| **«La skill di design ha rinominato una prop»** | tieni lo stile, rimetti i nomi del contratto. È esattamente il motivo per cui le firme stanno lì |
| **«`npm run check` non passa»** | non committare. Se non capisci l'errore, incollalo a Claude: è più veloce di te |
| **«Ho aperto una seconda PR e mostra cose già fatte»** | il secondo branch è partito da un `main` che non conteneva ancora il tuo lavoro. Chiudi la seconda PR e continua sulla prima: finché non è mergiata, è lì che vanno i commit |
| **«`git push` rifiutato: `src refspec main does not match any`»** | il branch si chiama `master`: hai fatto `git init` senza `-b main`. `git branch -M main` e ripeti il push |
| **«Nel `git log` mi manca un commit»** | `git status -sb`: *ahead* = hai committato ma non pushato, *behind* = non hai fatto `git pull`. I tre casi con i comandi stanno in [`02-si-allinea.md`](02-si-allinea.md) |
| **«Ho fatto un casino con git»** | fermati prima di peggiorare e chiedi. Dieci minuti persi in tre valgono meno di un `reset --hard` sbagliato |
| **«Non finiamo in tempo»** | normale. Tagliate gli stretch goal, non i criteri di demo: meglio due track finiti e uno a metà che tre a metà |

## La domanda da farsi prima di chiedere aiuto

> È un problema mio, o è materiale per la fase 3?

Se è materiale per la fase 3, **annotalo e vai avanti.** Fermare tutti e tre per una cosa che si risolve in venti minuti insieme è il modo più efficace di sprecare il pomeriggio.
