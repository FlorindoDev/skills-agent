
# Legge di Demetra examples

Usa questa reference quando trovi catene di chiamate, accesso a dati interni o manipolazione fuori posto.

## Segnale negativo

```java
user.getAccount().getWallet().getBalance();
```

Problema:

```text
Il codice conosce troppa struttura interna degli oggetti.
Se cambia Account o Wallet, questo codice rischia di rompersi.
```


Soluzione:

```java
user.getBalance();
```

Oppure:

```java
user.canPay(amount);
```

Preferisci chiedere all'oggetto di fare qualcosa, invece di prendere i suoi dati interni e manipolarli fuori.

## Paper boy rule

Problema:

```text
PaperBoy prende il wallet del Customer e decide come pagarsi.
```

Questo rompe incapsulamento: PaperBoy conosce dettagli interni di Customer e Wallet.

Soluzione:

```text
Customer espone pay(amount) o canPay(amount).
PaperBoy chiede al Customer di pagare.
```

Regola:

```text
Non prendere dati interni per fare lavoro fuori. Chiedi all'oggetto giusto di fare il lavoro.
```
