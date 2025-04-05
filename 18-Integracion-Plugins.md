---
icon: octicons/plug-16
tags:
- Plugin Integration
- Extensions
---

En el tutorial anterior aprendiste sobre mejores prácticas y consejos. Este tutorial trata sobre la integración con otros plugins.
Es importante saber cómo expandir las funcionalidades de BetonQuest usando otros plugins.
¡Aprenderás cómo integrar diferentes plugins!

<div class="grid" markdown>
!!! danger "Requisitos"
    * [Tutorial de Eventos](05-Fundamentos-Eventos.md)
    * [Tutorial de Variables](07-Fundamentos-Variables.md)
    * [Tutorial de Condiciones](06-Fundamentos-Condiciones.md)
    * [Tutorial de Mejores Prácticas](17-Mejores-Practicas-Consejos.md)

!!! example "Documentación Relacionada"
    * [Lista de Plugins Compatibles](../../../Documentation/Features/CompatiblePlugins.md)
</div>

## 1. Integración con Vault

Vault permite integrar economía y permisos:

``` YAML title="vault_integration.yml" linenums="1"
# Comandos de economía
events:
  giveMoney: "money give %player% 100"
  takeMoney: "money take %player% 50"
  checkMoney: "money check %player%"

# Comandos de permisos
conditions:
  hasPermission: "permission essentials.home"
  isAdmin: "permission betonquest.admin"
```

## 2. Integración con PlaceholderAPI

PlaceholderAPI permite usar placeholders en diálogos:

``` YAML title="placeholder_integration.yml" linenums="1"
conversations:
  Blacksmith:
    quester: Blacksmith
    first: greeting
    NPC_options:
      greeting:
        text: "¡Hola %player_name%! Tu nivel es %player_level%"
        pointer: mainMenu
      mainMenu:
        text: "Tienes %vault_eco_balance% monedas"
        pointer: quest,shop
```

## 3. Integración con WorldEdit

WorldEdit permite manipular el mundo:

``` YAML title="worldedit_integration.yml" linenums="1"
events:
  pasteStructure: "paste schematic house"
  clearArea: "clear 10"
  setBlock: "setblock stone"
```

## 4. Integración con WorldGuard

WorldGuard permite gestionar regiones:

``` YAML title="worldguard_integration.yml" linenums="1"
conditions:
  inRegion: "region spawn"
  canBuild: "region build"

events:
  createRegion: "region create house"
  removeRegion: "region remove house"
```

## 5. Integración con Citizens

Citizens permite gestionar NPCs:

``` YAML title="citizens_integration.yml" linenums="1"
events:
  spawnNPC: "spawnnpc Blacksmith"
  removeNPC: "removenpc Blacksmith"
  teleportNPC: "tpnpc Blacksmith 100 64 100 world"

conditions:
  npcExists: "npc Blacksmith"
  npcNearby: "npcrange Blacksmith 10"
```

## 6. Mejores Prácticas

Algunas recomendaciones para la integración:

* Verifica la compatibilidad de versiones
* Usa nombres descriptivos
* Documenta las dependencias
* Maneja errores adecuadamente
* Prueba la integración
* Mantén el código organizado

## 7. Ejemplos de Integración

Aquí hay algunos ejemplos de integración:

``` YAML title="integration_examples.yml" linenums="1"
# 1. Quest con múltiples plugins
package: tutorialQuest
variables:
  questStage: 0
  rewardAmount: 100

events:
  startQuest: |
    # Inicio
    variable questStage set 1
    notify "&a¡Has comenzado la quest!"
    
    # Dar dinero
    money give %player% 50
    
    # Crear región
    region create questArea
    
    # Spawnear NPC
    spawnnpc QuestGiver
    
  completeQuest: |
    # Completar
    variable questStage set 100
    
    # Dar recompensa
    money give %player% %rewardAmount%
    
    # Remover región
    region remove questArea
    
    # Remover NPC
    removenpc QuestGiver

conditions:
  canStart: "money check %player% 0"
  canComplete: "region questArea"
```

## Resumen

Has aprendido:
* Integración con Vault
* Integración con PlaceholderAPI
* Integración con WorldEdit
* Integración con WorldGuard
* Integración con Citizens
* Mejores prácticas
* Ejemplos de integración

En el siguiente tutorial aprenderás sobre **optimización y rendimiento** para mejorar el funcionamiento de tus quests. 