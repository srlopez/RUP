# PRUEBAS UNITARIAS

Este capítulo explica cómo se puede probar el software orientado a objetos desarrollado con las técnicas mostradas en los capítulos anteriores. Específicamente, se presentan tres niveles de pruebas: pruebas unitarias para métodos y clases, pruebas de funcionamiento del sistema y pruebas de casos de uso. El capítulo se centra en el enfoque funcional de las pruebas basado en las restricciones de operación. Para cada parámetro de un sistema o de una operación básica, el diseñador debe definir si tiene valores aceptables y/o inaceptables. Se debe crear una prueba de éxito para cada escenario de éxito y una prueba de fracaso para cada conjunto de valores inaceptables. Con este enfoque se pueden diseñar sistemáticamente casos de prueba. También se presentan la partición de equivalencia y el análisis de valores límite para determinar las mejores opciones para los casos de prueba.

                ​ Palabras clave
Unit test; system operations test; system test; test-driven development; functional test

            ​ Conceptos en este Capítulo

    • Pruebas funcionales
    • Stubs y drivers
    • Desarrollo impulsado por pruebas
    • Pruebas unitarias
    • Pruebas de funcionamiento del sistema
    • Pruebas de casos de uso

            ​ 11.1 Introducción a los test
No importa cuán sofisticadas sean las técnicas de modelado y especificación utilizadas para desarrollar software, no importa cuán disciplinado y competente sea el equipo, hay un factor que hace que las pruebas de software siempre sean necesarias: el error humano. Es un mito pensar que los buenos desarrolladores que trabajan con herramientas de última generación son capaces de desarrollar software libre de errores (Beizer, 1990).
La Ley de Murphy (Bloch, 1980) en muchos de sus corolarios parece hablar directamente a la industria del software. Por ejemplo:
    • Cualquier cosa que pueda salir mal, saldrá mal.
    • Si todo parece estar bien, no lo has comprobado adecuadamente.
    • La naturaleza siempre se pone del lado del defecto oculto.
Durante muchos años, las actividades de pruebas de software se consideraron un castigo para los programadores. Las pruebas se consideraron una pérdida de tiempo porque se suponía que el software era correcto desde el principio.
Sin embargo, las cosas han cambiado. La disciplina de prueba ahora se considera extremadamente importante. Hoy en día es una parte integral del proceso de desarrollo de software y una de las disciplinas del Proceso Unificado.
Además, las principales empresas de desarrollo de software comenzaron a subcontratar las pruebas de software, mediante la contratación de fábricas de pruebas. Esto significa que no sólo los desarrolladores, sino también los equipos están especialmente capacitados para realizar pruebas.
Este capítulo presenta las actividades de prueba que están fuertemente adaptadas para su uso con las técnicas mostradas en los capítulos anteriores.
Las pruebas de unidad se utilizan básicamente para comprobar el comportamiento de las clases, incluyendo sus métodos básicos y delegados. Si se utiliza la generación automática de código, tales pruebas pueden ser suprimidas, porque se supone que los generadores automáticos de código no cometen errores humanos.
Las pruebas de funcionamiento del sistema son pruebas funcionales de alto nivel que pueden basarse en el examen del  contrato de funcionamiento del sistema: sus parámetros, condiciones previas y excepciones determinan conjuntos de parámetros válidos e inválidos que deben verificarse sistemáticamente, y las condiciones posteriores determinan los resultados que deben lograrse cuando se prueban las entradas válidas.
Finalmente, las pruebas del sistema se realizan como pruebas de casos de uso sistemático. Cada caso de uso es un script que establece flujos normales y alternativos para lograr los objetivos de negocio. Las pruebas de casos de uso pueden ser ejecutadas manualmente o pueden ser automatizadas. Si el cliente realiza pruebas de casos de uso, se denominan pruebas de aceptación.
Existen dos categorías principales de técnicas de prueba:
    • Pruebas estructurales, que evalúan la estructura interna del código.
    • Pruebas funcionales, que evalúan las operaciones basándose únicamente en sus entradas y salidas.
En este libro, sólo se introducen técnicas funcionales aplicadas específicamente a los tres niveles de pruebas:
    • Test unitario de funcionamiento para operaciones básicas y delegadas.
    • Pruebas funcionales de funcionamiento del sistema basadas en restricciones.
    • Pruebas de sistema y aceptación basadas en casos de uso del sistema.
Los lectores interesados en comprender con más detalle las pruebas automatizadas deben echar un vistazo al libro de Meszaros (2007), que presenta un conjunto significativo de patrones de pruebas de estilo xUnit, una familia de frameworks para innumerables lenguajes basados en el diseño creado originalmente por Kent Beck (1989)..

            ​ 11.2 Pruebas Funcionales
