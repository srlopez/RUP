# PLANIFICAR el proyecto basado en CASOS DE USO

        ​ Panificar el proyecto basándose en los casos de uso

Este capítulo muestra cómo planificar y desarrollar un proyecto utilizando iteraciones, análisis de riesgo y estimación del esfuerzo basado en casos de uso de alto nivel. Explica cómo se estima el esfuerzo para desarrollar el proyecto basándose en la complejidad percibida de cada caso de uso y otras características del sistema y del equipo de desarrollo. Finalmente, el capítulo explica cómo organizar una serie de iteraciones incrementales basadas en una lista priorizada de casos de uso y riesgos, que es la columna vertebral del plan de desarrollo con el Proceso Unificado.

                ​ Palabras clave
Use case point analysis; risk analysis; effort estimation; iteration; project planning

            ​ 4.1 Introducción a la estimación del esfuerzo y al análisis de riesgos en proyectos de software
La motivación para la estimación del esfuerzo en proyectos de software proviene del hecho de que, históricamente, la mayoría de los proyectos de desarrollo de software:
• Requieren más tiempo para completarse de lo esperado.
• Cuesta mucho más de lo esperado.
• Resulta un producto que no tiene la calidad necesaria.
• Resulta un producto que no tiene el alcance esperado.
Por lo tanto, el hecho es que los equipos de desarrollo de software y los clientes deben aprender a cumplir el plazo, el costo, la calidad y el alcance adecuados con respecto a su proyecto y su equipo. Las técnicas de estimación del esfuerzo se utilizan para lograr dichos objetivos.

                ​ 4.1.1 Técnicas a medida
En las últimas décadas se han propuesto y utilizado una serie de técnicas para la estimación del esfuerzo. Una de las más populares es la técnica de Smith, que puede resumirse como "Smith, ¡dinos cuánto tiempo necesitas para desarrollar ese sistema! Una variación de la técnica de Smith es la técnica de Smith, que puede resumirse como "Smith, tienes tres meses para desarrollar ese sistema". Aunque popular (y conocido por otros nombres, como Susan, Peter, Mary, etc.), este enfoque no es muy preciso.
Otra técnica ad-hoc que se utiliza es la técnica de los seis meses. Consiste en estimar "seis meses" para cualquier proyecto de software al inicio de su desarrollo y luego ajustarlo hacia arriba o hacia abajo a medida que se descubren el alcance y los requisitos. Las variaciones de esta técnica son prácticamente infinitas, incluyendo la técnica de Un Año y la técnica de Dieciocho Meses, entre otras.
Este tipo de técnicas se conocen como estimación no paramétrica porque no se basan en medidas sobre el proyecto a desarrollar. Somerville (2006) identifica algunas otras técnicas no paramétricas:
    • Juicio experto. La técnica del juicio experto propone que uno o más expertos en el dominio del proyecto y el desarrollo de software se reúnan y utilicen su experiencia para producir una estimación. La técnica de Smith es un escenario potencialmente malo para la técnica del juicio experto: la técnica puede ser muy imprecisa, dependiendo de la experiencia de los estimadores. Sin embargo, si los expertos realmente tienen experiencia en proyectos similares, es una técnica factible, rápida y relativamente barata.
    • Estimación por analogía. Esa técnica es de hecho la base pragmática de la técnica del juicio experto. Se supone que el esfuerzo para desarrollar un nuevo sistema será similar al esfuerzo para desarrollar otros sistemas similares. Esta técnica no es factible si no se dispone de proyectos similares para su comparación. Puede hacer buen uso de uno o más expertos para determinar qué es lo que califica como un sistema similar y cómo el tiempo empleado en desarrollarlo puede ser utilizado como base para estimar el esfuerzo para el proyecto actual. Por lo tanto, esta técnica puede evolucionar hasta convertirse en un juicio experto.
    • Ley de Parkinson. Esta técnica no suele adoptarse abiertamente, pero es recurrente en los proyectos de software y en otras áreas: el proyecto cuesta los recursos disponibles. La ventaja es que el proyecto no costará más de lo esperado, pero con frecuencia el alcance del sistema no estará completamente cubierto.
    • Precio a obtener. El costo del proyecto es igual al precio que se cree que ganará con el contrato. La desventaja de este método es que el sistema que obtiene el cliente puede no ser el que esperaba, porque como los costos deben ser reducidos, esto puede afectar la calidad y el alcance. Sin embargo, cuando no hay información detallada sobre el sistema y el equipo carece de experiencia en técnicas de estimación más avanzadas, se puede elegir esta técnica: el coste del proyecto se acuerda sobre la base de acuerdos comunes y el desarrollo se ve limitado por el coste.
La comunidad ágil suele adoptar una estrategia de estimación que se basa en los puntos de historia. Una historia de usuario es un escenario de uso de un sistema, y es algo similar a un caso de uso. Sin embargo, los casos de uso son más estructurados y formales; son producidos por un equipo de analistas. Por otra parte, las historias de los usuarios deben ser escritas por ellos mismos. Deben representar un escenario en el que los usuarios se vean a sí mismos utilizando el sistema que se va a producir. La idea detrás de esto es que los usuarios presenten primero las necesidades que son más importantes para ellos; los detalles serán recordados más tarde.
Un punto de historia se considera un día de trabajo ideal (de 6 a 8 horas enfocado y dedicado a un proyecto). El esfuerzo de estimación se calcula para cada historia de usuario en términos de puntos de historia. La pregunta que debe responder el equipo es: "¿Cuántos días ideales x personas tardarían en desarrollar una historia de usuario determinada? Si la respuesta es x, las personas tardarían y días, entonces el número de puntos de la historia es x*y. La asignación de puntos de historia es subjetiva y puede considerarse una técnica no paramétrica. El equipo suele evaluar el esfuerzo basándose en su experiencia en proyectos anteriores similares. La asignación se realiza en base al esfuerzo, la complejidad y el riesgo. Por ejemplo, se podrían hacer las siguientes preguntas:
    • Complejidad: ¿Tiene esta historia de usuario muchos escenarios posibles?
    • Esfuerzo: ¿Se va a hacer el cambio en muchos componentes diferentes?
    • Riesgo: ¿Alguien del equipo conoce la tecnología necesaria para desarrollar esta historia?
Otra forma de estimar las historias de los usuarios es colocar todas las historias de los usuarios en tarjetas sobre la mesa. Luego, se separan los más sencillos de desarrollar y se les asigna un punto de historia o menos. Después de eso, se separan las historias más simples de las restantes y se les asignan dos puntos de historia. Este procedimiento se repite hasta que no queden más historias de usuarios sobre la mesa. Se sugiere que cada iteración aumente el número de puntos de la historia siguiendo una serie similar a la serie de Fibonacci como 0, ½, 1, 2, 3, 5, 8, 13, 20, 40, 100, etc.1 El razonamiento detrás de esto es que para un humano promedio es difícil calcular cuánto pesa un caballo; sin embargo, la mayoría de la gente estará de acuerdo en que un caballo pesa más que un perro y menos que un elefante.
Si se determina que una historia de usuario requiere menos de un día de trabajo ideal, debe adjuntarse a otra historia, y las historias que están por encima de un límite dado (por ejemplo, 10 puntos de historia) deben dividirse en historias más simples.

                ​ 4.1.2 Técnicas paramétricas 
Otra clase de técnicas de estimación incluye las paramétricas que tienen como objetivo presentar una estimación del esfuerzo basada en el tamaño estimado del sistema, la dificultad técnica para desarrollarlo y la capacidad del equipo, entre otras características. El tamaño del sistema puede medirse en términos de:
    • Líneas de código. Técnicas como COCOMO II - COnstructive COst MOdel II (Boehm, 2000) comienzan a estimar cuántas líneas de código fuente (SLOC) tendrá el sistema. De hecho, como la mayoría de los sistemas tienen miles de líneas de código, la medida usual es el kilo de líneas de código fuente (KSLOC).
    • Puntos de función. Las técnicas basadas en el análisis de puntos de función (FPA) (Albrecht, 1979) y sus variaciones no se refieren a las líneas de código. Estiman que el esfuerzo para desarrollar un sistema depende de la funcionalidad aparente que se va a implementar. Por lo tanto, normalmente estas técnicas cuentan el número de requisitos funcionales y evalúan su complejidad preguntando cuántas clases o registros de datos necesitan utilizar para ser implementados y cuántos argumentos envía o recibe un usuario desde el sistema para realizar la función.
    • Usar puntos de caso. Es una variación de la técnica de análisis de puntos de función que se basa en casos de uso en lugar de requisitos funcionales para la estimación. Esta técnica se explica en detalle en la Sección 4.2.
Aunque COCOMO II es la técnica más detallada, tiene una desventaja en comparación con los puntos de función y los puntos de caso de uso: el número de KSLOC debe ser estimado por los especialistas antes de aplicar el método, y esto es una fuente significativa de incertidumbre.2 Los puntos de función y los puntos de caso de uso se basan en los requisitos, que pueden conocerse al principio de un proyecto (por supuesto, los requisitos pueden cambiar durante el desarrollo, pero cuando cambian la estimación puede actualizarse inmediatamente de manera sistemática).
Además del tamaño del sistema medido en líneas de código o funcionalidad aparente, las técnicas paramétricas también utilizan factores de ajuste técnico. Se supone que la implementación de una función del mismo tamaño puede ser más fácil o más difícil dependiendo del tipo de sistema que se esté desarrollando. Por ejemplo, un sistema de información como Livir es más sencillo de implementar que un sistema de cirugía robótica o un sistema central integrado en un avión. La misma cantidad de líneas de código fuente puede tardar más o menos tiempo en desarrollarse dependiendo de la complejidad técnica del sistema.
La técnica más completa en cuanto a los factores de ajuste técnico es COCOMO II, que propone el uso de hasta 16 multiplicadores de esfuerzo divididos en cuatro grupos:
    • Atributos del producto. Estos incluyen la fiabilidad requerida para el software, el tamaño relativo de la base de datos de pruebas, la complejidad interna del producto, el desarrollo destinado a la reutilización y la cantidad de documentación esperada y necesaria.
    • Atributos de hardware. Estos incluyen aspectos relacionados con la eficiencia en el tiempo y el espacio y la volatilidad de la plataforma de desarrollo.
    • Atributos del personal. Estos incluyen la capacidad de los analistas y programadores, la continuidad del personal, la experiencia en aplicaciones similares y la experiencia en la plataforma, el lenguaje de programación y otras herramientas de software.
    • Atributos del proyecto. Estos incluyen el uso de herramientas de ingeniería de software asistido por computadora (CASE), la distribución del equipo de desarrollo y la necesidad de acelerar el programa de desarrollo.
Los puntos de uso de casos y puntos de función tienen multiplicadores de esfuerzo similares, pero con una organización diferente y a veces una interpretación diferente. En ambos métodos, los multiplicadores de esfuerzo son un índice numérico que se multiplica por el tamaño estimado del sistema para producir una estimación del esfuerzo. Sin embargo, COCOMO II tiene una característica única: un conjunto de factores de escala. Existen cinco de estos factores:
    • Precedencia. ¿El producto es similar a otros que ya fueron desarrollados por el mismo equipo?
    • Flexibilidad de desarrollo. ¿El producto tiene que ser desarrollado directamente de los requisitos o los requisitos son sólo objetivos generales?
    • Arquitectura y resolución de riesgos. ¿Existe un buen apoyo para resolver los riesgos y los problemas arquitectónicos?
    • Cohesión de equipo. ¿Han trabajado juntos antes? ¿Están bien integrados?
    • Madurez del proceso. ¿Cuál es la madurez de la organización? CMMI3 (SEI-CMU, 2010) y SPICE4 (Emam, Melo & Drouin, 1997) pueden utilizarse como medida de madurez. COCOMO II también propone un cuestionario sencillo que ayuda a estimar la madurez de la organización si no se dispone de otras evaluaciones.

