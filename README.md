# Javascript

## Patrones de diseño en Javascript

En este artículo, vamos a hablar sobre patrones de diseño que pueden y deben usarse para escribir un código JavaScript 
mejor y mantenible. Supongo que tiene una comprensión básica de JavaScript y conceptos como clases (las clases en 
JavaScript pueden ser complicadas), objetos, herencia de prototipos, cierres, etc.

Este artículo es una lectura larga en su conjunto debido a la naturaleza del tema, por lo que he tratado de mantener 
las secciones independientes. De modo que usted, como lector, puede elegir partes específicas (o, en este caso, 
patrones específicos) e ignorar las que no le interesan o con las que está muy familiarizado. Ahora, comencemos.

### Introducción

Escribimos código para resolver problemas. Estos problemas generalmente tienen muchas similitudes y, cuando tratamos de 
resolverlos, notamos varios patrones comunes. Aquí es donde entran los patrones de diseño.

> Un patrón de diseño es un término utilizado en ingeniería de software para una solución general y reutilizable a un problema común en el diseño de software.

El concepto subyacente de los patrones de diseño ha existido en la industria de la ingeniería de software desde el 
principio, pero en realidad no estaban tan formalizados. Patrones de diseño: elementos de software reutilizable 
orientado a objetos escrito por Erich Gamma, Richard Helm, Ralph Johnson , y John Vlissides - la famosa banda de los 
cuatro (GOF) -era un papel decisivo en empujando el concepto formal de los patrones de diseño en ingeniería de software. 
Ahora, los patrones de diseño son una parte esencial del desarrollo de software y lo han sido durante mucho tiempo.

Hubo 23 patrones de diseño introducidos en el libro original.

> Agregar tabla con patrones

Los patrones de diseño son beneficiosos por varias razones. Son soluciones comprobadas que los veteranos de la 
industria han probado y probado. Son enfoques sólidos que resuelven problemas de una manera ampliamente aceptada y 
reflejan la experiencia y los conocimientos de los desarrolladores líderes de la industria que ayudaron a definirlos. 
Los patrones también hacen que su código sea más reutilizable y legible al tiempo que acelera enormemente el proceso de 
desarrollo.

Los patrones de diseño no son soluciones terminadas. Solo nos proporcionan enfoques o esquemas para resolver un problema.

