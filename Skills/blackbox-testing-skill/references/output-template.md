# Output templates for black-box tests

Usa questa reference quando devi produrre tabelle finali, suite completa o test implementabili.

## Template: equivalence classes only

```markdown
## Parametri

| Parametro | Tipo | Dominio | Valore nominale | Note |
|---|---|---|---|---|

## Classi di equivalenza

| ID | Parametro / caratteristica | Tipo | Descrizione | Valori rappresentativi | Expected behavior |
|---|---|---|---|---|---|
```

## Template: full black-box test design

```markdown
# Black-box test design: [nome]

## Requisiti assunti

[Regole funzionali usate]

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

- Tecnica:
- Motivazione:
- Numero di test atteso:

## Casi di test

| Test ID | Tecnica | Input concreti | CE coperte | Expected result | Motivazione |
|---|---|---|---|---|---|

## Note finali

[Limiti, assunzioni, alternative]
```

## Template: implementable unit test

```markdown
### Test [ID]: [nome]

**Arrange**
- [preparazione input/stato]

**Act**
- [azione eseguita]

**Assert**
- [risultato atteso]
```

## Template: compact test case

```markdown
| Test ID | Tecnica | Input | Expected result |
|---|---|---|---|
| T1 | ... | ... | ... |
```
