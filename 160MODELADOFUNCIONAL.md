# MODELADO FUNCIONAL con restricciones OCL

        ​ Modelado funcional con restricciones OCL

Se deben implementar los comandos y consultas identificados en el diagrama de secuencia del sistema. Las contratos son especificaciones de alto nivel para esas operaciones. Pueden estar escritos en lenguaje natural o en un lenguaje formal como el OCL. Este capítulo presenta una disciplina de escritura para restricciones OCL que evita interpretaciones ambiguas y que es relativamente fácil de leer y escribir. Las restricciones se componen de condiciones previas, condiciones posteriores, excepciones y valores de retorno. Se presentan restricciones para CRUDs así como restricciones para otras operaciones que se encuentran en los diagramas de secuencia del sistema.

                ​ Palabras clave
System operation contract; precondition; postcondition; exception; formal specification; OCL; Object Constraint Language

            ​ Conceptos en este Capítulo

    • Condiciones previas
    • Devolución de consultas
    • Postcondiciones
    • Excepciones
    • Restricciones/contratos de explotación del sistema

            ​ 8.1 Introducción al modelado funcional
Antes del modelado funcional, el proceso de análisis en la fase de elaboración produce dos artefactos importantes:
    • El modelo conceptual refinado (Capítulos 6 y 7), que representa estáticamente la información gestionada por el sistema.
    • Los casos de uso ampliado o diagramas de secuencia del sistema (Capítulo 5), que muestran cómo los usuarios potenciales intercambian información con el sistema, sin mencionar cómo el sistema procesa esa información internamente y sin mencionar la tecnología de la interfaz.
Cuando se construyen los diagramas de secuencia del sistema, se identifican los comandos y consultas del sistema que deben implementarse. Cada comando y consulta del sistema implica una intención u objetivo del usuario; por ejemplo, el usuario puede estar proporcionando información sobre los libros que tiene intención de comprar, o puede estar preguntando cuánto cuesta un libro. Esa intención se refleja en las restricciones de comando del sistema y las restricciones de consulta del sistema, denominados genéricamente contratos de operación del sistema, que incorporan el modelo funcional del sistema.
Una contrato de comando de sistema puede tener tres secciones:
    • Condiciones previas (opcional): Establece lo que se supone que es verdad por el comando y por lo tanto no debe ser comprobado por él.
    • Postcondiciones (obligatorio): Indica cómo el comando cambia la información existente si se ejecuta correctamente.
    • Excepciones (opcional): Establece las condiciones que podrían impedir que el comando tenga éxito.
Por otra parte, un contrato de consulta del sistema puede tener las siguientes secciones:
    • Condiciones previas (opcional): Establece lo que se supone que es cierto en la consulta y, por lo tanto, no debe ser comprobado por ella.
    • Resultados (obligatorio): Define la información que devuelve la consulta.
    • Excepciones (opcional): Indica las condiciones que fueron añadidas por el diseñador para evitar que el sistema realice la consulta en algunas situaciones.
Existen condiciones previas en ambos tipos de restricciones. Definen limitaciones complementarias a las ya existentes en el modelo conceptual. Se supone que las condiciones previas son ciertas para la operación. Esto significa que las condiciones previas no son probadas por la operación definida por la restricción; deben ser probadas y aseguradas antes de que se realice la operación.
Las condiciones posteriores sólo existen en las restricciones de comandos del sistema porque especifican cómo se modifica la información guardada por el sistema. Se debe tener especial cuidado para no confundir las condiciones posteriores con los resultados de la consulta. Por el principio de Separación Comando-Consulta (Meyer, 1988) no es apropiado que un comando devuelva ningún resultado (excepto en casos especiales justificados). Las consultas, por otro lado, deben devolver algún resultado, pero no pueden producir ningún cambio en la información existente. Por lo tanto, las consultas del sistema deben tener resultados y los comandos del sistema deben tener condiciones posteriores.
A diferencia de las condiciones previas que deben ser ciertas antes de que se llame a la operación, las excepciones son situaciones que normalmente no pueden o no deben probarse antes; las excepciones son probadas por la propia operación. Las excepciones son eventos que, si se producen, impiden que la operación tenga éxito.
Las excepciones en las restricciones de comando y las excepciones en las restricciones de consulta pueden tener propósitos distintos. En las restricciones de comando, se utilizan excepciones cuando los argumentos o la información existente no satisfacen una determinada regla de negocio (por ejemplo, intentar registrar un cliente que ya está registrado).
Sin embargo, en las restricciones de consulta, las excepciones tienen un significado diferente. Como una consulta no cambia la información, no hay argumento inválido que pueda impedir que se realice una consulta bien definida. Si un usuario consulta un sistema sobre un cliente que no existe, no se impide que se realice la consulta: respondería que no hay ningún cliente para la consulta; ésta es la respuesta correcta, no una excepción. Las excepciones en las consultas se utilizarán sólo si por casualidad el equipo decide que para una determinada condición no se debe realizar la consulta. Por lo general, estas condiciones están relacionadas con problemas de seguridad, u otros problemas tecnológicos tales como la interfaz multi-ventana, la concurrencia, la comunicación, etc. Como estos problemas no suelen ser abordados por el modelado funcional, las excepciones en las restricciones de consulta no son frecuentes.
Normalmente, en un contrato de operación, ya sea un comando o una consulta, una excepción puede transformarse en una precondición y viceversa. La decisión de diseñar un problema como precondición o excepción determina qué parte del sistema es responsable de probar ese problema: la operación invocante o la operación invocada. Por lo general, en los grandes sistemas multiusuario, las condiciones de acceso1 pueden llevar a optar por evitar las precondiciones; sin embargo, si el sistema no está sujeto a una concurrencia compleja o existe un mecanismo de control de concurrencia que impide que los datos cambien durante las transacciones, entonces un diseño basado en las precondiciones puede ser la mejor opción.
Para los ejemplos de este capítulo se utiliza un refinamiento parcial del modelo conceptual presentado en capítulos anteriores (Figura 8.1), así como una versión sin estado del diagrama de secuencia del sistema para el caso de uso 01: Pedir Libros (Figura 8.2).

Figura 8.1 Modelo conceptual de referencia.

Figura 8.2 Diagrama de secuencia del sistema de referencia.

El estereotipo inmutable utilizado para algunos atributos y roles en la Figura 8.1 se explica en la Sección 8.7.2.
En el modelo conceptual parcial de la figura 8.1, se añadió el concepto de carrito de la compra porque un usuario puede empezar a comprar aunque aún no esté identificado. Por lo tanto, el carro de la compra tiene un código de identificación (porque a medida que se va adoptando la estrategia de los sin estado debe identificarse de alguna manera). Además, a pesar de que el carro de la compra no es un concepto independiente, debería estar conectado al controlador porque puede existir sin un cliente e incluso sin artículos (un carro de la compra puede estar vacío).
En la clase libro, la cantidad del atributo InStock probablemente podría ser un atributo derivado si el stock se modelara usando el patrón de cuenta/transacción (Capítulo 7). Pero aquí se mantiene como un atributo simple.2
El primer comando en el diagrama de secuencia del sistema crea una cesta de la compra y devuelve su identificador. Esta es una excepción aceptable para el principio de Separación Comando-Consulta, ya que la interfaz necesita una referencia al carro de la compra para poder enviarle más mensajes. Si se utilizara la estrategia con estado en lugar de la estrategia sin estado, este retorno no sería necesario porque el controlador recordaría qué pedido se acaba de crear.
Si el cliente no está conectado, se llama a un fragmento llamado login (que podría ser especificado por un diagrama de secuencia separada reutilizable). El fragmento devuelve un identificador de cliente y reemplaza los dos fragmentos que se mencionan en la Figura 5.40: si el usuario tiene una cuenta, puede iniciar sesión; de lo contrario, puede crear una nueva cuenta e iniciar sesión.
Las operaciones (comandos y consultas) que se encuentran en la Figura 8.2 son las siguientes (el argumento que se muestra en el diagrama se adaptó a un estilo que es más común en los lenguajes de programación):
    • createCart():CartId - Este es un comando que crea una nueva instancia vacía de Cart y le asigna un identificador. Devuelve el identificador.
    • searchBook(Palabras clave:Set[String]):OrderedSet[Tuple] - Esta es una consulta que devuelve un conjunto ordenado de tuplas que contienen información sobre los libros que son relevantes para la búsqueda. Cada tupla tiene título, nombre del autor, precio, número de páginas, nombre del editor, isbn, imagen de portada y cantidad en stock de un libro.
    • add2Cart(aCartId:CartId, anIsbn:Isbn, aQuantity:Whole) - Este es un comando que crea una nueva instancia de Item y la enlaza con el carro y el libro identificados por los parámetros.
    • getCartSummary(aCartId:CartId):OrderedSet[Tuple] - Esta es una consulta que devuelve un conjunto ordenado de tuplas con información sobre el carro identificada por el ID del carro. La información devuelta, como se indica en la nota de la Figura 8.2, es el título, el nombre del autor, la cantidad, el precio unitario y el total.
    • finishOrder(aCartId:CartId, aCustomerId:CustomerId) - Este es un comando que crea una nueva instancia de Orden y la enlaza con el cliente y el carro identificado por los parámetros.

            ​ 8.2 Precondiciones
