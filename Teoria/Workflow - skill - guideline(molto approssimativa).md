


La distinzione utile è questa:

|Elemento|A cosa serve|Livello|
|---|---|---|
|**Skill**|Insegna all’agente una capacità specifica|“Come fare code review”, “come creare API”, “come scrivere test”|
|**Guideline**|Definisce regole generali e vincoli|“Non modificare file non richiesti”, “scrivi codice tipizzato”, “prima leggi il contesto”|
|**Workflow**|Definisce una procedura passo-passo|“Leggi → pianifica → modifica → testa → riepiloga”|

Il formato più diffuso per le skill è una cartella con un file `SKILL.md`: dentro ci sono metadata come `name` e `description`, più le istruzioni operative. La skill può anche includere script, reference, template e asset. ([agentskills.io](https://agentskills.io/home "Agent Skills Overview - Agent Skills"))

---

## 1. Cos’è una skill

Una **skill** è un modulo operativo riusabile. Serve quando vuoi che l’agente impari **un modo specifico di fare una cosa**.

Esempio:

```text
skills/
└── code-review/
    ├── SKILL.md
    ├── references/
    │   └── review-checklist.md
    └── scripts/
        └── run-tests.sh
```

Il concetto importante è che l’agente non deve caricare tutto sempre. Le skill funzionano spesso con **progressive disclosure**: prima l’agente vede solo nome e descrizione, poi carica l’intera skill solo quando serve. ([agentskills.io](https://agentskills.io/home "Agent Skills Overview - Agent Skills"))

### Com’è fatta una skill

Una skill di solito ha questa struttura:

```md
---
name: code-review
description: Use this skill when the user asks to review code, find bugs, improve maintainability, or check implementation quality.
---

# Code Review Skill

## Goal

Review code changes in a precise, practical way.

## When to use this skill

Use this skill when:
- the user asks for code review
- the user asks if an implementation is correct
- the user asks to find bugs
- the user asks to improve code quality

## Inputs expected
...
...
...
...

## Procedure/workflow

1. Read the relevant files before making judgments.
2. Identify the intended behavior.
3. Check correctness first.
4. Check edge cases.
5. Check maintainability.
6. Suggest minimal fixes.
7. Avoid rewriting unrelated code.

## Core principles
...
...
...
...

## Output format

Return:
1. Critical bugs
2. Possible edge cases
3. Suggested improvements
4. Final corrected code, only if needed

## Constraints

- Do not invent files or APIs.
- Do not modify unrelated parts.
- Prefer small patches.
- Explain why each change is needed.
```

Questa è una **skill buona** perché dice:

- quando usarla;
    
- quale obiettivo ha;
    
- che procedura seguire;
    
- che formato deve avere l’output;
    
- quali errori evitare.
    

Una skill invece è debole quando dice solo:

```md
You are an expert code reviewer.
Review code carefully.
```

Perché non dà una procedura concreta.

---

## 2. Cosa sono le guideline

Le **guideline** sono regole generali. Non sono legate a una singola capacità, ma valgono sempre o quasi sempre.

Esempio: se programmi con agenti, puoi avere un file tipo:

```text
AGENT.md
```

oppure:

```text
.guidelines/
├── coding.md
├── testing.md
├── git.md
└── security.md
```

### Esempio di guideline per programmazione

```md
# Coding Guidelines for Agents

## General rules

Before editing code:
1. Read the relevant files.
2. Understand the current architecture.
3. Identify the smallest safe change.
4. Explain the plan if the change touches multiple files.

## Coding style

- Follow the existing style of the repository.
- Prefer readable code over clever code.
- Use explicit names.
- Avoid unnecessary abstractions.
- Do not introduce new dependencies unless required.

## Safety rules

- Do not delete files unless explicitly requested.
- Do not rewrite large modules without a reason.
- Do not change public APIs unless the user asked for it.
- Do not expose secrets, tokens, or credentials.

## Testing rules

After code changes:
1. Run existing tests when possible.
2. Add tests for new behavior.
3. If tests cannot be run, explain why.
4. Report what was verified and what was not verified.
```

La differenza principale è:

```text
Skill = come fare un compito specifico.
Guideline = regole generali di comportamento.
```

Per esempio:

```text
Skill: "come implementare un endpoint REST"
Guideline: "non introdurre dipendenze inutili"
```

---

## 3. Cosa sono i workflow

Un **workflow** è una procedura. Serve per task più lunghi, dove l’agente deve seguire una sequenza controllata.

Per esempio, un coding agent di solito lavora con un ciclo:

```text
Read → Reason → Act → Evaluate
```

Questa struttura è comune negli agenti di programmazione: leggono i file, ragionano sui passi, modificano codice o usano strumenti, poi valutano il risultato. ([realpython.com](https://realpython.com/ai-coding-agents-guide/ "AI Coding Agents Guide: A Map of the Four Workflow Types – Real Python"))

### Esempio di workflow per implementare una feature

```md
# Workflow: Implement Feature

## Trigger

Use this workflow when the user asks to add a new feature.

## Steps

### 1. Understand the request

- Identify the expected behavior.
- Identify inputs and outputs.
- Identify affected modules.
- Ask for clarification only if the task is ambiguous and cannot be safely approximated.

### 2. Inspect the codebase

- Read existing related files.
- Find similar implementations.
- Identify architectural conventions.

### 3. Plan the change

Produce a short plan:
- files to modify
- behavior to add
- tests to update
- risks

### 4. Implement minimally

- Make the smallest correct change.
- Reuse existing patterns.
- Avoid unrelated refactors.

### 5. Validate

- Run tests if available.
- Run typecheck/linter if available.
- Manually verify edge cases.

### 6. Report

Return:
- what changed
- files touched
- tests run
- remaining risks
```

Questo è diverso da una skill. Il workflow non insegna una competenza specifica, ma organizza il lavoro.

---

## 4. Come usare skill, guideline e workflow insieme

La struttura migliore secondo me è questa:

```text
.agent/
├── guidelines/
│   ├── coding.md
│   ├── testing.md
│   ├── security.md
│   └── git.md
├── skills/
│   ├── code-review/
│   │   └── SKILL.md
│   ├── api-design/
│   │   └── SKILL.md
│   ├── database-migration/
│   │   └── SKILL.md
│   └── frontend-component/
│       └── SKILL.md
└── workflows/
    ├── implement-feature.md
    ├── fix-bug.md
    ├── refactor-module.md
    └── review-pr.md
```

Poi l’agente lavora così:

```text
1. Legge le guideline generali.
2. Capisce il task.
3. Sceglie la skill rilevante.
4. Applica il workflow corretto.
5. Usa eventuali script/test/reference.
6. Produce output verificabile.
```

---

## 5. Esempio concreto: agente per programmare meglio

Mettiamo che tu voglia gestire task di sviluppo backend.

### Guideline generale

```md
# Backend Agent Guidelines

- Preserve existing architecture.
- Prefer small, testable changes.
- Do not change database schema without migration.
- Never hardcode secrets.
- Validate input at API boundaries.
- Keep business logic outside controllers when the project already follows a service pattern.
```

### Skill specifica

```md
---
name: express-api-endpoint
description: Use this skill when implementing or modifying Express.js API endpoints.
---

# Express API Endpoint Skill

## Goal

Implement Express endpoints consistent with the existing backend architecture.

## Procedure

1. Find the existing route structure.
2. Identify controller/service/repository layers.
3. Add validation.
4. Add or update service logic.
5. Add error handling.
6. Add tests if the project has tests.
7. Update documentation if endpoint behavior changes.

## Constraints

- Do not place business logic directly in routes if services exist.
- Do not bypass existing auth middleware.
- Do not expose internal error details to clients.
```

### Workflow operativo

```md
# Workflow: Add Backend Endpoint

1. Read similar endpoints.
2. Identify route, controller, service, model, and tests.
3. Propose minimal implementation plan.
4. Modify files.
5. Run tests.
6. Summarize changed behavior and verification.
```

In questo modo l’agente non “improvvisa”: ha regole, competenze e procedura.

---

## 6. Dove entrano handoff e guardrail

Quando usi più agenti, puoi anche separare i ruoli:

```text
Planner Agent → decide il piano
Coder Agent → modifica il codice
Reviewer Agent → controlla bug e qualità
Tester Agent → esegue test e verifica
```

Negli agent framework, questo passaggio tra agenti viene spesso chiamato **handoff**: un agente delega un task a un altro specialista. OpenAI, per esempio, descrive gli handoff come deleghe tra agenti specializzati. ([openai.github.io](https://openai.github.io/openai-agents-python/handoffs/ "Handoffs - OpenAI Agents SDK"))

I **guardrail** invece sono controlli che bloccano o richiedono review umana prima di azioni rischiose. Nella documentazione OpenAI, guardrail e human review sono consigliati quando il workflow deve fermarsi o validare prima di continuare. ([Sviluppatori OpenAI](https://developers.openai.com/api/docs/guides/agents "Agents SDK | OpenAI API"))

Esempio:

```text
Se l’agente vuole:
- cancellare file
- fare push
- modificare migration
- toccare configurazioni di produzione
- cambiare auth/security

allora deve fermarsi e chiedere conferma.
```

---

## 7. Template compatto che puoi riusare

### Skill template

```md
---
name: nome-skill
description: Use this skill when...
---

# Nome Skill

## Goal

Descrivi cosa deve ottenere l’agente.

## When to use

Usa questa skill quando:
- ...
- ...

## Inputs expected

L’agente dovrebbe cercare:
- file rilevanti
- esempi simili
- test esistenti
- vincoli architetturali

## Procedure/workflow

1. ...
2. ...
3. ...
   
## Core principles
...
...
...
...

## Output format

Restituisci:
1. ...
2. ...
3. ...

## Constraints

- ...
- ...

## Common mistakes to avoid

- ...
- ...
```

### Guideline template

```md
# Agent Guidelines

## General behavior

- ...
- ...

## Coding rules

- ...
- ...

## Testing rules

- ...
- ...

## Security rules

- ...
- ...

## Git rules

- ...
- ...
```

### Workflow template

```md
# Workflow: Nome Workflow

## Trigger

Usa questo workflow quando...

## Steps

### 1. Understand

...

### 2. Inspect

...

### 3. Plan

...

### 4. Execute

...

### 5. Validate

...

### 6. Report

...
```

---

## 8. Regola pratica per non confonderli

La distinzione più semplice è questa:

```text
Guideline = regole sempre valide.
Skill = competenza specifica.
Workflow = sequenza di lavoro.
```

Esempio:

```text
Guideline:
"Non modificare file non richiesti."

Skill:
"Come fare code review in questo progetto."

Workflow:
"Per ogni bugfix: riproduci → individua causa → patch minima → test → report."
```

Per programmare meglio con agenti, ti conviene partire da poche cose:

```text
1. AGENT_GUIDELINES.md
2. skills/code-review/SKILL.md
3. skills/bug-fix/SKILL.md
4. skills/feature-implementation/SKILL.md
5. workflows/fix-bug.md
6. workflows/implement-feature.md
7. workflows/review-pr.md
```

Poi ogni volta che l’agente sbaglia, non correggi solo il prompt: aggiorni la skill o la guideline. Anthropic consiglia proprio di iterare sulle skill catturando approcci riusciti ed errori comuni, invece di provare ad anticipare tutto dall’inizio. ([anthropic.com](https://www.anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills "Equipping agents for the real world with Agent Skills \ Anthropic"))