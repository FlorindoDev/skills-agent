# Black-box test criteria

Usa questa reference quando devi scegliere, confrontare o applicare criteri di test black-box.

## Regola di flessibilita

Questi criteri sono riferimenti principali, non una lista chiusa. Se dominio o requisiti richiedono una tecnica black-box non presente qui, usala e spiega:

- quale rischio copre;
- perche e piu adatta dei criteri elencati;
- quali input o classi copre;
- quale risultato atteso verifica.

## Equivalence classes

Dividi dominio input in classi trattate allo stesso modo dal sistema.

Esempio `age` valido tra 18 e 65:

| CE | Tipo | Descrizione | Valori |
|---|---|---|---|
| CE1 | valida | eta valida | 18..65 |
| CE2 | non valida | sotto minimo | <18 |
| CE3 | non valida | sopra massimo | >65 |

## N-WECT

Obiettivo: ogni classe di equivalenza deve comparire almeno una volta.

Numero di test:

```text
max(numero di CE tra le caratteristiche)
```

Usalo quando:

- vuoi suite minima;
- input sembrano indipendenti;
- rischio interazioni e basso.

Limite:

- puo perdere bug dovuti a combinazioni tra parametri.

## R-WECT

Obiettivo:

1. coprire classi valide;
2. testare ogni classe non valida in isolamento.

Numero di test:

```text
max(numero di CE valide tra le caratteristiche) + numero totale di CE non valide
```

Regole:

- in un test non valido deve esserci un solo valore non valido;
- gli altri parametri devono essere validi nominali;
- test non validi isolati non sostituiscono copertura delle classi valide.

Usalo quando:

- ci sono input non validi importanti;
- vuoi capire quale parametro causa errore;
- vuoi expected result chiaro per ogni invalidita.

## ACoC / N-SECT

Obiettivo: testare tutte le combinazioni delle classi.

Numero di test:

```text
CE_param1 * CE_param2 * ... * CE_paramN
```

Usalo quando:

- parametri sono correlati;
- numero combinazioni e piccolo;
- serve copertura forte;
- utente chiede tutte le combinazioni.

Limite:

- combinatorial explosion.

Se test diventano troppi, proponi Pairwise, R-WECT o criterio mirato.

## Pairwise

Obiettivo: coprire tutte le coppie di valori/classi tra parametri.

Usalo quando:

- ci sono molti parametri;
- ACoC produce troppi test;
- bug plausibili dipendono da interazioni a coppie.

Limite:

- non copre interazioni a 3 o piu parametri.

## Boundary Value Testing

Per ogni variabile ordinata usa:

```text
min, min+, nom, max-, max
```

Strategia standard:

- varia una variabile alla volta;
- mantieni le altre al valore nominale;
- aggiungi test tutto nominale.

Numero di test:

```text
4n + 1
```

dove `n` e numero di variabili.

Usalo per:

- numeri;
- date;
- lunghezze;
- quantita;
- soglie;
- range.

## Robustness Testing

Per ogni variabile ordinata usa:

```text
min-, min, min+, nom, max-, max, max+
```

Strategia standard:

- varia una variabile alla volta;
- mantieni le altre al valore nominale;
- aggiungi test tutto nominale.

Numero di test:

```text
6n + 1
```

Usalo quando vuoi testare anche valori appena fuori dominio valido.

## Worst case Boundary Value Testing

Ogni variabile ha 5 valori:

```text
min, min+, nom, max-, max
```

Numero combinazioni:

```text
5^n
```

Usalo solo se `n` e piccolo o se utente vuole copertura forte dei limiti combinati.

## Worst case Robustness Testing

Ogni variabile ha 7 valori:

```text
min-, min, min+, nom, max-, max, max+
```

Numero combinazioni:

```text
7^n
```

Attenzione: cresce molto rapidamente.

## Scelta rapida

```text
Solo firma disponibile -> Signature-based + N-WECT/R-WECT
Requisiti di dominio chiari -> Functionality-based
Invalidi importanti -> R-WECT
Suite minima -> N-WECT
Interazioni complete -> ACoC/N-SECT
Molti parametri -> Pairwise
Range numerici/date/lunghezze -> Boundary
Valori fuori range -> Robustness
```