La prueba funcional consiste en una secuencia de pruebas que definen los valores de entrada de una operación y observan si el resultado es el esperado. Las pruebas funcionales se pueden realizar sin conocer el código de programación que implementa la operación; sólo se observa su comportamiento. La cantidad de pruebas a realizar para asegurar que una operación es correcta puede ser virtualmente infinita. Las pruebas funcionales pueden utilizar técnicas para reducir el número de pruebas necesarias sin perder cobertura. Las técnicas más útiles para lograr ese objetivo son la partición de equivalencia y el análisis de valores límite, que se explican en las siguientes subsecciones.

                ​ 11.2.1 Partición de equivalencia
Uno de los principios de las pruebas funcionales es la identificación de situaciones equivalentes. Por ejemplo, si una operación acepta un conjunto de datos (normalidad) y rechaza otro conjunto (excepción), puede decirse que hay dos conjuntos de equivalencias1 de datos de entrada para esa operación: valores aceptados y rechazados. Por lo general, es imposible probar todos los valores incluidos en esos conjuntos, ya que pueden ser prácticamente infinitos. Por lo tanto, la técnica de división de equivalencia indica que se debe probar al menos un elemento de cada conjunto de equivalencias (Burnstein, 2003).
Clásicamente, la técnica de partición de equivalencia considera la división de las entradas a través de los siguientes criterios (Myers, Sandler, Badgett y Thomas, 2004):
    • Si los valores válidos se especifican como un intervalo (por ejemplo, de 10 a 20), se define un set válido (de 10 a 20) y dos sets no válidos (menos de 10 y más de 20).
    • Si los valores válidos se especifican como una cantidad de valores (por ejemplo, una lista con cinco elementos), se define un set válido (lista con cinco elementos) y dos sets no válidos (listas con menos de cinco elementos y listas con más de cinco elementos).
    • Si las entradas válidas se especifican como un conjunto de valores aceptables que pueden ser procesados en diferentes formas (por ejemplo, las cadenas de una enumeración como "hombre" y "mujer"), entonces definimos un conjunto válido para cada una de las opciones válidas y un conjunto no válido para cualquier otro valor.
    • Si los valores válidos están especificados por una condición lógica (por ejemplo, "la fecha final debe ser mayor que la fecha inicial"), se debe definir un set válido (cuando la condición es verdadera) y un set no válido (cuando la condición es falsa).
Los conjuntos de datos de entrada válidos pueden definirse no sólo en términos de restricciones sobre los datos de entrada, sino también en términos de los resultados que pueden producirse. Si la operación que se está probando tiene un comportamiento diferente dependiendo del valor de la entrada, se deben definir diferentes conjuntos válidos para cada comportamiento. Por ejemplo, considere una operación simple mitad(x:Entero):Entero. Esta operación acepta que x puede ser cualquier número positivo. Tenga en cuenta también que la operación está definida de forma que no puede aceptar números cero o negativos. Finalmente, considere que la operación produce (x-1)/2 para los números impares y x/2 para los pares. Por lo tanto, debemos considerar que la mitad tiene tres conjuntos de equivalencias para el parámetro x:
    • Un conjunto válido compuesto de enteros positivos impares: 1, 3, 5, .....
    • Un conjunto válido compuesto de enteros positivos: 2, 4, 6, .....
    • Un conjunto inválido compuesto de números enteros no positivos: 0, -1, -2, -3, ......
Los valores del conjunto de equivalencias deben limitarse siempre al dominio definido por el tipo de parámetro. Por ejemplo, si el tipo de parámetro no fuera un número entero, se definirían diferentes conjuntos de equivalencias. Si la operación era half(x:Natural):Integer, entonces los conjuntos de equivalencias deben redefinirse para que permanezcan dentro del dominio Natural, que no incluye números cero y negativos:
    • Un conjunto válido compuesto de enteros positivos impares: 1, 3, 5, .....
    • Un conjunto válido compuesto de enteros positivos: 2, 4, 6, .....
    • No hay sets inválidos.
Por otro lado, supongamos que la operación se define con un tipo de parámetro más amplio como half(x:Real):Integer; entonces los conjuntos de equivalencias serían:
    • Un conjunto válido compuesto de enteros positivos impares: 1, 3, 5, .....
    • Un conjunto válido compuesto de enteros positivos: 2, 4, 6, .....
    • Un conjunto inválido compuesto de números no naturales: .
Podemos ver en los ejemplos anteriores que si el diseñador restringe el tipo de parámetro tanto como sea posible, entonces se definen menos o más sencillos conjuntos de equivalencias no válidos. Es por eso que los ejemplos de los capítulos anteriores utilizan el tipo Natural en lugar de Entero cuando los números cero o negativos no pueden ser aceptados. Y es por eso que las enumeraciones deben ser utilizadas en lugar de cadenas sin restricciones siempre que sea posible..

                ​ 11.2.2 Análisis de valores límite
La gente que trabaja en pruebas de software solía decir que los errores (de software) se esconden en las rendijas. Debido a esto, la técnica de partición de equivalencia se utiliza normalmente junto con otra técnica conocida como análisis de valores límite.
El análisis de valores límite consiste en no elegir ningún valor aleatorio de un conjunto de equivalencias, sino dos o más valores límite si se pueden determinar.
En los dominios ordenados, como los números, se puede aplicar este criterio. Por ejemplo, si una operación requiere un parámetro entero que es válido sólo si está incluido en el intervalo[10..20], entonces hay tres conjuntos de equivalencias:
    • No es válido para cualquier x<10.
    • Válido para x≥10 y x≤20.
    • No es válido para cualquier x>20.
