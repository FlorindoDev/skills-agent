---

name: blackbox-testing

description: Progetta casi di test black-box modulari a partire da requisiti funzionali, firme di funzioni, API o componenti. Usa questa skill per classi di equivalenza, N-WECT, R-WECT, ACoC, boundary value testing e robustness testing.

---

# Black-Box Test Design Skill

## Goal

Aiutare l’agente a progettare casi di test black-box partendo da requisiti funzionali, firme di funzioni, API, componenti o descrizioni di comportamento atteso.

La skill deve produrre una suite di test ragionata, modulare e adattabile alla tecnica richiesta dall’utente: classi di equivalenza, N-WECT, R-WECT, ACoC, boundary value testing, robustness testing o combinazioni di queste.

## When to use

Usa questa skill quando l’utente chiede di:

- progettare test black-box;
- creare casi di test a partire da requisiti funzionali;
- testare una funzione, API, form, servizio o componente senza basarsi sulla struttura interna del codice;
- individuare classi di equivalenza;
- scegliere una tecnica di testing come N-WECT, R-WECT, ACoC, boundary values o robustness;
- trasformare combinazioni astratte di classi in input concreti;
- scrivere test unitari o casi JUnit/pytest partendo da una progettazione black-box.

Non usare questa skill per testing white-box, code coverage strutturale, branch coverage, path coverage o analisi del CFG, salvo che l’utente chieda esplicitamente un confronto.

## Core principle

Il black-box testing verifica il comportamento esterno del sistema rispetto ai requisiti funzionali.

Non progettare i test partendo dalla struttura interna del codice. Usa invece:

1. requisiti funzionali;
2. input disponibili;
3. output attesi;
4. vincoli del dominio;
5. casi validi, non validi e limite.

## Default behavior

Se l’utente non specifica una tecnica, usa questo default:

1. Functionality-based approach se sono presenti requisiti o regole di dominio.
2. Signature-based approach se è disponibile solo la firma della funzione o dell’API.
3. R-WECT come criterio predefinito quando sono presenti input non validi.
4. N-WECT se il sistema è semplice e gli input sembrano indipendenti.
5. Boundary Value Testing se ci sono intervalli numerici, lunghezze, date, limiti o soglie.
6. ACoC solo se il numero di combinazioni è piccolo o se l’utente vuole copertura forte.

Non presentare tutte le tecniche come equivalenti. Scegli un default motivato e indica brevemente le alternative.

## Workflow

### 1. Identify testable functions

Individua cosa deve essere testato.

Per ogni funzione, endpoint, form o componente, ricava:

- nome della funzionalità;
- comportamento atteso;
- input osservabili;
- output atteso;
- errori o risposte non valide attese;
- precondizioni rilevanti.

Non analizzare la logica interna del codice se non serve a capire la firma o gli input esposti.

### 2. Find all parameters

Elenca tutti i parametri che possono influenzare il comportamento.

Includi:

- parametri formali della funzione;
- campi di un form;
- query/body/path parameters di un endpoint;
- file, configurazioni o database se sono input osservabili;
- stato esterno rilevante se influenza il comportamento.

Per ogni parametro indica:

- tipo;
- dominio ammesso;
- vincoli;
- valori validi;
- valori non validi;
- valore nominale, se esiste.

### 3. Partition the input domain

Dividi ogni dominio in classi di equivalenza.

Ogni classe deve rappresentare un gruppo di valori che il sistema dovrebbe trattare allo stesso modo.

Per intervalli ordinati usa almeno:

- valori validi interni;
- valori sotto il minimo;
- valori sopra il massimo;
- eventuali sottointervalli con significato diverso.

Per enumerazioni usa:

- una classe per ogni valore valido significativo;
- almeno una classe per valore non appartenente all’insieme.

Per booleani usa:

- true;
- false;
- eventuale valore mancante/null se tecnicamente possibile.

### 4. Choose test criterion

Scegli il criterio in base alla richiesta dell’utente o al default.

Criteri supportati:

- N-WECT: coprire ogni classe di equivalenza almeno una volta.
- R-WECT: coprire classi valide e isolare ogni classe non valida in un test separato.
- ACoC / N-SECT: testare tutte le combinazioni delle classi.
- Boundary Value Testing: usare min, min+, nom, max-, max.
- Robustness Testing: usare min-, min, min+, nom, max-, max, max+.
- Pairwise: usare quando ci sono molti parametri e interazioni a coppie plausibili.

Se la scelta produce troppi test, segnala il problema e proponi un criterio più leggero.

### 5. Refine combinations into concrete test inputs

Trasforma le combinazioni astratte in valori concreti.

Ogni caso di test deve avere:

- ID;
- tecnica usata;
- input concreti;
- classi di equivalenza coperte;
- expected result;
- motivazione;
- eventuali note sui valori limite.