La diferencia aquí es que esos factores de escala no se multiplican por el tamaño del sistema: se utilizan de forma exponencial. Los valores medios (cerca de 1) de estos factores significan una escala nominal en la que cada línea de código produce los mismos costes independientemente del tamaño del software. Si los factores de escala son malos, entonces su valor numérico es mayor que 1 y esto significa que una línea de código en un sistema más grande cuesta más que una línea de código en un sistema más pequeño. Si los factores de escala son buenos, entonces el equipo gana en escala, es decir, una línea de código en un sistema más grande cuesta menos que una línea de código en un sistema más pequeño.

                ​ 4.1.3 Análisis de riesgos
Un riesgo es algo que puede ocurrir y causar problemas.5 Los riesgos son muy frecuentes y numerosos en los proyectos de software. Existen diferentes categorías de riesgo y tienen diferentes impactos: hay algunos que son sólo una molestia y otros que pueden causar la terminación del proyecto. Por lo general, el proceso de hacer frente a los riesgos implica:
    • Identificación. El equipo debe descubrir y ser consciente de las condiciones que pueden desencadenar problemas en un proyecto. Listas de control como la de Carr et al. (1993) pueden ayudar al proceso de identificación.
    • Análisis. Se analizan los riesgos para descubrir algunos de sus atributos. Por lo general, se deben identificar al menos dos atributos: la probabilidad de que ocurra la condición que desencadena el riesgo, y el impacto que el riesgo tiene en el proyecto. La exposición o importancia de un riesgo es una combinación de probabilidad e impacto. Por lo general, los riesgos con alta probabilidad de ocurrencia y alto impacto en el proyecto son los más importantes.
    • Planificación. Una vez evaluada la exposición a los riesgos, se deben planificar los riesgos de exposición media y alta y el proyecto debe incluir actividades para minimizar la probabilidad y/o el impacto de los riesgos más importantes. Estos planes son los planes de mitigación. Además, los planes de recuperación o de contingencia también deben prepararse para los riesgos más importantes y se ejecutarán si, a pesar de las actividades de mitigación, el riesgo sigue siendo un problema.
    • Control. Los riesgos de un proyecto son aún más inestables que sus requisitos: cambian con frecuencia y de forma inesperada. Durante el desarrollo se descubren nuevos riesgos y su importancia puede cambiar. Por lo tanto, el director del proyecto debe ser consciente de ello y prestar mucha atención a la situación de los riesgos durante todo el proyecto.
Se pueden identificar diferentes fuentes de riesgo. Carr et al (1993) presenta la siguiente estructura:
Ingeniería de producto:
    • Requisitos: ¿Son estables, completos, claros, válidos y factibles? ¿Es el proyecto algo que nunca se ha hecho antes? ¿Es el proyecto más grande que cualquier otro que la organización haya emprendido anteriormente?
    • Diseño: ¿Es difícil de obtener? ¿Son claras y sencillas las interfaces con otros sistemas? ¿Existen limitaciones de rendimiento, testeabilidad y hardware? ¿Se utilizará software desarrollado fuera de la empresa?
    • Código y pruebas: ¿Es factible la implementación? ¿Es suficiente el tiempo reservado para las pruebas?
    • Integración y test: ¿Es adecuado el entorno de integración y de pruebas?
    • Aspectos de ingeniería: ¿El software será fácil de mantener? ¿Son fáciles de obtener y verificar los requisitos de confiabilidad, seguridad y protección? ¿Existen factores humanos especiales a tener en cuenta? ¿Es la documentación adecuada para el proyecto?
Entorno de desarrollo:
    • Proceso de desarrollo: ¿Existe un proceso de desarrollo claro y probado en uso? ¿Se controlan formalmente los planes? ¿Es el proceso adecuado para este tipo de sistema? ¿Los miembros del equipo conocen y utilizan el proceso? ¿Existen mecanismos claros para gestionar los cambios en el producto?
    • Sistema de desarrollo: ¿Existe un hardware adecuado y otras herramientas para el desarrollo del proyecto? ¿Las herramientas son fáciles de usar? ¿Sabe el equipo cómo usar las herramientas? ¿Son fiables las herramientas?
    • Proceso de gestión: ¿Son adecuados los planes? ¿Incluyen planes de contingencia? ¿Están bien definidas las funciones y la autoridad dentro del proyecto? ¿Los directores tienen experiencia? ¿Cómo se comunica el equipo con otras partes interesadas?
    • Método de gestión: ¿Existen métricas que ayuden a la gestión? ¿Se capacita al personal del proyecto? ¿Es adecuada la gestión de la calidad? ¿Se controla la configuración del código y otros artefactos?
    • Entorno de trabajo: ¿El equipo se preocupa por la calidad? ¿El equipo es cooperativo? ¿Es buena la comunicación entre los miembros del equipo? ¿La moral del equipo está alta?
Restricciones externas:
    • Recursos: ¿Es fiable y estable el programa? ¿El equipo tiene experiencia y es capaz? ¿Es adecuado el presupuesto? ¿Las instalaciones son adecuadas?
    • Restricción: ¿Qué tipo da restricción existe? ¿Existen restricciones contractuales? ¿Depende el proyecto de socios externos?
    • Interfaces de comunicación: ¿Existen problemas con el cliente, como una comunicación débil o un conocimiento incompleto del dominio?
    • Personal subcontratado: ¿Existen problemas con las empresas asociadas, como interfaces débiles, mala comunicación o falta de colaboración? ¿Depende el proyecto de ellos?
    • Contratista principal: Si usted es una empresa subcontratada, ¿hay algún problema con el contratista principal?
    • Gestión: ¿Está ausente el responsable máximo o se trata de un microdelegado?
    • Vendedores: ¿Los vendedores de productos que está utilizando resuelven los problemas rápidamente?
    • Políticas: ¿Las políticas están creando problemas para el proyecto?
Esta lista es sólo una referencia; muchos otros riesgos impredecibles pueden aparecer en la mayoría de los proyectos.
Después de ser identificados, los riesgos deben ser analizados. Se pueden identificar muchos atributos de riesgo. Entre ellos, quizás los más importantes son:
    • Probabilidad: La posibilidad de que un riesgo se convierta en un problema. Si existe una serie histórica de datos, la probabilidad de riesgo puede medirse numéricamente. Sin embargo, la mayoría de los riesgos se evalúan utilizando la escala de camisetas, donde "alto" significa que es casi seguro que el riesgo se convertirá en un problema, "medio" significa que se espera que el riesgo se convierta en un problema, y "bajo" significa que la probabilidad de que el riesgo se convierta en un problema es mínima.
    • Impacto: El precio a pagar (monetario o no) cuando el riesgo se convierte en un problema. Una vez más, se pueden utilizar medidas numéricas si se dispone de suficiente información. Para la mayoría de los proyectos, el impacto del riesgo podría evaluarse como "alto" (puede poner fin al proyecto), "medio" (puede aumentar significativamente los costes del proyecto) y "bajo" (puede causar algunos problemas, pero las pérdidas son fácilmente recuperables).
    • Importancia o exposición: La combinación de probabilidad e impacto, tal como se expresa en la Tabla 4.1.- Probabilidad: La posibilidad de que un riesgo se convierta en un problema. Si existe una serie histórica de datos, r


Tabla 4.1
Cómo calcular la exposición a un riesgo


Probabilidad

Alta
Media
Baja
Impacto
Alto
Alta exposición
Alta exposición
Exposición media

Medio
Alta exposición
Exposición media
Baja exposición

Bajo
Exposición media
Baja exposición
Baja exposición

Los riesgos de exposición alta y media deben tener planes de mitigación para reducir la probabilidad y/o el impacto. En el caso de riesgos de alta exposición, es aconsejable ejecutar los planes lo antes posible, mientras que los riesgos de exposición media pueden abordarse más adelante. Por lo tanto, las actividades de mitigación de riesgos se incluirán en el esfuerzo del proyecto en este momento. Los riesgos de baja exposición sólo pueden ser monitoreados para detectar si su exposición cambia durante el proyecto.
Entre otras posibles definiciones, se puede decir que un riesgo se compone de tres partes:
    • Causa: Una condición incierta que puede crear problemas.
    • Problema: Una situación que podría ocurrir dada la incertidumbre de la causa.
    • Efecto: Un impacto sobre uno o más de los objetivos del proyecto.
Por lo tanto, hay tres tipos de planes que pueden estar asociados a los riesgos:
    • Plan de mitigación para reducir la probabilidad de riesgo: Debe actuar sobre la causa del riesgo, reduciendo la probabilidad de que ocurra.
    • Plan de mitigación para reducir el impacto del riesgo: Debe actuar sobre los efectos del riesgo, reduciendo el coste de la recuperación si el riesgo se convierte realmente en un problema.
    • Plan de contingencia o plan de recuperación de desastres: Indica qué hacer después de que el riesgo se convierte en un problema, es decir, actúa sobre el problema creado por el riesgo.
Los planes de mitigación son preventivos: deben ejecutarse antes de que el riesgo se convierta en un problema. Por otra parte, los planes de contingencia se llevan a cabo sólo si el riesgo se convierte realmente en un problema.
La Tabla 4.2 presenta un ejemplo con algunos riesgos relacionados con el proyecto Livir y una simple declaración de acciones de mitigación y contingencia. Sin embargo, si fuera necesario, se podrían elaborar planes más detallados.


Tabla 4.2
Ejemplo de Riesgos y Planes para el Proyecto Livir

Código
Riesgo
Atributos del riesgo
Plan de reducción de la probabilidad
Plan de reducción del impacto
Plan de contingencia

Causa
Problema
Efecto
Prob.
Imp.
Exp.



K1
Requisitos inestables
Los requisitos clave pueden cambiar durante el desarrollo
Tiempo perdido desarrollando partes que no serán utilizadas
A
A
A
Aplicar un cuidado especial en la selección de requisitos. Estudiar productos similares. Desarrollar prototipos para validar los requisitos.
Enfatizar el desarrollo modular. Implementar un sistema eficiente de control de versiones.
Usar un sistema de gestión de l cambio para controlar adecuadamente los cambios en los requisitos 
K2
Equipo sin experiencia
Pueden realizarse malas decisiones de diseño
Código difícil de mantener y lleno de defectos
A
M
A
Contratar un arquitecto de software experto para coordinar y validar las decisiones de diseño
Usar pruebas automáticas intensamente para encontrar defectos.
Reescribir código para mejorar el diseño.
K3
El equipo no está familiarizado con  el protocolo de comunicación de los operadores de tarjetas de crédito
Mala o ineficiente interfaz de comunicación con los operadores de tarjetas
Errores en las operaciones de crédito
A
B
A
Desarrollar un prototipo descartable para estudiar el protocolo de comunicaciones del sistema operador de créditos
Implementar procedimientos de doble-check para las operaciones de tarjeta basado en invariantes y postcondiciones.
Seguridad de doble-check en las operaciones de tarjetas.
Interrumpir las operaciones con tarjetas hasta que el problema se haya resuelto.


Los riesgos deben ser monitorizados durante el desarrollo del proyecto. Como suelen hacer los requisitos, el riesgo puede cambiar con el tiempo. Incluso sus nombres y propiedades pueden cambiar. Por eso, los riesgos se identifican mediante un código: para hacer un seguimiento de los mismos incluso cuando cambian.

            ​ 4.2 Análisis de los Puntos de caso de uso
