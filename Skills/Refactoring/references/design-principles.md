# Design principles for refactoring

Usa questa reference quando devi capire se il codice ha problemi di responsabilita, coesione, accoppiamento o confini.

## Regola di flessibilita

Questi principi sono criteri guida, non una checklist chiusa. Se trovi un criterio di design o un refactoring piu adatto al codice reale, usalo e spiega:

- quale smell o problema di design risolve;
- perche e migliore delle tecniche o dei criteri elencati;
- quale trade-off introduce;
- come preserva il comportamento osservabile;
- come verificarlo con test.

## Design goal e trade-off

Nel refactoring non cambiare funzionalita. Migliora qualita interna.

Criteri utili:

- Performance: attenzione a non peggiorare tempi, memoria o throughput.
- Affidabilita: preserva robustezza, disponibilita e gestione errori.
- Costi: preferisci step piccoli, non riscritture grandi.
- Manutenibilita: obiettivo principale del refactoring.
- Usabilita: per API pubbliche, non rompere contratti esistenti.

Trade-off frequenti:

- piu astrazione vs piu semplicita;
- meno duplicazione vs codice piu leggibile;
- refactor completo vs step sicuri;
- velocita di intervento vs copertura test.

Regola:

```text
Se non puoi verificare il comportamento, riduci ampiezza del refactoring.
```

## Decomposizione

Dividi sistema in parti piu piccole solo quando riduce complessita reale.

Buoni segnali per decomporre:

- una classe cambia per motivi diversi;
- un modulo contiene UI, business logic e persistenza insieme;
- una modifica richiede cambiamenti in molti punti;
- responsabilita di un sottosistema non sono chiare;
- tutti i moduli accedono direttamente al database.

Opzioni:

- Layers: separa UI, logica, persistenza, infrastruttura.
- Partizionamento per feature: separa funzionalita autonome.
- Sottosistemi: definisci servizi offerti e interfacce.

## Coesione

Coesione misura quanto responsabilita e servizi di un modulo sono collegati e mirati.

Alta coesione:

- metodo con un solo compito;
- classe che rappresenta un singolo concetto;
- responsabilita correlate;
- nome facile da scegliere;
- cambiamento localizzato.

Segnali di bassa coesione:

- Long Method;
- Large Class;
- commenti necessari per capire sezioni interne;
- nomi generici;
- business logic, formattazione, stampa e accesso dati nello stesso posto.

Refactoring utili:

- Extract Method;
- Extract Class;
- Move Method;
- Rename Method/Class.

## SRP

Single Responsibility Principle:

```text
Una classe dovrebbe avere una sola responsabilita.
Una responsabilita e un motivo per cambiare.
```

Domande:

- Questa classe cambia per piu motivi?
- Recupera dati, formatta e stampa insieme?
- Contiene logica di domini diversi?
- Una piccola modifica obbliga a toccare una classe troppo grande?

Esempio:

```text
Report carica dati, formatta e stampa.
Motivi per cambiare:
1. cambia origine dati;
2. cambia formato;
3. cambia modalita di stampa.

Possibile separazione:
- Report;
- ReportRepository/DataAccess;
- ReportFormatter;
- ReportPrinter.
```

## Accoppiamento

Accoppiamento misura quanto una classe dipende da altre classi.

Basso accoppiamento aiuta a:

- capire una classe senza leggere troppe altre;
- modificare una classe senza effetti diffusi;
- riusare una classe senza portarsi dietro tutto il sistema;
- testare con fake o mock.

Forme di accoppiamento:

- attributo di tipo concreto;
- parametro o variabile locale di tipo concreto;
- ereditarieta non necessaria;
- classe che conosce dettagli interni di altre;
- accesso diretto a DB da molti punti.

Refactoring utili:

- Introduce Interface se esistono varianti o serve testabilita;
- Dependency Injection;
- Move Method;
- Preserve Whole Object;
- DAO/Repository per persistenza;
- Legge di Demetra.

## Legge di Demetra

Spingi information hiding.

Evita:

```java
order.getCustomer().getWallet().getBalance();
```

Preferisci:

```java
order.canBePaid();
customer.canPay(amount);
```

Un metodo dovrebbe parlare solo con:

- `this`;
- attributi di `this`;
- parametri;
- oggetti creati dentro il metodo.

## Responsibility-Driven Design

Analizza codice con:

```text
Classe:
Responsabilita:
Collaboratori:
```

Regole:

- la classe che possiede dati dovrebbe gestire logica strettamente collegata;
- troppi collaboratori indicano possibile accoppiamento eccessivo;
- responsabilita vaghe indicano possibile bassa coesione;
- responsabilita disperse indicano possibile Shotgun Surgery.

## Principio aperto/chiuso

Una classe dovrebbe essere:

- aperta all'estensione;
- chiusa alla modifica.

Durante refactoring, applicalo solo quando c'e variazione reale o frequente. Non creare gerarchie speculative.