Las precondiciones establecen lo que debe ser cierto cuando se realiza una consulta o comando del sistema. Por ejemplo, considerando el modelo conceptual de referencia de la Figura 8.1, la operación add2Cart(aCartId:CartId, anIsbn:Isbn, aQuantity:Natural) puede asumir que el ID del carro es válido porque fue obtenido por la operación anterior createCart():CartId. Por lo tanto, se podría escribir una condición previa que diga que esto es cierto:

Context Livir:: add2Cart(aCartId:CartId, anIsbn:Isbn, aQuantity:Natural)   
  pre:
    cart[aCartId]→notEmpty()

La expresión OCL anterior indica que en el contexto del método add2Cart, que es un comando del sistema implementado por el controlador Livir, existe una condición previa que establece que existe efectivamente una instancia de Cart que se identifica con el argumento aCartId.
Si la asociación entre Livir y Cart en la Figura 8.1 no fue calificada, entonces la precondición podría ser escrita aplicando select al conjunto de carros:

Context Livir:: add2Cart(aCartId:CartId, anIsbn:Isbn, aQuantity:Natural)
  pre:
    cart->select(id=aCartId)->notEmpty()

Sin embargo, cuando una asociación se califica como en la Figura 8.1, se debe utilizar un valor clave para acceder directamente al elemento mapeado por la asociación. Así, como el comando add2Cart tiene un argumento aCartId, la expresión cart[aCartId] produce el mismo resultado que la expresión cart->select(id=aCartId). Recuerde que la expresión anterior es también una abreviatura de self.cart->select(aCart|aCart.id=aCartId).
Para ser útil para el desarrollo de software, las condiciones previas deben ser expresadas de una manera cuidadosa. Deben reflejar hechos que pueden ser identificados en el modelo conceptual previamente desarrollado, o el modelo tiene que ser actualizado para reflejar la nueva información recién descubierta. Esto justifica el uso de lenguajes formales como el OCL para escribir restricciones (Warmer & Keppe, 1998) en lugar de lenguaje natural.
Se pueden identificar dos familias de condiciones previas:
    • Garantía de parámetros: Condiciones previas que aseguran que los argumentos de un comando o consulta corresponden a objetos válidos (por ejemplo, "existe un carro de la compra con el ID pasado como argumento").
    • Limitación complementaria: Condiciones previas que limitan aún más el modelo conceptual a la hora de realizar un determinado comando o consulta, con el fin de asegurar que la información se encuentra en un estado determinado cuando se está ejecutando la operación (por ejemplo, "el carro tiene al menos un elemento").

                ​ 8.2.1 Garantía de parámetros
Existe una forma sistemática de saber si una operación determinada debe tener una precondición (o excepción) de garantía de parámetros. Esta técnica también está relacionada con la prueba funcional de la operación, como se ve en el Capítulo 13. El equipo debe examinar cada parámetro de la operación y preguntar si existen valores válidos e inválidos teniendo en cuenta el tipo de parámetro.
Por ejemplo, si el tipo de parámetro es Isbn, y el comando es add2Cart(..., anIsbn:Isbn, ...), entonces, considerando las reglas de negocio, hay un grupo de valores válidos (ISBNs que pertenecen a un libro registrado), y un grupo de valores no válidos (ISBNs que son válidos pero que no están asignados a ningún libro del sistema).
Por otro lado, si el tipo de parámetro es String y el comando es add2Cart(..., anIsbn:String, ...), se deben considerar tres clases: una válida (igual que antes: ISBNs para libros registrados), y dos clases inválidas que consisten en ISBNs válidos pero que no pertenecen a ningún libro registrado (como antes), e ISBNs formados incorrectamente (ya que el tipo String admite cualquier cadena, no sólo ISBNs). Esta distinción entre ISBNs mal formados e inexistentes puede ser útil para evitar, por ejemplo, malentendidos relacionados con los errores tipográficos cuando el usuario introduce ISBN como parámetro de búsqueda.
Así, considerando el tipo de parámetro e identificando los grupos de parámetros no válidos, la regla para encontrar las condiciones previas de garantía de los parámetros es la siguiente:

Para cada grupo de valores no válidos para un parámetro de operación del sistema, se debe definir una condición previa o una excepción.

En cuanto a las condiciones previas de la garantía de los parámetros, se debe tener especial cuidado de no confundir las condiciones previas semánticas con simples verificaciones sintácticas. La verificación semántica requiere que se consulte la base de datos: por ejemplo, verificar si existe un libro con un determinado ISBN. Sin embargo, la verificación sintáctica puede realizarse mediante mecanismos distintos de las condiciones previas. Si un parámetro tiene un tipo Natural, no se necesita ninguna consulta a la base de datos para verificar si un argumento dado pertenece al tipo o no. Entonces, si un parámetro se declara como x:Natural no es necesario escribir ninguna condición previa para asegurar que x es un número positivo: el tipo ya lo indica.
Otro ejemplo es el ISBN, que tiene una regla de formación y se puede verificar sintácticamente. En lugar de escribir condiciones previas para verificar si un parámetro es un ISBN bien formado, el equipo debería simplemente crear un Isbn tipo primitivo con un método de verificación y utilizarlo.
¿Qué hay de PrimeNumber? ¿Podría ser un tipo? La respuesta es sí, porque para saber si un número dado es un número primo, una verificación sintáctica es suficiente.
Los tipos deben definirse en la firma de comandos. Si el tipo no existe, el equipo puede definir un tipo primitivo. Por ejemplo, la Figura 8.1 presenta tipos primitivos como CustomerId y OrderId que pueden incorporar no sólo mecanismos de identificación y suma de comprobación, sino también mecanismos de seguridad, ya que esos identificadores pueden ser encriptados para evitar el acceso no autorizado. En ambos casos, podrían definirse tipos primitivos para hacer frente a la complejidad del mecanismo de verificación.

                ​ 8.2.2 Restricciones complementarias
Una restricción complementaria consiste en asegurar que se obtengan ciertas restricciones más fuertes que las del modelo conceptual mientras se ejecuta un comando dado. Así, si el modelo conceptual establece que un determinado rol tiene multiplicidad 0..1, por ejemplo, una restricción complementaria podría decir simplemente que al ejecutar un determinado comando ese rol se cumple (1) o no (0). Por ejemplo, en general un Carrito puede tener una Orden asociada o no (0..1). Pero el comando que finaliza una Orden debe tener una condición previa que indique que el Carro no estaba aún vinculado a ninguna orden (el rol de Carro a Orden no debe ser ocupado: 0).
Por lo tanto, una condición previa nunca puede contradecir el modelo conceptual. Si el modelo conceptual establece 0..1, entonces ninguna condición previa podría establecer una multiplicidad de 2 o más para el mismo rol. Pero si el modelo conceptual establece 0..2, entonces la precondición puede restringirlo aún más, indicando, por ejemplo, 0..1 o 1..2.
Las restricciones complementarias son comunes en los diseños que utilizan la estrategia de estado, porque en ese caso cada comando necesitará información que fue dejada en memoria transitoria por otros comandos, como por ejemplo, la identificación del cliente, que es pasada por un comando y utilizada por otros. Así, esos otros comandos habrían establecido como condición previa que el cliente fue identificado adecuadamente (posiblemente por una asociación transitoria).
Es posible identificar al menos tres tipos de limitaciones complementarias:
    • Una declaración específica sobre una instancia o sobre un conjunto de instancias.
    • Una declaración existencial sobre un conjunto de instancias.
    • Una declaración universal sobre un conjunto de instancias.
Un ejemplo de una declaración específica sobre una instancia, considerando nuevamente el modelo de la Figura 8.1, podría ser declarar que un cliente con ID 123 tiene una fecha de nacimiento igual al 14 de julio de 1970:

Context Livir::someCommand()
  pre:
    customer[123].birthDate=Date.getDate(1970,7,14)

Como OCL no define ningún literal para el tipo de fecha, una operación predefinida Date.getDate puede ser usada para definir una fecha dada.
Un ejemplo de una declaración existencial sería decir que hay al menos un cliente nacido el 14 de julio de 1970 (no importa quién):

Context Livir::someCommand()
  pre:
    customer->exists(aCustomer|
      aCustomer.birthDate=Date.getDate(1970,7,14))

Un ejemplo de una declaración universal sería decir que cada cliente nació el 14 de julio de 1970:

Customer Livir::someCommand()
  pre:
    customer->forAll(aCustomer|
      aCustomer.birthDate=Date.getDate(1970,7,14))

Ambas expresiones existen y paraTodo puede ser escrito en forma simplificada como existe (birthDate=Date.getDate(1970,7,14)) y forAll(birthDate=Date.getDate(1970,7,14)), manteniendo el mismo significado arriba mencionado.

                ​ 8.2.3 Aseguramiento de las condiciones previas
Como las precondiciones no son probadas por el comando que las declara, debe existir un mecanismo externo para asegurar que serán garantizadas antes de que el comando sea llamado.
Esta garantía puede hacerse llamando explícitamente a una consulta que verifica si la condición es verdadera antes de llamar el comando, o mediante mecanismos de interfaz que evitan que el comando sea llamado con datos inválidos.
Por ejemplo, en lugar de permitir que el usuario escriba cualquier cadena en un campo ISBN, el usuario podría ser llevado a seleccionar de una lista de ISBNs válidos. De esta forma, el parámetro sería validado antes de ejecutar el comando.
Normalmente, el flujo de mensajes expresado en el diagrama de secuencia del sistema es una forma de verificar si las condiciones previas son viables en lugar de las excepciones. Por ejemplo, en la Figura 8.2 observe que el ID de carro recibido por la operación add2Cart es válido porque fue devuelto por el comando createCart; el ISBN del libro también es válido porque fue recogido de una lista devuelta por la consulta searchBook. Finalmente, la cantidad puede ser aceptada como válida porque la interfaz puede compararla con la cantidad disponible en stock que fue devuelta con otra información sobre el libro..3

                ​ 8.2.4 Condiciones previas y excepciones frente a invariantes
