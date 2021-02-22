# DISEÑO DE CAPAS DEL DOMINIO

        ​ Diseño de Capas del Dominio

Este capítulo muestra cómo diseñar la interacción entre objetos (modelado dinámico) para implementar restricciones de operación del sistema utilizando diagramas de interacción UML (comunicación y secuencia). Inicialmente, la responsabilidad y la visibilidad de los objetos se explican para mostrar que los objetos sólo pueden comunicarse entre sí para cumplir con sus responsabilidades si tienen una línea de visibilidad que seguir. A continuación, el capítulo discute cómo construir modelos dinámicos en los que los objetos cambian los mensajes para realizar las acciones necesarias para cumplir con las condiciones posteriores de una restricción, y cómo las condiciones previas y las excepciones lo afectan. Se presentan patrones de diseño para la distribución de responsabilidad entre objetos con el fin de mejorar el diseño de código orientado a objetos con delegación y bajo acoplamiento. Finalmente, el capítulo explica cómo usar la información aprendida durante el modelado dinámico para mejorar el diagrama de clase de diseño.

                ​ Palabras clave
Object responsibility; object visibility; delegation; low coupling; communication diagram; interaction diagram; design class diagram

            ​ Conceptos en este Capítulo

    • Responsabilidad
    • Visibilidad
    • Bajo Acoplamiento
    • Delegación
    • Modelado dinámico
    • Diagrama de clase de diseño

            ​ 9.1 Introducción al diseño de capas del dominio
El diseño de software en general tiene como objetivo producir una solución a un problema que ya ha sido suficientemente aclarado por el análisis. Los aspectos estáticos del problema se representan en el modelo conceptual y los aspectos funcionales se representan en los casos de uso ampliados, diagramas de secuencia del sistema y restricciones de operación del sistema. Ahora es el momento de diseñar una solución de software (y posiblemente de hardware) para implementar los aspectos lógicos y tecnológicos del sistema. En este sentido el diseño es una solución para un problema modelado por el análisis.
Durante las iteraciones, después de expandir los casos de uso, refinar el modelo conceptual y redactar las restricciones, el equipo puede llevar a cabo actividades de diseño, que pueden dividirse en dos grupos:
    • Diseño lógico (este capítulo), que incluye los aspectos del problema relacionados con la lógica del negocio. Normalmente el diseño lógico se representa en el diagrama de clase de diseño (DCD), que evoluciona a partir del modelo conceptual, y en los diagramas de interacción, que muestran cómo los objetos intercambian mensajes para realizar las operaciones del sistema y lograr las condiciones posteriores de las restricciones.
    • Diseño tecnológico, que incluye todos los aspectos del problema inherentes a la tecnología utilizada: interfaz, almacenamiento de datos, seguridad, comunicación, tolerancia a fallos, etc. Las actividades relacionadas con el diseño tecnológico se abordan más adelante:
    • Diseño de la capa de interfaz (Capítulo 12), que consiste en diseñar la interfaz de usuario y preferiblemente mantenerla desacoplada de la capa del dominio.
    • Diseño de la capa de persistencia (Capítulo 13), que consiste en la definición de un mecanismo de persistencia para permitir la carga y almacenamiento de datos, que puede realizarse automáticamente, evitando que el diseñador se preocupe (sobre)  por esos aspectos.
El diseño lógico también se conoce como diseño de la capa de dominio. La capa de dominio corresponde al conjunto de clases que realizan todas las transformaciones y consultas de datos. Otros niveles implementan aspectos tecnológicos del sistema: persistencia, interfaz, comunicación, seguridad, etc. Suelen derivarse y depender de la capa de dominio y su utilidad es conectar la lógica pura del dominio a los aspectos físicos del ordenador (redes de comunicación, interfaces humanas, dispositivos de almacenamiento, etc.).
El diseño de la capa de dominio consiste básicamente en dos actividades que se pueden realizar de forma iterativa:
    • Modelado dinámico, que consiste en construir modelos de ejecución para las restricciones de operación del sistema. En los sistemas orientados a objetos, estos modelos suelen representarse mediante diagramas de interacción, como los diagramas de comunicación y secuencia, o incluso como algoritmos de texto puro.
    • Construcción de la DCD, que consiste básicamente en agregar al modelo conceptual alguna información que no era posible o deseable obtener antes, como por ejemplo, la dirección de navegación de la asociación, y los métodos a implementar en cada clase. Estos aspectos pueden ser efectivamente incluidos en el diseño del software si se realiza un modelado dinámico. Además, la estructura de las clases de diseño puede ser un poco diferente del modelo conceptual, ya que pueden ser necesarias nuevas clases o una organización de clases diferente para realizar algunas funciones que se necesitarán en este punto.
El diseño lógico puede ser realizado sistemáticamente si el equipo está en posesión de dos artefactos:
    • El diagrama de la clase de diseño en evolución.
    • El modelo funcional representado por las restricciones de operación del sistema.
Las actividades de diseño lógico consisten en construir diagramas de interacción para las operaciones del sistema que se encuentran en los diagramas de secuencia del sistema (especialmente los comandos del sistema, como se explica más adelante), teniendo en cuenta la DCD y la restricción de operación del sistema respectivo.
El modelado dinámico, como se mencionó anteriormente, puede hacer uso de diagramas de comunicación o de secuencia, o incluso de algoritmos. Cada una de estas formas tiene ventajas y desventajas:
    • Los algoritmos, para los programadores, son más fáciles de escribir, pero puede ser difícil realizar claramente las conexiones entre objetos en texto simple. Por lo tanto, la elección de algoritmos para utilizar el modelado dinámico orientado a objetos puede aumentar el riesgo de un acoplamiento alto entre clases, generando un mal diseño.
    • Los diagramas de comunicación son mejores que los algoritmos para fines de visualización y distribución de responsabilidades, y son mejores que los diagramas de secuencia para proporcionar una visión explícita de las líneas de visibilidad entre objetos. Sin embargo, estos diagramas pueden ser difíciles de organizar y en el caso de colaboraciones complejas pueden llegar a ser más difíciles de leer que los diagramas de secuencia.
    • Los diagramas de secuencia suelen ser más fáciles de leer que los diagramas de comunicación, pero no muestran explícitamente las líneas de visibilidad entre objetos. Si el diseñador no está atento, se pueden incluir en el diagrama comunicaciones inválidas o imposibles.
Este capítulo utiliza diagramas de comunicación para el modelado dinámico con el fin de facilitar la visualización de las líneas de visibilidad entre objetos. En algunos casos, se muestran los diagramas de secuencia equivalentes para su comparación.
Los ejemplos de diagramas de clase en este capítulo asumen que es tiempo de diseño. Así, las asociaciones pueden ser dirigidas y las clases pueden tener métodos y atributos privados.
El capítulo discute inicialmente la responsabilidad de los objetos, que es un concepto clave para entender cómo distribuir los métodos entre los objetos. Saber qué objeto debe implementar qué responsabilidad permite que las clases de diseño sean altamente cohesivas.
Otro concepto clave que se presenta en detalle es el de visibilidad, que establece que la comunicación entre objetos debe ocurrir sólo cuando existen líneas de visibilidad. Si se minimiza la cantidad de esas líneas, se logra un acoplamiento bajo (Meyer, 1988) en el diseño.
Finalmente, el capítulo explica cómo transformar las restricciones en modelos dinámicos utilizando la distribución y visibilidad de la responsabilidad, así como otros patrones de diseño, para producir el mejor diseño posible.

            ​ 9.2 Distribución de responsabilidad en un objeto
La distribución de la responsabilidad entre los objetos tiene que ver con la siguiente pregunta: ¿Qué métodos deben aplicarse y en qué clases?
A muchos diseñadores les resulta difícil construir una solución elegante a ese problema cuando simplemente intentan añadir métodos a un diagrama de clase. El uso de diagramas de interacción y patrones de diseño puede, sin embargo, proporcionar una manera más eficiente y efectiva de descubrir el lugar más adecuado para implementar cada método.
La DCD se construye a partir del modelo conceptual, que proporciona el conjunto básico de clases, atributos y asociaciones que se necesitan. Luego, es necesario desarrollar diagramas de interacción para cada restricción de operación del sistema. Estos diagramas muestran objetos que intercambian mensajes para conseguir las condiciones posteriores de los respectivas restricciones. Hay técnicas que ayudan a construir esos diagramas de una manera elegante. El uso de diagramas es mejor que los algoritmos, especialmente para los diseñadores noveles, porque con los algoritmos, el diseñador puede caer en la tentación de concentrar todas las responsabilidades en una sola clase, mientras que los diagramas permiten una mejor visualización de la distribución de las responsabilidades entre los objetos. Más adelante en este capítulo se presenta un ejemplo de esa situación.
Cuando un equipo construye código orientado a objetos sin un método adecuado para el modelado dinámico (es decir, simplemente haciendo un diagrama de clase y agregándole métodos ad-hoc) existe el riesgo de que las responsabilidades estén mal distribuidas entre las clases, y el resultado final pueda ser tan desestructurado como el antiguo código de spaghetti. Por lo general, los sistemas orientados a objetos están bien organizados a nivel de clase, pero infelizmente el código escrito dentro de los métodos está a menudo mal diseñado.
Por lo tanto, para que un sistema sea elegante, las responsabilidades deben estar bien distribuidas. Si no se utiliza un método sistemático, las responsabilidades pueden concentrarse en la clase del controlador o en clases que representen a los actores del negocio, como el cliente o el empleado. Al final, las clases tales como Libro, Orden y Pago no tendrían ningún método relevante aparte de sus propios getters y setters de atributos.
Cuando una o dos clases hacen todo el trabajo, y otras son pasivas, no hay un código orientado a objetos digno de ese nombre, sino una estructura concentradora. Sería preferible hacer un buen diseño estructurado que un mal diseño orientado a objetos.
Por otro lado, los diseñadores, a veces, cometen el error de creer que un sistema orientado a objetos es una simulación del mundo real. Pero eso no suele ser cierto. Un modelo orientado a objetos representa la información sobre el mundo real, y no las cosas mismas. La diferencia es sutil: los métodos no corresponden a la acción del mundo real, sino al procesamiento interno de la información del sistema. Es por eso que conceptos como Libro que son pasivos en el mundo real pueden realizar comandos en sistemas orientados a objetos.
Por lo tanto, el diseño de software orientado a objetos debe entenderse como un método preciso, guiado por patrones aprendidos, y no simplemente como el acto de crear clases y asociarles métodos ad hoc.
Antes de explicar cómo distribuir las responsabilidades entre los objetos, se definirá una taxonomía de esas responsabilidades. Básicamente, hay dos grupos de alto nivel de responsabilidades:
    • La responsabilidad de saber, que corresponde a las consultas sobre objetos.
    • La responsabilidad de la actualización, que corresponde a los comandos realizados por los objetos.