> Nota: En este artículo, hablaremos principalmente sobre patrones de diseño desde un punto de vista orientado a objetos y en el contexto de su usabilidad en JavaScript moderno. Es por eso que se pueden omitir muchos patrones clásicos de GoF, y se incluirán algunos patrones modernos de fuentes como [Learn JavaScript Design Patterns de Addy Osmani](https://addyosmani.com/resources/essentialjsdesignpatterns/book/). Los ejemplos se mantienen simples para facilitar la comprensión y, por lo tanto, no son la implementación más optimizada de sus respectivos patrones de diseño.


### Categorías de patrones de diseño

Los patrones de diseño generalmente se clasifican en tres grupos principales.

#### Patrones de diseño creacional
Como su nombre indica, estos patrones son para manejar mecanismos de creación de objetos. Un patrón de diseño 
creacional básicamente resuelve un problema controlando el proceso de creación de un objeto.

Analizaremos en detalle los siguientes patrones: Patrón de constructor, Patrón de fábrica, Patrón de prototipo y Patrón de Singleton.

#### Patrones de diseño estructural
Estos patrones se refieren a la composición de clases y objetos. Ayudan a estructurar o reestructurar una o más partes 
sin afectar todo el sistema. En otras palabras, ayudan a obtener nuevas funcionalidades sin alterar las existentes.

Discutiremos los siguientes patrones en detalle: Patrón de adaptador, Patrón compuesto, Patrón de decoración, Patrón de 
fachada, Patrón de peso mosca y Patrón de proxy.

#### Patrones de diseño conductual
Estos patrones están relacionados con la mejora de la comunicación entre objetos diferentes.

Analizaremos en detalle los siguientes patrones: Patrón de cadena de responsabilidad, Patrón de comando, Patrón de 
iterador, Patrón de mediador, Patrón de observador, Patrón de estado, Patrón de estrategia y Patrón de plantilla.

------

### Patrón Constructor

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


### Patrón Factory (Fábrica)

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


### Patrón Prototype (prototipo)

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

### Patrón Singleton

Singleton es un patrón de diseño creacional especial en el que solo puede existir una instancia de una clase. Funciona así: si no existe una instancia de la clase singleton, se crea y devuelve una nueva instancia, pero si ya existe una instancia, se devuelve la referencia a la instancia existente.

Un ejemplo perfecto de la vida real sería el de mongoose(la famosa biblioteca ODM Node.js para MongoDB). Utiliza el patrón singleton.

En este ejemplo, tenemos una Databaseclase que es un singleton. Primero, creamos un objeto mongousando el newoperador para invocar el Databaseconstructor de la clase. Esta vez se crea una instancia de un objeto porque ya no existe ninguno. La segunda vez, cuando creamos el mysqlobjeto, no se instancia ningún objeto nuevo, sino que mongose devuelve la referencia al objeto que se instanciaba anteriormente, es decir, el objeto.


```javascript
class Database {
  constructor(data) {
    if (Database.exists) {
      return Database.instance;
    }
    this._data = data;
    Database.instance = this;
    Database.exists = true;
    return this;
  }

  getData() {
    return this._data;
  }

  setData(data) {
    this._data = data;
  }
}

// usage
const mongo = new Database('mongo');
console.log(mongo.getData()); // mongo

const mysql = new Database('mysql');
console.log(mysql.getData()); // mongo
```


### Patrón Adapter (Adaptador)

Este es un patrón estructural donde la interfaz de una clase se traduce en otra. Este patrón permite que las clases trabajen juntas de otra manera que no podrían debido a interfaces incompatibles.

Este patrón a menudo se usa para crear contenedores para nuevas API refactorizadas para que otras API antiguas existentes puedan seguir trabajando con ellas. Esto generalmente se hace cuando las nuevas implementaciones o la refactorización de código (por razones como ganancias de rendimiento) dan como resultado una API pública diferente, mientras que las otras partes del sistema todavía usan la API anterior y necesitan adaptarse para trabajar juntas.

En este ejemplo, tenemos una API antigua, es decir OldCalculator, clase, y una nueva API, es decir, NewCalculatorclase. La OldCalculatorclase proporciona un operationmétodo para sumar y restar, mientras que NewCalculatorproporciona métodos separados para sumar y restar. La clase Adaptador CalcAdapterenvuelve NewCalculatorpara agregar el operationmétodo a la API pública mientras usa su propia implementación de suma y resta bajo el capó.

```javascript
// old interface
class OldCalculator {
  constructor() {
    this.operations = function(term1, term2, operation) {
      switch (operation) {
        case 'add':
          return term1 + term2;
        case 'sub':
          return term1 - term2;
        default:
          return NaN;
      }
    };
  }
}

// new interface
class NewCalculator {
  constructor() {
    this.add = function(term1, term2) {
      return term1 + term2;
    };
    this.sub = function(term1, term2) {
      return term1 - term2;
    };
  }
}

// Adapter Class
class CalcAdapter {
  constructor() {
    const newCalc = new NewCalculator();

    this.operations = function(term1, term2, operation) {
      switch (operation) {
        case 'add':
          // using the new implementation under the hood
          return newCalc.add(term1, term2);
        case 'sub':
          return newCalc.sub(term1, term2);
        default:
          return NaN;
      }
    };
  }
}

// usage
const oldCalc = new OldCalculator();
console.log(oldCalc.operations(10, 5, 'add')); // 15

const newCalc = new NewCalculator();
console.log(newCalc.add(10, 5)); // 15

const adaptedCalc = new CalcAdapter();
console.log(adaptedCalc.operations(10, 5, 'add')); // 15;
```


### Patrón Composite (Compuesto)

Este es un patrón de diseño estructural que compone objetos en estructuras en forma de árbol para representar jerarquías de partes enteras. En este patrón, cada nodo en la estructura en forma de árbol puede ser un objeto individual o una colección compuesta de objetos. Independientemente, cada nodo se trata de manera uniforme.


>> agregar imagen

Es un poco complejo visualizar este patrón. La forma más fácil de pensar en esto es con el ejemplo de un menú multinivel. Cada nodo puede ser una opción distinta, o puede ser un menú en sí mismo, que tiene múltiples opciones como elemento secundario. Un componente de nodo con hijos es un componente compuesto, mientras que un componente de nodo sin ningún hijo es un componente hoja.

En este ejemplo, creamos una clase base Componentque implementa las funcionalidades comunes necesarias y abstrae los otros métodos necesarios. La clase base también tiene un método estático que utiliza la recursividad para atravesar una estructura de árbol compuesta hecha con sus subclases. Luego creamos dos subclases que amplían la clase base, Leafque no tiene hijos y Compositeque pueden tener hijos, y, por lo tanto, tenemos métodos para agregar, buscar y eliminar funcionalidades secundarias. Las dos subclases se utilizan para crear una estructura compuesta: un árbol, en este caso.

```javascript
class Component {
  constructor(name) {
    this._name = name;
  }

  getNodeName() {
    return this._name;
  }

  // abstract methods that need to be overridden
  getType() {}

  addChild(component) {}

  removeChildByName(componentName) {}

  removeChildByIndex(index) {}

  getChildByName(componentName) {}

  getChildByIndex(index) {}

  noOfChildren() {}

  static logTreeStructure(root) {
    let treeStructure = '';
    function traverse(node, indent = 0) {
      treeStructure += `${'--'.repeat(indent)}${node.getNodeName()}\n`;
      indent++;
      for (let i = 0, length = node.noOfChildren(); i < length; i++) {
        traverse(node.getChildByIndex(i), indent);
      }
    }

    traverse(root);
    return treeStructure;
  }
}

class Leaf extends Component {
  constructor(name) {
    super(name);
    this._type = 'Leaf Node';
  }

  getType() {
    return this._type;
  }

  noOfChildren() {
    return 0;
  }
}

class Composite extends Component {
  constructor(name) {
    super(name);
    this._type = 'Composite Node';
    this._children = [];
  }

  getType() {
    return this._type;
  }

  addChild(component) {
    this._children = [...this._children, component];
  }

  removeChildByName(componentName) {
    this._children = [...this._children].filter(component => component.getNodeName() !== componentName);
  }

  removeChildByIndex(index) {
    this._children = [...this._children.slice(0, index), ...this._children.slice(index + 1)];
  }

  getChildByName(componentName) {
    return this._children.find(component => component.name === componentName);
  }

  getChildByIndex(index) {
    return this._children[index];
  }

  noOfChildren() {
    return this._children.length;
  }
}

// usage
const tree = new Composite('root');
tree.addChild(new Leaf('left'));
const right = new Composite('right');
tree.addChild(right);
right.addChild(new Leaf('right-left'));
const rightMid = new Composite('right-middle');
right.addChild(rightMid);
right.addChild(new Leaf('right-right'));
rightMid.addChild(new Leaf('left-end'));
rightMid.addChild(new Leaf('right-end'));

// log
console.log(Component.logTreeStructure(tree));
/*
root
--left
--right
----right-left
----right-middle
------left-end
------right-end
----right-right
*/
```


### Patrón Decorator (Decorador)

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


### Patrón Façade (Fachada)

Este es un patrón de diseño estructural que se usa ampliamente en las bibliotecas de JavaScript. Se utiliza para proporcionar una interfaz unificada y más simple, orientada al público para facilitar su uso que protege de las complejidades de sus subsistemas o subclases consistentes.

El uso de este patrón es muy común en bibliotecas como jQuery.

En este ejemplo, creamos una API pública con la clase ComplaintRegistry. Expone solo un método para ser utilizado por el cliente, es decir registerComplaint. Se maneja internamente crear instancias de objetos de obligados, ya sea ProductComplainto ServiceComplaintbasados en el argumento de tipo. También maneja todas las demás funcionalidades complejas, como generar una ID única, almacenar la queja en la memoria, etc. Pero, todas estas complejidades se ocultan utilizando el patrón de fachada.

```javascript
let currentId = 0;

class ComplaintRegistry {
  registerComplaint(customer, type, details) {
    const id = ComplaintRegistry._uniqueIdGenerator();
    let registry;
    if (type === 'service') {
      registry = new ServiceComplaints();
    } else {
      registry = new ProductComplaints();
    }
    return registry.addComplaint({ id, customer, details });
  }

  static _uniqueIdGenerator() {
    return ++currentId;
  }
}

class Complaints {
  constructor() {
    this.complaints = [];
  }

  addComplaint(complaint) {
    this.complaints.push(complaint);
    return this.replyMessage(complaint);
  }

  getComplaint(id) {
    return this.complaints.find(complaint => complaint.id === id);
  }

  replyMessage(complaint) {}
}

class ProductComplaints extends Complaints {
  constructor() {
    super();
    if (ProductComplaints.exists) {
      return ProductComplaints.instance;
    }
    ProductComplaints.instance = this;
    ProductComplaints.exists = true;
    return this;
  }

  replyMessage({ id, customer, details }) {
    return `Complaint No. ${id} reported by ${customer} regarding ${details} have been filed with the Products Complaint Department. Replacement/Repairment of the product as per terms and conditions will be carried out soon.`;
  }
}

class ServiceComplaints extends Complaints {
  constructor() {
    super();
    if (ServiceComplaints.exists) {
      return ServiceComplaints.instance;
    }
    ServiceComplaints.instance = this;
    ServiceComplaints.exists = true;
    return this;
  }

  replyMessage({ id, customer, details }) {
    return `Complaint No. ${id} reported by ${customer} regarding ${details} have been filed with the Service Complaint Department. The issue will be resolved or the purchase will be refunded as per terms and conditions.`;
  }
}

// usage
const registry = new ComplaintRegistry();

const reportService = registry.registerComplaint('Martha', 'service', 'availability');
// 'Complaint No. 1 reported by Martha regarding availability have been filed with the Service Complaint Department. The issue will be resolved or the purchase will be refunded as per terms and conditions.'

const reportProduct = registry.registerComplaint('Jane', 'product', 'faded color');
// 'Complaint No. 2 reported by Jane regarding faded color have been filed with the Products Complaint Department. Replacement/Repairment of the product as per terms and conditions will be carried out soon.'
```


### Patrón Flyweight (peso mosca)

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


### Patrón Proxy

Este es un patrón de diseño estructural que se comporta exactamente como su nombre lo sugiere. Actúa como un sustituto o marcador de posición para otro objeto para controlar el acceso a él.

Por lo general, se usa en situaciones en las que un objeto objetivo está bajo restricciones y es posible que no pueda manejar todas sus responsabilidades de manera eficiente. Un proxy, en este caso, generalmente proporciona la misma interfaz al cliente y agrega un nivel de indirección para admitir el acceso controlado al objeto de destino para evitar una presión indebida sobre él.

El patrón de proxy puede ser muy útil cuando se trabaja con aplicaciones con una gran cantidad de solicitudes de red para evitar solicitudes de red innecesarias o redundantes.

En este ejemplo, utilizaremos dos nuevas funciones de ES6, [Proxy](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Proxy) y [Reflect](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Reflect). Un objeto Proxy se usa para definir un comportamiento personalizado para operaciones fundamentales de un objeto JavaScript (recuerde, la función y las matrices también son objetos en JavaScript). Es un método constructor que puede usarse para crear un objeto `Proxy`. Acepta un objeto `target` que debe ser proxy y un objeto `handler` que definirá la personalización necesaria. El objeto controlador permite definir algunas funciones de trampa como `get`, `set`, `has`, `apply`, etc, que se utiliza para añadir un comportamiento personalizado unido a su uso. `Reflect`, por otro lado, es un objeto incorporado que proporciona métodos similares compatibles con el objeto controlador de Proxy como métodos estáticos en sí mismo. No es un constructor; Sus métodos estáticos se utilizan para operaciones JavaScript interceptables.

Ahora, creamos una función que puede considerarse como una solicitud de red. Lo nombramos como `networkFetch`. Acepta una URL y responde en consecuencia. Queremos implementar un proxy donde solo obtengamos la respuesta de la red si no está disponible en nuestro caché. De lo contrario, solo devolveremos una respuesta del caché.

La variable global `cache` almacenará nuestras respuestas en caché. Creamos un proxy nombrado `proxiedNetworkFetch` con nuestro original `networkFetch` como `target` y utilizamos el método de aplicación en nuestro objeto `handler` para representar la invocación de la función. El método de aplicación se pasa al objeto `target` mismo. Este valor como `thisArg` y los argumentos se le pasan en una estructura tipo matriz `arg`.

Verificamos si el argumento url pasado está en el caché. Si existe en el caché, devolvemos la respuesta desde allí, nunca invocando la función de destino original. Si no es así, entonces usamos el método `Reflect.apply` para invocar la función `target` con `thisArg` (aunque no es de ninguna importancia en nuestro caso aquí) y los argumentos que pasó.

```javascript
// Target
function networkFetch(url) {
  return `${url} - Response from network`;
}

// Proxy
// ES6 Proxy API = new Proxy(target, handler);
const cache = [];
const proxiedNetworkFetch = new Proxy(networkFetch, {
  apply(target, thisArg, args) {
    const urlParam = args[0];
    if (cache.includes(urlParam)) {
      return `${urlParam} - Response from cache`;
    } else {
      cache.push(urlParam);
      return Reflect.apply(target, thisArg, args);
    }
  },
});

// usage
console.log(proxiedNetworkFetch('dogPic.jpg')); // 'dogPic.jpg - Response from network'
console.log(proxiedNetworkFetch('dogPic.jpg')); // 'dogPic.jpg - Response from cache'
```


### Patrón Chain of Responsibility (Cadena de responsabilidad)

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


### Patrón Command (Comando)

Este es un patrón de diseño de comportamiento que tiene como objetivo encapsular acciones u operaciones como objetos. Este patrón permite un acoplamiento flexible de sistemas y clases al separar los objetos que solicitan una operación o invocan un método de los que ejecutan o procesan la implementación real.

La API de interacción del portapapeles se parece un poco al patrón de comando. Si eres un usuario de *Redux*, ya has encontrado el patrón de comando. Las acciones que permiten la asombrosa función de depuración de viajes en el tiempo no son más que operaciones encapsuladas que pueden rastrearse para rehacer o deshacer operaciones. Por lo tanto, viajar en el tiempo fue posible.

En este ejemplo, tenemos una clase llamada `SpecialMath` que tiene múltiples métodos y una clase `Command` que encapsula los comandos que se ejecutarán en su tema, es decir, un objeto de la clase `SpecialMath`. La clase `Command` también realiza un seguimiento de todos los comandos ejecutados, que se pueden utilizar para ampliar su funcionalidad para incluir operaciones de tipo deshacer y rehacer.

```javascript
class SpecialMath {
  constructor(num) {
    this._num = num;
  }

  square() {
    return this._num ** 2;
  }

  cube() {
    return this._num ** 3;
  }

  squareRoot() {
    return Math.sqrt(this._num);
  }
}

class Command {
  constructor(subject) {
    this._subject = subject;
    this.commandsExecuted = [];
  }
  execute(command) {
    this.commandsExecuted.push(command);
    return this._subject[command]();
  }
}

// usage
const x = new Command(new SpecialMath(5));
x.execute('square');
x.execute('cube');

console.log(x.commandsExecuted); // ['square', 'cube']
```


### Patrón Iterator (Iterador)

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


### Patrón Mediator (Mediador)

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


### Patrón Observer (Observador)

Es un patrón de diseño de comportamiento crucial que define las dependencias de uno a muchos entre los objetos, de modo que cuando un objeto (editor) cambia su estado, todos los demás objetos dependientes (suscriptores) son notificados y actualizados automáticamente. Esto también se llama PubSub (editor / suscriptores) o patrón de despachador de eventos / oyentes. El editor a veces se llama el tema, y ​​los suscriptores a veces se llaman observadores.

Lo más probable es que ya estés familiarizado con este patrón si has usado addEventListenero jQuery's. onpara escribir código de manejo uniforme. Tiene sus influencias en la programación reactiva (piense en RxJS ) también.

En el ejemplo, creamos una Subjectclase simple que tiene métodos para agregar y eliminar objetos de Observerclase de la colección de suscriptores. Además, un firemétodo para propagar cualquier cambio en el Subjectobjeto de clase a los Observadores suscritos. La Observerclase, por otro lado, tiene su estado interno y un método para actualizar su estado interno en función del cambio propagado desde el que Subjectse ha suscrito.

```javascript
class Subject {
  constructor() {
    this._observers = [];
  }

  subscribe(observer) {
    this._observers.push(observer);
  }

  unsubscribe(observer) {
    this._observers = this._observers.filter(obs => observer !== obs);
  }

  fire(change) {
    this._observers.forEach(observer => {
      observer.update(change);
    });
  }
}

class Observer {
  constructor(state) {
    this.state = state;
    this.initialState = state;
  }

  update(change) {
    let state = this.state;
    switch (change) {
      case 'INC':
        this.state = ++state;
        break;
      case 'DEC':
        this.state = --state;
        break;
      default:
        this.state = this.initialState;
    }
  }
}

// usage
const sub = new Subject();

const obs1 = new Observer(1);
const obs2 = new Observer(19);

sub.subscribe(obs1);
sub.subscribe(obs2);

sub.fire('INC');

console.log(obs1.state); // 2
console.log(obs2.state); // 20
```


### Patrón State (Estado)

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


### Patrón Strategy (Estrategia)

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


### Patrón Template (Plantilla)

Este es un patrón de diseño de comportamiento basado en la definición del esqueleto del algoritmo o la implementación de una operación, pero diferiendo algunos pasos a las subclases. Permite que las subclases redefinan ciertos pasos de un algoritmo sin cambiar la estructura externa del algoritmo.

En este ejemplo, tenemos una clase de Plantilla Employeeque implementa el workmétodo parcialmente. Corresponde a las subclases implementar el método de responsabilidades para que funcione como un todo. Luego creamos dos subclases Developery Testereso extiende la clase de plantilla e implementa el método requerido para llenar el vacío de implementación.

```javascript
class Employee {
  constructor(name, salary) {
    this._name = name;
    this._salary = salary;
  }

  work() {
    return `${this._name} handles ${this.responsibilities() /* gap to be filled by subclass */}`;
  }

  getPaid() {
    return `${this._name} got paid ${this._salary}`;
  }
}

class Developer extends Employee {
  constructor(name, salary) {
    super(name, salary);
  }

  // details handled by subclass
  responsibilities() {
    return 'application development';
  }
}

class Tester extends Employee {
  constructor(name, salary) {
    super(name, salary);
  }

  // details handled by subclass
  responsibilities() {
    return 'testing';
  }
}

// usage
const dev = new Developer('Nathan', 100000);
console.log(dev.getPaid()); // 'Nathan got paid 100000'
console.log(dev.work()); // 'Nathan handles application development'

const tester = new Tester('Brian', 90000);
console.log(tester.getPaid()); // 'Brian got paid 90000'
console.log(tester.work()); // 'Brian handles testing'
```


### Conclusión

Los patrones de diseño son cruciales para la ingeniería de software y pueden ser muy útiles para resolver problemas comunes. Pero este es un tema muy vasto, y simplemente no es posible incluir todo sobre ellos en una pieza corta. Por lo tanto, tomé la decisión de hablar breve y concisamente sobre los que creo que pueden ser realmente útiles para escribir JavaScript moderno. Para profundizar, le sugiero que eche un vistazo a estos libros:

* [Patrones de diseño: elementos de software orientado a objetos reutilizables](https://en.wikipedia.org/wiki/Design_Patterns) por Erich Gamma, Richard Helm, Ralph Johnson y John Vlissides (Gang of Four)
* [Aprender patrones de diseño de JavaScript](https://addyosmani.com/resources/essentialjsdesignpatterns/book/) por Addy Osmani
* [Patrones JavaScript](http://www.amazon.com/JavaScript-Patterns-Stoyan-Stefanov/dp/0596806752) de Stoyan Stefanov


> Fuente: https://medium.com/better-programming/javascript-design-patterns-25f0faaaa15