Una vez que se han identificado los casos de uso del sistema, se puede estimar el esfuerzo necesario para desarrollarlos. Además, los casos de uso deben ser priorizados para que los casos de uso más importantes sean desarrollados primero. En procesos iterativos como el Proceso Unificado, se desarrollará un conjunto relativamente pequeño de casos de uso en cada iteración. Por lo tanto, la planificación de un proyecto que utiliza este tipo de proceso consiste en determinar un plan general o un plan de fase y un conjunto de planes de iteración que determinan qué casos de uso o riesgos se abordarán en cada iteración. Por eso es importante determinar las prioridades de un proyecto y estimar el esfuerzo necesario para desarrollarlas. Durante el Inicio, sólo se construye el plan de esta fase y el plan para la primera iteración de la Elaboración. Cada iteración adicional se planifica mientras se realiza la anterior.
La planificación de fases e iteraciones son actividades típicas de la gestión de proyectos. La estimación del esfuerzo es una herramienta de planificación que indica, entre otras cosas, cuánto tiempo y personal se necesita para el proyecto.
La técnica conocida como puntos de caso de uso (Karner, 1993) se basa en puntos de función (Albrecht & Gaffney Jr., 1983), específicamente en la técnica de conteo MK II o Mark II (Symons, 1988), que es un enfoque relativamente más simple que el del IFPUG (International Functional Point Users Group).7
El análisis de puntos de caso de uso es más sencillo que el análisis de puntos de función, pero todavía no dispone de informes sólidos sobre su aplicación a un gran número de proyectos, como el análisis de puntos de función y COCOMO II. Otro problema con el análisis de casos de uso es que la comprensión del equipo sobre lo que constituye un caso de uso puede producir estimaciones dispares. COCOMO II sufre de un problema similar porque se basa en una estimación aproximada del número de líneas de código a ser producidas, pero permite a los estimadores usar una tabla de contrafuego (Center for Software Engineering USC, 2000) para convertir los puntos de función en líneas de código (con diferentes tasas de conversión dependiendo del lenguaje utilizado). Además, el análisis de los puntos de función también depende de la capacidad de los estimadores y de la capacidad de los analistas para identificar el conjunto correcto y completo de requisitos. La conclusión es que cada técnica tiene un punto débil; sin embargo, un equipo que está bien afinado, con registros históricos de estimaciones de proyectos anteriores, y que aplica los mismos patrones y convenciones cuando desarrolla software, produciría mejores estimaciones que un equipo sin experiencia, independientemente del método de estimación que utilice. Todos los métodos dependen de un buen historial de esfuerzo de estimación y de la calidad de los parámetros obtenidos para el proyecto actual (líneas de código, requisitos funcionales o casos de uso).
La técnica de análisis de casos de uso se incorporó al Proceso Unificado porque ese proceso está fuertemente basado en casos de uso. Como ya se ha dicho, una de las mayores dificultades para su aplicación no es el método en sí, que es muy sencillo, sino la falta de estandarización sobre lo que es efectivamente un caso de uso (Anda, 2001). Debido a la ausencia de un estándar internacional, el equipo puede crear y utilizar su propio entendimiento de la granularidad adecuada para los casos de uso.
El análisis de puntos de caso de uso se basa en la cantidad y complejidad de los actores del sistema y los casos de uso, que corresponden al valor de puntos de caso uso no ajustados (UUCP). La aplicación de factores técnicos y ambientales conduce al UCP, o casos de uso ajustados.
UUCP se calcula a partir de la complejidad estimada de los actores (UAW - peso de actor no ajustado) y casos de uso (UUCW - peso de caso de uso no ajustado), como se discute en las siguientes subsecciones.

                ​ 4.2.1 Peso no ajustado del actor - UAW – unadjusted actor weight
El método para asignar la complejidad a los actores es bastante simple. Cada actor se cuenta una vez, aunque esté asociado a muchos casos de uso. En el caso de los actores que son especializaciones de actores más genéricos, sólo se cuentan las especializaciones más elementales, es decir, actores que no tienen subtipos.
Una vez identificados los actores, su complejidad se define de la siguiente manera:
    • Los actores humanos que interactúan con el sistema a través de una interfaz gráfica de usuario son considerados complejos y reciben 3 puntos de caso de uso.
    • Otros sistemas que interactúan con el sistema a través de un protocolo como TCP/IP y actores humanos que interactúan con el sistema sólo a través de una línea de comandos son considerados de mediana complejidad y reciben 2 puntos de caso de uso.
    • Otros sistemas a los que se accede mediante interfaces de programación de aplicaciones (API) son considerados de baja complejidad y reciben 1 punto de caso de uso.
El valor del peso de actor no ajustado -UAW- es simplemente la suma de los puntos asignados a todos los actores del sistema.
En el ejemplo de la Figura 3.11 se consideraron los siguientes actores:
    • Gestor de depósitos: 3 puntos.
    • Gerente de adquisiciones: 3 puntos.
    • Gerente de ventas: 3 puntos.
    • Cliente: 3 puntos.
    • Sistema de operador de tarjeta de crédito: 2 puntos.
Así, para ese ejemplo, UAW=3+3+3+3+3+2=14.
Sin embargo, el uso de el UAW para la estimación del esfuerzo no se acepta unánimemente. A veces, se sugiere que puede ser ignorado en las ecuaciones. Por lo general, incluso las herramientas de recuento de UCP consideran el UAW como una medida opcional y su uso o no es una decisión que se deja en manos del equipo.

                ​ 4.2.2 Peso del caso de uso no ajustado - UUCW – unadjusted use case weight
Los casos de uso también se cuentan una vez. Sólo deben contarse los procesos completos. Esto significa que las extensiones, variantes y otros fragmentos, en general, no deben ser contados.
En la propuesta original de Karner (1993), la complejidad de un caso de uso se define sobre la base del número estimado de transacciones (información que se envía al sistema o se recibe del mismo), incluyendo secuencias alternativas (ver Capítulo 5 para más detalles). Entonces, los casos de uso podrían caracterizarse de la siguiente manera:
    • Casos de uso sencillo: No más de tres transacciones.
    • Casos de uso medio: De cuatro a siete transacciones.
    • Casos de uso complejos: Más de siete transacciones.
Sin embargo, si estamos trabajando con casos de uso de alto nivel, puede ser difícil saber con seguridad cuántas transacciones tiene realmente cada caso de uso, y eso hace que esa estimación sea un poco arriesgada.
Una forma alternativa de estimar la complejidad de un caso de uso es por el número de clases necesarias para implementar las funciones del caso de uso. Así:
    • Los casos de uso simple deben implementarse con cinco clases o menos.
    • Los casos de uso medio deben implementarse con seis a diez clases.
    • Los casos de uso complejo deben implementarse con más de diez clases.
El número de clases necesarias para implementar un caso de uso dependerá también de los requisitos detallados que normalmente no se conocen durante el inicio, dado que los casos de uso aún no se han ampliado. Esto hace que este enfoque también sea un poco arriesgado.
Otra forma de estimar la complejidad de un caso de uso es mediante el análisis de su riesgo. Así:
    • Los informes suelen tener sólo una o dos transacciones y bajo riesgo, ya que no cambian los datos. Se pueden considerar casos de uso simples.
    • Los casos de uso de patrones como CRUD tienen un número de transacciones que son conocidas y limitadas. Su riesgo es medio, porque aunque su lógica interna es conocida, reglas de negocio oscuras pueden afectarles, y pueden ser consideradas de complejidad media.
    • Los casos de uso sin patrón tienen un número desconocido de transacciones, y alto riesgo, porque además de que las reglas de negocio pueden ser desconocidas o malentendidas, incluso la estructura interna del caso de uso es desconocida (su flujo principal y secuencias alternas). Por lo tanto, este tipo de caso de uso se considera complejo.
El valor UUCW (peso del caso de uso no ajustado) viene dado por la suma del valor asignado a cada caso de uso utilizando el siguiente criterio:
    • Caso de uso sencillo: 5 puntos de uso de casos.
    • Caso de uso medio: 10 puntos de uso de casos.
    • Caso de uso complejo: 15 puntos de uso de casos.
Aplicando esta técnica al ejemplo de la Figura 3.11, hay ocho casos de uso estereotipados como informes, que reciben 8*5=40 puntos de uso de casos. También hay tres casos de uso de CRUD (casos de uso de patrones), que reciben 3*10=30 puntos. Por último, hay 10 casos de uso sin estereotipo y con mayor riesgo, que reciben 10*15=150 puntos de caso de uso. Así, la UUCW de este ejemplo es 40+30+150=220.
También hay otras técnicas de conteo. Pero la mayoría de ellas se basan en la versión detallada de un caso de uso. Algunas de ellas se presentan en la Sección 4.2.9.


                ​ 4.2.3 Puntos del caso de uso no ajustado - UUCP – unadjusted use case points
El valor para UUCP, o puntos de caso de uso no ajustados, se calcula como la suma de UAW y UUCW:

UUCP = UAW + UUCW

En el ejemplo, UUCP=14+220=234.
Como se mencionó anteriormente, los pesos de los actores pueden ser excluidos del cálculo de UUCP, y eso haría que UUCP sea inmediatamente igual a UUCW, es decir, UUCP=UUCW=220 en el ejemplo.

                ​ 4.2.4 Factor de complejidad técnica - TCF – technical complexity factor
La técnica de análisis de casos de uso propone que el UUCP se ajuste mediante dos criterios: factores técnicos (que están asociados al proyecto) y factores ambientales (que están asociados al equipo).
Cada factor recibe un peso y una valoración/ratio de 0 a 5, donde 0 significa que no hay influencia en el proyecto, 3 es influencia nominal y 5 es influencia máxima en el proyecto.
Sorprendentemente, esta es la única información que se suele dar en la literatura sobre los factores técnicos del análisis de puntos de caso de uso, y eso hace que la evaluación de estos factores sea altamente subjetiva, e incluso a veces contradictoria.
Existen 13 factores técnicos, cada uno con un peso específico, como se muestra en la Tabla 4.3.

Tabla 4.3
Factores técnicos para ajustar los puntos de caso de uso


Código
Factor
Peso
T1
Sistema distribuido
2
T2
Tiempo de respuesta/objetivos de rendimiento
1
T3
Eficiencia del usuario final
1
T4
Complejidad del tratamiento interno
1
T5
Diseño orientado a la reutilización de código
1
T6
Fácil de instalar
0.5
T7
Fácil de operar
0.5
T8
Portabilidad
2
T9
Diseño con el objetivo de facilitar el mantenimiento
1
T10
Tratamiento concurrente/paralelo
1
T11
Seguridad
1
T12
Acceso para/con código de terceros
1
T13
Necesidades de formación de los usuarios
1

Por otro lado, cada uno de los factores técnicos lo valoramos con  un ratio entre 0 y 5 que se multiplica por su peso. La suma de estos productos corresponde al valor de TFactor, es decir, el impacto de los factores técnicos, y oscila entre 0 y 70.
El TCF (factor de complejidad técnica) puede calcularse ajustando TFactor al rango de 0,6 a 1,3 con la siguiente fórmula:

TCF = 0.6 + (0.01 * Tfactor)

Para una mejor referencia sobre el significado del peso de 0 a 5, se sugiere que se utilicen las siguientes instrucciones, adaptadas de la técnica de análisis de puntos de función (Albrecht & Gaffney Jr., 1983).

T1 - Sistema distribuido: ¿La arquitectura del sistema está centralizada o distribuida?
0. La aplicación ignora cualquier aspecto relacionado con el procesamiento distribuido.
1. La aplicación genera datos que serán procesados por otros ordenadores con intervención humana (por ejemplo, hojas de cálculo o archivos preformateados enviados por medios o correo electrónico).
2. Los datos de aplicación se preparan y se transfieren automáticamente para su procesamiento en otros ordenadores.
3. El procesamiento de la aplicación se distribuye y los datos se transfieren en una sola dirección.
4. El procesamiento de la aplicación se distribuye y los datos se transfieren en ambas direcciones.
5. Los procesos de aplicación deben ejecutarse en el núcleo de procesamiento o en el ordenador más apropiado, que se determina dinámicamente.
T2 - Tiempo de respuesta/objetivos de rendimiento: ¿Cuál es la importancia del tiempo de respuesta de la aplicación para sus usuarios?
0. El cliente no definió ningún requisito especial de rendimiento.
1. Se establecieron y revisaron los requisitos de desempeño, pero no se debe tomar ninguna medida especial.
2. El tiempo de respuesta y las tasas de transferencia son críticas durante las horas pico. No es necesario ningún diseño especial para el uso del núcleo del procesador. La fecha límite para la mayoría de los procesos es al día siguiente.
3. El tiempo de respuesta y las tasas de transferencia son críticas durante las horas comerciales. No es necesario ningún diseño especial para el uso del núcleo del procesador. Los requisitos relativos a los plazos para la comunicación con los sistemas interconectados son restrictivos.
4. Además de 3, los requisitos de rendimiento son suficientemente restrictivos para requerir tareas de análisis de rendimiento durante el diseño.
5. Además de 4, se deben utilizar herramientas de análisis de rendimiento durante el diseño, desarrollo y/o implementación, con el fin de cumplir con los requisitos de rendimiento del cliente.
T3 - Eficiencia del usuario final: ¿La aplicación está diseñada para que los usuarios finales puedan hacer su trabajo o para mejorar su eficiencia?
0. La solicitud no necesita ninguno de los siguientes elementos.
1. La aplicación necesita de uno a tres de los siguientes elementos.
2. La aplicación necesita de cuatro a cinco de los siguientes elementos.
3. La aplicación necesita seis o más de los siguientes elementos, pero no hay ningún requisito relacionado con la eficiencia del usuario.
4. La aplicación necesita seis o más de los siguientes elementos, y los requisitos de eficiencia del usuario son tan estrictos que el diseño debe incluir características para minimizar la escritura, maximizar los valores predeterminados, utilizar plantillas, etc.
5. La aplicación necesita seis o más de los siguientes elementos, y los requisitos de eficiencia del usuario son tan estrictos que las actividades de diseño deben incluir herramientas y procesos especiales para demostrar que se han alcanzado los objetivos de rendimiento.
Para la evaluación de la eficiencia del usuario final deben tenerse en cuenta los siguientes aspectos:9
    • Ayuda a la navegación (por ejemplo, menús generados dinámicamente, hipermedios adaptables, etc.).
    • Ayuda y documentación en línea.
    • Movimiento automático del cursor.
    • Teclas de función predefinidas.
    • Tareas por lotes enviadas desde transacciones en línea.
    • Alto uso de colores y efectos visuales en las pantallas.
    • Minimizar el número de pantallas para alcanzar los objetivos de negocio.
    • Soporte bilingüe (cuenta como cuatro ítems).
    • Soporte multilingüe (cuenta con seis elementos).