Ambos grupos de alto nivel se dividen en tres subgrupos:
    • Cosas que el objeto conoce o actualiza dentro de sí mismo (sus atributos).
    • Cosas que el objeto conoce o actualiza en su vecindario (sus enlaces).
    • Otras cosas que el objeto conoce o actualiza que no están clasificadas en los dos grupos anteriores. Normalmente estas cosas corresponden a conocimientos derivados (atributos derivados y asociaciones, y otras consultas en general) y actividades coordinadas (métodos de delegación).
En el caso de las responsabilidades de saber, los tres subgrupos podrían caracterizarse de la siguiente manera:
    • Cosas que el objeto sabe sobre sí mismo: Esto equivale a poder acceder a los atributos de un objeto. Tales responsabilidades se incorporan a las clases mediante métodos de consulta básicos nombrados con el prefijo get seguido del nombre del atributo.1 Por ejemplo, si la clase Person tiene un atributo birthDate, entonces el método getBirthDate tiene la responsabilidad de conocer el valor de ese atributo.
    • Cosas que el objeto sabe sobre su vecindario: Esto equivale a poder acceder a objetos enlazados directamente. Esta responsabilidad se incorpora en los métodos que obtienen el conjunto de objetos vinculados a través de un determinado rol. Estos métodos suelen ir precedidos por get y seguidos por el nombre del rol (o el nombre de la clase en ausencia del nombre del rol). Por ejemplo, si Coche está asociado a Persona y el nombre del rol Persona es conductor, entonces el método getDriver devuelve el conjunto de personas que son conductores de un coche determinado.
    • Cosas derivadas que el objeto sabe: Esto es equivalente a la información que se compone o calcula a partir de otra información. Esta responsabilidad puede estar asociada a atributos derivados y asociaciones derivadas, en cuyo caso los métodos también están precedidos por get seguido del nombre del atributo derivado o asociación. Por ejemplo, si totalValue es el nombre de un atributo derivado de la clase Order, getTotalValue es un método que devuelve ese atributo derivado. El conocimiento derivado también incluye otras consultas sobre un objeto que no pueden representarse como atributos o asociaciones derivadas, como, por ejemplo, consultas con parámetros; en ese caso, los nombres pueden variar.
En el caso de las responsabilidades relacionadas con la actualización de la información, los tres subgrupos podrían caracterizarse como:
    • Cosas que el objeto hace sobre sí mismo: Esto corresponde al comando básico que actualiza un único atributo, al que se le asigna el prefijo set,2 seguido del nombre del atributo. Por ejemplo, si la clase Person tiene un peso de atributo, setWeight es un método que incorpora la responsabilidad de cambiar ese atributo.
    • Cosas que el objeto hace sobre su vecindario: Esto corresponde a los comandos básicos que añaden y eliminan enlaces entre objetos. Estos comandos se identifican respectivamente por los prefijos add y remove,3 seguidos del nombre de la función de asociación. Por ejemplo, si el Cliente de la clase tiene una asociación con Reservas, los métodos addReservation y removeReservation incorporan esa responsabilidad.
    • Cosas que el objeto coordina: Esto corresponde a comandos que realizan múltiples tareas, posiblemente en diferentes objetos. Estos comandos se conocen como métodos delegados y son cruciales para el diseño de la clase porque los métodos de los otros grupos son sólo comandos básicos con un comportamiento previamente conocido; pero los métodos delegados deben ser diseñados. Por ejemplo, si todos los libros de un pedido deben ser marcados como entregados, la coordinación de las actividades de marcaje debe ser realizada por la propia instancia de la Orden, ya que es el objeto con el acceso más inmediato a los objetos que participan en la operación.
La Tabla 9.1 resume los seis tipos de responsabilidades y los métodos típicamente asociados a cada tipo.

Tabla 9.1
Responsabilidades del objeto


Conocidas
Actualiza
Sobre sí mismo
Consulta sobre sus atributos:
-  getAttribute
Actualiza atributos:
-  setAttribute
Sobre sus vecinos
Consulta sobre su Rol en asociaciones:
-  getRole
Actualiza enlaces:
-  addRole
-  removeRole
-  replaceRole
Otras
Consultas sobre atributos derivados y roles, y consultas generales:
-  getAttribute
-  getRole
-  nombre variable ( en caso de consultas generales)
Métodos delegados:
-  nombre variable

No existe un nombre estándar para los métodos delegados y las consultas generales, que se denominan en función de la operación que realizan. Normalmente, estos nombres no deben incluir el nombre de la clase en la que se implementan. Por ejemplo, si Livir implementa un comando de sistema finishOrder, y ese comando delega esa responsabilidad a la clase Order, entonces el nombre del método implementado en la clase Order debe ser simplemente terminado, porque probablemente sería invocado como unOrder.finish().

            ​ 9.3 Visibilidad
Para que dos objetos puedan intercambiar mensajes para cumplir con sus responsabilidades, es necesario que exista algún tipo de visibilidad entre ellos. Hay cuatro formas básicas de visibilidad entre los objetos:
    • Por asociación: Si existe un vínculo entre dos objetos definidos por una asociación entre sus clases.
    • Por parámetro: Si un objeto, al ejecutar un método, recibe otro objeto como parámetro.
    • Declarado localmente: Si un objeto que está realizando un método recibe otro objeto como retorno de consulta.
    • Global: Si un objeto es visible por cualquier otro objeto.
Ninguna de las formas de visibilidad es simétrica. Es decir, si x tiene visibilidad a y eso no significa que y necesariamente tenga visibilidad a x. La visibilidad por asociación puede ser simétrica si la asociación es bidireccional, pero no siempre es así.

                ​ 9.3.1 Visibilidad por asociación
Hay visibilidad por asociación entre dos objetos sólo cuando hay una asociación entre sus respectivas clases. El tipo de visibilidad que se permite depende de la multiplicidad de roles y otras características, como que la asociación esté calificada, ordenada, etc.
Una función de asociación puede considerarse un conjunto de instancias, especialmente si su límite superior es superior a 1. Pero, en el caso de la multiplicidad 1 ó 0..1, es posible interpretar la función como un conjunto o como un objeto individual. OCL, en estos casos, considera el papel tanto como un objeto como una colección. En cuanto a la multiplicidad, entonces, se pueden identificar los siguientes tipos de visibilidad:
    • Si la multiplicidad es 1, entonces hay visibilidad directa a una instancia y al conjunto que contiene una instancia.
    • Cualquier otra multiplicidad sólo permite la visibilidad de un conjunto de instancias.4
La DCD no es la única especificación que determina la multiplicidad de una función. Se complementa con las condiciones previas de las restricciones, que pueden limitar aún más los límites de la multiplicidad, como se ve en las secciones siguientes.

                    ​ 9.3.1.1 Visibilidad de un solo objeto
La figura 9.1 muestra una clase de pago que tiene una asociación unidireccional con la orden con multiplicidad 1. En este caso, cualquier instancia de Pago tiene visibilidad directa a una instancia de Orden.5

Figura 9.1 El rol de la asociación con la multiplicidad 1.

De esta manera, cuando una instancia de pago se representa en un diagrama de interacción, como se muestra en el diagrama de comunicación de la Figura 9.2, puede enviar mensajes directamente a la instancia de la Orden que está vinculada a ella.

Figura 9.2 Diagrama de comunicación en el que un pago tiene visibilidad para un único pedido.

                    ​ 9.3.1.2 Visibilidad de múltiples objetos
Los valores de multiplicidad diferentes de 1, como *, 1..*, 0..1, o 5, proporcionan visibilidad a una colección6 de objetos, no sólo a una única instancia. De ahora en adelante, todos esos casos serán tratados como * multiplicidad, o asociación para muchos.
La figura 9.3 muestra la clase Orden con una asociación unidireccional con multiplicidad * a la clase Artículo.


Figura 9.3 Rol de asociación con multiplicidad *.

En este caso, una instancia de Orden puede enviar un mensaje a un conjunto de instancias de Item. Es posible enviar mensajes a la propia estructura del conjunto7, como se muestra en la figura 9.4. En el ejemplo, el mensaje verifica si el conjunto está vacío.

Figura 9.4 Diagrama de comunicación con un mensaje que se envía a una estructura de set.

Pero es posible enviar un mensaje de forma iterativa a cada elemento del conjunto, como se muestra en la Figura 9.5. En el ejemplo, el mensaje solicita el valor del subtotal de cada posición.

Figura 9.5 Diagrama de comunicación con un mensaje enviado a cada elemento del conjunto.

Así, los mensajes, en los diagramas de comunicación, pueden dirigirse a la estructura de la colección o a los elementos de la colección individualmente. Cuando se envía un mensaje a la estructura, el tipo de objeto que recibe el mensaje debe ser una colección, como Set<Item> en la Figura 9.4. El hecho de que el mensaje sea iterativo y se envíe a todos los elementos del conjunto está representado por el "*" que precede al mensaje. La condición[para todos] indica que todos los elementos del conjunto reciben el mensaje.
Se puede utilizar un filtro si el mensaje está destinado sólo a algunos elementos seleccionados. Por ejemplo, si el mensaje getSubtotal está destinado sólo a elementos con una cantidad superior a 1, podría escribirse como *[quantity>1]: anAmount:=getSubtotal().

                    ​ 9.3.1.3 Visibilidad por asociación con roles ordenados
Si la función de asociación se ordena con el uso de las restricciones {ordenadas} o {secuenciales}, se mantiene la visibilidad de la colección en su conjunto, pero además se permite la visibilidad recta de los elementos individuales indexados por su posición.
La Figura 9.6 presenta un diagrama de clase con una asociación unidireccional con una función ordenada.


Figura 9.6 Asociación ordenada.

En la figura 9.7 el mensaje se envía a cada uno de los elementos del conjunto ordenado, como en el caso de la figura 9.5.


Figura 9.7 Diagrama de comunicación con un mensaje que se envía a una estructura de conjunto ordenada.

