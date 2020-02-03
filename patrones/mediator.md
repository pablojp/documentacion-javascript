# Patrón Mediator (Mediador)

Es un patrón de diseño de comportamiento que encapsula cómo un conjunto de objetos interactúa entre sí. Proporciona la autoridad central sobre un grupo de objetos al promover un acoplamiento suelto, evitando que los objetos se refieran entre sí explícitamente.

En este ejemplo, tenemos TrafficTowercomo Mediador que controla la forma en que los Airplaneobjetos interactúan entre sí. Todos los Airplaneobjetos se registran con un TrafficTowerobjeto, y es el objeto de clase mediador el que maneja cómo un Airplaneobjeto recibe datos de coordenadas de todos los demás Airplaneobjetos.

```javascript
class TrafficTower {
  constructor() {
    this._airplanes = [];
  }

  register(airplane) {
    this._airplanes.push(airplane);
    airplane.register(this);
  }

  requestCoordinates(airplane) {
    return this._airplanes.filter(plane => airplane !== plane).map(plane => plane.coordinates);
  }
}

class Airplane {
  constructor(coordinates) {
    this.coordinates = coordinates;
    this.trafficTower = null;
  }

  register(trafficTower) {
    this.trafficTower = trafficTower;
  }

  requestCoordinates() {
    if (this.trafficTower) return this.trafficTower.requestCoordinates(this);
    return null;
  }
}

// usage
const tower = new TrafficTower();

const airplanes = [new Airplane(10), new Airplane(20), new Airplane(30)];
airplanes.forEach(airplane => {
  tower.register(airplane);
});

console.log(airplanes.map(airplane => airplane.requestCoordinates())) 
// [[20, 30], [10, 30], [10, 20]]
```

