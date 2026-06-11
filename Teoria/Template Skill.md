

# Template Skill

```text
mia-skill/
├── SKILL.md
├── references/
│   └── guida.md
├── scripts/
│   └── script.py
└── assets/
    └── template.md
```

---

## SKILL.md

````markdown
---
name: nome-della-skill
description: Usa questa skill quando l'utente chiede di [descrivi il task specifico]. Serve per [obiettivo principale]. Input tipici: [testo, file, dati, immagini, codice]. Output atteso: [formato finale].
metadata:
  version: "1.0"
  author: "tuo-nome"
---

# Nome della Skill

## Quando usarla

Usa questa skill quando l'utente vuole:

- [caso 1]
- [caso 2]
- [caso 3]

Non usare questa skill quando:

- [caso non pertinente]
- [task troppo diverso]
- [richiesta troppo generica]

## Obiettivo

L'obiettivo della skill è produrre:

- [output principale]
- [formato richiesto]
- [livello di dettaglio atteso]

Esempio:

- una spiegazione ordinata
- un file strutturato
- una tabella
- una checklist
- un template
- codice funzionante
- una revisione corretta

## Input richiesti

L'utente dovrebbe fornire:

- [input 1]
- [input 2]
- [input 3]

Se manca un input non essenziale, fai una scelta ragionevole e dichiarala.

Se manca un input essenziale, chiedi chiarimento.

## Procedura/workflow

1. Leggi attentamente la richiesta dell'utente.
2. Identifica il tipo di task.
3. Controlla se la skill è adatta al caso.
4. Raccogli gli input disponibili.
5. Applica le regole specifiche della skill.
6. Usa eventuali file in `references/` solo se servono.
7. Usa eventuali script in `scripts/` solo se servono.
8. Produci l'output nel formato richiesto.
9. Fai un controllo finale prima di rispondere.

## Regole importanti

- Mantieni la risposta chiara e ordinata.
- Non aggiungere sezioni inutili.
- Non inventare dati mancanti.
- Segnala sempre eventuali assunzioni.
- Segui il formato di output richiesto.
- Usa esempi solo se aiutano davvero.
- Non rendere la skill troppo generica.
- Non mettere nel file principale informazioni troppo lunghe.
- Sposta dettagli lunghi in `references/`.
- Sposta codice riutilizzabile in `scripts/`.
- Sposta template o risorse statiche in `assets/`.

## Uso di references

Usa la cartella `references/` per materiali lunghi, ad esempio:

- guide dettagliate
- documentazione
- esempi completi
- regole estese
- casi particolari

Non copiare tutto dentro `SKILL.md` se non serve sempre.

## Uso di scripts

Usa la cartella `scripts/` per codice riutilizzabile, ad esempio:

- script Python
- validatori
- generatori di file
- trasformatori di dati
- controlli automatici

Gli script devono essere usati solo quando migliorano davvero il risultato.

## Uso di assets

Usa la cartella `assets/` per file statici, ad esempio:

- template
- immagini
- modelli
- esempi base
- file di configurazione

## Formato di output

Restituisci il risultato in questo formato:

```text
Titolo:

Input usati:

Risultato:

Assunzioni:

Controllo finale:
```


## Quick Checklist

Il template della skill deve contenere:

- Nome della skill chiaro e breve.
- `description` precisa, che spiega quando la skill deve essere usata.
- Sezione “Quando usarla”.
- Sezione “Quando non usarla”.
- Obiettivo della skill.
- Input richiesti.
- Procedura operativa divisa in passaggi.
- Regole importanti da seguire.
- Formato di output atteso.
- Gestione delle assunzioni quando mancano informazioni.
- Indicazione di quando usare `references/`.
- Indicazione di quando usare `scripts/`.
- Indicazione di quando usare `assets/`.
- Sezione sugli errori da evitare.
- Controllo finale dell’output.
- Esempio minimo di utilizzo.
- Istruzioni corte, pratiche e non ridondanti.
- Nessuna informazione inutile nel `SKILL.md`.
- Possibilità di testare la skill con esempi realistici.
  

````
