---
icon: octicons/lightning-bolt-16
tags:
- Advanced Events
---

En el tutorial anterior aprendiste sobre objetivos avanzados. Este tutorial trata sobre eventos avanzados.
Los eventos son acciones que ocurren en respuesta a ciertas condiciones o triggers.
¡Aprenderás cómo crear eventos más complejos y poderosos!

<div class="grid" markdown>
!!! danger "Requisitos"
    * [Tutorial de Eventos](05-Fundamentos-Eventos.md)
    * [Tutorial de Variables](07-Fundamentos-Variables.md)
    * [Tutorial de Condiciones](06-Fundamentos-Condiciones.md)

!!! example "Documentación Relacionada"
    * [Lista de Eventos](../../../Documentation/Scripting/Building-Blocks/Events-List.md)
</div>

## 1. Eventos Múltiples

Puedes crear eventos que ejecuten múltiples acciones:

``` YAML title="events.yml" linenums="1"
events:
  complexReward: |
    give diamond_sword{display:'Espada del Héroe',lore:['Una espada legendaria'],enchantments:{sharpness:5}} 1
    give golden_apple{display:'Manzana de la Vida',lore:['Cura todas las heridas']} 5
    give diamond{display:'Diamante Mágico',lore:['Un diamante con poderes místicos']} 10
    variable questCompleted set true
    notify "&a¡Has completado la quest!\n&e¡Aquí están tus recompensas!"
    sound firework_rocket
```

## 2. Eventos con Condiciones

Puedes usar condiciones para modificar eventos:

``` YAML title="events.yml" linenums="1"
events:
  conditionalReward: |
    condition hasSword
    give diamond 5
    notify "&a¡Has recibido 5 diamantes por tener una espada!"
    condition !hasSword
    give stone_sword{display:'Espada Básica',lore:['Una espada para empezar']} 1
    notify "&a¡Has recibido una espada básica!"
```

## 3. Eventos con Variables

Puedes usar variables para hacer eventos dinámicos:

``` YAML title="events.yml" linenums="1"
events:
  dynamicReward: |
    variable rewardAmount add 1
    give diamond %rewardAmount%
    notify "&a¡Has recibido %rewardAmount% diamantes!"
    variable questProgress add 1
    notify "&eProgreso de la quest: %questProgress%"
```

## 4. Eventos con Temporizadores

Puedes crear eventos con retrasos:

``` YAML title="events.yml" linenums="1"
events:
  delayedEvent: |
    delay 5
    notify "&a¡Han pasado 5 segundos!"
    delay 10
    give diamond 1
    notify "&a¡Has recibido un diamante después de 15 segundos!"
```

## 5. Eventos con Efectos

Puedes añadir efectos visuales y sonoros:

``` YAML title="events.yml" linenums="1"
events:
  epicEvent: |
    effect lightning
    sound firework_rocket
    effect explosion
    notify "&6¡Un evento épico ha ocurrido!"
    delay 2
    effect ender_teleport
    sound dragon_growl
```

## 6. Mejores Prácticas

Algunas recomendaciones para crear eventos:

* Mantén los eventos organizados
* Usa nombres descriptivos
* Combina eventos de manera lógica
* Proporciona feedback al jugador
* Balancea las recompensas
* Usa efectos con moderación

## 7. Ejemplos Prácticos

Aquí hay algunos ejemplos de eventos complejos:

``` YAML title="events.yml" linenums="1"
events:
  epicQuestComplete: |
    # Efectos visuales y sonoros
    effect lightning
    sound firework_rocket
    effect explosion
    delay 2
    effect ender_teleport
    sound dragon_growl
    
    # Recompensas
    give diamond_sword{display:'Espada del Dragón',lore:['Una espada legendaria','Forjada en las llamas del dragón'],enchantments:{sharpness:5,unbreaking:3,fire_aspect:2}} 1
    give golden_apple{display:'Manzana de la Vida',lore:['Cura todas las heridas']} 5
    give diamond{display:'Diamante Mágico',lore:['Un diamante con poderes místicos']} 10
    give emerald{display:'Esmeralda del Sabio',lore:['Contiene la sabiduría de los antiguos']} 5
    
    # Variables y progreso
    variable questCompleted set true
    variable epicQuestsCompleted add 1
    
    # Notificaciones
    notify "&6=== &e¡Quest Épica Completada! &6==="
    notify "&a¡Has completado %epicQuestsCompleted% quests épicas!"
    notify "&e¡Aquí están tus recompensas legendarias!"
    
    # Desbloqueo de contenido
    delay 5
    notify "&6¡Has desbloqueado una nueva área!"
    event unlockNewArea
    
    # Inicio de siguiente quest
    delay 10
    notify "&e¡Una nueva aventura te espera!"
    event startNextQuest

  timedChallenge: |
    # Inicio del desafío
    notify "&6=== &e¡Desafío Iniciado! &6==="
    notify "&eTienes 10 minutos para completar los objetivos!"
    
    # Variables iniciales
    variable challengeStarted set true
    variable challengeTime set 600
    
    # Efectos de inicio
    effect lightning
    sound firework_rocket
    
    # Temporizador
    delay 600
    condition challengeStarted
    notify "&c¡Se acabó el tiempo!"
    event challengeFailed
```

## Resumen

Has aprendido cómo:
* Crear eventos múltiples
* Usar condiciones en eventos
* Integrar variables
* Añadir temporizadores
* Usar efectos visuales y sonoros
* Seguir las mejores prácticas

En el siguiente tutorial aprenderás sobre **condiciones avanzadas** y cómo crear lógica más compleja en tus quests. 