El análisis del valor límite sugiere que los eventuales errores en la lógica de un programa no se encuentran en puntos arbitrarios dentro de esos intervalos, sino en los puntos límite donde se encuentran dos intervalos. Por lo tanto, si el dominio del parámetro es Entero:
    • Para la primera clase no válida, se debe probar el valor 9.
    • Para la clase válida, se deben probar 10 y 20.
    • Para la segunda clase no válida, se debe probar el valor 21.
Por lo tanto, si hay un error lógico en la operación de algunas de estas entradas, es mucho más probable que se encuentre de esta forma que si se elige un valor aleatorio dentro de cada intervalo que defina un conjunto de equivalencias..

            ​ 11.3 Stubs y drivers
Frecuentemente, las partes del software deben ser probadas separadamente del cuerpo principal del código, pero al mismo tiempo deben comunicarse con otras partes.
Cuando un componente A que va a ser probado llama a operaciones de un componente B que aún no ha sido implementado, el componente B puede ser reemplazado por una versión simplificada del mismo que implementa sólo el comportamiento que es absolutamente necesario para realizar la prueba del componente A. Esta implementación simplificada que se utiliza en lugar de un componente que aún no ha sido implementado se llama un stub.
Por ejemplo, supongamos que una clase A necesita un generador de números primos B que todavía no se ha implementado. El enésimo número primo sería generado por una función primo(n:Natural):Natural. Una versión simplificada de B puede ser implementada sólo para permitir que la clase A sea probada. Supongamos que los primeros cinco números primos son suficientes para probar adecuadamente la clase A. Por lo tanto, un talón para B podría ser implementado de la siguiente manera:
 
CLASS B

STUB METHOD prime(n:Natural):Natural
CASE n OF
1: RETURN 2
2: RETURN 3
3: RETURN 5
4: RETURN 7
5: RETURN 11
OTHWERWISE Exception.throw(‘Stub implementation
requires argument less or equal to 5’)
END CASE
END STUB METHOD
 
END CLASS

De esta manera, la clase A puede ser probada sin invertir tiempo en implementar una función más compleja en la clase B.
Por otro lado, las operaciones implementadas en la clase A serán llamadas por otros componentes del sistema. Pero cuando se está probando la clase A, es posible que estos componentes no existan todavía. Además, si estamos probando la clase A, normalmente deseamos que esa prueba se realice de forma sistemática y reproducible. Para asegurar esto, se puede implementar un controlador de prueba para la clase A. El controlador es un componente del código (posiblemente una nueva clase) que tiene como objetivo único probar sistemáticamente un componente.
Para la clase A mencionada anteriormente, un controlador podría implementarse como una nueva clase llamada Driver4A, por ejemplo. En el apartado 11.5 se muestra un ejemplo de driver.
Por lo tanto, los stubs y drivers son implementaciones simples que simulan el comportamiento de otros componentes. El stub se utiliza en lugar de un componente que debería llamarse pero que todavía no se ha implementado. El driver se utiliza en lugar de un componente que debería llamar al componente que debe someterse a ensayo de manera sistemática y reproducible.
Los stubs son generalmente códigos desechables. Cuando se implementa el componente real, el stub ya no es necesario y puede ser desechado.
Por otro lado, los drivers son piezas importantes de código que deben ser guardadas para siempre. Cada vez que un componente debe ser probado - y esto ocurre frecuentemente durante el desarrollo y la evolución del software - el controlador estaría disponible para realizar automáticamente la prueba.

            ​ 11.4 Desarrollo impulsado por pruebas TDD
El desarrollo basado en pruebas o TDD (Beck, 2003) es una técnica y una filosofía de programación que incorpora las pruebas automáticas al proceso de producción de código. Funciona así:
1. Primero, el programador que recibe la especificación para una nueva funcionalidad que debe ser implementada debe crear un conjunto de pruebas automáticas para el código que aún no existe.
2. Este conjunto de pruebas debe ser ejecutado y observado para que falle. Esto se hace para mostrar que las pruebas no tendrán éxito a menos que se implemente una nueva característica en el código. Si la prueba pasa en este momento hay dos explicaciones: o bien la prueba está mal escrita o bien la característica que se está probando ya está disponible en el código, suponiendo que se trata de una actualización del código existente que se está produciendo y no de código nuevo desde cero.
3. Entonces, el código debe ser desarrollado con el único objetivo de pasar las pruebas. Si se detecta cualquier otra característica, entonces las pruebas deben ser actualizadas antes de ser introducidas en el código. En ese caso, el proceso se reinicia desde el paso 1.
4. Después de que el código pasa todas las pruebas, debe ser limpiado y mejorado si es necesario para cumplir con los estándares de calidad internos. Después de pasar las pruebas finales se considera estable y puede ser integrado en el cuerpo principal del código del sistema.
Las restricciones que se desarrollaron en el Capítulo 8 y los modelos dinámicos del Capítulo 9 son fuentes excepcionales de información para desarrollar casos de prueba completos y consistentes antes de producir cualquier código, como se explica en las siguientes secciones.
La motivación de TDD es incentivar al programador para que mantenga el código simple y produzca un activo de prueba que permita que cualquier parte del sistema se pruebe automáticamente..


            ​ 11.5 Pruebas unitarias
