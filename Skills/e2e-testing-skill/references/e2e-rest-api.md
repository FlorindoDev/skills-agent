# E2E REST API Testing Reference

Usa questa reference quando devi progettare o scrivere test E2E su endpoint HTTP, payload JSON, token, status code e persistenza.

## Regola di flessibilita

Questi scenari e controlli non sono esaustivi. Se l'API reale richiede uno scenario E2E diverso, usalo e spiega:

- quale flusso utente o client copre;
- perche e piu rilevante degli scenari elencati;
- quali effetti osservabili verifica;
- come isola dati, autenticazione e cleanup.

## Scopo

Nei test E2E REST API l'interfaccia esterna e composta dagli endpoint HTTP.

L'utente finale e un programma, servizio o client che invia richieste reali.

## Cosa verificare

Per ogni richiesta verifica:

- metodo HTTP corretto;
- URL corretto;
- headers necessari;
- payload corretto;
- status code;
- body JSON;
- schema o campi obbligatori;
- messaggi di errore;
- autorizzazione;
- effetti persistenti, se rilevanti.

## Scenari REST API comuni

### Login riuscito

```text
POST /auth
Body: { "usr": "gerry", "pwd": "sussman" }
Expected:
- 200 OK
- body contiene { "token": string }
- token valido o usabile in richiesta protetta
```

### Login fallito

```text
POST /auth
Body: { "usr": "gerry", "pwd": "wrong" }
Expected:
- 401 Unauthorized o status di errore documentato
- nessun token restituito
- body errore coerente con specifica API
```

### Creazione risorsa protetta

```text
1. Login e ottieni token.
2. POST /todos
   Headers: Authorization: Bearer <TOKEN>
   Body: { "todo": "foobar", "done": false }
3. Expected:
   - 200 OK o 201 Created
   - risposta contiene risorsa creata
   - risorsa recuperabile con GET
```

### Lettura risorsa

```text
GET /todos/:id
Expected:
- 200 OK
- body contiene risorsa richiesta
```

### Aggiornamento risorsa

```text
PUT /todos/:id
Body: campi aggiornati
Expected:
- 200 OK
- risposta contiene valori aggiornati
- GET successivo restituisce valori aggiornati
```

### Eliminazione risorsa

```text
DELETE /todos/:id
Expected:
- 200 OK, 204 No Content o status documentato
- GET successivo restituisce 404 o risorsa assente
```

## Isolamento REST API

Strategie preferite:

1. Crea dati dentro il test.
2. Usa identificatori unici.
3. Elimina dati creati nel cleanup.
4. Resetta database tra test se disponibile.
5. Non dipendere da dati creati da test precedenti.

## Template REST API

```markdown
### Test [ID]: [nome scenario]

**Arrange**
- Prepara base URL.
- Crea o identifica utente test.
- Fai login se endpoint richiede autenticazione.
- Prepara payload.

**Act**
- Invia richiesta HTTP.

**Assert**
- Verifica status code.
- Verifica response body.
- Verifica headers se rilevanti.
- Verifica stato persistente con altra richiesta se serve.

**Cleanup**
- Elimina risorse create.
- Cancella token/sessione se necessario.
```

## Errori comuni

- Non verificare solo status code.
- Non riusare stessa risorsa mutabile tra test.
- Non assumere ID fissi se database non viene resettato.
- Non lasciare che cleanup fallito nasconda errore di assert.
- Preferisci setup esplicito invece di dipendere da dati esistenti.
