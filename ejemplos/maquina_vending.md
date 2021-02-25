# Máquina Vending
<!--
Nomenclatura PlantUML
https://crashedmind.github.io/PlantUMLHitchhikersGuide/index.html

VSCODE settings.json
PlantUML Server:
https://www.plantuml.com/plantuml
-->
- [Máquina Vending](#máquina-vending)
  - [Enunciado](#enunciado)
  - [Modelado de Negocio](#modelado-de-negocio)
    - [Visión general del Sistema a desarrollar.](#visión-general-del-sistema-a-desarrollar)
    - [Diagrama de **Caso de uso de NEGOCIO**](#diagrama-de-caso-de-uso-de-negocio)
    - [Diagrama de **Actividad del NEGOCIO**](#diagrama-de-actividad-del-negocio)
    - [Diagrama de **Máquina de Estado** de la Golosina](#diagrama-de-máquina-de-estado-de-la-golosina)
  - [Casos de Uso de Sistema y Requisitos](#casos-de-uso-de-sistema-y-requisitos)
    - [Casos de uso de SISTEMA](#casos-de-uso-de-sistema)
    - [Diagrama Conceptual del Dominio](#diagrama-conceptual-del-dominio)
  - [Casos de Uso Completos](#casos-de-uso-completos)
  - [Diagrama de Secuencia UC](#diagrama-de-secuencia-uc)
  
## Enunciado

Ver el enunciado+

- Dos empresas A de Golosinas y B de Refrescos
- Los Dispensadores salen con las etiquetas de producto y precios establecidas
- Los Dispensadores pueden ser de dimensiones distintas
- La seguridad en A es por PIN, y en B es por algoritmo
- La máquina funcionará en modo USER o en modo ADMIN para las funciones de administración.
- Se oye hablar de fusión de empresas

## Modelado de Negocio

### Visión general del Sistema a desarrollar.

Queremos que la interacción de las personas con nuestras máquinas sea fácil, eficiente y segura. De esta manera queremos que:
- El usuario (sea un cliente o un reponedor pueda ver la matriz de los productos) visualizando el nombre del producto y el precio. Para modo ADMIN se pedirá un PIN de acceso, en caso de ser válido se mostrará también la cantidad del producto
- Para adquirir un producto bastará indicar las coordenadas del producto e introducir el importe del pago.
- En modo ADMIN: 
  - El reponedor repone la cantidad de productos hasta el máximo y también rellena la caja de cambios y retira el importe en el cajón.
  - Existe la posibilidad de obtener un informe, que será recordada antes de apagar la máquina.

Condicionantes/Reglas de negocio:
- Sólo manejamos monedas de 2€, 1€, .5€, .2€ y .1€ €uros.
- El cambio será con el mínimo numero de monedas posibles y no devolvemos moedas de 2€
- El pago será como máximo con 5 monedas

### Diagrama de **Caso de uso de NEGOCIO**

Presenta objetivos a largo plazo del Negocio.   
El caso de uso:
Un caso de uso de negocio `implica una relación entre la empresa y una entidad externa` (un cliente), `produciendo un resultado perceptible y consistente` para la empresa y el actor.

<img src="http://www.plantuml.com/plantuml/proxy?src=https://raw.githubusercontent.com/srlopez/RUP/master/ejemplos/maquina_vending.md&idx=0" alt=""/>

<details><summary>Code #0</summary>

```plantuml
@startuml
title == Máquina Vending ==\nModelado de Dominio
left to right direction
:Cliente:/ as cli
:Proveedor:/ as pro
:Administrador\nprincipal:/ as jefe <<worker>>
:Reponedor:/ as repo <<worker>>
(Comprar Golosinas)/ as comprar
rectangle Límite_de_Automatización:_La_Máquina {
  (Vender Golosinas)/ as vender
  (Reponer Golosinas)/ as reponer
}
cli -- vender
repo -- reponer
pro -- comprar
comprar -- jefe
@enduml
```
</details>

### Diagrama de **Actividad del NEGOCIO**

Presenta las actividades principales de la empresa en relación con el producto `lifemotiv` del negocio.

<img src="http://www.plantuml.com/plantuml/proxy?src=https://raw.githubusercontent.com/srlopez/RUP/master/ejemplos/maquina_vending.md&idx=1" alt=""/>


<details><summary>Code #1</summary>

```plantuml
@startuml
title == Máquina Vending ==\nDiagrama de Actividad
|Proveedor|
|Administrador|
|Reponedor|
|Cliente|
|Administrador|
start
:Encargar golosinas;
|Proveedor|
:Enviar golosinas;
|Reponedor|
:Recibir golosinas;
:Reponer golosinas;
|Cliente|
:Comprar golosinas;
stop
@enduml
```
</details>


### Diagrama de **Máquina de Estado** de la Golosina

Presenta las posibilidades en las que se puede encontrar el producto sobre el que gira nuestro negocio

<img src="http://www.plantuml.com/plantuml/proxy?src=https://raw.githubusercontent.com/srlopez/RUP/master/ejemplos/maquina_vending.md&idx=2" alt=""/>


<details><summary>Code #2</summary>

```plantuml
@startuml
title == Máquina Vending ==\nMáquina de Estado Golosina
skinparam state {
    ' StartColor PaleGreen
    ' EndColor Red
    BackgroundColor White
    ' BackgroundColor<<Junction>> GreenYellow  
    BorderColor Gray
    ' FontName Consolas
}
left to right direction
[*] -d-> Registrado
Registrado --> Encargado : Pedido
Encargado --> EnStock : Recibido 
EnStock -r-> EnMaquina : Reparto
state EnMaquina {    
  top to bottom direction
  [*] --> Disponible    
  Disponible --> Agotado : [OK]
  Agotado --> Disponible
  Agotado --> [*]
}

EnStock : Esperamos alerta de máquina
Registrado : Producto en nuestro sistema
Encargado: Pedido realizado
Disponible: Cantidad>0
Agotado: Cantidad=0
@enduml
```
</details>

Modelando el negocio descubrimos a partir de los diagramas presentados, un poco más sobre el Dominio de nuestra aplicación.


## Casos de Uso de Sistema y Requisitos

### Casos de uso de SISTEMA

Indicamos los Requisitos NO FUNCIONALES en Notas

<img src="http://www.plantuml.com/plantuml/proxy?src=https://raw.githubusercontent.com/srlopez/RUP/master/ejemplos/maquina_vending.md&idx=3" alt=""/>

<details><summary>Code #3</summary>

```plantuml
@startuml
title == Máquina Vending ==\n<i>Casos de uso</i>
'  skinparam handwritten true
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


left to right direction
:User: as cli
:Reponedor: as repo <<worker>>
rectangle ADMIN\nMode as admin {
  (Reponer\nGolosinas\n<b>UC3</b>) as reponer 
  (Informe\n<b>UC4</b>) as infor <<report>>
  (Apagar\nmáquina\n<b>UC5</b>) as off
  rectangle USER\nMode {
    (Ver\nDispensador\n<b>UC1</b>) as ver 
    (Comprar\nGolosinas\n<b>UC2</b>) as vender 
  }
}
note "- Pago de máximo 5 monedas\n- Cambio sin monedas de 2€\n- Se admite monedas de 2€, 1€, .5€, .2€ y .1€"  as N1  #white
note "Se aplica el sistema de\nSeguridad"  as N2  #white 

repo -l-|> cli
cli -- vender
cli -- ver
repo -- reponer
repo -- off
repo -- infor

admin -- N2
vender -- N1


vender .r.> ver: include
off .r.> infor: extends
@enduml
```
</details>

### Diagrama Conceptual del Dominio

<img src="http://www.plantuml.com/plantuml/proxy?src=https://raw.githubusercontent.com/srlopez/RUP/master/ejemplos/maquina_vending.md&idx=4" alt=""/>

<details><summary>Code #4</summary>

```plantuml
@startuml
' left to right direction
title == Máquina Vending ==\n<i>Modelo Conceptual</i>
skinparam class {
  skinparam monochrome true
  skinparam shadowing false
  BackgroundColor White
  BorderColor Gray
  ' FontName Consolas
  ArrowColor Gray
}
scale 1
legend center
    <b>Maquina de Vending</b>
endlegend
hide  circle

Maquina .. Dispensador 
Maquina .. ControladorDePagos
Maquina .. Seguridad
Dispensador .. Producto
Producto .. Refresco
Producto .. Golosina 
class  Efectivo

@enduml
```
</details>

## Casos de Uso Completos

## Diagrama de Secuencia UC
