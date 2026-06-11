# Code smells

Usa questa reference quando devi classificare problemi nel codice prima di scegliere il refactoring.

## Regola di flessibilita

Questa lista non e esaustiva. Se trovi uno smell non presente qui, segnalalo comunque e spiega:

- perche e un problema reale nel codice;
- quale impatto ha su leggibilita, manutenibilita, testabilita o rischio di modifica;
- quale refactoring lo risolve;
- come verificare che il comportamento osservabile resta uguale.

## Bloaters

Codice cresciuto troppo.

### Long Method

Segnali:

- metodo troppo lungo;
- tanti livelli di annidamento;
- commenti per separare blocchi;
- fa piu compiti.

Refactoring:

- Extract Method;
- Replace Temp with Query;
- Introduce Parameter Object se ci sono troppi parametri.

### Large Class

Segnali:

- troppi campi;
- troppi metodi;
- responsabilita diverse;
- nome troppo generico.

Refactoring:

- Extract Class;
- Extract Subclass;
- Move Method;
- Move Field.

### Long Parameter List

Segnali:

- molti parametri primitivi;
- stessi gruppi di parametri ripetuti.

Refactoring:

- Introduce Parameter Object;
- Preserve Whole Object;
- Replace Parameter with Method.

### Data Clumps

Segnali:

- stessi dati viaggiano sempre insieme;
- stessi parametri in molti metodi.

Refactoring:

- Extract Class;
- Introduce Parameter Object.

### Primitive Obsession

Segnali:

- stringhe o interi rappresentano concetti di dominio;
- controlli ripetuti su valori primitivi.

Refactoring:

- Replace Type Code with Class;
- Replace Array with Object;
- Value Object se il dato ha regole proprie.

## Object-Orientation Abusers

Uso debole o scorretto dell'OOP.

### Switch o if complessi

Segnali:

- molte condizioni su tipo/stato;
- stessa struttura condizionale ripetuta;
- aggiungere un caso richiede modifiche in molti punti.

Refactoring:

- Replace Conditional with Polymorphism se la variazione e stabile;
- Factory se lo switch serve solo a creare implementazioni;
- lascia lo switch se e semplice e locale.

### Temporary Field

Segnali:

- campo valorizzato solo in alcuni casi;
- campo serve solo a una fase del calcolo.

Refactoring:

- Extract Class;
- Replace Method with Method Object;
- variabile locale se non serve stato.

### Alternative Classes with Different Interfaces

Segnali:

- classi fanno cose simili con nomi/metodi diversi.

Refactoring:

- Rename Method;
- Extract Interface;
- Adapter se non puoi modificare una classe esterna.

### Refused Bequest

Segnali:

- sottoclasse eredita metodi o dati che non usa;
- gerarchia forza comportamento non coerente.

Refactoring:

- Replace Inheritance with Delegation;
- Push Down Method;
- estrarre interfaccia piu piccola.

## Change Preventers

Codice che rende difficili modifiche future.

### Divergent Change

Una classe cambia per motivi diversi.

Probabile causa:

- violazione SRP;
- responsabilita mischiate.

Refactoring:

- Extract Class;
- Move Method;
- separazione layer.

### Shotgun Surgery

Una modifica richiede piccole modifiche in molti file.

Probabile causa:

- responsabilita dispersa;
- astrazione mancante;
- duplicazione.

Refactoring:

- Move Method;
- Move Field;
- Extract Class;
- centralizzare responsabilita.

### Parallel Inheritance Hierarchies

Ogni nuova sottoclasse obbliga a crearne una parallela altrove.

Refactoring:

- Move Method;
- delegazione;
- fondere gerarchie solo se semplifica davvero.

Nota:

```text
Non sempre eliminare gerarchie parallele migliora codice. Se il tentativo peggiora design, fermarsi.
```

## Dispensables

Elementi inutili o superflui.

### Duplicated Code

Refactoring:

- stessa classe: Extract Method;
- sottoclassi: Extract Method + Pull Up Method;
- algoritmo diverso stesso risultato: Substitute Algorithm.

### Comments

Problema:

- commenti spiegano cosa fa codice confuso.

Refactoring:

- Extract Method;
- Rename Method;
- spezzare espressioni complesse.

Eccezione:

- commento utile se spiega perche una scelta non ovvia esiste.

### Lazy Class

Problema:

- classe con responsabilita troppo piccola o inutile.

Refactoring:

- Inline Class;
- accorpare responsabilita se coerente.

### Data Class

Problema:

- solo campi e getter/setter, nessun comportamento.

Refactoring:

- Encapsulate Field;
- Move Method vicino ai dati;
- distinguere DTO legittimo da dominio anemico.

### Dead Code

Problema:

- codice non piu usato.

Refactoring:

- rimuovere dopo verifica riferimenti;
- rimuovere parametri inutili;
- eliminare file non necessari solo se sicuro.

### Speculative Generality

Problema:

- astrazione creata per futuri requisiti non confermati.

Refactoring:

- rimuovere classi/metodi non usati;
- Inline Class;
- eliminare generalizzazioni inutili.

## Couplers

Problemi di accoppiamento eccessivo.

### Feature Envy

Un metodo usa dati di un altro oggetto piu dei propri.

Refactoring:

- Move Method nella classe che possiede i dati;
- Extract Method se solo una parte del metodo e invidiosa.

### Message Chains

Catene di chiamate lunghe.

Refactoring:

- Hide Delegate;
- Move Method;
- metodo intenzionale sull'oggetto corretto.

### Middle Man

Classe delega quasi tutto senza valore.

Refactoring:

- Remove Middle Man;
- Inline Class se non serve.

### Inappropriate Intimacy

Classi usano dettagli interni una dell'altra.

Refactoring:

- Move Method;
- Move Field;
- Extract Class;
- incapsulare dati.

### Incomplete Library Class

Libreria esterna non modificabile manca metodi utili.

Refactoring:

- Foreign Method per piccole aggiunte;
- Local Extension o wrapper per modifiche maggiori.
