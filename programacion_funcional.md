# Programación funcional en Javascript

La programación funcional de aprendizaje tiene la reputación de ser muy desafiante. Sin embargo, este es el caso de 
cualquier habilidad que intentes dominar. Entonces, diría que aprender programación funcional no es peor que aprender a 
programar en general, es simplemente diferente.

## Inmutabilidad

En la Programación Funcional (FP), tratamos de mutar nuestros datos lo menos posible. En caso de que no esté seguro de 
lo que esto significa, otra forma de decirlo es que tratamos de cambiar el valor de nuestras variables lo menos posible. 
Por ejemplo, tome la siguiente declaración:

```javascript
const a = 1;
```

La variable `a` nunca debe cambiar. Nunca debería ser otra cosa que 1. En este caso, estamos usando el `const`, por lo 
que no podemos cambiarlo sin ningún error. Sin embargo, las matrices le permiten a usted `push` o `pop` de elementos incluso 
cuando se declaran con const. Y no deberías hacer esto en la programación funcional.

La razón por la que digo que debemos mutar nuestros datos lo menos posible es porque nuestro programa todavía necesita hacer algo. Si los datos nunca mutaran, no pasaría nada, lo cual es bastante inútil. Sin embargo, la diferencia entre FP y "programación normal" es que la mutación ocurre de manera muy controlada.

Por ejemplo, todas las mutaciones normalmente ocurren al final de nuestro programa. Entiendo completamente por qué esto no tendrá sentido en este momento. Sin embargo, a medida que aprenda más, la bombilla se apagará en su cabeza. Por el momento, intente tener la mentalidad de que intentará y nunca mutará datos a menos que sea absolutamente necesario. Además, a medida que mejore en esto, verá que a menudo hay lugares donde pensará que tiene que hacerlo cuando realmente no lo hace.

Entonces, ¿por qué nos esforzamos por la inmutabilidad? Hay muchas razones, pero al menos mencionaré la razón número uno que creo que es importante: la estabilidad. Si sabe que su variable nunca cambia, sabe que puede confiar en que los datos están allí y puede garantizar que tiene el valor que espera. De este modo, su código tendrá menos posibilidades de albergar errores inesperados. Un gran beneficio, ¿verdad?

Entiendo por qué podrías ser escéptico en este momento. Preguntas como "¿Cómo voy a hacer que las cosas sucedan en mi programa?" Y "¿Cómo puedo agregar un elemento a mi matriz?" Probablemente te están surgiendo en la cabeza. Hablaré más sobre esto a medida que avancemos, pero ahora mismo, diré esto: en lugar de cambiar nuestros datos todo el tiempo, en FP creamos nuevos datos basados ​​en los datos existentes y trabajamos con eso. Esto se hará más claro a medida que avancemos. ¡Créeme!


## Funciones puras

En el gran espíritu de inmutabilidad, continuemos con el concepto de funciones puras. Como su nombre lo indica, las funciones son bastante importantes en la programación funcional. Afortunadamente para nosotros, en Javascript, las funciones son ciudadanos de primera clase. Esto lo convierte en un lenguaje bastante bueno para aprender FP.

En FP, todas las funciones deben ser puras, al menos cuando sea razonable. Pero, ¿qué significa puro? Significa que la función no tiene efectos secundarios. Duh ...

OK, intentemos otra pista. Las funciones puras devuelven el mismo valor cada vez que se le da la misma entrada.
¿Todavía no estás seguro de lo que eso significa? Eso es completamente comprensible. Déjame darte algunos ejemplos.

```javascript
let a = 1;
// Not pure, changes 'a' which is declared outside the function
function increaseA (addition) {
    a += addition;
    return a;
}
increaseA(2); // returns a which is now 3
increaseA(2); // returns a which is now 5
```

Veamos una función pura:
```javascript
const a = 1;
function add (num1, num2) {
    return num1 + num2;
}
add(a, 2); // returns a new value 3
add(a, 2); // returns a new value 3
```

La función `add` es pura porque solo hace el trabajo en sus argumentos. También tenga en cuenta que no cambia ningún argumento, solo devuelve un nuevo valor basado en los dos.

Recuerde que también mencioné que una función pura no debería tener efectos secundarios. Aquí hay algunos otros efectos secundarios que pueden no ser obvios:

* `console.log` (cambiando el mundo exterior, específicamente la salida)
* Escribir en un archivo (cambia el mundo exterior, el sistema de archivos)
* Aleatoriedad, es decir Math.random(no devuelve el mismo valor basado en la misma entrada)

Con suerte, esto deja en claro qué es una función pura.


## Currying

Hoy hablaremos de curry. Entonces, ¿qué es? En resumen, es una técnica que hace posible llamar parcialmente a su 
función para hacer una función completamente nueva, donde faltan algunos de los argumentos para aplicarla completamente 
en la llamada inicial.
Para hacer una función curry, en lugar de escribirla así:

```javascript
function add (a, b) {
    return a + b
}
```

La escribimos así:

```javascript
function add (a) {
    return function (b) {
        return a + b
    }
}
```