Las pruebas unitarias son las más elementales y consisten en verificar si un componente (unidad) individual del software fue implementado correctamente. Ese componente puede ser un método complejo o una clase entera. Normalmente, esta unidad sigue desconectada del sistema con el que se integrará posteriormente.
Las pruebas unitarias suelen ser realizadas por el programador y no por el equipo de pruebas. TDD requiere que el programador desarrolle el código de prueba antes de escribir el código que se va a probar. Este código de prueba es un conductor que debe generar sistemáticamente el conjunto de datos necesarios para probar todos los conjuntos de equivalencia válidos e inválidos, aplicando el análisis de valores límite cuando sea posible.
Un ejemplo de prueba unitaria consiste en comprobar si un método se ha implementado correctamente en una clase. Vuelva a ver la Figura 10.13 y delegue el método 3.2, incrementItem(aBook:Book; aQuantity:Natural), que debe implementarse en la clase Cart.
Ahora consideremos cuáles son los conjuntos de equivalencias para estos parámetros. Primero consideremos el parámetro aBook:Book. Como el tipo de parámetro es Book, se puede asumir que no se puede pasar ningún otro tipo de objeto como argumento. Por ejemplo, esta operación nunca recibiría una instancia de Cliente o Entrega en lugar de un Libro2 porque los mecanismos de escritura en lenguaje lo evitarían. El equipo debe preocuparse de si los objetos que se pueden recibir aquí son válidos o no.
Si los mecanismos del lenguaje no pueden impedir que un método reciba un valor nulo como parámetro, entonces el caso nulo siempre se considerará un conjunto de equivalencias (normalmente no válido) para cualquier parámetro que se escriba con un nombre de clase.
El método incrementItem fue desarrollado con el siguiente objetivo: incrementar la cantidad de un artículo que ya está en el carrito. Podemos empezar por considerar que hay tres conjuntos de equivalencias para el parámetro aBook:
    • Un conjunto de equivalencias válido que contiene instancias de Book que están vinculadas a un ítem en un Cart.
    • Un conjunto de equivalencias inválido que contiene instancias de Book que no están vinculadas a ningún ítem en un Cart.
    • Un set de equivalencia no válido que contiene sólo el valor nulo.
El segundo parámetro de incrementItem es un número natural identificado como aQuantity. La operación supone que la cantidad existente de la posición que ya está en el pedido se incrementará en aQuantity. El tipo Natural no incluye cero y por lo tanto esa cantidad potencialmente inválida no se permite como argumento. Sin embargo, pedir un número de copias de un libro que exceda su cantidad en stock podría considerarse una condición de error a menos que el sistema permita pedir libros que aún no estén disponibles. Suponiendo que la operación del sistema add2Cart que llama incrementItem no ha definido como condición previa que la cantidad de la orden esté disponible en stock (véase su restricción en la siguiente sección), entonces la operación incrementItem puede recibir cantidades no válidas en relación con esa regla de negocio. Por lo tanto, se pueden considerar los siguientes conjuntos de equivalencias para el parámetro aQuantity:Natural:
    • Un conjunto de equivalencias válido que incluye valores naturales que sumados a la cantidad del artículo respectivo producen un resultado que es menor o igual al atributo quantityInStock de un Libro.
    • Un conjunto de equivalencias inválido que incluye todos los valores naturales que añadidos a la cantidad del artículo respectivo son mayores que el atributo quantityInStock de un Libro.
Los posibles casos de prueba para incrementItem son combinaciones de los conjuntos de equivalencia para los dos parámetros, como se muestra en el cuadro 11.1.

Tabla 11.1
Combinaciones del Conjunto de Equivalencia para IncrementItem

Sólo hay una condición de éxito, que se obtiene cuando se obtienen valores válidos para ambos parámetros. Esto sucede cuando un Libro está vinculado a un artículo en el carrito y aQuantity más la cantidad actual es menor o igual a la cantidad en stock. En OCL esa condición puede ser expresada en el contexto de aCart como
self.item.book->include(aBook) and
self.item->select(book=aBook).quantity+aQuantity<=aBook.quantityInStock
Aunque hay cinco combinaciones en la Tabla 11.1 que producen fallas, sólo tres tienen que ser probadas porque si el libro no está vinculado a ningún ítem o si el libro es nulo, el valor de aQuantity no puede ser determinado como válido o inválido porque no hay una cantidad actual que pueda ser comparada con él. Por lo general, las reglas para obtener combinaciones para las pruebas son:
    • Obtenga todas las combinaciones de éxito y defina un caso de prueba para cada una de ellas.
    • Obtenga un conjunto inválido a la vez. Incluso si la operación tiene n parámetros, considere sólo un conjunto no válido para un solo parámetro a la vez. Los demás parámetros deben ser válidos o debe ser imposible determinar su validez.
    • Sólo se aceptará una combinación con más de un conjunto no válido si esa combinación es posible y útil.
