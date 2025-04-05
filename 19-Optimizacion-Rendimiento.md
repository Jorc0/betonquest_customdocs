---
icon: octicons/speed-16
tags:
- Optimization
- Performance
---

En el tutorial anterior aprendiste sobre integración con otros plugins. Este tutorial trata sobre optimización y rendimiento.
Es importante mantener un buen rendimiento para una experiencia fluida.
¡Aprenderás cómo optimizar tus quests!

<div class="grid" markdown>
!!! danger "Requisitos"
    * [Tutorial de Eventos](05-Fundamentos-Eventos.md)
    * [Tutorial de Variables](07-Fundamentos-Variables.md)
    * [Tutorial de Condiciones](06-Fundamentos-Condiciones.md)
    * [Tutorial de Integración](18-Integracion-Plugins.md)

!!! example "Documentación Relacionada"
    * [Guía de Optimización](../../../Documentation/Features/Optimization.md)
</div>

## 1. Optimización de Variables

Las variables pueden afectar el rendimiento:

``` YAML title="variables.yml" linenums="1"
# Mal uso
variables:
  playerLevel: 0
  playerXP: 0
  playerGold: 0
  playerItems: 0
  playerQuests: 0
  playerSkills: 0
  playerStats: 0
  playerAchievements: 0

# Buen uso
variables:
  playerLevel: 0
  playerXP: 0
  playerGold: 0
  # Usar variables solo cuando sea necesario
```

## 2. Optimización de Eventos

Los eventos deben ser eficientes:

``` YAML title="events.yml" linenums="1"
# Mal uso
events:
  complexEvent: |
    # Demasiadas operaciones
    variable questProgress add 1
    variable playerLevel add 1
    variable playerXP add 100
    variable playerGold add 50
    give diamond 1
    give iron 5
    give gold 10
    notify "&a¡Has progresado!"
    notify "&a¡Has subido de nivel!"
    notify "&a¡Has ganado XP!"
    notify "&a¡Has ganado oro!"
    notify "&a¡Has recibido items!"

# Buen uso
events:
  simpleEvent: |
    # Operaciones necesarias
    variable questProgress add 1
    give diamond 1
    notify "&a¡Has progresado en la quest!"
```

## 3. Optimización de Condiciones

Las condiciones deben ser simples:

``` YAML title="conditions.yml" linenums="1"
# Mal uso
conditions:
  complexCondition: "variable questProgress 1,variable playerLevel 5,variable playerXP 1000,variable playerGold 500,item diamond 1,item iron 5,item gold 10"

# Buen uso
conditions:
  simpleCondition: "variable questProgress 1"
  hasItems: "item diamond 1,iron 5"
```

## 4. Optimización de Conversaciones

Las conversaciones deben estar bien estructuradas:

``` YAML title="conversations.yml" linenums="1"
# Mal uso
conversations:
  Blacksmith:
    quester: Blacksmith
    first: greeting
    NPC_options:
      greeting:
        text: "¡Hola! ¿Qué quieres? ¿Comprar? ¿Vender? ¿Quest? ¿Información? ¿Ayuda? ¿Otra cosa?"
        pointer: buy,sell,quest,info,help,other

# Buen uso
conversations:
  Blacksmith:
    quester: Blacksmith
    first: greeting
    NPC_options:
      greeting:
        text: "¡Bienvenido! ¿En qué puedo ayudarte?"
        pointer: mainMenu
      mainMenu:
        text: "¿Qué te gustaría hacer?"
        pointer: buy,sell,quest
```

## 5. Mejores Prácticas

Algunas recomendaciones para optimizar:

* Usa variables solo cuando sea necesario
* Mantén los eventos simples
* Simplifica las condiciones
* Estructura bien las conversaciones
* Evita operaciones redundantes
* Usa nombres descriptivos
* Documenta el código
* Prueba el rendimiento

## 6. Ejemplos de Optimización

Aquí hay algunos ejemplos de optimización:

``` YAML title="optimization_examples.yml" linenums="1"
# 1. Quest optimizada
package: tutorialQuest
variables:
  questStage: 0
  rewardAmount: 100

events:
  startQuest: |
    # Inicio simple
    variable questStage set 1
    notify "&a¡Has comenzado la quest!"
    
  progressQuest: |
    # Progreso simple
    variable questStage add 1
    notify "&a¡Has progresado!"
    
  completeQuest: |
    # Completar simple
    variable questStage set 100
    give diamond %rewardAmount%
    notify "&a¡Has completado la quest!"

conditions:
  canStart: "variable questStage 0"
  canProgress: "variable questStage 1"
  canComplete: "variable questStage 5"
```

## Resumen

Has aprendido:
* Optimización de variables
* Optimización de eventos
* Optimización de condiciones
* Optimización de conversaciones
* Mejores prácticas
* Ejemplos de optimización

En el siguiente tutorial aprenderás sobre **depuración y solución de problemas** para resolver errores comunes. 