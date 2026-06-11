---
name: refactoring
description: Use this skill when reviewing existing code to identify code smells, evaluate cohesion and coupling, and propose safe refactoring steps without changing observable behavior.
---

## Goal

Migliorare la struttura interna di codice già esistente senza modificarne il comportamento osservabile.

L’agente deve analizzare il codice, identificare problemi di design o code smells, scegliere refactoring piccoli e sicuri, e spiegare perché ogni modifica migliora la qualità interna.

La skill deve aiutare l’agente a:

- capire il comportamento attuale prima di cambiare il codice;
- individuare responsabilità poco chiare;
- riconoscere problemi di coesione e accoppiamento;
- identificare code smells;
- scegliere il refactoring più adatto;
- evitare riscritture inutilmente grandi;
- preservare il comportamento esterno;
- verificare il risultato con test quando possibile.

L’obiettivo non è aggiungere nuove funzionalità, ma rendere il codice più leggibile, mantenibile, testabile e meno fragile ai cambiamenti.

## When to use

Usa questa skill quando:

- devi analizzare codice esistente;
- devi migliorare la struttura interna del codice;
- devi fare refactoring senza cambiare il comportamento osservabile;
- devi identificare code smells;
- devi valutare coesione, accoppiamento o responsabilità delle classi;
- devi capire se una classe viola SRP;
- devi ridurre duplicazione, metodi lunghi o classi troppo grandi;
- devi ridurre catene di chiamate, Feature Envy o dipendenze troppo forti;
- devi proporre un piano di refactoring sicuro;
- devi applicare piccoli refactoring incrementali;
- devi valutare il debito tecnico di una parte di codice;
- devi decidere se introdurre un pattern per risolvere un problema di design già presente.

## Review Procedure


### 1. Capisci il comportamento attuale

Prima di proporre refactoring, capisci cosa fa il codice.

Domande:

- qual è lo scopo del modulo?
- quali sono gli input?
- quali sono gli output?
- quali classi collaborano?
- quali parti sono business logic?
- quali parti sono infrastruttura, persistenza, UI o formattazione?

Non proporre modifiche strutturali se non hai capito il comportamento.

---

### 2. Identifica responsabilità e confini

Per ogni classe importante, scrivi:

```text
Classe:
Responsabilità principale:
Responsabilità secondarie:
Collaboratori:
Possibili motivi per cambiare:
```

Se trovi più motivi per cambiare, segnala una possibile violazione di SRP.

---

### 3. Controlla coesione

Cerca:
- metodi troppo lunghi;
- classi troppo grandi;
- responsabilità mischiate;
- nomi poco chiari;
- metodi che richiedono molti commenti;
- logica non collegata allo scopo principale della classe.

Suggerisci:
- Extract Method;
- Extract Class;
- rinomina;
- spostamento della logica nella classe più coerente.
- oppure un altro refactoring più adatto, motivando perché è preferibile.

---

### 4. Controlla accoppiamento

Cerca:
- dipendenze dirette da classi concrete;
- classi che accedono ai dettagli interni di altre;
- catene di chiamate lunghe;
- troppi collaboratori;
- dipendenza diretta dal database in molte classi;
- metodi che passano troppi dati primitivi.

Suggerisci:

- interfacce;
- dependency injection;
- factory solo quando serve;
- DAO o repository per isolare la persistenza;
- spostamento della logica vicino ai dati;
- applicazione della Legge di Demetra.
- DTO  


---

### 5. Cerca code smells

Classifica i problemi trovati in queste categorie.

#### Bloaters

Codice cresciuto troppo.

Cerca:

- Long Method;
- Large Class;
- Long Parameter List;
- Data Clumps;
- Primitive Obsession.

Refactoring tipici:
- Extract Method;
- Extract Class;
- Introduce Parameter Object;
- Preserve Whole Object;
- Replace Type Code with Class;
- Replace Array with Object.

---

#### Object-Orientation Abusers

Uso incompleto o scorretto dell'OOP.

Cerca:

- switch complessi;
- sequenze lunghe di if;
- Temporary Field;
- Alternative Classes with Different Interfaces;
- Refused Bequest.

Refactoring tipici:

- sostituire switch complessi con polimorfismo, se ha senso;
- Extract Class;
- Rename Method;
- Extract Superclass;
- Replace Inheritance with Delegation.

Nota:

Non eliminare sempre gli switch. Uno switch semplice può essere accettabile. Gli switch usati dentro una Factory possono essere legittimi.

---

#### Change Preventers

Codice che rende difficili le modifiche future.

Cerca:
- Divergent Change;
- Shotgun Surgery;
- Parallel Inheritance Hierarchies.

Interpretazione:

