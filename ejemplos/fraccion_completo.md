# Suma dos Fracciones



## Enunciado

Se nos pide que creemos un aplicativo que sume dos fraciones.

## Modelado de Negocio
N/A

## Caso de Uso y Requisitos

### Casos de uso de sistema

Mostramos tres posibles casos de uso, pero sólo nos enfocamos en **UC1**

<img src="http://www.plantuml.com/plantuml/proxy?src=https://raw.githubusercontent.com/srlopez/RUP/master/ejemplos/fraccion_completo.md" alt=""/>

<details><summary>Code #0</summary>

```plantuml
@startuml
hide stereotype

skinparam usecase {
  BackgroundColor White
  BorderColor DarkSlateGray
  ArrowColor Grey
  
  BorderThickness<<beta>> 1
  BorderStyle<<beta>> dotted
  'BackgroundColor<<beta>> #FFE
  'BorderColor<<beta>> Red
}
skinparam actor {
  BackgroundColor White
  BorderColor DarkSlateGray
  ArrowColor Grey
}
skinparam note {
  BackgroundColor White
  BorderColor DarkSlateGray
}
note "UC#1\nRequisito <b>Funcional</b> == UC" as n1
note "UC#2\nRequisitos <b>No funcionales</b>\nescritos como notas" as n2

left to right direction
:User: as cli
rectangle sistema {
  (Sumar dos\nFracciones\n<b>UC1</b>) as suma 
  (Caso Dos\n<b>UC2</b>) as dos<<beta>> 
  (Caso Tres\n<b>UC3</b>) as tres<<beta>>
}

cli -- suma
suma -- n1
dos -- n2
cli -- dos
cli -- tres
@enduml
```
</details>

### Caso de Uso Completo

Use case 01: **Sumar Dos Fracciones**
1. El sistema pide una fracción
1. El usuario introduce f1
1. El sistema pide otra fracción
1. El usuario introduce f2
2. El sistema suma f1 y f2 y presenta el resultado
3. El sistema se acaba

> La descripción de un caso de uso **completo** narra un escenario en forma de diáloguo entre el _usuario_ y el _sistema_. Se concentra en el flujo principal aunque puede incluir escenarios alternativos, con el objetivo de describir una especificación general.


### Diagrama Conceptual del Dominio
N/A

### Diagrama de Clases

Se muestra _Fracción_ como Modelo principal del Dominio, pero también se muestra el `sistema` como clase _Calculadora_. Y a efectos pedagógicos se han introducido (no tienen porqué presentarse), dos clases de la arquitectura MVC.

<img src="http://www.plantuml.com/plantuml/proxy?src=https://raw.githubusercontent.com/srlopez/RUP/master/ejemplos/fraccion_completo.md&idx=1" alt=""/>

<details><summary>Code #1</summary>

```plantuml
@startuml
'left to right direction
skinparam class {
  skinparam monochrome true
  skinparam shadowing false
  BackgroundColor White
  BorderColor Gray
  ' FontName Consolas
  ArrowColor Gray
}
scale 1
hide circle

class Fraccion {
  -int numerador
  -int denominador
-- Constructores --
  + Fraccion ()
  + Fraccion (n, d)
  + Fraccion (s)
-- Métodos --
  +String toString()
}

class Calculadora <<Sistema>>{
  +Fraccion suma()
  +int multiplica()
}

class CtrlTerminal{
-- Métodos --
  +void run()
  +void useCase1()
}

class ViewTerminal{
-- Métodos --
  - String leerFraccionString()
  +Fraccion leerFraccion()
  +void mostrarResultado()
}

CtrlTerminal -- Calculadora: Usa >
CtrlTerminal -- ViewTerminal: Usa >
@enduml
```
</details>

## Diagrama de secuencia

### Versión básica:  
> Mostramos el ejemplo más sencillo. Un escenario con un único flujo principal. Sin escenarios alternativos y que acabaremos desarrollando el código.

<img src="http://www.plantuml.com/plantuml/proxy?src=https://raw.githubusercontent.com/srlopez/RUP/master/ejemplos/fraccion_completo.md&idx=2" alt=""/>

<details><summary>Code #2</summary>

```plantuml
@startuml
title <b>Sumar Dos Fracciones</b>\n<i>Diagrama de secuencia - UseCase1</i>
skinparam monochrome true
' skinparam handwritten true
' skinparam defaultFontName Comic Sans MS
' skinparam classArrowFontName Arial

autonumber "[0]"
hide footbox

actor Usuario as u
boundary Vista as v
control Controlador as c 
participant "Calculadora\n<<Sistema>>" as s

'group Comprar Producto
c -> v: leerFraccion
v -> u: "Indica una fracción (0/1): "
u -> v: Fraccion (f1)
v -> c: Fraccion (f1)
c -> v: leerFraccion
v -> u: "Indica una fracción (0/1): "
u -> v: Fraccion (f2)
v -> c: Fraccion (f2)
c -> s: suma(f1,f2)
s -> c: Fraccion (result)
c -> v: mostrarResultado(result)
v -> u: "Suma :" (result)

'end
@enduml
```
</details>


El código en el controlador:
```java
  public void useCase1() {
      // Punto de Entrada al Caso de Uso #1 
      // Indicando el número de mensaje que se indica en el diagrama 
      Fraccion f1 = viewTerminal.leerFraccion(); // 1..4
      Fraccion f2 = viewTerminal.leerFraccion(); // 5..8
      Fraccion result = sistema.suma(f1, f2); // 9..10
      viewTerminal.mostrarResultado(result); // 11
  }
```


### Versión con una caja de `loop` y `alt` 
>Versión pedagócica para mostrar alternativas de cómo se puede modelar un diagrama de secuencia mostrando un ciclo de repetición, y las alternativas secuencias en caso de escenarios distintos. 

<img src="http://www.plantuml.com/plantuml/proxy?src=https://raw.githubusercontent.com/srlopez/RUP/master/ejemplos/fraccion_completo.md&idx=3" alt=""/>

<details><summary>Code #3</summary>

```plantuml
@startuml
title <b>Sumar Dos Fracciones</b>\n<i>Diagrama de secuencia - UseCase1</i>
skinparam monochrome true
' skinparam handwritten true
' skinparam defaultFontName Comic Sans MS
' skinparam classArrowFontName Arial

autonumber "[0]"
hide footbox

actor Usuario as u
boundary Vista as v
control Controlador as c 
participant "Calculadora\n<<Sistema>>" as s

'group Comprar Producto
c -> v: leerFraccion
v -> u: "Indica una fracción (0/1): "
u -> v: Fraccion (f1)
v -> c: Fraccion (f1)
loop mientras que f1==f2
  c -> v: leerFraccion
  v -> u: "Indica una fracción (0/1): "
  u -> v: Fraccion (f2)
  v -> c: Fraccion (f2)
end
c -> s: suma(f1,f2)
s -> c: Fraccion (result)
c -> v: mostrarResultado(result)
v -> u: "Suma :" (result)
alt result == "1/1"
  c -> v: muestraMensajeEnhorabuena
  v -> u: "Enhorabuena has sumado la unidad"
else result != "1/1"
  c -> v: muestraMensajePruebaOtraVez
  v -> u: "Inténtalo otra vez"
end

'end
@enduml
```
</details>


## Código de la aplicación
[Código completo en GitHub](https://github.com/srlopez/javaPlantilla)