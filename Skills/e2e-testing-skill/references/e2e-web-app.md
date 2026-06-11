# E2E Web App Testing Reference

Usa questa reference quando devi progettare o scrivere test E2E su browser, pagine, form, click, redirect, selettori e UI visibile.

## Regola di flessibilita

Questi scenari e controlli non sono esaustivi. Se l'app reale richiede uno scenario E2E diverso, usalo e spiega:

- quale flusso utente copre;
- perche e piu rilevante degli scenari elencati;
- quale risultato visibile verifica;
- come gestisce stato browser, dati di test e cleanup.

## Scopo

Nei test E2E Web App l'interfaccia esterna e la pagina web.

L'utente finale e una persona che usa il browser.

Il test deve simulare azioni reali:

- visitare pagine;
- scrivere nei campi;
- cliccare bottoni o link;
- verificare redirect;
- verificare testo o componenti visibili.

## Cosa verificare

Per ogni scenario verifica:

- pagina iniziale;
- elementi interattivi;
- input inseriti;
- azione utente;
- redirect o cambio pagina;
- messaggi visibili;
- aggiornamento della UI;
- persistenza dopo refresh, se rilevante.

## Scenari web app comuni

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

## Isolamento web app

Prima o dopo ogni test:

- pulisci cookie;
- pulisci local storage;
- pulisci session storage;
- resetta database o elimina risorse create;
- crea dati unici;
- evita dipendenza da stato browser precedente.

## Guida selettori

Preferisci selettori stabili:

1. role/name selectors;
2. labels;
3. test ids, se il progetto li usa;
4. evita selettori CSS fragili legati al layout.

Esempi:

```text
getByRole("button", { name: "Login" })
getByLabel("Username")
getByText("Hi, Gerry")
```

## Guida attese

Evita sleep fissi.

Preferisci aspettare condizioni osservabili:

- URL pagina cambiato;
- elemento visibile;
- response completata;
- loading indicator sparito;
- item apparso in lista.

## Template web app

```markdown
### Test [ID]: [nome scenario]

**Arrange**
- Resetta stato browser.
- Prepara dati o crea utente.
- Visita pagina iniziale.

**Act**
- Esegui azioni utente: fill, click, navigate.

**Assert**
- Verifica risultato visibile nella UI.
- Verifica redirect se rilevante.
- Verifica persistenza se rilevante.

**Cleanup**
- Elimina dati creati.
- Pulisci stato browser.
```

## Errori comuni

- Non usare sleep arbitrari se evitabili.
- Non dipendere da ordine di esecuzione.
- Non usare selettori che si rompono quando cambia layout.
- Non saltare cleanup per entita create.
- Non controllare solo che un bottone sia stato cliccato: verifica risultato visibile.