T4 - Complejidad del procesamiento interno: ¿Necesita la aplicación algoritmos complejos?
0. Ninguna de las siguientes opciones.
1. Una de las opciones a continuación.
2. Dos de las opciones a continuación.
3. Tres de las siguientes opciones.
4. Cuatro de las opciones a continuación.
5. Las cinco opciones a continuación.
Las siguientes opciones deben ser consideradas para evaluar la complejidad del procesamiento interno:
    • Control cuidadoso (por ejemplo, procesamiento especial de auditoría) y/o procesamiento seguro específico de la aplicación.
    • Procesamiento lógico extensivo.
    • Amplio procesamiento matemático.
    • Mucho procesamiento de excepciones como resultado de transacciones incompletas que necesitan ser reprocesadas, tales como transacciones de cajeros automáticos incompletas causadas por la interrupción de la comunicación, valores de datos faltantes o cambios de datos fallidos.
    • Procesamiento complejo para gestionar múltiples posibilidades de entrada y salida, como la independencia de dispositivos o multimedia.

T5 - Diseño orientado a la reutilización de código: ¿Está la aplicación diseñada para que su código y sus artefactos sean altamente reutilizables?
0. No hay ninguna preocupación sobre la producción de código reutilizable.
1. El código reutilizable se genera para su uso dentro del mismo proyecto.
2. Menos del 10% de la aplicación debe considerar más de lo que el usuario necesita.
3. El 10% o más de la aplicación debe considerar más de lo que el usuario necesita.
4. La aplicación debe estar específicamente empaquetada y/o documentada para facilitar su reutilización, y la aplicación debe ser personalizable por el usuario a nivel de código fuente.
5. La aplicación debe estar específicamente empaquetada y/o documentada para facilitar la reutilización, y la aplicación debe ser personalizable por el usuario con el uso de parámetros.
T6 - Fácil de instalar: ¿La aplicación se diseñará de forma que su instalación sea automática (por ejemplo, en el caso de usuarios con una capacidad técnica baja o desconocida), o no existe una preocupación especial al respecto?
0. El cliente no estableció ninguna consideración especial, y no se necesita ninguna configuración especial para la instalación.
1. El cliente no estableció ninguna consideración especial, pero se requiere una configuración especial para la instalación.
2. Los requisitos establecidos por el cliente para la conversión de datos y la instalación, y las guías de conversión e instalación deben ser proporcionadas y probadas. El impacto de la conversión en el proyecto no se considera importante.
3. Los requisitos establecidos por el cliente para la conversión de datos y la instalación, y las guías de conversión e instalación deben ser proporcionadas y probadas. El impacto de la conversión en el proyecto es considerable.
4. Además de 2, se deben proporcionar y probar herramientas para la conversión e instalación automáticas.
5. Además de 3, se deben proporcionar y probar herramientas para la conversión e instalación automáticas.
T7 - Fácil de manejar:10 ¿Existen requisitos especiales para el funcionamiento del sistema?
0. El usuario no estableció ninguna consideración especial sobre el funcionamiento del sistema aparte de los procedimientos normales de copia de seguridad.
1. Una de las siguientes posiciones es válida para el sistema.
2. Dos de las siguientes posiciones son válidas para el sistema.
3. Tres de los siguientes puntos se aplican al sistema.
4. Cuatro de los siguientes puntos se aplican al sistema.
5. La aplicación está diseñada para operar de manera no supervisada. "No supervisado" significa que la intervención humana no es necesaria para mantener el sistema operativo, incluso si se producen fallos, excepto quizás para la primera puesta en marcha y el último apagado. Una de las características de la aplicación es la recuperación automática de errores.
Para la evaluación del factor de facilidad de uso, se deben tener en cuenta los siguientes puntos:
    • Se deben proporcionar procesos efectivos para la inicialización, copia de seguridad y recuperación, pero la intervención del operador sigue siendo necesaria.
    • Se deben proporcionar procesos efectivos para la inicialización, copia de seguridad y recuperación, y no es necesaria la intervención del operador (cuenta como dos elementos).
    • La aplicación debe minimizar la necesidad de almacenar datos en medios fuera de línea (por ejemplo, cintas).
    • La solicitud debe minimizar la necesidad de tratar con papel.
T8 - Portabilidad: ¿Está la aplicación o partes de ella diseñada para funcionar en más de una plataforma?
0. No es necesario que el usuario considere la necesidad de instalar la aplicación en más de una plataforma.
1. El diseño debe tener en cuenta la necesidad de que el sistema funcione en diferentes plataformas, pero la aplicación debe estar diseñada para funcionar sólo en entornos de hardware y software idénticos.
2. El diseño debe tener en cuenta la necesidad de que el sistema funcione en diferentes plataformas, pero la aplicación debe estar diseñada para funcionar sólo en entornos de hardware y software similares.
3. El diseño debe tener en cuenta la necesidad de que el sistema funcione en diferentes plataformas, pero la aplicación debe estar diseñada para funcionar en entornos heterogéneos de hardware y software.
4. Además de 1 ó 2, se debe elaborar y probar un plan de documentación y mantenimiento para soportar la operación en múltiples plataformas.
5. Además de 3, se debe elaborar y probar un plan de documentación y mantenimiento para apoyar la operación en múltiples plataformas.
T9 - Diseño con el objetivo de facilitar el mantenimiento: ¿El cliente requiere que la aplicación sea fácil de cambiar en el futuro?
0. Ninguno de los puntos a continuación.
1. Uno de los puntos a continuación.
2. Dos de los puntos a continuación.
3. Tres de los puntos siguientes.
4. Cuatro de los puntos a continuación.
5. Cinco o más de los siguientes puntos.
Para evaluar este factor, se consideran los siguientes puntos:
    • Se debe proporcionar una estructura de informe flexible para tratar consultas simples como los operadores binarios lógicos aplicados a un único archivo lógico (contar como un solo elemento).
    • Se debe proporcionar una estructura de informe flexible para tratar consultas de complejidad media, como los operadores binarios lógicos aplicados a más de un archivo lógico (contar como dos elementos).
    • Se debe proporcionar una estructura de informe flexible para tratar consultas de alta complejidad, como combinaciones de operadores binarios lógicos aplicados a uno o más archivos lógicos (contar como tres elementos).
    • Los datos de control de la empresa se guardan en tablas gestionadas por el usuario con acceso interactivo en línea, pero las modificaciones sólo deben ser efectivas al día siguiente (contar como un elemento).
    • Los datos de control del negocio se mantienen en tablas gestionadas por el usuario con acceso interactivo en línea, y los cambios son efectivos inmediatamente (cuentan como dos ítems).
T10 - Tratamiento simultáneo/paralelo: ¿Debe diseñarse la aplicación para tratar problemas relacionados con la concurrencia, como, por ejemplo, el intercambio de datos y recursos?
0. No se espera un acceso simultáneo a los datos.
1. A veces se espera un acceso simultáneo a los datos.
2. Se espera un acceso simultáneo a los datos con frecuencia.
3. Se espera un acceso simultáneo a los datos en todo momento.
4. Además de 3, el usuario indica que se van a producir muchos accesos múltiples, lo que obliga a realizar tareas de análisis de rendimiento y resolución de bloqueos durante el diseño.
5. Además de 4, el diseño requiere el uso de herramientas especiales para controlar el acceso.
T11 - Seguridad: ¿Son las necesidades de seguridad sólo nominales o se requiere un diseño especial y especificaciones adicionales?
0. No hay requisitos especiales de seguridad.
1. La necesidad de seguridad debe tenerse en cuenta en el diseño.
2. Además de 1, la aplicación debe estar diseñada para que sólo puedan acceder a ella los usuarios autorizados.
3. Además de 2, el acceso al sistema será controlado y auditado.
4. Además de 3, se debe elaborar y probar un plan de seguridad para soportar el control de acceso a la aplicación.
5. Además de 4, se debe elaborar y probar un plan de seguridad para apoyar a los audífonos.
T12 - Acceso para/con código de terceros: ¿Va a utilizar la aplicación código ya desarrollado, como componentes, frameworks o librerías comerciales disponibles en el mercado (COTS)? La alta reutilización de software de buena calidad reduce el valor de este elemento, ya que implica un menor esfuerzo de desarrollo.
0. El código preexistente altamente fiable se utilizará ampliamente para el desarrollo de la aplicación.
1. El código preexistente altamente fiable se utilizará en pequeñas partes de la aplicación.
2. El código preexistente que eventualmente necesite ser ajustado será utilizado ampliamente para el desarrollo de la aplicación.
3. El código preexistente que eventualmente necesite ser ajustado será utilizado en pequeñas partes de la aplicación.
4. El código preexistente que necesita ser corregido o que es difícil de entender será utilizado en la aplicación.
5. No se utilizará ningún código preexistente en la aplicación o se utilizará un código de calidad cuestionable en la aplicación.
T13 - Necesidades de formación de los usuarios: ¿Será fácil de usar la aplicación, o se debe dar una amplia formación a los futuros usuarios?
0. No existen requisitos específicos para la formación de los usuarios.
1. Se han mencionado los requisitos específicos de formación de los usuarios.
2. Existen requisitos formales de formación específicos para los usuarios, y la aplicación debe estar diseñada para facilitar la formación.
3. Existen requisitos formales de formación específicos para los usuarios, y la aplicación debe estar diseñada para apoyar a los usuarios con diferentes niveles de formación.
4. Debe elaborarse un plan de formación detallado para la fase de transición y ejecutarse.
5. Además de 4, los usuarios están distribuidos geográficamente.
Aplicando los factores técnicos al ejemplo actual, se puede obtener un resultado similar al presentado en la Tabla 4.4.





Tabla 4.4
Evaluación de los Factores Técnicos del Livir

Código
Factor
Peso
Ratio
Peso x Ratio
Justificación (del ratio)
T1
Sistema distribuido
2
0
0
La aplicación ignora aspectos relacionados con los procesos distribuidos
T2
Tiempo de respuesta/objetivos de rendimiento
1
2
2
El tiempo de respuesta y los ratios de transferencia son críticos durante las horas pico. No se necesita ningún diseño especial para el uso de los núcleos del procesador. El plazo para la mayoría de los procesos finaliza el siguiente día.
T3
Eficiencia del usuario final
1
3
3
La aplicación necesita los siguientes aspectos, pero no son requisitos especiales relacionados con la eficiencia del usuario:
    • Ayuda navigacional (por ejemplo menús contextuales generados dinámicamente, hipermedia adaptable, etc.)
    • Ayuda Online y Documentación.
    • Uso del color alto y resaltes de visualización en las pantallas.
    • Minimizar el uso de pantallas para alcanzar los objetivos.
    • Soporte multiidioma (cuenta como siete elementos)
