# CASOS DE USO AMPLIADOS

Aquí se explica cómo detallar los casos de uso como texto y cómo evolucionarlos a diagramas de secuencia del sistema para descubrir qué operaciones de alto nivel debe implementar el sistema. Se concentra en explicar lo que es realmente necesario para la descripción de un caso de uso durante la elaboración, cuando su funcionalidad debe ser completamente entendida. Se evitan los detalles técnicos y de interfaz. Sólo los flujos de información, incluidos los flujos de variantes y excepciones, se incluyen en una descripción de caso de uso esencial; en este capítulo se explica cómo descubrirlos sistemáticamente. También explica cómo transformar una descripción textual e informal de un caso de uso en un diagrama secuencial, que es un artefacto de más elevada ceremonia.

## Palabras clave
`Detailed use case`; `expanded use case`; `full-dressed use case`; `exception in use case`; `use case alternate flow`; `essential use case`; `CRUD use case`; `system sequence diagram`

## Conceptos en este Capítulo

- Flujo principal de un caso de uso ampliado
- Movimientos alternativos: gestores de excepciones y variantes
- Redacción de recomendaciones
- Diagramas de secuencia del sistema

## 5.1 Introdución a los casos de uso ampliados
Como se explica en el Capítulo 3, los casos de uso pueden utilizarse para representar, entre otras cosas, los requisitos del sistema. Hoy en día son uno de los principales enfoques de los requisitos, ya que permiten la construcción de una estructura más fácil de entender, comunicar y gestionar que los enfoques anteriores. Ivar Jacobson identifica algunas de las razones por las que los casos de uso se hicieron tan populares:
- Un modelo de caso de uso es una imagen que permite a un equipo describir incluso un sistema complejo. Dice en términos simples lo que el sistema va a hacer por sus usuarios.
- Un caso de uso produce valor para un usuario en particular, no para una comunidad no identificable de ellos.
- Los casos de uso también son casos de prueba; cuando el equipo termina de organizar los requisitos en los casos de uso, también ha producido la estructura necesaria para los casos de prueba.
- Los casos de uso son el punto de partida para diseñar experiencias de usuario efectivas, coamo, por ejemplo, un sitio web.
- Los casos de uso impulsan el desarrollo desde el análisis hasta el diseño, desde el diseño hasta el código, y desde el código hasta las pruebas.
  
Frecuentemente, la primera actividad de análisis de las iteraciones de Elaboración, es detallar los casos de uso asignados a cada iteración. El proceso de detallar o ampliar un caso de uso en una secuencia de pasos corresponde a refinar el análisis de requerimientos, especialmente los requerimientos funcionales. En cada iteración, es posible ampliar uno o más casos de uso y analizar y diseñar las estructuras necesarias para que el producto de software cumpla con los requisitos, permitiendo a los usuarios interactuar con el sistema siguiendo los pasos indicados en el caso de uso ampliado.
Para proceder a la ampliación de un determinado caso de uso de alto nivel, es necesario tener a mano el diagrama del caso de uso del sistema, incluidas todas las anotaciones, y el documento de especificaciones suplementarias. También sería útil, para la primera iteración, tener una versión del modelo conceptual preliminar si se desarrolló durante Inicio. Para iteraciones distintas de la primera iteración de la elaboración, es muy útil tener una versión del modelo conceptual en evolución ya refinada por las actividades de iteraciones anteriores.

Como la expansión de casos de uso corresponde al refinamiento del análisis de requisitos, el equipo debe realizar un examen muy detallado del proceso incorporado en el caso de uso desde el punto de vista del usuario. El caso de uso debe ser descrito paso a paso: cómo se realiza y qué interacciones entre los actores y el sistema existen. La tecnología y las interfaces deben ser ignoradas en este punto. Sólo la información intercambiada entre el sistema y los actores es la obligatoria en estas descripciones.

Esta descripción paso a paso, en principio, no debe estructurarse como ramas. Debe basarse en una secuencia por defecto, o flujo principal (Sección 5.2), que describe lo que sucede cuando todo va bien durante la interacción entre casos de uso. A este flujo también se le llama el "camino feliz" porque en él no hay error, fracaso o excepción.

Después de describir el flujo principal del caso de uso, las reglas de negocio o los requisitos no funcionales anotados para el caso de uso deben ser revisados y analizados desde el punto de vista del usuario, con el fin de descubrir qué es lo que podría salir mal en un determinado paso, lo que podría generar una excepción. Después de identificar una posible excepción, se debe describir un procedimiento para corregir el problema (Sección 5.3.3). Puede haber al menos una excepción para cada regla de negocio. El caso de uso se completa con flujos alternativos que se asemejan a los manejadores utilizados para el manejo de excepciones en la programación.

Además de lo anterior, el equipo puede verificar si el usuario puede ejecutar el caso de uso en diferentes modos o escenarios (Sección 5.3.1). Si su estructura de ejecución varía mucho, se pueden identificar variantes del flujo principal (Sección 5.3.2).

## 5.2 Flujo principal
El flujo principal es la sección más importante de un caso de uso ampliado. Es la descripción del proceso del caso de uso cuando todo va bien, es decir, cuando no hay flujo alternativo.

En el ejemplo de la librería, un primer borrador del flujo principal del caso de uso de los libros de pedidos puede incluir la identificación del cliente, la búsqueda y selección de libros y, finalmente, el pago.

En cuanto a la identificación de los usuarios, aquí se plantea un problema recurrente: ¿Qué pasa si el usuario ya se ha identificado en un caso de uso que se ejecutó justo antes del actual? Esta es una situación común y debe ser tratada adecuadamente. Como en este punto la identificación del usuario es opcional, puede dejarse como un flujo alternativo, como se explica en la Sección 5.3. Así, para el flujo principal de este caso de uso se asume que el usuario ya es conocido por el sistema; si éste no es el caso, se debe realizar un flujo alternativo en el que el usuario se identifique a sí mismo.

Por lo tanto, las acciones que mejor describen el flujo principal de este caso de uso son las siguientes: un usuario busca y selecciona libros para comprar y procede al pago. Sin embargo, no se trata de una comunicación unidireccional, y el sistema debe presentar al usuario qué libros están disponibles para la venta, así como otra información que sea importante para el usuario, como el precio de los libros y el valor total del pedido.

La Figura 5.1 presenta un borrador del flujo principal del caso de uso de los libros de pedidos, que se considera el caso de uso de mayor prioridad del sistema Livir (Sección 4.3.5).

**Caso de uso 01: Pedir Libros**
1. El cliente proporciona palabras clave para la búsqueda de libros.
1. El sistema genera una lista de libros a la venta que coincide con las palabras clave, incluyendo al menos título, autor, precio, número de páginas, editorial, ISBN e imagen de portada. 
1. El cliente selecciona los libros de la lista e indica la cantidad deseada para cada uno. 
1. El sistema genera el resumen de la orden (título, autor, cantidad, precio unitario y subtotal para cada libro) y el valor total. 
1. El cliente finaliza el pedido. 

Figura 5.1 Primer borrador del flujo principal del caso de uso de Pedir libros.

En el paso 1 el usuario puede elegir no proporcionar una palabra clave, y luego en el paso 2 recibirá una lista con todos los libros disponibles en la librería. Por ahora no es necesario decidir sobre el formato de la interfaz. Por ejemplo, si la lista de libros es demasiado larga, tal vez una lista limitada con comandos de presentación sería preferible a una lista completa. Esto se puede decidir cuando se diseña la interfaz. La interacción del usuario con los comandos de desplazamiento de la interfaz es algo que no debe incluirse en la descripción del caso de uso esencial.  

Para ejecutar el paso 5 es necesario que el usuario esté identificado y validado, o bien, ¿cómo reanudaría el pedido más tarde? El flujo principal aquí asume que ya está identificado, pero si este no es el caso, se plantearía una excepción como se explica en la Sección 5.3.3.  

Después del paso 5 se asume que el caso de uso termina y se ha guardado el carro de la compra (como es una operación interna, no se menciona necesariamente en el caso de uso, como se explica en la Sección 5.4.6). En este punto, el usuario puede elegir desconectarse y reanudar sus compras otro día, o puede proceder inmediatamente al caso de uso de la orden de pago (Figura 5.2).


**Caso de uso 02: Orden de pago**
1. El sistema genera el resumen del pedido pendiente (título, autor, cantidad, precio unitario y subtotal para cada libro), así como el precio total del pedido y una lista de direcciones de entrega registradas para el cliente. 
1. El cliente selecciona una dirección de entrega.
1. El sistema presenta los costes de envío, la fecha de llegada programada y una lista de tarjetas de crédito ya registradas para el cliente (marca y los últimos cuatro dígitos del número de la tarjeta de crédito). 
1. El cliente selecciona una de sus tarjetas de crédito para el pago. 
1. El sistema envía al operador de la tarjeta de crédito correspondiente los siguientes datos: número de tarjeta, nombre del propietario, validez, código de seguridad, valor total de la compra y código de la tienda. 
1. El operador de la tarjeta de crédito aprueba la venta enviando un código de autorización. 
1. El sistema informa al cliente de que la venta ha sido autorizada y le proporciona el número de seguimiento del paquete. 
   
Figura 5.2 Primer borrador del flujo principal del caso de uso de la orden de pago.

Nótese que estos casos de uso son borradores porque todavía debemos discutir algunos temas y hacer algunas mejoras en sus formulaciones, lo cual ocurrirá en las próximas secciones. Por ejemplo, los flujos alternativos que se presentarán más adelante están relacionados con las posibles excepciones y variantes identificadas por el equipo. Por ejemplo, el paso 3 de la Pedir Libros puede presentar una excepción, como por ejemplo una cantidad insuficiente de libros en stock. Otra excepción evidente puede ocurrir en el paso 5 de la orden de pago, en el que el operador de la tarjeta de crédito aprueba la venta: aunque esto se necesita para el éxito del caso de uso, puede no ocurrir.

Las excepciones, sin embargo, en lugar de producir pruebas condicionales en el flujo principal, deben ser ignoradas por él y manejadas por separado. Sería más difícil entender el propósito de un caso de uso que tiene en su cuerpo una estructura algorítmica que considera todas las excepciones posibles, como la que se muestra en la Figura 5.3.

**Caso de uso 01: Pedir Libros**
(manejo inadecuado de las excepciones en el flujo principal) EVITAR! 
1. Si el cliente no tiene un registro, entonces se registra, indicando su nombre, teléfono, dirección, número de seguro social y al menos una tarjeta de crédito. Si ya está registrada, entonces se identifica, a menos que ya haya sido identificada anteriormente. 
2. Si el cliente todavía no ha pagado la última venta, el sistema muestra la cesta de la compra para que se pueda pagar, cancelar o reanudar. 
3. El sistema presenta las opciones de libros a la venta, indicando al menos el título, autor, precio, número de páginas, editorial. ISBN, e imagen de portada. 
4. El cliente selecciona los libros, e indica la cantidad deseada de cada uno. Si la cantidad deseada no está disponible en stock, el sistema debe pedir al usuario que rehaga el pedido teniendo en cuenta la cantidad disponible. Si la cantidad es cero, el cliente debe tener la opción de retirar ese artículo del pedido. Todavía es posible para el cliente dividir su pedido en dos bandejas, recibiendo lo antes posible los libros disponibles y recibiendo una segunda entrega con los libros que faltan cuando sea posible. 
5. ...
Figura 5.3 Caso de uso con excepciones manejadas inadecuadamente en el flujo principal.

El problema con el flujo de casos de uso en la Figura 5.3 que lo hace tan innecesariamente complejo es la cantidad de afirmaciones "if-then" en su formulación. El flujo principal no debe ser rociado con condiciones. Debe indicar lo que sucedería en una situación ideal en la que toda la información transmitida es correcta y completa. Las excepciones y otras variaciones al flujo principal deben manejarse como flujos alternativos, como se ve en la siguiente sección.

## 5.3 Flujos alternativos
Un caso de uso especifica un proceso que se puede realizar en la vida real de varias maneras diferentes. Dos personas comprando libros tomarían diferentes secuencias de pasos. Si las secuencias son suficientemente similares2, se debe utilizar el mismo flujo para describir ambas. Pero en algunas situaciones se deben utilizar flujos alternativos para indicar secuencias que podrían ocurrir de maneras muy diferentes.
Existen básicamente dos tipos de flujos alternativos: variantes (Sección 5.3.2), que indican diferentes formas de alcanzar el mismo objetivo, y manejadores de excepciones (Sección 5.3.3), que indican cómo tratar los problemas que aparecen durante la ejecución de un caso de uso.
Sin embargo, a veces las variantes son tan diferentes que pueden considerarse casos de uso individuales. Entonces, las variantes pueden ser escenarios simples (Sección 5.3.1) de un solo caso de uso, o, a veces, pueden ser la clave para descubrir nuevos casos de uso.

### 5.3.1 Escenarios
Un caso de uso puede entenderse como una descripción o especificación general que soporta un conjunto de escenarios diferentes. Cada escenario es una realización o instancia particular del caso de uso. Normalmente, un caso de uso tiene un escenario principal (ejecución del flujo principal) y escenarios alternativos (ejecuciones del flujo principal que pasan por uno o más flujos alternativos). Sin embargo, la noción de variantes de flujo principal a veces crea dudas sobre lo que realmente debería ser un caso de uso. En el ejemplo de la librería, considerando el proceso de compra de libros, se me ocurren al menos dos escenarios diferentes:
- Un cliente ordena libros y guarda el carrito de compras para continuar comprando más tarde.
- Un cliente hace un pedido de libros y paga por ellos.
¿Es un solo caso de uso con dos finales alternativos? ¿O debería dividirse en dos casos de uso?
Ambas opciones son igualmente válidas, aunque una de ellas es posiblemente más útil que la otra. Las posibilidades son:
- Crear más casos de uso (uno para cada escenario). Cada caso de uso tiene una estructura más simple, pero habría un gran número de casos de uso similares.
- Agrupe escenarios similares en un solo caso de uso. Hay un número menor de casos de uso, pero cada uno de ellos sería más complejo.
En este punto, es más importante descubrir la información intercambiada entre los actores y el sistema que decidir si dos escenarios consisten en uno o dos casos de uso. Por lo tanto, no es tan importante, con respecto al resultado final, si las operaciones se descubren o describen en un caso de uso único con dos escenarios o en dos casos de uso, cada uno con un único escenario.
La ventaja de unir escenarios alternativos en un solo caso de uso es que la descripción de algunos pasos no debe repetirse en casos de uso diferentes. Esta es la misma ventaja que se obtiene cuando los atributos de las diferentes clases son compartidos por una superclase (Sección 6.6.1).
Sin embargo, los casos de uso no deben considerarse llamadas a procedimientos: estos son descripciones lineales de escenarios que pueden darse en el mundo real, donde un usuario interacciona con un sistema.

