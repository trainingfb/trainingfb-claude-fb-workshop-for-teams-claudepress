# Da un'idea a delle specifiche

> **Questa parte la racconto io.** Voi non la fate: arrivate al workshop con le spec, il contratto e i ticket già pronti. Ma è il pezzo che in un progetto vero fate per primo, e vale i dieci minuti che ci mettiamo a guardarlo.

Il progetto di oggi non è nato da un documento. È nato da otto righe scritte di getto. In mezzo ci sono cinque passaggi, ognuno con un prompt e un file che esce.

| | Passo | Cosa esce |
|---|---|---|
| 0 | L'idea buttata giù | `idea.md`, grezzo |
| 1 | Le domande che non mi sono fatto | un elenco di decisioni aperte |
| 2 | Le risposte, e i tagli | `idea.md`, pulito |
| 3 | Le specifiche | `spec.md` |
| 4 | Il contratto | `src/contracts/blog.ts` |
| 5 | I ticket | un file per persona |

Tre regole che valgono per tutti e cinque:

- **Finché non c'è il contratto, non si scrive codice.** Ogni prompt qui sotto lo dice esplicito, perché altrimenti Claude parte a implementare.
- **Ogni passo produce un file, e il file si committa.** Il passo dopo lo legge con `@`. Se resta nella chat, al passo 4 non esiste più.
- **La risposta che conta è «no».** Metà del lavoro è togliere.

---

## 0 · L'idea, com'era davvero

Il punto di partenza, copiato senza ritocchi:

```
GOAL
Creiamo un Blog in NextJS utilizzando SSR con CMS per la creazione di contenuti.
Non è necessario proteggere la parte di admin in questa fase.

- Server: fornito
- tecnologia: NextJS

TEAM
- FrontEnd: libreria React con i componenti base
- FrontEnd: Blog Vetrina (Next)
- FrontEnd (CMS): Backoffice (Next)

ROUTES
- /admin/posts
- /admin/posts/[id]
- /home

API
- CRUD lista posts
- CRUD dettaglio post
```

Va benissimo così. Un'idea non deve essere completa, deve essere scritta.

---

## 1 · Fatti fare le domande

Il passaggio che salta il 90% delle persone. Se non lo fai, le decisioni le prende Claude al posto tuo — e le prende bene, ma senza dirtelo.

```
Leggi @idea.md. Non scrivere codice e non propormi soluzioni.

Fammi solo le domande a cui questa idea non risponde e che, se non
rispondo, ti costringerebbero a inventare qualcosa.

Massimo otto, ordinate da quella che cambia di più il progetto a quella
che cambia di meno. Una riga ciascuna.
```

Quello che è uscito, in sintesi: da dove arrivano i dati? Un post ha stati (bozza / pubblicato)? Chi possiede i componenti condivisi, visto che servono a due persone su tre? Chi mergia?

**L'ultima è quella che ha cambiato il progetto.** Nell'idea di partenza le tre persone consegnavano tutte e tre una feature, e nessuna teneva insieme il lavoro.

---

## 2 · Rispondi, e taglia

```
Ecco le risposte:
1. ...
2. ...

Tutto quello che non ho nominato è fuori perimetro: sono due ore.
Riscrivi @idea.md tenendo queste scelte e togliendo il resto.
Resta corto: è ancora un'idea, non una specifica.
```

Due cose da notare nel risultato, che oggi vive nella prima sezione di [`_01-prima-di-venire.md`](../../doc-studenti/_01-prima-di-venire.md):

- è comparsa una sezione **«Cosa non c'è»**. È la più utile del documento: è quella che al minuto 70 impedisce a qualcuno di mettersi a fare la ricerca.
- è comparsa **una frase sola che descrive la demo**. Se un lavoro non serve a quella frase, oggi non si fa.

---

## 3 · Le specifiche

```
Da @idea.md scrivi spec.md. Mi servono quattro cose, e solo quelle:

1. le storie utente, una riga ciascuna
2. le rotte del sito, con cosa mostra ognuna
3. le rotte API, con la forma esatta dei dati in entrata e in uscita
4. cosa è fuori perimetro, esplicito

Niente codice. Se qualcosa non è ancora deciso, mettilo in una lista
"da decidere" invece di sceglierlo tu.
```

La lista «da decidere» è il motivo per cui questo prompt funziona: senza, ogni buco viene riempito da un'invenzione plausibile che scopri tre ore dopo.

---

## 4 · Il contratto

Qui la specifica smette di essere prosa e diventa un file TypeScript. È il momento in cui il progetto diventa divisibile in tre.

```
Da @spec.md scrivi src/contracts/blog.ts:

- i tipi TypeScript delle entità
- gli schemi zod per gli input delle API
- le costanti delle rotte API
- la forma dell'errore, uguale per tutti gli endpoint

È l'unico file che tre persone si scambiano: nomi espliciti, niente
abbreviazioni, e sopra ogni blocco un commento che dica a chi serve.
Solo questo file, nient'altro.
```

Da qui in poi il contratto è **congelato**. Chi lo cambia, rompe il lavoro degli altri due.

---

## 5 · I ticket

```
Da @spec.md e @src/contracts/blog.ts scrivi tre ticket, uno per persona.
Devono essere di peso simile e nessuno deve dipendere dagli altri due:
se un ticket consegna qualcosa che serve a un altro, hai sbagliato a dividere.

Per ognuno:
- l'obiettivo in una frase
- i file che possiede, come elenco di path
- cosa deve funzionare alla demo
- uno stretch goal, per chi finisce prima

Nessun file deve comparire in due ticket. Se non riesci a dividerli,
fermati e dimmi quale si sovrappone invece di inventare una divisione.
```

L'ultima riga è la più importante di tutto il documento. Se due ticket si contendono un file, non è un problema di ticket: è un problema di architettura, e lo vuoi scoprire adesso e non durante il merge.

---

## Il punto

Cinque prompt, venti minuti, quattro file. Nessuno di quei venti minuti è tempo tolto al codice: è tempo tolto al pomeriggio in cui tre branch non si parlano e nessuno sa di chi è la colpa.
