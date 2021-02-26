# Suma dos Fracciones



## Enunciado

Se nos pide que creemos un aplicativo que sume dos fraciones.

## Modelado de Negocio
N/A

## Caso de Uso y Requisitos

### Caso de uso del sistema

<img src="http://www.plantuml.com/plantuml/proxy?src=https://raw.githubusercontent.com/srlopez/RUP/master/ejemplos/fraccion_completo.md&idx=0" alt=""/>

<details><summary>Code #0</summary>

```plantuml
@startuml
skinparam usecase {
  BackgroundColor White
  BorderColor DarkSlateGray
  ArrowColor Grey
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
note "Requisito funcional #1" as n1

left to right direction
:User: as cli
rectangle sistema {
  (Sumar dos\nFracciones\n<b>UC1</b>) as suma 
}

cli -- suma
suma -- n1
@enduml
```
</details>

### Caso de Uso Completo

Use case 01: **Sumar Dos Fracciones**
1. El sistema pide una fracción
2. El usuario introduce f1
3. El sistema pide otr fracción
4. El usuario introduce f2
5. El sistema suma f1 y f2 y presenta el resultado
6. El sistema se acaba

### Diagrama Conceptual del Dominio
N/A

### Diagrama de Clases

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

CtrlTerminal -- Calculadora
CtrlTerminal -- ViewTerminal


@enduml
```
</details>

## Diagrama de secuencia

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
        Fraccion f1 = viewTerminal.leerFraccion();
        Fraccion f2 = viewTerminal.leerFraccion();
        Fraccion result = sistema.suma(f1, f2);
        viewTerminal.mostrarResultado(result);
    }
```

[Código completo en GitHub](https://github.com/srlopez/javaPlantilla)