T4
Complejidad del tratamiento interno
1
0
0
 No se aplica ninguna de las opciones
T5
Diseño orientado a la reutilización de código
1
0
0
 Nada concierne a  la reutilización de código.
T6
Fácil de instalar
0.5
0
0
 Ninguna consideración ha sido establecida por el cliente y no se necesita establecer nada especial en la instalación.
T7
Fácil de operar
0.5
5
2.5
 La aplicación está diseñada para funcionar en modo sin supervisión. “Sin supervisión”, significa que no se necesita intervención humana para que el sistema se mantenga en estado operativo, incluso si ocurre una rotura, excepto quizás para el primer arranque y último apagado. Una de las característica de la aplicación es la recuperación automática ante errores.
T8
Portabilidad
2
3
6
El diseño debe considerar  la necesidad del sistema de operar en diferentes plataformas, pero la aplicación cliente debe ser diseñada para operar en entornos heterogéneos de hardware y software. 
T9
Diseño con el objetivo de facilitar el mantenimiento
1
0
0
 No se aplica ninguno de los elementos.
T10
Tratamiento concurrente/paralelo
1
1
1
 Ocasionalmente se esperar accesos a los datos concurrentemente.
T11
Seguridad
1
3
3
 La necesidad de seguridad debe ser tenida encuenta en el diseño. La aplicación debe ser diseñada de tal manera que sólo pueda ser accededa por los usuarios autorizados.
T12
Acceso para/con código de terceros
1
5
5
Ningun código preexistente será utilizado en la aplicación.
T13
Necesidades de formación de los usuarios
1
0
0
No existen requisitos especiales para el entrenamiento de usuarios.
TFactor



22.5


El valor de los factores técnicos, TCF, para el ejemplo se obtiene por:

TCF =  0.6 + (0.01 *22.5)  = 0.825

Como ese valor es inferior a 1, los factores técnicos de este proyecto indican un tiempo de desarrollo inferior al nominal (82,5% del nominal). Sin embargo, aún no se han determinado los factores medioambientales.

                ​ 4.2.5 Factores del entorno - EF – environmental factors
Un aspecto que distingue el análisis de puntos de caso de uso del análisis de puntos de función es que el análisis de puntos de uso utiliza un factor de ajuste para las características del equipo de desarrollo. Por lo tanto, el mismo proyecto, con los mismos factores técnicos, puede tener un número diferente de puntos de caso de uso ajustados para diferentes equipos.
Existen ocho factores de entorno que evalúan el ambiente de trabajo. Cada uno tiene su propio peso y dos de ellos tienen pesos negativos. Una vez más, las calificaciones van de 0 a 5, pero su significado es un poco diferente de las calificaciones atribuidas a los factores técnicos. Mientras que las calificaciones de los factores técnicos evalúan la influencia de esos factores en el proyecto, las calificaciones de los factores de entorno evalúan la calidad de esos factores en el ambiente de trabajo. Por ejemplo, una calificación 0 para el factor "motivación" significa que el equipo no está motivado, una calificación 3 significa que la motivación es media, y una calificación 5 significa que el equipo está muy motivado.
Los factores ambientales se definen en la Tabla 4.5.


Tabla 4.5
Factores ambientales para ajustar los puntos de caso de uso


Código
Factor
Peso
E1
Familiaridad con el proceso de desarrollo
1.5
E2
Experiencia en la aplicación
0.5
E3
Experiencia orientada a objetos
1
E4
Experiencia como analista líder
0.5
E5
Motivación
1
E6
Requisitos de estabilidad
2
E7
Trabajadores a tiempo parcial
−1
E8
Dificultad con el lenguaje de programación
−1

Así, las calificaciones multiplicadas por el peso de los factores ambientales pueden oscilar entre -10 y 32,5. Este valor se denomina EFactor.
El EFactor se ajusta al intervalo de 0,425 a 1,7, generando el EF (factor de entorno) mediante la siguiente fórmula:

EF = 1.4 – (0.03 * EFactor)

Ribu (2001) presenta una referencia para asignar valoración a los factores de entorno, que se describe a continuación con algunas adaptaciones.

E1 - Familiaridad con el proceso de desarrollo: Este factor evalúa la experiencia del equipo con el proceso de desarrollo que está utilizando. Originalmente el factor mencionaba el Proceso Unificado, y algunos autores incluso mencionan UML aquí. Pero esto ha sido ajustado para reflejar el hecho de que otros procesos y lenguajes de modelado podrían ser usados en su lugar.
0. El equipo no tiene experiencia con el proceso de desarrollo o no utiliza ningún proceso.
1. El equipo tiene conocimientos teóricos sobre el proceso de desarrollo, pero no experiencia.
2. Algunos miembros del equipo ya han utilizado el proceso en un proyecto.
3. Algunos miembros del equipo han utilizado el proceso en más de un proyecto.
4. Hasta la mitad del equipo ha utilizado el proceso en muchos proyectos.
5. Más de la mitad del equipo ha utilizado el proceso en muchos proyectos.
E2 - Experiencia en la aplicación: Este factor evalúa la familiaridad del equipo con el área de aplicación o dominio. Por ejemplo, si la aplicación es sobre comercio electrónico, ¿el equipo ya ha trabajado con sistemas en la misma área?
0. Ningún miembro del equipo tiene experiencia en proyectos en la misma área.
1. Algunos miembros del equipo tienen de 6 a 12 meses de experiencia en proyectos en la misma área.
2. Algunos miembros del equipo tienen de 12 a 18 meses de experiencia en proyectos en la misma área.
3. La mayoría de los miembros del equipo tienen de 18 a 24 meses de experiencia en proyectos en la misma área.
4. La mayoría de los miembros del equipo tienen más de dos años de experiencia en la misma área.
5. Todos los miembros del equipo tienen más de dos años de experiencia en la misma área.
E3 - Experiencia orientada a objetos: Este factor no debe confundirse con la familiaridad con el proceso de desarrollo (E1) ni con la experiencia en la aplicación (E2): se trata de la experiencia del equipo en la realización de análisis, modelado, diseño y programación orientados a objetos, independientemente del área de aplicación y del proceso de desarrollo utilizado.
0. El equipo no tiene experiencia en técnicas orientadas a objetos.
1. Todos los miembros del equipo tienen alguna experiencia en técnicas orientadas a objetos (hasta un año).
2. La mayoría de los miembros del equipo tienen de 12 a 18 meses de experiencia en técnicas orientadas a objetos.
3. Todos los miembros del equipo tienen de 12 a 18 meses de experiencia, o la mayoría de los miembros del equipo tienen de 18 a 24 meses de experiencia en técnicas orientadas a objetos.
4. La mayoría de los miembros del equipo tienen más de dos años de experiencia en técnicas orientadas a objetos.
5. Todos los miembros del equipo tienen más de dos años de experiencia en técnicas orientadas a objetos.
E4 - Experiencia como analista líder: Este factor mide la experiencia del analista líder con el análisis de requerimientos y el modelado orientado a objetos.
0. El analista principal no tiene experiencia.
1. El analista líder tiene experiencia previa en un solo proyecto similar.
2. El analista líder tiene alrededor de un año de experiencia en más de un proyecto similar.
3. El analista líder tiene alrededor de dos años de experiencia en proyectos similares.
4. El analista líder tiene más de dos años de experiencia en proyectos similares.
5. El analista líder tiene más de tres años de experiencia en una variedad de proyectos.
E5 - Motivación: Este factor describe la motivación del equipo.11
0. El equipo no tiene ninguna motivación. Sin una supervisión constante, el equipo se vuelve improductivo. El equipo sólo hace lo que se le pide estrictamente.
1. El equipo tiene muy poca motivación. Es necesaria una supervisión constante para mantener la productividad a niveles aceptables.
2. El equipo tiene poca motivación. Las intervenciones de manejo son necesarias de vez en cuando para mantener la productividad.
3. El equipo tiene algo de motivación. Por lo general, el equipo tiene iniciativa, pero la intervención de la dirección sigue siendo necesaria esporádicamente para mantener la productividad.
4. El equipo está bien motivado. El equipo suele ser autogestionado, pero la existencia de supervisión sigue siendo necesaria porque la productividad puede perderse sin ella.
5. El equipo está muy motivado. Incluso sin supervisión, todo el mundo sabe lo que hay que hacer, y el ritmo se mantiene indefinidamente.
E6 – Estabilidad de Requisitos: Este factor evalúa si el equipo ha sido capaz de mantener estables los requerimientos en proyectos anteriores, minimizando su cambio durante el proyecto. Este factor puede variar de un proyecto a otro, porque hay ámbitos en los que las necesidades cambian a menudo independientemente de la capacidad de los analistas. Este factor debe evaluar sólo los cambios de software que fueron causados por la incapacidad del equipo para descubrir los requisitos correctos.
0. No hay datos históricos sobre la estabilidad de los requisitos o, en el pasado, un análisis deficiente desembocó en grandes cambios en los requisitos después del inicio del proyecto.
1. Anteriormente, las necesidades fueron predominantemente inestables. Los clientes pidieron muchos cambios, originados principalmente por requisitos incompletos o incorrectos.
2. Anteriormente, las necesidades fueron inestables. Los clientes solicitaron algunos cambios causados por requisitos incompletos o incorrectos.
3. Las necesidades se mantuvieron relativamente estables anteriormente. Los clientes solicitaron cambios en las funcionalidades secundarias con cierta regularidad. Rara vez se pedían cambios en las funcionalidades principales.
4. Las necesidades anteriormente se mantuvieron estables en su mayor parte. Los usuarios pedían pequeños cambios, sobre todo cosméticos. Los cambios en las funcionalidades principales o secundarias fueron inusuales.
5. Las necesidades anteriormente fueron totalmente estables. Los pequeños cambios, si los hubiere, no tuvieron ningún impacto en los proyectos.
E7 - Trabajadores a tiempo parcial: Se trata de un factor negativo, es decir, a diferencia de los seis primeros factores medioambientales, los valores más altos aquí representan más tiempo de desarrollo, no menos. Un equipo con muchos miembros involucrados en otros proyectos o actividades es menos productivo que un equipo dedicado.
0. Ningún miembro del equipo trabaja a tiempo parcial en el proyecto.
1. Hasta un 10% del equipo es a tiempo parcial.
2. Hasta un 20% del equipo es a tiempo parcial.
3. Hasta el 40% del equipo es a tiempo parcial.
4. Hasta el 60% del equipo es a tiempo parcial.
5. Más del 60% del equipo trabaja a tiempo parcial.
E8 - Dificultad con el lenguaje de programación: Este es otro factor negativo, lo que significa que los valores altos aquí son malos para el tiempo de desarrollo.
0. Todos los miembros del equipo son programadores muy experimentados.
1. La mayoría de los miembros del equipo tienen al menos dos años de experiencia en programación.
2. Todos los miembros del equipo tienen al menos 18 meses de experiencia en programación.
3. La mayoría de los miembros del equipo tienen al menos 18 meses de experiencia en programación.
4. Algunos miembros del equipo tienen alguna experiencia en programación (no más de un año).
5. Todos los miembros del equipo son programadores sin experiencia.
Para continuar con el ejemplo de Livir, supongamos que la empresa está formada por un grupo de cinco profesionales que recientemente obtuvieron títulos de Ciencias de la Computación y estudiaron técnicas orientadas a objetos, pero que no tienen una experiencia profesional significativa. Tres de ellos están totalmente dedicados al proyecto, mientras que los otros dos tienen otras actividades. Livir será el primer proyecto que van a realizar profesionalmente juntos. Con esta empresa ficticia, la evaluación de los factores ambientales podría ser algo así como la Tabla 4.6.





Tabla 4.6
Evaluación de los factores de entorno, para el equipo ficticio del proyecto Livir