Las invariantes (Sección 6.7) se utilizan en el modelo conceptual para representar reglas que son siempre válidas, independientemente de cualquier comando o consulta. Las condiciones previas se utilizan para las reglas que son válidas sólo cuando se está ejecutando un comando o una consulta determinados.
Cuando ya existe una invariante para una situación dada, equivale a la existencia de una excepción para cualquier operación. Por ejemplo, si hay una invariante que indica que un estudiante puede inscribirse sólo en cursos relacionados con su carrera, entonces la invariante funciona como una excepción para cualquier comando. Por lo tanto, los comandos para inscribir a un estudiante pueden considerar que la excepción ya existe en la forma de la invariante y si el estudiante trata de inscribirse en un curso que no pertenece a su carrera una excepción sería planteada.
Sin embargo, una invariante no funciona como condición previa. La existencia de una invariante no garantiza que el diseño no la viole. Sin embargo, un comando puede añadir una condición previa que establezca que la invariante debe estar asegurada antes de que se ejecute.
Los mecanismos de prueba deben verificar si se están respetando las invariantes y las condiciones previas durante las actividades de prueba del sistema. Si esas condiciones se violan en cualquier momento, deben preverse excepciones. Sin embargo, en esos casos, el diseñador debe revisar el diseño para corregir ese error y evitar que vuelva a ocurrir. Cuando el sistema se entrega al usuario final, debe garantizarse que no se infringe ninguna condición previa ni invariable en ningún momento.

            ​ 8.3 Asociaciones transitorias
Cuando se utiliza la estrategia de estado en el diagrama de secuencia del sistema, es necesario que el controlador mantenga en memoria cierta información que no es persistente, pero que debe ser almacenada durante la ejecución del caso de uso.
Algunos objetos, atributos o asociaciones que no son persistentes pueden definirse para indicar información que se almacena sólo en la memoria principal durante un caso de uso, y que se descarta después. Esos elementos pueden ser estereotipados con elementos transitorios.
Por ejemplo, se puede utilizar una asociación transitoria para indicar que el controlador debe almacenar información sobre quién es el cliente actual en el modelo conceptual refinado, como se muestra en la Figura 8.3.

Figura 8.3 Una asociación transitoria.

Así, una condición previa de un comando, por ejemplo, podría indicar que ya existe un cliente actual: 

Context Livir::someCommand() 
  pre:
    currentCustomer->notEmpty()

Los atributos o clases transitorias, si es necesario, también se pueden definir con este estereotipo. En cualquier caso, esto significa que la información estereotipada no es persistente.

            ​ 8.4 Retorno de consultas
Como se mencionó anteriormente, los comandos del sistema cambian los datos mientras que las consultas sólo devuelven los datos al usuario. Las restricciones para consultas del sistema deben definir lo que se devuelve, y esto se puede hacer en OCL utilizando la cláusula body.
Las expresiones que representan condiciones previas son todas booleanas, pero las expresiones que representan el retorno de una consulta pueden tener otros tipos. Pueden devolver cadenas, números, listas, tuplas o incluso estructuras más complejas. Los siguientes ejemplos se basan en el modelo de la figura 8.1. Inicialmente, se define una consulta que devuelve el total de un carro determinado:

Context Livir::getCartTotal(aCartId:CartId):Money
  body:
    cart[aCartId].total

Las consultas del sistema, así como los comandos del sistema, siempre tienen al controlador como contexto. Por lo tanto, en el ejemplo anterior, carro es una propiedad del controlador Livir: una función de asociación de la misma a la clase Cart.
La siguiente consulta devuelve el nombre y la fecha de nacimiento de un cliente determinado:

Context  Livir::getCustomerNameBirthDate(aCustomerId:CustomerId):Tuple
    body:
      Tuple {
        name=customer[aCustomerId].name,
        birthDate=customer[aCustomerId].birthDate
      }

El constructor Tuple es una de las formas de representar DTOs4 en OCL; la tupla funciona como un registro Pascal en el ejemplo con dos campos: nombre y fecha de nacimiento. Los valores de los campos están definidos por las expresiones después del "=".
Para evitar repetir expresiones como customer[aCustomerId] o incluso expresiones más complejas, se puede utilizar la cláusula def para definir una constante que se refiera a la expresión original. Usando la cláusula def, la restricción anterior se vería como el siguiente: 

Context  Livir::getCustomerNameBirthDate(aCustomerId:CustomerId):Tuple
    def:
      aCustomer=customer[aCustomerId]
    body:
      Tuple {
        name=aCustomer.name,
        birthDate=aCustomer.birthDate
      }

La expresión dentro de la cláusula def indica que el identificador aCustomer se refiere al cliente cuyo ID es el parámetro aCustomerId recibido de la consulta.
La siguiente expresión hace una proyección en el conjunto de clientes que devuelven los nombres de todos los clientes: 

Context Livir::listCustomerNames():Set
  body:
    customer.name

La siguiente expresión aplica un filtro y una proyección, devolviendo los nombres de todos los clientes menores de 25 años:

Context Livir::listYoungCustomers():Set
  body:
    customer->select(birthDate.addYear(25)>Date.getCurrent()).name

La idea del ejemplo anterior es añadir 25 años a la fecha de nacimiento del cliente y compararla con la fecha actual: si el cliente cumple 25 años después de la fecha actual, entonces es menor de 25 años. OCL también tiene operaciones para agregar días y meses a las fechas: addDay y addMonth, respectivamente. La expresión Date.currentDate devuelve la fecha actual del sistema.
El último ejemplo es una consulta que devuelve el resumen del carro, como se muestra en la Figura 8.2.

Context Livir::getCartSummary(aCartId:CartId):Tuple
  def: aCart=cart[aCartId]
  body:
    Tuple {
      total=aCart.total,
    items=aCart.item->collect(anItem|
        Tuple {
          title=anItem.book.title,
          authorsName=anItem.book.authorsName,
          quantity=anItem.quantity,
          unitPrice=anItem.unitPrice,
          subtotal=anItem.subtotal
        }
      )
    }

La expresión collect es una forma de obtener un conjunto cuyos elementos son propiedades o transformaciones sobre propiedades de otro conjunto. La notación por puntos (".") en sí misma es una forma abreviada de coleccionar. Por ejemplo, customer.name es equivalente a customer->collect(aCustomer|aCustomer.name) o customer->collect(name).
Cuando sea posible, se prefiere la notación por puntos porque es más corta. Pero en el ejemplo getCartSummary, la necesidad de crear una tupla en lugar de acceder a una propiedad de los elementos de un conjunto impide el uso del punto, porque el operador Tuple está prefijado. Por lo tanto, la expresión collect tiene que ser usada explícitamente en ese caso.
En el ejemplo, se construyeron dos estructuras tuplas: la exterior contiene el total del carro y el conjunto ordenado de sus artículos; la interior contiene para cada artículo la información que se necesita según se menciona en la Figura 8.2: título del libro, nombre del autor, etc.

            ​ 8.5 Postcondiciones
Las postcondiciones establecen qué cambios en la información gestionada por el sistema se producen después de que se ejecuta algún comando. Las condiciones posteriores también deben ser cuidadosamente especificadas en términos que puedan ser reconocidos inmediatamente en las estructuras conceptuales del modelo. Por lo tanto, aunque las restricciones pueden ser escritos en lenguaje natural, deben ser cuidadosamente escritos para que puedan ser traducidos inmediatamente a expresiones OCL.
Una postcondición  OCL se escribe en el contexto de un comando (sistema) utilizando la cláusula post:

Context Livir::someCommand()
  post:
    <OCL expression>

Si hay más de una condición posterior, se pueden combinar mediante el uso de la palabra clave and:5

Context Livir::someCommand()
  post:
    <OCL expression> and
    <OCL expression> and
    …
    <OCL expression>

Para clasificar los tipos de postcondiciones que se pueden utilizar en una restricción, debemos tener en cuenta que el modelo conceptual tiene tres elementos básicos, que son conceptos, atributos y asociaciones. Así, considerando que las instancias de clases pueden ser creadas y destruidas, los enlaces de asociación pueden ser añadidos y eliminados, y los valores de los atributos pueden ser cambiados, sólo cinco tipos de postcondiciones son posibles:
    • Modificar un valor de atributo.
    • Cree una instancia de clase.
    • Añadir un enlace de asociación.
    • Destruir una instancia de clase.
    • Eliminar un enlace de asociación.
Estos comandos son los comandos más fundamentales o básicos que se pueden definir para un sistema orientado a objetos. No se pueden descomponer más y todos los demás comandos se definen como combinaciones de ellos.
Por lo tanto, un comando básico es un comando que realiza una de las cinco postcondiciones enumeradas anteriormente. El significado y el comportamiento de un comando básico está predefinido.
Desafortunadamente, los lenguajes de programación todavía no proporcionan una implementación estándar para estos comandos básicos. La implementación de estos comandos a veces se deja como una tarea manual difícil para los programadores, especialmente en el caso de los comandos que añaden y destruyen enlaces.
Los comandos básicos, tal como se definen en las siguientes subsecciones, son efectivamente básicos en el sentido de que realizan la tarea sin realizar ciertas verificaciones de consistencia. Por ejemplo, un comando que agrega un enlace no verificaría si se alcanzaron los límites superiores para ambas funciones de la asociación. Este tipo de verificación de consistencia se realiza preferentemente para todo un conjunto de comandos pertenecientes al misma restricción.
La discusión sobre cómo mantener la coherencia de los objetos en las restricciones continúa en la Sección 8.5.6.


                ​ 8.5.1 Modificación del valor de un atributo
