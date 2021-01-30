# MODELADO DE NEGOCIO

El modelado de negocio es la primera actividad que se lleva a cabo durante el desarrollo de la mayoría de los proyectos en la industria del software. Aunque los diagramas de casos de uso de negocio y otros diagramas UML se utilizan actualmente para ayudar a los equipos a comprender los procesos de negocio, a veces las conexiones entre esos elementos no son claras. Este capítulo muestra cómo los casos de uso de negocio pueden ser utilizados para producir una visión de alto nivel de un negocio, y cómo pueden ser detallados usando diagramas de actividad de negocio y diagramas de máquinas de estado que describen los procesos clave de negocio y los objetos clave de negocio. También muestra cómo se pueden utilizar los diagramas de casos de uso del negocio para definir el alcance de un sistema.

## Palabras clave
`Modelado de negocio`; `diagrama de caso de uso de negocio`; `diagrama de actividad`; `diagrama de máquina de estados`; `alcance del proyecto`.

## Conceptos en este Módulo

    • Vista general del sistema
    • Diagrama de Caso de Uso de Negocio
    • Diagrama de actividades
    • Diagrama de la máquina de estado

## 2.1 Introdución al modelado del negocio
La fase de **inicio** del proceso unificado (UP) consiste en un período de tiempo en el que los analistas buscan recopilar información 
sobre el negocio que se va a automatizar o reestructurar.  
Se asume que el conocimiento que los analistas tienen sobre el negocio es mínimo, y que la interacción con los grupos de interés será intensa.  
El objetivo de esta fase es descubrir si vale la pena hacer el análisis sin profundizar demasiado en el proyecto.  
Normalmente, antes de empezar a descubrir y analizar los requisitos del sistema, es necesario comprender los objetivos de la organización.   
Esta visión puede ser obtenida por la disciplina UP llamada modelado de negocios.
El modelado de negocio es, por lo tanto, una actividad que apoya el **descubrimiento de los requisitos del sistema** 
ayudando al equipo a percibir el contexto empresarial más amplio en el que operará el futuro sistema. 
Diferentes artefactos de texto o diagramas pueden apoyarla, como se presenta en este capítulo.

Los **artefactos** en esta fase usualmente no necesitan ser demasiado detallados.  
Las reuniones con las partes interesadas podrían producir un registro (actas) que probablemente pueda recoger varias ideas sobre los objetivos de la empresa y las oportunidades de automatización. Al usar esta información, el equipo puede construir una visión general del negocio.
A partir de los registros obtenidos, el equipo puede organizar un documento inicial para el proyecto, que puede denominarse **vista general del sistema** o 
**resumen ejecutivo**. Este documento suele incluir la declaración de alcance.  

Otra información relevante también suele incluirse en la vista general, como; las partes interesadas, la asignación de poder, el análisis de riesgos, el presupuesto y el calendario preliminares, y las instalaciones del proyecto.  

