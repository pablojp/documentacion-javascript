# Patrón Decorator (Decorador)

Este también es un patrón de diseño estructural que se centra en la capacidad de agregar dinámicamente comportamiento o funcionalidades a las clases existentes. Es otra alternativa viable a la subclasificación.

El comportamiento de tipo decorador es muy fácil de implementar en JavaScript porque JavaScript nos permite agregar métodos y propiedades para objetar dinámicamente. El enfoque más simple sería simplemente agregar una propiedad a un objeto, pero no será reutilizable de manera eficiente.

De hecho, hay una propuesta para agregar decoradores al lenguaje JavaScript. Echa un vistazo a [la publicación de Addy Osmani](https://medium.com/google-developers/exploring-es7-decorators-76ecb65fb841) sobre decoradores en JavaScript.

Si desea leer sobre la [propuesta en sí](https://tc39.es/proposal-decorators/), siéntase libre.

En este ejemplo, creamos una Bookclase. Además, creamos dos funciones de decorador que aceptan un objeto de libro y devuelven un objeto "decorado" book, giftWrapque agrega un nuevo atributo y una nueva función y hardbindBookagrega un nuevo atributo y edita el valor de un atributo existente.


```javascript
class Book {
  constructor(title, author, price) {
    this._title = title;
    this._author = author;
    this.price = price;
  }

  getDetails() {
    return `${this._title} by ${this._author}`;
  }
}

// decorator 1
function giftWrap(book) {
  book.isGiftWrapped = true;
  book.unwrap = function() {
    return `Unwrapped ${book.getDetails()}`;
  };

  return book;
}

// decorator 2
function hardbindBook(book) {
  book.isHardbound = true;
  book.price += 5;
  return book;
}

// usage
const alchemist = giftWrap(new Book('The Alchemist', 'Paulo Coelho', 10));

console.log(alchemist.isGiftWrapped); // true
console.log(alchemist.unwrap()); // 'Unwrapped The Alchemist by Paulo Coelho'

const inferno = hardbindBook(new Book('Inferno', 'Dan Brown', 15));

console.log(inferno.isHardbound); // true
console.log(inferno.price); // 20
```
