# Patrón Strategy (Estrategia)

Es un patrón de diseño de comportamiento que permite la encapsulación de algoritmos alternativos para una tarea en particular. Define una familia de algoritmos y los encapsula de tal manera que son intercambiables en tiempo de ejecución sin interferencia o conocimiento del cliente.

En el siguiente ejemplo, creamos una clase Commutepara encapsular todas las estrategias posibles para ir al trabajo. A continuación, definimos tres estrategias a saber Bus, PersonalCary Taxi. Usando este patrón podemos intercambiar la implementación para usarla para el travelmétodo del Commuteobjeto en tiempo de ejecución.

```javascript
// encapsulation
class Commute {
  travel(transport) {
    return transport.travelTime();
  }
}

class Vehicle {
  travelTime() {
    return this._timeTaken;
  }
}

// strategy 1
class Bus extends Vehicle {
  constructor() {
    super();
    this._timeTaken = 10;
  }
}

// strategy 2
class Taxi extends Vehicle {
  constructor() {
    super();
    this._timeTaken = 5;
  }
}

// strategy 3
class PersonalCar extends Vehicle {
  constructor() {
    super();
    this._timeTaken = 3;
  }
}

// usage
const commute = new Commute();

console.log(commute.travel(new Taxi())); // 5
console.log(commute.travel(new Bus())); // 10
```