La Parte (A) de la Figura 9.7 es la manera explícita de representar un mensaje iterativo enviado a los elementos de un conjunto o secuencia ordenada. La Parte (B) es una manera aceptable más corta de representar lo mismo. El formulario *[para todos]: utilizado para los lances también sería aceptable.
En la Figura 9.8 sólo el tercer elemento del conjunto ordenado recibe el mensaje, y la visibilidad no es para múltiples objetos como antes, sino para un solo objeto. Esto se indica en el índice utilizado para representar el nombre del objeto: órdenes[3]. El valor entre paréntesis puede ser una constante, como en el ejemplo, o una variable conocida por la instancia del Cliente, o incluso una expresión matemática que resulta en un entero.

Figura 9.8 Diagrama de comunicación con un mensaje que se envía a un elemento específico de un conjunto ordenado.

En la Figura 9.9 sólo el último elemento de la colección ordenada recibe el mensaje.


Figura 9.9 Diagrama de comunicación con un mensaje que se envía al último elemento de un conjunto ordenado.

                    ​ 9.3.1.4 Visibilidad por asociación con los clasificados
Si la asociación está calificada como mapa (sólo un elemento por cada valor del calificador), hay al menos dos formas de visibilidad directa:
    • Visibilidad del conjunto de elementos en su conjunto (como si se tratara de un conjunto regular).
    • Visibilidad de un solo elemento si el objeto tiene una clave para acceder al elemento en el rol de asociación.
La Figura 9.10 presenta un diagrama de clase con una asociación cualificada desde el Cliente hasta la Tarjeta de Crédito.


Figura 9.10 Diagrama de clase con una asociación cualificada que define un mapa.

La figura 9.11 muestra que en este caso, una instancia de Cliente tiene visibilidad sobre el conjunto de instancias de Tarjeta de Crédito que están vinculadas a ella.

Figura 9.11 Diagrama de comunicación con un mensaje que se envía a la estructura del conjunto mapeado.

La figura 9.12 muestra un mensaje que se envía a cada una de las tarjetas de crédito del conjunto asignado.

Figura 9.12 Diagrama de comunicación con un mensaje enviado a cada elemento del conjunto asignado.

Finalmente, la Figura 9.13 muestra que si la instancia de Cliente tiene un valor clave para el calificador (aNumber en el ejemplo), entonces tiene visibilidad directa al elemento del conjunto mapeado calificado por ese valor clave.

Figura 9.13 Diagrama de comunicación que muestra un objeto con visibilidad directa a un objeto calificado en un conjunto mapeado.
                                                                                                                                                                                     
Por otro lado, si la asociación cualificada representa una partición, como en la Figura 9.14, se asocia un conjunto de valores a cada cualificador.

Figura 9.14 Diagrama de clase con una asociación cualificada que define una partición.
En este caso, se puede acceder a todo el conjunto (todos los libros del ejemplo de la Figura 9.15).

Figura 9.15 Diagrama de comunicación con un mensaje que se envía a cada elemento del conjunto particionado.                       

Pero el uso del calificador permite el acceso a libros que pertenecen a un subconjunto dado (libros de suspense, en el ejemplo de la Figura 9.16).

Figura 9.16 Mensaje iterativo para cada elemento de una partición de un conjunto calificado. 

Ambos ejemplos en la Figura 9.15 y Figura 9.16 muestran mensajes que se envían a los elementos de set y no a la estructura de set.
                                            
                    ​ 9.3.1.5 Visibilidad de la asociación con la clase de asociación
Como se explica en la Sección 6.6.2, una instancia de clase de asociación se crea y elimina cuando se añaden y eliminan enlaces de las instancias de las clases participantes. Así, si la Persona tiene una asociación unidireccional a la Empresa y esa asociación tiene una clase de asociación Job, como se muestra en la Figura 9.17, cuando se añade un enlace entre las instancias de Persona y Empresa, se crea una instancia de Trabajo; y cada vez que se elimina un enlace de Persona a Empresa, se elimina la instancia de Trabajo correspondiente. Por lo tanto, una instancia de Persona tiene visibilidad para dos conjuntos8 con el mismo tamaño: uno con instancias de Compañía, y otro con instancias de Trabajo. Una instancia de trabajo tiene visibilidad sólo para una única instancia de la empresa.



Figura 9.17 Clase de asociación.

Si la asociación en la Figura 9.17 fuera bidireccional, entonces una instancia de la Compañía también tendría visibilidad para un conjunto de Personas y un conjunto de Trabajos. Además, cualquier instancia de Trabajo tendría visibilidad para una instancia de Persona y una instancia de Compañía.
La figura 9.18 representa la visibilidad que una instancia de Persona tiene sobre el conjunto de instancias de la Compañía. Esto corresponde a la visibilidad por defecto obtenida para la multiplicidad *.



Figura 9.18 Un mensaje que se envía a los elementos del conjunto vinculados por una asociación con una clase de asociación.

La Figura 9.19 representa la visibilidad que una instancia de Persona tiene sobre un conjunto de instancias de Trabajo, la clase de asociación.


Figura 9.19 Un mensaje que se envía a los elementos del conjunto de instancias de la clase de asociación.

La clase de asociación también funciona como un mapeo de una manera muy similar a la de la asociación calificada. El modelo de la Figura 9.17 es equivalente al mapeo de un trabajo para cada empresa para la que trabaja una persona. Así, si una instancia de Persona tiene visibilidad a una instancia específica de la Compañía, puede encontrar su trabajo en la compañía, como se ilustra en la Figura 9.20.


Figura 9.20 Un mensaje que se envía a un elemento específico de la clase de asociación.

También en la Figura 9.20, podemos ver que una Compañía debe ser una instancia de la Compañía y que la instancia de Persona debe tener algún tipo de visibilidad para poder usarla para acceder a la respectiva instancia de Trabajo.
Finalmente, la Figura 9.21 muestra la visibilidad que las instancias de la clase de asociación tienen sobre las instancias de las clases participantes: una visibilidad que es estrictamente una.



Figura 9.21 Visibilidad desde la instancia de la clase de asociación a una de las instancias de las clases participantes.

                    ​ 9.3.1.6 La influencia de las condiciones previas en la visibilidad por asociación
Cuando una condición previa en una restricción establece una multiplicidad que es más restrictiva que la permitida en el diagrama de clase, es la visibilidad establecida por la condición previa la que debe considerarse válida en el contexto de esa operación.
Por ejemplo, considere el diagrama de clase de la Figura 9.22, que define que una orden puede o no tener un pago vinculado a ella.


Figura 9.22 Asociación con rol opcional.

Considere ahora que una restricción de operación determinada tiene una condición previa que establece

pre:
anOrder.payment→notEmpty()

Entonces, en el contexto de esa operación, y para el caso específico de una orden, se debe considerar una visibilidad más restrictiva, como se muestra en la Figura 9.23.


Figura 9.23 Cómo debe considerarse la visibilidad original de Figura 9.22 para un caso específico si un contrato tiene una condición previa más restrictiva.


                ​ 9.3.2 Visibilidad por parámetro
La visibilidad por parámetro se obtiene cuando un objeto A, realizando un método, recibe un objeto B como parámetro. En ese caso, el objeto A puede comunicarse con B incluso si sus clases no están asociadas.
Considere el ejemplo de la Figura 9.24, donde la clase Book no tiene asociación con la clase Delivery. Por lo tanto, ninguna instancia de Book puede enviar un mensaje directamente a una instancia de Entrega o viceversa.


Figura 9.24 Diagrama de clase de referencia.

Considere una instancia de Pedido que esté vinculada a una instancia de Libro y a una instancia de Entrega como se muestra en la Figura 9.25.

Figura 9.25 Situación inicial donde la instancia de Entrega no tiene visibilidad directa de la instancia de Book.

Ahora, considere que la instancia de Orden envía un mensaje registerWeight a la instancia de Entrega, pasando una referencia a la instancia de Libro como argumento, como se muestra en la Figura 9.26. Luego, la instancia de Entrega adquiere visibilidad por parámetro a la instancia de Libro.


Figura 9.26 Situación inicial en la que la instancia de Entrega no tiene visibilidad directa de la instancia de Libro.

En el caso de la visibilidad por parámetro, se debe asumir que el objeto que envía el argumento originalmente tiene algún tipo de visibilidad al objeto que fue enviado.
Una buena práctica de diseño exige cuidado con la visibilidad por parámetros. Este no es el mismo tipo de acoplamiento que se obtiene con visibilidad por asociación. Con visibilidad por asociación, las clases participantes ya están acopladas por una asociación semántica, es decir, están vinculadas de todos modos porque el significado de una está ligado al significado de la otra (por ejemplo, una orden y sus elementos). Pero en el caso de la visibilidad por parámetro, cualquier objeto puede ser pasado como un parámetro a otro objeto, incluso si no tienen absolutamente ninguna relación entre ellos.
Cada vez que una clase declara métodos con parámetros pertenecientes a clases a las que no está asociada, puede crearse un nuevo acoplamiento (y posiblemente innecesario). Un acoplamiento alto significa un diseño deficiente. Por lo tanto, es conveniente evitarlo siempre que sea posible.
El mejor uso para la visibilidad por parámetro es recibir y reenviar objetos hasta que lleguen a las operaciones (básicas) del terminal. En la práctica, lo que sucede es que ciertos objetos pasan a otros objetos de una cadena hasta que llegan a un objeto que debe estar enlazado o desvinculado con ellos, como en el ejemplo siguiente.
Inicialmente, considere el diagrama de clases de la Figura 9.27, con las clases Livir (el controlador-fachada), Book, Customer y Reservation.


Figura 9.27 Diagrama de clase de referencia.

La Figura 9.28 presenta una colaboración en la que instancias de estas clases cooperan para realizar el comando del sistema reserveBook, que añade una reserva para un libro dado a un cliente dado. El comando de sistema, implementado en el controlador, es llamado por la capa de interfaz, que pasa como argumentos el ISBN del libro y el ID del cliente. El controlador, inicialmente, obtiene visibilidad de la instancia específica de Book (mensaje etiquetado "1") enviándose a sí mismo un mensaje de consulta sobre el libro de roles: el mensaje getBook(anIsbn). Entonces obtiene visibilidad a la instancia de Cliente (mensaje etiquetado "2") de forma similar. Las instancias devueltas por los mensajes se asignan a las variables locales aBook y aCustomer. Finalmente, el controlador delega en la instancia del Cliente la reserva del libro (mensaje etiquetado "3").


Figura 9.28 Creación de visibilidad por parámetro.

