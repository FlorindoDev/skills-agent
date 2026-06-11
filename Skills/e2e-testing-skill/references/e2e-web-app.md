# E2E Web App Testing Reference

## Purpose

Nei test E2E Web App l’interfaccia esterna è la pagina web.

L’utente finale è una persona che usa il browser.

Il test deve simulare azioni reali:

- visitare pagine;
- scrivere nei campi;
- cliccare bottoni o link;
- verificare redirect;
- verificare testo o componenti visibili.

## What to verify

Per ogni scenario verifica:

- pagina iniziale;
- elementi interattivi;
- input inseriti;
- azione dell’utente;
- redirect o cambio pagina;
- messaggi visibili;
- aggiornamento della UI;
- persistenza dopo refresh, se rilevante.

## Common Web App scenarios

### Login riuscito

```text
1. Visit login page
2. Fill username with "gerry"
3. Fill password with "sussman"
4. Click Login
5. Expected:
   - redirect to homepage
   - navbar shows "Hi, Gerry"
```

### Login fallito

```text
1. Visit login page
2. Fill username with valid username
3. Fill password with wrong password
4. Click Login
5. Expected:
   - stay on login page
   - error message is visible
   - user is not authenticated
```

### Creazione To-do

```text
1. Visit To-do page
2. Fill input with "example"
3. Click "Save to-do"
4. Expected:
   - new item appears in list
   - item text is "example"
```

### Persistenza To-do

```text
1. Create To-do
2. Refresh page
3. Expected:
   - created To-do is still visible
```

### Logout

```text
1. Login
2. Click Logout
3. Expected:
   - redirect to login page
   - protected page is no longer accessible
```

## Web App isolation

Before or after each test:

- clear cookies;
- clear local storage;
- clear session storage;
- reset database or delete created resources;
- create unique test data;
- avoid depending on previous browser state.

## Selector guidance

Prefer stable selectors:

1. role/name selectors;
2. labels;
3. test ids, if project convention supports them;
4. avoid brittle CSS selectors tied to layout.

Examples:

```text
getByRole("button", { name: "Login" })
getByLabel("Username")
getByText("Hi, Gerry")
```

## Waiting guidance

Avoid fixed sleeps.

Prefer waiting for observable conditions:

- page URL changed;
- element visible;
- response completed;
- loading indicator disappeared;
- item appeared in list.

## Web App test template

```markdown
### Test [ID]: [scenario name]

**Arrange**
- Reset browser state.
- Prepare data or create user.
- Visit starting page.

**Act**
- Perform user actions: fill, click, navigate.

**Assert**
- Verify visible UI result.
- Verify redirect if relevant.
- Verify persistence if relevant.

**Cleanup**
- Delete created data.
- Clear browser state.
```

## Gotchas

- Do not use arbitrary sleep unless unavoidable.
- Do not rely on test execution order.
- Do not use selectors that break when layout changes.
- Do not skip cleanup for created entities.
- Do not check only that a button was clicked: check the user-visible result.
