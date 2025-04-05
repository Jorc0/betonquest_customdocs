---
icon: octicons/speed-16
tags:
- Optimization
- Performance
---

En el tutorial anterior aprendiste sobre integración con plugins. Este tutorial trata sobre optimización y rendimiento.
El rendimiento es crucial para mantener un servidor estable y una experiencia fluida para los jugadores.
¡Aprenderás cómo hacer tus quests más eficientes!

<div class="grid" markdown>
!!! danger "Requisitos"
    * [Tutorial de Eventos](05-Fundamentos-Eventos.md)
    * [Tutorial de Variables](07-Fundamentos-Variables.md)
    * [Tutorial de Condiciones](06-Fundamentos-Condiciones.md)

!!! example "Documentación Relacionada"
    * [Guía de Optimización](../../../Documentation/Features/Optimization.md)
</div>

## 1. Optimización de Variables

Las variables pueden afectar el rendimiento si se usan incorrectamente:

``` YAML title="package.yml" linenums="1"
package: tutorialQuest
variables:
  # Buenas prácticas
  playerLevel: 0 # (1)!
  questProgress: 0 # (2)!
  
  # Malas prácticas
  playerPosition: "%player%.location" # (3)!
  playerInventory: "%player%.inventory" # (4)!
```

1. Variables simples y eficientes
2. Variables con propósito claro
3. Variables que se actualizan constantemente
4. Variables que almacenan datos complejos

## 2. Optimización de Eventos

Los eventos deben ser eficientes y bien organizados:

``` YAML title="events.yml" linenums="1"
events:
  # Buenas prácticas
  simpleEvent: "give diamond 1" # (1)!
  organizedEvent: |
    # Dar recompensa
    give diamond 1
    # Actualizar progreso
    variable questProgress add 1
    # Notificar al jugador
    notify "&a¡Has recibido un diamante!"
  
  # Malas prácticas
  complexEvent: |
    # Demasiadas acciones en un solo evento
    give diamond 1
    give emerald 1
    give gold_ingot 1
    give iron_ingot 1
    give coal 1
    give redstone 1
    give lapis_lazuli 1
    give quartz 1
    variable questProgress add 1
    variable playerLevel add 1
    variable experience add 100
    notify "&a¡Has recibido muchos items!"
    sound firework_rocket
    effect lightning
    effect explosion
```

## 3. Optimización de Condiciones

Las condiciones deben ser simples y eficientes:

``` YAML title="conditions.yml" linenums="1"
conditions:
  # Buenas prácticas
  simpleCondition: "item diamond 1" # (1)!
  organizedCondition: "item diamond 1;item emerald 1" # (2)!
  
  # Malas prácticas
  complexCondition: "item diamond 1;item emerald 1;item gold_ingot 1;item iron_ingot 1;item coal 1;item redstone 1;item lapis_lazuli 1;item quartz 1" # (3)!
```

1. Condiciones simples y directas
2. Condiciones organizadas y claras
3. Condiciones demasiado complejas

## 4. Optimización de Conversaciones

Las conversaciones deben ser eficientes y bien estructuradas:

``` YAML title="conversations.yml" linenums="1"
conversations:
  Blacksmith:
    quester: Blacksmith
    first: greeting
    NPC_options:
      # Buenas prácticas
      greeting:
        text: "&6¡Bienvenido!"
        pointer: mainMenu
      mainMenu:
        text: "¿En qué puedo ayudarte?"
        pointer: quest,shop
      
      # Malas prácticas
      longGreeting:
        text: "&6=== &e¡Bienvenido a la Forja del Herrero Legendario! &6===\n&7Hola &f%player%&7, ¿en qué puedo ayudarte hoy?\n&7Tenemos muchas opciones disponibles para ti.\n&7Puedes ver nuestras quests, comprar items, o simplemente charlar.\n&7¿Qué te gustaría hacer?"
        pointer: manyOptions
```

## 5. Mejores Prácticas

Algunas recomendaciones para optimizar el rendimiento:

* Usa variables simples y con propósito
* Mantén los eventos concisos y organizados
* Evita condiciones demasiado complejas
* Estructura las conversaciones de manera clara
* Minimiza el uso de efectos y sonidos
* Limpia variables y datos no utilizados
* Usa nombres descriptivos y consistentes
* Documenta el código para facilitar el mantenimiento

## 6. Ejemplos de Optimización

Aquí hay algunos ejemplos de cómo optimizar el código:

``` YAML title="events.yml" linenums="1"
events:
  # Antes de optimizar
  complexQuestComplete: |
    give diamond_sword{display:'Espada del Dragón',lore:['Una espada legendaria','Forjada en las llamas del dragón'],enchantments:{sharpness:5,unbreaking:3,fire_aspect:2}} 1
    give golden_apple{display:'Manzana de la Vida',lore:['Cura todas las heridas']} 5
    give diamond{display:'Diamante Mágico',lore:['Un diamante con poderes místicos']} 10
    give emerald{display:'Esmeralda del Sabio',lore:['Contiene la sabiduría de los antiguos']} 5
    variable questCompleted set true
    variable epicQuestsCompleted add 1
    notify "&6=== &e¡Quest Épica Completada! &6==="
    notify "&a¡Has completado %epicQuestsCompleted% quests épicas!"
    notify "&e¡Aquí están tus recompensas legendarias!"
    effect lightning
    sound firework_rocket
    effect explosion
    delay 2
    effect ender_teleport
    sound dragon_growl

  # Después de optimizar
  optimizedQuestComplete: |
    # Recompensas
    give diamond_sword{display:'Espada del Dragón',lore:['Una espada legendaria'],enchantments:{sharpness:5}} 1
    give golden_apple 5
    give diamond 10
    give emerald 5
    
    # Progreso
    variable questCompleted set true
    variable epicQuestsCompleted add 1
    
    # Notificación
    notify "&6=== &e¡Quest Completada! &6===\n&aRecompensas recibidas!"
    
    # Efecto final
    effect lightning
    sound firework_rocket
```

## Resumen

Has aprendido cómo:
* Optimizar variables
* Mejorar eventos
* Simplificar condiciones
* Estructurar conversaciones
* Seguir las mejores prácticas
* Optimizar el código existente

En el siguiente tutorial aprenderás sobre **depuración y solución de problemas** y cómo resolver errores comunes. 