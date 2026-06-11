---
name: blackbox-testing
description: >
  Usa questa skill quando l'utente chiede di progettare test black-box a
  partire da requisiti funzionali, firme di funzioni, API, form, componenti o
  descrizioni di comportamento atteso. Serve per identificare funzioni
  testabili, parametri, classi di equivalenza, valori limite e casi di test
  senza usare la struttura interna del codice. Input tipici: requisiti, firma
  di funzione, API, dominio input, output attesi, vincoli. Output atteso:
  classi di equivalenza, criterio scelto, casi di test concreti, expected
  result e assunzioni.
---

# Black-Box Testing

## Quando usarla

Usa questa skill quando l'utente vuole:

- progettare test black-box;
- creare casi di test da requisiti funzionali;
- testare funzione, API, form, servizio o componente senza guardare implementazione interna;
- individuare classi di equivalenza;
- scegliere o applicare N-WECT, R-WECT, ACoC/N-SECT, Boundary Value Testing, Robustness Testing o Pairwise;
- trasformare combinazioni astratte di classi in input concreti;
- costruire una tabella di test con input, expected result e motivazione;
- scrivere test implementabili con struttura Arrange, Act, Assert partendo da progettazione black-box.

## Quando non usarla

Non usare questa skill quando:

- l'utente chiede testing white-box come branch coverage, path coverage, condition coverage o CFG;
- l'utente vuole analizzare la struttura interna del codice come criterio principale;
- l'utente chiede solo implementazione di test senza progettazione dei casi;
- l'utente chiede test end-to-end completi su browser o API reali;
- mancano requisiti, firma, input osservabili o comportamento atteso minimi;
- la richiesta e troppo generica per derivare input e output attesi.

## Obiettivo

L'obiettivo della skill e produrre:

- una progettazione black-box ordinata;
- funzioni o comportamenti testabili;
- parametri osservabili e domini;
- classi di equivalenza valide e non valide;
- criterio di test motivato;
- casi di test concreti;
- expected result chiari;
- assunzioni dichiarate;
- limiti della suite dichiarati.

## Input richiesti

L'utente dovrebbe fornire:

- requisiti funzionali o comportamento atteso;
- firma della funzione, endpoint API, form o componente;
- parametri di input osservabili;
- dominio valido e vincoli;
- output atteso o regole di validazione;
- tecnica richiesta, se gia scelta;
- formato finale desiderato, se diverso dalla tabella.

Se manca un input non essenziale, fai una scelta ragionevole e dichiarala.

Se manca un input essenziale, chiedi chiarimento.

## Procedura/workflow

1. Leggi attentamente la richiesta dell'utente.
2. Identifica il tipo di task: classi di equivalenza, criterio combinatorio, boundary, robustness, suite completa o test implementabili.
3. Controlla se la skill e adatta al caso.
4. Raccogli requisiti, firma, parametri, dominio, vincoli e output attesi.
5. Identifica le funzioni o caratteristiche testabili.
6. Trova tutti i parametri osservabili che influenzano comportamento.
7. Partiziona il dominio degli input in classi di equivalenza disgiunte e rilevanti.
8. Distingui classi valide, non valide e casi limite.
9. Scegli il criterio piu adatto: N-WECT, R-WECT, ACoC/N-SECT, Boundary, Robustness, Pairwise o altro criterio motivato.
10. Calcola o stima numero di test quando la tecnica lo richiede.
11. Raffina combinazioni astratte in input concreti.
12. Definisci expected result per ogni test.
13. Usa eventuali file in `references/` solo se servono.
14. Produci l'output nel formato richiesto.
15. Fai un controllo finale prima di rispondere.

## Regole importanti

- Mantieni la risposta chiara e ordinata.
- Non aggiungere sezioni inutili.
- Non inventare requisiti mancanti.
- Segnala sempre eventuali assunzioni.
- Segui il formato di output richiesto.
- Usa esempi solo se aiutano davvero.
- Non rendere la skill troppo generica.
- Non progettare test partendo dalla logica interna del codice.
- Non promettere complete coverage per moduli non banali.
- Preferisci functionality-based approach quando hai requisiti o regole di dominio.
- Usa signature-based approach quando hai solo firma o parametri esposti.
- In R-WECT, un test non valido deve contenere un solo valore non valido.
- In Boundary Value Testing varia una variabile alla volta e tieni le altre nominali.
- In Robustness Testing includi anche valori appena fuori limite.
- In ACoC/N-SECT avvisa se il prodotto cartesiano causa combinatorial explosion.
- Ogni test deve avere input concreti ed expected result verificabile.
- Se una tecnica non e nella lista ma e piu adatta, usala e motiva la scelta.

## Uso di references

Leggi queste reference solo quando utili:

- `references/blackbox-workflow.md`: concetti base, complete coverage, black-box workflow, parameter identification, equivalence classes, signature/functionality-based approach.
- `references/test-criteria.md`: N-WECT, R-WECT, ACoC/N-SECT, Pairwise, Boundary Value Testing, Robustness Testing e formule.
- `references/output-template.md`: template di output per classi, suite completa, test AAA e tabella compatta.

## Formato di output

Restituisci il risultato in questo formato:

```text
Titolo:

Input usati:

Risultato:

Assunzioni:

Controllo finale:
```

Per una progettazione completa, struttura `Risultato` cosi:

```text
Funzione / componente testato:

Parametri:

Classi di equivalenza:

Criterio scelto:

Casi di test:

Note finali:
```

Per test implementabili, usa anche:

```text
Arrange:
Act:
Assert:
```

## Errori da evitare

- Confondere black-box testing con white-box testing.
- Usare branch/path/condition coverage come criterio principale black-box.
- Trascurare input osservabili come stato esterno, file, configurazioni o parametri API.
- Creare classi di equivalenza sovrapposte.
- Lasciare buchi nel dominio rilevante.
- Mischiare piu input non validi nello stesso test R-WECT.
- Usare N-WECT senza segnalare limite su interazioni tra parametri.
- Generare ACoC senza avvisare se i test diventano troppi.
- Dimenticare valore nominale nei test boundary/robustness.
- Dare expected result vaghi come "funziona".

## Controllo finale

Prima di concludere, verifica:

- la suite e black-box;
- funzioni testabili sono chiare;
- tutti i parametri osservabili sono considerati;
- classi di equivalenza sono disgiunte;
- dominio rilevante e coperto;
- classi valide e non valide sono distinguibili;
- criterio scelto e motivato;
- numero di test e dichiarato quando utile;
- input concreti sono presenti;
- expected result sono verificabili;
- assunzioni e limiti sono dichiarati.

## Quick Checklist

```text
[ ] Ho identificato funzioni o comportamenti testabili?
[ ] Ho trovato tutti i parametri osservabili?
[ ] Ho definito dominio, vincoli e valore nominale?
[ ] Ho creato classi di equivalenza disgiunte?
[ ] Ho distinto classi valide e non valide?
[ ] Ho scelto criterio coerente col rischio?
[ ] Ho isolato input non validi se uso R-WECT?
[ ] Ho incluso boundary se esistono range?
[ ] Ogni test ha input concreto?
[ ] Ogni test ha expected result verificabile?
[ ] Assunzioni e limiti sono dichiarati?
```