El mensaje "3", reserveBook(aBook), es enviado desde el controlador al cliente cuyo ID es aCustomerId. El responsable del tratamiento no debe ser responsable de la creación de la reserva, ya que no tiene ninguna relación con la reserva y, por lo tanto, delega la responsabilidad en un cliente. En este punto, el cliente adquiere visibilidad por parámetro a un libro.
En este punto, el cliente puede empezar a cumplir con sus responsabilidades. Crea una nueva instancia de Reserva y la vincula a sí misma y a un Libro. La figura 9.29 muestra el mensaje del constructor Create que se está enviando para crear una reserva con sus parámetros de inicialización: aBook y aCustomer. Este mensaje está etiquetado con 3.1 porque se llama dentro de la implementación del mensaje 3, que fue recibido por un cliente.


Figura 9.29 Un diagrama de comunicación donde se crea una nueva instancia de Reserva.

Como última observación sobre el ejemplo, intente averiguar qué pasaría si en lugar de pasar la instancia de Book al cliente, el controlador hubiera pasado su código ISBN como recibido de la interfaz. Cuando la instancia de Reserva va a añadir el libro a sus enlaces tendría que obtener la instancia, porque no puede simplemente añadir el código ISBN. ¿Cómo podría la instancia de Reserva buscar una instancia de Libro por su ISBN si no tiene acceso al conjunto de todos los libros? Tendría que enviar un mensaje al controlador, pidiendo el libro. Esto no es un diseño de buena calidad porque el flujo de mensajes en este caso regresa al controlador sin ninguna razón. En el ejemplo mostrado en la Figura 9.29, el controlador obtiene el libro tan pronto como recibe el mensaje original. No hay motivo para retrasarlo a fin de revertir el flujo de control más adelante.

                ​ 9.3.3 Visibilidad declarada localmente
Otra forma de visibilidad ocurre cuando un objeto envía una consulta a otro y recibe como retorno un tercer objeto, como se muestra en la Figura 9.31. La colaboración se basa en el diagrama de clase de la Figura 9.30.


Figura 9.30 Diagrama de clase de referencia.


Figura 9.31 Un ejemplo de la creación de visibilidad local.

En el ejemplo, una instancia de Cliente envía un mensaje getPayment a una instancia de Pedido. El cliente y el pedido están inicialmente vinculados, pero el cliente y el pago no lo están. Sin embargo, después de que se realiza el método getPayment y se devuelve una instancia de pago al cliente, éste adquiere visibilidad local del pago porque, en ese momento, el pago se asigna a una variable local (aPayment) del método que el cliente está ejecutando.
A partir de este momento, la instancia del Cliente adquiere visibilidad local del pago y puede comunicarse directamente con él.
Sin embargo, un patrón de diseño conocido como Don't talk to strangers (Larman, 2004)9 no recomienda que un objeto envíe mensajes a objetos que sólo son visibles localmente. De acuerdo con ese patrón, el cliente no debe enviar mensajes a aPayment. Como se ha visto en la Sección 9.6, siempre hay una opción de diseño que evita este tipo de comunicación. El problema aquí de nuevo es el acoplamiento alto: si el cliente adquiere visibilidad local a una instancia de Pago, adquiere un vínculo que no está semánticamente soportado por el modelo conceptual. Por otra parte, el precio a pagar por un acoplamiento bajo en este caso es a veces tener que implementar más métodos, como se verá más adelante.
Un uso aceptable para la visibilidad local ocurre cuando se invoca un comando básico que crea un objeto. Cuando se crea un objeto, la nueva instancia suele estar referenciada por una variable local. Esta visibilidad local puede transformarse inmediatamente en visibilidad por asociación, como se muestra en la figura 9.32.


Figura 9.32 Un ejemplo de nueva visibilidad local que se transforma en visibilidad por asociación.


                ​ 9.3.4 Visibilidad global
Hay visibilidad global para un objeto cuando es accesible por cualquier objeto en cualquier momento. El patrón de diseño singleton (Gamma, Helm, Johnson, & Vlissides, 1995) sugiere que una instancia puede ser globalmente visible si es la única instancia de una clase. Esto tiene sentido, porque si esa clase sólo tiene una instancia, no es necesario crear asociaciones de otros objetos con ella. Además, si esa clase tiene una sola instancia, no es necesario pasarla como argumento a una función porque la idea con los parámetros es que pueden variar y eso no ocurre con la clase Singleton. En el ejemplo, el primer mensaje es un comando básico, un constructor que produce la instancia de pago. En ese momento la instancia de Orden obtiene una nueva visibilidad local de la misma, a través de la variable local aPayment. El segundo mensaje enlaza esa nueva instancia con la orden, que adquiere visibilidad por asociación a la misma.
Tanto las visibilidades locales como las de parámetros son válidas sólo en el ámbito del método que las originó; al igual que los parámetros y las variables locales en los lenguajes de programación, sólo son válidos dentro de los métodos en los que han sido declarados, y desaparecen después de que los métodos salgan del ámbito de aplicación. Pero la visibilidad por asociación es permanente, persistiendo hasta que se elimina explícitamente mediante un comando básico que elimina un enlace. es que pueden variar, y eso no sucede si la clase tiene una sola instancia. La visibilidad global es la opción en este caso.
Ejemplos de singletons son las clases que representan servicios, como CurrencyConverter, TimeCounter, OrderNumberGenerator, etc. Debe haber una única instancia de clases de servicio a la que pueda acceder cualquier objeto en cualquier momento. En la figura 9.33 se muestra un ejemplo.


Figura 9.33 Visibilidad global

Si el patrón singleton es usado en exceso, puede convertirse en un anti-patrón. Los diseñadores no deben utilizar singletons para entidades del modelo conceptual; por ejemplo, si el sistema es de un solo usuario y puede existir un solo carro de la compra a la vez, no debe declararse un singleton porque es una entidad conceptual, no una clase de servicio. Una entidad conceptual que es única hoy en día puede admitir múltiples instancias en el futuro y declararla un singleton obstaculizaría la evolución de esa clase.
Además, un singleton, en principio, no debería tener referencias directas a entidades, porque eso reduce su potencial de reutilización y crea altos problemas de acoplamiento. Las clases de servicio no deben estar asociadas a clases de entidad; son visibles globalmente pero no permiten el acceso a otras instancias.

            ​ 9.4 Modelado dinámico basado en postcondiciones 
Vimos que las restricciones de comandos del sistema presentan un conjunto de condiciones posteriores que corresponden a ciertos comandos básicos para crear y eliminar instancias, añadir y eliminar enlaces y modificar valores de atributos. Estas restricciones sólo indican lo que se supone que debe suceder, pero no muestran cómo se intercambian los mensajes entre los objetos para lograr esos objetivos. Los diagramas de interacción UML pueden utilizarse para diseñar exactamente cómo pueden producirse estas colaboraciones. Se recomiendan los siguientes principios:
    • El tipo de visibilidad entre los objetos depende fundamentalmente de las características del rol, como la multiplicidad, el orden y la cualificación, que se definen en el diagrama de clase y que a veces se ven restringidas por condiciones previas (Sección 9.3).
    • Cada postcondición  end el contrato debe ser alcanzada en el diagrama de interacción por un mensaje que llame a un comando básico en el objeto que tiene la responsabilidad (Sección 9.2).
    • El flujo de control en un modelo dinámico comienza en la instancia del controlador-fachada que recibe un mensaje de la interfaz.
    • Cuando un objeto que se está ejecutando no tiene visibilidad sobre el objeto que debe realizar una operación básica, debe delegar la responsabilidad y la ejecución a otro objeto más cercano al que tiene la responsabilidad.
Santos (2007) presenta una sistematización de estos principios mediante la definición de un sistema de producción basado en la búsqueda automática capaz de generar diagramas de comunicación bien diseñados a partir de una amplia selección de restricciones.
Además de estos principios, los patrones de diseño deben aplicarse siempre que sea posible para ayudar al diseñador a construir métodos que sean efectivamente reutilizables y mantenibles.

                ​ 9.4.1 Creación de instancias
Cuando una restricción establece que se ha creado una instancia, otro objeto debe crearla enviando un mensaje básico de creación en el diagrama de comunicación correspondiente. El patrón de diseño del creador (Larman, 2004) establece que la elección debe ser preferiblemente:
    • Una instancia de una clase que tiene una agregación compuesta o compartida con la clase del objeto a crear.
    • Una instancia de una clase que tiene una o varias asociaciones con la clase del objeto a crear.
    • Un objeto que tiene los datos de inicialización para el objeto que se va a crear y que preferiblemente está asociado a él.
Cada regla se aplica sólo si no se aplica la anterior.
Para que sirva de referencia para los siguientes ejemplos, volvamos a las operaciones del caso de uso 01: Pedir Libros, presentado en el Capítulo 8. El modelo conceptual de referencia de la figura 8.1 se repite aquí como figura 9.34.


Figura 9.34 Diagrama de clase de referencia.

El primer comando del sistema del diagrama de secuencia del sistema del caso de uso 01 es add2Cart(aCartId:CartId, anIsbn:ISBN, aQuantity:Natural). Su restricción establece que si el libro no está ya en la cesta, se crea un nuevo artículo y se enlaza con el libro y la cesta. La cantidad de artículos se fija en el valor recibido como argumento y unitPrice en el precio del libro. De lo contrario, si el libro ya está en el pedido, la nueva cantidad se añade a la actual. La restricción de nuevo es el siguiente:
 
Context Livir::add2Cart(aCartId:CartId; anIsbn:ISBN; aQuantity:Natural)

def:aCart=cart[aCartId]
def:aBook=book[anIsbn]
def:anItem=aCart.item->select(book.isbn=anIsbn)
pre:
  aCart->notEmpty() and
  aBook->notEmpty()
post:
  if anItem->isEmpty() then
    newItem.isNewInstanceOf(Item) and
    aCart^addItem(newItem) and
    newItem^setQuantity(aQuantity) and
    newItem^addBook(aBook) and
    newItem^setUnitPrice(aBook.price)
  else
    anItem^setQuantity(anItem.quantity@pre + aQuantity)
  endif

Entre otras postcondiciones, se debe crear una instancia de Item si el libro aún no está en el carrito. La pregunta en este momento es: Si el flujo de control comienza en el controlador-fachada (Livir), ¿qué clase tiene que crear una instancia de Item? Las opciones son:
    • El propio controlador-fachada, que ya tiene el flujo de control (sería la elección de los diseñadores noveles).
    • Un ejemplo de la clase de Libro, porque tiene una asociación de uno a muchos a Item.
    • Una instancia de la clase Cart, porque es una agregación compuesta de Item.
