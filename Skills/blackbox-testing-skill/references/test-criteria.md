# Black-box test criteria reference

## Equivalence Classes

Usa le classi di equivalenza per dividere il dominio degli input in gruppi trattati allo stesso modo dal sistema.

Esempio per un input `age` valido tra 18 e 65:

| CE | Tipo | Descrizione | Valori |
|---|---|---|---|
| CE1 | valida | età valida | 18..65 |
| CE2 | non valida | sotto il minimo | <18 |
| CE3 | non valida | sopra il massimo | >65 |

## Signature-based approach

Usa questo approccio quando conosci soprattutto la firma della funzione.

Esempio:

```java
checkTriangle(int s1, int s2, int s3)
```

Caratteristiche:

- s1
- s2
- s3

Classi possibili per ogni lato:

- > 0
- = 0
- < 0

È semplice, ma può perdere informazioni sul dominio del problema.

## Functionality-based approach

Usa questo approccio quando conosci le regole funzionali.

Esempio triangolo:

| CE | Descrizione |
|---|---|
| CE1 | scaleno |
| CE2 | equilatero |
| CE3 | isoscele |
| CE4 | non valido |

È più efficace quando il comportamento dipende da relazioni tra input.

## N-WECT

Obiettivo: ogni classe di equivalenza deve apparire almeno una volta.

Numero di test:

```text
max(numero di CE tra le caratteristiche)
```

Usalo per suite minima e input indipendenti.

Limite: può perdere bug dovuti a interazioni tra parametri.

## R-WECT

Obiettivo:

1. coprire le classi valide;
2. testare ogni classe non valida in isolamento.

Numero di test:

```text
max(numero di CE valide tra le caratteristiche) + numero totale di CE non valide
```

Regola importante: in un test non valido deve esserci un solo valore non valido.

## ACoC / N-SECT

Obiettivo: testare tutte le combinazioni delle classi.

Numero di test:

```text
CE_param1 × CE_param2 × ... × CE_paramN
```

Usalo quando:

- i parametri sono correlati;
- il numero di combinazioni è piccolo;
- serve copertura forte.

Limite: combinatorial explosion.

## Boundary Value Testing

Per ogni variabile ordinata usa:

```text
min, min+, nom, max-, max
```

Numero di test:

```text
4n + 1
```

dove `n` è il numero di variabili.

## Robustness Testing

Per ogni variabile ordinata usa:

```text
min-, min, min+, nom, max-, max, max+
```

Numero di test:

```text
6n + 1
```

Usalo quando vuoi testare anche valori appena fuori dal dominio valido.
