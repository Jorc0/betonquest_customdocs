---
icon: octicons/people-16
tags:
- NPCs
- Dialogues
---

En el tutorial anterior aprendiste sobre items y recompensas. Este tutorial trata sobre NPCs y diálogos.
Los NPCs son personajes no jugables que pueden interactuar con el jugador a través de conversaciones.
¡Aprenderás cómo crear NPCs interesantes y diálogos dinámicos!

<div class="grid" markdown>
!!! danger "Requisitos"
    * [Tutorial de Conversaciones](03-Fundamentos-Conversaciones.md)
    * [Tutorial de Condiciones](06-Fundamentos-Condiciones.md)
    * [Tutorial de Variables](07-Fundamentos-Variables.md)

!!! example "Documentación Relacionada"
    * [Referencia de NPCs](../../../Documentation/Features/Npcs.md)
</div>

## 1. Creando NPCs

Los NPCs se definen en el archivo `package.yml`:

``` YAML title="package.yml" linenums="1"
package: tutorialQuest
npcs:
  Blacksmith:
    name: "&6Herrero"
    skin: "steve"
    location: "50;70;50;world"
    conversation: "Blacksmith"
    visible: true
    walking: true
    walkingRadius: 5
```

## 2. Diálogos Básicos

Los diálogos se definen en archivos YAML separados:

``` YAML title="conversations/blacksmith.yml" linenums="1"
conversations:
  Blacksmith:
    quester: Blacksmith
    first: greeting
    NPC_options:
      greeting:
        text: "&6¡Bienvenido a mi forja, %player%!"
        pointer: askHelp
      askHelp:
        text: "¿En qué puedo ayudarte hoy?"
        pointer: questStart,shop
      questStart:
        text: "Necesito que me ayudes a recolectar algunos minerales."
        pointer: accept,decline
      shop:
        text: "¿Quieres ver mis productos?"
        pointer: showItems
    player_options:
      accept:
        text: "Por supuesto, me encantaría ayudarte."
        event: startMiningQuest
        pointer: questAccepted
      decline:
        text: "Lo siento, estoy ocupado."
        pointer: maybeLater
      questAccepted:
        text: "¡Excelente! Aquí tienes tu equipo."
        event: giveMiningEquipment
```

## 3. Diálogos Condicionales

Puedes usar condiciones para mostrar diferentes diálogos:

``` YAML title="conversations/blacksmith.yml" linenums="1"
conversations:
  Blacksmith:
    quester: Blacksmith
    first: greeting
    NPC_options:
      greeting:
        text: "&6¡Bienvenido de nuevo, %player%!"
        condition: hasCompletedTutorial
        pointer: welcomeBack
      greeting:
        text: "&6¡Bienvenido a mi forja, %player%!"
        pointer: firstTime
      welcomeBack:
        text: "¿Listo para una nueva aventura?"
        pointer: newQuest
      firstTime:
        text: "Es la primera vez que te veo por aquí."
        pointer: tutorial
```

## 4. Diálogos con Variables

Puedes usar variables para hacer los diálogos más dinámicos:

``` YAML title="conversations/blacksmith.yml" linenums="1"
conversations:
  Blacksmith:
    quester: Blacksmith
    first: greeting
    NPC_options:
      greeting:
        text: "&6¡Hola %player%! Has completado %questsCompleted% quests."
        pointer: questStatus
      questStatus:
        text: "Tu progreso actual es: %questProgress%"
        condition: hasActiveQuest
        pointer: continueQuest
```

## 5. Diálogos con Eventos

Puedes disparar eventos durante los diálogos:

``` YAML title="conversations/blacksmith.yml" linenums="1"
conversations:
  Blacksmith:
    quester: Blacksmith
    first: greeting
    NPC_options:
      greeting:
        text: "&6¡Bienvenido a mi forja!"
        event: checkQuestProgress
        pointer: questStatus
      questStatus:
        text: "Has recolectado %diamondsCollected%/%diamondsRequired% diamantes."
        condition: hasActiveQuest
        pointer: continueQuest,completeQuest
    player_options:
      completeQuest:
        text: "He recolectado todos los diamantes."
        condition: hasEnoughDiamonds
        event: completeMiningQuest
        pointer: questComplete
```

## 6. Mejores Prácticas

Algunas recomendaciones para crear NPCs y diálogos:

* Da personalidad a tus NPCs
* Usa nombres y descripciones descriptivos
* Mantén los diálogos concisos pero informativos
* Usa condiciones para crear ramas de diálogo
* Integra eventos y variables para hacer los diálogos dinámicos
* Usa formateo de texto para mejorar la legibilidad

## 7. Ejemplos Prácticos

Aquí hay un ejemplo completo de un NPC con diálogos complejos:

``` YAML title="conversations/blacksmith.yml" linenums="1"
conversations:
  Blacksmith:
    quester: Blacksmith
    first: greeting
    NPC_options:
      greeting:
        text: "&6=== &eBienvenido a la Forja &6===\n&7Hola &f%player%&7, ¿en qué puedo ayudarte hoy?"
        pointer: mainMenu
      mainMenu:
        text: "Puedo ayudarte con:\n&e1. &7Quests\n&e2. &7Comprar items\n&e3. &7Reparar equipo"
        pointer: questMenu,shopMenu,repairMenu
      questMenu:
        text: "Tengo varias quests disponibles:"
        condition: hasAvailableQuests
        pointer: miningQuest,huntingQuest
      shopMenu:
        text: "Estos son mis productos:"
        pointer: showWeapons,showArmor,showTools
      repairMenu:
        text: "¿Qué equipo necesitas reparar?"
        pointer: repairWeapon,repairArmor
    player_options:
      miningQuest:
        text: "¿Tienes alguna quest de minería?"
        condition: hasMiningQuest
        pointer: miningQuestStatus
      huntingQuest:
        text: "¿Tienes alguna quest de caza?"
        condition: hasHuntingQuest
        pointer: huntingQuestStatus
```

## Resumen

Has aprendido cómo:
* Crear NPCs con personalidad
* Diseñar diálogos básicos y complejos
* Usar condiciones en diálogos
* Integrar variables y eventos
* Seguir las mejores prácticas

En el siguiente tutorial aprenderás sobre **objetivos avanzados** y cómo crear quests más complejas. 