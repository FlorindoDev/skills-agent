---
name: clean-code-writing
description: >
  Usa questa skill quando l'utente chiede di scrivere nuovo codice, implementare
  feature, aggiungere o modificare classi/metodi/moduli, progettare piccole
  architetture interne o migliorare codice mentre resta pulito, coeso, poco
  accoppiato, mantenibile e testabile. Serve per prevenire debito tecnico
  durante l'implementazione. Input tipici: richiesta utente, codice esistente,
  requisiti, vincoli tecnici, file di progetto. Output atteso: codice o patch
  con scelte di design, responsabilita, testabilita, rischi e controllo finale.
---

# Clean Code Writing

## Quando usarla

Usa questa skill quando l'utente vuole:

- scrivere nuovo codice pulito e mantenibile;
- implementare una nuova feature;
- aggiungere classi, metodi, moduli o componenti;
- modificare codice esistente senza peggiorare il design;
- decidere dove collocare una responsabilita;
- progettare una piccola architettura interna;
- scegliere tra classe concreta, interfaccia, dependency injection, DTO, DAO/Repository, Factory o altro pattern;
- ridurre accoppiamento inutile;
- aumentare coesione e chiarezza delle responsabilita;
- evitare code smells, generalita speculativa e debito tecnico;
- scrivere codice facile da testare.

## Quando non usarla

Non usare questa skill quando:

- l'utente chiede solo una spiegazione teorica senza codice o progettazione;
- l'utente chiede solo refactoring di codice esistente senza aggiungere comportamento;
- l'utente chiede una review generale senza scrivere codice;
- il task riguarda sicurezza, performance avanzata, UI design o deployment come obiettivo principale;
- la richiesta e troppo generica e non contiene un obiettivo implementativo chiaro.

## Obiettivo

L'obiettivo della skill e produrre:

- codice funzionante, leggibile, coeso e mantenibile;
- patch coerenti con lo stile del progetto;
- classi con responsabilita chiare e un solo motivo principale per cambiare;
- metodi piccoli, nominati bene e facili da testare;
- dipendenze limitate e sostituibili;
- design che anticipa il cambiamento senza introdurre astrazioni inutili;
- output finale con scelte di design, funzionalita, testabilita, rischi e controllo finale.

## Input richiesti

L'utente dovrebbe fornire:

- richiesta funzionale o comportamento atteso;
- file o porzioni di codice da modificare;
- linguaggio, framework e vincoli del progetto;
- formato di output desiderato, se diverso dalla patch;
- eventuali requisiti non funzionali importanti: performance, affidabilita, costi, manutenibilita, usabilita.

Se manca un input non essenziale, fai una scelta ragionevole e dichiarala.

Se manca un input essenziale, chiedi chiarimento.

## Procedura/workflow

1. Leggi attentamente la richiesta dell'utente.
2. Identifica il tipo di task: nuova feature, nuovo modulo, modifica puntuale, scelta di design o codice testabile.
3. Controlla se la skill e adatta al caso.
4. Raccogli gli input disponibili nel codice esistente.
5. Cerca nel progetto codice simile e segui lo stile gia presente se e corretto.
6. Identifica la responsabilita principale del codice da aggiungere.
7. Decidi dove collocare la responsabilita usando alta coesione e basso accoppiamento.
8. Valuta i design goal rilevanti: performance, affidabilita, costi, manutenibilita, usabilita.
9. Esplicita eventuali trade-off di design quando influenzano la soluzione.
10. Scrivi la soluzione piu semplice che soddisfa i requisiti.
11. Usa interfacce, Factory, DAO/Repository, Observer, Iterator, Composite o altri pattern solo se risolvono un problema reale.
12. Separa logica pura, I/O e dipendenze esterne per rendere il codice testabile.
13. Usa eventuali file in `references/` solo se servono.
14. Produci l'output nel formato richiesto.
15. Esegui o proponi test coerenti con il rischio della modifica.
16. Fai un controllo finale prima di rispondere.

## Regole importanti

