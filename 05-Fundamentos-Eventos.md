---
icon: octicons/play-16
tags:
- Events
---

En el tutorial anterior aprendiste a crear conversaciones. 
Este tutorial trata sobre eventos. Los eventos son acciones que ocurren en momentos específicos. Por ejemplo, dar ítems al jugador o
teleportarlo a una ubicación. ¡Las posibilidades son casi infinitas! Aprenderás sobre esto en este tutorial.

<div class="grid" markdown>
!!! danger "Requisitos"
    * [Tutorial de Conversaciones](03-Fundamentos-Conversaciones.md)

!!! example "Documentación Relacionada"
    * [Referencia de Eventos](../../../Documentation/Scripting/About-Scripting.md#events)
    * [Lista de Eventos](../../../Documentation/Scripting/Building-Blocks/Events-List.md)
</div>

## 1. Creando la estructura de carpetas para tu primer evento

Añade un nuevo archivo a tu `QuestPackage` "_tutorialQuest_" llamado "_events.yml_".
Aquí está una visión general de cómo debería verse tu estructura de directorios ahora:

* :material-folder-open: tutorialQuest
    - :material-file: package.yml
    - :material-file: {==events.yml==}
    - :material-folder-open: conversations
        - :material-file: jack.yml

## 2. Definiendo tu primer evento

Abre el archivo recién creado "_events.yml_" y añade lo siguiente:

``` YAML title="events.yml" linenums="1"
events: # (1)!
  giveSteak: "give steak 1" # (2)!
```

1. Todos los eventos deben definirse en una sección `events`.
2. `giveSteak` es el nombre del evento. Puedes elegir cualquier nombre que quieras. Sin embargo, se recomienda nombrarlo
   según lo que hace. Esto hace que sea más fácil entender tu quest.

## 3. Creando el ítem en la sección de ítems

Antes de que podamos dar un bistec al jugador, tenemos que definir qué es un bistec en BetonQuest.
Para hacer esto, abre el archivo "_package.yml_" y añade una sección de ítems:

``` YAML title="package.yml" hl_lines="4" linenums="1"
npcs:
  '1': "Jack"

items: # (1)!
  steak: "COOKED_BEEF" # (2)!
```

1. Todos los ítems deben definirse en una sección `items`.
2. `steak` es el nombre del ítem que usaremos en BetonQuest. `COOKED_BEEF` es el nombre del ítem en Minecraft.

## 4. Probando tu primer evento en el juego

!!! warning ""
    ¡Es muy importante guardar todos los archivos cada vez que pruebas algo!
    Escribe `/bq reload` en tu servidor después de guardar.

Para probar el evento, necesitamos ejecutarlo. La forma más fácil de hacer esto es con un comando:

Escribe `/bq event TU_NOMBRE tutorialQuest.giveSteak` en el servidor.
Este comando ejecutará el evento para el jugador.

| Parte del Comando | Significado |
|-------------------|-------------|
| `/bq event` | Le dice a BetonQuest que debe ejecutar un evento. |
| `NOMBRE` | El nombre de un jugador. |
| `tutorialQuest` | El nombre de un QuestPackage. Esto es necesario porque podrías tener eventos con el mismo nombre en diferentes paquetes. |
| `giveSteak` | El nombre del evento a ejecutar. No olvides separarlo con un punto del paquete `tutorialQuest{==.==}giveSteak`. |

## 5. Usando eventos en conversaciones

Ahora que sabemos cómo crear y ejecutar eventos, podemos usarlos en conversaciones.
Vamos a modificar la conversación con Jack para que dé un bistec al jugador:

``` YAML title="jack.yml" hl_lines="12" linenums="1"
conversations:
  Jack:
    quester: Jack
    first: firstGreeting
    NPC_options:
      firstGreeting:
        text: ¡Hola y bienvenido a mi ciudad viajero! Me alegro de verte. ¿De dónde eres?
        pointer: whereYouFrom
      whoAmI:
        text: Soy &6Jack&r. El alcalde de esta hermosa ciudad. ¡Tenemos algunas granjas grandes y buenas tabernas que vale la pena visitar! Entonces, ¿de dónde eres?
        pointer: smallIsland,bigCity
      islandAnswer:
        text: ¡Eso suena familiar! Crecí en un pequeño pueblo con pocas personas. ¡Así que ya tenemos algo en común! ¿Quieres algo de comer?
        pointer: yesPlease
      cityAnswer:
        text: ¡Oh, lo sé! Creo que eres de Kayra, ¿verdad? Bonita ciudad pero para ser honesto prefiero la vida en el campo... Pareces un poco hambriento. ¿Quieres algo de comer?
        pointer: yesPlease
      foodAnswer:
        text: ¡De nada! Tómalo... &7*da comida*
        event: giveSteak # (1)!
    player_options:
      whereYouFrom:
        text: Primero quiero saber quién eres tú.
        pointer: whoAmI
      smallIsland:
        text: De una pequeña isla ubicada al este.
        pointer: islandAnswer
      bigCity:
        text: De una gran ciudad ubicada al oeste.
        pointer: cityAnswer
      yesPlease:
        text: ¡Oh sí, estoy hambriento! Gracias.
        pointer: foodAnswer
```

1. Este evento se ejecutará cuando el jugador llegue a esta opción de diálogo.

## Resumen

Has aprendido qué son los eventos y cómo crearlos. Ahora puedes hacer que sucedan cosas cuando el jugador
elige ciertas opciones en una conversación! Más eventos se pueden encontrar en la [lista de eventos](../../../Documentation/Scripting/Building-Blocks/Events-List.md).
En el siguiente tutorial aprenderás sobre **objetivos** y cómo usarlos para darle al jugador tareas que completar. 