Por lo tanto, hay tres pruebas de falla que deben realizarse para determinar cómo se comporta incrementItem con parámetros no válidos. La primera ocurre cuando un Libro no está en un Carrito. La segunda ocurre cuando un Libro es nulo. La tercera ocurre cuando la cantidad deseada supera la cantidad en stock:
(1) not self.item.book->include(aBook)
(2) aBook.isNull()
(3) self.item->select(book=aBook).quantity+aQuantity > aBook.quantityInStock
Con el fin de evitar pruebas que dejan efectos secundarios en el sistema, generalmente se realizan en tres pasos:
1. Prepara el escenario para la prueba. Por lo general, se crean objetos especiales llamados accesorios con el único propósito de permitir que se realice la prueba.
2. Ejecute la prueba.
3. Limpiar el entorno. El sistema debe volver al estado en que se encontraba antes de la prueba. Las instalaciones deben ser eliminadas en este punto.
Consideremos primero el escenario de prueba de éxito para incrementItem. Cualquier accesorio creado para esta prueba debe ser evaluado como verdadero para la condición de éxito mencionada anteriormente. Un ejemplo de código para generar estos dispositivos es el siguiente:
 
CLASS Driver4Cart
METHOD testIncrementItemSuccess()
FIXTURE VAR aBook:Book
FIXTURE VAR aCart:Cart
FIXTURE VAR anItem:Item
aBook:=Book.Create(‘0752201360’,
’Bring me the head of Willy the mailboy!’, ’Scott Adams’,
US$12.30, 128, 5) -- quantity in stock is 5.
aCart:=Cart.Create() -- cart id is assigned internally
anItem:=Item.Create(aBook,aCart,3)
…
Como vamos a probar la clase Cart es posible que algunos de sus métodos o métodos de otras clases como Book and Item no estén todavía implementados. En ese caso, se pueden utilizar aquí los stubs para permitir que se realice la prueba de incrementItem.
Después del código de inicialización, se puede realizar la prueba en sí.:
…
aCart.incrementItem(aBook,2) -- using limit value analysis
IF anItem.getQuantity()=5 THEN
Write(‘incrementItem success test: successful’)
ELSE
Write(‘incrementItem success test: failed’)
ENDIF
…
Por último, debemos deshacernos de las fixtures instaladas.
…
anItem.destroy()
aCart.destroy()
aBook.destroy()
END METHOD

Ahora, las condiciones de falla deben ser probadas también. Aquí, se implementan como tres métodos independientes en la clase Driver4Cart:

…
METHOD testIncrementItemFailure1 ()
-- not self.item.book->includes(aBook)
FIXTURE VAR aBook:Book
FIXTURE VAR aCart:Cart
aBook:=Book.Create(‘0752201360’,
’Bring me the head of Willy the mailboy!’, ’Scott Adams’,
US$12.30, 128, 5)
aCart:=Cart.Create() -- the book is not in the cart
TRY
aCart.incrementItem(aBook,2)
Write(‘incrementItem failure test 1: failed’)
CAPTURE Exception.itemAbsent
Write(‘incrementItem failure test 1: successful’)
END TRYCAPTURE
aCart.destroy()
aBook.destroy()
END METHOD
METHOD testIncrementItemFailure2 ()
-- aBook.isNull()
FIXTURE VAR aBook:Book
FIXTURE VAR aCart:Cart
aCart:=Cart.Create() -- the book is null
TRY
aCart.incrementItem(aBook,2)
Write(‘incrementItem failure test 2: failed’)
CAPTURE Exception.bookIsNull
Write(‘incrementItem failure test 2: successful’)
END TRYCAPTURE
aCart.destroy()
END METHOD
METHOD testIncrementItemFailure3 ()
-- item->select(book=aBook).quantity+aQuantity > aBook.quantityInStock
FIXTURE VAR aBook:Book
FIXTURE VAR aCart:Cart
FIXTURE VAR anItem:Item
aBook:=Book.Create(‘0752201360’,
’Bring me the head of Willy the mailboy!’, ’Scott Adams’,
US$12.30, 128, 5) -- quantity in stock is 5.
aCart:=Cart.Create() -- cart id is filled internally
anItem:=Item.Create(aBook,aCart,3))
TRY
aCart.incrementItem(aBook,3) -- limit analysis
Write(‘incrementItem failure test 3: failed’)
CAPTURE Exception.quantityAboveStock
Write(‘incrementItem failure test 3: successful’)
END TRYCAPTURE
anItem.destroy()
aCart.destroy()
aBook.destroy()
END METHOD
 
