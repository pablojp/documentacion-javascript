# Patrón State (Estado)

Es un patrón de diseño de comportamiento que permite que un objeto altere su comportamiento en función de los cambios en su estado interno. El objeto devuelto por una clase de patrón de estado parece cambiar su clase. Proporciona lógica específica de estado a un conjunto limitado de objetos en el que cada tipo de objeto representa un estado particular.

Tomaremos un ejemplo simple de un semáforo para comprender este patrón. La TrafficLightclase cambia el objeto vuelve basado en su estado interno, que es un objeto de Red, Yellowo Greenclase.

```javascript
class TrafficLight {
  constructor() {
    this.states = [new GreenLight(), new RedLight(), new YellowLight()];
    this.current = this.states[0];
  }

  change() {
    const totalStates = this.states.length;
    let currentIndex = this.states.findIndex(light => light === this.current);
    if (currentIndex + 1 < totalStates) this.current = this.states[currentIndex + 1];
    else this.current = this.states[0];
  }

  sign() {
    return this.current.sign();
  }
}

class Light {
  constructor(light) {
    this.light = light;
  }
}

class RedLight extends Light {
  constructor() {
    super('red');
  }

  sign() {
    return 'STOP';
  }
}

class YellowLight extends Light {
  constructor() {
    super('yellow');
  }

  sign() {
    return 'STEADY';
  }
}

class GreenLight extends Light {
	constructor() {
		super('green');
	}

	sign() {
		return 'GO';
	}
}

// usage
const trafficLight = new TrafficLight();

console.log(trafficLight.sign()); // 'GO'
trafficLight.change();

console.log(trafficLight.sign()); // 'STOP'
trafficLight.change();

console.log(trafficLight.sign()); // 'STEADY'
trafficLight.change();

console.log(trafficLight.sign()); // 'GO'
trafficLight.change();

console.log(trafficLight.sign()); // 'STOP'
```
