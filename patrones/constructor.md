# Patrón Constructor

Este es un patrón de diseño creacional basado en clases. Los constructores son funciones especiales que se pueden usar 
para crear instancias de nuevos objetos con métodos y propiedades definidas por esa función.

No es uno de los patrones de diseño clásicos. De hecho, es más una construcción de lenguaje básico que un patrón en la 
mayoría de los lenguajes orientados a objetos. Pero en JavaScript, los objetos se pueden crear sobre la marcha sin 
ninguna función de constructor o definición de "clase". Por lo tanto, creo que es importante sentar las bases para que 
otros patrones vengan con este sencillo.

El patrón de constructor es uno de los patrones más utilizados en JavaScript para crear nuevos objetos de un tipo determinado.

En este ejemplo, definimos una Heroclase con atributos como namey specialAbilityy métodos como getDetails. Luego, 
instanciamos un objeto IronManinvocando el método del constructor con la newpalabra clave pasando los valores de los 
atributos respectivos como argumentos.

```javascript
// traditional Function-based syntax
function Hero(name, specialAbility) {
  // setting property values
  this.name = name;
  this.specialAbility = specialAbility;

  // declaring a method on the object
  this.getDetails = function() {
    return this.name + ' can ' + this.specialAbility;
  };
}

// ES6 Class syntax
class Hero {
  constructor(name, specialAbility) {
    // setting property values
    this._name = name;
    this._specialAbility = specialAbility;

    // declaring a method on the object
    this.getDetails = function() {
      return `${this._name} can ${this._specialAbility}`;
    };
  }
}

// creating new instances of Hero
const IronMan = new Hero('Iron Man', 'fly');

console.log(IronMan.getDetails()); // Iron Man can fly
```