Si se elige la opción de controlador, entonces se creará un acoplamiento que no existía antes entre ella y la clase Item. Esa sería una mala elección para el diseño.
Siguiendo el patrón de diseño del creador, la mejor opción sería Cart. La asociación entre el artículo y el libro es normal, mientras que la asociación entre el carro y el artículo es una agregación compuesta.
Para la primera versión del diagrama de comunicación, olvidemos por un momento el condicional if, y las condiciones posteriores que añaden enlaces y cambian los valores de los atributos. Concentrémonos en crear una instancia de Item.
La primera tarea del diseñador es obtener la instancia correcta de Cart dado su ID, y delegar en él la creación de la nueva instancia de Item. Esto se muestra en la Figura 9.35.


Figura 9.35 Diagrama de comunicación que muestra una instancia que se está creando.

Este diagrama implementa sólo una condición posterior: la creación de una instancia de Item. Inicialmente, el controlador debe determinar a qué carro se le da aCartId. Esto se realiza mediante el mensaje "1," getCart, que consulta el rol del carro del controlador Livir y almacena la instancia resultante en la variable aCart, que es una variable local para el comando de sistema add2Cart que se está modelando. Como la condición previa aCart->notEmpty() asegura que aCartId es válido, el modelo dinámico no necesita volver a comprobarlo.10
En la secuencia, el mensaje etiquetado "2," createItem, delega en el carrito la responsabilidad de crear un ítem, ya que el controlador no tiene ninguna asociación con el ítem. Si el controlador ha creado el nuevo ítem sin delegar, entonces Livir tendría que ser acoplado a la clase Item y se producirían problemas relacionados con el acoplamiento alto. Los parámetros de createItem se dejaron para ser añadidos más tarde, ya que todavía no son necesarios.
Finalmente, la instancia de Cart logra la condición posterior enviando un mensaje básico Create, etiquetado "2.1" en el diagrama, que produce una nueva instancia de Item. Esta instancia se almacena en una variable llamada newItem que es local al método createItem en la clase Cart.
Algunos diseñadores preferirían visualizar la colaboración entre los objetos mostrados en la Figura 9.35 como un diagrama de secuencia. La Figura 9.36 presenta un diagrama de secuencia que es equivalente al diagrama de comunicación de la Figura 9.35.



Figura 9.36 Diagrama de secuencia equivalente al diagrama de comunicación de la Figura 9.35.

Los diagramas de secuencia y comunicación utilizados para el modelado dinámico tienen aquí tres tipos de mensajes:
    • Un mensaje que invoca una operación del sistema, que es enviado por la interfaz y recibido por el controlador: add2Cart en el ejemplo.
    • Mensajes básicos que invocan operaciones que no necesitan ser refinadas más: getCart y Create en el ejemplo.
    • Delegar mensajes que se pueden utilizar cuando una instancia no tiene visibilidad sobre el objeto que debe realizar una responsabilidad: createItem en el ejemplo.
El primer y segundo tipo de mensajes siempre están presentes en esos diagramas. El mensaje que llama la operación del sistema es la raíz del árbol de mensajes del modelo dinámico. Los mensajes básicos son las hojas del árbol de mensajes, que corresponden a las consultas y actualizaciones finales del objeto.
Básicamente, hay un mensaje básico para cada postcondición individual. Estos mensajes son básicos en el sentido de que no necesitan ser refinados más: el flujo de control cesa cuando se alcanzan.
El tercer tipo de mensajes mencionado anteriormente, los mensajes de los delegados, son opcionales. Se pueden utilizar si el controlador, en lugar de enviar los mensajes básicos, tiene que delegar responsabilidades a otros objetos que tengan una visibilidad más inmediata de los objetos que deben ser consultados o actualizados.
Los mensajes delegados son las ramas del árbol de mensajes, y el flujo normalmente debe continuar después de ellos. El flujo de mensajes sólo termina cuando se alcanza un mensaje básico.


                ​ 9.4.2 Adición de enlaces
Se mencionó que cuando se crea una instancia, debe estar inmediatamente enlazada con otra instancia para que pueda ser accesible desde el controlador de la fachada. La restricción para add2Cart presentado en la Sección 9.4.1 establece que la instancia recientemente creada de Item debe estar vinculada a un libro y un pedido. La Figura 9.37 muestra una evolución del modelo dinámico con esas dos condiciones posteriores.


Figura 9.37 Evolución del modelo en la Figura 9.35 mostrando la adición de enlaces.

Ahora, cuando el carro está realizando el método createItem, crea el nuevo ítem (mensaje 3.1), añade un enlace entre él y el nuevo ítem (mensaje 3.2), y añade un enlace entre el nuevo ítem y el libro identificado por anIsbn (mensaje 3.3).
Este diseño podría ser aceptable porque reproduce casi literalmente lo especificado en la restricción. Sin embargo, este sería el caso sólo si el código generado por ese diseño no se modificara manualmente más tarde. Si el código de programación final se va a cambiar directamente en algún momento en el futuro, hay que tomar precauciones adicionales, y casi siempre es así.
El problema es que cuando un elemento es creado por un constructor básico sin parámetros, no es consistente con su definición hasta que se definen todos los atributos y enlaces obligatorios para él. En el caso de la figura 9.37, newItem es incoherente en el intervalo entre los mensajes 3.1 y 3.3. La solución a este problema es evitar que los constructores devuelvan objetos inconsistentes. En este caso, el constructor debe recibir todos los parámetros necesarios para generar una instancia consistente. Por lo tanto, el constructor de Create no es simplemente un mensaje básico en la concepción inicial del término, porque debe ser refinado aún más. La figura 9.38 muestra una nueva versión del modelo dinámico donde el constructor de Item produce una instancia con las asociaciones obligatorias necesarias.




Figura 9.38 Una variación del modelo de la Figura 9.37 donde el constructor de Item produce una instancia consistente.

Ahora, incluso si el código de programación final se cambia manualmente en el futuro, el diseñador sabe que cada vez que se utiliza una instancia de Item es consistente con su definición.

                ​ 9.4.3 Modificación del valor del atributo
Otro tipo de postcondición que debe ser considerada en el modelado dinámico es la modificación del valor del atributo, que puede ser lograda por el mensaje básico del setter que puede ser enviado por el objeto que posee el atributo o por uno de sus vecinos. Continuando con el ejemplo, el atributo de cantidad de la nueva instancia de Item debe rellenarse con el respectivo parámetro aQuantity de add2Cart, y el atributo unitPrice de Item debe inicializarse con el respectivo precio contable, tal y como se indica en la declaración de valor inicial para ese atributo en el diagrama. Estas condiciones posteriores se añaden al diagrama y se muestran en la figura 9.39.


Figura 9.39 Evolución del modelo en la Figura 9.38 mostrando los atributos que se están cambiando.

                ​ 9.4.4 Destrucción de instancias
La destrucción de una instancia se modela dinámicamente enviando un mensaje de destrucción básico a un objeto. Los mismos principios del patrón de diseño del creador se aplican aquí: el objeto que destruye una instancia debe tener una relación de agregación compartida o compuesta con el objeto que se supone que debe ser destruido, o una asociación de uno a muchos, o, al menos, estar asociado al objeto.
Se debe tener cuidado para evitar dejar los objetos con enlaces obligatorios inconsistentes después de que un objeto sea destruido. Si la restricción está bien formado, no quedarán objetos huérfanos, y los diagramas de comunicación sólo tienen que representar las condiciones posteriores que se mencionan en la restricción.
La Figura 9.40 presenta un modelo dinámico para el comando de borrado CRUD para una instancia de Book. La restricción asume que sólo los ISBNs de instancias que pueden ser borradas pueden ser pasados como argumento:11


Figura 9.40 Diagrama de comunicación con un objeto que se está destruyendo.
 
Context Livir::deleteBook(anIsbn:ISBN)

pre:
  book[anIsbn]->notEmpty() and
  book[anIsbn].item->isEmpty()
post:
  book[anIsbn]^destroy()

                ​ 9.4.5 Eliminación y sustitución de un enlace
Cuando una condición posterior establece que un enlace debe ser eliminado, algún objeto del modelo dinámico debe enviar un mensaje básico de eliminación a una de las instancias participantes. La figura 9.42 muestra un ejemplo de un modelo dinámico, basado en el diagrama de clases de la figura 9.41, en el que un eslabón se elimina y se sustituye por otro; es la versión dinámica de la siguiente restricción la que especifica cómo un coche cambia de propietario:


Figura 9.41 Diagrama de clase de referencia.

Figura 9.42 Diagrama de comunicación con un comando de sustitución de enlace.
 
Context Control::

changeOwner(newOwnerId:IdNumber,aLicense:CarLicense)
pre:
  person[newOwnerId]->notEmpty() and
  car[aLicense]->notEmpty
post:
  car[aLicense]^removeOwner() and
  car[aLicense]^addOwner(person[aNewOwnerId])

Como el rol propietario tiene la multiplicidad 1, el comando que elimina el enlace no requiere la especificación del parámetro.
Además, como el rol tiene multiplicidad 1, se podría crear un nuevo mensaje básico para reemplazar la asociación en lugar de la secuencia remove/add. Ese mensaje podría llamarse setOwner(nuevoPropietario:Persona) o replaceOwner(nuevoPropietario:Persona), y sería seguro para el hilo. La secuencia remove/add puede ser peligrosa si en el corto tiempo entre esos comandos algún otro proceso (thread) realiza una consulta sobre el objeto que se encuentra en un estado temporalmente inconsistente. Si en su lugar se utiliza un único comando, como reemplazar, y se asegura que mientras se realiza el objeto se bloquea incluso para su lectura, entonces no se producirá la situación peligrosa descrita anteriormente.

                ​ 9.4.6 Postcondiciones condicionales
Como se ha explicado anteriormente, a veces sólo se debe obtener una condición posterior si las condiciones dadas son válidas. En estos casos, es posible utilizar mensajes condicionados en diagramas de interacción que son similares a las condiciones de protección utilizadas en los diagramas de máquina de estado y de actividad.
Reanudando el ejemplo de add2Cart, la expresión condicional verifica si el carro ya tiene un artículo con el libro. Esa expresión no califica como un atributo derivado porque está parametrizada (es booleana, pero su valor depende del libro), y por lo tanto puede ser definida como una consulta normal en la clase Cart:
 
