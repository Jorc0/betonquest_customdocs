---
icon: octicons/git-branch-16
tags:
- Advanced Conditions
---

En el tutorial anterior aprendiste sobre eventos avanzados. Este tutorial trata sobre condiciones avanzadas.
Las condiciones son reglas que determinan cuándo ocurren ciertas acciones.
¡Aprenderás cómo crear condiciones más complejas y sofisticadas!

<div class="grid" markdown>
!!! danger "Requisitos"
    * [Tutorial de Condiciones](06-Fundamentos-Condiciones.md)
    * [Tutorial de Variables](07-Fundamentos-Variables.md)
    * [Tutorial de Eventos](05-Fundamentos-Eventos.md)

!!! example "Documentación Relacionada"
    * [Lista de Condiciones](../../../Documentation/Scripting/Building-Blocks/Conditions-List.md)
</div>

## 1. Condiciones Múltiples

Puedes combinar múltiples condiciones:

``` YAML title="conditions.yml" linenums="1"
conditions:
  complexCondition: "item diamond_sword 1;item golden_apple 5;location 50;70;50;world;10" # (1)!
  orCondition: "item diamond 5|item emerald 10" # (2)!
  andCondition: "item diamond 5&item emerald 10" # (3)!
  notCondition: "!item diamond 5" # (4)!
```

1. Todas las condiciones deben cumplirse (usando `;`)
2. Al menos una condición debe cumplirse (usando `|`)
3. Todas las condiciones deben cumplirse (usando `&`)
4. La condición no debe cumplirse (usando `!`)

## 2. Condiciones con Variables

Puedes usar variables en condiciones:

``` YAML title="conditions.yml" linenums="1"
conditions:
  variableCondition: "variable questProgress >= 5" # (1)!
  variableRange: "variable playerLevel >= 10;variable playerLevel <= 20" # (2)!
  variableCompare: "variable diamondsCollected >= variable diamondsRequired" # (3)!
```

1. Verifica si la variable es mayor o igual a 5
2. Verifica si la variable está en un rango
3. Compara dos variables

## 3. Condiciones con Items

Puedes crear condiciones complejas con items:

``` YAML title="conditions.yml" linenums="1"
conditions:
  enchantedItem: "item diamond_sword{enchantments:{sharpness:5}} 1" # (1)!
  namedItem: "item diamond_sword{display:'Espada del Héroe'} 1" # (2)!
  complexItem: "item diamond_sword{display:'Espada del Dragón',lore:['Una espada legendaria'],enchantments:{sharpness:5,unbreaking:3}} 1" # (3)!
```

1. Verifica un item con encantamientos
2. Verifica un item con nombre personalizado
3. Verifica un item con múltiples atributos

## 4. Condiciones con Ubicación

Puedes crear condiciones basadas en ubicación:

``` YAML title="conditions.yml" linenums="1"
conditions:
  locationRange: "location 50;70;50;world;10" # (1)!
  multipleLocations: "location 50;70;50;world;10|location 100;70;100;world;10" # (2)!
  locationAndItem: "location 50;70;50;world;10&item diamond 5" # (3)!
```

1. Verifica si el jugador está en un rango de una ubicación
2. Verifica si el jugador está en cualquiera de varias ubicaciones
3. Combina condiciones de ubicación con items

## 5. Condiciones con Temporizadores

Puedes crear condiciones basadas en tiempo:

``` YAML title="conditions.yml" linenums="1"
conditions:
  timeOfDay: "time 6000;12000" # (1)!
  timeAndLocation: "time 6000;12000&location 50;70;50;world;10" # (2)!
  timeOrItem: "time 6000;12000|item diamond 5" # (3)!
```

1. Verifica si es de día (entre 6000 y 12000 ticks)
2. Combina condiciones de tiempo con ubicación
3. Combina condiciones de tiempo con items

## 6. Mejores Prácticas

Algunas recomendaciones para crear condiciones:

* Mantén las condiciones organizadas
* Usa nombres descriptivos
* Combina condiciones de manera lógica
* Evita condiciones demasiado complejas
* Documenta condiciones importantes
* Prueba todas las combinaciones posibles

## 7. Ejemplos Prácticos

Aquí hay algunos ejemplos de condiciones complejas:

``` YAML title="conditions.yml" linenums="1"
conditions:
  epicQuestAvailable: |
    # Verifica requisitos básicos
    variable playerLevel >= 20
    variable questsCompleted >= 10
    
    # Verifica equipo necesario
    item diamond_sword{enchantments:{sharpness:5}} 1
    item golden_apple 5
    
    # Verifica ubicación y tiempo
    location 50;70;50;world;10
    time 6000;12000
    
    # Verifica que no haya quests activas
    !variable hasActiveQuest

  bossFightReady: |
    # Verifica equipo completo
    item diamond_helmet{enchantments:{protection:4}} 1
    item diamond_chestplate{enchantments:{protection:4}} 1
    item diamond_leggings{enchantments:{protection:4}} 1
    item diamond_boots{enchantments:{protection:4}} 1
    item diamond_sword{enchantments:{sharpness:5,unbreaking:3}} 1
    
    # Verifica consumibles
    item golden_apple 10
    item ender_pearl 16
    
    # Verifica nivel y experiencia
    variable playerLevel >= 30
    variable bossKills >= 5
    
    # Verifica ubicación correcta
    location 0;70;0;world;5
```

## Resumen

Has aprendido cómo:
* Crear condiciones múltiples
* Usar variables en condiciones
* Crear condiciones con items
* Usar condiciones de ubicación
* Implementar temporizadores
* Seguir las mejores prácticas

En el siguiente tutorial aprenderás sobre **integración con plugins** y cómo extender la funcionalidad de BetonQuest. 