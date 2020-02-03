# Patrón Prototype (prototipo)

Este patrón es un patrón de diseño de creación basado en objetos. En esto, usamos una especie de "esqueleto" de un objeto existente para crear o instanciar nuevos objetos.

Este patrón es específicamente importante y beneficioso para JavaScript porque utiliza la herencia prototípica en lugar de una herencia clásica orientada a objetos. Por lo tanto, juega con la fuerza de JavaScript y tiene soporte nativo.

En este ejemplo, tenemos un carobjeto que usamos como prototipo para crear otro objeto myCarcon la Object.create función de JavaScript y definir una propiedad adicional owneren el nuevo objeto.

```javascript
// using Object.create as was recommended by ES5 standard
const car = {
  noOfWheels: 4,
  start() {
    return 'started';
  },
  stop() {
    return 'stopped';
  },
};

// Object.create(proto[, propertiesObject])

const myCar = Object.create(car, { owner: { value: 'John' } });

console.log(myCar.__proto__ === car); // true
```