### 5.3.2 Variantes
Se admite, en principio, que el flujo principal es una secuencia estricta de pasos de interacción: no está ramificado ni anidado. Sin embargo, a veces puede ser útil representar la secuencia principal de una manera no tan lineal.
Como se mencionó en la sección anterior, los casos de uso para pedir libros y pagar por ellos podrían considerarse un caso de uso único con dos escenarios. En ese caso, cada escenario sería un final alternativo para el caso de uso: Guardar carrito de compras o Continuar con el proceso de compra.
Estas dos posibles terminaciones pueden ser representadas como variantes del flujo principal de un caso de uso único.
Como se muestra en la Figura 5.4, el caso de uso Comprar libros tiene dos finalidades posibles: en la primera, el carrito se guarda para que el pedido se pueda reanudar más tarde, y en la segunda, el cliente paga y termina el pedido.

**Caso de uso 01/02: Compra de libros**
(se une con Pedir libros y Pagar pedido)
1. El cliente proporciona palabras clave para la búsqueda de libros. 
1. El sistema genera una lista de libros a la venta que coincide con las palabras clave, incluyendo al menos el título, autor, precio, número de páginas, editorial, ISBN e imagen de portada. 
1. El cliente selecciona los libros de la lista e indica la cantidad deseada para cada uno. 
1. El sistema genera el resumen de la orden (título, autor, cantidad, precio unitario y subtotal para cada libro) y el valor total. 

1. El cliente finaliza el pedido. 
1. El cliente decide:
        ◦ Guardar el carro de la compra: Variante 6a.
        ◦ Proceder al pago: Variante 6b. 

Variante 6a: Guardar el carro de la compra

6a.1   El cliente informa al sistema de que se debe grabar la cesta de la compra. 
6a.2   El sistema informa al cliente de cuántos días estará disponible el carro. 

Variante 6b: Proceder al pago

6b.1   El sistema genera una lista de direcciones registradas para el cliente.  
6b.2   El cliente selecciona una dirección de entrega.  
6b.3  El sistema presenta la tarifa de entrega, la fecha prevista de llegada y una lista de las tarjetas de crédito ya registradas para el cliente.  
6b.4   El cliente selecciona una de sus tarjetas para el pago.  
6b.5  El sistema envía al operador de la tarjeta de crédito correspondiente los siguientes datos: número de tarjeta, nombre del propietario, validez, código de seguridad, valor total de la compra y código de la tienda.  
6b.6 El operador de la tarjeta de crédito aprueba la venta enviando un autorización.  
6b.7  El sistema informa al cliente de que la venta se ha autorizado y le proporciona un número de seguimiento.  


Figura 5.4 Flujo principal de un caso de uso con variantes.

Guardar el carrito para reanudar el pedido más tarde no es una excepción (en el sentido indicado en la Sección 5.3.3) sino una opción para el cliente. Esa no es una condición que impida que el caso de uso concluya, porque el caso de uso todavía produce algo: el carrito se almacena para ser usado más tarde. Ésta es sólo una variante de movimiento principal, y por ello ambas variantes se muestran con el mismo status en el flujo.3

Algunos analistas pueden elegir una de las variantes para que esté en el flujo principal y la otra para que sea un flujo alternativo en forma de variante. En la Figura 5.5 se eligió la variante Proceder al pago para que estuviera en el flujo principal, mientras que la variante Guardar carro de la compra se dejó fuera del flujo principal. Una ventaja de esta elección es que permite asociar la variante a más de un paso en el flujo principal. Por ejemplo, tenga en cuenta que la variante Grabar cesta de la compra puede ejecutarse cuando el usuario se encuentra en cualquier paso del 1 al 8. En este caso el código de la variante sería el 1-8a. Si la variante pudiera ejecutarse en cualquier momento durante el flujo principal, su número sería *a.

**Caso de uso 01/02: Comprar libros**
1. El cliente proporciona palabras clave para la búsqueda de libros.
1. El sistema presenta una lista de libros a la venta que coincide con las palabras clave, incluyendo al menos el título, autor, precio, número de páginas, editorial, ISBN e imagen de portada. 
1. El cliente selecciona los libros de la lista e indica la cantidad deseada para cada uno. 
1. El sistema genera el resumen del pedido (título, autor, cantidad, precio unitario y subtotal para cada libro) y el valor total. 
1. El cliente finaliza el pedido.
1. El sistema genera una lista de direcciones registradas para el cliente.
1. El cliente selecciona una dirección de entrega.
1. El sistema presenta la tarifa de entrega, la fecha de llegada programada y una lista de tarjetas de crédito ya registradas para el cliente.
1. El cliente selecciona una de sus tarjetas para el pago. 
1. El sistema envía al operador de la tarjeta de crédito correspondiente los siguientes datos: número de tarjeta, nombre del propietario, validez, código de seguridad, valor total de la compra y código de la tienda. 
1. El operador de la tarjeta de crédito aprueba la venta enviando un código de autorización.
1. El sistema informa al cliente de que la venta ha sido autorizada y le proporciona el número de seguimiento del paquete. 
2. 
Variante 1-8a: Guardar carro de compras 

1-8a.1. El cliente indica al sistema que la compra debe guardarse.   
1-8a.2. El sistema informa al cliente de cuántos días estará disponible su carro.   

Figura 5.5 Forma alternativa de representar un caso de uso con variantes en las que una se mantiene en el flujo principal y las otras en el flujo alternativo.

Este estilo, aunque predominante en la literatura, obliga al analista de casos de uso a elegir entre variantes que pueden ser artificiales en algunos casos. Si no hay un claro predominio entre las diferentes variantes, entonces un estilo como el presentado en la Figura 5.4 parece preferible, porque da el mismo estatus a cada una de ellas.

### 5.3.3 Manejo de excepciones
Después de describir el flujo principal de un caso de uso y añadir variantes (si las hubiera), el analista debe concentrarse en identificar las excepciones que podrían ocurrir y crear un flujo alternativo para cada una. Existen básicamente dos técnicas para identificar las excepciones:
1. Cada regla de negocio anotada para un caso de uso puede generar una excepción. Por ejemplo, si el caso de uso para ordenar libros tiene una regla de negocio que establece que el valor del pedido no puede ser inferior a 50 dólares, entonces cuando se confirma un pedido habrá una excepción si no alcanza ese valor. Para hacer frente a esta excepción será necesario añadir más libros al pedido, o se cancelará.
2. Adicionalmente, el analista puede observar cada uno de los pasos del flujo principal, especialmente aquellos que representan información que fluye de los actores hacia el sistema. En esos flujos habrá posiblemente datos que el sistema no puede aceptar por definición, lo que constituye una excepción. Por ejemplo, en el paso en el que se le pide al operador de la tarjeta de crédito que autorice la venta, podría enviar un código de rechazo - esto sería una excepción, porque el caso de uso no puede completarse con éxito. En ese caso, se deben tomar medidas correctivas (fuera del flujo principal), o el caso de uso se dará por terminado sin alcanzar sus objetivos.
   
Una excepción (en el sentido utilizado en informática) no es necesariamente un evento que rara vez ocurre, sino un evento que si no se maneja impide que un proceso continúe. Una excepción no es necesariamente algo que impide que se inicie un caso de uso, pero normalmente es algo que impide que se concluya. El hecho de que la tarjeta de crédito haya alcanzado su límite no impide que el cliente acceda al sitio de la librería y empiece a comprar, pero le impide completar el pedido a menos que se le proporcione una tarjeta de crédito válida con crédito disponible. Por lo tanto, aunque el caso de uso puede iniciarse, no puede concluirse hasta que se manejen todas las excepciones que ocurran.

La Figura 5.6 muestra una evolución del caso de uso Pedir Libros, ahora con algunas excepciones identificadas tras el flujo principal. Cada excepción se identifica con un número que indica la línea del flujo principal de donde se origina, y una letra que ayuda a diferenciar las excepciones que pueden ocurrir en el mismo paso. Por ejemplo, si el paso 5 tiene tres excepciones, entonces se identificarán como 5a, 5b y 5c. Si una excepción puede ocurrir en cualquier paso, entonces se identifica como *a, *b, etc., y si puede ocurrir en una serie de pasos, como 3-7, se identifica como 3-7a, 3-7b, etc. Además, si una excepción puede ocurrir en pasos no adyacentes, tales como los pasos 3 y 6, entonces puede ser identificada como 3,6a. Una frase sigue al código de identificación que corresponde a la regla de negocio o situación que es la causa de la excepción. La figura 5.6 también presenta la variante 5d que permite al usuario continuar comprando otros libros en lugar de terminar el pedido. Esto no es una excepción, sólo una elección.

**Caso de uso 01: Pedir Libros**
1. El cliente proporciona palabras clave para la búsqueda de libros.
2. El sistema genera una lista de libros a la venta que coincide con las palabras clave, incluyendo al menos título, autor, precio, número de páginas, editorial, ISBN e imagen de portada. 
3. El cliente selecciona los libros de la lista e indica la cantidad deseada para cada uno. 
4. El sistema genera el resumen de la orden (título, autor, cantidad, precio unitario y subtotal para cada libro) y el valor total. 
5. El cliente finaliza el pedido. 
   
Excepción 3a: La cantidad solicitada es superior a la cantidad en stock de uno o más libros.   
Excepción 5a: El cliente aún no está identificado.   
Excepción 5b: El cliente no tiene una cuenta.   
Excepción 5c: No se seleccionó ningún libro para la compra.   


Figura 5.6 Ejemplo de caso de uso con excepciones identificadas.

El número de excepciones que un equipo puede hacer puede ser muy alto; sin embargo, sólo nos interesan algunas de ellas. La mayoría de las excepciones en las que se podría pensar pueden ser resueltas por otros mecanismos que no sean la lógica del caso de uso. Una clave para reducir la complejidad de los casos de uso y seguir tratando con la complejidad del sistema es reducir el número de excepciones identificadas aquí a aquellas que realmente deben ser tratadas. Las excepciones que ahora son realmente interesantes son aquellas en las que el usuario intenta enviar al sistema algunos datos que no pueden ser aceptados. Cualquier otro tipo de excepción probablemente pueda ser resuelta por otros mecanismos. En el ejemplo de la figura 5.6:

- En el paso 1 no puede haber excepciones porque el sistema puede aceptar cualquier palabra clave que el usuario proporcione. Simplemente sucede que para algunas palabras clave puede que no haya ningún libro para presentar. En este caso, el comportamiento del sistema no debería mostrar libros, o tal vez mostrar los libros que más se acerquen a las palabras clave (Google lo hace). Esta no es una excepción que impida que el caso de uso continúe, sólo un caso especial de su comportamiento.
- En el paso 2, y en cualquier otro paso en el que el sistema presente datos, no puede haber excepciones en la lógica, porque en el paso 2 el sistema no está intentando acomodar los datos enviados por el usuario; si se produjera alguna excepción, entonces probablemente habría ocurrido en el paso anterior y habría generado un efecto aquí. El sistema que muestra una lista sin libros no es una excepción. Nuevamente es un caso especial de su comportamiento normal, y la acción del usuario sería no elegir ningún libro en el paso 3 y después repetir el paso 1 o proceder a terminar la orden en el paso 5.
- Aún en el paso 2, un analista podría pensar: "¿Qué pasa si los cálculos relacionados con la consulta tienen un defecto que hace que el sistema se detenga al intentar presentar el resultado? Bueno, si el código tiene un defecto, entonces debe ser corregido, y no incorporado en la lógica del caso de uso. Este no es el tipo de excepción que nos interesa.
- En cualquier momento, un analista puede pensar que podría ocurrir una excepción si falla la comunicación entre el sistema y el usuario. Esto es lo que los desarrolladores suelen entender como una excepción en el mundo real. Sin embargo, este no es el tipo de excepción que nos interesa aquí, porque no es específico de la lógica del caso de uso; la comunicación puede fallar en cualquier momento - no importa qué paso de cada caso de uso se esté ejecutando. Además, esta excepción está relacionada con la tecnología, y se trata de casos de uso esencial, en los que se evitan las referencias a la tecnología de implementación. Por lo tanto, este tipo de excepción debe ser implementada por mecanismos generales, no por la lógica del caso de uso.
- En el paso 3, ¿qué pasa si el usuario indica una cantidad negativa? ¿Y si escribe una carta en el campo de cantidad? Aquí la idea es que todas las malas acciones del usuario podrían ser eliminadas por simples widgets de la interfaz. Por ejemplo, en lugar de escribir un número en un cuadro de texto, el usuario selecciona una cantidad deslizando una barra que representa sólo cantidades positivas. Estos mecanismos de interfaz forman parte de la tecnología y no deben mencionarse en el caso de uso esencial. Sin embargo, el analista puede saber que hay maneras de evitar que un usuario elija una cantidad negativa o "xyz", y por lo tanto esto no es una preocupación que deba incluirse en la estructura del caso de uso. Como se explicó en el Capítulo 8, este tipo de error sintáctico del usuario se tratará definiendo el tipo de argumentos que el sistema puede recibir. Si el tipo se define como "natural,4" entonces el equipo no debe preocuparse por ningún otro valor; simplemente no puede ser producido por el usuario. La interfaz no lo permitirá.
- Sin embargo, hay una excepción lógica en el paso 3, que corresponde a que el usuario solicite una cantidad superior a la disponible en stock. La cantidad de libros disponibles en stock varía de un libro a otro y varía en el tiempo. Por lo tanto, no puede definirse como un tipo estático. El sistema podría impedir que el usuario seleccionara una cantidad superior a la disponible, pero en ese caso, el sistema tendría que verificar esas cantidades antes de la acción del usuario.
- Finalmente, el paso 5 tiene al menos tres excepciones que son justo el tipo que estamos buscando; tres problemas que están relacionados con la lógica del caso de uso y que impiden que el caso de uso alcance sus objetivos: un usuario que aún no está identificado, un usuario que no tiene identificación válida, y un pedido sin libros seleccionados.