Código
Factor
Peso
Ratio
P x R
Justificación
E1
Familiaridad con el proceso de desarrollo
1.5
1
1.5
El equipo tiene los conocimientos teóricos sobre el sistema de desarrollo pero no tiene experiencia profesional.
E2
Experiencia en la aplicación
0.5
0
0
Ningún miembro tiene experiencia previa en proyectos similares
E3
Experiencia orientada a objetos
1
3
3
Todos los miembroscdrl equipo tienen entre 12 y 18 meses de experiencia (académica) con técnicas OO.
E4
Experiencia como analista líder
0.5
0
0
El analista líder no tiene experiencia
E5
Motivación
1
5
5
El equipo está altamente motivado. Incluso sin supervisión, cada miembro conoce su trabajo y mantiene su paz indefinidamente.
E6
Requisitos de estabilidad
2
0
0
No hay histórico confiable para el equipo.
E7
Trabajadores a tiempo parcial
−1
3
-3
El 40% del equipo trabaja a tiempo parcial.
E8
Dificultad con el lenguaje de programación
−1
5
-5
Aunque poseen experiencia académica, se trata de programadores novatos.
EFactor



1.5


Aplicando la fórmula de ajuste a los factores ambientales de la empresa se obtiene lo siguiente:

EF = 1.4 – (0.03 * 1.5) = 1.355

Esto indica que los factores ambientales son malos para este equipo de principiantes, y que su esfuerzo será alrededor de un 35% mayor que el nominal.

                ​ 4.2.6 Puntos de caso de uso ajustados - UCP – adjusted use case points
Una vez calculados los pesos de los casos de los actores y de los usos, así como los factores técnicos y ambientales, los puntos de los casos de uso ajustados pueden obtenerse mediante una simple multiplicación:

UCP = UUCP * TCF * EF

Para el ejemplo en ejecución que obtenemos:

UCP = 234 * 0.825 * 1.355 = 261.583

                ​ 4.2.7 Esfuerzo
El objetivo clave de todas las técnicas de estimación es predecir el esfuerzo necesario para desarrollar un proyecto. En primer lugar, es necesario definir la extensión del esfuerzo que se está estimando. El método COCOMO II, por ejemplo, cuando se aplica con el Proceso Unificado, estima el esfuerzo que se gastará durante la Elaboración y Construcción solamente.
Además de esto, ¿incluye el esfuerzo actividades administrativas, ventas, etc.? ¿O incluye sólo el esfuerzo invertido en actividades de ingeniería de software? La literatura sobre puntos de casos de uso generalmente no es tan detallada como COCOMO II y el análisis de puntos de función con respecto al tipo de esfuerzo que se está estimando. Como el análisis de puntos de casos de  uso se basa en el análisis de puntos de función Mk II (UKSMA Metrics Practices Committee, 1998), podemos asumir que por defecto se aplican las mismas definiciones, como "El esfuerzo del proyecto debe incluir personal que esté claramente asignado al proyecto y que trabaje de acuerdo con los requisitos del proyecto". Por ejemplo, no se incluiría el tiempo de un usuario entrevistado, mientras que sí se incluiría el tiempo de un usuario asignado al equipo del proyecto durante una cantidad significativa de tiempo". Del mismo modo, también puede aplicarse la siguiente definición: El esfuerzo de trabajo debe medirse en unidades de horas de trabajo `productivas' o `netas', que se definen como....": Una hora de trabajo de una persona, incluidas las pausas personales normales, pero excluidas las pausas importantes, como las de la comida". Mk II también establece que un proyecto comienza cuando "se ha acordado y aprobado que se debe trabajar para entregar una solución IS12 [...] uno o más empleados han sido asignados al proyecto y empiezan a trabajar en él" (esto ocurre durante la fase de inicio), y que un proyecto finaliza cuando "la aplicación cobra "vida" al trasladarla al entorno de producción por primera vez, y los usuarios hacen uso de ella" (esto ocurre durante la fase de transición).
El esfuerzo que se calcula normalmente debe incluir todos los riesgos y situaciones inesperadas. Sin embargo, la estimación no es una ciencia precisa. En algunas situaciones las cosas pueden salirse de control y los ajustes deben hacerse sobre la marcha para mantener el proyecto en los rieles. Podemos decir que el calendario final definiría el tiempo máximo tolerable para la entrega de un producto con el alcance mínimo aceptable. Es decir, si tenemos suerte y los riesgos causan pocos problemas, podemos entregar el producto antes o entregar un producto mejor de lo esperado.
Una vez calculado el número de puntos de casos de uso, éstos deben transformarse en una medida de esfuerzo utilizando un índice de productividad del equipo (TPI). Si el TPI se mide como el tiempo que un miembro del equipo pasó en un solo caso de uso13, entonces el esfuerzo puede ser dado por:

E = UCP * TPI

Como UCP es un valor independiente de la escala, se debe decidir en qué escala se medirá el esfuerzo. La literatura de puntos de uso generalmente se refiere a las horas de trabajo del personal por punto de caso de uso. Sin embargo, otros métodos como COCOMO II (Boehm, 2000) prefieren los meses de personal.
Debido a que la mayoría de las fórmulas que se aplican habitualmente a la productividad en la industria del software se define en términos de meses de personal, y debido a que la unidad elegida puede afectar a los resultados, este libro adopta los meses de personal como la unidad de productividad, pero se refiere a las horas de trabajo del personal cuando es necesario.
Si se considera que un mes corresponde a una media de 158 horas de trabajo (sin tener en cuenta los días festivos ni los fines de semana), entonces x horas de trabajo por punto de caso de uso corresponden a x/158 meses de trabajo por punto de caso de uso.
Originalmente, Karner (1993) estimó que 20 horas de trabajo (aproximadamente 0,127 meses de trabajo) por caso de uso14 sería una buena suposición cuando se carece de un historial fiable. Posteriormente, Ribu (2001) determinó que ese valor podía oscilar entre 15 y 30 horas de trabajo (0,095 a 0,190 meses de trabajo) por caso de uso.
El valor del TPI también se puede estimar tomando proyectos anteriores, buscando el tiempo total del personal empleado y dividiéndolo por el número de puntos de casos de uso. Así, por ejemplo, si el esfuerzo total dedicado a un proyecto determinado fue de 9 meses de personal y el total de UCP del proyecto fue de 60, entonces el índice de productividad del equipo en ese caso es de 9/60, es decir, 0,15 meses de personal por punto de uso.
Otros trabajos (Schneider & Winters, 1998) proponen que el número de factores de entorno E1 a E6 clasificados por debajo de 3 se sume al número de factores ambientales E7 y E8 clasificados por encima de 3, y:
    • Si el resultado es 2 o menos, asumimos 20 horas de trabajo (0,127 meses de trabajo) por punto de caso de uso.
    • Si el resultado es 3 ó 4, asumimos 28 horas de trabajo (0,177 meses de trabajo) por punto de caso de uso.
    • Si el resultado es superior a 4, los factores de entorno presentan un riesgo demasiado alto para el proyecto y deben ser mejorados antes de asumir cualquier compromiso de desarrollo, o bien, asumir 36 horas de trabajo (0,228 meses de trabajo) por punto de uso.
En el ejemplo actual hay cinco factores ambientales negativos: E1, E2, E4, E6 y E8. La recomendación, en este caso, sería tratar de mejorar la calidad del entorno antes de desarrollar cualquier proyecto. Sin embargo, si el equipo decide asumir el riesgo, el proyecto debe asumir la peor estimación de 0,228 meses de personal por punto de caso de uso. Así pues, el esfuerzo total del proyecto Livir es de 261.583*0.228=59.64 meses de personal.

                ​ 4.2.8 Agenda y tamaño medio del equipo
El valor de esfuerzo obtenido para el ejemplo de la última sección (59,64 meses de personal) se refiere al esfuerzo total para desarrollar el proyecto desde su inicio hasta la entrega del producto. Sin embargo, más de un miembro del personal trabajará en el proyecto y, por lo tanto, el tiempo del calendario (tiempo lineal sin tener en cuenta los fines de semana y los días festivos) probablemente será mucho menor.
Existe una sencilla regla empírica que permite aproximar el tiempo de calendario ideal para un proyecto a partir de su esfuerzo total (McConnel, 1996). La fórmula es:

Bbbbnn


En esta fórmula, T es el tiempo de calendario ideal para desarrollar el proyecto.
Esta fórmula sólo funciona si E se expresa en meses de personal. El uso de otras unidades, como las semanas o las horas de trabajo del personal, causaría distorsiones en el resultado debido al uso de la raíz cúbica.
Existen otras fórmulas basadas en puntos de función (Jones, 2007) o líneas de código (Boehm, 2000). Pero, para poder ser aplicado con puntos de casos de uso, se necesitan algunas conversiones. Si se desea una aproximación más precisa, tal vez valga la pena el esfuerzo porque las fórmulas de Boehm y Jones utilizan información sobre la complejidad del proyecto y la capacidad del equipo como parámetros para producir el calendario temporal estimado.
Aplicando la regla de la fórmula general anterior al ejemplo actual produce:

El tamaño medio del equipo (P) se calcula por:
P = E/T
Para el ejemplo en ejecución, obtenemos:
P = 59.64/9.768 = 6.106
Por lo tanto, el tamaño promedio del equipo, en ese caso, debe ser aproximadamente igual a seis. En resumen, el proyecto sería idealmente desarrollado por seis personas en unos 10 meses. Para este ejemplo, la empresa desarrolladora podría optar por contratar a un nuevo profesional (especialmente a un profesional con más experiencia que podría ayudar a mejorar las clasificaciones de los factores ambientales); tratar de desarrollar el proyecto con cinco personas podría llevar más tiempo del ideal. Para este ejemplo, es posible calcular el tiempo que un equipo de cinco personas tardaría en desarrollar el proyecto como 59.64/5=11.928. En ese caso, el proyecto sería completado por cinco personas en unos 12 meses. Dijimos "es posible" porque el número de personas consideradas es menor que el tamaño recomendado para el equipo. Sin embargo, sería poco realista aplicar esta división para calcular el tiempo de calendario para un equipo más grande que el ideal. Por ejemplo, no sería realista asumir que 20 personas podrían completar el proyecto en 59,64/20=2,982 meses. Cualquier tamaño de equipo superior al ideal significa que el esfuerzo total (E) debe ajustarse a un valor superior. El multiplicador de esfuerzo SCED (Required Development Schedule) de COCOMO II indica que ejecutar un proyecto en un tiempo que es el 85% del tiempo ideal implica sumar el 14% del esfuerzo total, y ejecutar un proyecto en un tiempo que es el 75% del tiempo ideal implica sumar el 43% del esfuerzo total (Boehm, 2000).
Puede parecer que esos tiempos son demasiado altos para el proyecto presentado en el ejemplo. Sin embargo, hay que tener en cuenta que los factores de entorno son muy malos, ya que el equipo tiene muy poca experiencia. Cometerán errores y posiblemente tendrán que rehacer mucho trabajo. Lo más importante es que la falta de experiencia puede llevar al equipo a malinterpretar los requisitos y tener que solucionarlos más tarde, lo que aumenta significativamente el tiempo de desarrollo.
Si en lugar de esos novatos tuviéramos un equipo de ensueño con los mejores ratios posibles de factores ambientales, entonces EF sería 0.425 (el mejor valor posible). En ese caso, UCP=234*0.825*0.425=82.046. Utilizando la recomendación de Schneider y Winters (1998), se puede suponer que el equipo de ensueño podría trabajar a razón de 20 horas de trabajo o 0,127 meses de trabajo por caso de uso. Así, E=82.046*0.127=10.42. Aplicando la fórmula para el tiempo de calendario y el tamaño promedio del equipo, el resultado es T=5.46 y P=1.908. Es decir, un equipo de ensueño de dos personas podría completar el proyecto en unos cinco meses y medio. Parece una estimación muy razonable teniendo en cuenta el tamaño del proyecto y la capacidad del equipo.
Sin embargo, es importante mencionar que esas fórmulas son algo "mágicas" porque hay una gran variedad de proyectos y equipos de desarrollo. Antes de utilizarlos seriamente en una empresa, siempre es útil probarlos y ajustarlos a la realidad local.

                ​ 4.2.9 Métodos de recuento para casos de uso detallados
