# PLANIFICAR el proyecto basado en CASOS DE USO

**Panificar el proyecto basándose en los casos de uso**

Explica cómo organizar una serie de iteraciones incrementales basadas en una lista priorizada de casos de uso y riesgos, que es la columna vertebral del plan de desarrollo con el Proceso Unificado.

## 4.3 Planificación de un proyecto iterativo

El objetivo de la planificación del proyecto es construir un plan para el proyecto en su conjunto. Entre otras cosas, es importante que la persona o grupo responsable de la planificación utilice las mejores herramientas disponibles para evaluar la cantidad de esfuerzo que se debe invertir en el proyecto. Esta estimación conducirá al cronograma y presupuesto del proyecto.


Hay varios aspectos a considerar al principio. La declaración de alcance ya ha definido los objetivos del proyecto y los criterios de aceptación. Además, ya se ha completado el modelado de negocio necesario y se han incorporado los requisitos de alto nivel a los casos de uso del sistema.


Con la técnica de análisis de casos de uso, se puede estimar el esfuerzo total para desarrollar el proyecto, así como el tiempo de calendario ideal y el tamaño medio del equipo; estas son medidas globales para el proyecto.

Ahora es necesario definir la duración y el número de iteraciones.

### 4.3.1 Estimación de la duración de las iteraciones
**Una iteración comienza con la planificación y termina con una nueva versión del sistema que se libera internamente o se entrega al cliente**. La duración de una iteración en UP y metodologías ágiles suele oscilar entre una y ocho semanas,15 y depende, entre otros factores, de la complejidad del proyecto y del tamaño del equipo.

Los equipos pequeños con hasta cinco personas pueden hacer la planificación juntos un lunes por la mañana, realizar el trabajo durante la semana y generar un comunicado el viernes.

Los grupos con más de 20 personas pueden necesitar más tiempo para distribuir y sincronizar las actividades. Considera que la cantidad de trabajo es normalmente mayor. Además, la generación de una versión lleva más tiempo, porque habrá una mayor cantidad de partes de software que integrar, verificar y arreglar. Por lo tanto, en ese caso, se permitirían iteraciones de tres a cuatro semanas.

Los grupos de más de 40 personas necesitan trabajar en un entorno más estructurado y formal, con más documentación intermedia, para que el flujo de información sea naturalmente más lento. Por lo tanto, una iteración de seis a ocho semanas sería aconsejable.
Otros factores que pueden afectar la duración de las iteraciones son los siguientes:

- La generación automática de código y las herramientas de software de ciclo de vida integradas permiten iteraciones más cortas.
- Un equipo que es muy competente en UP y en técnicas de análisis, diseño y codificación permite iteraciones más cortas.
- Si la calidad es una preocupación crítica y, en consecuencia, las pruebas y revisiones son intensas, entonces las iteraciones deben ser más largas, a menos que se utilice una automatización extensa y patrones de codificación de calidad eficaces.

### 4.3.2 Número de iteraciones
El número de iteraciones de un proyecto depende del tiempo de calendario dividido por la duración de cada iteración. Por ejemplo, para el proyecto Livir, con el equipo de novicios, el proyecto duraría unos 10 meses con un equipo de seis personas. Así, se utilizaría una iteración de dos semanas, con un total de 20 iteraciones.

El número de iteraciones que se considerarían para la Elaboración y Construcción depende fundamentalmente de la necesidad de abordar los problemas arquitectónicos. Esto puede estimarse aproximadamente por la cantidad proporcional de casos de uso complejos que deben ser estudiados y desarrollados. Como el hito de la fase de Elaboración es una arquitectura estable, se puede asumir que la Elaboración no terminará mientras haya casos complejos de uso de alta prioridad que necesiten ser analizados. Kruchten (2003) estima que la Elaboración tomaría alrededor del 30% del tiempo lineal de un proyecto típico y la Construcción tomaría alrededor del 50% del tiempo de un proyecto típico, mientras que la Iniciación y la Transición tomaría alrededor del 10% cada una.

