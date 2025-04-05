---
icon: octicons/plug-16
tags:
- Plugin Integration
---

En el tutorial anterior aprendiste sobre condiciones avanzadas. Este tutorial trata sobre la integración con otros plugins.
BetonQuest puede trabajar con varios plugins populares para añadir funcionalidad adicional.
¡Aprenderás cómo extender tus quests con características de otros plugins!

<div class="grid" markdown>
!!! danger "Requisitos"
    * [Tutorial de Eventos](05-Fundamentos-Eventos.md)
    * [Tutorial de Condiciones](06-Fundamentos-Condiciones.md)
    * [Tutorial de Variables](07-Fundamentos-Variables.md)

!!! example "Documentación Relacionada"
    * [Lista de Plugins Compatibles](../../../Documentation/Features/Plugin-Integration.md)
</div>

## 1. Integración con Vault

Vault permite integrar economía y permisos:

``` YAML title="events.yml" linenums="1"
events:
  giveMoney: "money add 1000" # (1)!
  takeMoney: "money take 500" # (2)!
  checkBalance: "money check 1000" # (3)!
```

``` YAML title="conditions.yml" linenums="1"
conditions:
  hasMoney: "money 1000" # (1)!
  hasPermission: "permission essentials.home" # (2)!
```

1. Dar dinero al jugador
2. Quitar dinero al jugador
3. Verificar si tiene suficiente dinero
4. Verificar si tiene un permiso

## 2. Integración con PlaceholderAPI

Puedes usar placeholders en tus mensajes:

``` YAML title="conversations.yml" linenums="1"
conversations:
  Blacksmith:
    quester: Blacksmith
    first: greeting
    NPC_options:
      greeting:
        text: "&6¡Hola %player%! Tu nivel es %player_level% y tienes %player_money% monedas."
        pointer: questStart
```

## 3. Integración con WorldEdit

Puedes usar WorldEdit para crear estructuras:

``` YAML title="events.yml" linenums="1"
events:
  spawnStructure: "worldedit paste structure1" # (1)!
  clearArea: "worldedit clear 10" # (2)!
```

1. Pegar una estructura guardada
2. Limpiar un área

## 4. Integración con WorldGuard

Puedes proteger áreas y verificar regiones:

``` YAML title="conditions.yml" linenums="1"
conditions:
  inRegion: "region spawn" # (1)!
  canBuild: "region build" # (2)!
```

``` YAML title="events.yml" linenums="1"
events:
  setRegion: "region add player_%player% 10" # (1)!
  removeRegion: "region remove player_%player%" # (2)!
```

1. Verificar si está en una región
2. Verificar si puede construir
3. Crear una región para el jugador
4. Eliminar una región

## 5. Integración con Citizens

Puedes controlar NPCs de Citizens:

``` YAML title="events.yml" linenums="1"
events:
  spawnNPC: "citizens spawn 1" # (1)!
  removeNPC: "citizens remove 1" # (2)!
  walkTo: "citizens walk 1 50;70;50;world" # (3)!
```

``` YAML title="conditions.yml" linenums="1"
conditions:
  npcExists: "citizens 1" # (1)!
  npcNearby: "citizens distance 1 10" # (2)!
```

1. Spawnear un NPC
2. Eliminar un NPC
3. Hacer que un NPC camine
4. Verificar si existe un NPC
5. Verificar si un NPC está cerca

## 6. Mejores Prácticas

Algunas recomendaciones para la integración con plugins:

* Verifica la compatibilidad de versiones
* Usa nombres descriptivos para regiones y NPCs
* Maneja errores y casos extremos
* Documenta las dependencias
* Prueba todas las integraciones
* Mantén las configuraciones organizadas

## 7. Ejemplos Prácticos

Aquí hay algunos ejemplos de integración compleja:

``` YAML title="events.yml" linenums="1"
events:
  startEpicQuest: |
    # Configuración de región
    region add quest_area_%player% 20
    region flag quest_area_%player% pvp deny
    
    # Spawn de NPCs
    citizens spawn 1
    citizens spawn 2
    citizens walk 1 50;70;50;world
    citizens walk 2 51;70;51;world
    
    # Configuración de economía
    money take 1000
    variable questStarted set true
    
    # Notificaciones
    notify "&6=== &e¡Quest Épica Iniciada! &6==="
    notify "&aSe ha creado una zona segura para tu quest"
    notify "&eCosto de entrada: 1000 monedas"

  completeEpicQuest: |
    # Limpieza de región
    region remove quest_area_%player%
    
    # Eliminación de NPCs
    citizens remove 1
    citizens remove 2
    
    # Recompensas
    money add 5000
    give diamond_sword{display:'Espada del Héroe'} 1
    
    # Notificaciones
    notify "&6=== &e¡Quest Épica Completada! &6==="
    notify "&a¡Has ganado 5000 monedas y una espada legendaria!"
```

## Resumen

Has aprendido cómo:
* Integrar Vault para economía y permisos
* Usar PlaceholderAPI para mensajes dinámicos
* Trabajar con WorldEdit para estructuras
* Proteger áreas con WorldGuard
* Controlar NPCs con Citizens
* Seguir las mejores prácticas

En el siguiente tutorial aprenderás sobre **optimización y rendimiento** y cómo hacer tus quests más eficientes. 