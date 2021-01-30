# ADOO

- [Análisis y Diseño de sistemas orientado a Objetos](#análisis-y-diseño-de-sistemas-orientado-a-objetos)
- [El proceso visto hasta ahora](#el-proceso-visto-hasta-ahora)
- [Preguntas](#preguntas)
---

## Análisis y Diseño de sistemas orientado a Objetos

¿Qué es el desarrollo de sistemas orientados a objetos? 

Al observar la forma en que el análisis y el diseño orientado a objetos se enseña y se practica en algunos lugares, se puede concluir que muchos profesores simplemente adoptan un lenguaje de programación orientado a objetos, o utilizan fragmentos de un proceso de desarrollo basado en objetos.   
No es suficiente organizar la arquitectura del sistema en niveles y módulos si el código implementado en su interior es desorganizado.   
Algunos programadores organizan el sistema adecuadamente en clases y paquetes, pero todavía escriben “código espagueti” dentro de los métodos de estas clases y paquetes.   
Además, otros desarrolladores todavía utilizan la descomposición funcional de arriba hacia abajo dentro de los métodos, lo que no es apropiado cuando se utiliza programación orientada a objetos (_la descomposición de arriba hacia abajo es adecuada si se utiliza programación estructurada en su lugar_).   
Para construir código realmente orientado a objetos, los desarrolladores deben aprender las **técnicas de delegación** y **asignación de responsabilidades**, que pueden conducir a código reutilizable y de bajo acoplamiento. El uso de diagramas no necesariamente mejorará la calidad del software, aunque puede ayudar. 

Sin lugar a dudas utilizaremos el [UP y UML](060UP.md).


## El proceso visto hasta ahora
Tras cada paso, una tabla muestra qué actividades de análisis y diseño han sido cubiertas, destacando aquellas que fueron cubiertas por el tema actual. 

![UP](https://eternalsunshineoftheismind.files.wordpress.com/2013/03/rup.jpg)

En este módulo sólo se abordan las fases de inicio y elaboración, y sólo se abordan las disciplinas de modelado de negocio, requisitos, análisis y diseño, implementación, pruebas y algunos aspectos de la gestión de proyectos (si se puede).
El resto se las dejamos a otros módulos.


|                                    | Inicio | Elaboración | Construcción | Transición |
| ---------------------------------- | ------ | ----------- | ------------ | ---------- |
| Modelado del Negocio               | x      | x           |              |            |
| Requerimientos                     | x      | x           |              |            |
| Analisis y Diseño                  | x      | x           |              |            |
| Implementación                     | x      | ?           |              |            |
| Pruebas/Test                       | x      | x           |              |            |
| Gestión de Proyectos               | ?      | ?           |              |            |
| Despliegue                         |        |             |              |            |
| Configuración y Gestión del cambio |        |             |              |            |
| Entorno                            |        |             |              |            |



## Preguntas

1. ¿Cuáles son los cuatro principios fundamentales del Proceso Unificado?
2. ¿Cuál es el objetivo de cada una de las cuatro fases del Proceso Unificado?
3. ¿En qué se diferencian las fases de UP de las fases de la cascada?