Otra pregunta que viene a la mente en este punto es si la estimación del esfuerzo incluye la fase de inicio o no (porque el inicio está prácticamente terminado cuando se hace la estimación). El método COCOMO II, por ejemplo, cuando se aplica al Proceso Unificado, estima sólo el esfuerzo que se va a gastar en Elaboración y Construcción, dejando que Iniciación y Transición se calcule como un porcentaje del esfuerzo total. Normalmente, se cree que el análisis de casos de uso estima el esfuerzo total de un proyecto, desde su inicio hasta la entrega del producto. Sin embargo, si el equipo utiliza otra interpretación, lo importante es mantenerla coherente de un proyecto a otro. Cualquier discrepancia en las medidas de estimación sería absorbida por el índice de productividad del equipo.


### 4.3.5 Definición de la prioridad del caso de uso
Una de las principales técnicas para reducir el riesgo en un proyecto es tratar primero los casos de uso más complejos, especialmente si son los que representan los procesos de negocio más críticos, porque con ellos el equipo puede aprender más sobre el sistema que con otros casos de uso. Los casos de uso de patrones como CRUD (complejidad media) e informes (complejidad mínima) pueden ser tratados más adelante durante la construcción.


La planificación indica cuándo se va a analizar, diseñar e implementar cada caso de uso. El Proceso Unificado, como la mayoría de las técnicas ágiles, no espera que el plan general del proyecto defina cuándo se va a implementar cada caso de uso. Sin embargo, se colocan en una lista dinámica de prioridades y, aunque puede actualizarse sobre la marcha, es posible saber cuándo debe completarse cada caso de uso. La planificación de una iteración comienza eligiendo qué casos de uso, riesgos o requisitos de cambio se tratarán en la siguiente iteración. Al planificar una iteración, se deben tener en cuenta los siguientes aspectos a la hora de elegir los casos de uso a tratar:

- Usar la complejidad de los casos: Los casos de uso de mayor riesgo y complejidad deben abordarse en primer lugar en la mayoría de los casos, a menos que condiciones especiales (por ejemplo, un caso de uso relativamente simple con alto riesgo tecnológico) justifiquen la elección de casos de uso diferentes.
- Dependencias entre casos de uso: Los casos de uso que tienen una fuerte dependencia de los que ya estaban acomodados en la iteración deben ser tratados en conjunto si es posible, ya que evita la fragmentación del trabajo en las clases.
- Capacidad de carga del equipo: El trabajo de desarrollo debe ser asignado a los miembros del equipo en base a su capacidad de carga.
  
Una sugerencia para priorizar los casos de uso del ejemplo de Livir representado en la Figura 3.11 se presenta en la Tabla 4.7.


Tabla 4.7
Sugerencia de prioridades de Caso de Uso para el ejemplo de Livir


1.Order books    
    Pedidos de libros
2.Pay order    
    Orden de pago
3.Deliver order    
    Entregar pedido
4.Register delivery confirmation
    Registrar confirmación de entrega
5.Receive books
    Recibir libros
6.Resend order
    Reenviar pedido
7.Register order return
    Registrar la devolución de pedidos
8.Discard books  
    Descartar libros
9.Cancel order
    Cancelar pedido
10.Create/remove special offer
    Crear/eliminar oferta especial
11.Manage customers <<crud>>
    Mantenimiento de libros
12.Manage books <<crud>>
     Mantenimiento de libros
13.Manage publishers<<crud>>
    Mantenimiento de Editores
14.Order status <<report>>
    Informe de estado del pedido
15.Past sales <<report>>
    Informe de ventas anterior
16.Book sales by period <<report>>
    Ventas de libros por informe de período
17.Books available for sale <<report>>
    Informe de libros disponibles para la venta
18.Book returns by period <<report>>
    Devoluciones de libros en un periódo
19.Upcoming orders by period <<report>>
    Pedidos previstos por periodo 
20.Deliveries by period <<report>>
    Entregas previstas por periodo
21.Discarded books by period <<report>>
   Informe de Libros descartados en un período

El orden de esta lista es el más crítico para los casos de uso complejos, porque una elección errónea en términos de sus prioridades podría llevar a una refactorización innecesaria en iteraciones posteriores. Consideramos que los casos de uso más importantes para este negocio son los relacionados con el proceso de venta de libros, porque eso es lo que genera beneficios para la empresa. Sin embargo, el orden de los casos de uso con menor riesgo, como los cruds y los informes, no es tan crítico.