END CLASS

El estilo del código del caso de prueba depende del lenguaje y del framework utilizado. Aquí se ilustra una implementación de pseudocódigo genérico para permitir que la lógica de la prueba sea entendida por lectores con conocimientos sobre lenguajes de programación pero no necesariamente con experiencia en frameworks de prueba.
Como podemos ver en el código anterior, los dispositivos y los procedimientos de prueba son usualmente similares, y por lo tanto se pueden utilizar métodos uniformes y parametrizados para crear dichos objetos, reduciendo la cantidad de código que se está produciendo. Esto lo proporcionan normalmente los frameworks como xUnit.
Las pruebas unitarias pueden ser extremadamente minimizadas si se utiliza un generador automático de código para generar las operaciones básicas y los métodos de delegación. En ese caso, se puede asumir que el código es correcto porque el generador no comete errores humanos. La prueba podría comenzar a nivel de operaciones del sistema, lo que se explica en la siguiente sección.

            ​ 11.6 Pruebas de operaciones del sistema
El nivel superior de las pruebas funcionales se produce cuando el equipo verifica si las operaciones del sistema funcionan realmente de acuerdo con las especificaciones del contrato.
Las operaciones del sistema pueden llamar a métodos de muchas clases, delegar responsabilidades y coordinar la ejecución de los métodos básicos y de delegación. Así, a nivel de integración de las clases que realizan un conjunto consistente de responsabilidades, la prueba de operación del sistema verifica si cada operación del sistema implementa correctamente su restricción.
La prueba de funcionamiento del sistema consiste, pues, en verificar si en condiciones normales (las condiciones previas son verdaderas y las excepciones falsas), se obtienen realmente las condiciones posteriores deseadas, y si en condiciones anormales, las excepciones son efectivamente lanzadas. Las pruebas de funcionamiento del sistema son muy similares a las pruebas unitarias, excepto que ahora la operación tiene una restricción, lo que facilita la identificación de los casos de prueba necesarios.
Veamos ahora el funcionamiento del sistema add2Cart en la Figura 10.13. Su restricción fue definido en el Capítulo 8 y es el siguiente:

 Context Livir::add2Cart(aCartId:CartId, anIsbn:Isbn, aQuantity:Natural)

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
exception:
anItem.quantity+aQuantity > aBook.quantityInStock implies
Exception.throw(‘quantity not available’)

La condición previa aCart->notEmpty() implica que hay un conjunto no válido para el parámetro aCartId. La condición previa aBook->notEmpty() implica que hay un conjunto no válido para el parámetro anIsbn. Finalmente, la excepción en esa restricción establece que también hay valores no válidos para aQuantity.
En cuanto a los valores válidos, cada parámetro debe tener al menos un conjunto de equivalencias válido, de lo contrario el método siempre fallaría. Sin embargo, como las condiciones posteriores son condicionales (incluyen una estructura if-then-else-endif), hay al menos dos comportamientos posibles para esta operación, y esto define dos conjuntos de equivalencias válidos: uno cuando un elemento está vacío y otro cuando un elemento no está vacío. Los casos de prueba para esta operación del sistema se presentan en la Tabla 11.2.

Tabla 11.2
Casos de prueba funcional para la operación de un sistema

Type
Condition to Be Tested
Expected Result
Success
aCart->notEmpty() and
aBook->notEmpty() and
anItem->isEmpty() and
aQuantity <=
  aBook.quantityInStock
aCart.item->
  select(book=aBook).quantity=
  aQuantity
Success
aCart->notEmpty() and
aBook->notEmpty() and
anItem->notEmpty() and
anItem.quantity+aQuantity <=  
  aBook.quantityInStock
anItem.quantity=
  anItem.quantity@pre+
  aQuantity
Exception
aCart->isEmpty()
‘There is no such cart’
Exception
aBook->isEmpty()
‘There is no such book’
Exception
anItem->notEmpty() and
anItem.quantity+aQuantity <=  
  aBook.quantityInStock
‘Quantity not available’

También se pueden probar combinaciones de condiciones excepcionales. Por ejemplo, una situación que no aparece en la Tabla 11.2 es cuando tanto el ISBN como el ID del carro son inválidos. Si ese es el caso, sólo se plantearía una de las excepciones en cualquier caso. Además, como ya se ha mencionado, a veces las condiciones no válidas no son compatibles. Por ejemplo, si el ISBN no es válido, no hay cantidadEnStock que comparar con la cantidad pedida y, por lo tanto, las excepciones correspondientes nunca podrían producirse juntas.
Esta es la razón por la que las únicas combinaciones que se prueban son las que sólo incluyen condiciones de éxito o sólo una condición de fracaso combinada con condiciones de éxito. Sin embargo, si el equipo encuentra fácil y seguro añadir nuevas variaciones que incluyan combinaciones de condiciones de fallo no válidas que puedan ser implementadas.
Por lo tanto, aunque no todas las combinaciones se prueban, es necesario probar al menos:
    • Todas las combinaciones posibles de sets de equivalencia válidos.
    • Todas las combinaciones de un set de equivalencia no válido con sets válidos.
