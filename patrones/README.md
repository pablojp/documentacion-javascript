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

Creacionales | Basados en el concepto de crear un objeto 
--- | ---
*Class* | -----------------------------------------------  
Factory Method | Esto crea una instancia de varias clases derivadas basadas en datos o eventos interconectados.
*Object* | -----------------------------------------------
Abstract Factory | Cree una instancia de varias familias sin detallar clases concretas.
Builder | Separa la construcción del objeto de su representación, siempre crea el mismo tipo de objeto.
Prototype | Una instancia completamente inicializada utilizada para copiar y clonar.
Singleton | Una clase con solo una instancia con puntos de acceso global.

> faltan 2 tablas mas


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

Analizaremos en detalle los siguientes patrones:
 * [Constructor](/patrones/constructor.md)
 * [Factory](/patrones/factory.md)
 * [Prototype](/patrones/prototype.md)
 * [Singleton](/patrones/singleton.md)
 

#### Patrones de diseño estructural
Estos patrones se refieren a la composición de clases y objetos. Ayudan a estructurar o reestructurar una o más partes 
sin afectar todo el sistema. En otras palabras, ayudan a obtener nuevas funcionalidades sin alterar las existentes.

Discutiremos los siguientes patrones en detalle: 
 * [Adapter](/patrones/adapter.md)
 * [Composite](/patrones/composite.md) (falta agregar imagen)
 * [Decorator](/patrones/decorator.md)
 * [Facade](/patrones/facade.md)
 * [Flyweight](/patrones/flyweight.md)
 * [Proxy](/patrones/proxy.md)

#### Patrones de diseño conductual
Estos patrones están relacionados con la mejora de la comunicación entre objetos diferentes.

Analizaremos en detalle los siguientes patrones: 
 * [Chain of Responsibility](/patrones/chain_of_responsibility.md)
 * [Command](/patrones/command.md)
 * [Iterator](/patrones/iterator.md)
 * [Mediator](/patrones/mediator.md)
 * [Observer](/patrones/observer.md)
 * [State](/patrones/state.md)
 * [Strategy](/patrones/strategy.md)
 * [Template](/patrones/template.md)


### Conclusión

Los patrones de diseño son cruciales para la ingeniería de software y pueden ser muy útiles para resolver problemas comunes. Pero este es un tema muy vasto, y simplemente no es posible incluir todo sobre ellos en una pieza corta. Por lo tanto, tomé la decisión de hablar breve y concisamente sobre los que creo que pueden ser realmente útiles para escribir JavaScript moderno. Para profundizar, le sugiero que eche un vistazo a estos libros:

* [Patrones de diseño: elementos de software orientado a objetos reutilizables](https://en.wikipedia.org/wiki/Design_Patterns) por Erich Gamma, Richard Helm, Ralph Johnson y John Vlissides (Gang of Four)
* [Aprender patrones de diseño de JavaScript](https://addyosmani.com/resources/essentialjsdesignpatterns/book/) por Addy Osmani
* [Patrones JavaScript](http://www.amazon.com/JavaScript-Patterns-Stoyan-Stefanov/dp/0596806752) de Stoyan Stefanov


> Fuente: https://medium.com/better-programming/javascript-design-patterns-25f0faaaa15
