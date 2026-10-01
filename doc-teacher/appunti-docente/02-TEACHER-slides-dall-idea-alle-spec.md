<!--
Slide per il racconto "Da un'idea a delle specifiche" — 10 minuti, lo racconto io. Separatore: `---`. Funziona con Marp, Slidev e reveal.js senza modifiche. I commenti HTML sotto le slide sono le note per chi parla: non si vedono a schermo. La versione lunga e leggibile è in 02-TEACHER-dall-idea-alle-spec.md -->

# Da un'idea<br>a delle specifiche

Cinque prompt, venti minuti, quattro file.

<!-- Questa parte non la fanno loro: arrivano al workshop con spec, contratto e ticket pronti. Ma è il pezzo che in un progetto vero fanno per primo. -->

---

## Il problema

**Tre persone. Due ore. Una sola codebase.**

Se partono dal codice, alle 17:45 hanno tre branch che non si parlano.

<!-- Non è un problema di Claude Code. È il problema di sempre. Claude Code lo rende solo più veloce da sbagliare. -->

---

## Il punto di partenza

```
GOAL
Creiamo un Blog in NextJS utilizzando SSR con CMS.
Non è necessario proteggere la parte di admin.

TEAM
- FrontEnd: libreria React con i componenti base
- FrontEnd: Blog Vetrina (Next)
- FrontEnd (CMS): Backoffice (Next)

ROUTES        /admin/posts   /admin/posts/[id]   /home
API           CRUD lista posts, CRUD dettaglio post
```

Otto righe, scritte di getto. **Va benissimo così.**

<!-- Un'idea non deve essere completa. Deve essere scritta. Questo è il testo vero, non ritoccato. -->

---

## Cinque passaggi

| | | Cosa esce |
|---|---|---|
| **0** | L'idea buttata giù | `idea.md`, grezzo |
| **1** | Le domande che non mi sono fatto | decisioni aperte |
| **2** | Le risposte, e i tagli | `idea.md`, pulito |
| **3** | Le specifiche | `spec.md` |
| **4** | Il contratto | `contracts/blog.ts` |
| **5** | I ticket | uno per persona |

---

## Tre regole

**Finché non c'è il contratto, non si scrive codice.**

**Ogni passo produce un file, e il file si committa.**
Il passo dopo lo legge con `@`.

**La risposta che conta è «no».**

<!-- La seconda è quella che dimentichiamo tutti: se resta nella chat, al passo 4 non esiste più. -->

---

## 1 · Le domande

Il passaggio che salta il 90% delle persone.

Se non lo fai, **le decisioni le prende Claude al posto tuo.**

E le prende bene — ma senza dirtelo.

---

## 1 · Il prompt

```
Leggi @idea.md. Non scrivere codice e non propormi soluzioni.

Fammi solo le domande a cui questa idea non risponde e che, se non
rispondo, ti costringerebbero a inventare qualcosa.

Massimo otto, ordinate da quella che cambia di più il progetto
a quella che cambia di meno. Una riga ciascuna.
```

<!-- Le tre clausole che contano: "non scrivere codice", "che ti costringerebbero a inventare", "massimo otto ordinate". Senza la terza arrivano quaranta domande e non ne leggi nessuna. -->

---

## 1 · Cosa è uscito

- Da dove arrivano i dati?
- Un post ha degli stati — bozza, pubblicato?
- Chi possiede i componenti condivisi, visto che servono a due persone su tre?
- **Chi mergia?**

<!-- L'ultima ha cambiato il progetto. -->

---

## L'ultima domanda ha cambiato il progetto

Nell'idea di partenza le tre persone consegnavano **tutte e tre una feature**.

Nessuna teneva insieme il lavoro delle altre.

→ un ruolo su tre diventa **contratto, componenti e merge**

---

## 2 · Rispondi e taglia

```
Ecco le risposte:
1. ...
2. ...

Tutto quello che non ho nominato è fuori perimetro: sono due ore.
Riscrivi @idea.md tenendo queste scelte e togliendo il resto.
Resta corto: è ancora un'idea, non una specifica.
```

---

## 2 · Le due sezioni che contano

### «Cosa non c'è»

La sezione più utile del documento: al minuto 70 impedisce a qualcuno di mettersi a fare la ricerca full-text.

### «La demo», una frase sola

*Creo un post nel backoffice, lo vedo in home, lo apro.*

**Se un lavoro non serve a quella frase, oggi non si fa.**

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

<!-- La lista "da decidere" è il motivo per cui il prompt funziona: senza, ogni buco viene riempito da un'invenzione plausibile che scopri tre ore dopo. -->

---

## 4 · Il contratto

La specifica smette di essere prosa e **diventa un file TypeScript**.

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

---

## Da qui il contratto è congelato

È il momento in cui il progetto **diventa divisibile in tre**.

Chi lo cambia, rompe il lavoro degli altri due.

<!-- Nel workshop questa è la regola numero uno del CLAUDE.md. Se pensi che vada cambiato, ti fermi e lo dici. -->

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

---

## La riga più importante di tutte

> *Se non riesci a dividerli, fermati e dimmi quale si sovrappone invece di inventare una divisione.*

Se due ticket si contendono un file, non è un problema di ticket: **è un problema di architettura.**

E lo vuoi scoprire adesso, non durante il merge.

---

## Il punto

Cinque prompt. Venti minuti. Quattro file.

Nessuno di quei venti minuti è tempo tolto al codice.

È tempo tolto **al pomeriggio in cui tre branch non si parlano
e nessuno sa di chi è la colpa.**
