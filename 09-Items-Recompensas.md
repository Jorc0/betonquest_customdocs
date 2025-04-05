---
icon: octicons/gift-16
tags:
- Items
- Rewards
---

En el tutorial anterior aprendiste sobre formateo de texto. Este tutorial trata sobre items y recompensas.
Los items son una parte fundamental de las quests, ya que pueden ser objetivos, recompensas o herramientas necesarias.
¡Aprenderás cómo manejar items de manera efectiva en tus quests!

<div class="grid" markdown>
!!! danger "Requisitos"
    * [Tutorial de Conversaciones](03-Fundamentos-Conversaciones.md)
    * [Tutorial de Eventos](05-Fundamentos-Eventos.md)
    * [Tutorial de Condiciones](06-Fundamentos-Condiciones.md)

!!! example "Documentación Relacionada"
    * [Referencia de Items](../../../Documentation/Features/Items.md)
</div>

## 1. Dar Items al Jugador

Hay varias formas de dar items al jugador:

``` YAML title="events.yml" linenums="1"
events:
  giveBasicItems: "give diamond_sword 1\ngive golden_apple 5" # (1)!
  giveNamedItem: "give diamond_sword{display:'Espada del Héroe',lore:['Una espada legendaria']} 1" # (2)!
  giveEnchantedItem: "give diamond_sword{enchantments:{sharpness:5,unbreaking:3}} 1" # (3)!
```

1. Dar items básicos
2. Dar un item con nombre y descripción personalizada
3. Dar un item con encantamientos

## 2. Quitar Items al Jugador

Puedes quitar items del inventario del jugador:

``` YAML title="events.yml" linenums="1"
events:
  removeItems: "take diamond 5" # (1)!
  removeSpecificItem: "take diamond_sword{display:'Espada del Héroe'} 1" # (2)!
```

1. Quitar 5 diamantes
2. Quitar un item específico con nombre personalizado

## 3. Verificar Items

Puedes verificar si el jugador tiene ciertos items:

``` YAML title="conditions.yml" linenums="1"
conditions:
  hasDiamond: "item diamond 1" # (1)!
  hasEnchantedSword: "item diamond_sword{enchantments:{sharpness:5}} 1" # (2)!
  hasEnoughEmeralds: "item emerald 10" # (3)!
```

1. Verificar si tiene al menos 1 diamante
2. Verificar si tiene una espada con Sharpness V
3. Verificar si tiene al menos 10 esmeraldas

## 4. Recompensas Complejas

Puedes crear recompensas más complejas combinando diferentes tipos de items:

``` YAML title="events.yml" linenums="1"
events:
  giveQuestReward: |
    give diamond_sword{display:'Espada del Dragón',lore:['Una espada legendaria','Forjada en las llamas del dragón'],enchantments:{sharpness:5,unbreaking:3,fire_aspect:2}} 1
    give golden_apple{display:'Manzana de la Vida',lore:['Cura todas las heridas']} 5
    give diamond{display:'Diamante Mágico',lore:['Un diamante con poderes místicos']} 10
    give emerald{display:'Esmeralda del Sabio',lore:['Contiene la sabiduría de los antiguos']} 5
```

## 5. Items como Objetivos

Los items pueden ser parte de los objetivos de una quest:

``` YAML title="objectives.yml" linenums="1"
objectives:
  collectDiamonds:
    type: item
    item: diamond
    amount: 10
    notify: "&a¡Has recolectado %amount%/%total% diamantes!"
    cancel: "&c¡Has perdido algunos diamantes!"
    events:
      - giveReward
```

## 6. Mejores Prácticas

Algunas recomendaciones para manejar items:

* Usa nombres y descripciones descriptivos
* Balancea las recompensas según la dificultad
* Verifica siempre si el jugador tiene espacio en el inventario
* Usa encantamientos y atributos para hacer items únicos
* Mantén un registro de los items importantes

## 7. Ejemplos Prácticos

Aquí hay algunos ejemplos de cómo usar items en una quest:

``` YAML title="events.yml" linenums="1"
events:
  startMiningQuest: |
    give stone_pickaxe{display:'Pico del Minero',lore:['Un pico básico para empezar'],enchantments:{efficiency:2}} 1
    give torch 16
    notify "&a¡Has recibido tu equipo de minería!"

  giveMiningReward: |
    give diamond_pickaxe{display:'Pico del Maestro Minero',lore:['Un pico legendario','Forjado con la experiencia ganada'],enchantments:{efficiency:5,unbreaking:3,fortune:3}} 1
    give diamond{display:'Diamante del Minero',lore:['Un diamante especial']} 5
    give emerald{display:'Esmeralda del Minero',lore:['Una esmeralda especial']} 3
    notify "&6¡Has completado la quest de minería!\n&a¡Aquí están tus recompensas!"
```

## Resumen

Has aprendido cómo:
* Dar y quitar items
* Verificar posesión de items
* Crear recompensas complejas
* Usar items como objetivos
* Seguir las mejores prácticas

En el siguiente tutorial aprenderás sobre **NPCs y diálogos** y cómo crear conversaciones más dinámicas. 