---
name: refactoring
description: >
  Usa questa skill quando l'utente chiede di analizzare o migliorare codice
  esistente senza cambiare il comportamento osservabile. Serve per identificare
  code smells, debito tecnico, problemi di coesione, accoppiamento,
  responsabilita, testabilita e scegliere refactoring piccoli e sicuri. Input
  tipici: codice, file, diff, descrizione del comportamento attuale, errori,
  test disponibili. Output atteso: analisi strutturata, piano di refactoring,
  patch o modifiche applicate con verifica.
---

# Refactoring

## Quando usarla

Usa questa skill quando l'utente vuole:

- migliorare codice gia esistente senza aggiungere funzionalita;
- rendere il codice piu leggibile, manutenibile e testabile;
- identificare code smells;
- ridurre metodi lunghi, classi grandi, duplicazione o codice morto;
- valutare coesione, accoppiamento, responsabilita e confini delle classi;
- capire se una classe viola SRP;
- ridurre catene di chiamate e violazioni della Legge di Demetra;
- spostare responsabilita nella classe corretta;
- proporre un piano di refactoring sicuro;
- applicare piccoli refactoring incrementali;
- valutare debito tecnico;
- decidere se un design pattern risolve un problema di design gia presente.

## Quando non usarla

Non usare questa skill quando:

- l'utente chiede di implementare una nuova feature come obiettivo principale;
- il comportamento osservabile deve cambiare;
- l'utente chiede solo una spiegazione teorica senza codice;
- l'utente chiede una review di sicurezza;
- l'utente chiede performance tuning puro senza problema di design;
- la richiesta richiede riscrittura totale non giustificata;
- mancano codice o contesto minimi per capire il comportamento attuale.

## Obiettivo

L'obiettivo della skill e produrre:

- una diagnosi chiara del codice esistente;
- una lista ordinata di code smells e problemi di design;
- un piano di refactoring piccolo, incrementale e verificabile;
- patch che preservano il comportamento osservabile;
- motivazione di ogni refactoring scelto;
- indicazione dei test eseguiti o mancanti;
- rischi residui e assunzioni esplicite.

## Input richiesti

L'utente dovrebbe fornire:

- codice o file da analizzare;
- comportamento atteso o comportamento attuale da preservare;
- linguaggio, framework e vincoli del progetto;
- test disponibili o comando di test;
- obiettivo del refactoring: leggibilita, duplicazione, responsabilita, testabilita, accoppiamento o altro;
- eventuali limiti: non cambiare API pubbliche, non cambiare schema DB, non toccare file esterni.

Se manca un input non essenziale, fai una scelta ragionevole e dichiarala.

Se manca un input essenziale, chiedi chiarimento.

## Procedura/workflow

1. Leggi attentamente la richiesta dell'utente.
2. Identifica il tipo di task: analisi, piano, patch, riduzione smell, separazione responsabilita o verifica.
3. Controlla se la skill e adatta al caso.
4. Raccogli codice, test, vincoli e comportamento da preservare.
5. Prima di cambiare codice, capisci input, output, collaboratori e side effect.
6. Identifica responsabilita principali, responsabilita secondarie e motivi per cambiare.
7. Valuta coesione, accoppiamento, Legge di Demetra e Responsibility-Driven Design.
8. Cerca code smells e classificali per gravita.
9. Scegli il refactoring piu piccolo che risolve il problema piu importante.
10. Applica una modifica alla volta quando devi editare codice.
11. Mantieni invariato il comportamento osservabile.
12. Usa eventuali file in `references/` solo se servono.
13. Produci l'output nel formato richiesto.
14. Esegui i test se disponibili; se non sono disponibili, segnala il rischio.
15. Fai un controllo finale prima di rispondere.

## Regole importanti

