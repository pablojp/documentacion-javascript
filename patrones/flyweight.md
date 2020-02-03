# Patrón Flyweight (peso mosca)

Este es un patrón de diseño estructural centrado en el intercambio eficiente de datos a través de objetos de grano fino. Se utiliza con fines de eficiencia y conservación de la memoria.

Este patrón se puede utilizar para cualquier tipo de almacenamiento en caché. De hecho, los navegadores modernos usan una variante de un patrón de peso mosca para evitar cargar las mismas imágenes dos veces.

En este ejemplo, creamos una clase de peso mosca de grano fino Icecreampara compartir datos sobre sabores de helados y una clase de fábrica IcecreamFactorypara crear esos objetos de peso mosca. Para la conservación de la memoria, los objetos se reciclan si el mismo objeto se instancia dos veces. Este es un ejemplo simple de implementación de peso mosca.

```javascript
// flyweight class
class Icecream {
  constructor(flavour, price) {
    this.flavour = flavour;
    this.price = price;
  }
}

// factory for flyweight objects
class IcecreamFactory {
  constructor() {
    this._icecreams = [];
  }

  createIcecream(flavour, price) {
    let icecream = this.getIcecream(flavour);
    if (icecream) {
      return icecream;
    } else {
      const newIcecream = new Icecream(flavour, price);
      this._icecreams.push(newIcecream);
      return newIcecream;
    }
  }

  getIcecream(flavour) {
    return this._icecreams.find(icecream => icecream.flavour === flavour);
  }
}

// usage
const factory = new IcecreamFactory();

const chocoVanilla = factory.createIcecream('chocolate and vanilla', 15);
const vanillaChoco = factory.createIcecream('chocolate and vanilla', 15);

// reference to the same object
console.log(chocoVanilla === vanillaChoco); // true
```
