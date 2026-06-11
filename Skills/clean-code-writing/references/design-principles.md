# Design principles

Usa questa reference quando devi decidere dove mettere responsabilita, come dividere classi o moduli, e come bilanciare qualita diverse del codice.

## Regola di flessibilita

Questi principi sono criteri guida, non una checklist chiusa. Se trovi un criterio di design o un micro-refactoring piu adatto al codice reale, usalo e spiega:

- quale smell o problema di design risolve;
- perche e migliore delle tecniche o dei criteri elencati;
- quale trade-off introduce;
- come preserva il comportamento gia esistente quando modifichi codice;
- come verificarlo con test.

## Design goal e trade-off

Prima di scrivere codice, identifica i criteri piu rilevanti:

- Performance: tempo di risposta, throughput, uso memoria.
- Affidabilita: robustezza, disponibilita, tolleranza ai fault, sicurezza.
- Costi: sviluppo, manutenzione, gestione.
- Manutenibilita: estendibilita, modificabilita, adattabilita, portabilita.
- Usabilita: chiarezza e facilita d'uso per chi usa il sistema o le API.

Non puoi massimizzare tutto. Esplicita i compromessi:

- spazio vs velocita;
- tempo di rilascio vs funzionalita;
- tempo di rilascio vs qualita;
- tempo di rilascio vs numero di persone coinvolte.

Regola pratica:

```text
Anticipare il cambiamento significa rendere semplice modificare il codice, non prevedere ogni possibile futuro.
```

## Decomposizione

Riduci complessita dividendo il sistema in parti piu piccole e relativamente autonome.

Opzioni comuni:

- Layers: separa UI, logica applicativa, persistenza e infrastruttura.
- Partizionamento per funzionalita: ogni area funzionale contiene la parte UI, logica e dati necessari.
- Sottosistemi: ogni sottosistema espone servizi chiari tramite interfacce o API interne.

Quando definisci un sottosistema, specifica:

- operazioni offerte;
- parametri;
- valore di ritorno;
- comportamento ad alto livello;
- dipendenze accettate;
- responsabilita escluse.

Evita accesso diretto al database da tutti i moduli. Introduci un livello DataAccess/DAO/Repository quando serve isolare il DBMS o centralizzare I/O.

## Indipendenza funzionale

Obiettivo: alta coesione e basso accoppiamento.

Alta coesione:

- responsabilita correlate;
- classe centrata su un concetto;
- metodo con un solo compito;
- nomi chiari;
- cambiamenti localizzati.

Basso accoppiamento:

- poche dipendenze;
- dipendenze da interfacce quando utile;
- oggetti che non conoscono dettagli interni degli altri;
- cambiamenti in una classe che non obbligano modifiche diffuse.

## SRP

Single Responsibility Principle:

```text
Una classe dovrebbe avere una sola responsabilita.
Una responsabilita e un motivo per cambiare.
```

Segnale di violazione:

```text
Report carica dati, formatta output e stampa.
```

Soluzione:

```text
Report: rappresenta i dati del report.
ReportRepository/DataAccess: recupera dati.
ReportFormatter: formatta.
ReportPrinter: stampa.
```

## Accoppiamento

Due classi sono accoppiate quando una non puo essere riusata senza l'altra.

Forme comuni:

- attributo di tipo concreto;
- parametro o variabile locale di tipo concreto;
- ereditarieta non necessaria;
- implementazione di interfacce troppo grandi o non coerenti;
- accesso a dettagli interni di un altro oggetto.

Preferisci:

- dependency injection per dipendenze esterne;
- interfacce quando esistono varianti reali o serve testabilita;
- oggetti di dominio con comportamento vicino ai dati;
- confini chiari tra logica, I/O e infrastruttura.

## Legge di Demetra

Un metodo dovrebbe mandare messaggi solo a:

- `this`;
- attributi di `this`;
- parametri del metodo;
- oggetti creati dentro il metodo.

Evita:

```java
user.getAccount().getWallet().getBalance();
```

Preferisci:

```java
user.getBalance();
user.canPay(amount);
```

Motivo: il chiamante non deve conoscere la struttura interna degli oggetti.

## Responsibility-Driven Design

Progetta ogni classe con tre domande:

```text
Classe:
Responsabilita:
Collaboratori:
```

Regole:

- ogni classe deve avere ruolo chiaro;
- la classe che possiede i dati dovrebbe gestire la logica strettamente collegata a quei dati;
- troppi collaboratori indicano possibile accoppiamento eccessivo;
- responsabilita vaghe indicano possibile bassa coesione.

Esempio:

```text
Classe: OrderService
Responsabilita:
- validare ordine;
- orchestrare pagamento;
- salvare esito.

Collaboratori:
- OrderRepository;
- PaymentGateway;
- DiscountPolicy.

Errore:
- aggiungere generazione PDF, invio email e logica UI nello stesso service.
```
