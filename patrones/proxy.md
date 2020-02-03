# Patrón Proxy

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