- Mantieni la risposta chiara e ordinata.
- Non aggiungere sezioni inutili.
- Non inventare dati mancanti.
- Segnala sempre eventuali assunzioni.
- Segui il formato di output richiesto.
- Usa esempi solo se aiutano davvero.
- Non rendere la skill troppo generica.
- Non cambiare comportamento osservabile durante refactoring.
- Non fare riscritture grandi se bastano piccoli passi.
- Non modificare codice non correlato.
- Non introdurre pattern senza prima identificare il problema.
- Non introdurre astrazioni speculative.
- Non eliminare codice senza verificare se e usato.
- Non applicare SRP in modo estremo creando classi inutili.
- Non sostituire ogni `switch` o `if` con polimorfismo: valuta complessita e stabilita del caso.
- Non usare Singleton come soluzione predefinita.
- Se mancano test, evita refactoring invasivi e segnala il rischio.
- Se i test falliscono dopo il refactoring, considera la modifica non sicura finche non hai capito la causa.

## Uso di references

Leggi queste reference solo quando utili:

- `references/design-principles.md`: coesione, accoppiamento, SRP, Legge di Demetra, RDD, decomposizione e design trade-off.
- `references/code-smells.md`: categorie di code smells e segnali da cercare.
- `references/refactoring-techniques.md`: tecniche di refactoring e quando applicarle.
- `references/refactoring-cycle-tests-debt.md`: ciclo di refactoring, test unitari e debito tecnico.
- `references/patterns-during-refactoring.md`: uso prudente di Factory, DAO/Repository, Observer, Singleton, Iterator e Composite durante refactoring.

## Formato di output

Restituisci il risultato in questo formato:

```text
Titolo:

Input usati:

Risultato:

Assunzioni:

Controllo finale:
```

Se il task richiede solo analisi, struttura `Risultato` cosi:

```text
Findings:
- Problema, file/riga se disponibile, impatto.

Piano di refactoring:
- Step piccoli e ordinati.

Rischi:
- Cosa puo rompere il comportamento.
```

Se il task richiede modifiche al codice, struttura `Risultato` cosi:

```text
Modifiche applicate:
- File modificati.
- Refactoring applicati.

Miglioramenti di design:
- Coesione migliorata.
- Accoppiamento ridotto.
- Responsabilita chiarite.

Verifica:
- Test eseguiti.
- Test mancanti.
- Rischi residui.
```

## Errori da evitare

- Confondere refactoring con aggiunta di funzionalita.
- Cambiare comportamento e chiamarlo refactoring.
- Proporre pattern prima di aver trovato lo smell.
- Fare refactor grande senza test.
- Rendere il codice piu astratto ma meno leggibile.
- Spezzare classi in troppe classi senza responsabilita reali.
- Rimuovere codice morto senza cercare riferimenti.
- Spostare metodi senza capire dove stanno i dati.
- Usare commenti per nascondere nomi o metodi poco chiari.
- Ignorare side effect, I/O, persistenza, API pubbliche e compatibilita.

## Controllo finale

Prima di concludere, verifica:

- il comportamento osservabile e preservato;
- il refactoring risolve uno smell reale;
- ogni modifica ha motivo chiaro;
- ogni classe toccata ha responsabilita piu chiara;
- coesione non e peggiorata;
- accoppiamento non e aumentato inutilmente;
- non sono state introdotte astrazioni speculative;
- test disponibili sono stati eseguiti;
- test mancanti o rischi sono dichiarati;
- output segue il formato richiesto.

## Quick Checklist

```text
[ ] Ho capito comportamento attuale?
[ ] Ho identificato input, output e side effect?
[ ] Ho trovato smell reali?
[ ] Ho scelto refactoring piccolo?
[ ] Il comportamento osservabile resta uguale?
[ ] Ogni classe ha responsabilita chiara?
[ ] Ogni metodo fa una cosa sola?
[ ] Coesione migliorata?
[ ] Accoppiamento ridotto o almeno non peggiorato?
[ ] Catene tipo a.getB().getC() evitate?
[ ] Pattern introdotti solo se necessari?
[ ] Test eseguiti o rischio dichiarato?
[ ] Debito tecnico residuo dichiarato?
```
