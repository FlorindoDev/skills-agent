# Output templates for black-box tests

## Template: equivalence classes only

```markdown
## Parametri

| Parametro | Tipo | Dominio | Valore nominale | Note |
|---|---|---|---|---|

## Classi di equivalenza

| ID | Parametro / caratteristica | Tipo | Descrizione | Valori rappresentativi | Expected behavior |
|---|---|---|---|---|---|
```

## Template: full test suite

```markdown
## Casi di test

| Test ID | Tecnica | Input concreti | CE coperte | Expected result | Motivazione |
|---|---|---|---|---|---|
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
| Test ID | Input | Expected result |
|---|---|---|
| T1 | ... | ... |
```
