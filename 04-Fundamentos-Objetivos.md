---
icon: octicons/codescan-checkmark-16
tags:
- Objectives
---

En el tutorial anterior aprendiste a crear y usar eventos. 
Este tutorial trata sobre los objetivos. Los objetivos son tareas que puedes asignar a un jugador. Por ejemplo, romper bloques o
pescar peces. ¡Las posibilidades son casi infinitas! Aprenderás sobre esto en este tutorial.

<div class="grid" markdown>
!!! danger "Requisitos"
    * [Tutorial de Conversaciones](03-Fundamentos-Conversaciones.md)
    * [Tutorial de Eventos](05-Fundamentos-Eventos.md)

!!! example "Documentación Relacionada"
    * [Referencia de Objetivos](../../../Documentation/Scripting/About-Scripting.md#objectives)
    * [Lista de Objetivos](../../../Documentation/Scripting/Building-Blocks/Objectives-List.md)
</div>

## 1. Creando la estructura de carpetas para tu primer objetivo

Añade un nuevo archivo a tu `QuestPackage` "_tutorialQuest_" llamado "_objectives.yml_" y 
un nuevo archivo a tu carpeta de Conversaciones "_tutorialQuest_" llamado "_blacksmith.yml_".
Te preguntarás por qué añadimos un nuevo archivo a la carpeta de conversaciones. Esto es porque el tour de la ciudad actualmente termina en nada. 
Vamos a añadir un NPC herrero con el que el jugador pueda hablar.

Aquí está una visión general de cómo debería verse tu estructura de directorios ahora:

* :material-folder-open: tutorialQuest
    - :material-file: package.yml
    - :material-file: events.yml
    - :material-file: {==objectives.yml==}
    - :material-folder-open: conversations
        - :material-file: jack.yml
        - :material-file: {==blacksmith.yml==}

## 2. Definiendo tu primer objetivo y evento de finalización

Abre el archivo recién creado "_objectives.yml_" y añade lo siguiente:

``` YAML title="objectives.yml" linenums="1"
objectives: # (1)!
  fishingObj: "fish cod 3 notify hookLocation:100;63;100;world range:20 events:caughtAllFish"
```

1. Todos los objetivos deben definirse en una sección `objectives`.

Explicación:

* `fishingObj` es el nombre del objetivo. Puedes elegir cualquier nombre que quieras. Sin embargo, se recomienda nombrarlo
  según lo que hace. Esto hace que sea más fácil entender tu quest.
  * La Instrucción del Objetivo.
    - `fish`: El primer valor en la instrucción es siempre el **tipo de objetivo**.
    - `cod`: Esta es una **opción** del objetivo `fish`. Define qué ítem debes pescar.
    - `3`: Esta es otra **opción**. Define la cantidad a pescar.
    - `notify`: Este es un argumento general para la mayoría de los objetivos. Habilita una notificación cuando el jugador progresa en el objetivo.
    - `hookLocation:100;63;100;world`: Esta **opción** define dónde debe estar ubicado el anzuelo de la caña de pescar. Solo los peces pescados
       en esta área específica son contados por el objetivo. ¡Debes ajustar esto a tu mundo!
    - `range:20`: Si usas la ubicación del anzuelo también debes definir la **opción** range. Este es el rango alrededor de la coordenada de ubicación del anzuelo
       donde los peces pescados aún son contados.
    - `events:caughtAllFish`: Este no es una opción del objetivo fish sino un argumento general de objetivo. El evento definido
       se activa una vez que se completa el objetivo (después de pescar 3 bacalaos en la ubicación del anzuelo especificada).

Después de esto, añadimos el evento `caughtAllFish` al archivo "_events.yml_" así:

``` YAML title="events.yml" hl_lines="4" linenums="1"
events:
  # Otros eventos no mostrados aquí
  tpBlacksmith: "teleport 50;70;50;world"
  caughtAllFish: "notify ¡Has pescado suficientes peces!\n¡Regresa al herrero! io:Title sound:firework_rocket"
```

Esto le permite al jugador saber que completó exitosamente el objetivo.

## 3. Creando el ítem en la sección de ítems

Como aprendimos en el [tutorial anterior](05-Fundamentos-Eventos.md#3-creando-el-ítem-en-la-sección-de-ítems) tenemos que definir `cod` en
la sección de ítems porque BetonQuest no sabe qué es `cod`.
Para añadir el ítem a la lista, volvamos a abrir el archivo "_package.yml_".

``` YAML title="package.yml" hl_lines="6" linenums="1"
npcs:
  '1': "Jack"

items:
  steak: "COOKED_BEEF"
  cod: "COD" # (1)!
```

1. Vincula el nombre del ítem `cod` de tus configuraciones de BetonQuest al ítem del juego `minecraft:COD`.

Ahora, `cod` es un ítem definido que puede ser utilizado en toda la quest.

## 4. Probando tu primer objetivo en el juego

!!! warning ""
    ¡Es muy importante guardar todos los archivos cada vez que pruebas algo!
    Escribe `/bq reload` en tu servidor después de guardar.

Los objetivos deben iniciarse antes de que empiecen a vigilar las acciones del jugador.
La forma más fácil de hacer esto es ejecutando un comando:

Escribe `/bq objective TU_NOMBRE add tutorialQuest.fishObj` en el servidor.
Este comando iniciará el objetivo para el jugador.
Si quieres verificar si lo has hecho correctamente, ve a la ubicación definida y pesca 3 bacalaos. Después de pescar 3 bacalaos
deberías recibir una notificación.

## 5. Usando eventos para iniciar objetivos

Los objetivos no solo pueden iniciarse y detenerse usando comandos, sino también con eventos.
Añadamos un evento para iniciar el objetivo de pesca:

``` YAML title="events.yml" hl_lines="5" linenums="1"
events:
  # Otros eventos no mostrados aquí
  tpBlacksmith: "teleport 50;70;50;world"
  caughtAllFish: "notify ¡Has pescado suficientes peces!\n¡Regresa al herrero! io:Title sound:firework_rocket"
  startFishingObj: "objective start fishingObj" # (1)!
```

1. Inicia el objetivo `fishingObj` para el jugador en el que se ejecuta este evento.

## 6. Integrando objetivos en conversaciones

Como sabes, podemos ejecutar eventos desde conversaciones. Ahora podemos usar el nuevo evento para iniciar un objetivo desde una conversación.

Añadamos algo de diálogo al archivo recién creado llamado "_blacksmith.yml_" en la carpeta de conversaciones:

``` YAML title="blacksmith.yml" linenums="1" 
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
        pointer: accept,deny # (1)!
      maybeLater:
        text: ¡No hay problema! También puedes volver más tarde. ¡Adiós!
      goodLuck:
        text: ¡Buena suerte y te veré más tarde!
    player_options:
      thatsRight:
        text: Sí, es verdad. ¡Gracias!
        pointer: newArmorForNewCitizens
      whatToDo:
        text: ¿Qué puedo hacer por ti?
        pointer: collectFish
      accept:
        text: ¡Por supuesto! Me vendría bien una nueva armadura.
        event: startFishingObj # (2)!
        pointer: goodLuck
      deny:
        text: No tengo tiempo ahora mismo.
        pointer: maybeLater
```

1. El jugador tiene la opción de decir sí o no.
2. Este es el evento para iniciar tu tarea real de objetivo de pescar 3 bacalaos frescos.

Ahora vincula la conversación a un nuevo NPC que esté colocado donde termine el tour de la ciudad. Ya deberías saber cómo vincular
el diálogo al NPC en "_package.yml_". Si no, [¡revisa los tutoriales anteriores](03-Fundamentos-Conversaciones.md#1-vinculando-una-conversación-a-un-npc)!

## Resumen

Has aprendido qué son los objetivos y cómo crearlos. Ahora puedes darle a un jugador un 
objetivo para tener una quest más avanzada! Más objetivos se pueden encontrar en la [lista de objetivos](../../../Documentation/Scripting/Building-Blocks/Objectives-List.md).
En el siguiente tutorial aprenderás cómo funcionan las **condiciones** y cómo usarlas para hacer que el Herrero reaccione al objetivo completado. 