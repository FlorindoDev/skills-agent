
Segnali negativi:

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