Esto puede parecer un poco raro. Aquí, la función interna obtiene acceso al parámetro `a` mediante el return 
(una función tiene acceso a todas las variables declaradas fuera de ella).

Desafortunadamente, funciones como esta son más difíciles de leer que las funciones escritas de forma "normal". 
Pero esto es 2020, y afortunadamente para nosotros, esta función se puede refactorizar usando la sintaxis ES6 como esta:

```javascript
const add = a => b => a + b;
```

Si no has visto esta sintaxis antes, puede parecer un poco raro. Pero es muy útil saber qué está pasando. Tenga en 
cuenta que no usamos `return` aquí. Cuando devuelve instantáneamente un valor en su función, se puede 
omitir y el intérprete lo entenderá. Si no se utilizan corchetes `{}` para ajustar un cuerpo de función flecha, 
devolverá implícitamente el valor.

Entonces, ¿cómo llamamos a esta función?

```javascript
// The first "old" version
add(1, 2) // 3

// The curried version (both with and without the ES6 syntax)
add(1)(2) // 3
```

Algunos afirmarán que llamar a la versión curry es más feo debido a todos los paréntesis. Pero te acostumbrarás. 
Además, a medida que avancemos en los conceptos de FP, comenzará a ver grandes beneficios al escribir funciones curriculares.

### Aplicación parcial

Entonces, ¿qué funcionalidad adicional nos brinda esto? Bueno, supongamos que a menudo agrega un número con 2. 
Puede crear una nueva función que haga exactamente eso. Sé que el ejemplo es bastante inútil, pero solo tómalo con una 
pizca de sal, ya que es solo para fines de demostración.

```javascript
// Create a new function
const add2 = add(2);

// Now, add2 is a new function
add2(1) // 3
add2(8) // 10
```

Esta técnica es lo que llamamos aplicación parcial porque no aplicamos la función por completo. Simplemente le damos el 
primer argumento que devuelve la función interna a la que le falta su argumento. La función interna obtiene acceso al 
argumento de la función externa a través del cierre. ¿Tiene sentido?
Para aclarar, permítame mostrarle una forma útil de pensarlo cuando llamamos a `add(2)`.

```javascript
function add (a) {
    return function (b) {
        return a + b
    }
}

const add2 = add(2);

// A la variable 'a' se le asigna el valor 2, 
// a la que tiene acceso la función interna.
const a = 2;

//'add2' se asigna a la función interna
const add2 = function (b) {
    return a + b;
}
```


## ¿Qué es componer?

Puede que no te sorprenda que las funciones son los bloques de construcción más fundamentales en la Programación 
Funcional (FP). Esto también es cierto cuando se codifica en un estilo orientado a objetos, pero en FP los usamos de 
manera un poco diferente. Como todo el programa está hecho de pequeños bloques de construcción, necesitamos algunas 
técnicas para que funcionen juntos. Y aquí es donde entra componer. Quiero que piense en componer como una forma de 
combinar dos o más funciones para crear una nueva función.

En FP, hacemos una gran parte de la filosofía de que nuestras funciones solo deben hacer una cosa. Además, las 
funciones deben ser completamente puras, y esta granularidad puede hacer que una sola función parezca inútil. 
Pero cuando se compone junto con otras funciones, el poder de todo realmente comienza a brillar.

Comencemos por hacer algunos ejemplos simples.

```javascript
// Eliminar espacio en blanco adicional entre palabras
const trim = s => s.replace(/ +/g, " ")

// Escribe la primera letra de la cadena en mayúscula
const capitalize = s => 
  s.replace (/^./, c => c.toUpperCase ());

// Pone un signo de exclamación al final de la cadena
const exclaim = s => `${s}!`;
```

Entonces, ¿cómo podemos usar estas funciones para formatear una cadena? Conocí a varios desarrolladores que lo habrían 
hecho como en el siguiente ejemplo, sin ofender si este es usted. Es por eso que estás aquí ¿verdad?

```javascript
let myString = 'an unformatted   string';
myString = trim(myString)
myString = capitalize(myString);
myString = exclaim(myString);
// Result: 'An unformatted string!'
```

Veamos la forma FP:

```javascript
const myString = exclaim (capitalize (trim ('an unformatted   string')));
// Result: 'An unformatted string!'
```

¿Qué, cómo funcionó eso? El truco es leer este código de adentro hacia afuera. Primero se llama a `trim`. Luego se envía el 
resultado de esa función a `capitalize`, luego se envía ese resultado a `exclaim` que devuelve la cadena final. Muy bien, 
¿eh? Y todo esto sucedió sin mutar ningún dato. La cadena original se deja intacta porque estamos componiendo usando 
solo funciones puras.

Otra cosa interesante es que, si formatear una cadena como esta es algo que hacemos a menudo, podríamos hacer una nueva 
función como esta:

```javascript
const formatString = x => exclaim (capitalize (trim (x)));

formatString('yo, format   me    plz') 
// Result:  Yo, format me plz!
```