Una de las clases de postcondiciónes consiste en indicar que se ha modificado el valor de un atributo. Eso es usualmente escrito en OCL como

object.attribute=value

Pero, como OCL es un lenguaje declarativo, esta expresión no debe ser entendida como una asignación. Tiene, de hecho, tres maneras posibles de hacerse realidad:
    • object.attribute puede ser cambiado para que sea igual al valor. Esta es generalmente la interpretación por defecto.
    • puede ser cambiado para que sea igual a object.attribute.
    • Tanto el valor como el atributo pueden cambiarse a un tercer valor y volverse iguales.
Por lo tanto, en términos de generación de código, este tipo de expresión puede producir interpretaciones ambiguas. Cabot (2007) propone una semántica por defecto para interpretar tales expresiones de manera que se reduzca la ambigüedad. Sin embargo, otro enfoque es posible, que no requiere cambiar la semántica original de OCL. La idea es utilizar el predicado "^" (caret) en lugar del predicado "=" (signo igual), como se explica a continuación.
Podemos indicar sin ambigüedad que un atributo se ha modificado simplemente declarando que se ha enviado al objeto un mensaje básico sobre el cambio. El mensaje básico está predefinido, y su nombre debe comenzar con el prefijo "set" seguido del nombre del atributo. El nuevo valor se pasa como argumento.
El mensaje setAttribute puede ser enviado a una instancia de una clase que contenga el atributo. Por ejemplo, si estamos interesados en cambiar el precio de un libro dado, se puede utilizar la siguiente expresión OCL:

Context Livir::updateBookPrice(anIsbn:Isbn;newPrice:Money)
  post:
    book[anIsbn].price=newPrice

Pero ya hemos visto que se puede interpretar de manera ambigua. La siguiente expresión expresa la misma intención, pero sin ambigüedad:

Context Livir::updateBookPrice(anIsbn:Isbn;newPrice:Money)
  post:
    book[anIsbn]^setPrice(newPrice)

La notación caret significa que el mensaje de la derecha fue enviado al objeto o colección de objetos de la izquierda. Por lo tanto, es un predicado booleano y el resultado de la expresión anterior es booleano.
La expresión libro[anIsbn].price=newPrice significa que dos valores son iguales sin importar cómo se haya logrado ese resultado. Pero book[anIsbn]^setPrice(newPrice) establece sin ambigüedad que el precio de atributo del libro objeto[anIsbn] fue cambiado a newPrice.
Esta forma de escritura se sigue considerando una especificación declarativa, no imperativa. La expresión book[anIsbn]^setPrice(newPrice) sólo indica que un objeto ha recibido un mensaje; no dice quién lo envió. La decisión sobre qué objeto va a enviar ese mensaje al libro[anIsbn] se deja para el modelado dinámico (Capítulo 9).

                ​ 8.5.2 Creación de una instancia
El comando que crea una instancia debe hacer eso: crear una instancia de clase. Aunque OCL no es un lenguaje imperativo, tiene un constructor que indica que se ha creado una nueva instancia de una clase. Esto se expresa como una propiedad de un objeto y se hace referencia de la siguiente manera:

object.oclIsNew()

Su significado, cuando se usa en una postcondición, es que el objeto fue creado durante el comando especificado por la postcondición. Esta propiedad puede ser usada en conjunto con otra que declare la clase del objeto:

object.isTypeOf(class)

Sin embargo, como sería un poco tedioso seguir declarando la creación de una instancia usando dos expresiones, se sugiere la definición de un único predicado que establece que un objeto fue creado como instancia de una clase dada. Por lo tanto, la expresión object.isNewInstanceOf(class) se define como equivalente a

object.oclIsNew() and object.oclIsTypeOf(class)

Así, una condición posterior que declara que una nueva instancia de Libro, referida como nuevo Libro, fue creada puede ser definida como

newBook.newInstanceOf(Book)

En este caso, no se utiliza la notación caret porque no es un mensaje enviado a una instancia de Book. Es una declaración de que se ha creado un nuevo Libro de la clase Book.
El mensaje newInstanceOf no dice nada sobre los atributos y enlaces de la instancia, ni siquiera los obligatorios. Como antes, se puede asumir que otras expresiones inicializarán atributos y enlaces obligatorios, y que la consistencia de la nueva instancia se comprobará para la restricción como un todo y no para cada comando básico individual.
Los atributos con valores iniciales se consideran automáticamente inicializados cuando se crea la instancia. Por lo tanto, sería redundante especificar postcondiciones para actualizar los atributos con valores iniciales, a menos que se deseen valores diferentes de los predeterminados.
Los atributos derivados, por otra parte, se calculan y no se pueden modificar directamente. Por lo tanto, no se inicializan.
Los atributos estereotipados con opcional pueden mantenerse indefinidos en el momento de la creación; la definición de un valor para ellos no es obligatoria.
Pero, ¿qué sucede con otros atributos (normales y obligatorios) en el momento en que se crea una instancia? El comando básico representado por el predicado newInstanceOf simplemente produce la instancia. No inicializa atributos y enlaces excepto aquellos que están definidos con valores iniciales predeterminados. Si no se inicializan los atributos y enlaces obligatorios, la instancia puede ser inconsistente; por lo tanto, la restricción debe especificar otras condiciones posteriores que aseguren que todos los atributos y enlaces obligatorios se inicializan cuando se crea un objeto.
Hemos visto hasta ahora postcondicionales para crear instancias y cambiar atributos. Esto nos permite combinarlos para crear una restricción para un comando CRUD que crea una nueva instancia de Book. El comando de sistema createBook puede tener lo siguiente como borrador inicial de una restricción:

Context Livir::createBook(anIsbn:ISBN;
  aTitle,anAuthorsName:String; aPrice:Money;
  aPageCount:Natural; aCoverImage:Image)
  post:
    newBook.newInstanceOf(Book) and
    newBook^setIsbn(anIsbn) and
    newBook^setTitle(aTitle) and
    newBook^setAuthorsName(anAuthorsName) and
    newBook^setPrice(aPrice) and
    newBook^setPageCount(aPageCount) and
    newBook^setCoverImage(aCoverImage)

Tenga en cuenta que quantityInStock se define con un valor inicial y no es necesario inicializarlo en este pedido abierto.
El atributo coverImage es un atributo opcional y por esa razón es el único parámetro que puede aceptar el valor nulo; alternativamente, puede ser suprimido de la lista de parámetros de createBook.
El atributo publisherName se deriva, y como sólo se lee no se puede definir en la restricción (en su lugar, la cláusula derive de la clase define su valor para cada instancia). Sin embargo, su valor depende de un vínculo entre el libro y su editor y la primera versión de esta restricción no define cómo se añade ese vínculo. Esto se discute en la siguiente sección.
Hay una preocupación más: si consideramos que toda la información es accesible navegando por enlaces desde la instancia del controlador, entonces no sería aconsejable declarar que una instancia fue creada si no está vinculada a ninguna otra instancia con una ruta al controlador de la fachada. A menos que otro mecanismo de búsqueda de núcleo permita encontrar instancias que no estén vinculadas (directamente o no) al controlador, la instancia recién creada es inalcanzable. Por lo tanto, la creación de una instancia debe realizarse siempre junto con la adición de un enlace, que se explicará en la siguiente sección.

                ​ 8.5.3 Añadir un enlace
Como se mencionó anteriormente en el capítulo, otro tipo de comando básico es el que establece que se agregó un enlace entre dos objetos. Aunque las adiciones de enlaces están limitadas por la multiplicidad de los roles, esto sólo se verifica para la restricción en su conjunto y no para cada comando básico individual.
Usualmente, una postcondición a la OCL para indicar que un enlace fue creado se vería como la siguiente:

object.role->incluye(anotherObject)

Pero, de nuevo, esta expresión puede ser interpretada ambiguamente cuando se encuentra en la etapa de generación de código, porque hay al menos cuatro maneras de que se haga realidad:
    • Incluir anotherObjet en object.role.
    • Asignar a anotherObjet un objeto que ya está en object.role.
    • Asigne un tercer objeto a anotherObjet e inclúyalo en object.role.
    • Asigne el set vacío a anotherObjet, porque independientemente del contenido de object.role incluye el set vacío.
Usualmente, la primera opción es el significado deseado. Pero de nuevo sugerimos una notación que no cause interpretaciones ambiguas y al mismo tiempo sea más familiar para los desarrolladores de software. Una vez más, la notación "^" y un comando básico se utilizan para indicar que se ha creado un enlace.
Hay muchos dialectos para nombrar comandos que modifican los roles de asociación. Aquí, usamos el prefijo add seguido del nombre del rol. Otra opción común sería utilizar el prefijo set, como en el caso de los atributos. Sin embargo, los atributos tienen sus valores cambiados o reemplazados, mientras que los enlaces se añaden; por lo tanto, diferentes objetivos deben tener diferentes nombres.
Considerando la asociación entre las clases Book y Publisher, y considerando dos instancias, aBook y aPublisher, respectivamente, se puede crear un vínculo entre las instancias de dos maneras diferentes. Primero, desde el punto de vista de un libro:

