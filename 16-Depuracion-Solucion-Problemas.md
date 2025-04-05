---
icon: octicons/bug-16
tags:
- Debugging
- Troubleshooting
---

En el tutorial anterior aprendiste sobre optimización y rendimiento. Este tutorial trata sobre depuración y solución de problemas.
Es importante saber cómo identificar y resolver errores comunes en BetonQuest.
¡Aprenderás cómo depurar tus quests y solucionar problemas!

<div class="grid" markdown>
!!! danger "Requisitos"
    * [Tutorial de Eventos](05-Fundamentos-Eventos.md)
    * [Tutorial de Variables](07-Fundamentos-Variables.md)
    * [Tutorial de Condiciones](06-Fundamentos-Condiciones.md)

!!! example "Documentación Relacionada"
    * [Guía de Depuración](../../../Documentation/Features/Debugging.md)
</div>

## 1. Comandos de Depuración

BetonQuest proporciona varios comandos para depuración:

``` YAML title="commands.yml" linenums="1"
# Comandos básicos
/bq reload # Recargar todas las quests
/bq save # Guardar el estado actual
/bq cancel # Cancelar una quest
/bq list # Listar quests activas

# Comandos de depuración
/bq debug # Activar modo depuración
/bq debug off # Desactivar modo depuración
/bq variable # Ver variables
/bq variable clear # Limpiar variables
/bq journal # Ver diario de quests
```

## 2. Errores Comunes

Aquí hay algunos errores comunes y cómo solucionarlos:

``` YAML title="common_errors.yml" linenums="1"
# 1. Error de sintaxis YAML
events:
  wrongEvent: "give diamond 1" # Falta espacio después de los dos puntos
  correctEvent: "give diamond 1" # Correcto

# 2. Error de referencia
conversations:
  Blacksmith:
    quester: Blacksmith
    first: greeting
    NPC_options:
      greeting:
        text: "¡Hola!"
        pointer: nonexistentOption # Error: opción no existe
        pointer: validOption # Correcto

# 3. Error de variable
conditions:
  wrongCondition: "variable nonexistentVar" # Error: variable no existe
  correctCondition: "variable existingVar" # Correcto
```

## 3. Verificación de Archivos

Es importante verificar la estructura de los archivos:

``` YAML title="package.yml" linenums="1"
package: tutorialQuest
# Verificar que el nombre del paquete coincida en todos los archivos
variables:
  playerLevel: 0
  questProgress: 0
```

``` YAML title="conversations.yml" linenums="1"
conversations:
  Blacksmith:
    quester: Blacksmith # Verificar que el quester exista
    first: greeting # Verificar que la opción exista
```

## 4. Depuración de Eventos

Para depurar eventos:

``` YAML title="events.yml" linenums="1"
events:
  debugEvent: |
    # Añadir notificaciones de depuración
    notify "&e[DEBUG] Iniciando evento"
    give diamond 1
    notify "&e[DEBUG] Item dado"
    variable questProgress add 1
    notify "&e[DEBUG] Variable actualizada"
    notify "&e[DEBUG] Evento completado"
```

## 5. Depuración de Condiciones

Para depurar condiciones:

``` YAML title="conditions.yml" linenums="1"
conditions:
  debugCondition: |
    # Usar condiciones simples para depuración
    item diamond 1
    notify "&e[DEBUG] Condición verificada"
```

## 6. Mejores Prácticas

Algunas recomendaciones para la depuración:

* Usa el modo depuración cuando sea necesario
* Verifica la sintaxis YAML
* Comprueba las referencias a eventos y condiciones
* Usa notificaciones de depuración
* Mantén un registro de cambios
* Prueba cada parte por separado
* Documenta los problemas y soluciones

## 7. Ejemplos de Depuración

Aquí hay algunos ejemplos de cómo depurar problemas comunes:

``` YAML title="debug_examples.yml" linenums="1"
# 1. Depuración de eventos complejos
events:
  debugComplexEvent: |
    # Inicio del evento
    notify "&e[DEBUG] Iniciando evento complejo"
    
    # Verificar variables
    notify "&e[DEBUG] Variable questProgress: %questProgress%"
    
    # Dar items
    give diamond 1
    notify "&e[DEBUG] Item dado"
    
    # Actualizar variables
    variable questProgress add 1
    notify "&e[DEBUG] Variable actualizada: %questProgress%"
    
    # Verificar condiciones
    condition hasDiamond
    notify "&e[DEBUG] Condición verificada"
    
    # Finalizar evento
    notify "&e[DEBUG] Evento completado"

# 2. Depuración de conversaciones
conversations:
  Blacksmith:
    quester: Blacksmith
    first: greeting
    NPC_options:
      greeting:
        text: "&e[DEBUG] Iniciando conversación"
        event: debugConversation
        pointer: mainMenu
      mainMenu:
        text: "&e[DEBUG] Mostrando menú principal"
        pointer: quest,shop
```

## Resumen

Has aprendido cómo:
* Usar comandos de depuración
* Identificar errores comunes
* Verificar archivos
* Depurar eventos
* Depurar condiciones
* Seguir las mejores prácticas

En el siguiente tutorial aprenderás sobre **mejores prácticas y consejos** para crear quests profesionales. 