### 4.3.6 Fase de planificación e iteraciones
Con la información obtenida en las secciones anteriores, es posible elaborar el plan de liberación preliminar utilizando las prioridades de los casos de uso, el esfuerzo y la capacidad de carga del equipo.
Los objetivos de una iteración pueden ser de tres tipos:

- Implementar total o parcialmente uno o más casos de uso.
- Mitigar uno o más riesgos, generando o realizando un plan de reducción de probabilidad, reducción de impacto o recuperación de desastres.
- Implementar total o parcialmente uno o más cambios solicitados. A medida que la arquitectura del sistema evoluciona durante las iteraciones, se pueden solicitar cambios debido a la falta de conformidad con los requisitos o a errores de diseño. Incorporar estos cambios en el software puede ser uno de los objetivos de una interacción. Este tipo de objetivo suele surgir sólo después de la primera iteración.
  

Para cada elemento (caso de uso, riesgo o cambio solicitado) debe haber una estimación del esfuerzo. Los elementos serán seleccionados para su inclusión en una iteración u otra dependiendo de su prioridad (las prioridades pueden cambiar a medida que el proyecto avanza - por lo tanto, la planificación también puede cambiar). Se debe dar mayor prioridad a los elementos más complejos y arriesgados, que son los que tienen mayor potencial para aprender sobre el sistema. La sugerencia es elegir primero:

- Casos de uso que representen los procesos de negocio más críticos, por ejemplo, aquellos que ayuden a la empresa a alcanzar sus objetivos organizativos, como la obtención de beneficios.
- Riesgos de alta importancia (o de alta exposición), es decir, aquellos con un alto impacto y una alta probabilidad de convertirse en problemas.
- Solicitudes urgentes de cambio, por ejemplo, las que requieren refactorización de la arquitectura.
  

Al considerar los elementos de mayor prioridad, otros elementos con prioridades más bajas, pero estrechamente relacionados con los de mayor prioridad, pueden añadirse en la misma iteración por conveniencia. Lo importante es que el esfuerzo total asignado a la iteración no supere el valor del mes del personal que corresponde a la capacidad de carga del equipo.
La mitigación del riesgo y algunas solicitudes de cambio pueden no ser adecuadas para la estimación del esfuerzo porque su tamaño no puede medirse en términos de puntos de casos de uso (o cualquier otra métrica). Por ejemplo, encontrar y arreglar un error puede tomar segundos o semanas. En estos casos, normalmente se asigna una cantidad fija de tiempo, como, por ejemplo, invertir un miembro del equipo durante una semana para trabajar en la mitigación de un riesgo determinado. Al final del cuadro de tiempo previamente definido se evalúa el resultado y se decide si la actividad debe continuar o no.

Consideremos que el proyecto tiene 10 meses (40 semanas) y la duración de la iteración es de tres semanas. Luego, la Iniciación y Transición tomaría alrededor de cuatro semanas (10% del tiempo total), la Elaboración tomaría alrededor de 12 semanas (30% del tiempo total) y cuatro iteraciones de tres semanas, y la Construcción tomaría alrededor de 20 semanas (50% del tiempo total) y cerca de siete iteraciones (una de ellas podría ser una semana más corta, o una semana a partir de la fase de Transición podría ser prestada para la última iteración de la Construcción - la alternativa escogida que se presenta a continuación).
Kroll (2004) presenta una sugerencia para un plan de fase genérico que se adapta al ejemplo de Livir en la Tabla 4.8. Por el momento no se incluyeron las solicitudes de cambio porque aparecen sólo cuando el proyecto está en marcha, no al principio. Por lo tanto, el plan en este caso se basó únicamente en la liberación de casos de uso y la mitigación de riesgos.

Una vez concluida la fase de planificación (normalmente al final de Inicio), se puede detallar el plan para la primera iteración de la Elaboraciónn E1, eligiendo los casos de uso, y detallando y asignando las actividades a los desarrolladores. Sólo cuando esa iteración está en marcha debe comenzar la planificación para la segunda iteración.
El propósito de un plan de iteración incluye lo siguiente (Kroll 2004):
1. Definir el alcance de la iteración definiendo sus objetivos en términos de los artefactos que se producirán, tales como:
    • Detallar e implementar casos de uso específicos.
    • Mitigación de riesgos conocidos.
    • Realizar los cambios solicitados.
