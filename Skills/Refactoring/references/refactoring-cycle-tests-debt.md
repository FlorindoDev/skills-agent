# Refactoring cycle, tests, technical debt

Usa questa reference quando devi decidere quanto refactoring fare, come verificarlo e come comunicare rischio.

## Refactoring

Refactoring significa:

```text
Migliorare struttura interna senza cambiare comportamento osservabile.
```

Non e refactoring:

- aggiungere funzionalita;
- cambiare output;
- cambiare API pubblica senza accordo;
- riscrivere tutto senza preservare comportamento.

## Ciclo di refactoring

1. Identifica smell piu grave.
2. Scegli refactoring mirato.
3. Applica modifica piccola.
4. Esegui test.
5. Ripeti.

Regole:

- una modifica alla volta;
- se test falliscono, capisci prima di continuare;
- se non sai spiegare il miglioramento, non applicare refactor;
- non correggere ogni smell se non serve al task.

## Test unitari

Il refactoring dipende molto dai test.

Con test:

```text
1. Esegui test prima.
2. Applica refactoring.
3. Esegui test dopo.
4. Confronta risultato.
```

Senza test:

- segnala rischio;
- proponi test minimi;
- limita ampiezza modifica;
- preserva API e output;
- evita refactor strutturali grandi.

Piu il refactoring tocca confini, persistenza o comportamento implicito, piu servono test.

## Perche fare refactoring

Motivi:

- progetto iniziale raramente e perfetto;
- dominio e requisiti diventano chiari col tempo;
- codice fragile rallenta sviluppo;
- duplicazione aumenta costo delle modifiche;
- nomi e responsabilita chiare aiutano lettura;
- miglior design facilita evoluzione futura.

Refactoring aiuta a:

- capire codice esistente;
- trovare bug;
- programmare piu velocemente dopo;
- ridurre interesse del debito tecnico.

## Debito tecnico

Debito tecnico: codice che funziona ma e subottimale.

Esempi:

- code smells;
- algoritmo inefficiente;
- design approssimativo;
- test insufficienti;
- implementazione complessa senza motivo.

Debito intenzionale:

- scelto per consegnare prima;
- deve avere motivo e piano di rimborso.

Debito non intenzionale:

- nasce da fretta, poca conoscenza, processi deboli;
- spesso emerge tramite smell e bug.

Domande utili:

```text
Possiamo permetterci questo debito?
Quanto costa mantenerlo?
Esiste un piano per ridurlo?
Sta rallentando modifiche future?
```

Conseguenze di troppo debito:

- sviluppo piu lento;
- bug piu costosi;
- pianificazione meno prevedibile;
- piu rischio in ogni modifica.

## Verifica finale

Quando chiudi un refactoring, dichiara:

- cosa e cambiato internamente;
- cosa non e cambiato nel comportamento;
- test eseguiti;
- test mancanti;
- rischio residuo;
- eventuale debito non risolto.