A través de la discusión anterior podemos concluir que en la práctica las excepciones ocurren generalmente en pasos que corresponden a la información que se envía al sistema, porque sólo en esos casos existen reglas de negocio o situaciones que impiden que el sistema acepte los datos y siga adelante. Muchas excepciones potenciales pueden ser tratadas como chequeos de tipo o asuntos tecnológicos, como se explicó anteriormente. Y en la mayoría de los casos, las excepciones identificadas en un paso en el que el sistema presenta información deberían haberse tratado en el paso anterior en el que el usuario estaba enviando información al sistema. En resumen, las excepciones interesantes en un flujo de casos de uso son aquellas en las que el usuario intenta enviar información que el sistema no puede aceptar.

Cada excepción debe ser manejada por un flujo alternativo que corresponda a una rama del flujo principal. Este flujo alternativo define una secuencia de pasos que deben realizarse para eliminar el problema creado por la excepción. Si esta secuencia de pasos no se puede realizar o si el actor no quiere realizarlos, la única opción que queda es abortar el caso de uso, es decir, terminarlo sin alcanzar ninguno de sus objetivos.

Por lo tanto, cada excepción identificada en un caso de uso tiene un manejador de excepciones. Un gestor de excepciones tiene al menos cuatro partes:

- Un código de identificación que, como se ha explicado anteriormente, consiste en el número de la(s) etapa(s) que origina(n) la excepción, seguido de una letra que identifica la excepción.
- La excepción, que consiste en una frase que indica qué regla de negocio se rompió, porque en una sola línea en el flujo principal pueden ocurrir diferentes tipos de excepciones, como en, por ejemplo, el paso 5 del caso de uso de la Figura 5.6.
- Acciones correctivas que consisten en un flujo alternativo, es decir, una secuencia de acciones que se deben realizar para corregir la excepción. Las acciones correctivas se numeran secuencialmente y cada paso va precedido de la identificación de excepción. Por ejemplo, la excepción 2a tiene pasos numerados como 2a.1, 2a.2, 2a.3, etc.
- Finalización, que es la última línea del flujo alternativo e indica si y cómo el caso de uso regresa al flujo principal después de realizar las acciones correctivas.
  
Hay cinco maneras básicas de terminar una secuencia de acciones correctivas:
1. Termine el caso de uso normalmente después de que se hayan realizado las acciones correctivas. Por defecto, si no se menciona ninguna acción de finalización, se asume que el caso de uso termina al final del flujo alternativo. El caso de uso no retorna al flujo principal sino que sus objetivos son alcanzados por el flujo alternativo.
2. Vuelva al paso anterior al que causó la excepción. A veces es necesario volver al principio del caso de uso o retroceder algunos pasos antes del que causó la excepción. Esto no es muy común ni deseable, porque implica que el usuario repetirá los pasos que ya se han dado. Sin embargo, en los sistemas que deben obtener datos en tiempo real o en los sistemas con transacciones concurrentes intensivas, este puede ser el caso.
3. Vuelva al paso que causó la excepción y vuelva a realizarla. Esto es más habitual. Se debe elegir esta opción cuando el paso que causó la excepción pueda eventualmente causar otras excepciones, incluso si una de ellas ya ha sido manejada. Este es el caso de las excepciones del paso 6 de la Figura 5.6, porque además de no tener una identificación válida, el usuario no podría haber seleccionado ningún libro.
4. Avanzar a algún paso después del que causó la excepción. Esto se puede hacer cuando las acciones correctivas ya han producido lo que el paso o secuencia de pasos se suponía que debían hacer. Sin embargo, todavía es necesario comprobar si podrían producirse nuevas excepciones en el flujo principal o alternativo (véase la opción anterior).
5. Aborta el caso de uso. En este caso, el control no vuelve al flujo principal y el caso de uso no alcanza sus objetivos. Si es necesario realizar algunas acciones correctivas (por ejemplo, eliminar registros transitorios), esto puede indicarse en los pasos del flujo alternativo (este enfoque para manejar una excepción se conoce como pánico organizado).
   
La Figura 5.7 presenta una nueva versión del caso de uso de los libros de pedidos, ahora con las acciones correctivas para los flujos alternativos definidos.


**Caso de uso 01: Pedir Libros**
1. El cliente proporciona palabras clave para la búsqueda de libros.
2. El sistema genera una lista de libros a la venta que coincide con las palabras clave, incluyendo al menos título, autor, precio, número de páginas, editorial, ISBN e imagen de portada. 
3. El cliente selecciona los libros de la lista e indica la cantidad deseada para cada uno. 
4. El sistema genera el resumen de la orden (título, autor, cantidad, precio unitario y subtotal para cada libro) y el valor total. 
5. El cliente finaliza el pedido.
    
Excepción 3a: La cantidad solicitada es superior a la cantidad en stock de uno o más libros.   
3a.1. El sistema informa las cantidades disponibles para cada libro en el que el usuario ha pedido más de lo que está disponible.   
3a.2. El usuario cambia las cantidades deseadas para cumplir con las cantidades en stock.*   
3a.3. Avance al paso 4.   
Excepción 5a: El cliente aún no está identificado. 
5a.1 . El cliente proporciona una identificación válida.   
5a.2. Vuelva al paso 5.    
Excepción 5b: El cliente no tiene una cuenta. 
5b.1 . El cliente se registra proporcionando un nombre de usuario, una contraseña y una dirección de correo electrónico.   
5b.2. Volver al paso 5.   
Excepción 5c: No se seleccionó ningún libro para la compra.   
5c.1. Volver al paso 1.   
Variante 5d: El cliente decide seguir comprando. 
5d.1 . Vuelva al paso 1

Figura 5.7 Ejemplo de caso de uso con manejadores de excepciones.   
*Contrariamente a lo que se dijo en el Modelo de negocio, aquí asumimos por simplicidad que los libros agotados no pueden ser vendidos.*

En el ejemplo, cada excepción identificada y manejada es específica para el paso en el que se produce. Por ejemplo, la cantidad de libros disponibles sólo se puede detectar en el paso 3 cuando el usuario lo proporciona.  
Es importante que sólo se incluyan en el caso de uso las excepciones que son específicas para algunos pasos. De lo contrario, podría convertirse rápidamente en algo innecesariamente complejo. Las excepciones genéricas que puedan ocurrir en cualquier paso de cualquier caso de uso no deben ser tratadas como excepciones aquí. Por ejemplo, el actor puede cancelar un proceso en cualquier momento. Ese tipo de situación se maneja más adecuadamente mediante mecanismos genéricos. Para este ejemplo, debe preverse un mecanismo genérico de desmantelamiento para el sistema. Si se incluyera este tipo de excepción en todos los casos de uso, se introduciría un gran número de excepciones similares sin resultado práctico. Si en cualquier paso de cualquier caso de uso el usuario puede cancelar la transacción, no es necesario repetir esa información muchas veces. Pueden existir cientos o miles de pasos en el conjunto de casos de uso de un sistema. Las excepciones genéricas que son específicas para un caso de uso único se pueden numerar con la notación "*". En caso contrario, si la excepción puede darse en cualquier caso de uso o en un gran número de ellos, deberá consignarse en el pliego de condiciones complementario y, por tanto, deberá aplicarse mediante mecanismos generales y no mediante pasos específicos para cada caso de uso.

## 5.4 Recomendaciones de redacción
El estilo de escritura de un caso de uso debe seguir un patrón como "el actor proporciona... / el sistema informa....". Estilos como "el sistema pregunta..." deben evitarse, porque lo que debe representarse en el caso de uso es el flujo de información, no las demandas ocasionales que dieron lugar a esos flujos; esas demandas no existen en todos los escenarios, y en la mayoría de ellos ni siquiera son necesarias.  
El equipo debe evitar colocar condiciones en el flujo principal del caso de uso. Deben evitarse condiciones como "si el usuario tiene un registro, el sistema presenta...". Este tipo de prueba es innecesaria porque los manejadores de excepciones ya deberían estar asociados a los pasos del flujo principal. Entonces, si ocurre una excepción, se manejaría en un flujo alternativo.  

Estas pruebas no deben colocarse en el flujo principal para evitar que se convierta en un diagrama de flujo complejo en lugar de una secuencia de pasos recta y sencilla. Muchas de las afirmaciones de "si/entonces" pueden hacer que el flujo sea oscuro, y la parte interesada no sabría cuál es el flujo esperado (camino feliz).

La única situación en la que una prueba sería aceptable en un flujo es cuando se trata de un solo paso opcional, como, por ejemplo, "si el usuario lo desea, también puede proporcionar su número de teléfono móvil". Pero incluso en ese caso, un flujo alternativo sería una mejor opción.

Otro aspecto común de la escritura, es que un caso de uso debe alternar entradas y salidas de información. En otras palabras, normalmente un caso de uso tiene la forma *"el actor proporciona .... , el sistema informa... , el actor proporciona... , el sistema informa... ."*
Secuencias como *"el actor proporciona ...., el actor proporciona..., el actor proporciona..., el actor proporciona..."* o *"el sistema informa..., el sistema informa..., el sistema informa..., el sistema informa..."* deben evitarse a menos que se justifique.

La idea detrás del patrón alterno es reducir cualquier discrepancia en el número de pasos que diferentes analistas podrían asignar al mismo caso de uso. Sin esa regla, un analista podría escribir:

1. El cliente proporciona su nombre, ID,5 y número de teléfono.
Por otro lado, otro analista podría escribir:
1. El cliente proporciona su nombre.
2. El cliente proporciona su identificación.
3. El cliente proporciona su número de teléfono.
   
La versión más útil y correcta desde este punto de vista es la primera, porque, entre otras cosas, la segunda exigiría que la información se proporcionara en el orden de los pasos: después de proporcionar su ID, el usuario no puede volver atrás y corregir su nombre. Así, la primera versión es más compatible con la mayoría de los sistemas de información, que presentan interfaces donde la información puede ser introducida y editada antes de ser finalmente enviada al sistema.  
Una secuencia de dos pasos de entrada sólo puede justificarse si el primer paso puede causar una excepción que pueda impedir que el caso de uso siga adelante. Un ejemplo de esto es:  
1. El cliente proporciona una identificación.
2. El cliente proporciona la marca, el número, la fecha de vencimiento y el código de seguridad de su tarjeta de crédito.  
En este ejemplo, cuando el cliente presenta una identificación, se producirá una excepción si la identificación no es válida. En ese caso, la información sobre la tarjeta de crédito no debe ser proporcionada por el usuario. El actor sólo dará esa información después de que se haya realizado el primer paso o se hayan tomado las medidas correctivas.
Incluso en ese caso, se podría utilizar un paso intermedio de validación para mejorar la comprensión de la secuencia, como por ejemplo:  
1. El cliente proporciona una identificación.
2. El sistema valida la identificación del cliente.
3. El cliente proporciona la marca, el número, la fecha de vencimiento y el código de seguridad de su tarjeta de crédito.  
Por último, algunos mensajes del sistema pueden evitarse en el flujo de casos de uso porque no implican que el sistema presente información almacenada. Por ejemplo, el primer paso para el flujo alternativo para la excepción 5a en la Figura 5.5 podría ser *"El sistema informa al usuario que el cliente aún no ha sido identificado"*. Esto no es un error, pero el paso es algo redundante en el flujo porque la excepción ya establece la condición que lo causa. Al diseñar una interfaz para manejar esa excepción, el equipo debe preocuparse por mensajes de error como ese. Sin embargo, no es necesario para entender el flujo de información del caso de uso. Tenga en cuenta que si fuera necesario, cualquier gestor de excepciones en cualquier caso de uso debería empezar por presentar un mensaje de excepción, lo que ya puede deducirse de la condición de excepción. Se puede asumir por defecto que el mensaje se mostrará, por lo que no es necesario mencionarlo cada vez.

### 5.4.1 Caso de uso esencial versus real
Una duda frecuente sobre los casos de uso es qué sistema debe describirse. ¿El actual? ¿O el que se construirá? Si las operaciones actuales se realizan manualmente, y en el futuro se realizarán con un ordenador, ¿cuál debe ser la descripción proporcionada por el caso de uso? La respuesta es ninguna, ¡pero ambas! El caso de uso escrito con fines de análisis debe describir la esencia de las operaciones, no su realización concreta. Por lo tanto, el analista siempre debe tratar de evitar mencionar la tecnología utilizada para realizar el proceso y concentrarse sólo en la información intercambiada. En lugar de escribir "el empleado escribe el nombre y la dirección del cliente en una hoja de papel", correspondiente a una tecnología manual utilizada normalmente en sistemas no automatizados, o "el cliente rellena el nombre y la dirección en la pantalla principal", que corresponde a una tecnología automatizada, el analista debe registrar el caso de uso simplemente porque "el cliente proporciona un nombre y una dirección". La última forma es libre de tecnología e independiente de interfaces y representa, por lo tanto, una descripción esencial para la operación.