aBook^addPublisher(aPublisher)

Segundo, desde el punto de vista de un editor:

aPublisher^addBook(aBook)

Ambas expresiones son simétricas y producen exactamente el mismo resultado (se crea un vínculo basado en la asociación entre las instancias).
Las asociaciones con funciones obligatorias, como la que va de Book to Publisher, suelen exigir que sus enlaces se creen en la misma restricción que crea el objeto que debe ser ocupado por la función. Por lo tanto, se agregará un enlace de Libro a Editor cuando se cree una instancia de Libro, como se muestra a continuación:

Context Livir::createBook(anIsbn:ISBN; aTitle,anAuthorsName:String;
aPrice:Money; 
aPageCount:Natural; 
    aPublisherName:String; 
aCoverImage:Image)

  post:
    newBook.newInstanceOf(Book) and
    newBook^setIsbn(anIsbn) and
    newBook^setTitle(aTitle) and
    newBook^setAuthorsName(anAuthorsName) and
    newBook^setPrice(aPrice) and
    newBook^setPageCount(aPageCount) and
    newBook^setCoverImage(aCoverImage) and
    newBook^addPublisher(publisher[aPublisherName]) and
    self^addBook(newBook)

En la restricción anterior, se añadieron dos enlaces obligatorios al nuevo libro: uno de él a su editor y otro al controlador Livir. Recuerde que como Livir es el contexto de la restricción, self es una instancia de Livir.

                ​ 8.5.4 Destruir una instancia
Aunque la destrucción de objetos es poco frecuente en los sistemas orientados a objetos, a veces puede ocurrir. Por lo general, los libros agotados y los clientes fallecidos no se eliminan de los registros: simplemente se marcan como inactivos o se trasladan a un lugar alternativo. La información no debe perderse si se necesitan registros fiables de las actividades de la empresa en el pasado.
Sin embargo, si un editor o cualquier otra instancia de clase se insertó en el registro del sistema dos veces por error, las instancias pueden fusionarse si ambas ya han sido modificadas o, si no se registró ninguna actividad para la segunda instancia, puede simplemente borrarse de los registros. En este caso, un objeto debe ser destruido.
Existen dos enfoques para indicar que una instancia fue destruida:
    • Explícito: Se declara que un objeto fue destruido enviándole un mensaje de destrucción explícito.
    • Implícito: Todas las asociaciones con el objeto se eliminan para que sea inaccesible. En los lenguajes de programación es posible implementar la recolección de basura para eliminar de la memoria los objetos que ya no son accesibles.
En este libro, se escoge el enfoque explícito porque hace más clara la intención real del modelador. Un objeto que tiene que ser destruido, entonces, debe recibir un mensaje básico como el siguiente:

object^destroy()

El significado de esta expresión en una postcondición del comando de sistema que es que el objeto referido fue destruido durante la ejecución del comando.
Se asume que todos los enlaces al objeto destruido también se eliminan. Si algún objeto anteriormente enlazado con él se vuelve incoherente, la restricción debe especificar qué sucede con ese objeto (si también se suprime o si el rol se sustituye por un enlace con otro objeto).

                ​ 8.5.5 Eliminar un enlace
LA eliminación de in enlace entre dos objectos, está hecha por in comando básico prefijado por la palabra remove, seguida pot el nombre del rol,y recibiendo como parameter el objeto miembro del role que debe see eliminado. Por ejemplo, para eliminar el último artículo de in carrito, debería usarse el siguiente contrato:

Context Livir::removeLastItem(aCartId:CartId)
  def: aCart=cart[aCartId]
  def: lastItem=aCart.item->last()
  post:
    aCart^removeItem(lastItem)

Cuando la multiplicidad de la función de destino del enlace a eliminar es 1 o 0..1, es opcional informar el parámetro, ya que sólo hay un enlace posible a eliminar. Si en lugar de eliminar el enlace desde el punto de vista del carro se hiciera desde el punto de vista del artículo, el resultado final sería el mismo, pero el comando básico no necesitaría un parámetro:

Context Livir::removeLastItem(aCartId:CartId)
  def: aCart=cart[aCartId]
  def: anItem=aCart.item->last()
  post:
          anItem^removeCart()

Sin embargo, ambas restricciones anteriores dejan el artículo inconsistente, porque tiene una asociación obligatoria con el Cart que ya no existe si la restricción tiene éxito. La restricción debe tener en cuenta que, al ser obligatorio el paso de artículo a carro (1), la eliminación de este enlace implica la destrucción del artículo o su vinculación a otro carro, que debe completarse en la misma restricción.
Si la opción es borrar el artículo, entonces sólo ese comando básico debe ser usado en la restricción porque con él, todos los enlaces al artículo se consideran automáticamente eliminados también: 

Context Livir::removeLastItem(aCartId:CartId)
  def: aCart=cart[aCartId]
  def: lastItem=aCart.item->last()
  post:
    lastItem^destroy()

Intentar eliminar un enlace inexistente es un error de diseño y no se puede declarar en restricciones bien formadas, que se discuten en la siguiente sección.

                ​ 8.5.6 Postcondiciones bien formadas
Si suponemos que los comandos básicos no comprueban si los objetos y enlaces se dejan en un estado consistente después de que se ejecutan, entonces el diseñador debe hacer la verificación cuando está especificando las restricciones de comandos del sistema.
Las verificaciones que se deben realizar se pueden resumir de la siguiente manera:
    • Un comando que crea una instancia también debe tener postcondiciones que establezcan que todos los atributos de la instancia fueron inicializados, excepto (1) los atributos derivados (que son calculados), (2) los atributos con un valor inicial (que son predefinidos por una cláusula init, a menos que se desee un valor diferente), y (3) los atributos opcionales, que pueden ser nulos (en ese caso, la inicialización es opcional).
    • Todos los enlaces obligatorios para una instancia recién creada deben ser añadidos.
    • Incluso si no tiene enlaces o asociaciones, una instancia recién creada debe estar enlazada con al menos una instancia que tenga una ruta de enlace al controlador o estar enlazada con el propio controlador.
    • Todos los enlaces creados deben permanecer dentro de los límites inferior y superior definidos por sus funciones de asociación.
    • Todas las invariantes afectadas por cambios en atributos, enlaces o instancias deben permanecer verdaderas.
El mecanismo de verificación de invariantes no asegura que el diseñador esté escribiendo una restricción que mantenga todas las invariantes verdaderas. Es responsabilidad del diseñador estar al tanto de las invariantes y evitar hacer excepciones. Si una invariante plantea una excepción que no es manejada por el sistema, entonces ciertamente hay un problema de diseño.
Otro problema se refiere a los atributos declarados con valores iniciales. Si la definición del valor inicial de un atributo utiliza información que sólo puede obtenerse navegando por sus enlaces, ¿cómo puede calcularse antes de crear los enlaces? Debemos tener en cuenta que la inicialización de atributos con valores iniciales será una de las últimas tareas en el código de programación que implemente una restricción, es decir, los atributos con valores iniciales sólo podrán definirse después de que se añadan todos los enlaces y la instancia sea consistente. Por ejemplo, el precio unitario de un artículo en la Figura 8.1 sólo puede ser inicializado después de que se agregue un enlace entre el artículo y el libro, porque el valor inicial depende del enlace. El diseñador de las restricciones no necesita preocuparse por esto porque las restricciones son declarativas, pero el programador debe preocuparse por ello al producir código.

                ​ 8.5.7 Combinaciones de post-condiciones
Normalmente, un comando de sistema tendrá muchas condiciones posteriores a las que puede unirse el operador and, como se mencionó anteriormente. Pero también es posible utilizar el operador or, que establece que se obtuvo una de las condiciones posteriores, pero no necesariamente la otra:

post:
  <postcondition1> or
  <postcondition2>

El principal problema con este operador es que es intrínsecamente ambiguo en términos de generación de código, y por lo tanto, su uso debe evitarse si las expresiones determinísticas son posibles.
Otro operador que se puede utilizar para conectar expresiones OCL es el operador implies, que tiene el mismo significado que el operador de implicación de la lógica booleana. Implica que se utiliza cuando se debe obtener una condición posterior sólo si una cierta condición es verdadera. Por ejemplo, el siguiente restricción añade un libro a un carro sólo si aún no está allí:
 
Context Livir::add2Cart(aCartId:CartId,  anIsbn:Isbn,aQuantity:Natural)
  def:aCart=cart[aCartId]
  def:aBook=book[anIsbn]
  def:anItem=aCart.item->select(book.isbn=anIsbn)
  pre:
    aCart->notEmpty() and
    aBook->notEmpty()
  post:
    anItem->isEmpty() implies
      newItem.isNewInstanceOf(Item) and
      aCart^addItem(newItem) and
      newItem^setQuantity(aQuantity) and
      newItem^addBook(aBook) and
      newItem^setUnitPrice(aBook.price)

El operador implices que también puede ser reemplazado por una expresión if-then-endif. Esta expresión es especialmente útil si se debe obtener una postcondición alternativa cuando la condición es falsa; en este caso se debe usar la forma if-then-else-endif. En el caso del último ejemplo, si el libro ya está en el pedido, la cantidad pedida puede añadirse a la cantidad del artículo existente. El siguiente restricción muestra cómo utilizar este operador:
 
