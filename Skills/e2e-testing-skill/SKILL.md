---
name: e2e-testing
description: Progetta test end-to-end modulari per REST API e web application simulando flussi realistici dal punto di vista dell’utente finale. Usa questa skill per scenari E2E, test API reali, test browser, isolamento dei test, setup/cleanup e template AAA.
---

# E2E Testing Skill

## Goal

Aiutare l’agente a progettare test End-to-End che verifichino il comportamento del sistema nel suo insieme, dal punto di vista dell’utente finale o del client esterno.

La skill deve produrre scenari realistici, isolati, ripetibili e controllabili per:

- REST API o API in generale;
- web application tradizionali;
- SPA;
- flussi utente completi;
- setup, cleanup e isolamento tra test.

## When to use

Usa questa skill quando l’utente chiede di:

- progettare test E2E;
- testare un flusso completo utente;
- verificare una REST API tramite richieste HTTP reali;
- verificare una web app tramite browser, click, input e navigazione;
- scrivere scenari Playwright, Cypress, Selenium, Postman, Newman, pytest + requests o simili;
- controllare login, registrazione, creazione/modifica/eliminazione risorse;
- verificare che UI, backend e database lavorino correttamente insieme;
- rendere i test indipendenti, isolati e ripetibili.

Non usare questa skill per test unitari puri, test white-box, branch coverage, path coverage o test di singole funzioni isolate.

## Core principle

Un test E2E verifica il sistema completo attraverso le interfacce esterne.

Il test deve simulare un utilizzo realistico:

- per REST API o API, l’utente finale è un altro programma o servizio che invia richieste HTTP;
- per web app, l’utente finale è una persona che interagisce con il browser;
- il test deve controllare output osservabili: status code, body JSON, redirect, elementi UI, stato visibile, dati persistiti.

Non basarti sulla struttura interna del codice, salvo per capire come avviare ambiente, seed dati o cleanup.

## Default behavior

Se l’utente non specifica il tipo di E2E:

1. Usa REST API mode se l’input parla di endpoint, metodi HTTP, payload, token, status code o JSON.
2. Usa sempre isolamento dei test come vincolo obbligatorio.
3. Usa AAA come struttura di ogni test.
4. Se il flusso modifica dati persistenti, prevedi setup e cleanup.

## Workflow

### 1. Identify user-level scenarios

Individua gli scenari realistici da testare.

Uno scenario E2E deve rappresentare un flusso completo, non una singola funzione interna.

Esempi:

- login riuscito;
- login fallito;
- registrazione nuovo utente;
- creazione di un To-do;
- modifica di un To-do;
- eliminazione di un To-do;
- accesso a risorsa protetta;
- logout;
- flusso completo: registrazione → login → creazione risorsa → verifica → cleanup.

Per ogni scenario chiarisci:

- attore;
- obiettivo;
- precondizioni;
- azioni;
- risultato atteso;
- dati coinvolti;
- cleanup necessario.

### 2. Identify external interfaces

Stabilisci da quali interfacce il test interagisce con il sistema.

Per REST API/ API:

- endpoint;
- metodo HTTP;
- headers;
- payload;
- query/path parameters;
- status code atteso;
- body atteso;
- autenticazione;
- eventuale persistenza verificabile.


### 3. Define test data

Ogni test deve avere dati controllati.

Per evitare conflitti:

- usa dati unici per ogni test;
- preferisci username/email/titoli generati con suffisso casuale o timestamp;
- non dipendere da dati creati da altri test;
- non assumere ordine di esecuzione;
- evita credenziali condivise se il test modifica lo stato dell’utente.

Per test autenticati:

- crea utente nel setup, oppure
- usa fixture stabile solo se read-only, oppure
- effettua login nel test e ottieni token/sessione.

### 4. Design isolation strategy

Ogni test E2E deve essere isolato.

Regole obbligatorie:

- un test che fallisce non deve sporcare quelli successivi;
- i test devono poter girare in qualsiasi ordine;
- i test devono poter girare in parallelo se l’infrastruttura lo consente;
- ogni test deve partire da uno stato noto;
- database, sessioni, local storage e cookie devono essere puliti o controllati.

Strategie possibili:

- reset database prima di ogni test;
- transazione rollback, se supportata;
- seed iniziale ripetibile;
- cleanup via API dopo il test;
- uso di dati unici e cancellazione finale;
- container/database dedicato per test suite;
- pulizia cookie/local storage/session storage per test web.

