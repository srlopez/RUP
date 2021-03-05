# Calculadora de Fracciones Persistentes


## Enunciado

Se nos pide que creemos un aplicativo que:
- Sume dos fraciones.
- Multiplique dos fracciones.
- Persistamos las operaciones y seamos capaces de:
  - Consultar todas las operaciones
  - Consultar las operaciones por fraccion
  - Consultar el ranking de fracciones
  - Consultar los resultados impropios

Con esto ya podemos empezar a jugar.  

## Modelado de Negocio
N/A

## Caso de Uso y Requisitos

### Casos de uso de sistema

Mostramos tres posibles casos de uso, pero sólo nos enfocamos en **UC1**

<img src="http://www.plantuml.com/plantuml/proxy?src=https://raw.githubusercontent.com/srlopez/RUP/master/ejemplos/fraccion_completo.md&idx=0&a=3" alt=""/>

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
note "Requisito <b>Funcional</b>\n<b>UC1:</b>Sumar f1+f2\n<b>UC2:</b>Multiplicar f1+f2\n<b>UC3</b>\n<b>UC4</b>\n<b>UC5</b>\n<b>UC6</b>" as n1
note "Requisitos <b>No funcionales Lógicos</b>\n<b>Reglas de Negocio</b>\n<i>Escritos como notas</i>\n<b>RL1:</b> Solo operamos con fracciones propias\n<b>RL2:</b> Y de 8:00 a 15:00" as n2
note "Requisitos <b>No funcionales Técnicos</b>\n<i>Escritos como notas</i>\n<b>RT1:</b> Tiempo de respuesta<1sg\n<b>RT2:</b>Operaciones persistentes" as n3

left to right direction
:User: as cli
rectangle sistema {
  (Sumar\n2 Fracciones\n<b>UC1</b>) as uno 
  (Multiplicar\n2 Fracciones\n<b>UC2</b>) as dos 
  (Ranking\n<b>UC3</b>) as tres
  (Consultar\nFraccion\n<b>UC4</b>) as cuatro
  (Mostrar las\nOperacions\n<b>UC5</b>) as cinco
  (Resultados\nImpropios\n<b>UC6</b>) as seis
  (No Implementado\n<b>UC7</b>) as siete<<beta>>
}

cli -- uno
sistema -- n2
sistema -- n3
cli -- dos
cli -- tres
cli -- cuatro
cli -- cinco
cli -- seis
cli -- siete
uno -- n1
dos -- n1
tres -- n1
cuatro -- n1
cinco -- n1
seis -- n1
siete -- n1

@enduml
```
</details>

### Caso de Uso Completo

**Documento de Requisitos**

| ID | Descripción requisito | Implementado en | Invocado desde | Estado |
| -- | -- | -- | -- | -- | 
| UC1 | Suma de Fracciones | | | | 
| UC2 | Multiplicación de Fracciones | | | | 
| UC3 | Ranking de apariciones  | | | | 
| UC4 | Consulta de Fracciones | | | | 
| UC5 | Todas las Operaciones | | | | 
| UC6 | Resultados Impropias | | | | 
| UC7 | N/A | | | N/A | 
| RL1 | Fracciones propias | | | | 
| RL2 | De 8:00 a 15:00 | | | | 
| RT1 | Tiempo de respuesta de operacion <1sg. | | | | 
| RT2 | Operaciones persistentes | | | | 
   
   

Use case 01: **Sumar Dos Fracciones**
1. El sistema pide una fracción
1. El usuario introduce f1
1. El sistema pide otra fracción
1. El usuario introduce f2
   1. Si RL1 f1 goto 6
   1. Si RL1 f2 goto 6
   1. Si RL2 goto 6
1. El sistema suma f1 y f2 y presenta el resultado
1. El sistema se acaba

> La descripción de un caso de uso **completo** narra un escenario en forma de diáloguo entre el _usuario_ y el _sistema_. Se concentra en el flujo principal aunque puede incluir escenarios alternativos, con el objetivo de describir una especificación general.


### Diagrama Conceptual del Dominio
N/A

### Diagrama de Clases

Se muestra _Fracción_ y _Operación_ como Modelo principal del Dominio, pero también se muestra el `sistema` como clase _Calculadora_. 

<img src="http://www.plantuml.com/plantuml/proxy?src=https://raw.githubusercontent.com/srlopez/RUP/master/ejemplos/fraccion_completo.md&idx=1&a=3" alt=""/>

<details><summary>Code #1</summary>

```plantuml
@startuml
left to right direction
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
class Operacion {
 Date fh
-- Métodos --
  +String toString()
}
class OperacionTipo<<enum>> {}