- Mantieni la risposta chiara e ordinata.
- Non aggiungere sezioni inutili.
- Non inventare dati mancanti.
- Segnala sempre eventuali assunzioni.
- Segui il formato di output richiesto.
- Usa esempi solo se aiutano davvero.
- Non rendere la skill troppo generica.
- Preferisci alta coesione: ogni metodo deve fare una cosa, ogni classe deve rappresentare un concetto chiaro.
- Applica SRP: una responsabilita e un motivo per cambiare.
- Preferisci basso accoppiamento: evita dipendenze concrete inutili e accesso a dettagli interni di altre classi.
- Applica la Legge di Demetra: evita catene tipo `a.getB().getC().doX()`.
- Usa Responsibility-Driven Design: ragiona in termini di classe, responsabilita e collaboratori.
- Se una classe possiede i dati, di solito dovrebbe anche gestire la logica strettamente legata a quei dati.
- Evita commenti che compensano nomi poveri o metodi troppo lunghi.
- Evita liste di parametri lunghe: valuta Parameter Object o Preserve Whole Object.
- Evita primitive obsession quando un dato di dominio ha regole proprie.
- Evita generalita speculativa: rendere il codice modificabile non significa renderlo astratto senza motivo.
- Non accedere direttamente al database dalla business logic se esiste o serve un livello di persistenza.
- Evita Singleton come scelta predefinita: puo mascherare cattivo design e complicare test.
- Mantieni il comportamento esistente quando il task non richiede di cambiarlo.

## Uso di references

Leggi queste reference solo quando utili:

- `references/design-principles.md`: coesione, SRP, accoppiamento, Legge di Demetra, Responsibility-Driven Design, decomposizione e trade-off.
- `references/smells-refactoring.md`: code smells, debito tecnico, ciclo di refactoring e refactoring tipici.
- `references/coupling-examples.md`: esempio `Traveler`/`Vehicle` per ridurre dipendenza concreta.
- `references/Legge di Demetra-examples.md`: esempi di catene di chiamate e incapsulamento.

## Formato di output

Restituisci il risultato in questo formato:

```text
Titolo:

Input usati:

Risultato:

Scelte di design:

Funzionalita:

Testabilita:

Rischi:

Assunzioni:

Controllo finale:
```

Quando produci codice, includi:

- cosa e stato implementato;
- responsabilita delle classi create o modificate;
- come e stata mantenuta alta la coesione;
- come e stato ridotto l'accoppiamento;
- pattern usati, se presenti, e perche;
- input, output, dominio degli input, vincoli e comportamento delle funzioni principali;
- test eseguiti o test da aggiungere;
- debito tecnico introdotto, se presente;
- alternative non scelte quando rilevanti.

## Errori da evitare

- Usare un design pattern solo perche conosciuto.
- Creare interfacce con una sola implementazione senza motivo reale.
- Mischiare business logic, accesso ai dati, formattazione, stampa e UI nella stessa classe.
- Creare classi troppo piccole e inutili solo per applicare SRP.
- Lasciare metodi lunghi con commenti che spiegano il "cosa".
- Passare molti parametri quando un oggetto del dominio e piu chiaro.
- Manipolare dati interni di altri oggetti invece di chiedere all'oggetto di fare il lavoro.
- Aggiungere astrazioni speculative per requisiti futuri non richiesti.
- Cambiare architettura esistente senza motivo.
- Ignorare test e casi limite quando la modifica tocca comportamento importante.

## Controllo finale

Prima di concludere, verifica:

- la modifica soddisfa la richiesta;
- il codice segue lo stile del progetto;
- ogni classe ha responsabilita chiara;
- ogni metodo fa una cosa riconoscibile;
- le dipendenze concrete sono giustificate;
- le catene di chiamate lunghe sono evitate;
- le astrazioni introdotte risolvono un problema reale;
- il codice e testabile;
- eventuali trade-off sono dichiarati;
- non e stato introdotto debito tecnico non segnalato.

## Quick Checklist

```text
[ ] La classe ha una responsabilita chiara?
[ ] Il metodo fa una sola cosa?
[ ] I nomi sono espressivi?
[ ] Ho evitato dipendenze concrete inutili?
[ ] Ho evitato catene di chiamate lunghe?
[ ] Ho evitato parametri troppo numerosi?
[ ] Ho evitato primitive obsession?
[ ] Ho evitato generalita speculativa?
[ ] Il codice e testabile?
[ ] Il pattern usato risolve davvero un problema?
[ ] Eventuale debito tecnico e dichiarato?
```