Todos los casos de uso utilizados a efectos de los requisitos deben ser, en principio, esenciales. Esencial en este contexto significa que el caso de uso se describe en un lenguaje donde sólo se presenta la esencia de las operaciones, no su contraparte concreta. En otras palabras, el analista debe describir *"lo que"* ocurre entre el usuario y el sistema sin informar *"cómo"* se produce esa interacción. El analista no debe, por lo tanto, mientras realiza el análisis, intentar describir la tecnología de la interfaz entre el usuario y el sistema. Esto se describirá durante el tiempo de diseño en el que se pueden escribir casos de uso reales después de que se haya diseñado la interfaz real. Los casos de uso real se mantienen unidos a una tecnología de interfaz específica, mientras que los casos de uso esencial están libres de tecnología.

¿Por qué casos de uso esenciales? Según Ambler (2004), los casos de uso real (los que mencionan la tecnología) contienen demasiadas suposiciones incorporadas, a menudo ocultas o implícitas sobre la tecnología subyacente en las estrategias de implementación de interfaces. Esto puede ser una buena característica durante el diseño, pero no durante el análisis de requisitos. Un caso de uso esencial, por otro lado, establece las necesidades o intenciones del usuario, y no la tecnología concreta que podría apoyar esas necesidades.

Como la descripción del caso de uso en ese momento se hace sin referencia a la tecnología de interfaz, no es necesario decidir cómo son las interfaces, sino sólo qué información se intercambia entre los agentes y el sistema. Las referencias a menús, ventanas, botones y otros dispositivos gráficos deben evitarse en el texto de los casos de uso esencial.

Entonces, ¿cómo describimos los casos de uso que parecen ser particularmente concretos como, por ejemplo, sacar dinero de un cajero automático? ¿Cómo lo hacemos sin describir la tecnología? Es posible.

En lugar de decir "el usuario pasa una tarjeta magnética" se podría decir que "el usuario proporciona identificación". En lugar de decir que la máquina "imprime los detalles de la cuenta", se podría decir que la máquina "presenta los detalles de la cuenta". Así, al eliminar la referencia a la tecnología física, sólo queda la esencia. Esto abre el camino para el diseño de tecnologías innovadoras más adelante, es decir, interfaces diferentes a las que se pueden ver a primera vista. Por ejemplo, el usuario puede ser identificado por huellas dactilares, el recibo puede ser enviado por SMS (Short Message Service), e incluso el dinero puede ser entregado en efectivo o en créditos a una tarjeta precargada.

Es responsabilidad del analista estudiar los procesos actuales de la empresa y producir una versión esencial de los mismos en forma de casos de uso. Más tarde, el diseñador dará una nueva forma a esos procesos utilizando la tecnología para producir una nueva versión concreta del sistema.

### 5.4.2 Información explícita
En aras de la comprensión de los casos de uso como requisitos funcionales, se recomienda que el analista explicite los datos individuales intercambiados entre los actores y el sistema. Así, en lugar de un lacónico "el cliente proporciona sus datos", el caso de uso debería decir "el cliente proporciona su nombre, identificación, correo electrónico, teléfono y dirección".

Eventualmente, un término como "`cliente`" podría definirse externamente como "`nombre, ID, correo electrónico, teléfono y dirección`". Una expresión como `customer=<nombre, id, email, teléfono, dirección>` podría ser escrita. Si esa definición se registra adecuadamente, por ejemplo, en el modelo conceptual o en un diccionario de datos, puede utilizarse en el texto del caso de uso para evitar repetir los elementos individuales cada vez que se necesiten.

### 5.4.3 Identificación y selección
Un problema recurrente asociado a los casos de uso es cómo identificar personas y cosas. Por ejemplo, un cliente debe ser identificado y validado para concluir el caso de uso de Pedir libros. ¿Cómo lo hace ella? Nombre de usuario y contraseña? ¿Número de la seguridad social? ¿Huellas dactilares? ¿Seleccionar el nombre de una lista o menú predefinido? Para mantener el caso de uso esencial, esa acción particular debe dejarse genérica, y las referencias a las posibles formas de identificar a un cliente deben dejarse al diseño. Además, la comunidad de seguridad informática ya ha establecido métodos comunes para validar de forma segura una identidad, y estos métodos probados deberían utilizarse en lugar de reinventar la rueda. Por ahora, el caso de uso simplemente indicará que el usuario proporciona identificación, sin mencionar por qué medio se obtuvo y validó esa identificación. Esto se puede hacer cuando los problemas de seguridad se diseñan en el sistema.

Otro ejemplo es la selección de libros para la compra. ¿El cliente envía el ISBN del libro? ¿Lo selecciona de una lista? ¿Utiliza una interfaz de voz en lenguaje natural? Durante la expansión del caso de uso, no es necesario decidir estos temas (a menos que se trate de requisitos no funcionales o suplementarios). En el nivel esencial del caso de uso, el usuario simplemente selecciona los libros. Posteriormente, el diseño presentará algunas opciones para proporcionar los medios para que el usuario pueda hacer esa selección de la forma más cómoda posible.

### 5.4.4 Pasos obligatorios
Una de las mayores dudas manifestadas por los equipos que trabajan con casos de uso es qué pasos incluir en el caso de uso expandido.

De hecho, dos personas que describen el mismo caso de uso, a menos que tengan una convención bien establecida, pueden producir secuencias de pasos diferentes. Por ejemplo, en una librería tradicional, un analista podría decir que el empleado le pregunta al cliente qué libros quiere; pero otro analista podría ignorar ese paso y decir que el cliente simplemente recoge los libros y se los da al empleado para comprarlos. La pregunta es: ¿Cuál de las dos versiones es la correcta?

Ambos pueden ser correctos, pero uno de ellos es más útil. En cualquier escenario de este caso de uso, es obligatorio que el cliente seleccione los libros que desea comprar; de lo contrario, el pedido no podrá ser completado. Sin embargo, es opcional que el empleado pida los libros. Esto puede suceder sólo en algunos escenarios, pero no en todos. Por lo tanto, la selección de libros para comprar es obligatoria, pero pedir esa información es opcional en el flujo del caso de uso.

Los analistas deben animarse a construir versiones correctas de los casos de uso, pero no debemos detenernos ahí: diferentes analistas deben construir descripciones similares para el mismo proceso. Esto se puede obtener cuando se minimiza el número de pasos opcionales.

Cada caso de uso tiene pasos obligatorios. Estos pasos incluyen información que se transmite de los actores al sistema y del sistema a los actores (Figura 5.8). Sin uno de esos pasos, el caso de uso puede no tener sentido. Estos pasos deben aparecer en cualquier caso de uso ampliado, y su ausencia implica que el caso de uso es incorrecto.


Figura 5.8 Pasos obligatorios para el caso de uso.

Otros pasos como "consultar por libros" son opcionales o complementarios. Pueden ayudar a contextualizar el caso de uso, pero no son fundamentales porque no transmiten ninguna información a través de los límites del sistema.

Por lo tanto, un caso de uso expandido para la compra de libros debe contener pasos que indiquen que el cliente selecciona los libros que va a comprar. El cliente también debe informar al sistema de cuántas copias desea si este es el caso. El sistema debe informar al cliente del importe total de la compra.
 ¿Por qué son obligatorios estos pasos? Porque sin el intercambio de esta información sería imposible registrar adecuadamente una venta. Ciertamente no sería de gran ayuda que un sistema registrara una venta sin mencionar qué libros se vendieron o cuánto se gastó. Debido a que esa información es tan importante para la conclusión del caso de uso, se considera obligatoria para el caso de uso expandido.

En la descripción de un caso de uso, la información no aparece de la nada. Se transmite de los actores al sistema y viceversa. La ausencia de cualquier paso obligatorio puede hacer que el caso de uso parezca incompleto, como se muestra en la Figura 5.9, donde el caso de uso está mal descrito porque se omitió información obligatoria.

**Caso de uso 01: Pedir Libros**
(falta información obligatoria) EVITAR! 
1. El cliente proporciona palabras clave para la búsqueda de libros.
1. El sistema presenta una lista de libros a la venta que coincide con las palabras clave, incluyendo al menos el título, autor, precio, número de páginas, editorial, ISBN e imagen de portada. 
1. El sistema genera el resumen del pedido (título. autor, cantidad, precio unitario y subtotal para cada libro) y valor total. 
1. El cliente finaliza el pedido. 
   
Figura 5.9 Ejemplo de un caso de uso pobremente descrito que carece de pasos obligatorios.

El caso de uso en la Figura 5.9 está incompleto porque una orden necesitaría más información de la que proporciona la descripción del caso de uso. ¿Cómo podría el sistema saber qué libros quiere comprar el cliente? Independientemente de cómo se obtenga la información, son datos obligatorios que deben ser recibidos por el sistema, y por lo tanto deben ser registrados en el caso de uso.

Existe una razón clara para que toda la información obligatoria aparezca en el caso de uso ampliado: esta información se utilizará más adelante para definir cuáles son las operaciones del sistema, es decir, qué métodos deben aplicarse para satisfacer los requisitos. Si esta información no está completa en este momento, los métodos incompletos se implementarán más tarde, lo que planteará la necesidad de rehacer parte del sistema cuando se identifique el problema.

Además, la información contenida en los pasos obligatorios de los casos de uso se utilizará para refinar el modelo conceptual, que es la base de la estructura de las clases del sistema.

Dependiendo de la dirección que tome la información, se pueden identificar los pasos obligatorios:
- Eventos del sistema: Pasos que indican que cierta información es transmitida de los actores al sistema.
- Retornos del sistema: Pasos que indican que cierta información es transmitida del sistema a los actores.
Se debe tener especial cuidado al considerar los retornos del sistema. Para que esos pasos sean realmente obligatorios deben pasar alguna información que el sistema almacena o a la que puede acceder. Esa información debe ser algo a lo que, en principio, los actores no tienen acceso, excepto mediante la consulta del sistema.

Por ejemplo, el sistema debe informar al actor del valor total de la compra en el caso de uso Pedir Libros. De lo contrario, el actor no sabrá cuánto pagar. Esa información podría ser calculada por el cliente si añade mentalmente los precios individuales de los libros, pero aún así no puede estar segura del valor total porque el sistema debe proporcionar información sobre descuentos, impuestos y tasas. La responsabilidad de proporcionar esa información corresponde al sistema.

Por otro lado, cuando un cliente envía alguna información al sistema, la interfaz puede proporcionar algún tipo de retroalimentación para dejar claro que los datos fueron recibidos y procesados adecuadamente. Sin embargo, esa retroalimentación (normalmente un mensaje como "OK", o "done") no es una devolución del sistema porque no se almacena ni deriva de información sobre libros, clientes y pedidos. Este tipo de mensaje es sólo una retroalimentación de la interfaz, y por lo tanto pertenece al dominio de la tecnología de la interfaz. Dado que no consiste en información almacenada, no debe considerarse un paso obligatorio.

Puede ser interesante si los eventos y devoluciones del sistema se identifican explícitamente en los casos de uso. Un lector que es nuevo en el uso de casos puede elegir identificar claramente los pasos obligatorios marcando las entradas con [IN] y las salidas con [OUT]. Estos marcadores pueden colocarse justo después del número de línea, como se muestra en la Figura 5.10.

**Caso de uso 01: Pedir Libros**
1.  [IN] El cliente proporciona palabras clave para la búsqueda de libros.
2. [OUT] El sistema presenta una lista de libros a la venta que coincide con las palabras clave, incluyendo al menos el título, autor, precio, número de páginas, editorial. ISBN. e imagen de portada.
3. [IN] El cliente selecciona los libros de la lista e indica la cantidad deseada para cada uno. 
4. [OUT] El sistema genera el resumen del pedido (título, autor, cantidad, precio unitario y subtotal para cada libro) y el valor total. 
5. [IN] El cliente termina el pedido. 
6. 
Excepción 3a: La cantidad solicitada es superior a la cantidad en stock de uno o más libros. 

3a.1. [OUT] El sistema informa al usuario de las cantidades disponibles para cada libro en el que el usuario ha pedido más de lo que está disponible.   
3a.2. [IN] El cliente cambia las cantidades deseadas para satisfacer las cantidades en stock. 3a.3. Avance al paso 4.   
Excepción 5a: El cliente aún no está identificado. 
5a.1. [IN] El cliente proporciona una identificación válida.   
5a.2. Vuelva al paso 5.   
Excepción 5b: El cliente no tiene una cuenta. 
5b.1. [IN] El cliente se registra proporcionando su nombre de usuario, contraseña y dirección de correo electrónico.   
5b.2.  Volver al paso 5.   
Excepción 5c: No se seleccionó ningún libro para la compra.   
5c.I. Volver al paso 1.   

Figura 5.10 Un caso de uso con los pasos obligatorios marcados.

Estas marcas también pueden ayudar al analista a verificar si cada paso es realmente una sola transacción porque ningún paso puede marcarse con [IN] y [OUT] al mismo tiempo. También ayuda al analista a ver si hay secuencias [IN] o secuencias [OUT] que se puedan unir en un solo paso.

### 5.4.5 Pasos complementarios
Otro tipo de caso de uso es el paso opcional o complementario, que no representa un flujo de información entre los actores y el sistema. Sin embargo, este tipo de paso puede ser utilizado a veces para ayudar a entender el contexto del caso de uso.  
Este tipo de paso suele corresponder a la comunicación entre actores (comunicación que no involucra al sistema, como se muestra en la Figura 5.11) o a la descripción de acciones o actitudes que tampoco configuran el flujo de información, como "el cliente abre la página de inicio de la librería", "el cliente decide comprar libros", "el sistema le pide al cliente que se identifique", o "el dependiente le pregunta al cliente qué libros quiere comprar".

Figura 5.11 Complementary use case steps.