class Calculadora {
  +Fraccion suma()
  +Fraccion multiplica()
}
class CalculadoraDB<<Sistema>> {
  +Fraccion suma()
  +Fraccion multiplica()
  -registrarOperacion()
  +qryOperacionesPor()
  +qryRanking() 
  +qryResultadosImpropios()
  +qryTodaslasOperaciones()
}
CalculadoraDB --|> Calculadora
Fraccion --* Operacion: f1
Fraccion --* Operacion: f2
Fraccion --* Operacion: resultado
OperacionTipo -- Operacion
CalculadoraDB ..> Operacion: crea >
@enduml
```
</details>

Diagrama de Clases de Arquitectura de la aplicación.
Patrones MVC y Fachada (CalculadoraDB) al Sistema.
Y Clase de Acceso a Datos con Interface, mostrando dos implementaciones.

<img src="http://www.plantuml.com/plantuml/proxy?src=https://raw.githubusercontent.com/srlopez/RUP/master/ejemplos/fraccion_completo.md&idx=2&a=3" alt=""/>

<details><summary>Code #2</summary>

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

class Calculadora {
  +Fraccion suma()
  +Fraccion multiplica()
}
class CalculadoraDB<<Sistema>> {
  +Fraccion suma()
  +Fraccion multiplica()
  -registrarOperacion()
  +qryOperacionesPor()
  +qryRanking() 
  +qryResultadosImpropios()
  +qryTodaslasOperaciones()
}

class CtrlTerminal{
-- Métodos --
  +void run()
  +void useCase1()
  +void useCase2()
  +void useCase3()
  +void useCase4()
  +void useCase5()
  +void useCase6()
}

class ViewTerminal{
-- Métodos --
  - String leerFraccionString()
  +Fraccion leerFraccion()
  +void mostrarResultado()
  +int mostrarMenu()
}

class OperacionesSQLite{ 
 -dbname 
}
class OperacionesMem{ 
  -filename 
}

class IOperacionesDAO
{
 +cmdRegistrarOperacion(op)
 +qryOperacionesPor(f)
 +qryRanking() 
 +qryResultadosImpropios()
 +qryTodasLasOperaciones() 
}

IOperacionesDAO <- CalculadoraDB : repositorio
CalculadoraDB --|> Calculadora
CtrlTerminal -- CalculadoraDB: Usa >
CtrlTerminal -- ViewTerminal: Usa >
OperacionesSQLite --|> IOperacionesDAO
OperacionesMem --|> IOperacionesDAO
@enduml
```
</details>


## Diagrama de secuencia

### Versión básica:  
> Mostramos el ejemplo más sencillo. Un escenario con un único flujo principal. Sin escenarios alternativos y que acabaremos desarrollando el código.
> Tampoco se muestran la aplicación de las Reglas de Negocio.

<img src="http://www.plantuml.com/plantuml/proxy?src=https://raw.githubusercontent.com/srlopez/RUP/master/ejemplos/fraccion_completo.md&idx=3&a=3" alt=""/>

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
v -[#LightGrey]> u: "Indica una fracción (0/1): "
u -[#LightGrey]> v: Fraccion (f1)
v -> c: Fraccion (f1)
c -> v: leerFraccion
v -[#LightGrey]> u: "Indica una fracción (0/1): "
u -[#LightGrey]> v: Fraccion (f2)
v -> c: Fraccion (f2)
c -> s: suma(f1,f2)
s -> c: Fraccion (result)
c -> v: mostrarResultado(result)
v -[#LightGrey]> u: "Suma :" (result)

'end
@enduml
```
</details>


El código en el controlador:
```java
  public void useCase1() {
      // Punto de Entrada al Caso de Uso #1 
      // Indicando el número de mensaje en el diagrama 
      Fraccion f1 = viewTerminal.leerFraccion(); // 1..4
      Fraccion f2 = viewTerminal.leerFraccion(); // 5..8
      Fraccion result = sistema.suma(f1, f2); // 9..10
      viewTerminal.mostrarResultado(result); // 11
  }
```


### Versión con una caja de `loop` y `alt` 
>Versión pedagógica para mostrar alternativas de cómo se puede modelar un diagrama de secuencia mostrando un ciclo de repetición, y las alternativas secuencias en caso de escenarios distintos. 

`Loop` para indicar un ciclo. Se describe la condición de salida.
`Alt` para indicar una condición _IF_, y se describen las condiciones que escenifican las opciones.

<img src="http://www.plantuml.com/plantuml/proxy?src=https://raw.githubusercontent.com/srlopez/RUP/master/ejemplos/fraccion_completo.md&idx=4&a=3" alt=""/>

<details><summary>Code #4</summary>

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
alt NO RL1 or NO RL2
c -> c: RL1 (f1)
c -> c: RL1 (f2)
c -> c: RL2
note right
Verificamos las Reglas de Negocio
Si no se cumple alguna -> Fin UC
end note
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
[Código de plantilla  en GitHub](https://github.com/srlopez/javaPlantilla)

[Código completo](https://github.com/srlopez/javaFraccionMVC) (Privado por ahora)