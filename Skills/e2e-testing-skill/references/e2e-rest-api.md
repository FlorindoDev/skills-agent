# E2E REST API Testing Reference

## Purpose

Nei test E2E REST API l’interfaccia esterna è composta dagli endpoint HTTP.

L’utente finale è un programma, servizio o client che invia richieste reali.

## What to verify

Per ogni richiesta verifica:

- metodo HTTP corretto;
- URL corretto;
- headers necessari;
- payload corretto;
- status code;
- body JSON;
- schema o campi obbligatori;
- messaggi di errore;
- effetti persistenti, se rilevanti.

## Common REST API scenarios

### Login riuscito

```text
POST /auth
Body: { "usr": "gerry", "pwd": "sussman" }
Expected:
- 200 OK
- body contains { "token": string }
- token is valid or usable in a protected request
```

### Login fallito

```text
POST /auth
Body: { "usr": "gerry", "pwd": "wrong" }
Expected:
- 401 Unauthorized, or documented error status
- no token returned
- error body matches API specification
```

### Creazione risorsa protetta

```text
1. Login and obtain token
2. POST /todos
   Headers: Authorization: Bearer <TOKEN>
   Body: { "todo": "foobar", "done": false }
3. Expected:
   - 200 OK or 201 Created
   - response contains created resource
   - resource can be retrieved with GET
```

### Lettura risorsa

```text
GET /todos/:id
Expected:
- 200 OK
- body contains requested resource
```

### Aggiornamento risorsa

```text
PUT /todos/:id
Body: updated fields
Expected:
- 200 OK
- response contains updated values
- subsequent GET returns updated values
```

### Eliminazione risorsa

```text
DELETE /todos/:id
Expected:
- 200 OK, 204 No Content, or documented status
- subsequent GET returns 404 or resource is absent
```

## REST API isolation

Preferred strategies:

1. Create data inside the test.
2. Use unique identifiers.
3. Delete created data in cleanup.
4. Reset database between tests when available.
5. Do not depend on data created by previous tests.

## REST API test template

```markdown
### Test [ID]: [scenario name]

**Arrange**
- Prepare base URL.
- Create or identify test user.
- Login if endpoint requires authentication.
- Prepare payload.

**Act**
- Send HTTP request.

**Assert**
- Check status code.
- Check response body.
- Check headers if relevant.
- Optionally verify persisted state with another request.

**Cleanup**
- Delete created resources.
- Clear token/session if needed.
```

## Gotchas

- Do not assert only the status code.
- Do not reuse the same mutable resource across tests.
- Do not assume fixed IDs unless the database is reset.
- Do not let failed cleanup hide the real assertion failure.
- Prefer explicit setup over relying on production-like existing data.