Context Cart::includeBook(aBook:Book):Boolean
body:
  item.book->exists(aBook)

La Figura 9.43 muestra la evolución del modelo de la Figura 9.39, ahora probando si un libro ya pertenece al carro o no. Note que el mensaje 3 fue renombrado como insertItem, porque ya no está creando un nuevo ítem: puede ser creado o incrementado.


Figura 9.43 Un borrador completo de un modelo dinámico para el contrato add2Cart.

Si el condicional es simplemente un "implies", entonces un mensaje condicional sería suficiente en el diagrama. Pero si el condicional implica una estructura del tipo if-then-else-endif, como en la Figura 9.43, se deben usar dos mensajes condicionales mutuamente excluyentes. En la Figura 9.43, el mensaje 3.1 se ejecuta sólo si includeBook(aBook) es verdadero, y el mensaje 3.2 se ejecuta sólo si esa condición es falsa.
Observe que los mensajes 3.1.1 a 3.1.5 están subordinados a 3.1 y se ejecutan sólo si se ejecuta 3.1. Del mismo modo, los mensajes 3.2.1 y 3.2.2 están subordinados a 3.2 y se ejecutan sólo si se ejecuta 3.2.
Mensaje 3.2.1, seleccioneItemFor, es otra consulta que es útil para la clase Cart. Se puede definir como
 
Context Cart::selectItemFor(aBook:Book):Item
body:
  item->select(book=aBook)

El mensaje 3.2.2 también es importante: si sólo se utilizaran mensajes básicos (tal como se definieron anteriormente), en lugar del mensaje 3.2.2, se utilizaría una secuencia de currentQuantity:=getQuantity() y setQuantity(currentQuantity+aQuantity). Sin embargo, esa construcción no es procesablemente segura. A menos que la concurrencia esté perfectamente controlada, esa secuencia de mensajes podría dejar la cantidad en un estado inconsistente si se actualiza entre esos dos mensajes mediante otro proceso. Por lo tanto, normalmente, en lugar de realizar una secuencia de get y set para incrementar los atributos numéricos, es preferible definir un mensaje básico de incremento que simplemente añada la cantidad pasada como parámetro al atributo numérico respectivo.
Hasta este punto, el modelado dinámico produjo dos nuevas consultas para la clase Cart: includeBook y selectItemFor. También produjo dos métodos de delegado para la clase Cart: insertItem e incrementItem. Para la clase Item, se definió un constructor, y como la cantidad de artículos debe ser incrementada, también se definió un nuevo mensaje básico: increaseQuantity. Los otros mensajes en el diagrama como getCart, setQuantity, etc., son todos mensajes básicos.
Sin embargo, ahora hay que abordar otra preocupación: ¿Se supone que los elementos, después de su creación, deben cambiar? Esta pregunta está relacionada con el patrón de diseño de inmutabilidad que establece que un objeto que no debe cambiar no debe implementar métodos de actualización pública. Específicamente, en el caso de la clase Item, que tiene una instancia creada en la Figura 9.43, debemos considerar si su libro, carro, precio o cantidad puede ser cambiado más tarde. Eso depende, por supuesto, de otros modelos dinámicos que serán construidos para otras operaciones del sistema, pero podemos asumir ahora que la cantidad y el precio unitario pueden cambiar mientras que el libro y el carrito vinculados son inmutables. Por lo tanto, el ítem no debe dejar addBook y addCart como métodos públicos. Los métodos privados pueden declararse en los diagramas de clase UML añadiendo un signo menos ("-") antes del nombre del método. Se muestran en el diagrama de la figura 9.50. Los métodos privados existen pero sólo pueden ser llamados por la instancia que los posee; para otros objetos no son accesibles.

                ​ 9.4.7 Excepciones
Los condicionales también pueden ser usados para modelar excepciones. Considere de nuevo la restricción para borrar un libro, pero esta vez, en lugar de asegurar que el libro puede ser borrado por una  precondición, se hace una excepción si el libro está vinculado a por lo menos un ítem:
 
Context Livir::deleteBook(anIsbn:ISBN)
pre:
  book[anIsbn]->notEmpty() and
post:
  book[anIsbn]^destroy()
exception:
  book[anIsbn].item->notEmpty() implies
  Exception.throw(‘Cannot delete a book that was sold’)12

Las excepciones suelen ser las primeras condiciones que se prueban en el modelo dinámico, porque si ocurre una de ellas, no se deben obtener todas las demás condiciones posteriores. Por lo tanto, un mensaje condicional se usaría para probar la condición de excepción antes que cualquier otra cosa.
El diagrama de la Figura 9.44 muestra cómo probar y plantear una excepción si el libro tiene elementos.


Figura 9.44 Un modelo dinámico para un contrato con una excepción

El modelo de la Figura 9.44 asume que el mensaje de lanzamiento es terminal, es decir, que la ejecución de la operación del sistema es interrumpida por éste. Esto significa que si la condición de excepción es verdadera, el mensaje 3 (el destructor real) no se ejecuta.

                ​ 9.4.8 Postcondiciones sobre las colecciones
Cuando los comandos del sistema tienen restricciones con postcondiciones que especifican actualizaciones sobre colecciones de objetos, la estructura de iteración puede utilizarse en el diagrama de comunicación para indicar que un mensaje se envía de forma iterativa a todos los elementos de la colección. Por ejemplo, el siguiente comando del sistema aumenta el precio de cada libro en un porcentaje:

Context Livir::raisePrices(aPercentage:Percentage)
post:
  book->forAll(aBook|
    aBook^setPrice(aBook.price@pre*(1+aPercentage))
  )

El diagrama de la Figura 9.45 es un modelo dinámico para esa restricción.

Figura 9.45 Modelo dinámico para un contrato con una condición posterior sobre una colección de objetos.

Una vez más, la elección de definir un nuevo mensaje básico para elevar el precio en lugar de una secuencia de getPrice y setPrice se debe a que es seguro para los hilos de proceso. El mensaje básico raisePrice cambia el valor del atributo price multiplicándolo por 1 más el parámetro porcentaje.
Otra situación común ocurre cuando la iteración no debe ocurrir sobre cada objeto de la colección, sino sólo sobre aquellos que satisfacen una condición dada. El siguiente comando aumenta en un porcentaje los precios de los libros con más de una página que aPageCount:

Context Livir::raiseThickBooks(aPercentage:Percentage; aPageCount:Natural)
post:
  book->select(pageCount>aPageCount)->forAll(aBook|
    aBook^setPrice(aBook.price@pre*(1+aPercentage))
  )

El diagrama de comunicación para esa restricción se muestra en la figura 9.46.


Figura 9.46 Diagrama de comunicación con iteración y selección.


            ​ 9.5 Consultas del sistema
Las restricciones de consulta del sistema suelen definir únicamente combinaciones de datos que se obtienen de los objetos. Es posible, aunque no siempre útil, desarrollar diagramas de comunicación o secuencia para tales restricciones, como, por ejemplo, el diagrama de comunicación de la Figura 9.47 que se construyó para la restricción de la consulta del sistema listBooks a continuación:


Figura 9.47 Diagrama de colaboración para una consulta del sistema.
 
Context Livir::listBooks():Set

body:
book->collect(aBook|
Tuple {
isbn=aBook.isbn,
title=aBook.title,
authorsName=aBook.authorsName,
price=aBook.price,
pageCount=aBook.pageCount,
publisherName=aBook.publisher.name,
coverImage=aBook.coverImage,
quantityInStock=aBook.quantityInStock
}
)

El aspecto más difícil relacionado con estos diagramas cuando se utilizan para modelar consultas del sistema es que no facilitan la representación de la composición de los datos. Por ejemplo, en la Figura 9.47 el controlador envía ocho mensajes a cada instancia de Book; cada mensaje produce una respuesta diferente. ¿Qué hace el controlador con todos esos valores? Sabemos, por la restricción de la consulta que forma la tupla con los ocho valores y agrupa las tuplas en un conjunto que es el dato de retorno final de la consulta. Pero representar eso en el diagrama sólo repetiría lo que ya se conoce en la restricción. Por lo tanto, la utilidad de estos diagramas en el caso de consultas es limitada.
Sin embargo, hay algunas cuestiones importantes sobre el modelado de consultas. En primer lugar, se pueden identificar tres tipos de mensajes de consulta:
    • La consulta del sistema, que se implementa en el controlador y es llamada directamente por la interfaz. Como los objetos de dominio están encapsulados en la capa de dominio y la interfaz se ocupa de los campos y botones, las consultas del sistema deben recibir datos alfanuméricos como parámetros y también devolver datos alfanuméricos.
    • Consultas básicas, que consultan atributos reales y enlaces correspondientes a las consultas básicas de get.
    • Las consultas intermedias, que corresponden a los atributos y asociaciones derivadas. Los atributos derivados devuelven datos alfanuméricos y las asociaciones derivadas devuelven objetos o estructuras de datos que contienen objetos. Otro tipo de consulta intermediaria es la consulta parametrizada, que no puede ser definida como un atributo derivado o asociación, como includeBook en la Figura 9.43.
En la Figura 9.47, la única consulta intermedia es getPublisherName, enviada por el controlador al libro. El libro, durante su turno, envía la consulta básica getName a su editor. Por lo tanto, publisherName puede ser considerado un atributo derivado de Book.
En cuanto a la pregunta "¿Debe la consulta intermediaria devolver el nombre del editor o el propio editor?
    • Si se necesita un solo atributo de un objeto, evite devolverlo, ya que puede generar un riesgo de no conformidad con el patrón "No hablar con extraños". Si se necesita un único valor alfanumérico, entonces es mejor definirlo como un atributo derivado como publisherName en la clase Book.
    • Cuando un conjunto de atributos o valores debe obtenerse a partir de uno o más objetos, y la intención es operar sobre ellos, por ejemplo, realizando una suma, o encontrando el valor más alto o la media, es preferible realizar la operación sobre la clase que tenga el acceso más inmediato a los valores. En otras palabras, la operación debería realizarse lo antes posible y el resultado ya procesado debería devolverse como un atributo derivado. Por ejemplo, totalValue, que es un atributo derivado de Cart, debe ser calculado por el propio cartucho, no por el cliente o el controlador. Sería un mal diseño si el carro devolviera los artículos al controlador para que éste realice la suma sobre los subtotales.
    • Cuando las colecciones de valores con una estructura compleja deben ser devueltas y no pueden ser transformadas en un único valor alfanumérico, es preferible devolver esa información como una colección de objetos, definiéndola como una asociación derivada, ya que de esta forma, los métodos que las clases ya tienen para realizar cálculos y operaciones sobre los datos permanecen disponibles. Sin embargo, esta opción puede posiblemente crear más acoplamiento, y debe utilizarse sólo si las otras opciones no son realmente aplicables.

            ​ 9.6 Delegación y acoplamiento bajo
