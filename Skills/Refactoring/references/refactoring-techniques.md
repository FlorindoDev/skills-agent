# Refactoring techniques

Usa questa reference quando hai gia identificato uno smell e devi scegliere una tecnica.

## Regola di flessibilita

Questa lista non e esaustiva. Usa queste tecniche come riferimento principale, ma se trovi un refactoring piu adatto al codice reale, usalo e spiega:

- quale smell risolve;
- perche e migliore delle tecniche elencate;
- come preserva il comportamento osservabile;
- come verificarlo con test.

## Metodo

### Extract Method

Usa quando:

- metodo troppo lungo;
- blocco commentato dentro metodo;
- logica ripetuta;
- espressione complessa.

Prima:

```java
void printOwing() {
    printBanner();
    System.out.println("name: " + name);
    System.out.println("amount " + getOutstanding());
}
```

Dopo:

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

### Inline Method

Usa quando:

- metodo delega soltanto;
- nome non aggiunge significato;
- astrazione e inutile.

### Move Method

Usa quando:

- metodo usa piu dati di un'altra classe che della propria;
- comportamento sta lontano dai dati;
- vuoi ridurre Feature Envy.

### Rename Method

Usa quando:

- nome non comunica intenzione;
- serve commento per capire il metodo.

### Add Parameter

Usa quando:

- metodo ha bisogno di informazione dal chiamante;
- il parametro non crea lista troppo lunga.

### Remove Parameter

Usa quando:

- parametro non usato;
- parametro e derivabile dall'oggetto.

### Replace Parameter with Method

Usa quando:

- chiamante passa un valore che il metodo puo calcolare o ottenere.

### Replace Temp with Query

Usa quando:

- variabile temporanea impedisce Extract Method;
- calcolo puo essere espresso come metodo.

## Classe

### Extract Class

Usa quando:

- classe ha responsabilita diverse;
- gruppi di campi/metodi cambiano insieme;
- classe ha troppi motivi per cambiare.

### Inline Class

Usa quando:

- classe non fa abbastanza;
- classe e solo passaggio inutile;
- responsabilita puo stare in classe vicina.

### Preserve Whole Object

Usa quando:

- codice estrae molti valori da un oggetto e li passa a un metodo.

Prima:

```java
int low = range.getLow();
int high = range.getHigh();
boolean ok = plan.withinRange(low, high);
```

Dopo:

```java
boolean ok = plan.withinRange(range);
```

### Extract Superclass

Usa quando:

- classi condividono comportamento comune reale;
- duplicazione e stabile;
- non crei ereditarieta speculativa.

### Replace Inheritance with Delegation

Usa quando:

- sottoclasse non e davvero un tipo della superclasse;
- eredita metodi che rifiuta;
- gerarchia crea accoppiamento forte.

## Attributi e dati

### Encapsulate Field

Usa quando:

- campo pubblico o manipolato da troppi punti;
- vuoi proteggere invarianti.

### Move Field

Usa quando:

- campo e usato soprattutto da un'altra classe;
- campo appartiene concettualmente a un altro oggetto.

### Replace Array with Object

Usa quando:

- array contiene dati di significato diverso.

Prima:

```java
String[] row = new String[2];
row[0] = "Liverpool";
row[1] = "15";
```

Dopo:

```java
Performance row = new Performance();
row.setName("Liverpool");
row.setWins("15");
```

### Introduce Parameter Object

Usa quando:

- stesso gruppo di parametri ricorre spesso;
- parametri formano un concetto unico.

## Gerarchie

### Pull Up Method

Usa quando:

- sottoclassi hanno metodo uguale o quasi uguale;
- comportamento appartiene alla superclasse.

### Push Down Method

Usa quando:

- metodo della superclasse serve solo ad alcune sottoclassi.

### Pull Up Field

Usa quando:

- sottoclassi hanno stesso campo con stesso significato.

### Push Down Field

Usa quando:

- campo della superclasse serve solo ad alcune sottoclassi.

## Algoritmi

### Substitute Algorithm

Usa quando:

- due algoritmi producono stesso risultato;
- uno e piu semplice, efficiente o leggibile;
- test dimostrano equivalenza.

## Scelta rapida

```text
Long Method -> Extract Method
Large Class -> Extract Class
Feature Envy -> Move Method
Message Chain -> Hide Delegate / Move Method
Duplicated Code -> Extract Method / Pull Up Method
Lazy Class -> Inline Class
Data Class -> Move Method / Encapsulate Field
Long Parameter List -> Introduce Parameter Object / Preserve Whole Object
Primitive Obsession -> Replace Type Code with Class / Value Object
Refused Bequest -> Replace Inheritance with Delegation
```