Los pasos complementarios no son fundamentales en casos de uso esencial porque no corresponden a eventos del sistema o retornos del sistema, ya que no transmiten información a través de la frontera del sistema.  
Algunos de ellos pueden incluso asignarse a operaciones de navegación durante el diseño de la interfaz. Por ejemplo, un caso de uso real (diseño) podría tener un paso como "el cliente selecciona una opción". Esta línea no corresponde a un evento del sistema porque en ese momento el cliente no pasa ninguna información al sistema (como nombre, teléfono, dirección, título del libro, etc.). Esta acción corresponde simplemente a un cambio de estado que se implementará como navegación de la interfaz (se abre una nueva pantalla después de seleccionar la opción, por ejemplo).

### 5.4.6 Pasos inadecuados
El equipo debe tener en cuenta que, como el caso de uso es una descripción de la interacción entre los actores y el sistema, debe evitar incluir cualquier proceso interno del sistema (Figura 5.12), como "el sistema almacena la información en la base de datos". Estos pasos se consideran inadecuados para la descripción del caso de uso.

Figura 5.12 Pasos para el caso de uso inadecuado.

El caso de uso es una herramienta para describir la interacción entre los usuarios y un sistema, no una herramienta para describir el tratamiento interno. Los procesos internos del sistema se describirán mejor durante el diseño con herramientas más adecuadas, como diagramas de comunicación. 

En la descripción del caso de uso, el analista debe concentrarse en describir la información que se transmite de los usuarios al sistema (por ejemplo, "el usuario selecciona los libros que se van a pedir") y del sistema a los usuarios (por ejemplo, "el sistema presenta el total"). Se debe omitir cualquier aspecto sobre el tratamiento interno. Se puede decir que el sistema presenta el valor total, pero no los pasos que ha dado para calcularlo. En otras palabras, el sistema todavía debe ser visto como una caja negra en este momento.

Si el analista desea registrar una fórmula o un algoritmo para realizar un determinado cálculo que es necesario para presentar algunos datos, puede hacerlo en las anotaciones del caso de uso y registrarlo como un requisito no funcional.

La figura 5.13 presenta una situación en la que la descripción de un caso de uso va más allá de lo recomendado y se añaden pasos inadecuados. Los pasos inadecuados se marcan con [X].

**Caso de uso 01: Pedir Libros**
(con pasos inadecuados) EVITAR! 
1. El cliente proporciona palabras clave para la búsqueda de libros.
1. [X] El sistema verifica en la base de datos los libros que cumplen los criterios de búsqueda.
1. El sistema genera una lista de libros a la venta que coincide con las palabras clave, incluyendo al menos el título, autor, precio, número de páginas, editor. ISBN. e imagen de portada.
1. El cliente selecciona los libros de la lista e indica la cantidad deseada para cada uno.
1. [X] El sistema calcula el total de la venta como la suma de los subtotales, que consisten en el precio de cada libro multiplicado por la cantidad deseada respectiva. 
1. El sistema genera el resumen de la orden (título, autor, cantidad, precio unitario y subtotal para cada libro) y el valor total.
1. El cliente finaliza el pedido.
1. [X] El sistema marca la orden como "terminada" y la almacena en la base de datos. 
   
Figura 5.13 Ejemplo de un caso de uso con pasos inadecuados.

El caso de uso de la figura 5.13 incluye todas las etapas obligatorias, pero también las inadecuadas (etapas 2, 5 y 8), que corresponden al procesamiento interno y no a la entrada o salida de información.

El hecho de que el sistema realice verificaciones, cálculos y consultas internas no afecta su interacción con el usuario. El usuario sólo necesita saber que la información que envía es recibida por el sistema, y que puede ser recuperada del sistema cuando sea necesario. Cómo el sistema va a hacer eso es un problema interno que será contestado sólo durante el diseño y la codificación.


## 5.5 Casos de uso y fragmentos incluidos
Es posible que dos o más casos de uso tengan partes coincidentes. Por ejemplo, muchos casos de uso pueden incluir un fragmento de pago. En otros casos, un caso de uso puede incluir no sólo un fragmento, sino un caso de uso completo. La relación include sólo se puede utilizar cuando el fragmento duplicado o caso de uso es significativo, es decir, no se debe utilizar cuando sólo se duplica un paso. Un caso o fragmento de uso incluido es llamado en un flujo usando la expresión "include". Suponga que el pago es un fragmento que aparece en más de un caso de uso en el sistema. Este fragmento podría ser llamado por cualquier caso de uso como se hace en la Figura 5.14.


**Caso de uso 02: Orden de pago**
1. El sistema genera el resumen del pedido pendiente (título, autor, cantidad, precio unitario y subtotal para cada libro), así como el importe total del pedido y una lista de direcciones de entrega registradas para el cliente. 
1. El cliente selecciona una dirección de entrega.
1. El sistema presenta los costes de envío y la fecha de llegada programada,
1. Incluya el Fragmento 02a: Pago.
1. El sistema informa al cliente de que la venta ha sido autorizada y le proporciona el número de seguimiento del paquete.
   
Figura 5.14 Caso de uso que llama a un fragmento incluido.

El fragmento en sí puede definirse como en la figura 5.15.

Fragmento 02a: Pago 
1. El sistema presenta una lista de tarjetas de crédito ya registradas para el cliente (marca y últimos cuatro dígitos del número de tarjeta de crédito).
2. El cliente selecciona una de sus tarjetas de crédito para el pago.
3. El sistema envía al operador de la tarjeta de crédito correspondiente los siguientes datos: número de tarjeta, nombre del propietario, validez, código de seguridad, valor total de la compra y código de la tienda. 
4. El operador de la tarjeta de crédito aprueba la venta enviando un código de autorización. 
Figura 5.15 Un fragmento de caso de uso que puede incluirse en más de un caso de uso.

Date cuenta que el fragmento no es un caso de uso completo en este ejemplo. No puede ser ejecutado solo por un usuario; sólo puede ser ejecutado como parte de otro caso de uso.

Hay que tener algo de cuidado aquí. En primer lugar, los casos de uso no son procedimientos como los que se utilizan en los lenguajes de programación; son descripciones lineales de procesos del mundo real. No se anima a los analistas a estructurar los casos de uso como lo hacen con el código. Los casos o fragmentos de uso incluidos sólo podrán utilizarse cuando la situación lo justifique realmente.

Sin embargo, el analista debe tener en cuenta que el objetivo del caso de uso ampliado en el análisis es ayudar a comprender la naturaleza de las interacciones entre el sistema y sus actores, y no estructurar un programa de computadora para simular esa interacción. Por lo tanto, las llamadas de caso o fragmento de uso incluidas deben utilizarse con cuidado.

## 5.6 Expansión de los casos de uso estereotipados
Los casos de uso estereotipados o patrones presentan un riesgo medio o bajo para el proceso de desarrollo de software porque la estructura de sus flujos ya se conoce. La indicación de estereotipos `<<crud>>` o `<<report>>`, si se documenta adecuadamente, puede transmitir a los programadores una idea clara de lo que se tiene que implementar.

Idealmente, si los requisitos funcionales son suficientemente detallados, los casos de uso estereotipados no necesitarían ser detallados. Por ejemplo, si la especificación de un informe ya presenta toda la información que recibe y devuelve, no hay necesidad de escribir un caso de uso detallado para ello, porque sólo repetiría la información que el analista ya tiene.

Una preocupación que debe tenerse en cuenta durante la obtención de requisitos es si un caso de uso que se identificó realmente pertenece a un patrón. Se debe realizar un esfuerzo de análisis en los casos de uso antes de decidir si realmente pertenecen al patrón.6 Por ejemplo, los informes nunca deben cambiar los datos. Si el caso de uso presenta datos pero también modifica datos, no debe definirse como un caso de uso de informe. Podría ser una variación de ese patrón o una estructura completamente nueva que no pertenece a ningún patrón conocido.

En el caso de los CRUDs lo que se puede decir es que no todas las entidades del modelo conceptual son aptas para ser manejadas por el patrón CRUD. Se espera que los CRUDs sean las entidades más simples. Si se vuelven más complejos, es necesario un conjunto de casos de uso no relacionados con el CRUD para describir cómo trabaja el usuario con ellos.

Por ejemplo, una dirección o una tarjeta de crédito son entidades muy simples y podrían ser bien administradas por un caso de uso de CRUD. En el lado opuesto, un pedido es una de las entidades más complejas del sistema de la librería. Los pedidos pueden ser emitidos, cancelados, completados, enviados, reenviados, recibidos, etc. Eso no lo caracteriza como un CRUD.

En la mitad de la escala hay conceptos que el equipo debe tener en cuenta para decidir si pueden ser adecuadamente manejados como un CRUD o no. Por ejemplo, ¿la gestión de clientes es un CRUD o no? Se puede dedicar algún tiempo al análisis antes de que el equipo pueda decidirlo. El apartado 5.6.2 muestra que puede considerarse una variación del patrón CRUD.
Los modelos expandidos para los patrones de los casos de uso presentados en las siguientes subsecciones sirven como referencia para el lector. Se presentan en forma de plantilla, de modo que los analistas pueden utilizarlos para escribir sus propias versiones de casos de uso de patrones, o incluso trabajar en nuevos patrones o subpatrones.

### 5.6.1 Expasión de Informe
Un informe es un simple caso de uso que consiste en un único acceso y cálculos sobre los datos gestionados por un sistema. La información enviada por el actor consiste en argumentos de selección, filtrado, ordenación, agrupación, etc. La Figura 5.16 presenta un formato general para un caso de uso ampliado del informe.


**Caso de Uso plantilla: `<<report>>` Informe sobre ....**
1. El usuario proporciona .... 
1. El sistema muestra … agrupadas por … y ordenadas por ...
   

Figura 5.16 A template for the expanded report use case.

La Figura 5.17 presenta un ejemplo concreto de un informe, es decir, una instancia de la plantilla, aplicada al ejemplo de Livir.

**Caso de uso 18: `<<report>>` Pedidos devueltos en un período**
1. El gestor del almacén proporciona las fechas inicial y final. 
2. El sistema presenta una lista de los pedidos devueltos recibidos en el período que incluye los datos de la devolución, el número del pedido, el nombre del cliente, el valor total del pedido, el motivo de la devolución y la lista de libros devueltos (nombre, cantidad y precio). La lista de pedidos está ordenada por datos, y la lista de productos devueltos está ordenada por nombre. 
Figura 5.17 Un ejemplo de un informe ampliado.

Por las razones explicadas en la Sección 5.3.3, este tipo de caso de uso no tiene flujos alternativos (de lo contrario no sería un informe, sino un caso de uso diferente). El usuario simplemente envía los argumentos y recibe un conjunto de datos organizados a cambio. Si el usuario pasa los argumentos erróneos (por ejemplo, datos incorrectos), recibirá la respuesta correcta para los datos incorrectos. Por ejemplo, si el usuario pasa por error un período en el que no hubo devoluciones, entonces recibirá una lista vacía, que corresponde a la respuesta correcta para los argumentos pasados. En ese sentido, por lo tanto, este tipo de caso de uso no puede tener excepciones.

Sin embargo, el equipo todavía debe asegurarse de que el caso de uso es realmente un informe antes de enviarlo a diseño y codificación, porque podría ser una variación de ese patrón.

### 5.6.2 Expansión de CRUD
Al igual que los informes, los CRUDs también son casos de uso que siguen un patrón conocido. Este tipo de caso de uso consiste en la ejecución opcional de una de cada cuatro operaciones posibles: crear, recuperar, actualizar y eliminar.

Este tipo de caso de uso tiene un flujo principal con cuatro variantes, ya que ninguna de las operaciones puede considerarse un "happy path" o "excepción". Son operaciones distintas agrupadas más por conveniencia, por estar asociadas a la misma entidad, que por similitudes entre sus pasos. Por lo tanto, el flujo principal es sólo una decisión del usuario sobre qué operación se ejecutará. La Figura 5.18 presenta una posible plantilla para este tipo de caso de uso.


**Caso de Uso plantilla: <CRUD> Mantenimiento de ...**
1. El usuario elige: - Crear   
Variante 1a - Recuperar:   
Variante lb - Actualizar:   
Variante lc - Borrar: Identificador de variante   

Variante 1a: Crear   
la. I . El usuario proporciona ....   

Variante 1b: Recuperar   
1b.l. El usuario identifica/selecciona un....   
1b.2. El sistema presenta .... del elemento  identificado. 

Variante lc: Actualizar 
1c.I. Incluir la variante 1b: Recuperar.   
1c.2. El usuario proporciona nuevos valores para .... 

Variante 1d Borrar  
1d. I. El usuario identifica/selecciona un .... para ser eliminado.   
Excepción 1a. la: La inclusión viola la regla del negocio...   
1a.1a.1. El sistema informa que la regla .... impide la inclusión. la.  
1a.1a.2. Volver al paso 1a.1   
Excepción 1c.2a: La actualización viola las reglas del negocio ....   
1c.2a.1. El sistema informa de que la regla ....   impide la actualización.   
1c.2a.2. Volver al paso 1c.2.   
Excepción 1d.1a: Borrar deniega la regla de negocio o estructural....   
1d.1a.1: El sistema informa de que la regla ....   impide el borrado.   
1d.1a.2: Volver al paso 1d.1  

Figura 5.18 Una plantilla para un caso de uso ampliado de CRUD.

Observe que en ese caso, la variante 1c del modelo de caso de uso (Actualizar) incluye los pasos de la variante 1b (Recuperar).  

El gestor de excepciones 1d.1a utiliza una estrategia específica que consiste en evitar que el usuario borre un objeto cuando hay alguna regla que lo impida. En la Sección 8.5.4, se revisa este tema y se discuten otras estrategias para tratar esta excepción.

La Figura 5.19 presenta un ejemplo de expansión de un caso típico de uso de CRUD.


**Caso de Uso 13: `<<crud>>` Mantenimiento de Editores**
1. El gerente de adquisiciones elige: 
- Crear editor: Variante 1a
- Recuperar editor: Variante Ib 
- Actualizar editor: Variante Ic 
- Borrar editor: Variante 1d
  
