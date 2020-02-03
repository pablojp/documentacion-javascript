# Patrón Adapter (Adaptador)

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
