---
icon: octicons/text-size-16
tags:
- Text Formatting
---

En el tutorial anterior aprendiste sobre variables. Este tutorial trata sobre formateo de texto.
El formateo de texto te permite hacer tus mensajes más atractivos y legibles usando colores, estilos y efectos especiales.
¡Aprenderás cómo hacer que tus quests se vean más profesionales!

<div class="grid" markdown>
!!! danger "Requisitos"
    * [Tutorial de Conversaciones](03-Fundamentos-Conversaciones.md)
    * [Tutorial de Variables](07-Fundamentos-Variables.md)

!!! example "Documentación Relacionada"
    * [Referencia de Formateo](../../../Documentation/Features/Message-Formatting.md)
</div>

## 1. Colores Básicos

BetonQuest soporta los siguientes colores básicos:

``` YAML title="conversations.yml" linenums="1"
conversations:
  Blacksmith:
    quester: Blacksmith
    first: firstGreeting
    NPC_options:
      firstGreeting:
        text: "&a¡Bienvenido! &eEste es un &6mensaje &ccolorido!" # (1)!
```

1. Los códigos de color comienzan con `&` seguido de un carácter:
   - `&a` = Verde claro
   - `&e` = Amarillo
   - `&6` = Dorado
   - `&c` = Rojo
   - `&b` = Azul claro
   - `&9` = Azul
   - `&d` = Rosa claro
   - `&5` = Púrpura
   - `&f` = Blanco
   - `&7` = Gris
   - `&8` = Gris oscuro
   - `&0` = Negro

## 2. Estilos de Texto

Puedes aplicar diferentes estilos al texto:

``` YAML title="conversations.yml" linenums="1"
conversations:
  Blacksmith:
    quester: Blacksmith
    first: firstGreeting
    NPC_options:
      firstGreeting:
        text: "&lTexto en negrita &nTexto subrayado &oTexto en cursiva" # (1)!
```

1. Los códigos de estilo son:
   - `&l` = Negrita
   - `&n` = Subrayado
   - `&o` = Cursiva
   - `&m` = Tachado
   - `&k` = Texto aleatorio
   - `&r` = Reiniciar formato

## 3. Variables con Formato

Puedes aplicar formato a las variables:

``` YAML title="conversations.yml" linenums="1"
conversations:
  Blacksmith:
    quester: Blacksmith
    first: firstGreeting
    NPC_options:
      firstGreeting:
        text: "&6%player% &eha completado &a%questProgress% &ede la quest!" # (1)!
```

1. Las variables mantienen el formato del color que les precede

## 4. Efectos Especiales

BetonQuest soporta efectos especiales en las notificaciones:

``` YAML title="events.yml" linenums="1"
events:
  questComplete: "notify &a¡Quest completada! &e¡Felicidades! io:Title sound:firework_rocket" # (1)!
  questFailed: "notify &c¡Quest fallida! &eInténtalo de nuevo. io:Title sound:entity_villager_no" # (2)!
```

1. Notificación con sonido de fuegos artificiales
2. Notificación con sonido de villager negando

## 5. Mejores Prácticas

Algunas recomendaciones para el formateo de texto:

* Usa colores consistentes para cada tipo de mensaje
* No abuses de los efectos especiales
* Mantén el texto legible
* Usa el formato para enfatizar información importante
* Combina colores y estilos de manera coherente

## 6. Ejemplos Prácticos

Aquí hay algunos ejemplos de cómo usar el formateo de texto:

``` YAML title="conversations.yml" linenums="1"
conversations:
  Blacksmith:
    quester: Blacksmith
    first: firstGreeting
    NPC_options:
      firstGreeting:
        text: "&6=== &eBienvenido a la Forja &6===\n&7Hola &f%player%&7, ¿en qué puedo ayudarte hoy?"
      questComplete:
        text: "&a=== &e¡Quest Completada! &a===\n&7Has ganado &6%diamonds% &7diamantes."
      questFailed:
        text: "&c=== &e¡Quest Fallida! &c===\n&7Vuelve a intentarlo más tarde."
```

## Resumen

Has aprendido cómo:
* Usar colores básicos
* Aplicar estilos de texto
* Formatear variables
* Usar efectos especiales
* Seguir las mejores prácticas

En el siguiente tutorial aprenderás sobre **items y recompensas** y cómo usarlos en tus quests. 