La técnica de análisis de puntos de caso de uso presentada en las subsecciones anteriores se considera sólo una conjetura sobre la complejidad de los casos de uso, ya que se trata de casos de uso de alto nivel, que se representan sólo por su nombre y, eventualmente, una o dos frases explicativas.
Existen técnicas para contar los puntos de uso con casos de uso expandido (explicados en el Capítulo 5), pero su utilidad es más limitada porque, con el Proceso Unificado, los casos de uso generalmente sólo se detallan durante las iteraciones. Durante el inicio, el equipo suele tener sólo casos de uso de alto nivel.
Aún así, estas técnicas pueden ser útiles si los casos de uso ya están detallados, o si la estimación del esfuerzo debe ser refinada cuando se inicia una iteración. Es por eso que estas técnicas se resumen en esta sección.
Robiolo y Orosco (2008) sugieren que se debe analizar el texto del caso de uso detallado y contar las entidades (clases) y las transacciones (pasos). El tamaño de una aplicación en puntos de caso de uso no ajustados sería la suma de esos valores.
Braz y Vergilio (2006) proponen una técnica denominada FUSP (Fuzzy Use Case Size Points), en la que el recuento se basa en la complejidad de los:
    • Actores que participan en el caso de uso.
    • Usar las condiciones previas y posteriores de los casos.
    • Número de entidades necesarias para el caso de uso.
    • Número de transacciones del caso de uso.
    • Complejidad de los flujos alternativos del caso de uso.
Por lo tanto, la medida es bastante detallada, pero se necesita mucho trabajo para aplicarla y los casos de uso deben ser ampliados para que funcione.
Mohagheghi, Anda y Conradi (2005) proponen una técnica (Adapted Use Case Points) que asume que cada actor tiene una complejidad media, y que cada caso de uso es complejo al principio. Posteriormente, los casos de uso deben dividirse en casos de uso más pequeños y reclasificarse como simples o medianos a medida que avanza el proceso de refinación. También se cuentan los casos de uso extendido y los flujos alternativos.
Kamal y Ahmed (2011) presentan una amplia comparación entre los métodos de recuento mencionados y otros.
Se propuso el método de Tamaño de Caso de Uso Completo (Ibarra & Vilain, 2010) con el objetivo de medir el tamaño de los casos de uso. El método mide aspectos funcionales y no funcionales y, para ello, necesita casos de uso de alto nivel y una lista de requisitos no funcionales anotados para cada caso de uso. La medición se basa en tres componentes:
    • El tipo de caso de uso.
    • El número de operaciones del sistema (transacciones) y reglas de negocio.
    • El número de requisitos de la interfaz.
Los detalles sobre estas técnicas pueden encontrarse en las obras originales citadas anteriormente.

            ​ 4.3 Planificación de un proyecto iterativo
El objetivo de la planificación del proyecto es construir un plan para el proyecto en su conjunto. Entre otras cosas, es importante que la persona o grupo responsable de la planificación utilice las mejores herramientas disponibles para evaluar la cantidad de esfuerzo que se debe invertir en el proyecto. Esta estimación conducirá al cronograma y presupuesto del proyecto.
Hay varios aspectos a considerar al principio. La declaración de alcance ya ha definido los objetivos del proyecto y los criterios de aceptación. Además, ya se ha completado el modelado de negocio necesario y se han incorporado los requisitos de alto nivel a los casos de uso del sistema.
Con la técnica de análisis de casos de uso, se puede estimar el esfuerzo total para desarrollar el proyecto, así como el tiempo de calendario ideal y el tamaño medio del equipo; estas son medidas globales para el proyecto.
Ahora es necesario definir la duración y el número de iteraciones.

                ​ 4.3.1 Estimación de la duración de las iteraciones
Una iteración comienza con la planificación y termina con una nueva versión del sistema que se libera internamente o se entrega al cliente. La duración de una iteración en UP y metodologías ágiles suele oscilar entre una y ocho semanas,15 y depende, entre otros factores, de la complejidad del proyecto y del tamaño del equipo.
Los equipos pequeños con hasta cinco personas16 pueden hacer la planificación juntos un lunes por la mañana, realizar el trabajo durante la semana y generar un comunicado el viernes.
Los grupos con más de 20 personas pueden necesitar más tiempo para distribuir y sincronizar las actividades. Considera que la cantidad de trabajo es normalmente mayor. Además, la generación de una versión lleva más tiempo, porque habrá una mayor cantidad de partes de software que integrar, verificar y arreglar. Por lo tanto, en ese caso, se permitirían iteraciones de tres a cuatro semanas.
Los grupos de más de 40 personas necesitan trabajar en un entorno más estructurado y formal, con más documentación intermedia, para que el flujo de información sea naturalmente más lento. Por lo tanto, una iteración de seis a ocho semanas sería aconsejable.
Otros factores que pueden afectar la duración de las iteraciones son los siguientes:
    • La generación automática de código y las herramientas de software de ciclo de vida integradas permiten iteraciones más cortas.
    • Un equipo que es muy competente en UP y en técnicas de análisis, diseño y codificación permite iteraciones más cortas.
    • Si la calidad es una preocupación crítica y, en consecuencia, las pruebas y revisiones son intensas, entonces las iteraciones deben ser más largas, a menos que se utilice una automatización extensa y patrones de codificación de calidad eficaces.

                ​ 4.3.2 Número de iteraciones
El número de iteraciones de un proyecto depende del tiempo de calendario dividido por la duración de cada iteración. Por ejemplo, para el proyecto Livir, con el equipo de novicios, el proyecto duraría unos 10 meses con un equipo de seis personas. Así, se utilizaría una iteración de dos semanas, con un total de 20 iteraciones.
El número de iteraciones que se considerarían para la Elaboración y Construcción depende fundamentalmente de la necesidad de abordar los problemas arquitectónicos. Esto puede estimarse aproximadamente por la cantidad proporcional de casos de uso complejos que deben ser estudiados y desarrollados. Como el hito de la fase de Elaboración es una arquitectura estable, se puede asumir que la Elaboración no terminará mientras haya casos complejos de uso de alta prioridad que necesiten ser analizados. Kruchten (2003) estima que la Elaboración tomaría alrededor del 30% del tiempo lineal de un proyecto típico y la Construcción tomaría alrededor del 50% del tiempo de un proyecto típico, mientras que la Iniciación y la Transición tomaría alrededor del 10% cada una.
Otra pregunta que viene a la mente en este punto es si la estimación del esfuerzo incluye la fase de inicio o no (porque el inicio está prácticamente terminado cuando se hace la estimación). El método COCOMO II, por ejemplo, cuando se aplica al Proceso Unificado, estima sólo el esfuerzo que se va a gastar en Elaboración y Construcción, dejando que Iniciación y Transición se calcule como un porcentaje del esfuerzo total. Normalmente, se cree que el análisis de casos de uso estima el esfuerzo total de un proyecto, desde su inicio hasta la entrega del producto. Sin embargo, si el equipo utiliza otra interpretación, lo importante es mantenerla coherente de un proyecto a otro. Cualquier discrepancia en las medidas de estimación sería absorbida por el índice de productividad del equipo.

                ​ 4.3.3 Esfuerzo por caso de uso
Con el fin de encontrar el esfuerzo para desarrollar cada tipo de caso de uso (simple, medio o complejo), se puede utilizar el siguiente procedimiento:
1. Tome el esfuerzo total del proyecto (E) y divídalo entre el peso total no ajustado del caso de uso (UUCW) - ignore el peso de los actores.
2. El valor resultante es el esfuerzo estimado por punto de caso de uso no ajustado para el proyecto específico y el equipo (EUCP=E/UUCW).
3. Finalmente, encuentre el esfuerzo para cada tipo de caso de uso multiplicando EUCP por 5 en el caso de los casos de uso simple, por 10 en el caso de los casos de uso medio y por 15 en el caso de los casos complejos.
Para el ejemplo que tenemos:

Así:
    • Los casos de uso simple requieren 5*0.271=1.355 meses de personal.
    • Los casos de uso medio requieren 10*0,271=2,71 meses de personal.
    • Los casos de uso complejo requieren 15*0,271=4,065 meses de personal.
Note que el equipo de los sueños produciría valores mucho más bajos que esos. En el caso del equipo de los sueños:

Así:
• Los casos de uso simple demandan 5 * 0.047 = 0.235 meses de personal.
• Los casos de uso medio demandan 10 * 0.047 = 0.47 meses de personal.
• Los casos de uso complejos demandan 15 * 0.047 = 0.705 meses de personal.

                ​ 4.3.4 Capacidad de carga del equipo
Otra información que se puede calcular es la capacidad de carga del equipo (TLC) para cada iteración. Se calcula como el número de miembros del equipo multiplicado por la duración de la iteración (expresada en meses):

TLC = P * tamaño de iteración (en meses)

En el ejemplo, considerando el equipo de novatos (seis personas) y las iteraciones de dos semanas (alrededor de 0.5 meses), TLC=6*0.5=3. Esto significa que cada iteración de ese proyecto tiene una carga de trabajo de tres meses de personal.
Con una iteración de dos semanas, el equipo no podría terminar un caso de uso complejo (requiere 4.065 meses de personal, como se ha visto anteriormente). Se pueden considerar dos opciones:
    • Extienda la duración de las iteraciones a tres semanas (aproximadamente 0,75 meses).
    • Cortar los casos de uso para que puedan ser implementados parcialmente en iteraciones de dos semanas.
Aunque los desarrolladores ágiles preferirían iteraciones más cortas, si elegimos extender las iteraciones, el tiempo de calendario para el proyecto (10 meses) dividido por la duración de la iteración (0.75) resulta en 13.3 iteraciones, las cuales pueden ser ajustadas a 14, a menos que el proyecto sea apresurado. De esta manera, la carga de equipo por iteración sería de 6*0.75=4.5 y una iteración sería suficiente para tratar un caso de uso complejo completo.

                ​ 4.3.5 Definición de la prioridad del caso de uso
Una de las principales técnicas para reducir el riesgo en un proyecto es tratar primero los casos de uso más complejos, especialmente si son los que representan los procesos de negocio más críticos, porque con ellos el equipo puede aprender más sobre el sistema que con otros casos de uso. Los casos de uso de patrones como CRUD (complejidad media) e informes (complejidad mínima) pueden ser tratados más adelante durante la construcción.
La planificación indica cuándo se va a analizar, diseñar e implementar cada caso de uso. El Proceso Unificado, como la mayoría de las técnicas ágiles, no espera que el plan general del proyecto defina cuándo se va a implementar cada caso de uso. Sin embargo, se colocan en una lista dinámica de prioridades y, aunque puede actualizarse sobre la marcha, es posible saber cuándo debe completarse cada caso de uso. La planificación de una iteración comienza eligiendo qué casos de uso, riesgos o requisitos de cambio se tratarán en la siguiente iteración. Al planificar una iteración, se deben tener en cuenta los siguientes aspectos a la hora de elegir los casos de uso a tratar:
    • Usar la complejidad de los casos: Los casos de uso de mayor riesgo y complejidad deben abordarse en primer lugar en la mayoría de los casos, a menos que condiciones especiales (por ejemplo, un caso de uso relativamente simple con alto riesgo tecnológico) justifiquen la elección de casos de uso diferentes.
    • Dependencias entre casos de uso: Los casos de uso que tienen una fuerte dependencia de los que ya estaban acomodados en la iteración deben ser tratados en conjunto si es posible, ya que evita la fragmentación del trabajo en las clases.
    • Capacidad de carga del equipo: El trabajo de desarrollo debe ser asignado a los miembros del equipo en base a su TLC.
Una sugerencia para priorizar los casos de uso del ejemplo de Livir representado en la Figura 3.11 se presenta en la Tabla 4.7.


Tabla 4.7
Sugerencia de prioridades de Caso de Uso para el ejemplo de Livir


1.Order books 
   Pedidos de libros
12. Manage books <<crud>>
     Mantenimiento de libros
2.Pay order
   Orden de pago
13.Manage publishers<<crud>>
    Mantenimiento de Editores
3.Deliver order
   Entregar pedido
14.Order status <<report>>
    Informe de estado del pedido
4.Register delivery confirmation
   Registrar confirmación de entrega
15.Past sales <<report>>
    Informe de ventas anterior
5.Receive books
   Recibir libros
16.Book sales by period <<report>>
    Ventas de libros por informe de período