La declaración de **alcance del proyecto** puede estar relacionada con las actividades de análisis de negocio.   
Después de descubrir información útil sobre el negocio, el equipo está en mejores condiciones de determinar qué debe y qué no debe incluirse en el proyecto.   
La vista general del sistema puede ser elaborada con la ayuda de algunos diagramas UML.   
Se pueden utilizar diagramas de casos de uso de negocio (Sección 2.3) y diagramas de actividades de negocio (Sección 2.4, y ocasionalmente diagramas de estado de máquinas (Sección 2.5). Alternativamente, se puede utilizar el Business Process Model and Notation, BPMN, en lugar de los diagramas de actividad UML. 
Estos diagramas ayudan a determinar si el alcance del proyecto es completo y consistente con los objetivos de la organización.

El modelado de negocio consiste en estudiar y entender la organización y sus procesos, porque normalmente el sistema a desarrollar no será un producto aislado, 
sino una parte orgánica del contexto de la organización. Los objetivos de esta disciplina son:  

- Comprender la estructura y la dinámica de la organización objetivo en la que se utilizará el software.  
- Comprender los problemas actuales de la organización objetivo e identificar las mejoras potenciales que se pueden obtener con el software.  
- Asegurar que los clientes, usuarios y el equipo de desarrollo compartan un entendimiento consistente de la organización objetivo.  
- Derivar los requisitos que conducirán a las mejoras deseadas.

Uno de los puntos críticos para el éxito de un proyecto de desarrollo de software es su financiación. 
Para mantener el interés en el desarrollo de un producto de software, el cliente debe estar siempre convencido de que su inversión representa una ganancia, 
y no una pérdida de tiempo y dinero.  
La comprensión del modelo de negocio es fundamental para que el equipo de desarrollo pueda mantener al cliente interesado en el proyecto.
Otro aspecto importante del modelado de negocio es acercar el equipo de expertos en el negocio y el equipo de ingeniería de software, 
para que los problemas reales de la organización y sus necesidades sean entendidos, analizados y resueltos mediante el uso de la tecnología de la información.  
El modelado de negocios es muy importante cuando se introducen cambios significativos en el comportamiento de un grupo de personas.   
En este caso, el contexto empresarial y las consecuencias de la instalación de un nuevo sistema deben ser reconocidos y estudiados.   
Puede ser menos importante cuando no se esperan tales cambios de comportamiento.
Por lo tanto, el modelado de negocios puede tener diferentes niveles de importancia dependiendo de las necesidades del proyecto.   
Kruchten (2003) identifica seis escenarios de creciente complejidad en términos de la necesidad de modelos de negocio:  

- **Organigrama**: Puede que sólo sea necesario construir un organigrama para conocer los sectores y las responsabilidades relacionadas con el área en la que se inserta el proyecto. En este caso, el modelado de negocios, en general, es muy simple, y sólo ocurre durante el inicio. El organigrama ayudará a los analistas a localizar a las personas responsables de los diferentes aspectos relacionados con el futuro sistema, y qué grado de autoridad se asigna a cada uno a la hora de decidir los requisitos.  
- **Modelado de dominios**: Si el objetivo del proyecto es construir aplicaciones para gestionar y presentar información, entonces el modelado de negocio puede realizarse durante el análisis de dominio, es decir, cuando se produce un modelo estático de la información (modelo conceptual). En este caso, el modelado de negocio se realiza durante el inicio y la elaboración.  
- **Una compañía, muchos sistemas**: Puede ocurrir que el equipo esté desarrollando toda una familia de sistemas para una empresa. En este caso, el modelado de negocios no se trata sólo de un sistema, sino que se extiende a lo largo de muchos proyectos, e incluso podría ser un proyecto separado por sí mismo. Ayudará a descubrir los requisitos individuales del sistema, así como a determinar una arquitectura común para toda la familia.  
- **Modelo de negocio genérico**: Si el objetivo es construir uno o más sistemas que sirvan a un grupo de organizaciones, entonces el modelado de negocios es útil para alinear las diferentes organizaciones a una visión común de negocios, o, si esto no es posible, para obtener una visión de negocios en la que los detalles de las organizaciones sean visibles.  
- **Nuevos negocios**: Si una organización decide iniciar un nuevo negocio, y se debe desarrollar todo un conjunto de sistemas para darle soporte, entonces se debe realizar un esfuerzo significativo de modelado de negocios. En este caso, el objetivo del modelado de negocios no es sólo encontrar requisitos, sino verificar la viabilidad efectiva del nuevo negocio. Por lo tanto, el modelado de negocios, en esa situación, podría ser un proyecto independiente.  
- **Renovación**: Si una organización decide renovar completamente su forma de hacer negocios, entonces el modelado de negocios será un proyecto separado, realizado en varios pasos: visión del nuevo negocio, ingeniería inversa del negocio existente, ingeniería directa del nuevo negocio e instalación del nuevo negocio.  

Otros factores que aumentan o disminuyen la necesidad de un modelo de negocio en un proyecto son:  

- Los requisitos bien definidos y estables al principio del proyecto (por ejemplo, crear un sustituto para un sistema existente) reducen la necesidad de realizar un intenso modelado de negocio.  
- Si el nuevo sistema va a cambiar la forma en que las personas hacen su trabajo, entonces se debe prestar especial atención al modelado de negocios, especialmente cuando el modelo de negocios va a ser cambiado o reconstruido después de la automatización de algunos casos de uso de negocios.  
- Si el proyecto tiene riesgos importantes, especialmente riesgos de negocio, entonces el modelado de negocio debe ser más detallado e intenso.  
- Si la comunidad de usuarios es grande y heterogénea, entonces el modelado de negocios probablemente será más difícil.  
- Si es necesario integrar el nuevo sistema con los sistemas hardware y legados, entonces la comprensión de esos elementos debe ser incluida en el modelado de negocio, generando más trabajo.  
- Más incertidumbre sobre los requisitos significa más atención al modelado de negocios.  

No importa el nivel de detalle y esfuerzo que se deba poner en el modelado de negocios, cada proyecto debe comenzar con documentación preliminar que permita comprender su alcance. Un proyecto con un alcance mal definido puede dar lugar a molestias o incluso peleas entre el cliente y el equipo de desarrollo, en cuanto a la inclusión (o falta de inclusión) de ciertas características.

## 2.2 Visión general del sistema

Las actividades relacionadas con la definición del alcance de un proyecto deben tomar generalmente una fracción relativamente pequeña del tiempo de todo el proyecto, aunque pueden existir variaciones dependiendo del tipo de proyecto: los proyectos con requisitos simples y bien definidos pueden requerir no más de un par de días de modelado de negocios, mientras que los proyectos complejos y grandes pueden requerir semanas o meses. En el momento de la definición del alcance, toda la información sobre el negocio de la empresa debe ser explorada mediante entrevistas a los usuarios, clientes y especialistas en la materia, así como mediante el examen de documentos, informes, sistemas existentes y bibliografía relacionada.


Para la mayoría de los proyectos, la primera pregunta que el analista debe responder es la siguiente: 

¿Cuál es la visión de la empresa para el proyecto? En otras palabras, ¿qué quiere la empresa con el proyecto? ¿Por qué se propone y por qué la empresa va a gastar dinero con ella?

En ese momento, otra pregunta, a menudo olvidada, puede ser planteada: ¿Comprar o desarrollar? A veces, el producto que el cliente desea está disponible para su compra.  
Estas preguntas deben ser contestadas en un tiempo relativamente corto. Por ello, se sugiere que la fase inicial se lleve a cabo con relativa rapidez. ¿Por qué? Porque, en este momento, el cliente y el equipo de desarrollo no suelen tener una idea de la extensión real del proyecto y es, desde el punto de vista de ambos, una inversión de futuro y, por tanto, un riesgo.  
La visión general del sistema o resumen ejecutivo es un documento de formato libre, donde la analista puede reportar los puntos relevantes que descubrió sobre el sistema después de las entrevistas iniciales con las partes interesadas.   
El documento suele incluir la declaración del alcance del proyecto.  
No tenemos intención de proponer normas para la redacción de ese documento. Pero se sugiere que no sea demasiado largo. Unas pocas páginas de texto y algunos diagramas parecen ser suficientes para describir de forma resumida el alcance de la mayoría de los sistemas. Más que eso podría significar que se incluyeron demasiados detalles en el resumen.   
Estos detalles podrían ser tratados alternativamente en otros documentos, como la lista de riesgos, requisitos o casos de uso.
La declaración de alcance en la visión general debe presentar, en líneas generales, el producto que debe desarrollarse: qué debe incluirse y qué puede incluirse pero no debe incluirse. Esta información puede obtenerse inicialmente entrevistando a las partes interesadas, y puede afinarse más tarde con el uso de los diagramas presentados en este capítulo.  
Si es posible, los principales entregables del proyecto también deben ser definidos en la vista general, así como el marco de tiempo en el que el cliente va a recibir algún tipo de entrega del equipo de desarrollo. Normalmente, esta lista de entregables consiste en versiones implementadas del software, pero la lista también puede incluir otros elementos, como diseño, manuales, medios de instalación, formación, etc.   
Puede ser muy difícil establecer plazos de entrega antes de realizar el análisis de los requisitos del sistema, ya que las técnicas de estimación del esfuerzo, como los puntos de función (Albrecht y Gaffney Jr., 1983), los puntos de caso de uso (Karner, 1993) o COCOMO II (Boehm, 2000), sólo pueden aplicarse después de que se conozca una buena parte de los requisitos.   
Por lo tanto, la información sobre los plazos en esta fase previa es más una suposición que un fuerte compromiso formal para el desarrollo.
El documento de vista general también puede contener **algunos criterios de aceptación del producto**, es decir, elementos cuantificables que se utilizarán para decidir si el proyecto ha sido un éxito o no. Los criterios de aceptación del producto deben incluir al menos métricas de plazos, presupuesto y calidad. Si se utilizan criterios subjetivos como "_satisfacción del cliente_", "_sistema fácil de usar_" o "_tecnología punta_", deben cuantificarse, es decir, debe definirse cómo medir la "satisfacción del cliente", "facilidad de uso", "estado actual de la técnica", etc.   
Ejemplos de criterios de aceptación cuantificables son "_el sistema debe soportar hasta 50.000 accesos simultáneos sin degradar el rendimiento_", "_el sistema debe eliminar la necesidad de utilizar papel para realizar los procesos x e y_", y "_el sistema debe permitir la venta de hasta 100 libros por minuto en Internet_".  
Si es necesario, se puede añadir más información al documento de visión general (por ejemplo, los principales riesgos, las tecnologías que se utilizarán, etc.). 

>La vista general del sistema es el documento base del acuerdo para el cliente y el desarrollador. Se tomará como base para la planificación del resto del proyecto.   

Es importante mencionar que cuando se está construyendo la vista general, todavía no se ha completado el análisis de requisitos y, por lo tanto, la información mencionada en la vista general consiste en compromisos tempranos. Se espera que el análisis de los requisitos detalle el alcance en profundidad, pero no aumente su extensión. Por ejemplo, en el análisis de requisitos, el proceso de venta de libros puede detallarse con descuentos, ventas, entregas, etc. (teniendo en cuenta que "venta de libros" se menciona en la declaración de alcance), pero si la transferencia de pagos de la empresa no se mencionara en la declaración de alcance, entonces la inclusión de ese elemento en el proyecto requeriría una renegociación de la declaración de alcance.
Pressman (2008) propone una serie de técnicas para comunicarse con los grupos de interés con el fin de descubrir, por ejemplo, los objetivos del negocio:  

- Grupos focales tradicionales, donde un analista capacitado se reúne con un grupo de usuarios finales o personas que representan sus funciones.
- Grupos focales electrónicos, en los que las reuniones se llevan a cabo mediante el uso de medios electrónicos.
- Encuestas iterativas, en las que se realizan una serie de encuestas entre los usuarios finales, en las que se les presentan algunas preguntas y se les pide aclaración.
- Encuestas exploratorias, en las que se realiza una investigación exploratoria entre usuarios finales que utilizan un producto existente similar.
- Construcción de escenarios, donde un grupo de usuarios finales es guiado a producir una descripción de un número de escenarios para el uso del sistema.

La última opción parece ser muy popular entre los profesionales de métodos ágiles, donde los escenarios a veces se identifican como **historias de usuarios**.
La figura 2.1 presenta una visión general con una declaración de alcance muy preliminar para una librería virtual ficticia Livir, que se utilizará para ilustrar las técnicas de modelado dentro de este libro. Este texto se habría obtenido tras una rápida reunión preliminar con el cliente.   
Utilizando esto como base, se puede realizar un estudio más profundo con casos de uso de negocio y otros diagramas, de manera que la información contenida en ellos sea refinada, como se muestra a continuación en este capítulo.   

El documento se divide en dos partes:

- Una simple declaración de visión de lo que el proyecto ofrecerá a los clientes y al negocio que lo está creando.
- Las restricciones de la versión 1.0.

```  
**Vista general del proyecto Livir**
Version 1.0

Visión:
Se iniciar un nuevo negocio: una librería virtual. 
El sistema a desarrollar debe manejar los procesos de adquisición y venta de la compañía. 
El acceso para los clientes y el personal de gestión debe ser realizado a través de un sitio Web.
Cuando un libro sea ordenado, si está disponible en stock es enviado inmediatamente, en caso contrario, 
el libro es solicitado al editor, y el plazo estimado  se comunica al cliente. El sistema calculará 
impuestos y gastos de envío, al mismo tiempo que aplicará descuentos cuando sea pertinente.

El sistema permitirá al administrador generar informes sobre bestselers y sobre los clientes más rentables,
al mismo tiempo que sugerirá libros para comprar basados en anteriores intereses del cliente.

Restriciones:
        a) Los clientes podrán abonar sólo mediante Tarjeta de Cŕedito
        b) La tienda sólo servirá libros nuevos, no usados.
        c) El acceso al sistema estará disponible sólo a través de un sitio Web.
```
`Figura 2.1 Vista general del proyecto Livir`


La descripción y modelización de un proyecto real deberían ser mucho más extensa. Además, los modelos presentados a veces serían parciales en un momento dado y se perfeccionarían o modificarían posteriormente.  
Se puede ver que la vista general es una vista no estructurada del proyecto. Incluye información del negocio para los gerentes e información operativa para los desarrolladores. A veces, incluso se pueden describir detalles sobre la tecnología que se va a utilizar, si es necesario. Lo que el analista debe tener en cuenta es que la visión general describe las principales preocupaciones de los clientes y que esas preocupaciones se estructurarán mejor más adelante durante el análisis y el diseño.  
Un buen analista debe actuar como un psicoanalista, es decir, debe evitar hablar en lugar del cliente. El analista debe ayudar al cliente a hablar; cuando el cliente comienza a reportar algunas de sus necesidades, el analista debe escuchar, en lugar de presentar soluciones rápidas y prefabricadas (y a menudo erróneas).  
>El analista debe motivar al cliente a detallar sus requerimientos y debe cuestionarlos para que el cliente pueda decidir cuáles son urgentes y cuáles no.  

## 2.3 Casos de uso del Negocio

Jacobson (1994) presenta en detalle técnicas para el modelado de negocios con casos de uso de negocios. 
En general, en los modelos de negocio, existen entidades (personas o empresas) externas a la organización objetivo, 
llamadas actores del negocio, y entidades internas, llamadas trabajadores del negocio. 
Los casos de uso empresarial son los procesos realizados por aquellos actores y trabajadores que les permiten alcanzar algunos de los objetivos del negocio de la empresa.
El modelo de caso de uso de negocio considera a toda la compañía como un sistema, y los actores pueden ser personas, compañías u otras organizaciones que crean negocios o mantienen relaciones con el negocio (Kroll y Kruchten, 2003).
Lo primero que el equipo debe tener en cuenta al hacer el modelado de negocios es que lo que se está modelando no es un sistema de software. 
Una compañía está siendo modelada. La información de negocios se busca de los gerentes y especialistas de alto nivel, porque ellos conocen y a veces crean las metas de la compañía.
La cantidad de casos de uso de negocio que se identificarán puede ser relativamente pequeña. 
Un proceso de negocio es un proceso de largo alcance que realiza la empresa; piense, por ejemplo, en la venta de productos, la realización de marketing, la prestación de servicios, la resolución de problemas de los clientes, etc. Cada proceso de este tipo debe contribuir a un objetivo empresarial. No es el momento de detallar tales procesos. Por ejemplo, la venta de productos puede incluir muchos subprocesos como el registro de clientes, la oferta de productos, el envío de productos, la aplicación de descuentos, etc. Pero esos procesos (que más tarde posiblemente serán identificados como casos de uso del sistema si van a ser automatizados) están involucrados en el proceso de más alto nivel, que es Vender libros.

Aunque UML todavía no tiene un símbolo estándar para diferenciar los **casos de uso empresarial** de los **casos de uso del sistema** (Capítulo 3), es habitual representar los casos de uso empresarial con el negocio estereotipado, o cortando la elipse de caso de uso con un borde como se muestra en la Figura 2.2.

TODO: FFFF Figura de caso de uso empresarial

`Figura 2.2 Caso de uso de Negocio.`

En este ejemplo, “Sell books” es un caso de uso de negocio porque implica una relación entre la empresa y una entidad externa (un cliente), produciendo un resultado perceptible y consistente: uno o más libros vendidos. Este caso de uso posiblemente será realizado por el cliente con la colaboración de algunos trabajadores dentro de la empresa; puede o no utilizar sistemas de software.
Los nombres de los casos de uso deben elegirse cuidadosamente, ya que en esta etapa resumirán la información crítica sobre el sistema, y las decisiones equivocadas pueden impedir que el equipo y las partes interesadas compartan la comprensión de la intención real de los actores y trabajadores de la empresa. Blain4 presenta algunas de las mejores prácticas recogidas de muchas fuentes:
    • Los buenos nombres de casos de uso reflejan los objetivos del usuario. Los nombres como Access system o Open main window deben evitarse porque reflejan tecnología y no un objetivo empresarial. También los nombres sin verbos como Factura deben evitarse porque no está claro lo que va a pasar con la factura. Mejores nombres pueden ser Generar factura, Cancelar factura, Pagar factura, etc.
    • Los buenos nombres de casos de uso son tan cortos como sea posible. Aunque algunas personas pueden proponer que el nombre de un caso de uso no debe tener más de dos o tres palabras (o cualquier otro número), no es factible definir dicho límite porque existe el riesgo de perder claridad sobre el objetivo empresarial si el nombre es demasiado corto. Como señala Blain, ¿qué palabra podría ser eliminada del nombre Cobrar pagos atrasados sin ocultar su significado? Sin embargo, ese nombre es mejor que Cobrar pagos atrasados de clientes que están atrasados.
    • Los buenos nombres de casos de uso utilizan verbos significativos. Los nombres de los caso de uso, no sólo deben tener verbos fuertes, sino que deben ser significativos. Un verbo sin sentido es aquel que no aclara lo que logra el caso de uso; por ejemplo, ¿qué logra un caso de uso como "Orden de proceso"? ¿Qué resultado produce? Un nombre como "artículos pedidos por separado para su envío" sería más significativo en ese caso.
    • Los buenos nombres de casos de uso utilizan la voz activa. Como en la escritura general, la voz activa es preferible a la voz pasiva. El pago del pedido es mejor que el pedido pagado.
    • Los buenos nombres de casos de uso utilizan el tiempo presente. El tiempo presente indica lo que el usuario está tratando de hacer. El pasado y el futuro pueden parecer confusos e innecesarios.
    • Los buenos nombres de casos de uso no identifican al actor. Como los casos de uso están vinculados a los actores, éstos no forman parte de sus nombres. Por lo tanto, el nombre de un caso de uso no debe identificar al actor, ya que el Administrador crea un informe de ventas. Simplemente nombre el caso de uso Crear informe de ventas y vincularlo a un gerente u otros actores si es necesario.
    • Los buenos nombres de casos de uso son consistentes. Las mismas reglas de nomenclatura y las mismas convenciones de nomenclatura deben aplicarse a lo largo de un proyecto o grupo de proyectos. Evite, por ejemplo, nombrar un caso de uso Generar informe de ventas y otro Informe de reservas de productos. Elige un verbo para ese significado y úsalo consistentemente.
Además, Probasco (2001) propone que la lista de nombres de casos de uso se asemeje a una lista de tareas pendientes. Por lo tanto, en lugar de escribir Retirada de efectivo, Transferencia de fondos y Servicio de cajero automático, sería mejor escribir Retirar efectivo, Transferir fondos y Servirse del cajero automático, respectivamente.
Probasco también insiste en que el significado del nombre de un caso de uso debe ser preciso. Por ejemplo, ¿es la subasta un buen caso de uso? ¿Es un verbo o un sustantivo? Si considera que se trata de un sustantivo y que debe añadirse un verbo, ¿es Execute auction un buen nombre? El verbo Ejecutar sería probablemente la elección de un programador, pero probablemente no tiene ningún significado para un subastador (¿Va a morir de un disparo la subasta?). En este caso, una idea sería hablar con un especialista en dominios para obtener un nombre mejor. Por otra parte, incluso si "subasta" es en realidad un verbo, no está suficientemente claro. ¿Es la subasta de un solo artículo? ¿Es la subasta de un conjunto completo de artículos? ¿Es simplemente un participante de la subasta que hace una oferta? En ese caso, los nombres como Subastar un artículo, Subastar artículos o Realizar puja serían más claros.

### 2.3.1 Actores del negocio y trabajadores del negocio.
Durante el modelado de negocios hay dos tipos de actores que deben ser abordados (Figura 2.3):
    • Actores del negocio: Personas, organizaciones o incluso sistemas que realizan algunas actividades pertenecientes al proceso, pero que no forman parte de la empresa objetivo. Es decir, no están bajo el control de la empresa. Los actores del negocio pueden ser, por ejemplo, clientes, editores, auditores externos, empresas asociadas o incluso otros sistemas automáticos con los que la empresa objetivo pueda interactuar.
    • Trabajadores del negocio: Personas, organizaciones o incluso sistemas que realizan algunas actividades pertenecientes al proceso y que forman parte de la empresa objetivo. Pueden ser los empleados de la empresa, sus departamentos o incluso los sistemas de software existentes pertenecientes a la empresa. Gráficamente, se distinguen de los actores del negocio por el uso del estereotipo <<worker>>.

TODO: FFFF Figura worker
Figura 2.3 Actor del negocio (izda) y  trabajador del negocio (derecha).

Esta diferenciación es importante porque los actores del negocio normalmente no pueden automatizarse, es decir, no serán sustituidos por sistemas computacionales. Sin embargo, los roles de los trabajadores de negocios pueden ser reemplazados por sistemas automáticos (English, 2007).
Los agentes y trabajadores del negocio están vinculados a los casos de uso empresarial en los que participan mediante líneas de conexión sin flechas, como se muestra en la figura 2.4.

TODO: FFFF

Figura 2.4 Enlaces entre actores del negocio y casos de uso del negocio.

### 2.3.2 Oportunidades de automatización
Una librería que pretende vender a través de Internet, como Livir, debe producir un modelo de negocio que identifique sus principales casos de uso empresarial, actores externos (clientes, editores, etc.), y trabajadores del negocio (gerentes, empleados, etc.). Si suponemos que la librería ya existe y no tiene ninguna o muy incipiente automatización, entonces los trabajadores del negocio serán, básicamente, personas reales. Estos trabajadores pueden ser candidatos a la automatización si hay interés en aumentar el nivel de automatización de la empresa. Por ejemplo, el papel del empleado que actualmente ayuda a los clientes a encontrar libros en las estanterías puede ser sustituido en la librería virtual por un sistema de guía automática. Sin embargo, la función de cliente no puede sustituirse por un sistema automático.
Por lo general, no se reemplazan todas las funciones de los trabajadores de una empresa. Dependerá del alcance del proyecto que se defina. Una ventaja de hacer el diagrama del caso de uso del negocio, entonces, es ayudar en la visualización y toma de decisiones sobre la automatización. Con el diagrama, es posible visualizar lo que debe permanecer dentro y fuera del ámbito de la automatización, dependiendo de los objetivos del proyecto.
Normalmente, durante un proceso de automatización dentro de una empresa, es útil sustituir al menos los roles de los trabajadores que corresponden a meros apoderados, es decir, los que simplemente realizan acciones en lugar de un actor externo. En el caso de la librería, el papel del vendedor sólo es necesario para ayudar al cliente en la tienda física. Pero, cuando las ventas se trasladan al espacio virtual, ese papel ya no es necesario, porque el cliente puede encontrar fácilmente su camino en el sitio web.
La asociación de los casos de uso del negocio con los principales objetivos comerciales de la empresa ayuda a identificar el alcance del sistema, es decir, las actividades que se automatizarán eficazmente en el proyecto que se está iniciando. En el ejemplo de la Figura 2.5, todos los casos de uso son candidatos para la automatización con diferentes niveles de prioridad. Sin embargo, la empresa sólo podría estar interesada en implementar ventas y adquisiciones en este punto, dejando el marketing y los servicios al cliente en manos de un segundo proyecto.

TODO: FFFF

Figura 2.5 Caso de uso de Negocio: candidatos para automatizarse.

El límite del sistema se puede utilizar para identificar el conjunto de casos de uso empresarial y de trabajadores del negocio que se automatizarán, como se muestra en la Figura 2.6.

TODO: FFFF

Figura 2.6 El límite del sistema que se utiliza para indicar el alcance del proyecto.

El diagrama del caso de uso de negocio muestra que el proyecto de automatización incluirá los procesos de compra y venta de libros y el papel del empleado. También muestra que los procesos de publicidad y fidelización de clientes están fuera del alcance del proyecto.
Sin embargo, un análisis más profundo puede mostrar que el trabajador que compra libros para la librería no puede ser fácilmente automatizado. Podría darse el caso de que todos los libros pudieran ser comprados automáticamente mediante un proceso automático que analizara las ventas y existencias potenciales, sin la participación de ningún ser humano. Pero, si ese no es el caso, lo mejor es considerar que el empleado realmente tiene dos roles diferentes: ayudar al cliente (ese rol será automatizado) y comprar libros para la librería (ese rol no será automatizado). La figura 2.7 muestra una evolución del diagrama en la que parte de la responsabilidad del empleado se reasigna a un trabajador llamado "Gestor de adquisiciones". No existe una equivalencia uno a uno entre un rol y una persona: una persona puede desempeñar muchos roles y un rol puede ser desempeñado por muchas personas diferentes.

TODO: FFFF
Figura 2.7 Un actor se divide porque sólo parte de su rol se automatiza.

Si el proyecto, por el contrario, consiste en una serie de subproyectos o etapas, en los que se automatizarían diferentes partes de la empresa, esto también podría indicarse mediante el uso de diferentes límites de sistema en el diagrama: uno para cada subproyecto o etapa.
El siguiente paso que conduce al análisis de requisitos es el estudio detallado de los casos de uso empresarial que se automatizarán. El nivel de precisión y detalle depende de los objetivos del proyecto, como ya se discutió al principio de este capítulo.

## 2.4 Diagrama de actividad de Negocio
El diagrama de actividad UML es una opción muy popular para estudiar los detalles de un caso de uso empresarial. Con este diagrama se pueden especificar las diferentes actividades que realizan los actores del negocio y los trabajadores para alcanzar el objetivo general del caso de uso.
Para una mejor comprensión del funcionamiento de la empresa a través de sus casos de uso, es posible crear un diagrama de actividad para cada caso de uso empresarial que vaya a ser automatizado. Los diagramas de actividad pueden utilizarse para representar procesos a nivel de organización.

### 2.4.1 Elementos Básicos
Gran parte del diagrama de actividades de UML es similar a un diagrama de flujo. Hay actividades enlazadas secuencialmente. Se pueden utilizar puntos de decisión y bucles e incluso se puede expresar el paralelismo en dichos diagramas.
El diagrama de actividad puede dividirse en carriles o pistas, cada uno de los cuales representa a un actor o trabajador que participa en un conjunto de actividades. Como en el diagrama del caso de uso, un actor o trabajador puede ser una persona, un departamento, un sistema computacional o incluso una organización completa.
El proceso representado en el diagrama suele tener un nodo inicial, representado por un círculo sólido, y un nodo final de actividad, representado por un círculo sólido inscrito en una circunferencia. El nodo inicial puede no ser considerado obligatorio en algunos casos cuando el inicio del proceso puede ser inferido observando una actividad que no tiene un antecesor. Sin embargo, el uso de esa marca mejora la legibilidad del diagrama porque es más fácil ver dónde comienza realmente el proceso.
Las actividades están representadas por nodos de acción. Cuando una actividad se representa dentro de una pista de natación, significa que el actor correspondiente es el responsable de la actividad.
Los flujos o dependencias entre actividades se representan con flechas. Los flujos suelen vincular dos actividades, indicando la precedencia entre ellas.
Un camino es una secuencia de actividades enlazadas por flujos.
En el ejemplo de Livir, el diagrama de actividades puede ser usado como una manera de visualizar los detalles de casos de uso de negocios como Vender libros. El modelo presentado en la Figura 2.8 muestra un primer acercamiento al proceso.

TODO: FFFF 

Figura 2.8 Primer enfoque para modelar el diagrama de actividad 
del proceso de negocio “Vender Libros”.

El diagrama que está comenzando a ser diseñado en la Figura 2.8 no pretende ser un modelo para el sistema que se va a construir y no debe ser pensado de esa manera. Su utilidad es ayudar al equipo a entender qué actividades y actores están involucrados en los principales procesos de negocio de la empresa, para que, utilizando esa información, puedan realizar un análisis de requerimientos más efectivo más adelante. La trayectoria lógica del diagrama debe ser comprensible y validada por los empresarios.
Posteriormente, el analista examinará en detalle cada una de las actividades que se deben realizar. Si una actividad determinada pertenece al ámbito del sistema que se va a implementar, entonces debe ser un objetivo para un análisis más detallado.

### 2.4.2 Nodos de Flujo de Control
Dos nodos de flujo de control son comunes en el diagrama de actividad: los nodos de decisión y los nodos de paralelismo.
    • Los nodos de decisión (nodos de rama y de fusión) están representados por diamantes. Los flujos que salen del nodo de decisión deben tener condiciones de guarda (una expresión lógica entre paréntesis). Dos o más movimientos pueden salir de un nodo de decisión, pero es importante que las condiciones de guarda sean mutuamente excluyentes, es decir, sólo una de ellas puede ser verdadera a la vez.
    • Los nodos de paralelismo (nodos de horquilla y de unión) están representados por barras . Los flujos que salen de un nodo de horquilla se realizan en paralelo.
El diagrama de la Figura 2.8 es todavía una representación muy bruta del proceso real de venta de libros. Sólo para ilustrar una posible evolución de ese diagrama, examinemos la situación cuando algunos de los libros encargados no están disponibles en stock. Sería necesario pedirlos a uno de los editores y añadirlos al pedido del cliente después de su llegada. La Figura 2.9 muestra esta situación al indicar que si algunos libros no están disponibles, entonces tienen que ser ordenados a los editores, y el pedido se envía sólo después de su llegada.

TODO: FFFF

Figura 2.9 Ejemplo de decisión de control de flujo.

Justo debajo de la actividad Confirmar pago hay un nodo de rama representado por el diamante. Como se ha indicado anteriormente, el nodo de decisión sólo permite seguir un flujo de salida. Las condiciones de guardia ([some books missing] y [all books in stock])  son mutuamente excluyentes. Desde el nodo de rama, el flujo sigue uno de los caminos alternativos hasta llegar al nodo de fusión que se representa justo encima de la actividad Enviar libros.
Más tarde, el analista podría descubrir que el modelo todavía no es satisfactorio. Por ejemplo, incluso si algunos libros no están en stock, el pedido puede ser enviado en dos o más entregas. De este modo, se podrían realizar dos recorridos en paralelo: enviar los libros disponibles en stock y, si fuera necesario, encargar los demás libros y enviarlos más tarde, como se muestra en la Figura 2.10.

TODO: FFFF

Figura 2.10 Ejemplo de los siguientes flujos..

La barra debajo de Confirmar actividad de pago en la Figura 2.10 representa un nodo de horquilla porque inicia dos rutas paralelas, y la otra barra representa un nodo de unión porque sincroniza las rutas paralelas en una sola ruta.
La trayectoria única después de un nodo de unión sólo se puede seguir si se han seguido todas las trayectorias que llegan al nodo de unión. Se puede ver que en ese modelo, si todos los libros están en stock, sólo uno de los caminos paralelos tendrá actividades que realizar, porque el otro camino va inmediatamente a los nodos de fusión y unión.
Los nodos de bifurcación, unión, decisión y fusión, así como los nodos inicial y final de la actividad, pueden colocarse dentro de los carriles. Sin embargo, esto no afecta su semántica. Por lo tanto, la elección de un carril de baño para colocar tales nodos se debe únicamente a la idoneidad visual.
Otro nodo que puede ser útil a veces es el nodo final de flujo, , que termina una trayectoria (paralela o no) que se está realizando. La diferencia entre éste y el nodo final de la operación es que en el caso del nodo final de la operación, todos los movimientos del diagrama de actividades terminan cuando un solo movimiento lo alcanza, mientras que en el caso del nodo final de proceso sólo se termina un movimiento (entre otros movimientos paralelos), pero la operación continúa.
En el caso de uso de la Figura 2.7, sólo un actor (cliente) y un trabajador (empleado) participan en el caso de uso Vender libros. Sin embargo, después de detallar las actividades relacionadas con ese caso de uso, como se hace en la Figura 2.10, se descubrió que son necesarios dos actores más: el editor y el operador de la tarjeta de crédito. Además, el Editor es un actor que tiene que estar vinculado al caso de uso Comprar libros. Por lo tanto, dependiendo del nivel de detalle deseado en este punto del proyecto, el diagrama del caso de uso de negocio puede actualizarse para reflejar esos descubrimientos, como se muestra en la Figura 2.11.

Figura 2.11 Business use case diagram actualizado 
con información descubierta con el diagrama de actividad.

Otras opciones para detallar un caso de uso de negocio son el diagrama de secuencia UML y el diagrama de comunicación. Sin embargo, estos diagramas se utilizan para representar los mensajes que se envían a los elementos. No siempre es natural encontrar nombres para etiquetar esos mensajes en el caso de un proceso empresarial, y los nombres sin sentido como "buscar datos" y "verificar resultado" se eligen finalmente. Por lo tanto, el diagrama de actividad es una opción más natural para describir lo que sucede en el mundo real, dentro de una organización de personas. Sin embargo, como se verá en la Sección 5.8, los diagramas de secuencia son muy útiles para detallar los casos de uso del sistema, porque los casos de uso del sistema generalmente consisten en una secuencia de flujos de información que se intercambian entre los actores y un sistema.

------------------------
## 2.5 Aspectos dependientes del Estado de un negocio  

Además de los casos de uso de negocio, que pueden ser detallados por los diagramas de actividad, 
puede ser importante entender otros aspectos de un negocio que no siempre aparecen claramente en dichos diagramas, 
tales como algunos objetos clave de negocio que cambian de estado durante su ciclo de vida.
Así, otro diagrama UML que puede ayudar al equipo a entender el negocio de la organización es el diagrama de máquinas de estado.  
Al igual que el diagrama de actividad, éste es un diagrama de comportamiento, pero, en lugar de modelar actividades en procesos, 
representa un conjunto de estados en los que un sistema, actor o entidad podría estar en un momento dado.
El diagrama de máquina de estados especifica los eventos en sus flujos. Un evento desencadena el flujo que lleva a la entidad de un estado a otro.  
Es decir, los movimientos se etiquetan con eventos que, si ocurren, hacen que la entidad cambie de un estado a otro.
Sin embargo, estas ocurrencias pueden estar restringidas por las condiciones de los guardias. 
Por ejemplo, el evento de inicio de sesión sólo puede enviar el sistema a un estado de registro si la contraseña es correcta.
Gráficamente, los eventos se representan en los flujos mediante expresiones simples, 
y las condiciones de guardia se representan entre paréntesis, como en el caso de los diagramas de actividad.
Las transiciones en un diagrama de máquina de estados también pueden incluir efectos que se realizan en respuesta a una transición de estado. 
Por ejemplo, la transición activada por el evento de login y protegida por la condición [password correct] puede activar la acción / condecer acceso, 
que es un efecto de la transición (no su causa). Las acciones asociadas a las transiciones están representadas por expresiones iniciadas por una barra oblicua (/).  
Como ejemplo de cómo ese diagrama puede ser útil durante el análisis de negocios, 
podemos imaginar que un equipo está interesado en comprender el ciclo de vida de un libro en la librería.  
Examinar los diferentes estados de un objeto de negocio clave, como un libro para este proyecto,  
puede reducir el riesgo de subestimar la complejidad de los requisitos del sistema.
Así, el equipo puede descubrir que el libro está registrado inicialmente en el catálogo de una editorial.   
La librería puede entonces pedir un juego de copias del libro. Cuando llega la entrega, el libro se añade al stock y se pone a la venta.   
Una vez vendido, el libro se retira del almacén y se lleva al departamento de envíos.   
En algunas situaciones, los libros pueden regresar a la librería, por ejemplo, debido a una dirección incorrecta o por haber sido dañados durante el envío.  
En el primer caso, la librería debe ponerse en contacto con el cliente y, dependiendo del él, puede cancelar la venta o reenviar el libro.  
El ciclo de vida del libro termina sólo cuando el transportista confirma la entrega.   
Todos esos cambios de estado (transiciones) están representados en la Figura 2.12.

TODO: FFFF

Figura 2.12 Primer modelo de máquina para el ciclo de vida del libro.

Sin embargo, el modelo presentado en la Figura 2.12 todavía está incompleto en cuanto a las posibles transiciones de un libro.  
Por ejemplo, un libro entregado puede devolver dañado y, en ese caso, no puede ser reenviado o vendido de nuevo. 
Esto puede representarse añadiendo una condición de guarda a la transición que va del estado Retornado al estado Enviado,   
y añadiendo un nuevo estado final en el que el libro se desecha, como se muestra en la Figura 2.13.


Figura 2.13 Diagrama de Máquina de Estado con requisitos de guarda.

Estas condiciones de guardia siguen siendo muy informales. Pero esto es aceptable durante el modelado de negocios, porque el objetivo es entender la organización del negocio, no especificar un sistema computacional. Sin embargo, se pueden obtener condiciones de protección precisas si se utiliza un lenguaje formal como el OCL (Object Constraint Language). Más adelante en este libro se introducen expresiones que utilizan OCL.
En algunas situaciones es posible que un evento cause una transición desde más de un estado. En el ejemplo de la Figura 2.13, se puede imaginar que un libro no sólo puede ser dañado cuando está en estado Devuelto, sino también cuando está en otros estados como En almacén y Vendido. Entonces, debería existir una transición a Desechado desde esos tres estados. Sin embargo, para abreviar este conjunto de transiciones se puede utilizar un superestado.
En la Figura 2.14, cualquier transición desde el superestado En almacén representa un conjunto de transiciones desde cada uno de sus subestados. En el caso de una transición al superestado, es necesario establecer cuál de los substados sería el inicial. Para ello es necesario incluir un estado inicial dentro del superestado o, en su lugar, hacer que la transición vaya directamente al subestado.

TODO :FFFF

Figura 2.14 Diagrama de Maquina de Estado con superestado.

Un objeto puede estar simultáneamente en más de un estado. 
Por ejemplo, un libro puede ser una oferta especial o no desde el momento en que se encarga a la editorial hasta el momento en que llega a su estado final 
como liberado o vendido.  
Así, un libro puede ser modelado con dos estados concurrentes: el primero determina si es una oferta especial o no,  
y el segundo determina su estado con respecto a las ventas.  
En el diagrama de la Figura 2.15 los estados concurrentes se representan dentro de regiones ortogonales en un superestado.

TODO: FFFF

Figura 2.15 Diagrama de maquina de estado con regiones.

Cuando una transición deja el superestado, entonces todos los subestados concurrentes también quedan. 
Por ejemplo, cuando ocurre una confirmación de llegada o un evento de descarte en el diagrama de la Figura 2.15, 
ambos estados concurrentes dejan de estar activos y se considera que el libro está en un estado final.
El análisis de los estados de un libro podría continuar. 
Por ejemplo, sería posible determinar que un libro en estado Vendido, 
Devuelto o Enviado no pueda cambiar el precio de precio normal a oferta especial y viceversa. 
Eso podría ser modelado agregando una condición de guardia a las transiciones desde los estados Precio normal y Oferta especial: 
[no en el estado Vendido, Enviado o Devuelto].
La utilización de un diagrama de máquina de estado para representar un objeto de negocio es útil para mejorar el descubrimiento de los requisitos del sistema relacionados con algunos objetos de negocio clave, como se muestra en la Sección 3.4.

## 2.6 Observaciones

Es importante recordar que el objetivo del modelado de negocio suele ser encontrar una visión general del negocio, 
y no una especificación detallada de sus procesos. 
Así, en la mayoría de los casos, el objetivo del equipo es concentrarse en descubrir información sobre el negocio, 
y no en especificar formalmente cómo funciona el negocio como si fuera una máquina.  
Todavía se puede hacer una pregunta: ¿Qué elementos del negocio merecen la producción de una máquina de estado o un diagrama de actividad? 
A menos que se indique lo contrario, no es aconsejable preparar un diagrama para cada uno de los elementos de la empresa, 
porque, si se hace, la ejecución de Inicio llevaría demasiado tiempo y sus objetivos se verían obstaculizados.   
Lo que normalmente se necesita en ese momento es un modelo para algunos elementos clave, de modo que su comportamiento pueda ser mejor comprendido y sus necesidades puedan ser derivadas más tarde.
Una pista para identificar esos elementos clave es preguntarse cuáles son los objetos de negocio.   
En el caso de una librería, son libros, en el caso de un hotel, alojamiento, en el caso de un tribunal, procesos penales, etc.  
Por lo tanto, estos son los elementos clave que deben ser modelados en mayor detalle para ayudar a entender el negocio.  
Una segunda pregunta podría ser la siguiente: ¿Qué diagrama debemos usar - actividad o máquina de estados?   
La respuesta depende de la naturaleza del elemento a modelar.  
Un estado no corresponde necesariamente a una actividad. Un televisor, por ejemplo, puede estar en estado apagado, cuando no está haciendo nada.  
Un diagrama de actividades es útil para modelar personas, organizaciones o sistemas que hacen cosas.   
Por otro lado, el diagrama de máquina de estados es útil cuando una sola entidad pasa por diferentes estados en los que no necesariamente está haciendo algo. Además, el diagrama de actividad suele detallar un caso de uso de negocio (es decir, un proceso como la venta, la compra, la comprobación, etc.), mientras que el diagrama de máquina de estados suele asociarse a un objeto de negocio (como libros, personas, pedidos, etc.).
Sin embargo, el modelado de negocios no se trata sólo de construir diagramas.   
El propósito de los diagramas es ayudar a entender el contexto y los requisitos generales iniciales de un proyecto y un sistema. 
El modelado de negocios es una de las actividades clave que ayuda a un equipo a identificar y prepararse para los riesgos del proyecto. 
También se pueden realizar otras actividades de mitigación de riesgos durante la fase inicial, como pruebas de concepto, talleres, prototipos, pruebas previas, etc. Cualquier estrategia que ayude a comprender el panorama general e identificar los principales riesgos y complejidades de un proyecto es válida.

## 2.7 El proceso hasta ahora


|                                    | Inicio | Elaboración | Construcción | Transición |
| ---------------------------------- | ------ | ----------- | ------------ | ---------- |
| Modelado del Negocio               | [MI](#MI)     |             |              |            |
| Requerimientos                     |        |             |              |            |
| Analisis y Diseño                  |        |             |              |            |
| Implementación                     |        |             |              |            |
| Pruebas/Test                       |        |             |              |            |
| Gestión de Proyectos               |        |             |              |            |
| Despliegue                         |        |             |              |            |
| Configuración y Gestión del cambio |        |             |              |            |
| Entorno                            |        |             |              |            |

### MI
Construir una vista general del sistema:  
- Dibujar un caso de uso del negocio y determinar el ámbito de automatización para el proyecto.
- Dibujar un diagrama de actividad para el caso de uso del negocio
- Dibujar un diagrama de maquina de estado para los procesos clave del sistema



## 2.8 Preguntas
1. ¿Cuál es el propósito del modelado de negocios?
2. El modelado de negocios puede ocurrir con diferentes niveles de intensidad para diferentes tipos de proyectos. Explique y dé ejemplos!k
3. ¿Cuál es la diferencia entre un trabajador empresarial y un actor empresarial?
4. ¿Qué aspectos de un negocio pueden ser detallados en un diagrama de actividades? ¿Cuál puede ser detallado por un diagrama de máquina de estados?



            


















