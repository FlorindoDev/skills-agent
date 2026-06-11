
Segnale negativo:

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