2. Crear un plan detallado sobre cómo debe desarrollarse la iteración.
3. Crear, identificar y gestionar dependencias de tareas.
4. Asignar tareas a personas.

Tabla 4.8
Ejemplo genérico de planificación de fase para el Livir

| Fase | Iteración | Objetivo Principal (Riesgos y Casos de Uso A bordados) | Semanario |
| -- | -- | -- | -- |
| Inicio | I1 | Definir visión |  1 a 4 |
| | | Determinar el alcance del proyecto |
| | | Definir arquitectura candidata
| | | Crear caso de uso de negocio 
| | | Crear plan de desarrollo de software 
| Elaboración | E1 |Instalar y probar componentes de arquitectura |   5 a 7
| | | Validar los detalles de los requisitos
| | | Implementar casos de uso prioritario
| | | Probar la arquitectura propuesta
| | E2-E4 | Mitigar los riesgos arquitectónicos. |8 a 16
| | | Instalación y prueba completa de la arquitectura
| | | Implementación de casos de uso adicionales
| | | Elementos arquitectónicos de prueba de carga
| Construcción| C1-C6 | Describir e implementar casos de uso adicionales |17 a 34
| | | Integrar el producto y validar 
| | C7|Describir e implementar casos de uso adicionales | 34 a 37
| | | Integrar el producto y validar 
| | | Plan de prueba beta
| | | Manual de usuario
Transición | T1 | Entregar la versión beta al cliente | 38 a 40
| | | Analizar la retroalimentación de los usuarios de la versión beta
| | | Aplicar correcciones
| | | Finalizar el manual de usuario y otros artefactos
| | | Entrega al cliente



Por ejemplo, considera que estás planificando la primera iteración de elaboración E1 para el proyecto Livir. Consideras las metas generales presentadas en la Tabla 4.8, y el estado actual del sistema. Algunos de los objetivos de iteración podrían definirse como:
    • Expandir e implementar el caso de uso 01:  Pedir Libros
    • Probar y refinar la arquitectura preliminar.
    • Realizar planes de mitigación de riesgo K1: Requerimientos inestables.
Luego, la planificación puede continuar definiendo los entregables de la iteración y las tareas necesarias para producirlos, y asignándolos a los desarrolladores. Los equipos ágiles pueden preferir producir este plan en una reunión de equipo, mientras que los equipos que siguen a el UP pueden preferir instanciar algunos de los flujos de trabajo del UP y determinar qué tareas deben realizarse para lograr los objetivos de la iteración. Explicar esto está fuera del alcance de este libro, pero los lectores interesados en aprender más pueden empezar consultando a West (2002) o Crain (2004).

## 4.4 El proceso visto hasta ahora



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

### ADI
Preparar un modelo conceptual preliminar observando los casos de uso del sistema y los conceptos expresados en el.

### GPI
Estimar el esfuerzo total, el cronograma ideal y el tamaño medio del equipo para el proyecto.   

Estimar la duración y el número de iteraciones para cada fase.  

Preparar la fase de planificación y el plan de Iteración para la primera iteración.


## 4.5 Preguntas

1. Explicar las diferencias entre COCOMO II, el análisis de puntos de función y el análisis de puntos de uso. ¿Cuáles son sus ventajas y desventajas relativas?
2. En el análisis de casos prácticos, ¿cuál es la diferencia entre factores técnicos y ambientales? ¿Por qué el análisis de puntos de caso los considera como grupos separados?
3. Deje que E sea el esfuerzo total para desarrollar un proyecto, y T el tiempo de calendario ideal recomendado para el mismo proyecto. ¿Qué sucede con E cuando el proyecto debe ser desarrollado en un tiempo menor que T? ¿Ocurre lo mismo cuando el proyecto puede desarrollarse en un tiempo superior a T?
4. ¿Cómo se determina la duración ideal de una iteración para un proyecto determinado?
5. ¿Cómo se establece una lista de prioridades para los casos de uso?