Esto significa que después de probar las combinaciones válidas, el programador debe incluir un conjunto inválido a la vez para la prueba de excepción.
El código para el funcionamiento del sistema de pruebas es muy similar al que se presenta para las pruebas unitarias: los dispositivos deben crearse antes de cada prueba, las pruebas de éxito y de fallo se ejecutan, y el entorno se limpia después de cada prueba.

            ​ 11.7 Pruebas de casos de uso (Pruebas de sistema, aceptación y ciclo de negocio)
Las pruebas de casos de uso consisten en seguir manual o automáticamente todos los flujos posibles de un caso de uso y comprobar si se obtienen los resultados deseados (normalmente indicados como condiciones posteriores al caso de uso).
Si el equipo de desarrollo ejecuta la prueba en un único caso de uso, se trata de una prueba del sistema. Si la prueba es realizada por la cliente o bajo su supervisión, entonces es una prueba de aceptación. Si todo un conjunto de casos de uso del sistema relacionados con un caso de uso de negocio se realizan en una secuencia lógica como la definida por el diagrama de actividad de negocio, entonces se trata de una prueba de ciclo de negocio.
El test de caso de uso tiene como objetivo verificar si la versión actual del sistema realiza correctamente los procesos del caso de uso desde el punto de vista de un usuario que realiza una secuencia de operaciones del sistema en una interfaz (no necesariamente una interfaz gráfica) y es capaz de obtener los resultados esperados.
La prueba de caso de uso puede entenderse como una ejecución sistemática de los flujos de casos de uso. Si cada una de las operaciones y consultas del sistema ya ha pasado sus propias pruebas, se debe verificar que el flujo principal y los flujos alternativos del caso de uso se puedan realizar correctamente y que produzcan los resultados deseados..
Es posible automatizar estas pruebas para que puedan ser realizadas por un robot de pruebas que llame directamente al controlador o simule las acciones del usuario en la interfaz gráfica.
Considere, por ejemplo, una prueba de sistema que debe realizarse para evaluar el caso de uso de la Figura 5.7, reproducida aquí como Figura 11.1.


Caso de uso 01: Pedir Libros
    1. El cliente proporciona palabras clave para la búsqueda de libros.
    2. El sistema genera una lista de libros a la venta que coincide con las palabras clave, incluyendo al menos título, autor, precio, número de páginas, editorial, ISBN e imagen de portada. 
    3. El cliente selecciona los libros de la lista e indica la cantidad deseada para cada uno. 
    4. El sistema genera el resumen de la orden (título, autor, cantidad, precio unitario y subtotal para cada libro) y el valor total. 
    5. El cliente finaliza el pedido. 
Excepción 3a: La cantidad solicitada es superior a la cantidad en stock de uno o más libros. 
3a. I. El sistema informa las cantidades disponibles para cada libro en el que el usuario ha pedido más de lo que está disponible. 
3a.2. El usuario cambia las cantidades deseadas para cumplir con las cantidades en stock.* 
3a.3. Avance al paso 4. 
Excepción 5a: El cliente aún no está identificado. 
5a.1 . El cliente proporciona una identificación válida. 
5a.2. Vuelva al paso 5.  
Excepción 5b: El cliente no tiene una cuenta. 
5b.1 . El cliente se registra proporcionando un nombre de usuario, una contraseña y una dirección de correo electrónico. 
5b.2. Volver al paso 5. 
Excepción 5c: No se seleccionó ningún libro para la compra. 
5c.1. Volver al paso I.  
Variante 5d: El cliente decide seguir comprando. 
5d.1 . Vuelva al paso 1
Figura 11.1 Caso de uso de referencia.

Una prueba de caso de uso trataría con escenarios que son exitosos pero que recorren caminos diferentes. En primer lugar, el flujo principal del caso de uso debe considerarse como un escenario base a efectos de prueba. Entonces, cada variante o excepción puede ser incluida una a la vez para probar escenarios alternativos. Esto es lo mínimo que se espera de un paquete de pruebas de casos de uso. Las combinaciones de excepciones y variantes también se pueden probar si el equipo las considera útiles y viables.
La técnica para elaborar pruebas de casos de uso consiste entonces en seleccionar un conjunto de trayectorias que pasan al menos una vez por cada variante y flujo de excepción. Los casos de prueba para el ejemplo de la figura 11.1 pueden definirse como sigue:
• 1,2,3,4,5.
• 1,2,3a(1,2,3),4,5.
• 1,2,3,4,5a(1).
• 1,2,3,4,5b(1).
• 1,2,3,4,5c(1),1,2,3,4,5.
• 1,2,3,4,5d,1,2,3,4,5.
El plan de pruebas del sistema para el caso de uso de la figura 11.1 se muestra en la tabla 11.3..

Tabla 11.3
Ejemplo de un plan de prueba para un caso de uso


