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