Se l’utente non specifica strategia, proponi:

- setup con dati unici;
- cleanup esplicito dopo il test;
- reset sessione/browser tra test.

### 5. Write the E2E test plan

Per ogni scenario produci:

- ID test;
- nome scenario;
- tipo: REST API, Web App o Mixed;
- precondizioni;
- step;
- input;
- expected result;
- cleanup;
- note di isolamento.

Gli step devono essere concreti e verificabili.

### 6. Use AAA structure

Quando generi test implementabili, organizza sempre in:

- Arrange: prepara ambiente, dati, login, token, pagina iniziale.
- Act: esegui il flusso utente/API.
- Assert: verifica status, body, redirect, UI, dati persistiti.
- Cleanup: elimina dati creati o resetta stato.

Cleanup può stare dopo Assert o in hook dedicati come `afterEach`.

## Modes

### Mode: REST API/ API E2E

Usalo quando l’interfaccia esterna è una REST API.

Controlla sempre:

- status code;
- body JSON;
- schema o campi obbligatori;
- headers rilevanti;
- autenticazione/autorizzazione;
- effetti persistenti quando necessari.

Esempio di flusso:

1. POST `/auth` con credenziali valide.
2. Verifica `200 OK`.
3. Verifica presenza di `token`.
4. Usa `Authorization: Bearer <TOKEN>` per chiamare endpoint protetti.
5. Verifica risposta ed effetto della chiamata.

Leggi `references/e2e-rest-api.md` quando devi progettare o scrivere test API.


## Gotchas

- Non confondere E2E con unit test: un E2E attraversa più componenti.
- Non testare dettagli interni del codice.
- Non fare dipendere un test dal successo di un test precedente.
- Non riusare dati modificabili tra test paralleli.
- Non lasciare dati sporchi nel database.
- Non verificare solo `200 OK`: controlla anche body, stato visibile o persistenza.
- Non usare sleep fissi nei test web se puoi aspettare condizioni osservabili.
- Non rendere ogni test enorme: preferisci pochi flussi critici e realistici.
- Non testare tutti i casi black-box tramite E2E: usa E2E per flussi principali, non per ogni combinazione di input.
- Non salvare token/sessioni tra test senza pulizia.
- Per login E2E, verifica sia successo sia almeno un fallimento significativo.
- Per CRUD E2E, verifica almeno create/read/update/delete se sono flussi critici.

## Output format

Quando l’utente chiede una progettazione completa, usa:

```markdown
# E2E test design: [nome sistema/flusso]

## Obiettivo

[Spiega cosa viene verificato dal punto di vista dell’utente finale]

## Tipo di E2E

[REST API / API]

## Interfacce esterne coinvolte

| Interfaccia | Tipo | Descrizione |
|---|---|---|

## Scenari

| ID | Scenario | Attore | Precondizioni | Risultato atteso |
|---|---|---|---|---|

## Strategia di isolamento

[Come ogni test parte da stato pulito e come viene fatto cleanup]

## Casi di test

| Test ID | Scenario | Arrange | Act | Assert | Cleanup |
|---|---|---|---|---|---|

## Note finali

[Assunzioni, rischi, dati mancanti, casi futuri]
```

## Validation checklist

Prima di finalizzare, verifica:

- [ ] Ogni test simula un flusso realistico.
- [ ] Il test usa solo interfacce esterne osservabili.
- [ ] Sono definiti input, azioni e risultato atteso.
- [ ] Sono controllati status/body/UI/redirect/persistenza dove serve.
- [ ] Ogni test è isolato.
- [ ] Non esiste dipendenza dall’ordine di esecuzione.
- [ ] I dati creati sono unici o puliti.
- [ ] Cookie, sessioni e local storage sono gestiti.
- [ ] Il cleanup è esplicito.
- [ ] I test sono abbastanza pochi da essere mantenibili.
- [ ] Gli scenari critici utente sono coperti.

## When to load references

Leggi `references/e2e-rest-api.md` quando devi lavorare su endpoint REST, HTTP, token, payload JSON o status code.

Leggi `references/e2e-web-app.md` quando devi lavorare su browser, pagine, form, click, redirect o elementi UI.

Leggi `references/output-template.md` quando devi produrre una tabella finale o test implementabili.