Variante 1a: Crear editor   
1a.1 . El administrador de adquisiciones proporciona el nombre del editor, el código de identificación, la dirección y el correo electrónico. 

Variante 1b: Recuperar editor   
1b.1. El gestor de adquisiciones identifica a un editor.   
1b.2. El sistema presenta el nombre, código de identificación, dirección y correo electrónico del editor.   

Variante 1c: Actualizar editor   
1c.1. Incluir la variante 1b: Recuperar el editor   
1c.2. El gestor de adquisiciones proporciona nuevos valores para el nombre, el código de identificación, la dirección y el correo electrónico del editor.  

Variante 1d: Eliminar editor  
1d.1: El administrador de adquisiciones identifica al editor que se va a eliminar.   
Excepción ( 1a.1.1c.2)a: El código de identificación proporcionado ya existe.   
( 1 a.1,1c.2)a.1: El sistema informa al usuario de que ya existe un editor con el código de identificación proporcionado.   
( 1 a.1,1c.2)a.2: Volver al paso que causó la excepción.   

Excepción 1d.1a: Hay libros asociados al editor.   
1d.1a. I: El sistema informa al usuario de que no es posible eliminar un editor con libros asociados.   
1d.1a.2: Volver al paso 1d.1.    

Figura 5.19 Un ejemplo de un caso de uso ampliado de CRUD.

En este ejemplo, se utilizaron dos reglas de negocio para identificar las excepciones:
- El código de identificación de los editores debe ser único, que debe ser verificado tanto cuando se incluye una nueva instancia como cuando se actualiza una instancia. Esto produce excepciones en los pasos 1a.1 y 1c.2, que pueden identificarse como una única excepción (1a.1,1c.2)a.
- Si el editor ya tiene algún libro asociado (y esa asociación es obligatoria para los libros, es decir, cada libro debe estar vinculado a un editor), entonces no puede ser eliminado. Esta es una regla estructural que debe aparecer explícitamente en el modelo conceptual como un rol obligatorio de libro a editor (Sección 6.4.1).
  
La Figura 5.20 presenta el caso de uso de CRUD de Administrar clientes, que es una variación del patrón. Un cliente sólo puede recuperar y modificar sus propios datos. Por lo tanto, el caso de uso debe adaptarse a este hecho. Por otro lado, puede ser deseable que un administrador del sistema pueda acceder a los datos de cualquier cliente. Para ese administrador el caso de uso sería un CRUD regular. ¿Se crearían aquí dos casos de uso? Uno para que el cliente gestione sus propios datos y el otro para que el administrador del sistema gestione los datos de todos los usuarios? Quizás.... pero parece que este enfoque sería bastante repetitivo. Para empeorar aún más las cosas, imagínese que es posible que una gerente regional acceda a los datos de los usuarios sólo de su región. ¿Sería este un tercer caso de uso? Esto no parece una buena solución.


**Caso de uso 11:  `<<crud>>` Gestionar clientes**
1. El usuario elige: 
- Crear cliente: Variante 1a
- Recuperar al cliente: Variante 1b
- Actualizar cliente: Variante 1c
- Borrar cliente: Variante 1d
  
Variante 1a: Crear cliente   
1a.1. El usuario proporciona el nombre, la identificación, la dirección, el teléfono y el correo electrónico del cliente. 

Variante 1b: Recuperar cliente   
1b.I . El usuario identifica a un cliente.   
1b.2. El sistema presenta el nombre, la identificación, la dirección, el teléfono y el correo electrónico del cliente. 

Variante 1c: Actualizar cliente   
1c.1.  Incluya la variante 1b: Recuperar al cliente   
1c.2. El usuario proporciona nuevos valores para el nombre del cliente. Identificación, dirección, teléfono y correo electrónico.   

Variante 1d: Borrar cliente   
1d.1: El usuario identifica un cliente que debe borrarse. 

Excepción (1a.1,Ic.2)a: El ID ya existe.   
(1a.1.1c.2)a.1: El sistema informa al usuario de que ya existe un cliente con el ID dado.   
(1a.1,1c.2)a.2: Volver al paso que causó la excepción.   

Excepción (1b.1,1d.1)a: Acceso no autorizado.   
(1b.1,1d.1)a.1: El sistema informa al usuario de que se le niega el acceso.   
(1b.1.1d.1)a.2: Vuelva al paso que causó la excepción.   

Excepción 1d.1b: Hay pedidos asociados al cliente. 
1d.1b.1: El sistema informa al usuario que no es posible borrar a un cliente con pedidos asociados a él   
1d.1b.2: Volver al paso 1d.1. 

Figura 5.20 Un caso de uso CRUD ampliado con restricciones de acceso.

Para resolver este problema de una manera elegante, el caso de uso podría ser parametrizado, indicando que el usuario sólo puede acceder a los datos de los clientes que está autorizado a revisar. Cuando los clientes están siendo administrados, lo que debe ser verificado por una regla de negocio dada es si el usuario realmente tiene permiso para acceder o cambiar los datos del cliente al que está tratando de acceder o cambiar. En la Figura 5.20 se comprueba que el permiso es ejecutado por el manejador de excepciones (1b.1,1d.1)a: Acceso no autorizado.

Note que el caso de uso en la Figura 5.20 es una variación CRUD que podría llamarse CRUD con restricción de acceso, ya que el acceso a los datos depende de quién es el usuario. 

Existen otras variaciones del CRUD, tales como:
- CRUDL: Incluye una variante para listar los elementos existentes. Así, en lugar de simplemente identificar un objeto a recuperar, actualizar o eliminar, el usuario puede seleccionarlo de una lista.
- SCRUD: Incluye una variante para los elementos de búsqueda.
- RUD: Donde los elementos pueden ser recuperados, actualizados y eliminados, pero no creados.
- CRU: Donde los elementos pueden ser creados, recuperados y actualizados, pero no borrados.
  
Se pueden inventar muchas otras variaciones dependiendo de la necesidad y el costo/beneficio de tener más patrones que recordar.

Hay una manera más sencilla de definir un caso de uso basado en patrones si encaja perfectamente en el patrón. Consiste simplemente en listar el campo a rellenar y las reglas de negocio a respetar. Para el resto, se aplica el patrón. La figura 5.21 muestra un ejemplo.


**Caso de uso 12: Gestionar libros `<<crud>>`.**
Campos: 
- ISBN, título, autor, número de páginas, editorial, precio.
Reglas de inserción y actualización:
- El ISBN es único, es decir, los libros diferentes no pueden tener el mismo número de ISBN.
Reglas para borrar:
- Un libro que ha vendido copias no puede ser borrado. 
Figura 5.21 Ejemplo de una breve expansión para un caso de uso de CRUD.

Con la información dada en la Figura 5.21 y la plantilla de la Figura 5.18 es posible implementar el caso de uso sin expandirlo.

## 5.7 Otras secciones de un caso de uso ampliado
Desde que se creó el concepto de caso de uso (Jacobson, Christenson, Jonsson y Övergaard, 1992), se han propuesto diferentes formatos. Cada propuesta incluye elementos diferentes. Las secciones "flujo principal" y "flujos alternativos" son fundamentales para cualquier descripción detallada del caso de uso. Sin embargo, se pueden incluir otras secciones si el analista las necesita. Algunas de las más populares se presentan en las siguientes subsecciones.

### 5.7.1 Partes interesadas
A menudo existen escenarios en los que grupos que no son actores son relevantes para un caso de uso. Otros sectores de la empresa podrían tener algún interés en el caso de uso. Por ejemplo, en el caso de uso Order books el único actor es el cliente. Pero los resultados de ese caso de uso pueden interesar a los departamentos de existencias y contabilidad, porque los resultados de una venta pueden afectar tanto a la cantidad de libros en existencias como a la cantidad de dinero disponible o por recibir. Por lo tanto, incluso si esos departamentos no son participantes en el caso de uso, pueden ser incluidos en la lista de partes interesadas.

La utilidad de la lista de partes interesadas para un caso de uso es que el caso de uso debe satisfacer a todas las partes interesadas. Así, la documentación será útil para recordar al analista que busque información que necesite ser almacenada, procesada o transmitida, para que esos intereses puedan ser satisfechos.

### 5.7.2 Precondiciones
Por definición, las condiciones previas son hechos que se consideran ciertos antes de que se inicie un caso de uso. Las condiciones previas no deben confundirse con las excepciones: las excepciones sólo pueden detectarse después de que se haya iniciado el caso de uso. Las excepciones se detectan durante un caso de uso porque la mayoría de las veces no es posible verificar si las condiciones eran verdaderas o no antes de que comience el caso de uso. Por ejemplo, no es posible asegurar que el cliente tenga suficiente crédito para pagar el pedido antes de iniciar el caso de uso de los libros de pedidos, ya que el valor del pedido no se puede conocer en ese momento; por lo tanto, se trata de una excepción. Sin embargo, es posible admitir que sólo un libro que fue vendido y entregado puede ser devuelto. Por lo tanto, la venta y entrega del libro es una condición previa para su devolución.

Dado que las condiciones previas se aceptan como hechos reales antes de que comience el caso de uso, no se comprobarán durante el caso de uso. Aunque puede haber otras interpretaciones en la literatura, este tipo de condiciones previas no generan excepciones. Si son falsos, debería ser imposible iniciar el caso de uso (de lo contrario son excepciones, no condiciones previas).

### 5.7.3 Post-conditiones de éxito.
Las condiciones de éxito posteriores establecen los resultados de un caso de uso, es decir, lo que será cierto después de que se ejecute el caso de uso. Por ejemplo, el caso de uso de los libros de pedidos puede tener como condición posterior el siguiente resultado: "La orden fue registrada por el sistema."

### 5.7.4 Cuestiones pendientes
A veces, sin la presencia del cliente, el equipo no puede decidir sobre algún tema que pueda depender de las políticas de la empresa. Por ejemplo, ¿puede el cliente pagar el pedido a plazos? ¿Existen ofertas especiales para los clientes que compran más de ciertas cantidades?

Si el cliente no está disponible inmediatamente, estas dudas deben ser registradas en la sección de casos de uso "cuestiones abiertas" para poder ser resueltas lo antes posible.

Al final de las actividades de análisis de una iteración se espera que todas las cuestiones pendientes hayan sido resueltas e incorporadas a la descripción del caso de uso.

## 5.8 Diagramas de secuencia del sistema
Entre otros usos, el texto de los casos de uso expandido puede ser utilizado como:

- Una fuente de información para descubrir los conceptos y atributos para refinar el modelo conceptual (Sección 6.8).
- Una fuente de información para descubrir las operaciones del sistema, que consiste en los métodos que encapsulan la capa de dominio del sistema a partir de la interfaz (Capítulo 8).
Hay dos tipos de operaciones del sistema:
- Comandos del sistema, que cambian los datos y no deben devolverlos.
- Consultas del sistema, que devuelven datos y no deben modificarlos.
  
Esto sigue el principio de Separación Comand-Query o CQS de la ingeniería de software (Meyer, 1988), que permite una mejor reutilización y mantenimiento del código. Una consulta que cambie los datos sería menos cohesiva que una consulta sin efecto colateral y un comando sin retorno.

Los comandos del sistema son métodos que se activan por un evento del sistema, es decir, como reacción a una acción del usuario. Los comandos del sistema, por definición, implementan un flujo de información desde el exterior hacia el interior del sistema. Por lo tanto, los comandos del sistema actualizan la información que gestiona el sistema.
Las consultas del sistema son métodos que corresponden a la simple verificación de la información ya almacenada. Esa información puede ser presentada exactamente como existe o modificada por operaciones lógicas y matemáticas (como la suma, el promedio, etc.). Por definición, una consulta del sistema no puede ser responsable de la inserción de nueva información en el sistema. Tampoco debería ser responsable de actualizar o eliminar información del sistema: sólo puede leer información.

El conjunto de operaciones del sistema corresponde a la funcionalidad total de un sistema, es decir, al conjunto de todas las funciones que puede realizar un usuario con el sistema.

Los casos de uso son excelentes fuentes para descubrir las operaciones del sistema. Los comandos del sistema se asocian básicamente a pasos en los que el usuario envía alguna información al sistema (los marcados con [IN]). Las consultas del sistema se asocian para utilizar pasos de caso en los que el sistema envía información a los actores (los marcados con [OUT]).

### 5.8.1 Elementos de un diagrama de secuencia
Uno de los diagramas UML que puede ser particularmente útil para representar la secuencia de eventos y retornos del sistema en un caso de uso es el diagrama de secuencia. Cuando se utiliza un diagrama de secuencias para representar un caso de uso, puede llamarse diagrama de secuencia del sistema (Larman, 2004). El diagrama de secuencia tiene elementos que son instancias de actores y otros componentes del sistema. En la primera versión del diagrama de secuencia del sistema sólo están representados los actores y la interfaz del sistema (o nivel de aplicación) (Figura 5.22).

Figura 5.22 Diagrama de secuencia del sistema.

Las actividades relacionadas con el análisis de casos de uso todavía no tratan con objetos que son internos al sistema. Por lo tanto, el sistema debe representarse como un único objeto: una caja negra. 

En este caso, puede representarse con el símbolo de interfaz, tal y como proponen Jacobson y otros (1992). Un actor sólo puede comunicarse con un sistema a través de su interfaz. Los mensajes del actor no pueden llegar a los objetos, como se muestra en la Figura 5.23.

Figura 5.23 Un ejemplo de un diagrama de secuencia de sistema inadecuado, en el que los actores se comunican directamente con los objetos..

Los actores, interfaces y otros elementos del diagrama de secuencia tienen una línea de vida, representada por una línea vertical, donde pueden ocurrir eventos. Cuando la línea está discontinua, el actor o sistema está inactivo. Cuando la línea es sólida, el elemento está activo (procesando o esperando el resultado de una operación realizada por otro elemento). Los actores humanos siempre se consideran activos.

