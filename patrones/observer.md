# Patrón Observer (Observador)

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

