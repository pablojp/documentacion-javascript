# Patrón Composite (Compuesto)

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