Las flechas horizontales representan el flujo de información. Hay tres tipos de flujos de información en ese diagrama:
- Entre actores: La comunicación de los actores entre sí, correspondiente a los pasos complementarios del caso de uso expandido.
- De los actores al sistema: Corresponde a eventos del sistema, es decir, pasos que podrían marcarse con [IN] en casos de uso ampliado.
- Del sistema a los actores: Corresponde a las devoluciones del sistema, es decir, a los pasos que se pueden marcar con [OUT] en los casos de uso ampliado.
  
El intercambio de información entre actores no pertenece al ámbito del sistema, pero puede ser útil para ilustrar cómo se intercambia la información de actor a actor hasta llegar al sistema.

Una cosa a tener en cuenta cuando se construyen estos diagramas es que la información no se crea durante el proceso; sólo se transfiere de los actores al sistema y viceversa. El actor generalmente tiene alguna información que debe ser pasada al sistema para poder realizar un proceso. Para procesar un pedido de libros, el cliente debe informar al sistema quién es y qué libros desea. Al principio, el cliente es el único que tiene esa información; el sistema tiene el registro de todos los clientes y libros, pero no puede saber quién es ese cliente específico hasta que alguien le proporcione esa información.

El diagrama de secuencia puede construirse para el flujo principal de un caso de uso y completarse con flujos alternativos. Opcionalmente, se pueden construir diferentes diagramas de secuencia para cada flujo. Sin embargo, lo más importante en este momento es saber qué información se intercambia entre los actores y el sistema. El analista debe construir un catálogo con todos los comandos y consultas del sistema (que se explican en las secciones siguientes) identificados en los flujos principal y alternativo del caso de uso. Esta información se utilizará más adelante para definir restricciones que indiquen cómo el sistema recupera y transforma la información (Capítulo 8).

### 5.8.2 Casos de uso ampliados como diagramas de secuencia del sistema
El diagrama de secuencia del sistema es una herramienta para lograr descripciones de casos de uso más formales y detalladas. Adicionalmente, el desarrollo del diagrama de secuencia del sistema hace la conexión entre el análisis de requerimientos (el caso de uso expandido) y el diseño del software (las operaciones del sistema que serán implementadas).

La construcción del diagrama de secuencia del sistema puede realizarse en dos etapas:
1. Representar los pasos del caso de uso como intercambio de información entre los actores y la interfaz del sistema.
2. Representar las operaciones del sistema como métodos de llamada entre la interfaz y el controlador-fachada,7 que encapsula la capa de dominio del sistema.
   
El primer paso es simple: para cada entrada de caso de uso (un paso que se podría marcar con [IN]), hay un evento de sistema equivalente en el que un actor envía información a la interfaz, y para cada salida de caso de uso (un paso que se podría marcar con [OUT]), hay un retorno de sistema equivalente en el que un actor recibe información del sistema.
 (Figuras 5.24 y 5.25).


**Caso de uso 01: Pedir Libros**
1. El cliente proporciona palabras clave para la búsqueda de libros.
2. El sistema genera una lista de libros a la venta que coincide con las palabras clave, incluyendo al menos título, autor, precio, número de páginas, editorial, ISBN e imagen de portada. 
3. El cliente selecciona los libros de la lista e indica la cantidad deseada para cada uno. 
4. El sistema genera el resumen de la orden (título, autor, cantidad, precio unitario y subtotal para cada libro) y el valor total. 
5. El cliente finaliza el pedido. 
Variante 5d: El cliente decide seguir comprando. 
5d.1. Vuelva al paso 1. 
Figura 5.24 Un caso de uso de referencia.


Figura 5.25 La representación del flujo principal de un caso de uso como diagrama de secuencia del sistema.

Nótese que entre los actores y la interfaz los flujos consisten en enviar y recibir información. La información puede ser enviada por un actor, por ejemplo, escribiéndola en un formulario. La información puede ser recibida por un actor cuando se imprime en la pantalla, por ejemplo. En este nivel, los flujos no son métodos de llamada porque los actores no son objetos internos.

Las palabras o frases utilizadas en los flujos de los diagramas de secuencia para representar información son a veces una fuente de confusión y malentendidos. Para evitar tal confusión, se recomienda un patrón de etiquetado:
- La información simple (datos alfanuméricos) está representada por una o más palabras. Por ejemplo, keyword (paso 1 de la figura 5.25), cantidad (paso 3) y total (paso 5).
- La información compleja puede representarse entre "<" y ">" en el diagrama si está compuesta por unos pocos elementos (2 ó 3). Por ejemplo, <libro seleccionado, cantidad> (paso 3).
- La información compleja compuesta de numerosos elementos (más de 3) puede representarse en un diccionario de notas o de datos separado.8 En el diagrama sólo se utiliza el nombre del concepto complejo. Por ejemplo, libro (paso 2) e item (paso 4).
- Un conjunto de valores se indica con el sufijo "*". Por ejemplo, keyword* (paso 1), libro* (paso 2), <libro seleccionado, cantidad>* (paso 3) e item* (paso 4).
- Cuando se selecciona un objeto de una lista presentada por el sistema, la selección se indica con la palabra "seleccionado", como en el paso 3, donde "libro seleccionado" representa un libro que fue seleccionado del libro listado presentado en el paso 2.
Algunas otras consideraciones en el diagrama pueden seguir:
- En el paso 1, el equipo podría optar por utilizar palabras clave en lugar de palabras clave*. Sin embargo, en este caso, el hecho de que la información que se envía sea una lista de palabras no seguiría la notación propuesta.
- La información contenida en un libro es probablemente un subconjunto de los atributos de la clase Book del modelo conceptual; no necesariamente corresponde al conjunto completo de atributos de la clase Book.
- En el paso 3, cuando el usuario informa al sistema sobre la lista de libros que ha seleccionado, no es necesariamente la información completa sobre un libro que está siendo enviado por el usuario al sistema. Tecnológicamente hablando, el usuario sólo tiene que seleccionar un libro de una lista y la interfaz envía al sistema el identificador correcto para el libro seleccionado (el usuario ni siquiera tiene que saber qué identificador es).
- En el paso 4, se creó un ítem para representar diferentes aspectos de un libro: en lugar de recuento de páginas, editor, ISBN e imagen de portada, un ítem presenta la cantidad (que no es un atributo de un libro) y el subtotal (que se calcula a partir del precio y la cantidad).
- El paso 5 no representa la información alfanumérica que se está enviando o recibiendo como en los pasos anteriores. La orden de acabado es un paso de control. Sólo informa al sistema de que el estado de la orden ha cambiado sin pasar por ninguna otra información alfanumérica nueva.
- La variante 5d es una opción entre terminar el pedido o reanudar las compras. Está representado por el fragmento de bucle que incluye los pasos 1 a 4.

### 5.8.3 Conexión de la interfaz al controlador-fachada
Los eventos del sistema son acciones que un usuario realiza a través de la interfaz del sistema. Cuando se utiliza una interfaz web, por ejemplo, estas acciones consisten en rellenar formularios, pulsar botones, etc. Estas no son operaciones en el sentido de lenguajes de programación, es decir, estos flujos de un actor al sistema y viceversa no representan la llamada a métodos.

Sin embargo, los comandos y consultas del sistema son procedimientos computacionales que son necesarios para implementar eventos del sistema y devoluciones del sistema, respectivamente. Los comandos y consultas del sistema se activan mediante mensajes que se envían desde la interfaz al controlador-fachada. Ahora, tenemos un componente del sistema que invoca a otro componente del sistema. En este caso, es la interfaz la que envía un mensaje, pidiendo al controlador-fachada que realice un método que consista en un comando o consulta. El conjunto de todos los mensajes posibles es equivalente a toda la funcionalidad del sistema: todo el acceso y actualización de la lógica de datos se realiza mediante comandos y consultas del sistema.

Por lo tanto, cuatro tipos de flechas son de interés en los diagramas de secuencia del sistema:
- Evento del sistema: Como se muestra en la Figura 5.26, se trata de una acción realizada por un actor que envía alguna información al sistema. En el diagrama, está representado por una flecha desde el actor hasta la interfaz.
- Retorno del sistema: Como se muestra en la Figura 5.27, se trata de un flujo de información del sistema a un actor, representado en el diagrama como una flecha de la interfaz al actor.
- Comando del sistema: Como se muestra en la Figura 5.28, este es un mensaje que se envía desde la interfaz al controlador, generalmente en respuesta a un evento del sistema. El comando sistema debe, por definición, cambiar alguna información almacenada o gestionada por el sistema. En el diagrama, esto se representa mediante una flecha de la interfaz al controlador etiquetada con un mensaje (siempre se recomienda el uso de paréntesis para distinguirla de los flujos de información, como los eventos del sistema y los retornos).
- Consulta del sistema: Como se ve en la Figura 5.29, este es un mensaje que se envía desde la interfaz al controlador para obtener alguna información del sistema. Las consultas no deben cambiar los datos; sólo devuelven datos. En el diagrama, las consultas se representan con flechas desde la interfaz hasta el controlador etiquetadas con un mensaje con un valor de retorno explícito.



Figura 5.26 Evento de sistema.


Figura 5.27 Retorno del sistema.


Figura 5.28 Comando al sistema.


Figura 5.29 Consulta al sistema.

Los resultados de la consulta también pueden representarse mediante líneas discontinuas desde el controlador hasta la interfaz, como se muestra en la Figura 5.30. Ambas representaciones están permitidas y el equipo puede elegir una u otra. El enfoque de la Figura 5.29 crea menos flechas en el diagrama, pero puede ser complicado si la consulta debe devolver datos complejos. Este problema puede minimizarse si se utilizan notas como las de la Figura 5.25 para definir datos complejos. Otros analistas preferirían el enfoque de la Figura 5.30, que hace que el retorno aparezca explícitamente como una flecha en el diagrama. La desventaja de este enfoque es que divide una sola llamada de consulta en dos flechas.



Figura 5.30 Representación alternativa de una consulta del sistema.

La comunicación entre actores puede representarse en el diagrama de secuencia del sistema como flechas de un actor a otro. Sin embargo, como se ha explicado anteriormente, estas comunicaciones no afectan a la aplicación del sistema.

La capa de dominio de una aplicación (la parte del sistema que contiene todas las clases que realizan las operaciones lógicas sobre los datos) está encapsulado por su controlador-fachada, que es una instancia de una clase que implementa todos los comandos y consultas del sistema a los que debe accederse mediante una determinada interfaz o conjunto de interfaces. Hay al menos tres sub-patrones para el controlador-fachada. La primera, para sistemas más pequeños, consiste en implementar un único controlador para todo el sistema. Sin embargo, esto resultaría en un gran número de operaciones implementadas en una sola clase. Una solución a esto es dividirlo en controladores de casos de uso, es decir, una clase de controlador diferente para cada caso de uso. Sin embargo, esta no es una buena solución cuando diferentes casos de uso llaman a los mismos métodos, los cuales deben ser implementados en diferentes clases. La solución más adecuada para la mayoría de los sistemas medianos o grandes es implementar controladores de componentes o subsistemas, es decir, controladores que encapsulan la funcionalidad de los subsistemas o componentes definidos por la arquitectura del sistema.

El diseño de los mensajes entre la interfaz y el controlador se realiza después de un examen de los eventos del sistema y regresa utilizando las siguientes reglas:
- Un evento del sistema que envía datos al sistema que deben ser almacenados, actualizados o borrados, es decir, datos que causan un cambio en el estado interno del sistema, requiere al menos un comando del sistema (Figura 5.31).
- Un retorno de sistema que envía datos del sistema al usuario requiere al menos una consulta del sistema, de modo que los datos puedan obtenerse del controlador para ser presentados por la interfaz (Figura 5.32).
- Una secuencia de evento y retorno del sistema, donde el evento sólo proporciona argumentos para producir el retorno, requiere una consulta del sistema donde la información recibida del evento del sistema son los argumentos (Figura 5.33).

Figura 5.31 A evento del sistema que requiere un comando del sistema.

Figura 5.32 Una devolución del sistema que requiere una consulta del sistema.

Figura 5.33 Una secuencia de evento de sistema y retorno de sistema que requiere una consulta de sistema cuando el evento acaba de pasar sus argumentos.

La relación causa/efecto entre eventos y comandos y entre retornos y consultas no siempre es tan directa. A veces, una consulta puede usar argumentos que fueron pasados a la interfaz muchos pasos antes, o la información pasada por el actor a la interfaz puede ser utilizada muchas veces por diferentes comandos y consultas del sistema.

Estas reglas para derivar consultas y comandos de retornos y eventos son sólo una primera aproximación para diseñar la capa de interfaz. Posteriormente, las técnicas de modelado y las decisiones de diseño pueden cambiar la forma en que se invocan estos comandos y consultas.

### 5.8.4 Estrategia sin Estado
Cuando se está desarrollando el diagrama de secuencia del sistema, cada pieza de información se pasa una vez del actor al sistema. Sin embargo, en el siguiente nivel, entre la interfaz y el controlador, muchos comandos y consultas diferentes pueden necesitar los mismos argumentos. Por ejemplo, el ID de cliente puede ser necesario para realizar muchas operaciones posteriores. En este punto, el diseñador debe decidir si el controlador debe tener memoria transitoria para almacenar estos argumentos (estrategia de estado) o si no está provisto de memoria (estrategia sin estado). En la estrategia sin estado cada vez que una consulta o comando del sistema necesita un argumento tiene que recibirlo explícitamente desde la interfaz.

La Figura 5.34 muestra cómo se vería el diagrama de secuencia del sistema para el caso de uso Pedir Libros con una estrategia sin estado. La información se pasa del actor a la interfaz sólo una vez, pero cada vez que un comando o consulta del sistema necesita esa información, la interfaz debe enviarla de nuevo como argumento al controlador. Observe que cartId pasa por la interfaz al controlador tres veces: cuando se llama a add2Cart, getCartSummary y finishOrder.

