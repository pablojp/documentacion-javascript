# Patrón Iterator (Iterador)

Es un patrón de diseño de comportamiento que proporciona una forma de acceder a los elementos de un objeto agregado secuencialmente sin exponer su representación subyacente.

Los iteradores tienen un tipo especial de comportamiento en el que pasamos a través de un conjunto ordenado de valores uno a la vez llamando `next()` hasta llegar al final. La introducción de Iterator and Generators en ES6 hizo que la implementación del patrón iterador fuera extremadamente sencilla.

Tenemos dos ejemplos a continuación. Primero, un `IteratorClass` usa especificaciones del iterador, mientras que el otro `iteratorUsingGenerator` usa funciones de generador.

El `Symbol.iterator` (`Symbol` —un nuevo tipo de tipo de datos primitivo) se usa para especificar el iterador predeterminado para un objeto. Se debe definir para que una colección pueda usar la `for...of` construcción de bucle. En el primer ejemplo, definimos el constructor para almacenar una colección de datos y luego definimos `Symbol.iterator`, lo que devuelve un objeto con método `next` para la iteración.

Para el segundo caso, definimos una función generadora que le pasa una matriz de datos y devuelve sus elementos iterativamente usando `next` y `yield`. Una función generadora es un tipo especial de función que funciona como una fábrica para iteradores y puede mantener explícitamente su propio estado interno y generar valores de forma iterativa. Puede pausar y reanudar su propio ciclo de ejecución.

```javascript
// using Iterator
class IteratorClass {
  constructor(data) {
    this.index = 0;
    this.data = data;
  }

  [Symbol.iterator]() {
    return {
      next: () => {
        if (this.index < this.data.length) {
          return { value: this.data[this.index++], done: false };
        } else {
          this.index = 0; // to reset iteration status
          return { done: true };
        }
      },
    };
  }
}

// using Generator
function* iteratorUsingGenerator(collection) {
  var nextIndex = 0;

  while (nextIndex < collection.length) {
    yield collection[nextIndex++];
  }
}

// usage
const gen = iteratorUsingGenerator(['Hi', 'Hello', 'Bye']);

console.log(gen.next().value); // 'Hi'
console.log(gen.next().value); // 'Hello'
console.log(gen.next().value); // 'Bye'
```
