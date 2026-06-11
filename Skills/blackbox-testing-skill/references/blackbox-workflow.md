# Black-box workflow

Usa questa reference quando devi impostare processo completo di progettazione black-box.

## Complete coverage e limite pratico

Per moduli non banali non e realistico testare tutto.

Motivi:

- limitazioni teoriche;
- tempi e costi proibitivi;
- numero enorme di input;
- combinazioni tra parametri.

Regola:

```text
Il testing puo mostrare presenza di bug, non garantirne assenza.
```

Obiettivo black-box: scegliere casi di test rappresentativi, non pretendere complete coverage.

## Black-box testing

Black-box testing verifica comportamento esterno del sistema senza usare implementazione interna.

Usa:

- requisiti funzionali;
- input osservabili;
- output attesi;
- vincoli del dominio;
- classi valide, non valide e limite.

Non usare:

- branch coverage;
- path coverage;
- CFG;
- dettagli interni del codice come criterio principale.

## Workflow in 5 passi

1. Identify testable functions.
2. Find all parameters.
3. Partition input domain.
4. Apply test criterion.
5. Refine combinations into concrete test inputs.

## 1. Identify testable functions

Identifica funzioni o caratteristiche del sistema che devono essere testate.

Per ogni elemento, ricava:

- nome;
- comportamento atteso;
- input osservabili;
- output atteso;
- errori attesi;
- precondizioni rilevanti.

Esempio calcolatrice:

- addizione;
- sottrazione;
- moltiplicazione;
- divisione.

## 2. Find all parameters

Trova tutti i parametri che influenzano comportamento.

Fonti:

- parametri formali di metodi o funzioni;
- campi di form;
- path/query/body parameter di API;
- variabili di stato osservabili;
- file;
- configurazioni;
- database o dati persistenti se influenzano output;
- interazioni con altri sistemi, se osservabili.

Per ogni parametro annota:

- tipo;
- dominio;
- valori validi;
- valori non validi;
- vincoli;
- valore nominale.

## 3. Partition input domain

Dividi dominio input in classi di equivalenza.

Una classe di equivalenza e un insieme di valori che il sistema dovrebbe trattare allo stesso modo.

Regole:

- classi disgiunte;
- copertura del dominio rilevante;
- separazione tra valido e non valido;
- classi diverse se comportamento atteso cambia.

## Enumerazioni

Per insiemi discreti:

- una classe valida per ogni valore significativo;
- una classe non valida per valore fuori insieme;
- per booleani: `true`, `false`, eventuale `null/missing` se tecnicamente possibile.

Esempio semaforo:

```text
CE1 = rosso valida
CE2 = giallo valida
CE3 = verde valida
CE4 = blu non valida
```

## Intervalli

Per intervalli ordinati:

- classe valida interna;
- classe sotto minimo;
- classe sopra massimo;
- sottointervalli separati se producono comportamento diverso.

Esempio voto 0..30:

```text
CE1 = 18..30 valido, esame superato
CE2 = 0..17 valido, esame non superato
CE3 = <0 non valido
CE4 = >30 non valido
```

## Signature-based approach

Usa quando hai soprattutto firma funzione/API.

Focus:

- parametri individuali;
- tipi;
- dominio semplice;
- valori validi/non validi dedotti dalla firma.

Pro:

- semplice;
- veloce;
- parzialmente meccanico.

Contro:

- puo perdere comportamento di dominio;
- puo perdere relazioni tra input.

Esempio:

```java
checkTriangle(int s1, int s2, int s3)
```

Classi base per ogni lato:

```text
>0
=0
<0
```

## Functionality-based approach

Usa quando hai requisiti o regole di dominio.

Focus:

- comportamento atteso;
- validita nel dominio;
- relazioni tra input;
- output distinti.

Pro:

- test piu mirati;
- migliore per sistemi complessi;
- riduce test inutili.

Contro:

- richiede piu analisi;
- dipende da requisiti chiari.

Esempio triangolo:

```text
CE1 = scaleno
CE2 = equilatero
CE3 = isoscele
CE4 = non valido
```

## 4. Apply test criterion

Dopo classi di equivalenza, scegli criterio:

- N-WECT per suite minima;
- R-WECT per invalidi isolati;
- ACoC/N-SECT per combinazioni complete;
- Pairwise per molte combinazioni con rischio interazioni a coppie;
- Boundary per intervalli;
- Robustness per valori fuori range.

## 5. Refine combinations into test inputs

Trasforma combinazioni in input concreti.

Ogni test deve avere:

- ID;
- tecnica;
- input concreti;
- classi coperte;
- expected result;
- motivazione.

Usa valori nominali per parametri non sotto test.

## AAA

Per test implementabili usa:

```text
Arrange: prepara input, oggetti, stato.
Act: esegui funzione/API/componente.
Assert: verifica output, errore o stato.
```
