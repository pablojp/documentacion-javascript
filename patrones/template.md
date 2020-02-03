# Patrón Template (Plantilla)

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
