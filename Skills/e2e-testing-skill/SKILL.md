---
name: e2e-testing
description: >
  Usa questa skill quando l'utente chiede di progettare test end-to-end per
  REST API, API HTTP, web application o flussi misti simulando interazioni reali
  da interfacce esterne. Serve per definire scenari E2E, setup, dati di test,
  isolamento, cleanup, verifiche osservabili e casi Arrange/Act/Assert. Input
  tipici: requisiti, endpoint, pagine, flussi utente, API, payload, stato
  persistente, vincoli di autenticazione. Output atteso: piano E2E, scenari,
  casi di test, strategia di isolamento, cleanup e assunzioni.
---

# E2E Testing

## Quando usarla

Usa questa skill quando l'utente vuole:

- progettare test end-to-end;
- testare un flusso completo dal punto di vista utente o client esterno;
- verificare una REST API con richieste HTTP reali;
- verificare una web app con browser, form, click, input e navigazione;
- progettare test Playwright, Cypress, Selenium, Postman, Newman, pytest + requests o simili;
- testare login, registrazione, logout, CRUD, risorse protette o flussi multi-step;
- verificare integrazione tra UI, backend, API e persistenza;
- rendere test isolati, ripetibili e indipendenti dall'ordine di esecuzione;
- definire setup, cleanup, dati unici e strategia di isolamento.

## Quando non usarla

Non usare questa skill quando:

- l'utente chiede test unitari puri;
- l'utente chiede test black-box di singola funzione o combinazioni di input;
- l'utente chiede white-box testing, branch coverage, path coverage o analisi CFG;
- l'utente vuole solo mock isolati senza sistema reale;
- mancano flusso utente/client, interfacce esterne o risultato osservabile;
- la richiesta e solo debugging manuale senza progettazione test.

## Obiettivo

L'obiettivo della skill e produrre:

- scenari E2E realistici e verificabili;
- test che attraversano interfacce esterne osservabili;
- piano con precondizioni, step, input, output attesi e cleanup;
- strategia di isolamento tra test;
- dati di test controllati e unici quando necessario;
- casi Arrange/Act/Assert;
- verifiche su status, body, redirect, UI, persistenza o stato visibile;
- assunzioni e rischi dichiarati.

## Input richiesti

L'utente dovrebbe fornire:

- tipo di sistema: REST API, web app o mixed;
- flusso utente o client da testare;
- endpoint, pagine o interfacce esterne coinvolte;
- input, payload, credenziali o dati necessari;
- risultato atteso osservabile;
- stato persistente da verificare;
- vincoli di autenticazione/autorizzazione;
- strategia test disponibile, se esiste: reset DB, fixture, seed, cleanup API, browser state;
- tool desiderato, se serve codice implementabile.

Se manca un input non essenziale, fai una scelta ragionevole e dichiarala.

Se manca un input essenziale, chiedi chiarimento.

## Procedura/workflow

1. Leggi attentamente la richiesta dell'utente.
2. Identifica il tipo di task: piano E2E, scenari, test REST API, test web app, test mixed o codice implementabile.
3. Controlla se la skill e adatta al caso.
4. Raccogli interfacce esterne, flussi, dati, auth, stato persistente e output attesi.
5. Identifica scenari user-level o client-level: ogni scenario deve rappresentare un flusso completo.
6. Definisci attore, obiettivo, precondizioni, azioni, risultato atteso e cleanup.
7. Identifica interfacce esterne coinvolte: endpoint, pagine, form, browser, token, headers, payload, DB osservabile.
8. Definisci dati di test controllati e unici.
9. Progetta isolamento: stato noto iniziale, cleanup, reset browser/sessione/database quando necessario.
10. Scrivi casi con Arrange, Act, Assert e Cleanup.
11. Verifica solo risultati osservabili dall'esterno, non dettagli interni del codice.
12. Usa eventuali file in `references/` solo se servono.
13. Produci l'output nel formato richiesto.
14. Fai un controllo finale prima di rispondere.

## Regole importanti

- Mantieni la risposta chiara e ordinata.
- Non aggiungere sezioni inutili.
- Non inventare dati mancanti.
- Segnala sempre eventuali assunzioni.
- Segui il formato di output richiesto.
- Usa esempi solo se aiutano davvero.
- Non rendere la skill troppo generica.
- Non confondere E2E con unit test.
- Non testare dettagli interni del codice.
- Non far dipendere un test dal successo di un test precedente.
- Non riusare dati modificabili tra test paralleli.
- Non verificare solo `200 OK`: controlla anche body, UI, redirect, persistenza o effetto osservabile.
- Non usare sleep fissi nei test web se puoi aspettare condizioni osservabili.
- Non lasciare dati sporchi nel database.
- Ogni test deve poter partire da stato noto.
- Ogni test deve avere cleanup esplicito o isolamento equivalente.
- Se uno scenario modifica dati persistenti, prevedi dati unici e cleanup.

## Uso di references

Leggi queste reference solo quando utili:

- `references/e2e-rest-api.md`: test REST/API, endpoint, HTTP, token, payload JSON, status code, persistenza.
- `references/e2e-web-app.md`: test browser, pagine, form, click, redirect, selettori, attese e UI visibile.
- `references/output-template.md`: template per scenario table, piano E2E completo, casi REST, casi web e tabella compatta.

## Formato di output

Restituisci il risultato in questo formato:

```text
Titolo:

Input usati:

Risultato:

Assunzioni:

Controllo finale:
```

Per un piano E2E completo, struttura `Risultato` cosi:

```text
Obiettivo:

Tipo di E2E:

Interfacce esterne coinvolte:

Scenari:

Strategia di isolamento:

Casi di test:

Note finali:
```

Per test implementabili, usa:

```text
Arrange:
Act:
Assert:
Cleanup:
```

## Errori da evitare

- Testare una funzione interna invece di un flusso esterno.
- Controllare solo status code o solo click senza risultato osservabile.
- Dipendere da ordine di esecuzione dei test.
- Usare dati condivisi modificabili.
- Dimenticare cleanup o reset stato.
- Usare selettori fragili legati al layout.
- Usare sleep fissi invece di condizioni osservabili.
- Coprire ogni combinazione black-box con E2E: gli E2E devono coprire flussi critici, non tutte le combinazioni.
- Salvare token/sessioni tra test senza pulizia.
- Nascondere assunzioni su utenti, DB, seed o ambiente.

## Controllo finale

Prima di concludere, verifica:

- ogni test simula un flusso realistico;
- interfacce esterne sono dichiarate;
- input, azioni e expected result sono chiari;
- verifiche osservabili sono presenti;
- isolamento e cleanup sono definiti;
- i test non dipendono dall'ordine;
- dati creati sono unici o puliti;
- sessioni, cookie e local storage sono gestiti quando serve;
- assunzioni e rischi sono dichiarati;
- output segue il formato richiesto.

## Quick Checklist

```text
[ ] Ho identificato flussi utente/client realistici?
[ ] Ho definito interfacce esterne?
[ ] Ho indicato precondizioni e dati di test?
[ ] Ho previsto autenticazione/autorizzazione se serve?
[ ] Ho definito Arrange, Act, Assert e Cleanup?
[ ] Ho verificato output osservabili?
[ ] Ho verificato persistenza o stato visibile quando rilevante?
[ ] Ogni test e isolato?
[ ] I dati sono unici o puliti?
[ ] I test non dipendono dall'ordine?
[ ] Assunzioni e rischi sono dichiarati?
```
