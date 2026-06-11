# E2E Output Templates

Usa questa reference quando devi produrre tabella finale, piano E2E completo o casi implementabili.

## Template: scenario table

```markdown
## Scenari E2E

| ID | Scenario | Tipo | Attore | Precondizioni | Risultato atteso |
|---|---|---|---|---|---|
| S1 | ... | REST API / Web App / Mixed | ... | ... | ... |
```

## Template: full E2E test plan

```markdown
# E2E test design: [nome]

## Obiettivo

[Descrizione sintetica]

## Tipo di E2E

[REST API / Web App / Mixed]

## Interfacce esterne coinvolte

| Interfaccia | Tipo | Descrizione |
|---|---|---|

## Strategia di isolamento

[Reset, cleanup, dati unici, gestione sessioni]

## Casi di test

| Test ID | Scenario | Arrange | Act | Assert | Cleanup |
|---|---|---|---|---|---|
```

## Template: REST API test case

```markdown
### Test [ID]: [nome]

**Arrange**
- Base URL:
- Endpoint:
- Auth:
- Payload:

**Act**
- Request:

**Assert**
- Expected status:
- Expected body:
- Extra verification:

**Cleanup**
- Resources to delete/reset:
```

## Template: Web App test case

```markdown
### Test [ID]: [nome]

**Arrange**
- Browser state:
- Test data:
- Start page:

**Act**
- User actions:

**Assert**
- Expected URL:
- Expected visible elements:
- Expected persisted state:

**Cleanup**
- Data/browser cleanup:
```

## Template: compact table

```markdown
| Test ID | Tipo | Flusso | Expected result | Cleanup |
|---|---|---|---|---|
| T1 | REST API | ... | ... | ... |
| T2 | Web App | ... | ... | ... |
```
