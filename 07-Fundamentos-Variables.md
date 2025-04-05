---
icon: octicons/variable-16
tags:
- Variables
---

En el tutorial anterior aprendiste sobre condiciones. Este tutorial trata sobre variables.
Las variables son una forma de almacenar información sobre el jugador, como su progreso en una quest o sus elecciones.
¡Aprenderás cómo usar variables para hacer tus quests más dinámicas!

<div class="grid" markdown>
!!! danger "Requisitos"
    * [Tutorial de Conversaciones](03-Fundamentos-Conversaciones.md)
    * [Tutorial de Eventos](05-Fundamentos-Eventos.md)
    * [Tutorial de Objetivos](04-Fundamentos-Objetivos.md)
    * [Tutorial de Condiciones](06-Fundamentos-Condiciones.md)

!!! example "Documentación Relacionada"
    * [Referencia de Variables](../../../Documentation/Scripting/About-Scripting.md#variables)
    * [Lista de Variables](../../../Documentation/Scripting/Building-Blocks/Variables-List.md)
</div>

## 1. Tipos de Variables

BetonQuest soporta varios tipos de variables:

* **Números**: Para almacenar cantidades, contadores, etc.
* **Texto**: Para almacenar nombres, mensajes, etc.
* **Booleanos**: Para almacenar estados (verdadero/falso)
* **Listas**: Para almacenar colecciones de valores

## 2. Definiendo Variables

Las variables se definen en el archivo `package.yml` de tu quest:

``` YAML title="package.yml" linenums="1"
package: tutorialQuest
variables:
  playerKills: 0 # (1)!
  playerName: "%player%" # (2)!
  hasCompletedTutorial: false # (3)!
  collectedItems: # (4)!
    - "diamond"
    - "emerald"
    - "gold_ingot"
```

1. Variable numérica que cuenta los kills del jugador
2. Variable de texto que almacena el nombre del jugador
3. Variable booleana que indica si el tutorial está completado
4. Lista de items recolectados

## 3. Usando Variables en Eventos

Las variables se pueden modificar usando eventos:

``` YAML title="events.yml" linenums="1"
events:
  incrementKills: "variable playerKills add 1" # (1)!
  setTutorialComplete: "variable hasCompletedTutorial set true" # (2)!
  addCollectedItem: "variable collectedItems add diamond" # (3)!
  resetVariables: "variable playerKills set 0\nvariable hasCompletedTutorial set false\nvariable collectedItems clear" # (4)!
```

1. Incrementa la variable `playerKills` en 1
2. Establece `hasCompletedTutorial` como verdadero
3. Añade "diamond" a la lista `collectedItems`
4. Resetea todas las variables a sus valores iniciales

## 4. Usando Variables en Condiciones

Las variables se pueden usar en condiciones para tomar decisiones:

``` YAML title="conditions.yml" linenums="1"
conditions:
  isTutorialComplete: "variable hasCompletedTutorial" # (1)!
  hasEnoughKills: "variable playerKills >= 10" # (2)!
  hasCollectedDiamond: "variable collectedItems contains diamond" # (3)!
```

1. Verifica si el tutorial está completado
2. Verifica si el jugador tiene 10 o más kills
3. Verifica si el jugador ha recolectado un diamante

## 5. Usando Variables en Conversaciones

Las variables se pueden usar en conversaciones para mostrar información dinámica:

``` YAML title="blacksmith.yml" hl_lines="3" linenums="1"
conversations:
  Blacksmith:
    quester: Blacksmith
    first: firstGreeting
    NPC_options:
      firstGreeting:
        text: "¡Bienvenido %player%! Has matado %playerKills% monstruos y has recolectado %collectedItems.size% items." # (1)!
        pointer: thatsRight
```

1. Muestra el nombre del jugador, sus kills y la cantidad de items recolectados

## 6. Probando Variables en el Juego

Para probar las variables:

1. Usa el comando `/bq variable <variable> <valor>` para establecer variables
2. Usa `/bq variable <variable>` para ver el valor actual
3. Usa `/bq variable clear` para limpiar todas las variables

## Resumen

Has aprendido cómo usar variables para:
* Almacenar información sobre el jugador
* Modificar valores usando eventos
* Tomar decisiones usando condiciones
* Mostrar información dinámica en conversaciones

En el siguiente tutorial aprenderás sobre **formateo de texto** y cómo hacer tus mensajes más atractivos. 