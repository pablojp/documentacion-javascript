# Patrón Command (Comando)

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
