---
icon: octicons/light-bulb-16
tags:
- Best Practices
- Tips
---

En el tutorial anterior aprendiste sobre depuración y solución de problemas. Este tutorial trata sobre mejores prácticas y consejos para crear quests profesionales.
Es importante seguir ciertas pautas para crear quests de alta calidad y fáciles de mantener.
¡Aprenderás cómo crear quests profesionales!

<div class="grid" markdown>
!!! danger "Requisitos"
    * [Tutorial de Eventos](05-Fundamentos-Eventos.md)
    * [Tutorial de Variables](07-Fundamentos-Variables.md)
    * [Tutorial de Condiciones](06-Fundamentos-Condiciones.md)
    * [Tutorial de Depuración](16-Depuracion-Solucion-Problemas.md)

!!! example "Documentación Relacionada"
    * [Guía de Mejores Prácticas](../../../Documentation/Features/BestPractices.md)
</div>

## 1. Estructura de Archivos

Una buena estructura de archivos es fundamental:

``` YAML title="package.yml" linenums="1"
package: tutorialQuest
# Usar nombres descriptivos
# Mantener una estructura clara
# Documentar el propósito del paquete
variables:
  playerLevel: 0
  questProgress: 0
```

## 2. Nomenclatura

Usa nombres claros y descriptivos:

``` YAML title="naming.yml" linenums="1"
# Malos nombres
events:
  e1: "give diamond 1"
  e2: "give iron 1"

# Buenos nombres
events:
  giveDiamondReward: "give diamond 1"
  giveIronReward: "give iron 1"
```

## 3. Organización de Conversaciones

Organiza las conversaciones de manera lógica:

``` YAML title="conversations.yml" linenums="1"
conversations:
  Blacksmith:
    quester: Blacksmith
    first: greeting
    NPC_options:
      greeting:
        text: "¡Bienvenido a mi herrería!"
        pointer: mainMenu
      mainMenu:
        text: "¿En qué puedo ayudarte?"
        pointer: quest,shop,bye
      quest:
        text: "Tengo una tarea para ti"
        pointer: questAccept,questDecline
      shop:
        text: "Veamos qué tengo para vender"
        pointer: buyItems
      bye:
        text: "¡Hasta luego!"
        pointer: end
```

## 4. Gestión de Variables

Usa variables de manera eficiente:

``` YAML title="variables.yml" linenums="1"
variables:
  # Variables de progreso
  questProgress: 0
  playerLevel: 0
  
  # Variables de estado
  hasAcceptedQuest: false
  hasCompletedQuest: false
  
  # Variables de recompensa
  rewardAmount: 100
  rewardItem: diamond
```

## 5. Mejores Prácticas para Eventos

Crea eventos claros y eficientes:

``` YAML title="events.yml" linenums="1"
events:
  startQuest: |
    # Inicio de quest
    variable questProgress set 1
    variable hasAcceptedQuest set true
    notify "&a¡Has aceptado la quest!"
    
  completeQuest: |
    # Completar quest
    variable questProgress set 100
    variable hasCompletedQuest set true
    give %rewardItem% %rewardAmount%
    notify "&a¡Has completado la quest!"
```

## 6. Mejores Prácticas para Condiciones

Usa condiciones de manera efectiva:

``` YAML title="conditions.yml" linenums="1"
conditions:
  # Condiciones de progreso
  questStarted: "variable questProgress 1"
  questCompleted: "variable questProgress 100"
  
  # Condiciones de estado
  hasAccepted: "variable hasAcceptedQuest true"
  hasCompleted: "variable hasCompletedQuest true"
  
  # Condiciones de items
  hasRequiredItems: "item diamond 1,iron 5"
```

## 7. Consejos Generales

Algunos consejos importantes:

* Mantén el código organizado y documentado
* Usa nombres descriptivos
* Sigue una estructura consistente
* Prueba exhaustivamente
* Optimiza el rendimiento
* Mantén las quests simples al principio
* Documenta los cambios
* Usa control de versiones

## 8. Ejemplos de Mejores Prácticas

Aquí hay algunos ejemplos de buenas prácticas:

``` YAML title="best_practices.yml" linenums="1"
# 1. Quest bien estructurada
package: tutorialQuest
variables:
  questStage: 0
  hasStarted: false
  hasCompleted: false
  rewardAmount: 100

events:
  startQuest: |
    # Inicio
    variable questStage set 1
    variable hasStarted set true
    notify "&a¡Has comenzado la quest!"
    
  progressQuest: |
    # Progreso
    variable questStage add 1
    notify "&a¡Has progresado en la quest!"
    
  completeQuest: |
    # Completar
    variable questStage set 100
    variable hasCompleted set true
    give diamond %rewardAmount%
    notify "&a¡Has completado la quest!"

conditions:
  canStart: "variable hasStarted false"
  canProgress: "variable questStage 1"
  canComplete: "variable questStage 5"
```

## Resumen

Has aprendido:
* Cómo estructurar archivos
* Buenas prácticas de nomenclatura
* Organización de conversaciones
* Gestión de variables
* Mejores prácticas para eventos
* Mejores prácticas para condiciones
* Consejos generales

En el siguiente tutorial aprenderás sobre **integración con otros plugins** para expandir las funcionalidades de tus quests. 