A este punto, hemos visto algunas técnicas para construir diagramas de comunicación. Pero en la mayoría de las situaciones hay más de una opción de diseño y más de una forma de enviar un mensaje.
Como se discutió anteriormente, a veces el objeto que tiene control no tiene visibilidad sobre el objeto que puede realizar la responsabilidad. En este caso, se pueden identificar dos enfoques de diseño opuestos:
    • El objeto que tiene control trata de obtener una referencia al objeto que puede realizar la responsabilidad, y comunicarse directamente con él.
    • El objeto delega el mensaje a otro objeto más cercano al objeto que puede realizar la responsabilidad.
    • Para entender la diferencia entre estos dos enfoques, imagina que Manuel es el jefe de Pedro. El jefe quiere pedir un buffet para la fiesta de la oficina, pero no conoce ninguna empresa de catering. El jefe sabe que Pedro tiene contacto con algunas empresas de catering, entonces, tiene dos enfoques posibles:
    • El jefe le pide a Pedro los números de teléfono de las compañías y hace los arreglos por sí mismo. Lo único que hace Pedro es pasarle sus contactos al jefe.
    • El jefe le envía a Pedro los parámetros de la fiesta: cuánta gente, qué tipo de comida, cuánto gastar, etc., y le pide a Pedro que haga los arreglos. La fiesta ocurre, y el jefe nunca fue informado sobre el contacto del catering: delegó en Pedro.
Aunque en la vida real puede ser interesante hacer contacto con muchas personas y empresas, este no es el caso en los sistemas orientados a objetos. Cuando los objetos están altamente acoplados, el sistema es más complejo de lo que realmente necesita ser. Por lo tanto, es necesario evitar crear conexiones entre objetos que no estaban conectados en primer lugar.
El primer enfoque discutido anteriormente se llama concentración. Con él el objeto que tiene control de ejecución consigue obtener referencias a todos los objetos necesarios y realiza la propia operación. El segundo enfoque se llama delegación, y consiste en hacer que los objetos deleguen responsabilidades cuando no pueden cumplirlas. El segundo enfoque suele ser preferible, ya que ofrece más posibilidades de reutilización de clases y métodos, ya que las consultas intermedias o los métodos delegados que este enfoque crea suelen ser reutilizables.
A continuación se muestra un ejemplo concreto de ello. Considere una consulta del sistema getCartTotal definida de la siguiente manera:
 
Livir::getCartTotal(aCartId:CartId):Money
  body:
    cart[aCartId].item->sum(quantity*unitPrice)

La restricción de consulta del sistema anterior tiene como objetivo obtener el valor total de un carro determinado (la definición del contrato no utiliza intencionadamente los atributos derivados definidos en la Figura 9.34, suponiendo que aún no estén definidos). Este valor debe calcularse a partir del valor y la cantidad de cada una de las posiciones del pedido.
Con el enfoque de concentración, todo el proceso se implementaría en la clase Livir. Esta clase obtendría todos los datos necesarios para realizar el cálculo y devolver el resultado a la interfaz. El diagrama de comunicación de concentración tiene todos los mensajes que son enviados por Livir. No hay delegación, ya que ningún objeto envía mensajes aparte de la instancia de Livir. El pseudocódigo para esa consulta del sistema podría describirse de la siguiente manera:
 
CLASS
 Livir

ASSOCIATION VAR carts:MAP[CartId->Cart]
…
METHOD getCartTotal():Money
LOCAL VAR aCart:Cart
LOCAL VAR cartsItems:SET<Item>
LOCAL VAR total:Money
aCart:=carts.at(aCartId)
cartsItems:=aCart.getItem()
total:=0
FOR EACH item IN cartsItems DO
total:=total+(item.getValue()*item.getQuantity())
END FOR
RETURN total
END METHOD
 
END CLASS

Podemos tomar lo siguiente de este código:
    • Resuelve el problema.
    • No produce ningún elemento de software reutilizable aparte de la propia consulta que se implementa en la clase Livir.
    • Aumenta el acoplamiento entre clases, porque Livir adquiere visibilidad de Item, lo que no era el caso en el diagrama de clases de la Figura 9.34.
Al utilizar el enfoque de delegación, la consulta también se puede implementar correctamente, pero al mismo tiempo, se crean nuevas estructuras reutilizables con más cohesión y menos acoplamiento.
En primer lugar, la clase Livir debe ser impedida de tener acceso a cualquier instancia de Item, ya que no hay conexiones entre esas clases en el diagrama de clase. Para cumplir con las responsabilidades requeridas, Livir debe delegar el cálculo al carrito. Como el valor de retorno es Dinero (un alfanumérico específico), crear esta consulta intermedia para la clase Cart equivale a definir un atributo derivado para ella con la siguiente especificación OCL:
 
Context Cart::total:Money
  derive:
    item→sum(subtotal)

Además de crear un atributo derivado en el carro, también se debe crear un atributo derivado en la clase Artículo, para devolver el subtotal:
 
Context Item::subtotal:Money
  derive:
    unitPrice*quantity

Así, con estos dos atributos derivados, el pseudocódigo puede ser escrito con responsabiludades derivadas entre las clases:
 
CLASS
 Livir

ASSOCIATION VAR carts:MAP[CartId->Cart]
…
METHOD getCartTotal(aCartId:CartId):Money
RETURN carts.at(aCartId).getTotal()
END METHOD
 
END CLASS

 
CLASS
 Cart

ASSOCIATION VAR items:SET<Item>
…
METHOD getTotal ():Money
LOCAL VAR total:Money
total:=0
FOR EACH item IN items DO
total:=total+item.getSubtotal()
END FOR
RETURN total
END METHOD
 
END CLASS

 
CLASS
 Item

ATTRIBUTE VAR quantity:Natural
ATTRIBUTE VAR unitPrice:Money
…
METHOD getSubtotal():Money
RETURN quantity*unitPrice
END METHOD
 
END CLASS

Con este enfoque, la mayor parte del cálculo se realiza en la clase que efectivamente tiene el acceso más inmediato a la información necesaria, que es Cart. Por lo tanto, el procedimiento de cálculo aquí es más reutilizable que el producido por el enfoque de concentración, porque ahora está dentro de la clase Cart. Si la clase Cart es reutilizada, puede calcular su propio total sin depender de una clase que no sea un componente de ella (Livir). Lo mismo ocurre con Item, que ahora sabe cómo calcular su propio subtotal.
En el caso de los comandos del sistema, el principio de bajo acoplamiento también se obtiene cuando el diseñador decide delegar en lugar de devolver un objeto. Considere nuevamente el diagrama de clase de la Figura 9.34, pero suponga que el rol de Carrito a Artículo está marcado con {ordenado}. El diagrama de comunicación de la Figura 9.48 muestra el comando del sistema deleteLastItem, usando el enfoque de concentración. La figura 9.49 muestra el mismo comando con el enfoque de delegación, evitando acoplamientos innecesarios entre clases.


Figura 9.48 Estilo de diseño de concentración.


Figura 9.49 Estilo de diseño de la delegación.

El precio por utilizar la delegación suele ser tener más métodos declarados en las clases intermedias. Sin embargo, generalmente se producen métodos reutilizables para contrarrestar este problema. El precio de usar el enfoque de concentración es tener un diseño donde las responsabilidades se concentran en el controlador de la fachada en lugar de ser distribuidas entre los objetos; esto produce un modelo que es difícil de evolucionar y mantener a largo plazo.

            ​ 9.7 Diseño del Diagramas de clases
Uno de los objetivos del diseño lógico es construir y refinar el diagrama de clase de diseño (DCD), que se crea a partir del modelo conceptual y de la información obtenida durante el modelado dinámico (cuando se construyen los diagramas de interacción para las restricciones).
La primera versión de la DCD es una copia exacta del modelo conceptual, que será modificado posteriormente. Las modificaciones básicas que se realizan en el DCD durante el diseño de la capa de dominio son las siguientes:
    • Se añaden métodos. Durante el análisis, sólo se descubrieron y añadieron a la clase de controlador-fachada comandos y consultas del sistema. Durante el diseño, se añaden los métodos de delegado y los métodos básicos pertenecientes a otras clases.
    • Las asociaciones están dirigidas. Durante el análisis, las asociaciones fueron no direccionales. Durante el diseño, su dirección está determinada por la dirección de los mensajes que fluyen entre los objetos en los diagramas de interacción.
    • Los atributos y asociaciones pueden ser detallados. No es obligatorio presentar detalles sobre los atributos y asociaciones durante el análisis. Estos detalles pueden añadirse durante el diseño. Además, en el análisis sólo se utilizan tipos de datos abstractos para especificar las funciones de asociación, y pueden ser reemplazados por tipos de datos concretos durante el diseño (por ejemplo, reemplazando la secuencia por una lista de matrices o una lista de enlaces).
    • La estructura de las clases y asociaciones puede cambiar. Puede ser necesario crear nuevas clases para implementar ciertas estructuras de diseño, como estrategias y servicios, por ejemplo. Por lo tanto, es posible que la estructura de clases de la DCD no corresponda exactamente a la estructura del modelo conceptual, en algunos casos.
    • Posible creación de atributos protegidos y privados. En el modelo conceptual todos los atributos son públicos, porque representan información estática y no comportamiento. Sin embargo, cuando se representan los aspectos dinámicos de los objetos, puede ser necesario trabajar con atributos privados para encapsular estados internos que determinan el comportamiento de algunos objetos. Estos atributos a veces no son directamente accesibles a través de un getter o setter, pero su influencia en algunos métodos se siente.