Context Livir::add2Cart(aCartId:CartId,  anIsbn:Isbn,aQuantity:Natural)
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

El significado del operador pre se explica en la siguiente sección.
La ventaja de esto es que es más corto. La ventaja de if-then-endif o if-then-else-endif es que es más familiar para los programadores, e incluye una forma de especificar qué se debe obtener para ambos casos de una expresión booleana que es más corta que el uso de dos estructuras implies.

                ​ 8.5.8 Valores previos
A veces una condición posterior se construye sobre valores que los atributos y roles tenían antes de que se ejecutara el comando. Estos valores anteriores son referidos por la función @pre para indicar que no corresponden al valor del atributo después de ejecutar el comando (que podría ser diferente). Por ejemplo, una condición posterior que establece que una cantidad en stock para un libro determinado ha aumentado puede expresarse como
 
Context Livir::add2Stock(anIsbn:Isbn; aQuantity:Natural)
  def:aBook=book[anIsbn]
  post:
    aBook^setQuantityInStock(
      aBook.quantityInStock@pre + aQuantity
    )

Entonces, ¿por qué se usó @pre arriba? Porque después de ejecutar el comando, la cantidad en stock ya estaría incrementada, y el argumento para el comando básico setQuantityInStock tiene que ser definido como la cantidad anterior más la nueva cantidad.
Recuerda que OCL es declarativo, igual que la aritmética. x=x+1 no es una declaración verdadera en notación matemática, porque no puede serlo para ningún valor de x. Pero cuando escribes x :=x+1 en un lenguaje de programación significa lo mismo que x=x@pre+1.
El operador @pre también puede ser utilizado sobre los enlaces de un determinado rol. Por ejemplo, para indicar el conjunto de elementos que estaban vinculados a una orden antes de que se ejecutara el comando system, se podría utilizar la siguiente expresión:

def:anOrder=…
post:
  anOrder.item@pre …

Otro ejemplo con un uso más intenso de este operador es una expresión que obtiene el valor total derivado de una orden antes de que se ejecute el comando del sistema. No sólo pueden haber cambiado las cantidades y los precios de los artículos, sino también la lista de artículos en sí. Por lo tanto, es necesario utilizar el operador @pre tres veces:

def:anOrder=…
post:
  anOrder.item@pre->sum(unitPrice@pre*quantity@pre) …

Si, por otro lado, el analista cree que los valores de los atributos y enlaces no son cambiados por el comando system, entonces la expresión @pre puede ser omitida, como en el siguiente ejemplo:

def:anOrder= …
post:
  anOrder.item->sum(unitPrice*quantity) …

                ​ 8.5.9 Postcondiciones que cubren las colecciones de objetos
Es posible con una sola expresión OCL declarar que un conjunto entero de objetos fue cambiado. Por ejemplo, una expresión que dice que el precio de cada libro fue incrementado en un x% puede ser escrita usando la expresión forAll:
 
Context Livir::raiseBookPrice(x:Percent)
  post:
    self.book->forAll(aBook|
      aBook^setPrice(aBook.price@pre*(1+x))
    )

Si no hay necesidad de usar los valores anteriores en la ecuación, es decir, si cada objeto va a ser actualizado con el mismo precio, entonces es posible abreviar esta notación. Por ejemplo, si el precio de todos los libros tiene que ser fijado a x dólares, entonces la siguiente expresión podría ser usada en su lugar:

Context Livir::setBookPrice(x:Money)
  post:
    self.book->forAll(aBook|
      aBook^setPrice(x)
    )
En este caso, hay una forma aún más abreviada:

Context Livir::setBookPrice(x:Money)
  post:
    book^setPrice(x)

Recuerde que en nuestros ejemplos, el libro es un rol de una asociación del controlador a la clase Book, y por lo tanto es equivalente a self.book, es decir, representa el conjunto de todos los libros que están registrados en el sistema. Como en el caso de la notación ‘.’

                ​ 8.5.10 Postcondiciones y eventos del mundo real
El proceso de creación de restricciones está íntimamente relacionado con la ampliación del caso de uso y el modelo conceptual. El modelo conceptual debe ser utilizado como referencia en todo momento porque es la fuente de información con la que se pueden hacer afirmaciones sobre la información.
Las restricciones deben redactarse siempre con expresiones que puedan interpretarse en términos de elementos del modelo conceptual. Así, afirmaciones como "los libros fueron enviados" difícilmente serían condiciones posteriores porque no representan información contenida en el modelo conceptual; describen eventos del mundo real. Si el equipo desea expresar esto en una restricción, debe crear una estructura conceptual (atributo, rol o concepto) para representarlo. Por ejemplo, el hecho de que los libros fueron enviados podría representarse creando una instancia de la clase Delivery y vinculándola a la instancia actual de Order.

            ​ 8.6 Excepciones
Las excepciones en las restricciones son las condiciones de fallo que el diseñador no puede o no desea evitar antes de ejecutar el propio comando.
A veces, las condiciones identificadas como excepciones pueden convertirse en condiciones previas. Si es posible transformar una excepción en una condición previa, generalmente es aconsejable hacerlo, porque es preferible evitar problemas lo antes posible. Es preferible evitar que el usuario realice una acción equivocada en lugar de permitirle hacerlo y reportar el error más tarde.
OCL no presenta una cláusula específica para gestionar las excepciones, pero se pueden simular en las restricciones mediante condiciones postcondicionales tales como

post:
  if <condition> then
    <raise exception>
  else
    <all other post conditions, including other exceptions>
endif

Como no sería fácil representar muchas excepciones usando este enfoque anidado, usamos una nueva cláusula estereotipada, exception, que es una versión más corta de la expresión anterior:
exception:
  <condition> implies <raise exception>

Ahora, para que una restricción indique una excepción, es suficiente identificar la condición que produce la excepción y nombrar la excepción.
Una restricción sólo indica que pueden ocurrir excepciones, pero su manejo debe ser definido sólo durante el diseño de la interfaz o del nivel de aplicación, porque si una excepción es planteada por el controlador-fachada, debe ser manejada por el nivel inmediatamente superior: el nivel de aplicación o de interfaz.
El siguiente ejemplo muestra una restricción con una excepción basada en las figuras 8.1 y 8.2:.
 
Context Livir::finishOrder(aCartId:CartId, aCustomerId:CustomerId)
  def: aCustomer=customer[aCustomerId]
  def: aCart=cart[aCartId]
  pre:
    aCustomer->notEmpty() and
    aCart->notEmpty()
  post:
    newOrder.isNewInstanceOf(Order) and
    newOrder^addCart(aCart) and
    newOrder^addCustomer(aCustomer) and
    newOrder^setDate(Date.getCurrent()) and
    newOrder^setNumber(OrderNumberGenerator.getNew())
  
exception:
    aCart.item->isEmpty() implies Exception.throw(‘Cannot finish an empty order’)

Aquí, un mensaje de lanzamiento básico se usa para señalar la excepción a una clase llamada Exception, que no es una clase OCL básica. Cuando se genera el código para ese comando, la excepción debe ser señalada al objeto que llamó al comando del sistema (posiblemente un objeto del nivel de la aplicación o de la interfaz), y asumimos que no se obtiene ninguna de las condiciones posteriores.
Una excepción de comando del sistema debe ser una condición que no puede ser resuelta internamente por la implementación del comando del sistema, y que requiere que el control de flujo de ejecución sea devuelto al nivel de la interfaz para que se le pueda pedir al usuario que pruebe otras opciones.
Las excepciones internas de software que un comando del sistema puede manejar internamente no se elevan a la interfaz; por lo tanto, simplemente no se mencionan en las restricciones: se abordarán cuando se diseñen y programen los mecanismos de control interno.
También se asume que cuando se plantea una excepción, el comando no puede ejecutarse y no se obtiene ninguna de sus condiciones posteriores, ya que los datos deben mantenerse en un estado coherente incluso cuando se produce una excepción.
Como se mencionó un poco antes, algunas excepciones pueden convertirse en precondiciones si el diseñador concibe una forma de asegurar la condición antes de llamar el comando. Por lo tanto, la restricción, con una excepción como la que se muestra arriba, podría convertirse en el siguiente:

Context Livir::finishOrder(aCartId:CartId, aCustomerId:CustomerId)
  def: aCustomer=customer[aCustomerId]
  def: aCart=cart[aCartId]
  pre:
    aCustomer->notEmpty() and
    aCart->notEmpty() and
    
aCart.item->notEmpty()
  post:
    newOrder.isNewInstanceOf(Order) and
    newOrder^addCart(aCart) and
    newOrder^addCustomer(aCustomer) and
    newOrder^setDate(Date.getCurrent()) and
    newOrder^setNumber(OrderNumberGenerator.getNew())

En este caso, el comando asume que las operaciones anteriores en el diagrama de secuencia del sistema han comprobado y asegurado que en este punto el carro no está vacío; por lo tanto, el comando no lo comprobará de nuevo. Esto evita que el comando finishOrder realice verificaciones innecesarias cuando se llama, y por lo tanto simplifica su código.
Sólo los elementos conceptuales (conceptos, atributos y asociaciones) pueden aparecer en las expresiones OCL de las restricciones. Estos elementos están necesariamente relacionados con las reglas de negocio del sistema que se está analizando. Las excepciones mencionadas aquí deben ser excepciones relacionadas con las reglas del negocio, y no excepciones relacionadas con problemas de hardware o comunicación. Las excepciones que puedan ocurrir en el almacenamiento físico, la comunicación o los dispositivos externos deben ser abordadas por mecanismos específicos en los niveles a los que pertenecen esos elementos. Por lo general, los usuarios ni siquiera son conscientes de ello.

            ​ 8.7 Restricciones tipo para CRUD
