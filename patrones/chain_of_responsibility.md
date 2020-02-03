# Patrón Chain of Responsibility (Cadena de responsabilidad)

Este es un patrón de diseño de comportamiento que proporciona una cadena de objetos sueltos. Cada uno de estos objetos puede elegir actuar o manejar la solicitud del cliente.

Un buen ejemplo del patrón de la cadena de responsabilidad es el evento que burbujea en DOM en el que un evento se propaga a través de una serie de elementos DOM anidados, uno de los cuales puede tener un "escucha de eventos" adjunto para escuchar y actuar en el evento.

En este ejemplo, creamos una clase `CumulativeSum`, que puede ser instanciada con un opcional `initialValue`. Tiene un método `add` que agrega el valor pasado al atributo `sum` del objeto y devuelve el mismo objeto para permitir el encadenamiento de llamadas a métodos `add`.

Este es un patrón común que también se puede ver en jQuery , donde casi cualquier llamada a un método en un objeto jQuery devuelve un objeto jQuery para que las llamadas a los métodos se puedan encadenar.

```javascript
class CumulativeSum {
  constructor(intialValue = 0) {
    this.sum = intialValue;
  }

  add(value) {
    this.sum += value;
    return this;
  }
}

// usage
const sum1 = new CumulativeSum();
console.log(sum1.add(10).add(2).add(50).sum); // 62


const sum2 = new CumulativeSum(10);
console.log(sum2.add(10).add(20).add(5).sum); // 45
```
