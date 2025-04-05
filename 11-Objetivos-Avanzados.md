---
icon: octicons/tasklist-16
tags:
- Advanced Objectives
---

En el tutorial anterior aprendiste sobre NPCs y diálogos. Este tutorial trata sobre objetivos avanzados.
Los objetivos son tareas que el jugador debe completar para avanzar en una quest.
¡Aprenderás cómo crear objetivos más complejos y desafiantes!

<div class="grid" markdown>
!!! danger "Requisitos"
    * [Tutorial de Objetivos](04-Fundamentos-Objetivos.md)
    * [Tutorial de Condiciones](06-Fundamentos-Condiciones.md)
    * [Tutorial de Variables](07-Fundamentos-Variables.md)

!!! example "Documentación Relacionada"
    * [Lista de Objetivos](../../../Documentation/Scripting/Building-Blocks/Objectives-List.md)
</div>

## 1. Objetivos Múltiples

Puedes crear objetivos que requieran múltiples condiciones:

``` YAML title="objectives.yml" linenums="1"
objectives:
  complexMining:
    type: multi
    objectives:
      - type: item
        item: diamond
        amount: 5
      - type: item
        item: emerald
        amount: 3
      - type: location
        location: "100;70;100;world"
        radius: 5
    notify: "&a¡Has completado %amount%/%total% objetivos!"
    cancel: "&c¡Has perdido progreso en tus objetivos!"
    events:
      - giveReward
```

## 2. Objetivos con Temporizador

Puedes crear objetivos con límite de tiempo:

``` YAML title="objectives.yml" linenums="1"
objectives:
  timedHunt:
    type: kill
    mob: zombie
    amount: 10
    time: 300 # 5 minutos en segundos
    notify: "&a¡Has matado %amount%/%total% zombies! &eTiempo restante: %time%"
    cancel: "&c¡Se acabó el tiempo!"
    events:
      - giveReward
```

## 3. Objetivos con Progreso

Puedes crear objetivos que muestren el progreso:

``` YAML title="objectives.yml" linenums="1"
objectives:
  miningProgress:
    type: item
    item: diamond
    amount: 10
    notify: "&a¡Has recolectado %amount%/%total% diamantes!"
    cancel: "&c¡Has perdido algunos diamantes!"
    events:
      - updateProgress
      - checkCompletion
```

## 4. Objetivos con Condiciones

Puedes usar condiciones para modificar objetivos:

``` YAML title="objectives.yml" linenums="1"
objectives:
  conditionalHunt:
    type: kill
    mob: zombie
    amount: 10
    condition: hasSword
    notify: "&a¡Has matado %amount%/%total% zombies!"
    cancel: "&c¡Necesitas una espada para esta quest!"
    events:
      - giveReward
```

## 5. Objetivos con Eventos

Puedes disparar eventos durante el progreso:

``` YAML title="objectives.yml" linenums="1"
objectives:
  eventfulMining:
    type: item
    item: diamond
    amount: 5
    notify: "&a¡Has recolectado %amount%/%total% diamantes!"
    events:
      - updateProgress
      - checkHalfway
      - checkCompletion
```

## 6. Mejores Prácticas

Algunas recomendaciones para crear objetivos:

* Balancea la dificultad
* Usa notificaciones claras
* Integra eventos para feedback
* Usa condiciones para variabilidad
* Mantén los objetivos interesantes
* Proporciona recompensas adecuadas

## 7. Ejemplos Prácticos

Aquí hay algunos ejemplos de objetivos complejos:

``` YAML title="objectives.yml" linenums="1"
objectives:
  epicQuest:
    type: multi
    objectives:
      - type: item
        item: diamond
        amount: 5
        notify: "&a¡Has recolectado %amount%/%total% diamantes!"
      - type: kill
        mob: dragon
        amount: 1
        notify: "&a¡Has derrotado al dragón!"
      - type: location
        location: "0;70;0;world"
        radius: 10
        notify: "&a¡Has llegado al punto de encuentro!"
    events:
      - giveEpicReward
      - unlockNewArea
      - startNextQuest

  timedChallenge:
    type: multi
    time: 600 # 10 minutos
    objectives:
      - type: item
        item: emerald
        amount: 3
      - type: kill
        mob: skeleton
        amount: 5
      - type: location
        location: "50;70;50;world"
        radius: 5
    notify: "&a¡Has completado %amount%/%total% objetivos! &eTiempo restante: %time%"
    cancel: "&c¡Se acabó el tiempo!"
    events:
      - giveTimeReward
```

## Resumen

Has aprendido cómo:
* Crear objetivos múltiples
* Usar temporizadores
* Mostrar progreso
* Aplicar condiciones
* Integrar eventos
* Seguir las mejores prácticas

En el siguiente tutorial aprenderás sobre **eventos avanzados** y cómo crear interacciones más complejas. 