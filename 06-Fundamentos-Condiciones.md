---
icon: octicons/check-circle-16
tags:
- Conditions
---

En el tutorial anterior aprendiste a crear y usar objetivos. 
Este tutorial trata sobre condiciones. Las condiciones son reglas que determinan cuándo ocurren ciertas acciones. Por ejemplo, verificar si el jugador tiene un ítem o
si está en una ubicación específica. ¡Las posibilidades son casi infinitas! Aprenderás sobre esto en este tutorial.

<div class="grid" markdown>
!!! danger "Requisitos"
    * [Tutorial de Conversaciones](03-Fundamentos-Conversaciones.md)
    * [Tutorial de Eventos](05-Fundamentos-Eventos.md)
    * [Tutorial de Objetivos](04-Fundamentos-Objetivos.md)

!!! example "Documentación Relacionada"
    * [Referencia de Condiciones](../../../Documentation/Scripting/About-Scripting.md#conditions)
    * [Lista de Condiciones](../../../Documentation/Scripting/Building-Blocks/Conditions-List.md)
</div>

## 1. Creando la estructura de carpetas para tu primera condición

Añade un nuevo archivo a tu `QuestPackage` "_tutorialQuest_" llamado "_conditions.yml_".
Aquí está una visión general de cómo debería verse tu estructura de directorios ahora:

* :material-folder-open: tutorialQuest
    - :material-file: package.yml
    - :material-file: events.yml
    - :material-file: objectives.yml
    - :material-file: {==conditions.yml==}
    - :material-folder-open: conversations
        - :material-file: jack.yml
        - :material-file: blacksmith.yml

## 2. Definiendo tu primera condición

Abre el archivo recién creado "_conditions.yml_" y añade lo siguiente:

``` YAML title="conditions.yml" linenums="1"
conditions: # (1)!
  hasFish: "item cod 3" # (2)!
```

1. Todas las condiciones deben definirse en una sección `conditions`.
2. `hasFish` es el nombre de la condición. Puedes elegir cualquier nombre que quieras. Sin embargo, se recomienda nombrarlo
   según lo que hace. Esto hace que sea más fácil entender tu quest.

## 3. Usando condiciones en conversaciones

Ahora que sabemos cómo crear condiciones, podemos usarlas en conversaciones.
Vamos a modificar la conversación con el Herrero para que solo dé la armadura si el jugador tiene los peces:

``` YAML title="blacksmith.yml" hl_lines="12" linenums="1"
conversations:
  Blacksmith:
    quester: Blacksmith
    first: firstGreeting
    NPC_options:
      firstGreeting:
        text: ¡Bienvenido %player% a Valencia! El alcalde ya me dijo que eres nuevo en nuestra ciudad.
        pointer: thatsRight
      newArmorForNewCitizens:
        text: ¡Así que cada nuevo ciudadano en nuestra ciudad recibirá una nueva armadura de mi parte, pero tienes que hacer algo por mí para obtener esta mejora realmente agradable!
        pointer: whatToDo
      collectFish:
        text: Tendrás que pescar 3 bacalaos frescos para mí y traérmelos. ¡Después de eso te daré la nueva armadura! ¿Es un trato?
        pointer: accept,deny
      maybeLater:
        text: ¡No hay problema! También puedes volver más tarde. ¡Adiós!
      goodLuck:
        text: ¡Buena suerte y te veré más tarde!
      giveArmor:
        text: ¡Excelente trabajo! Aquí está tu nueva armadura.
        event: giveArmor
        condition: hasFish # (1)!
      noFish:
        text: Parece que aún no tienes los bacalaos que te pedí. ¡Vuelve cuando los tengas!
    player_options:
      thatsRight:
        text: Sí, es verdad. ¡Gracias!
        pointer: newArmorForNewCitizens
      whatToDo:
        text: ¿Qué puedo hacer por ti?
        pointer: collectFish
      accept:
        text: ¡Por supuesto! Me vendría bien una nueva armadura.
        event: startFishingObj
        pointer: goodLuck
      deny:
        text: No tengo tiempo ahora mismo.
        pointer: maybeLater
      returnWithFish:
        text: ¡He pescado los bacalaos que me pediste!
        pointer: giveArmor,noFish # (2)!
```

1. Esta condición se verificará cuando el jugador llegue a esta opción de diálogo.
2. Si la condición `hasFish` es verdadera, el jugador verá la opción `giveArmor`. Si es falsa, verá la opción `noFish`.

## 4. Añadiendo el evento para dar la armadura

Ahora necesitamos añadir el evento `giveArmor` al archivo "_events.yml_":

``` YAML title="events.yml" hl_lines="5" linenums="1"
events:
  # Otros eventos no mostrados aquí
  tpBlacksmith: "teleport 50;70;50;world"
  caughtAllFish: "notify ¡Has pescado suficientes peces!\n¡Regresa al herrero! io:Title sound:firework_rocket"
  startFishingObj: "objective start fishingObj"
  giveArmor: "give diamond_chestplate 1" # (1)!
```

1. Este evento dará al jugador una peto de diamante.

## 5. Probando las condiciones en el juego

!!! warning ""
    ¡Es muy importante guardar todos los archivos cada vez que pruebas algo!
    Escribe `/bq reload` en tu servidor después de guardar.

Para probar las condiciones, necesitamos:
1. Iniciar el objetivo de pesca
2. Pescar 3 bacalaos
3. Volver al Herrero y decirle que tenemos los peces

Si todo está configurado correctamente, el Herrero debería darte una peto de diamante.

## Resumen

Has aprendido qué son las condiciones y cómo crearlas. Ahora puedes hacer que los NPCs reaccionen de manera diferente
dependiendo de lo que tenga el jugador! Más condiciones se pueden encontrar en la [lista de condiciones](../../../Documentation/Scripting/Building-Blocks/Conditions-List.md).
En el siguiente tutorial aprenderás sobre **variables** y cómo usarlas para almacenar información sobre el jugador. 