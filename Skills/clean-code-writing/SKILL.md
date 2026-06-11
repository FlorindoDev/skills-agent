---

name: clean-code-writing

description: Use this skill when writing new code, implementing features, adding classes or methods, designing modules, or modifying existing code while keeping it clean, cohesive, low-coupled, maintainable, and testable.

---

# Code Quality Review Skill

## Goal

Scrivere codice nuovo che sia pulito, leggibile, mantenibile, testabile e facile da modificare.

L’agente deve produrre codice che non si limiti a funzionare, ma che rispetti buoni principi di progettazione:

- alta coesione;
- basso accoppiamento;
- responsabilità chiare;
- metodi piccoli e nominati bene;
- classi con un solo motivo per cambiare;
- dipendenze facili da sostituire o testare;
- niente astrazioni inutili;
- niente pattern usati senza un problema reale.

L’obiettivo principale è prevenire debito tecnico mentre si implementano nuove funzionalità.

---

## When to use this skill

Usa questa skill quando il task riguarda:

- scrittura di nuovo codice;
- implementazione di una nuova feature;
- aggiunta di classi, metodi, moduli o componenti;
- modifica di codice esistente per aggiungere nuovo comportamento;
- scelta di dove collocare una nuova responsabilità;
- progettazione di una piccola architettura interna;
- scelta tra classe concreta, interfaccia, dependency injection, DTO, DAO/Repository o Factory;
- scrittura di codice che deve essere facile da testare;
- prevenzione di code smells, accoppiamento inutile o generalità speculativa.

---

## Workflow

Quando scrivi codice nuovo, segui questa sequenza:

1. Identifica la responsabilità principale del codice da aggiungere.
2. Cerca nel progetto codice simile e segui lo stile esistente se è corretto.
3. Decidi dove collocare la nuova responsabilità.
4. Scrivi la soluzione più semplice che rispetta coesione e basso accoppiamento.
5. Evita astrazioni, pattern o interfacce se non risolvono un problema reale.
6. Rendi il codice testabile separando logica pura, I/O e dipendenze esterne.
7. Prima di finalizzare, controlla la checklist della skill.


## Core Principles

### 1. Alta coesione

Una classe o un metodo deve avere responsabilità strettamente correlate tra loro.

Controlla sempre:

- il metodo fa una sola cosa?
- la classe rappresenta un singolo concetto?
- le responsabilità sono mirate allo stesso obiettivo?
- il nome della classe o del metodo descrive chiaramente ciò che fa?

Se un metodo o una classe fa troppe cose, probabilmente viola la coesione.

Segnali negativi:

- metodo troppo lungo;
- classe troppo grande;
- nome generico;
- commenti necessari per spiegare troppe sezioni;
- responsabilità non correlate nella stessa classe.

Refactoring suggeriti:

- Extract Method;
- Extract Class;
- Extract Subclass;
- rinominare metodi o classi;
- spostare responsabilità nella classe corretta.

---

### 2. Single Responsibility Principle

Una classe dovrebbe avere una sola responsabilità.

Regola pratica:

> Una responsabilità è un motivo per cambiare.

Controlla:

- questa classe cambia per più motivi diversi?
- contiene logica di business, accesso ai dati, formattazione e stampa insieme?
- gestisce responsabilità che dovrebbero stare in classi diverse?
- una modifica piccola obbliga a cambiare una classe enorme?

Se sì, suggerisci una decomposizione.

Esempio di ragionamento:

```text
Problema:
La classe Report carica dati, formatta il report e lo stampa.

Violazione:
Ha almeno tre motivi per cambiare:
1. cambia il modo in cui recupero i dati;
2. cambia il formato del report;
3. cambia il modo in cui stampo.

Soluzione:
Separare in:
- Report
- ReportFormatter
- ReportPrinter
- eventualmente ReportRepository/DataAccess
```


---

### 3. Basso accoppiamento

Il codice deve evitare dipendenze troppo forti tra classi concrete.

Controlla:

- una classe istanzia direttamente un'altra classe concreta?
- una classe conosce troppi dettagli interni di un'altra?
- cambiare una classe obbliga a modificarne molte altre?
- una classe non può essere riusata senza portarsi dietro troppe dipendenze?
- il codice dipende da implementazioni concrete invece che da interfacce?

---

### 4. Legge di Demetra

Evita catene di chiamate lunghe.

Regola:

Un metodo dovrebbe comunicare solo con:
- this;
- attributi di this;
- parametri del metodo;
- oggetti creati dentro il metodo.


---

### 5. Responsibility-Driven Design

Quando analizzi una classe, ragiona sempre in termini di:

```text
Classe
Responsabilità
Collaboratori
```

Per ogni classe chiediti:

```text
Nome classe:
Responsabilità:
Collaboratori:
```

