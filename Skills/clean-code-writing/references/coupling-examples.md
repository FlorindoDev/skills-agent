
# Coupling examples

Usa questa reference quando devi ridurre dipendenze concrete o spiegare perche una classe e troppo legata a un'altra.

## Dipendenza concreta

```java
class Traveler {
    Car car = new Car();

    void startJourney() {
        car.move();
    }
}
```

Problema:

```text
Traveler dipende direttamente da Car.
Se voglio usare Bike, Train o Scooter, devo modificare Traveler.
```

Soluzione preferibile:

```java
interface Vehicle {
    void move();
}

class Traveler {
    private Vehicle vehicle;

    Traveler(Vehicle vehicle) {
        this.vehicle = vehicle;
    }

    void startJourney() {
        vehicle.move();
    }
}
```

Vantaggio:

```text
Traveler dipende da un'interfaccia, non da una classe concreta.
Questo abbassa l'accoppiamento e anticipa il cambiamento.
```

## Quando introdurre l'interfaccia

Introduci un'interfaccia quando:

- esistono piu implementazioni reali o molto probabili;
- vuoi testare il client con un fake/mock;
- vuoi isolare una dipendenza esterna;
- il costo di cambiare implementazione concreta sarebbe alto.

Evita l'interfaccia quando:

- c'e una sola implementazione stabile;
- l'interfaccia ripete esattamente la classe concreta senza aggiungere flessibilita;
- nasce solo per "fare clean code" senza problema reale.