Usa valori nominali per gli input non sotto test.

### 6. Apply AAA structure

Quando produci test implementabili, usa la struttura:

- Arrange: prepara input, oggetti, stato o fixture.
- Act: esegui la funzione/API/componente.
- Assert: verifica output, eccezione, stato o messaggio di errore.

## Modular testing modes

### Mode: equivalence-classes

Usalo quando l’utente vuole prima ragionare sulle partizioni.

Output richiesto:

1. tabella parametri;
2. tabella classi di equivalenza;
3. distinzione tra classi valide e non valide;
4. valori rappresentativi.

Non generare subito tutti i test se l’utente chiede solo le classi.

### Mode: n-wect

Usalo quando l’utente vuole una suite minima.

Regole:

- ogni classe di equivalenza deve comparire almeno una volta;
- il numero di test tende alla cardinalità massima tra le caratteristiche;
- combina più classi valide nello stesso test quando possibile;
- segnala che il criterio assume input indipendenti e può perdere bug da interazione.

### Mode: r-wect

Usalo quando ci sono classi non valide importanti.

Regole:

- ogni classe valida deve essere coperta;
- ogni classe non valida deve essere testata in isolamento;
- nei test non validi, un solo parametro deve essere non valido;
- gli altri parametri devono usare valori validi nominali;
- i test non validi isolati non contano come copertura delle classi valide.

### Mode: acoc

Usalo quando l’utente vuole copertura forte o interazioni complete.

Regole:

- genera il prodotto cartesiano delle classi;
- calcola il numero totale di test;
- avvisa se c’è combinatorial explosion;
- proponi Pairwise o R-WECT se il numero è troppo alto.

### Mode: boundary-values

Usalo per intervalli numerici, date, lunghezze, quantità, soglie o range.

Regole:

- per ogni variabile usa min, min+, nom, max-, max;
- varia una variabile alla volta;
- mantieni le altre al valore nominale;
- numero atteso: 4n + 1.

### Mode: robustness

Usalo quando vuoi includere valori fuori limite.

Regole:

- per ogni variabile usa min-, min, min+, nom, max-, max, max+;
- varia una variabile alla volta;
- mantieni le altre al valore nominale;
- numero atteso: 6n + 1.

## Gotchas

- Non confondere black-box testing con code coverage.
- Non usare branch/path coverage come criterio principale: sono tecniche white-box.
- Non assumere complete coverage: per sistemi non banali è impraticabile.
- Non mescolare più input non validi nello stesso test R-WECT.
- Non usare N-WECT quando i parametri sono chiaramente correlati senza segnalarne il limite.
- Non generare ACoC se produce troppi test senza avvisare.
- Per valori limite, non dimenticare il caso nominale con tutte le variabili nominali.
- Per classi non valide, l’expected result deve specificare errore, eccezione, validazione fallita o risposta attesa.
- Se i requisiti sono incompleti, dichiara le assunzioni usate.

## Output format

Quando l’utente chiede una progettazione completa, usa questa struttura:

```markdown
# Black-box test design: [nome funzionalità]

## Requisiti assunti

[Elenco sintetico delle regole funzionali usate]

## Funzione / componente testato

- Nome:
- Descrizione:
- Input:
- Output atteso:
- Vincoli:

## Parametri

| Parametro | Tipo | Dominio | Valore nominale | Note |
|---|---|---|---|---|

## Classi di equivalenza

| ID | Parametro / caratteristica | Classe | Tipo | Valori rappresentativi | Expected behavior |
|---|---|---|---|---|---|

## Criterio scelto

Tecnica: [N-WECT / R-WECT / ACoC / Boundary / Robustness / Pairwise]

Motivazione:
[Spiega brevemente perché questa tecnica è adatta]

## Casi di test

| Test ID | Tecnica | Input | CE coperte | Expected result | Motivazione |
|---|---|---|---|---|---|

## Note finali

[Limiti, assunzioni, eventuali casi da aggiungere]
```

## Validation checklist

Prima di finalizzare, verifica:

- [ ] La suite è black-box e non dipende dalla logica interna.
- [ ] Tutti i parametri osservabili sono stati considerati.
- [ ] Le classi di equivalenza sono disgiunte e coprono il dominio rilevante.
- [ ] Le classi valide e non valide sono distinguibili.
- [ ] Il criterio scelto è coerente con il rischio e il numero di combinazioni.
- [ ] I test non validi sono isolati se si usa R-WECT.
- [ ] I valori limite sono inclusi se ci sono range.
- [ ] Ogni test ha input concreti ed expected result.
- [ ] Le assunzioni sono dichiarate.

## When to load references

Leggi `references/test-criteria.md` quando devi scegliere o confrontare tecniche di test.

Leggi `references/output-template.md` quando devi produrre una tabella finale di test o casi implementabili.
