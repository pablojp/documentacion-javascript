# Patrón Singleton

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