6.Resend order
   Reenviar pedido
17.Books available for sale <<report>>
    Informe de libros disponibles para la venta
7.Register order return
   Registrar la devolución de pedidos
18.Book returns by period <<report>>
    Devoluciones de libros en un periódo
8.Discard books
   Descartar libros
19.Upcoming orders by period <<report>>
    Pedidos previstos por periodo 
9.Cancel order
   Cancelar pedido
20.Deliveries by period <<report>>
    Entregas previstas por periodo
10.Create/remove special offer
   Crear/eliminar oferta especial
21.Discarded books by period <<report>>
   Informe de Libros descartados en un período
11.Manage customers <<crud>>
   Mantenimiento de libros


El orden de esta lista es el más crítico para los casos de uso complejos, porque una elección errónea en términos de sus prioridades podría llevar a una refactorización innecesaria en iteraciones posteriores. Consideramos que los casos de uso más importantes para este negocio son los relacionados con el proceso de venta de libros, porque eso es lo que genera beneficios para la empresa. Sin embargo, el orden de los casos de uso con menor riesgo, como los cruds y los informes, no es tan crítico.

                ​ 4.3.6 Fase de planificación e iteraciones
Con la información obtenida en las secciones anteriores, es posible elaborar el plan de liberación preliminar utilizando las prioridades de los casos de uso, el esfuerzo y la capacidad de carga del equipo.
Los objetivos de una iteración pueden ser de tres tipos:
    • Implementar total o parcialmente uno o más casos de uso.
    • Mitigar uno o más riesgos, generando o realizando un plan de reducción de probabilidad, reducción de impacto o recuperación de desastres.
    • Implementar total o parcialmente uno o más cambios solicitados. A medida que la arquitectura del sistema evoluciona durante las iteraciones, se pueden solicitar cambios debido a la falta de conformidad con los requisitos o a errores de diseño. Incorporar estos cambios en el software puede ser uno de los objetivos de una interacción. Este tipo de objetivo suele surgir sólo después de la primera iteración.
Para cada elemento (caso de uso, riesgo o cambio solicitado) debe haber una estimación del esfuerzo. Los elementos serán seleccionados para su inclusión en una iteración u otra dependiendo de su prioridad (las prioridades pueden cambiar a medida que el proyecto avanza - por lo tanto, la planificación también puede cambiar). Se debe dar mayor prioridad a los elementos más complejos y arriesgados, que son los que tienen mayor potencial para aprender sobre el sistema. La sugerencia es elegir primero:
    • Casos de uso que representen los procesos de negocio más críticos, por ejemplo, aquellos que ayuden a la empresa a alcanzar sus objetivos organizativos, como la obtención de beneficios.
    • Riesgos de alta importancia (o de alta exposición), es decir, aquellos con un alto impacto y una alta probabilidad de convertirse en problemas.
    • Solicitudes urgentes de cambio, por ejemplo, las que requieren refactorización de la arquitectura.
Al considerar los elementos de mayor prioridad, otros elementos con prioridades más bajas, pero estrechamente relacionados con los de mayor prioridad, pueden añadirse en la misma iteración por conveniencia. Lo importante es que el esfuerzo total asignado a la iteración no supere el valor del mes del personal que corresponde a la capacidad de carga del equipo.
La mitigación del riesgo y algunas solicitudes de cambio pueden no ser adecuadas para la estimación del esfuerzo porque su tamaño no puede medirse en términos de puntos de casos de uso (o cualquier otra métrica). Por ejemplo, encontrar y arreglar un error puede tomar segundos o semanas. En estos casos, normalmente se asigna una cantidad fija de tiempo, como, por ejemplo, invertir un miembro del equipo durante una semana para trabajar en la mitigación de un riesgo determinado. Al final del cuadro de tiempo17 previamente definido se evalúa el resultado y se decide si la actividad debe continuar o no.
Consideremos que el proyecto tiene 10 meses (40 semanas) y la duración de la iteración es de tres semanas. Luego, la Iniciación y Transición tomaría alrededor de cuatro semanas (10% del tiempo total), la Elaboración tomaría alrededor de 12 semanas (30% del tiempo total) y cuatro iteraciones de tres semanas, y la Construcción tomaría alrededor de 20 semanas (50% del tiempo total) y cerca de siete iteraciones (una de ellas podría ser una semana más corta, o una semana a partir de la fase de Transición podría ser prestada para la última iteración de la Construcción - la alternativa escogida que se presenta a continuación).
Kroll (2004) presenta una sugerencia para un plan de fase genérico que se adapta al ejemplo de Livir en la Tabla 4.8. Por el momento no se incluyeron las solicitudes de cambio porque aparecen sólo cuando el proyecto está en marcha, no al principio. Por lo tanto, el plan en este caso se basó únicamente en la liberación de casos de uso y la mitigación de riesgos.

Tabla 4.8
Ejemplo genérico de planificación de fase para el Livir

Fase
Iteración
Objetivo Principal (Riesgos y Casos de Uso Abordados) 
Semanario
Inicio
I1
Definir visión
Determinar el alcance del proyecto
Definir arquitectura candidata
Crear caso de uso de negocio 
Crear plan de desarrollo de software 
  1 a 4
Elaboración
E1
Instalar y probar componentes de arquitectura 
Validar los detalles de los requisitos
Implementar casos de uso prioritario
Probar la arquitectura propuesta
  5 a 7

E2-E4
Mitigar los riesgos arquitectónicos.
Instalación y prueba completa de la arquitectura
Implementación de casos de uso adicionales
Elementos arquitectónicos de prueba de carga
8 a 16
Construcción
C 1-C6
Describir e implementar casos de uso adicionales
Integrar el producto y validar 
17 a 34

C7
Describir e implementar casos de uso adicionales 
Integrar el producto y validar 
Plan de prueba beta
Manual de usuario
34 a 37
Transición
T1
Entregar la versión beta al cliente
Analizar la retroalimentación de los usuarios de la versión beta
Aplicar correcciones
Finalizar el manual de usuario y otros artefactos
Entrega al cliente
38 a 40


Una vez concluida la fase de planificación (normalmente al final de Inicio), se puede detallar el plan para la primera iteración de la Elaboraciónn E1, eligiendo los casos de uso, y detallando y asignando las actividades a los desarrolladores. Sólo cuando esa iteración está en marcha debe comenzar la planificación para la segunda iteración.
El propósito de un plan de iteración incluye lo siguiente (Kroll 2004):
1. Definir el alcance de la iteración definiendo sus objetivos en términos de los artefactos que se producirán, tales como:
    • Detallar e implementar casos de uso específicos.
    • Mitigación de riesgos conocidos.
    • Realizar los cambios solicitados.
2. Crear un plan detallado sobre cómo debe desarrollarse la iteración.
3. Crear, identificar y gestionar dependencias de tareas.
4. Asignar tareas a personas.
Por ejemplo, considera que estás planificando la primera iteración de elaboración E1 para el proyecto Livir. Consideras las metas generales presentadas en la Tabla 4.8, y el estado actual del sistema. Algunos de los objetivos de iteración podrían definirse como:
    • Expandir e implementar el caso de uso 01:  Pedir Libros
    • Probar y refinar la arquitectura preliminar.
    • Realizar planes de mitigación de riesgo K1: Requerimientos inestables.
Luego, la planificación puede continuar definiendo los entregables de la iteración y las tareas necesarias para producirlos, y asignándolos a los desarrolladores. Los equipos ágiles pueden preferir producir este plan en una reunión de equipo, mientras que los equipos que siguen a el UP pueden preferir instanciar algunos de los flujos de trabajo del UP y determinar qué tareas deben realizarse para lograr los objetivos de la iteración. Explicar esto está fuera del alcance de este libro, pero los lectores interesados en aprender más pueden empezar consultando a West (2002) o Crain (2004).

            ​ 4.4 El proceso visto hasta ahora


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

Analisis y Diseño
Preparar un modelo conceptual preliminar observando los casos de uso del sistema y los conceptos expresados en el.

Implementación


Pruebas/Test


Gestión del Proyecto
Estimar el esfuerzo total, el cronograma ideal y el tamaño medio del equipo para el proyecto.
Estimar la duración y el número de iteraciones para cada fase.
Preparar la fase de planificación y el plan de Iteración para la primera iteración.


            ​ 4.5 Preguntas

1. Explicar las diferencias entre COCOMO II, el análisis de puntos de función y el análisis de puntos de uso. ¿Cuáles son sus ventajas y desventajas relativas?
2. En el análisis de casos prácticos, ¿cuál es la diferencia entre factores técnicos y ambientales? ¿Por qué el análisis de puntos de caso los considera como grupos separados?
3. Deje que E sea el esfuerzo total para desarrollar un proyecto, y T el tiempo de calendario ideal recomendado para el mismo proyecto. ¿Qué sucede con E cuando el proyecto debe ser desarrollado en un tiempo menor que T? ¿Ocurre lo mismo cuando el proyecto puede desarrollarse en un tiempo superior a T?
4. ¿Cómo se determina la duración ideal de una iteración para un proyecto determinado?
5. ¿Cómo se establece una lista de prioridades para los casos de uso?

1En la serie actual de Fibonacci, cada número es la suma de los dos anteriores. Así, la serie original es 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, etc. Sin embargo, para fines de estimación se utiliza una serie aproximada porque a medida que los números crecen, la estimación es menos precisa.
2Para minimizar esta incertidumbre, se pueden utilizar tablas que convierten los puntos de función en KSLOC (Boehm, 2000).
3Integración del modelo de madurez de la capacidad.
4Mejora de procesos de software y determinación de capacidades.
5Algunas definiciones también consideran los riesgos positivos como situaciones que pueden ocurrir y ayudan al proyecto.
6Los lectores que no estén interesados en conocer los detalles sobre cómo estimar el esfuerzo y desarrollar un plan de proyecto pueden pasar directamente de aquí al Capítulo 5, donde se siguen explicando las técnicas de análisis y diseño orientadas a objetos.
7http://www.ifpug.org/
8 Por ejemplo, en cuanto al factor T12, hay autores que dicen que más acceso de terceros significa menos esfuerzo, porque hay reutilización de código, mientras que otros autores dicen que más acceso de terceros significa más esfuerzo, porque es necesario entender código escrito por otros. En este libro, se construye una síntesis entre esas dos vistas: se considera bueno tener acceso a un código bien escrito, no tan bueno tener acceso a un código que necesita revisión, y peor aún, no tener acceso a ningún código de terceros. Reutilizar código de mala calidad se considera completamente indeseable (normalmente es más fácil desarrollarlo desde cero).
9Algunos elementos como "menús" y "desplazamiento" que se consideraron originalmente en el análisis de puntos de función se eliminaron de la lista porque se consideran demasiado triviales para las aplicaciones actuales.
10Ocasionalmente se hace referencia a este elemento como "usabilidad", pero el concepto original de usabilidad ya se consideraba en el factor T3, la eficiencia del usuario final. Preferimos interpretar este factor como "fácil de operar" por su compatibilidad con los factores técnicos del análisis de puntos de función, y también para evitar confusión y redundancia con el factor de eficiencia del usuario final.
11Seguramente ese es uno de los factores ambientales más difíciles de evaluar, porque la motivación real del equipo puede estar enmascarada. La sugerencia de Ribu (2001) pareció ayudar muy poco en la calificación de este factor, y nos tomamos la libertad de reinterpretar la referencia.
12Sistema de información.
13Opcionalmente, el TPI podría expresarse como el número de puntos de casos de uso que un miembro del equipo puede producir en una unidad de tiempo determinada. En ese caso, la fórmula debe ser E=UCP / TPI.
14Recuerde que un caso de uso complejo tiene 15 puntos de caso de uso y por lo tanto requiere alrededor de 300 horas de personal para ser desarrollado completamente de acuerdo con Karner (1993).
15Los métodos ágiles prefieren la duración más corta posible. Algunos métodos como XP son más radicales al prohibir las iteraciones con más de tres semanas, pero otros métodos son más relajados al respecto.
16Otros equipos más grandes que están muy afinados y tienen un excelente soporte de herramientas.
17Un cuadro de tiempo es un período fijo de tiempo asignado a una tarea.