```text
Divergent Change:
Una classe cambia spesso per motivi diversi.
Probabile violazione di SRP.

Shotgun Surgery:
Una singola modifica richiede piccole modifiche in tante classi.
Probabile responsabilità dispersa.

Parallel Inheritance Hierarchies:
Ogni nuova sottoclasse obbliga a creare una sottoclasse parallela altrove.
Probabile duplicazione strutturale.
```

Refactoring tipici:

- Extract Class;
- Move Method;
- Move Field;
- Inline Class;
- Extract Superclass;
- delegazione.

---

#### Dispensables

Elementi inutili o superflui.

Cerca:

- codice duplicato;
- codice morto;
- Lazy Class;
- Data Class;
- commenti ridondanti;
- generalità speculativa.

Refactoring tipici:
- rimuovere codice morto;
- Extract Method;
- Inline Class;
- Encapsulate Field;
- rimuovere astrazioni inutilizzate;
- rinominare metodi invece di commentare troppo.

Regola sui commenti:

```text
Un commento che spiega il "perché" può essere utile.
Un commento che spiega "cosa fa" codice confuso spesso indica bisogno di refactoring.
```

---

#### Couplers

Problemi di accoppiamento eccessivo.

Cerca:
- Feature Envy;
- Message Chains;
- Middle Man;
- Inappropriate Intimacy;
- Incomplete Library Class.

Refactoring tipici:
- Move Method;
- Move Field;
- Extract Method;
- rimuovere intermediari inutili;
- introdurre metodi più espressivi;
- local extension o foreign method per librerie incomplete.


#### Qualsiasi altro smells

Se trovi altri smell non presenti nella lista, segnalali e spiega perché sono rilevanti.


### 6. Scegli il refactoring

Il refactoring deve migliorare la struttura interna senza modificare il comportamento osservabile.

Procedura:

```text
1. Identifica il code smell più grave.
2. Scegli il refactoring più adatto.
3. Applica una modifica piccola.
4. Verifica che il comportamento non sia cambiato.
5. Ripeti.
```

Non proporre refactoring enormi se bastano piccoli passi.

---

### 7. Verifica con test quando possibile

Prima di refactor pesanti, controlla se ci sono test.

Se ci sono test:

```text
- eseguili prima;
- applica il refactoring;
- eseguili dopo;
- segnala eventuali fallimenti.
```

Se non ci sono test:

```text
- segnala il rischio;
- suggerisci test minimi;
- evita refactoring troppo invasivi;
- procedi con modifiche piccole e localizzate.
```

Regola:

> Più il refactoring è strutturale, più i test diventano importanti.

---


## Output Format

Se il task richiede solo analisi, restituisci una review.

Se il task richiede modifiche al codice, restituisci: 

```
## Changes Applied

- File modificati.
- Refactoring applicati.
- Comportamento preservato.

## Design Improvements

- Coesione migliorata.
- Accoppiamento ridotto.
- Responsabilità chiarite.

## Verification

- Test eseguiti.
- Test mancanti.
- Rischi residui.
```


---

## Constraints

- Non cambiare il comportamento osservabile del programma durante il refactoring.
- Non proporre design pattern senza aver prima identificato il problema.
- Non introdurre astrazioni inutili.
- Non generalizzare per requisiti futuri non confermati.
- Non modificare codice non correlato.
- Non riscrivere tutto se basta un refactoring locale.
- Non confondere qualità del codice con sola performance.
- Non eliminare codice senza verificare se è usato.
- Non applicare SRP in modo estremo creando classi troppo piccole e inutili.
- Non introdurre Singleton come soluzione di default.
- Non sostituire ogni switch con polimorfismo: valuta prima se lo switch è davvero complesso o fragile.
- Se mancano test, segnala il rischio prima di refactoring importanti.

## Quick Checklist

Quando analizzi codice, controlla sempre:

```text
[ ] Ogni classe ha una responsabilità chiara?
[ ] Ogni metodo fa una cosa sola?
[ ] I nomi sono espressivi?
[ ] Ci sono metodi troppo lunghi?
[ ] Ci sono classi troppo grandi?
[ ] Ci sono liste di parametri troppo lunghe?
[ ] Ci sono gruppi di dati ripetuti?
[ ] Ci sono primitive che dovrebbero essere oggetti?
[ ] Ci sono switch/if complessi?
[ ] Ci sono catene tipo a.getB().getC()?
[ ] Una modifica richiede cambiamenti in tanti file?
[ ] Una classe cambia per motivi diversi?
[ ] Ci sono dipendenze concrete evitabili?
[ ] La business logic accede direttamente al database?
[ ] Ci sono commenti che nascondono codice poco chiaro?
[ ] Ci sono duplicazioni?
[ ] Ci sono classi inutili o troppo generiche?
[ ] I pattern usati risolvono davvero un problema?
[ ] Esistono test prima di refactor importanti?
```


