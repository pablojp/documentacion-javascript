# Patrón Factory (Fábrica)

El patrón de fábrica es otro patrón de creación basado en clases. En esto, proporcionamos una interfaz genérica que delega la responsabilidad de la instanciación de objetos a sus subclases.

Este patrón se usa con frecuencia cuando necesitamos administrar o manipular colecciones de objetos que son diferentes pero que tienen muchas características similares.

En este ejemplo, creamos una clase de fábrica llamada BallFactoryque tiene un método que toma parámetros y, dependiendo de los parámetros, delega la responsabilidad de instanciación de objeto a la clase respectiva. Si el parámetro de tipo es `football` o la `soccer` instancia de objeto se maneja por Footballclase, pero si es `basketball` objeto, la instancia se maneja por Basketballclase.

```javascript
class BallFactory {
  constructor() {
    this.createBall = function(type) {
      let ball;
      if (type === 'football' || type === 'soccer') ball = new Football();
      else if (type === 'basketball') ball = new Basketball();
      ball.roll = function() {
        return `The ${this._type} is rolling.`;
      };

      return ball;
    };
  }
}

class Football {
  constructor() {
    this._type = 'football';
    this.kick = function() {
      return 'You kicked the football.';
    };
  }
}

class Basketball {
  constructor() {
    this._type = 'basketball';
    this.bounce = function() {
      return 'You bounced the basketball.';
    };
  }
}

// creating objects
const factory = new BallFactory();

const myFootball = factory.createBall('football');
const myBasketball = factory.createBall('basketball');

console.log(myFootball.roll()); // The football is rolling.
console.log(myBasketball.roll()); // The basketball is rolling.
console.log(myFootball.kick()); // You kicked the football.
console.log(myBasketball.bounce()); // You bounced the basketball.
```
