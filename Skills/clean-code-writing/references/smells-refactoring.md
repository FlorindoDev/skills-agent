# Smells and refactoring

Usa questa reference quando il codice nuovo rischia di introdurre cattivi odori o quando una modifica richiede micro-refactoring sicuro.

## Regola di flessibilita

Questa lista non e esaustiva. Usa queste tecniche come riferimento principale, ma se trovi uno smell, un micro-refactoring o un refactoring piu adatto al codice reale, usalo e spiega:

- quale smell risolve;
- perche e migliore delle tecniche elencate;
- come preserva il comportamento gia esistente;
- come verificarlo con test.

## Debito tecnico

Debito tecnico: codice che soddisfa i requisiti funzionali ma e subottimale.

Esempi:

- codice con cattivi odori;
- algoritmi inefficienti;
- design approssimativo;
- test insufficienti;
- implementazione troppo complessa o troppo rapida.

Debito strategico:

```text
Scelta intenzionale per spedire prima, con piano di rimborso.
```

Debito non strategico:

```text
Accumulo involontario causato da processi imperfetti, fretta o design non chiaro.
```

Conseguenze:

- sviluppo futuro piu lento;
- bug piu frequenti e costosi;
- pianificazione meno prevedibile;
- maggiore fatica di manutenzione.

## Ciclo di refactoring

Usa il ciclo solo su programma funzionante:

1. Identifica il cattivo odore piu grave.
2. Scegli un refactoring mirato.
3. Applica una modifica piccola.
4. Esegui i test.
5. Ripeti.

Regola:

```text
Il refactoring cambia struttura, non comportamento osservabile.
```

Senza test, procedi con modifiche piu piccole e segnala il rischio.

## Elementi dispensabili

### Commenti inutili

Problema:

- commenti ridondanti;
- commenti che spiegano codice poco chiaro;
- commenti usati per compensare nomi poveri.

Soluzione:

- Extract Method;
- rinominare metodo o variabile;
- spezzare espressioni complesse.

Eccezione:

- commenti che spiegano il perche di una scelta non ovvia.

### Codice duplicato

Problema:

- espressioni uguali o molto simili in piu punti.

Soluzioni:

- stessa classe: Extract Method;
- sottoclassi: Extract Method + Push Method Up;
- algoritmi diversi per stesso risultato: Substitute Algorithm quando uno e migliore.

### Lazy Class

Problema:

- classe con poche responsabilita o eliminabile senza impatti reali.

Soluzioni:

- aggiungere responsabilita coerente se esiste;
- Inline Class;
- accorpare con classe vicina.

### Speculative Generality

Problema:

- codice astratto o generico creato per futuri requisiti non reali.

Soluzioni:

- rimuovere classi non usate;
- rimuovere metodi non usati;
- eliminare generalizzazioni inutili;
- mantenere solo estensioni motivate.

### Data Class

Problema:

- classe con soli dati e nessun comportamento significativo.

Soluzioni:

- incapsulare campi;
- spostare comportamento vicino ai dati;
- usare DTO solo ai confini tra layer o processi;
- non trasformare tutto il dominio in contenitori passivi.

### Dead Code

Problema:

- variabile, parametro, campo, metodo, classe o file non usato.

Soluzioni:

- rimuovere parametro;
- eliminare codice inutilizzato;
- verificare test e riferimenti prima di cancellare.

## Smells di accoppiamento

### Feature Envy

Problema:

- un metodo usa piu dati di un altro oggetto che della propria classe.

Soluzioni:

- Move Method verso la classe che possiede i dati;
- Extract Method per separare la parte invidiosa;
- tenere insieme cose che cambiano insieme.

### Message Chains

Problema:

- lunghe catene di chiamate.

Soluzione:

- applicare Legge di Demetra;
- introdurre metodo sull'oggetto piu vicino al dato.

### Middle Man

Problema:

- classe che delega quasi tutto senza aggiungere valore.

Soluzione:

- Remove Middle Man;
- chiamare direttamente il collaboratore quando non rompe l'incapsulamento.

### Inappropriate Intimacy

Problema:

- una classe usa campi o dettagli interni di un'altra.

Soluzioni:

- Move Method;
- Move Field;
- nascondere dettagli con metodi intenzionali.

### Incomplete Library Class

Problema:

- libreria esterna non modificabile non offre il comportamento necessario.

Soluzioni:

- Foreign Method per piccole aggiunte;
- Local Extension o wrapper per cambiamenti maggiori.

## Refactoring tipici

Metodi:

- Extract Method;
- Rename Method;
- Add Parameter;
- Replace Parameter with Method;
- Replace Temp with Query;
- Push Method Up;
- Push Method Down;
- Move Method.

Classi:

- Extract Class;
- Inline Class;
- Preserve Whole Object;
- Add subclass;
- Rename Class;
- Remove Class.

Attributi:

- Rename Variable;
- Encapsulate Field;
- Push Field Up/Down;
- Replace Array with Object.

## Esempi rapidi

Extract Method:

```java
void printOwing() {
    printBanner();
    printDetails(getOutstanding());
}

void printDetails(double outstanding) {
    System.out.println("name: " + name);
    System.out.println("amount " + outstanding);
}
```

Preserve Whole Object:

```java
boolean withinPlan = plan.withinRange(daysTempRange);
```

Replace Array with Object:

```java
Performance row = new Performance();
row.setName("Liverpool");
row.setWins("15");
```