Durante la construcción de un diagrama de comunicación, cada vez que un objeto recibe un mensaje delegado, su clase debe implementar el método correspondiente.
En la Figura 9.43, el diagrama de comunicación muestra que un número de mensajes deben ser implementados como métodos en algunas clases:
    • Livir debe implementar:
        ◦ add2Cart(aCartId:CartId, anIsbn:ISBN, aQuantity:Natural) - el comando system.
        ◦ getCart(aCartId:CartId):Cart - consulta básica.
        ◦ getBook(anIsbn):Libro - consulta básica.
    • El carro debe implementarse:
        ◦ insertItem(aBook:Book, aQuantity:Natural) - comando de delegado.
        ◦ includeBook(aBook:Book):Booleano - consulta o predicado.
        ◦ incrementItem(aBook:Book, aQuantity:Natural) - comando delegate.
        ◦ selectItemFor(aBook:Book):Elemento - consulta.
    • El ítem debe implementarse:
        ◦ Create(aBook:Book, aCart:Cart, aQuantity:Natural) - constructor.
        ◦ addBook(aBook:Book) - comando básico privado.
        ◦ addCart(aCart:Cart) - comando básico privado.
        ◦ setQuantity(aQuantity:Natural) - comando básico.
        ◦ increaseQuantity(aQuantity:Natural) - comando básico.
        ◦ setUnitPrice(aValue:Money) - comando básico.
    • El libro debe ser implementado:
        ◦ getPrice():Dinero - consulta básica.

La DCD también puede incluir información sobre la dirección de las asociaciones si el diseñador decide no implementar cada asociación como bidireccional. Este es generalmente el caso porque las asociaciones unidireccionales tienden a ser más simples de implementar y más eficientes en comparación con las asociaciones bidireccionales.
Decidir si una asociación es unidireccional o bidireccional depende del flujo de mensajes en los diagramas de interacción. Ninguna asociación debe ser, en principio, navegable en la dirección del controlador: el controlador ve las clases, pero no las ve. Otras asociaciones pueden ser unidireccionales si los mensajes sólo fluyen en una dirección, y bidireccionales si los mensajes fluyen en direcciones diferentes, incluso si esto ocurre en diagramas diferentes. La Figura 9.50 presenta una evolución del diagrama de la Figura 9.34 donde se incluyen los métodos y direcciones de asociación descubiertos en el modelo dinámico de la Figura 9.39.


Figura 9.50 Diagrama de clase de diseño con métodos y dirección de asociación.

No todas las asociaciones de la Figura 9.50 están dirigidas porque el diagrama de la Figura 9.39 muestra los mensajes que se envían desde el controlador al carrito, del carrito al artículo y del artículo al libro. Las asociaciones que no fueron seguidas por mensajes en el diagrama de comunicación se dejan sin definir hasta que otro diagrama decida finalmente su dirección.
Si otros diagramas de colaboración desarrollados para diferentes operaciones del sistema requieren que los mensajes naveguen en la dirección opuesta a los que ya fueron descubiertos, entonces las asociaciones respectivas deben ser bidireccionales.
Como la dirección de las asociaciones depende de la dirección de los mensajes enviados en los modelos dinámicos, no tendría sentido intentar definir esa dirección durante el modelado conceptual preliminar (Capítulo 3). En ese momento, la información disponible es insuficiente para tomar esas decisiones de diseño. Lo mismo es válido para decidir qué métodos debe implementar una clase.
Se supone por defecto que las asociaciones unidireccionales no tienen restricciones sobre su origen. Sin embargo, no siempre es así. Es cierto, por ejemplo, para la asociación de item a libro, que no tiene ninguna restricción de multiplicidad en su origen. Pero la asociación de Carro a Artículo está restringida en el origen, porque exige que un artículo esté vinculado a un solo carro. Si la asociación se implementa simplemente como una variable en la clase Cart que contiene un conjunto de ítems, entonces esa restricción no sería fácil de asegurar. Por eso, en el próximo capítulo, las asociaciones unidireccionales con restricciones en el origen se tratan como asociaciones bidireccionales: no se pueden navegar en ambas direcciones, pero se deben implementar en ambos extremos.
La actividad de diseño lógico termina cuando la DCD tiene suficiente información para implementar las clases de la capa de dominio. Esto suele ocurrir cuando se examinan todos las restricciones de funcionamiento del sistema y se incorporan sus modelos dinámicos en el diseño.
            ​ 9.8 El proceso hasta ahora


Inicio
Elaboración
Modelado del Negocio
Construir una vista general del sistema:
    • Dibujar un caso de uso del negocio y determinar el ámbito de automatización para el proyecto.
    • Dibujar un diagrama de actividad para el caso de uso del negocio
    • Dibujar un diagrama de maquina de estado para los procesos clave del sistema

Requerimientos
Preparar un diagrama de caso de uso del sistema (requisitos funcionales)
    • Identificar los actores del sistema desde el modelo de caso de uso del negocio.
    • Identificar los casos de uso del sistema desde  el modelo de caso de uso del negocio, y el diagrama de actividad y maquinas de estado desde el modelo de negocio.
Identificar los requisitos no funcionales como anotaciones de los casos de uso:
    • Identificar las principales reglas de negocio asociadas a los casos de uso.
    • Identificar las principales puntos de calidad asociados a los casos de uso.
Identificar requisitos suplementarios.
Detalle de requisitos ampliando los casos de uso: 
- Identificar el flujo principal. 
- Identificar flujos alternativos: variantes y manejadores de excepciones. 
Analisis y Diseño
Preparar un modelo conceptual preliminar observando los casos de uso del sistema y los conceptos expresados en el.
Elaborar los diagramas de secuencia del sistema: 
 - Representar el flujo principal de un caso de uso como un diagrama de secuencia del sistema. 
- Representar los comandos y consultas del sistema utilizando estrategias de estado o sin estado. 
- Completar los diagramas de secuencia del sistema con flujos alternativos. 

Refinar el modelo conceptual: 
- Identificar conceptos, atributos y asociaciones en el texto de los casos de uso ampliado. 
- Detallar los atributos y asociaciones con los estereotipos, la multiplicidad y las limitaciones, según sea necesario. 
- Organizar el modelo utilizando la herencia, las clases de asociación y las especificaciones temporales.
- Añadir invariantes según sea necesario. 
- Mejorar el modelo conceptual con la aplicación de patrones de análisis

Escribir restricciones de operación del sistema para comandos y consultas en diagramas de secuencia del sistema: 
· Identificar precondiciones y excepciones basadas en parámetros no válidos y restricciones complementarias.
· Identificar las postcondiciones  para los comandos y los retornos para las consultas. 

Diseñar la capa de dominio: 
-  Cree una secuencia o diagrama de comunicación para cada  restricción de comandos del sistema. 
-  Utilice estos diagramas para decidir qué métodos implementar en cada clase. 
-  Inspeccione esos diagramas para descubrir qué asociaciones pueden ser unidireccionales y definirlas como tales. 
-  Examinar las restricciones de consulta del sistema y decidir qué consultas  delegadas podrían implementarse; algunas de ellas podrían ser atributos derivados o asociaciones derivadas.
- Generar o refinar el diagrama de diseño de clases. 
Implementación


Pruebas/Test


Gestión del Proyecto
Estimar el esfuerzo total, el cronograma ideal y el tamaño medio del equipo para el proyecto.
Estimar la duración y el número de iteraciones para cada fase.
Preparar la fase de planificación y el plan de Iteración para la primera iteración.



            ​ 9.9 Preguntas
1. ¿Cuáles son los seis tipos de responsabilidades que pueden tener los objetos? ¿Qué tipo de método se utiliza para llevar a cabo cada responsabilidad?
2. ¿Cuáles son los cuatro tipos de visibilidad que pueden existir entre los objetos? ¿Son simétricos? ¿Cómo influye cada uno de ellos en el alto acoplamiento entre clases?
3. Lea de nuevo el último párrafo de la Sección 9.3.2. Trate de dibujar un diagrama de comunicación que ilustre esa situación. ¿Por qué es un diseño peor que el diagrama presentado en la Figura 9.29?
4. Explicar la influencia de las precondiciones y excepciones contractuales en los modelos dinámicos. ¿Cómo afectan la complejidad del modelo dinámico?
5. Dibuje un diagrama de secuencia equivalente al de la figura 9.43.

1 Sin embargo, eso es válido para los atributos normales que pertenecen a las clases del modelo conceptual. Durante la construcción del DCD, los nuevos atributos de diseño que representan el estado interno e influyen en el comportamiento de un objeto pueden llegar a ser necesarios, y esos atributos no necesariamente deben ser accedidos por otros objetos: en ese caso, no deberían tener captadores ( son privados o protegidos).
2 Recuerde que no todos los atributos deben tener un definidor. Los atributos inmutables no deben tener setter. Los atributos derivados nunca tienen setters, y los atributos privados tampoco deben tener setters públicos.
3Los prefijos de agregar y eliminar se podrían usar aquí incluso para asociaciones a 1, porque conceptualmente son enlaces como cualquier otro. Sin embargo, generalmente las asociaciones a 1 no implementan comandos como agregar y eliminar: implementan el comando establecer o reemplazar, lo que puede reemplazar el enlace obligatorio actual con otro, dejando el rol siempre consistente.
4 Se podría considerar que un rol 0..1 se llena con un solo objeto o un valor nulo. Sin embargo, eso no es coherente con la interpretación de otras multiplicidades como, por ejemplo, 0..2 o *, donde 0 representa el conjunto vacío y no el valor nulo. Para evitar tal inconsistencia, es preferible considerar que la multiplicidad 0..1 se refiere a un conjunto que puede estar vacío o contener un solo elemento.
5 Y adicionalmente a un conjunto que contiene un pedido, incluso si esa opción no se utilizara a menudo.
6A establecido por defecto.
7En este texto, se supone que las operaciones disponibles para los conjuntos y otras colecciones son las definidas por OCL (Object Management Group, 2010). Sin embargo, si se utilizan diferentes idiomas o paquetes, estaría disponible un conjunto diferente de operaciones.
8 Sin embargo, la asociación probablemente se implementaría físicamente, no como dos conjuntos (vea el Capítulo 10). Aquí, la visibilidad significa que dos conjuntos de objetos pueden obtenerse por una instancia; Esto no significa que se implementen de esa manera.
9Un resumen de la Ley de Demeter (Lieberherr & Holland, 1989)
10 Esto es cierto en condiciones normales. Sin embargo, si el sistema está sujeto a complejas condiciones de carrera y si la seguridad es un problema importante, a veces sería aconsejable una doble verificación.
11Por ejemplo, el comando de eliminación podría llamarse solo para los libros seleccionados de una lista que contiene solo libros que se pueden eliminar, es decir, libros sin elementos vinculados a ellos.
12 En general, las excepciones no recibirían el mensaje como parámetro, sino un código de excepción que hace referencia a una lista de mensajes. Sin embargo, para mantener los ejemplos más simples, se dejan aquí como están.