Objetivo
Ruta
Cómo probar
Resultado
Flujo principal   
1,2,3,4,5 
 Un cliente previamente identificado busca y selecciona al menos un libro y termina el pedido. 
Se crea un pedido con los libros seleccionados. 
Excepción 3a
1,2,3a(1,2,3)4,5
Un cliente previamente identificado busca y selecciona una cantidad de al menos un libro que esté sobre stock. Luego cambia la cantidad para cumplir con el stock y termina el pedido.
Se crea un pedido con los libros seleccionados. 
Excepción 5a
1,2,3,4,5,5a(1).
Un cliente registrado que aún no ha sido identificado busca y selecciona al menos un libro. Ella provee identificación y termina la orden. 
Se crea una orden con los libros seleccionados. 
Excepción 5b
1,2,3,4,5,5b(1).
Un cliente no registrado busca y selecciona al menos un libro. Se registra y termina la orden. 
Se crea un pedido con los libros seleccionados. Se crea un registro para un nuevo cliente. 
Excepción 5c
1,2,3,4,5,50(11,1,2,3,4,5.) 
Un cliente previamente identificado intenta terminar un pedido vacío y el sistema se lo impide. Luego busca y selecciona al menos un libro y termina el pedido. 
Se crea un pedido con los libros seleccionados. 
Variante 5d
1,2,3,4,5d,1,2,3,4,5 
Un cliente previamente identificado busca y selecciona al menos un libro. Luego busca y selecciona otro libro y termina el pedido.
Se crea un pedido con los libros seleccionados. 

La prueba de caso de uso sólo se realiza en una versión del sistema en la que ya se han probado todas las operaciones del sistema. Si se detectan muchos errores en las operaciones del sistema durante la prueba del sistema, el enfoque habitual es abortar la prueba de caso de uso y rehacer las pruebas de operación del sistema hasta que se produzca una versión suficientemente estable del sistema y esté disponible para las pruebas de caso de uso.
Aunque las pruebas de casos de uso automático3 pueden comprobar si la funcionalidad es correcta o no, también se recomiendan las pruebas de casos de uso con motor humano porque hay aspectos de la prueba que son difíciles de evaluar para una máquina. Por ejemplo, ¿son claros los mensajes de error? ¿Están bien posicionados y dimensionados los botones y los campos de texto?
Además, puede ser necesario realizar una serie de pruebas no funcionales en función de las especificaciones suplementarias y de los requisitos no funcionales del sistema (capítulo 3). Ejemplos de pruebas no funcionales son la compatibilidad, el cumplimiento, la resistencia, la carga, la localización, el rendimiento, la recuperación, la resistencia, la seguridad, la escalabilidad, el estrés y la facilidad de uso. Explicar todos estos tipos de pruebas está fuera del alcance de este libro. Las pruebas no funcionales requieren técnicas heterogéneas y están cubiertas por un gran número de libros, como por ejemplo: Molyneaux (2009) sobre pruebas de rendimiento, Nelson (2004) sobre pruebas de esfuerzo y Nielsen (1994) sobre pruebas de usabilidad..

            ​ 11.8 El proceso hasta ahora


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

Generación de código: 
-  Generar código para las clases. 
-  Generar código para atributos. 
-  Generar código para asociaciones. 
-  Generar código para los métodos básicos necesarios tales como obtener, establecer, añadir, eliminar, crear, destruir y otros. 
-  Generar código para las operaciones del sistema y métodos delegados utilizando modelos dinámicos como referencia. 
Pruebas/Test

Planificar y ejecutar los Test:
• Realizar pruebas unitarias para métodos y clases que no se generaron automáticamente.
•  Realizar pruebas de funcionamiento del sistema basadas en contratos de operación del sistema. 
• Realizar pruebas de casos de uso basadas en escenarios de casos de uso.
Gestión del Proyecto
Estimar el esfuerzo total, el cronograma ideal y el tamaño medio del equipo para el proyecto.
Estimar la duración y el número de iteraciones para cada fase.
Preparar la fase de planificación y el plan de Iteración para la primera iteración.


            ​ 11.9 Preguntas
1. Considere los métodos definidos en la sección 10.2 para la clase de la figura 10.1 y escriba una secuencia de pruebas unitarias para cada una de las operaciones básicas definidas para esa clase.
2. Vea los cuatro restricciones para la operación deleteBook en la Sección 8.7.3. Escriba una prueba del sistema en su idioma favorito o en pseudocódigo para probar cada una de las versiones de esa operación.
3. Preparar una tabla de pruebas de casos de uso para el caso de uso de la figura 5.4.

1 Aunque la literatura generalmente usa el término clases de equivalencia, que es un concepto matemático, en este libro se usa el término conjuntos de equivalencia para evitar confundirse con las clases orientadas a objetos. 
2 Salvo que fueran subclases de Libro, que no es el caso. 
3 Un ejemplo de un marco de robot para pruebas de interfaz es: http://robotframework.googlecode.com/hg/doc/userguide/RobotFrameworkUserGuide.html?r=2.7.4. Accessed September 1st, 2013.