Las siguientes subsecciones presentan modelos de restricciones para comandos CRUD típicos. Hay tres restricciones de comando de sistema y una restricción de consulta de sistema. Los comandos y la consulta se realizan dentro de la clase Book, definida según el modelo de la Figura 8.1. Las restricciones para las operaciones del CRUD son similares y pueden considerarse patrones.

                ​ 8.7.1 Create 
La restricción para un comando create normalmente debería incluir la instanciación de un nuevo objeto, la inicialización de sus atributos obligatorios y la adición de sus enlaces obligatorios. Como ejemplo, el siguiente es una restricción completo para crear un nuevo libro:
 
Context Livir::createBook(anIsbn:ISBN;aTitle,anAuthorsName:String;aPrice:Money;
  aPageCount:Natural;aPublisherName:String;aCoverImage:Image)
  pre:
    publisher[aPublisherName]->notEmpty()
  post:
    newBook.newInstanceOf(Book) and
    newBook^setIsbn(anIsbn) and
    newBook^setTitle(aTitle) and
    newBook^setAuthorsName(anAuthorsName) and
    newBook^setPrice(aPrice) and
    newBook^setPageCount(aPageCount) and
    newBook^setCoverImage(aCoverImage) and
    newBook^addPublisher(publisher[aPublisherName]) and
    self^addBook(newBook)

Esta restricción asume que el nombre del editor ya ha sido verificado y es válido; de lo contrario, esta condición debería ser una excepción en lugar de una condición previa.
Como el atributo isbn ya está estereotipado como único, no es necesario establecer una excepción relacionada con el tema de la creación de un libro con un ISBN existente, porque esa excepción sería planteada por la invariante de clase definida por el estereotipo único. El diseñador puede querer hacer explícito en la restricción que tal excepción existe; sin embargo, es redundante declarar una excepción que ya está definida como invariante, y como la redundancia es una posible fuente de problemas, debe ser evitada.
Sin embargo, si el equipo quiere asegurarse de que el argumento anIsbn pasado al comando es realmente un ISBN que aún no está registrado, puede hacerlo añadiendo una condición previa al restricción. Esto no invalida la excepción que podría ser planteada por la invariante, pero asegura que esta operación específica no va a plantear esa excepción:
 
Context Livir::createBook(anIsbn:ISBN;aTitle,anAuthorsName:String;aPrice:Money;
 
  aPageCount:Natural;aPublisherName:String;aCoverImage:Image)
  pre:
    publisher[aPublisherName]->notEmpty() and
    
book[anIsbn]->isEmpty()
  post:
    newBook.newInstanceOf(Book) and
    newBook^setIsbn(anIsbn) and
    newBook^setTitle(aTitle) and
    newBook^setAuthorsName(anAuthorsName) and
    newBook^setPrice(aPrice) and
   newBook^setPageCount(aPageCount) and
    newBook^setCoverImage(aCoverImage) and
    newBook^addPublisher(publisher[aPublisherName]) and
    self^addBook(newBook)

                ​ 8.7.2 Update
El comando de actualización normalmente sólo implica cambiar el valor de algunos atributos, aunque a veces puede implicar añadir o quitar enlaces. Sin embargo, antes de definir una restricción para actualizar un objeto, el diseñador debe decidir qué atributos y enlaces son inmutables. El estereotipo inmutable añadido a algunos atributos y roles de asociación en la Figura 8.1 declara que esas propiedades no pueden cambiar después de crear un objeto. Sólo tiene sentido cuando se empieza a considerar si los objetos pueden cambiar o no, y el momento de redactar las restricciones es el momento justo para tener en cuenta esa característica. En el caso de un atributo inmutable, su valor puede definirse cuando se crea una instancia, pero no puede modificarse después. Un ejemplo es el ISBN de un libro. Un rol inmutable se refiere a un enlace que normalmente es obligatorio y se añade cuando se crea el objeto. El objeto en ese rol no se puede modificar. Por ejemplo, un artículo está vinculado a un carro cuando se crea y no puede cambiar a otro carro después de eso.
El comando update no puede cambiar atributos y enlaces inmutables. En el caso de un libro de la figura 8.1 sólo se pueden actualizar los siguientes atributos: precio, imagen de portada y cantidadEnStock.
En este caso, la restricción de actualización podría tener el siguiente aspecto:

Context Livir::updateBook(anIsbn:ISBN; aPrice:Money; aCoverImage:Image;
  aQuantity: Natural)
  def: aBook=book[anIsbn]
  pre:
    aBook->notEmpty()
  post:
    aBook^setPrice(aPrice) and
    aBook^setCoverImage(aCoverImage) and
    aBook^setQuantityInStock(aQuantity)

El ISBN sólo se utiliza para encontrar el libro. Pero como es inmutable, no se puede actualizar. Si se pudiera actualizar, entonces se deberían pasar dos valores del ISBN como parámetros: el antiguo ISBN utilizado para localizar el libro, y el nuevo ISBN que reemplazaría al antiguo valor.
Recuerde que los atributos únicos no son claves primarias, como se explica en el Capítulo 6; son sólo atributos con valores que no se repiten en diferentes instancias. Pueden o no ser inmutables dependiendo de la naturaleza del concepto.

                ​ 8.7.3 Delete
El comando que borra un objeto debe considerar las reglas estructurales del modelo conceptual antes de decidir si un objeto puede o no ser destruido.
En el caso de la Figura 8.1, por ejemplo, un ejemplo de Libro no puede ser eliminado sin una decisión sobre lo que sucede con los posibles casos de Ítem eventualmente vinculados a él, porque, desde el punto de vista de un Ítem, un enlace a un Libro es obligatorio.
Para realizar el borrado sin violar ninguna regla estructural, se debe elegir uno de los tres enfoques siguientes:
    • Asegurar, mediante una condición previa, que el objeto que se va a borrar no va a dejar otros objetos incoherentes en relación con el límite inferior de sus asociaciones. Con este enfoque, sólo se pueden seleccionar para su eliminación los libros que no tengan elementos asociados. Esto significa que sólo los libros que nunca fueron vendidos pueden ser borrados.
    • Utilice una excepción para abortar el comando de eliminación si se intenta para un objeto que dejará inconsistentes a otros objetos. Si un usuario intenta borrar un libro que tiene elementos vinculados a él, se levantará una excepción.
    • Asegurar por condición posterior que todos los objetos que se quedarían inconsistentes después del borrado también se borran. En este caso, los items vinculados al libro a eliminar también se eliminarían.
La tercera aproximación se utiliza cuando queremos propagar el comando delete a cada objeto que tiene asociaciones obligatorias con el objeto que se está borrando. Esta propagación es recursiva: la eliminación continuará hasta que no se encuentren más objetos con enlaces obligatorios a objetos que fueron eliminados.7 Este enfoque no siempre se puede utilizar; hay situaciones en las que la propagación de la eliminación va en contra de las reglas del negocio. En el caso de los libros, por ejemplo, la eliminación de elementos vinculados a un libro que se está eliminando crearía problemas con pedidos antiguos que ya están registrados; no es aceptable. Sin embargo, borrar artículos cuando se está eliminando un carro es aceptable, porque si se elimina un carro, las reglas de la empresa esperan que se elimine también toda la información relacionada con sus artículos.
Un posible restricción que utilice el enfoque de precondición se vería como el siguiente:
 
Context Livir::deleteBook(anIsbn:ISBN)
  pre:
    book[anIsbn]->notEmpty() and
    
book[anIsbn].item->isEmpty()

  post: 
    book[anIsbn]^destroy()

Como se indicó anteriormente, el mensaje de destrucción elimina la instancia del Libro, así como sus eventuales enlaces, que no necesitan ser eliminados uno por uno. Las condiciones previas aseguran que el libro existe y que el libro no tiene ningún elemento vinculado a él. Si un libro dado tiene elementos, entonces el comando no puede ser llamado.
Un posible restricción que utiliza el enfoque de excepción sería algo así como lo siguiente:
 
Context Livir::deleteBook(anIsbn:ISBN)
  pre:
    book[anIsbn]->notEmpty()
  post:
    book[anIsbn]^destroy()
  
exception:
  book[anIsbn].item->notEmpty() implies
    self^throw(‘The book cannot be deleted because copies of it have already been sold’)

Un posible restricción que utilice el método de postcondición que propague la eliminación de todos los artículos vinculados a un carro tendría el siguiente aspecto:
 
Context Livir::deleteCart(aCartId:CartId)
 
  pre:
    cart[aCartId]->notEmpty()
  post:
    
cart[aCartId].item^destroy()
 and
    cart[aCartId]^destroy()