Wow, mira eso, acabamos de hacer una función general que se puede reutilizar. OK, quizás no sea la función más útil del 
mundo. Pero espero que empieces a ver el poder que proporciona.

En FP puedes ver funciones como piezas de Lego. Cuando trabaje en un programa para un dominio específico, se 
sorprenderá al ver la cantidad de código que estamos repitiendo. Con funciones pequeñas y concisas que solo hacen una 
cosa, tendrá menos duplicación de código. También tendrá menos errores, y sus funciones pueden ser fácilmente 
comprobables, uno de los grandes beneficios de usar funciones puras.


## La función compose

Como puede haber descubierto, tener funciones envueltas en una función que nuevamente está envuelta en una función, 
no es exactamente bueno para la legibilidad. Entonces, ¿por qué no escribimos nuestra propia función para manejar esto? 
Nos encantan las funciones ¿verdad?

Veamos primero la versión simple:


```javascript
// Nuestra simple función de componer que solo
// funciona con dos funciones
const compose = (f, g) => x => f (g (x));

// Hacemos nuestra función reutilizable
const capitalizeAndExclaim = compose(exclaim, capitalize);

// Y se llama así
capitalizeAndExclaim('hello') // Hello!
```

¿Ves lo que está pasando aquí? Nuestra función `compose` toma funciones `f` y `g` como argumentos. Luego devuelve una nueva 
función que toma una cadena `x` como argumento. Observe que ordenado se ve.

Sin embargo, hay una cosa rara que notar aquí. Las funciones se aplican de derecha a izquierda, y esto es por 
convención. Si se desplaza hacia arriba y ve cómo aplicamos la función antes de hacer `compose`, podría tener más 
sentido. En ese ejemplo, también lees de derecha a izquierda.

¿Qué pasa si queremos componer más de dos funciones?. Bueno, entonces la función `compose` se vuelve mucho más 
complicada y, para la mayoría de las personas, ilegible. [Este artículo](https://medium.com/@dtipson/creating-an-es6ish-compose-in-javascript-ac580b95104a) hace un muy buen trabajo explicando cómo 
funciona si está interesado.

```javascript
const compose = (...fns) => fns.reduce((f, g) => (...args) => f(g(...args)));
```

Sin embargo `compose`, realmente no necesita saber cómo funciona internamente para usarlo.

```javascript
const capitalizeAndShout = compose(exclaim, exclaim, exclaim, capitalize, trim);

capitalizeAndShout('yo, format    me   plz') 
// Result: 'Yo, format me plz!!!'
```

Mira cuán limpio se vuelve esto. Es casi como leer un libro, ¿verdad? Primero recorto, luego capitalizo, 
luego exclamo tres veces.

De nuevo, `compose` funciona igual que nuestro primer ejemplo. El argumento final que pasa se envía a la función más a la 
derecha. Luego, los resultados se pasan a la función a la izquierda de la misma, antes de que se devuelva el resultado 
de la función situada más a la izquierda para toda la expresión.

También hay una contraparte que funciona de izquierda a derecha, normalmente llamada `pipe`. Si realmente no puede 
entender leer de derecha a izquierda, no dude en usar `pipe`. Pero normalmente, no tomará mucho tiempo acostumbrarse 
`compose`.

## Pointfree

Necesito consesarme. Hay otra técnica que te he estado ocultando. ¿Se dio cuenta de que no usamos ningún paréntesis 
después `exclaim`, `trim` y `capitalize` cuando compusimos? ¿Como puede ser? Bueno, estamos utilizando un concepto 
llamado ejecución sin puntos. Verá, en JavaScript, podemos omitir el último argumento de una función si tenemos la 
intención de llamarlo con algunos argumentos en una etapa posterior. Tomemos, por ejemplo, la función `trim` de la 
redacción anterior. Cuando declaramos `capitalizeAndShout` no estamos ejecutando nada. Eso sucede solo cuando corremos 
`capitalizeAndShout('yo, format me plz')`. Y ese es el momento en que `trim` envía su argumento.

Déjame mostrarte otro ejemplo usando `array.map`

```javascript
const myArray = [1, 2, 3, 4, 5];
const increase = n => n + 1;

// How many developers will use increase
const myNewArray = myArray.map(item => increase (item));
// Result: [2, 3, 4 , 5, 6]

// How to do the same with pointfree style
const myNewArray = myArray.map(increase);
// Result: [2, 3, 4 , 5, 6]
```

Recuerde que la función a la que envía `map` no se ejecuta de inmediato. Se ejecuta cada vez que llegamos a un 
elemento en nuestro bucle. JavaScript llamará a la función pasada con el elemento como argumento automáticamente. 
Entonces, usar la primera versión solo hace que su código sea más complejo de leer. Es mucho más fácil leer la segunda 
parte: mapeamos cada elemento de la matriz y aumentamos el número.

Te recomiendo que comiences a acostumbrarte al estilo libre de puntos. Después de un tiempo, se vuelve natural. 
Simplemente se siente bien con menos desorden.

[Link fuente](https://levelup.gitconnected.com/functional-programming-for-javascript-developers-compose-508d71b4e7b8)