Se non riesci a specificare chiaramente le responsabilità, probabilmente c'è un errore di design.

Se una classe ha troppi collaboratori, probabilmente è troppo accoppiata o fa troppe cose.

Template di analisi:

```text
Classe: OrderService

Responsabilità:
- validare un ordine;
- calcolare il totale;
- inviare l'ordine al repository.

Collaboratori:
- OrderRepository;
- PaymentService;
- DiscountPolicy.

Valutazione:
Se OrderService inizia anche a formattare PDF, mandare email e gestire logica UI, allora sta violando SRP.
```

### 6. Scrivi metodi piccoli e nominati bene

Quando scrivi un metodo:

- deve avere uno scopo chiaro;
- deve avere un nome comunicativo;
- deve evitare troppe istruzioni;
- deve evitare troppi livelli di annidamento;
- deve evitare commenti necessari per capire il “cosa”.

Se un metodo diventa lungo, dividilo subito con Extract Method.

---

### 7. Evita liste di parametri lunghe

Se un metodo riceve troppi parametri, valuta:
- Introduce Parameter Object;
- Preserve Whole Object;
- passare un oggetto che contiene quei dati;
- spostare il metodo nella classe che possiede quei dati.

Sbagliato:

```java
createUser(String name, String surname, String email, String phone, String city)
```

Meglio:

```java
createUser(UserData data)
```

---

### 8. Evita primitive obsession

Non usare sempre `String`, `int`, `boolean` per concetti importanti del dominio.

Esempio:

```java
String phoneNumber;
String email;
int role;
```

Meglio, quando ha senso:

```java
PhoneNumber phoneNumber;
Email email;
UserRole role;
```

Regola:

```text
Se un dato ha regole proprie, probabilmente merita un tipo proprio.
```

---

### 9. Non introdurre generalità speculativa

Non creare astrazioni solo perché “potrebbero servire in futuro”.

Evita:
- interfacce con una sola implementazione senza motivo;
- factory inutili;
- classi astratte non necessarie;
- configurazioni troppo generiche;
- pattern usati solo per eleganza.

Regola:

```text
Anticipare il cambiamento significa rendere il codice modificabile,
non renderlo inutilmente astratto.
```

---

### 10. Usa i design pattern solo se servono

Prima di usare un pattern, verifica:

```text
Problema reale:
Perché serve un pattern:
Alternative più semplici:
Pattern scelto:
Costo in complessità:
```

Usa Factory se vuoi separare creazione e uso degli oggetti.

Usa DAO/Repository se vuoi isolare la persistenza.

Usa Observer se più oggetti devono reagire a un cambiamento di stato.

Evita Singleton come soluzione predefinita.

---

### 11. Scrivi codice testabile

Mentre scrivi codice nuovo:

- separa logica pura da I/O;
- evita dipendenze globali;
- evita static non necessari;
- evita Singleton se rende difficile il mock;
- inietta dipendenze esterne;
- crea metodi piccoli verificabili;
- aggiungi test per comportamento importante.

---

## Constraints

- Non scrivere codice inutilmente complesso.
- Non introdurre pattern senza problema reale.
- Non mischiare responsabilità diverse.
- Non accedere direttamente al database dalla business logic se esiste un livello di persistenza.
- Non usare commenti per compensare nomi poco chiari.
- Non creare classi troppo piccole e inutili solo per applicare SRP.
- Non cambiare architettura esistente senza motivo.
- Segui lo stile già presente nel progetto.

---

## Output Format

Quando usi questa skill per scrivere codice, restituisci:

```md
## Implementazione

Descrizione breve di cosa è stato implementato.

## Scelte di design

- Responsabilità delle classi create/modificate.
- Come è stata mantenuta alta la coesione.
- Come è stato ridotto l’accoppiamento.
- Pattern usati, se presenti, e perché.

## funzionalità
descrivere funzionalità di ogni funzione/classe scritta e scrivere se è possibile: 

- input
- output
- Dominio dei vari input 
- eventuali vincoli
- Cosa dovrebbe fare

## Codice

Codice prodotto o patch.

## Testabilità

- Come testare il codice.
- Eventuali test aggiunti.
- Eventuali casi limite da coprire.

## Rischi

- Debito tecnico introdotto, se presente.
- Alternative non scelte.
```

---

## Quick Checklist

```text
[ ] La classe ha una responsabilità chiara?
[ ] Il metodo fa una sola cosa?
[ ] I nomi sono espressivi?
[ ] Ho evitato dipendenze concrete inutili?
[ ] Ho evitato catene di chiamate lunghe?
[ ] Ho evitato parametri troppo numerosi?
[ ] Ho evitato primitive obsession?
[ ] Ho evitato generalità speculativa?
[ ] Il codice è testabile?
[ ] Il pattern usato risolve davvero un problema?
```