La postcondición  anterior establece que, además del carro, también se eliminarán todos los artículos vinculados a él. Como la clase Item no tiene asociaciones con enlaces obligatorios procedentes de otras clases, el proceso de destrucción puede detenerse allí (los libros vinculados a los elementos, por ejemplo, no se destruyen). De lo contrario, sería necesario destruir otros objetos, y eso debería establecerse en la restricción.
La aproximación posterior a la condición debe elegirse cuando sea deseable propagar el borrado a todos los objetos que dependen del objeto que se está borrando. También es útil cuando se borra la agregación compuesta; por definición, todos los componentes deben ser borrados también, a menos que se hayan eliminado previamente de la agregación compuesta.
Sin embargo, como se mencionó anteriormente, hay situaciones en las que esta propagación no es deseable. Por ejemplo, no es posible eliminar un libro del catálogo si ya hay ventas registradas para ese libro. En este caso, debe elegirse la condición previa o los enfoques de excepción. La primera requiere que un libro que no puede ser borrado se impida que su ISBN sea pasado como argumento a ese comando. Por ejemplo, la lista de libros disponibles para ser borrados en la interfaz podría contener sólo aquellos libros que realmente podrían ser borrados. Si esta garantía no es posible o deseable, debe elegirse el enfoque de excepción. En este caso, la interfaz permite al usuario intentar eliminar, y si no es posible, se hace una excepción.
Normalmente, los sistemas de información no permiten que se borre la información. Un libro que se elimina de un catálogo, por ejemplo, no se elimina, sino que se marca como inactivo; si se elimina la información sobre el libro, entonces la información sobre las ventas anteriores no sería coherente con la realidad. Para implementar este enfoque, una solución sencilla es definir un nuevo atributo activo booleano para la clase cuyos miembros pueden ser inactivados en lugar de eliminados. El valor por defecto para este atributo es verdadero, porque el objeto normalmente está activo cuando se crea. En el ejemplo, para la clase Book, la solución se muestra en la Figura 8.4.


Figura 8.4 Una variación de la clase Book cuyas instancias no se pueden borrar, sino que se marcan como inactivas.

En este caso, una restricción para desactivar un libro sería
 
Context Livir::inactivateBook(anIsbn:ISBN)
  pre:
    book[anIsbn]->notEmpty()
  post:
    book[anIsbn]^setActive(false)

No hay necesidad de comprobar si el libro tiene elementos en este caso porque ninguno será borrado.
Otro enfoque es mover objetos inactivos a un espacio diferente, por ejemplo usando una nueva asociación con el controlador que mantiene los objetos inactivos separados de los activos. La Figura 8.5 muestra un ejemplo de este enfoque para la clase Book.

Figura 8.5 Alternativa para representar libros inactivos con dos asociaciones.

En la Figura 8.5 hay dos juegos de libros: (activo) libro e inactivoLibro. La restricción en la clase Libro asegura que un libro pertenece sólo a uno u otro conjunto.
Otro enfoque es utilizar el patrón de diseño de estados para modelar los dos estados de un objeto, como se muestra en la Figura 8.6. De nuevo, hay dos conjuntos de libros; el conjunto habitual de libros (activos) puede ser accedido directamente por una asociación derivada, mientras que el conjunto de libros inactivos de la figura debe ser accedido consultando el conjunto de libros vinculados a las instancias de Inactivo (sin embargo, nada impide la creación de otra asociación derivada para acceder a los libros inactivos si así se desea).


Figura 8.6 Una forma alternativa de representar objetos inactivos utilizando el patrón de diseño de estado.

Este modelo es un poco más complejo visualmente pero evita la necesidad de una restricción. También podría transformarse en un patrón y podría crearse un estereotipo para ello.

                ​ 8.7.4 Recuperación
La simple consulta CRUD recupera los datos disponibles sobre una instancia de un concepto dado que está identificada por uno de sus identificadores únicos. Estas consultas no devuelven datos que no estén explícitamente en la definición de clase. Las consultas que devuelven datos calculados a partir de uno o más objetos son informes (utilice casos estereotipados con informe). Las operaciones de recuperación no realizan cálculos.
Una simple consulta para recuperar el Libro de la clase de la Figura 8.1 podría definirse de la siguiente manera:

Context Livir::retrieveBook(anIsbn:ISBN):Tuple
  body:
    Tuple {
      isbn=anIsbn,
      title=book[anIsbn].title,
      authorsName=book[anIsbn].authorsName,
      price=book[anIsbn].price,
      pageCount=book[anIsbn].pageCount,
      publisherName=book[anIsbn].publisherName,
      coverImage=book[anIsbn].coverImage,
      quantityInStock=book[anIsbn].quantityInStock,
    }

La consulta de recuperación devuelve una tupla o registro con los datos de los atributos del objeto seleccionado por el parámetro de consulta.

            ​ 8.8 Modelos de contratos para listar objetos
Frecuentemente es necesario listar los objetos donde se presentan uno o más atributos. Un primer ejemplo de este tipo da restricción es el listado del título de todos los libros disponibles en la librería:
 
Context Livir::listBook():Set
  body:
    book.title

Como la función de libro del controlador es un conjunto estricto en la Figura 8.1, el resultado de la expresión book.title también será un conjunto. Por lo tanto, si hay dos libros con el mismo título, serán listados una sola vez, incluso si los libros tienen un ISBN diferente.
Si se desea una lista con múltiples columnas (por ejemplo, autor y título), entonces es necesario devolver una colección de tuplas:
 
Context Livir::listBook():Set
  body:
    book->collect(aBook|
      Tuple {
        authorsName=aBook.authorsName,
        title=aBook.title
      }
    )

A veces, es necesario aplicar un filtro a la lista, por ejemplo, devolver sólo el autor y el título de los libros que no tienen ningún elemento vinculado a ellos (libros que nunca se vendieron). En este caso, se puede aplicar el select al conjunto antes de formar las tuplas:
 
Context Livir::listBookNotSold():Set
  body:
    book->select(
      item->isEmpty()
    )->collect(aBook|
      Tuple {
        authorsName=aBook.authorsName,
        title=aBook.title
      }
    )

La mayoría de las consultas de listado probablemente sólo tienen estos dos constructores: seleccionar (filtro) seguido de recoger (proyección). Pero se pueden crear consultas más complejas. En esos casos, no se ajustan necesariamente al patrón de lista (lista) y se consideran informes más complejos (informe).

            ​ 8.9 Restricciones relacionados con casos de uso
Un caso de uso expandido es una cadena de comandos y consultas que se realizarán en una secuencia determinada. Por lo general, cada operación proporcionará información o asegurará las condiciones previas para otras operaciones. El mejor enfoque para escribir restricciones para esta secuencia de operaciones es seguir el flujo de casos de uso que se representa en el diagrama de secuencia del sistema. En esta secuencia, el diseñador debe preguntar:
    • ¿Cuál es el objetivo de cada operación?
    • ¿Qué producen en términos de información?
    • ¿Qué esperan que hayan producido sus predecesores?
    • ¿Qué excepciones podrían ocurrir durante la ejecución?
    • ¿Se pueden reconfigurar sus excepciones como condiciones previas?
    • ¿Sus parámetros incluyen grupos de valores que no son válidos?
    • ¿Siguen las operaciones un patrón conocido?
Al responder a estas preguntas, el diseñador construirá restricciones que permitan que los comandos y consultas se realicen de manera consistente en el contexto de la transacción del caso de uso. Si es necesario añadir nuevas consultas o comandos al diagrama de secuencia para asegurar ciertas condiciones previas, entonces este es el momento adecuado para hacerlo.
Este capítulo muestra muchos ejemplos relacionados con el diagrama de secuencia del sistema de la Figura 8.2. Se anima al lector a revisar esa cifra y a hacer las preguntas anteriores para cada operación, a fin de comprender cómo se han contestado durante el capítulo.

            ​ 8.10 El proceso hasta ahora


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
Implementación


Pruebas/Test


Gestión del Proyecto
Estimar el esfuerzo total, el cronograma ideal y el tamaño medio del equipo para el proyecto.
Estimar la duración y el número de iteraciones para cada fase.
Preparar la fase de planificación y el plan de Iteración para la primera iteración.




            ​ 8.11 Preguntas
1. Explicar y presentar un ejemplo de cómo una excepción puede transformarse en una condición previa y viceversa.
2. ¿Cuál es la diferencia entre las excepciones en las restricciones de comando y en las restricciones de consulta?
3. ¿Cuáles son las cinco posibles postcondiciones, y qué comandos básicos definen cada una de ellas? ¿Cómo pueden estar representados en las restricciones de OCL?
4. Producir la restricción para la consulta searchBook en la Figura 8.2.

1Por ejemplo, después de que un usuario ordena un libro, mientras el usuario está cerrando el pedido y proporcionando el pago, el único libro disponible podría ser vendido a otro usuario. Esto debe evitarse con mecanismos de control de concurrencia, como se explica en el Capítulo 13.
2El tipo Entero representa el conjunto {0, 1, 2, 3, ...}.
3Recuerde que las condiciones de carrera todavía no se están considerando aquí y que podrían invalidar esta condición previa si la concurrencia es un problema.
4Data Transfer Objects es un patrón de diseño que indica que los objetos que pasan por el controlador-fachada a la interfaz y viceversa no pueden ser instancias de clases de dominio (aquellas en el modelo conceptual). Deben ser datos puros, y no objetos de dominio con comportamiento. Esto puede ser implementado con objetos que sólo tienen atributos y sus respectivos getters y setters (si los hay), nada más. El tipo de registro en Pascal y la Tupla OCL son ejemplos de DTOs.
5La OCL y el operador también pueden utilizarse para combinar condiciones previas, excepciones e invariantes.
6Algunos dialectos pueden usar unset.
7 De hecho, en el caso general, el límite inferior de la función es la información que debe considerarse. Por ejemplo, si un rol tiene multiplicidad 3..*, que quitar un enlace cuando sólo quedan 3 hace que el objeto sea inconsistente.t.