Figura 5.34 Diagrama de secuencia del sistema para el flujo principal de casos de uso Pedir Libros utilizando una estrategia sin estado.

A partir de este punto se puede ver que el equipo está haciendo una transición del análisis al diseño, porque las decisiones de diseño deben ser tomadas para acomodarse a los requerimientos. Por ejemplo, el hecho de que un usuario deba identificarse sólo cuando la orden está terminada impide que el sistema cree una orden antes de ese momento (si la orden es realmente un concepto que debe asociarse a un cliente).  

Por lo tanto, se crea una cesta de la compra en lugar de un pedido en la inicialización de ese diagrama secuencial. La orden se creará sólo cuando el usuario decida dejar de comprar (finalizar la orden). En ese momento, si el usuario no está identificado, se plantearía una excepción, como se explicará más adelante. El punto a tener en cuenta es que como el controlador no tiene memoria transitoria, no registra la información de quién está comprando. Es la interfaz la que contiene la identificación del cliente en este punto. Cuando el pedido está listo para ser completado, la interfaz envía al controlador los IDs del cliente y del carro de la compra (recuerde que el carro de la compra todavía no está asociado a ningún cliente).

Como el controlador no tiene estado (memoria transitoria), cada operación enviada a él que se refiera al carro de la compra debe referirse a su número (cartId). ¿Por qué se utiliza el ID del carro y no el objeto del carro en sí? ¿No estamos haciendo diseño orientado a objetos? El hecho es que los objetos de dominio son encapsulados por el controlador. Esto significa que la interfaz no debería tener acceso directo a los objetos de dominio. Por este motivo, la interfaz envía un ID como parámetro en lugar del propio objeto de carro.

Hay que hacer una observación sobre el comando createShoppingCart: a medida que crea un nuevo objeto de dominio y devuelve su código de identificación, uno podría preguntarse si esto no va en contra del principio de separación comando-consulta. No lo es. 

Es una de las excepciones aceptables a ese principio, porque el comando sólo crea un nuevo objeto y devuelve su código de identificación. Puede hacerse porque intentar obtener el código de un objeto recién creado por otros medios sería contraproducente.

### 5.8.5 Estrategia de Estado completo
Cuando el controlador puede tener memoria transitoria para mantener los parámetros de trabajo durante la ejecución de un caso de uso, entonces estamos usando la estrategia de estado. Así, después de que un argumento es enviado al controlador por una operación, las operaciones subsiguientes no necesitarán recibir el argumento de nuevo; el controlador lo mantendrá en la memoria local.

Sin embargo, este argumento no es necesariamente información persistente; la información transitoria no se almacena en una base de datos u otra estructura equivalente. Consiste únicamente en información transitoria (por ejemplo, quién es el cliente actual, qué cesta de la compra se está utilizando, etc.), que sólo está disponible durante la transacción de caso de uso. La Figura 5.35 presenta el mismo caso de uso que el mostrado en la Figura 5.34, pero esta vez con el enfoque de estado. Se puede observar que, entre otras cosas, no es necesario devolver la nueva identificación del carro de la compra, ya que el controlador recordará cuál es.

Figura 5.35 Diagrama de secuencia del sistema para el flujo principal de casos de uso.

Con la estrategia de estado no es necesario devolver la referencia al nuevo carro de la compra porque el controlador tiene un mecanismo interno para almacenar ese valor. De la misma manera, los métodos add2Cart, getCartSummary y finishOrder tampoco necesitan recibir ese argumento. Es mantenido por el controlador. De la misma manera, la identidad del cliente, si se conoce, es mantenida por el controlador, no por la interfaz.

Una opción para implementar esta memoria transitoria es utilizar asociaciones transitorias, como se explica en la Sección 8.3. Es una decisión arquitectónica elegir uno u otro enfoque. Algunos de sus pros y contras son los siguientes:

- La estrategia de estado exige la implementación de un mecanismo de memoria transitorio (no persistente) para almacenar algunos parámetros (el uso de asociaciones transitorias, por ejemplo). La estrategia sin estado no exige ese tipo de mecanismo.
- La estrategia sin estado exige un mayor paso de parámetros entre la interfaz y el controlador. Cuando se trata de pasar información a través de la red, esto puede ser un inconveniente. Con la estrategia de estado la información se transmite una sola vez.
  
Adicionalmente, se puede decir que las operaciones son más reutilizables con la estrategia sin estado, ya que cada una de ellas recibe todos los parámetros que necesita, sin depender de las operaciones que antes se realizaban. Además, la estrategia sin estado escala mejor que la de con estado. Los sistemas con muchos usuarios simultáneos serían más fáciles de producir y mantener con una estrategia sin estado.


### 5.8.6 Flujos alternativos en los diagramas de secuencia del sistema
Como se ha visto al principio de este capítulo, los pasos del caso de uso, especialmente los eventos del sistema, pueden tener excepciones, que son manejadas por un flujo alternativo.

La inserción de esos flujos alternativos en un diagrama de secuencia del sistema puede hacerse por etapas. Inicialmente, las excepciones se pueden indicar en el diagrama, así como el lugar donde ocurren. Entonces se pueden producir fragmentos opt, es decir, piezas opcionales, como se muestra en la figura 5.36. El procedimiento es tomar el caso de uso completo como se muestra en la Figura 5.7 y agregar cada excepción como un fragmento de opción en la posición adecuada del flujo (usualmente justo después del paso que podría causar la excepción).

Figura 5.36 Diagrama de secuencia con excepciones incluidas.

El diagrama de la Figura 5.36 muestra literalmente que después del paso 3 y después del paso 5 pueden ocurrir eventos opcionales. Estos eventos corresponden a las excepciones 3a, 5a, 5b y 6c que se muestran en la Figura 5.7.

Ahora, es necesario diseñar lo que sucede dentro de los fragmentos opcionales cuando se maneja cada excepción. El fragmento opt contiene los pasos del flujo alternativo, pero también es importante observar cuidadosamente la terminación del flujo alternativo. Algunos de los movimientos alternativos vuelven al paso que generó la excepción y deben tratarse como ciclos repetitivos que incluyen el paso que causó la excepción. Otros avanzan al siguiente paso, y deben ser tratados como un fragmento opcional del diagrama. Cuando se hace referencia a otros casos de uso o cuando un fragmento es tan largo que justifica su definición en un diagrama separado, entonces se puede utilizar el fragmento de referencia, lo que indica que se está llamando a otro diagrama de secuencia. El fragmento de referencia puede recibir y devolver información de la misma manera que una función de programación, y usando la misma notación, como por ejemplo, ref otherDiagram(arguments):result.

Ahora el diagrama de la Figura 5.36 va a ser mejorado con el manejo de excepciones. Esto puede convertirse en una tarea compleja a menos que algunas decisiones de diseño se tomen con cuidado. Por ejemplo, en el paso 3, se envía al sistema un set de libros y las cantidades respectivas y sólo entonces se verifican las cantidades. Esto requeriría el manejo de una excepción cuando algunos libros se piden por encima del stock y otros no, lo que podría ser inconveniente. Por lo tanto, se decidió modificar el diagrama secuencial para que la excepción se verificara cada vez que se proporcionara una cantidad. Note que esta decisión cambia un poco la forma en que el usuario percibe el comportamiento del sistema: en lugar de quejarse de las cantidades al final de la selección, el sistema verificaría la cantidad después de cada elección de libro. El diagrama resultante se muestra en la Figura 5.37, donde sólo se representan los tres primeros pasos del caso de uso para simplificar.

Figura 5.37 Parte del diagrama de secuencia del sistema con un cambio de diseño y un gestor de excepciones.

Obsérvese en la figura 5.37 que el diseño podría mejorarse de nuevo. ¿Por qué intentar realizar un comando con una cantidad que está por encima del stock si el sistema ya conoce esa información? La información sobre el stock puede ser devuelta por la consulta searchBook, de modo que el campo de entrada de la interfaz ya puede estar limitado a la cantidad real disponible. Esa información también podría ser utilizada por la interfaz para mostrar libros que están en el catálogo pero que no están en stock como agotados. La figura 5.38 muestra el diseño resultante.

Figura 5.38 Parte del diagrama de secuencia del sistema donde se rediseñó un gestor de excepciones.

Observe que en la Figura 5.38 el fragmento que maneja la excepción simplemente desaparece. Esto sucedió porque la excepción se convirtió en una condición previa para el comando de sistema add2Cart. Esta es una técnica popular para mejorar el diseño que se revisará en el Capítulo 8. La técnica consiste en evitar que el usuario envíe un argumento inválido; la elección del usuario se limita a los valores válidos.

 Por lo tanto, la excepción no puede volver a ocurrir.
Las excepciones 5a y 5b pueden resolverse conjuntamente, ya que implican la identificación del usuario. Cuando se ejecuta el comando finishOrder, se produce una excepción si el usuario aún no está identificado. El usuario tiene dos opciones: introducir una identificación válida o crear una nueva. El diagrama parcial se muestra en la figura 5.39.

Figura 5.39 Identificación de usuarios.

Como se ve en la Figura 5.39, no es necesario probar el comando finishOrder para descubrir que el usuario aún no está identificado. La condición puede ser probada después de que el usuario decida terminar la orden pero antes de probar el comando. Así, si el usuario no está identificado, tiene dos opciones, representadas dentro del fragmento de alteración. El fragmento alt funciona como un if-then-else: si el usuario tiene una cuenta, entonces se conecta, en otro caso tiene que crear una nueva cuenta. En ambos casos, como esas secuencias pueden ser altamente reutilizables, se indica una referencia a otro diagrama de secuencia mediante la referencia del fragmento.

Por último, la excepción 5c establece que si no se seleccionó ningún libro, la orden no puede cerrarse.
 Esto puede ser implementado como un fragmento de bucle colocado sobre los flujos de 1 a 4 (excluyendo el flujo 5) que se repetiría hasta que se seleccione al menos un libro. Como ya existe un bucle de este tipo en el diagrama (véase la figura 5.37), basta con añadir esa condición al bucle existente. El diagrama de secuencia completo con todas las excepciones manejadas se muestra en la Figura 5.40.

Figura 5.40 Diagrama de secuencia completo con las excepciones manejadas.

El principal resultado práctico del diagrama de secuencia del sistema es el descubrimiento y diseño de los comandos y consultas del sistema que deben implementarse para permitir que la funcionalidad del sistema esté disponible para los usuarios. De acuerdo con la Figura 5.40, estos comandos y consultas son:
- createShoppingCart().
- searchBook(palabra clave*):libro*.
- add2Cart(libro seleccionado, cantidad).
- getCartSummary ():<item*, total>.
- finishOrder().  
  
Más adelante muestra cómo utilizar esta información para construir un conjunto de restricciones que definan toda la funcionalidad del sistema.

## 5.9 El proceso visto hasta ahora


| | Inicio | Elaboración | Construcción | Transición |
| -- | -- | -- | -- | -- |
| **M**odelado del Negocio | [MI](#MI) | | | | 
| **R**equerimientos | [RI](#RI) | | | | 
| **A**nalisis y Diseño | [ADI](#ADI)  | | | | 
| **I**mplementación  | | | | |
| **P**ruebas/Test  | | | | | 
| **G**estión de Proyectos  | [GPI](#GPI) | | | |
| **D**espliegue  | | | | |
| **C**onfiguración y Gestión del cambio | | | | |
| **E**ntorno | | | | |

### MI
Construir una vista general del sistema:  
- Dibujar un caso de uso del negocio y determinar el ámbito de automatización para el proyecto.
- Dibujar un diagrama de actividad para el caso de uso del negocio
- Dibujar un diagrama de maquina de estado para los procesos clave del sistema


### RI
Preparar un diagrama de caso de uso del sistema (requisitos funcionales)
- Identificar los actores del sistema desde el modelo de caso de uso del negocio.
- Identificar los casos de uso del sistema desde  el modelo de caso de uso del negocio, y el diagrama de actividad y maquinas de estado desde el modelo de negocio.

Identificar los requisitos no funcionales como anotaciones de los casos de uso:
- Identificar las principales reglas de negocio asociadas a los casos de uso.
- Identificar las principales puntos de calidad asociados a los casos de uso.

Identificar requisitos suplementarios.  
Detalle de requisitos ampliando los casos de uso: 
- Identificar el flujo principal. 
- Identificar flujos alternativos: variantes y manejadores de excepciones. 
  
### ADI
Preparar un modelo conceptual preliminar observando los casos de uso del sistema y los conceptos expresados en el.  

Elaborar los diagramas de secuencia del sistema: 
 - Representar el flujo principal de un caso de uso como un diagrama de secuencia del sistema. 
- Representar los comandos y consultas del sistema utilizando estrategias de estado o sin estado. 
- Completar los diagramas de secuencia del sistema con flujos alternativos. 
  

### GPI
Estimar el esfuerzo total, el cronograma ideal y el tamaño medio del equipo para el proyecto.   

Estimar la duración y el número de iteraciones para cada fase.  

Preparar la fase de planificación y el plan de Iteración para la primera iteración.



## 5.10 Preguntas
1. Las variantes y los gestores de excepciones son movimientos alternativos para un caso de uso. ¿En qué situaciones se debe utilizar una u otra?
2. ¿Cuál es la diferencia entre un caso de uso esencial y un caso de uso real? ¿Por qué el caso de uso esencial es más interesante a efectos de requisitos?
3. Explique las diferencias entre los pasos de caso de uso obligatorio, complementario e inadecuado.
4. Expandir el flujo principal del caso 03, Entregar orden, presentado en la Figura 3.10.
5. Finalizar la expansión del caso de uso de la Figura 5.2 indicando sus flujos alternativos.
6. Diseñar el diagrama de secuencia del sistema para el flujo principal del caso de uso de la Figura 5.2, eligiendo una de las siguientes estrategias: sin estado o con estado. Después de diseñar el diagrama del flujo principal, añada los flujos alternativos identificados en la Pregunta 5.

