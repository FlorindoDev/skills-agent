# Patterns during refactoring

Usa questa reference quando uno smell suggerisce un possibile design pattern. Non introdurre pattern per estetica.

## Regola di flessibilita

Questa lista non e esaustiva. Usa questi pattern come riferimento principale, ma se trovi un refactoring piu adatto al codice reale, usalo e spiega:

- quale smell risolve;
- perche e migliore delle tecniche o dei pattern elencati;
- quale complessita introduce;
- come preserva il comportamento osservabile;
- come verificarlo con test.

## Regola base

Prima del pattern, chiarisci:

```text
Smell:
Problema reale:
Pattern candidato:
Alternativa piu semplice:
Costo in complessita:
Beneficio:
```

Se non esiste smell reale, non usare pattern.

## Factory

Usa Factory quando:

- il client istanzia classi concrete direttamente;
- la creazione degli oggetti e sparsa;
- aggiungere nuovi prodotti obbliga a modificare codice client;
- vuoi separare scelta dell'implementazione e uso dell'oggetto.

Non usarla se esiste una sola implementazione stabile e la creazione e semplice.

## DAO / Repository

Usa DAO o Repository quando:

- business logic accede direttamente al database;
- query e connessioni sono sparse;
- vuoi testare business logic senza DB reale;
- cambiare storage romperebbe molte classi.

Un DAO/Repository deve rappresentare un oggetto o aggregato coerente, non una singola schermata o singolo caso d'uso casuale.

## Observer

Usa Observer quando:

- piu oggetti devono reagire a un cambio di stato;
- publisher non deve conoscere classi concrete dei subscriber;
- vuoi aggiungere subscriber senza modificare publisher.

Attenzione: troppi eventi rendono debugging piu difficile.

## Singleton

Evita Singleton come refactoring predefinito.

Rischi:

- dipendenze globali nascoste;
- test e mock piu difficili;
- possibile violazione SRP;
- attenzione extra in multithread.

Preferisci dependency injection quando possibile.

## Iterator

Usa Iterator quando:

- il client conosce troppo la struttura interna di una collezione;
- vuoi attraversare strutture diverse con stessa interfaccia;
- vuoi separare algoritmo di attraversamento dalla collezione.

## Composite

Usa Composite quando:

- il dominio e una struttura ad albero;
- client deve trattare foglie e contenitori allo stesso modo;
- esistono operazioni ricorsive come calcolo prezzo, render o validazione.

Non forzare Composite se foglie e contenitori hanno interfacce troppo diverse.
