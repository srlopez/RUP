# Control de Apuntes (gastos)


## Enunciado

Especificación de Requisitos Funcionales; **RF**
Se nos pide que creemos un aplicativo que: 
- Permita crear apuntes clasificados por categorias y subcategoriás
- Los consultemos
- Veamos la lista de conceptos/categorías con más importes
- Habrá un Administrador que pueda administrar las categorías
- El usuario identificado puede registrar apuntes y ver la lista de los mayores importes
- Un usuario sin identificar sólo puede ver categorias y apuntes
  
Se indican los Requisitos NO Funcionales (**RNF**), tanto los lógicos **RL** (Reglas de Negocio) como los Técnicos **RT** en NOTAS dentro del diagrama de Casos de Uso.

Con esto ya podemos empezar a jugar.  


## Código de la aplicación
[Código completo en GitHub](https://github.com/srlopez/javaApuntes)



## Modelado de Negocio
N/A

## Caso de Uso y Requisitos (RF, RL, RT)

<img src="http://www.plantuml.com/plantuml/proxy?src=https://raw.githubusercontent.com/srlopez/RUP/master/ejemplos/control_gastos.md&idx=0&v=1" alt=""/>

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

left to right direction
'top to bottom direction
:Invitado: as n
:Usuario: as u
:Admin: as a

rectangle admin #WhiteSmoke {
    rectangle user #AliceBlue{
        rectangle normal #FloralWhite {
            (Consultar\nCategorias\n<b>UC4</b>) as uc4 
            (Consultar\nSubCategorias\n<b>UC5</b>) as uc5 
        } 
        (Consultar\nApuntes\n<b>UC6</b>) as uc6 
        (Consultar\nImportes\n<b>UC7</b>) as uc7<<beta>>
        (Registrar\nApuntes\n«crud»\n<b>UC3</b>) as uc3 
    }
    (Registrar\nCategorias\n«crud»\n<b>UC1</b>) as uc1
    (Registrar\nSubCategorias\n«crud»\n<b>UC2</b>) as uc2 
}
a -- uc2
a -- uc1
u -- uc6
u -- uc3
u -- uc7
n -- uc4
n -- uc5
u -d-|> n
a -d-|> u
@enduml
```
</details>

## Casos de Uso Completos

## Diagrama de secuencia

## Diagrama de Clases

### Diagrama de Clases de Dominio

### Diagrama de Arquitectura

<img src="http://www.plantuml.com/plantuml/proxy?src=https://raw.githubusercontent.com/srlopez/RUP/master/ejemplos/control_gastos.md&idx=1&v=1" alt=""/>
<details><summary>Code #4</summary>

```plantuml
@startuml
title <b>Diagrama de Clases</b>\n<i>Arquitectura de la Aplicación</i>
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

class Fachada<<Sistema>> {   }
class View{  }

class Ctrl{
  -- Métodos --
    +void run()
    +void useCase1()
    +void useCase2()
    +void useCase3()
    +void useCase4()
    +void useCase5()
    +void useCase6()
  }


class ApuntesSQLite{ 
      -dbname 
    }

class ApuntesMem{ 
      -filename 
    }

class IApuntesDAL {  }

Ctrl ..> Fachada: sistema 
Ctrl ..> View: vista
IApuntesDAL <.r. Fachada : repositorio

ApuntesSQLite -u-|> IApuntesDAL
ApuntesMem -u-|> IApuntesDAL

@enduml
```
</details>