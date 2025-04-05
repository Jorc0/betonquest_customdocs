---
icon: octicons/comment-discussion-16
---

# Fundamentos de Conversaciones

Las conversaciones son el corazón de la interacción entre NPCs y jugadores en BetonQuest. Este documento cubre todo lo que necesitas saber para crear conversaciones efectivas.

## Estructura Básica

### Archivo de Conversación
```yaml
quester: NPCName
first: "Primer mensaje del NPC"
options:
  - text: "Respuesta del jugador"
    pointer: siguiente_dialogo
```

## Elementos Principales

### 1. Mensajes del NPC
- Texto simple
- Texto con formato
- Texto con variables
- Texto con condiciones

### 2. Opciones del Jugador
- Texto de la opción
- Puntero al siguiente diálogo
- Condiciones para mostrar la opción
- Eventos al seleccionar la opción

### 3. Punteros
- Referencias a otros diálogos
- Eventos
- Condiciones
- Objetivos

## Ejemplos Prácticos

### Conversación Simple
```yaml
quester: Mercader
first: "¡Bienvenido a mi tienda!"
options:
  - text: "¿Qué tienes para vender?"
    pointer: mostrar_items
  - text: "Adiós"
    pointer: despedida
```

### Conversación con Condiciones
```yaml
quester: Guardia
first: "¡Alto! ¿Tienes un permiso?"
options:
  - text: "Sí, aquí está"
    pointer: verificar_permiso
    condition: tiene_permiso
  - text: "No, lo siento"
    pointer: negar_acceso
```

## Características Avanzadas

### 1. Variables en Diálogos
```yaml
first: "Tienes %point.reputation.amount% puntos de reputación"
```

### 2. Formato de Texto
```yaml
first: "&6¡Bienvenido! &eEste es un mensaje formateado"
```

### 3. Diálogos Condicionales
```yaml
first: "Hola"
condition: es_noche
```

## Mejores Prácticas

1. **Organización**
   - Mantén las conversaciones organizadas
   - Usa nombres descriptivos
   - Comenta tu código

2. **Estructura**
   - Divide las conversaciones largas
   - Usa punteros para navegación
   - Mantén la coherencia

3. **Interactividad**
   - Ofrece múltiples opciones
   - Usa condiciones para opciones dinámicas
   - Incluye eventos para acciones

4. **Mantenimiento**
   - Verifica la sintaxis YAML
   - Prueba todas las ramas
   - Documenta cambios

## Integración con Otros Sistemas

### 1. Objetivos
```yaml
options:
  - text: "Aceptar quest"
    pointer: aceptar_quest
    event: start_quest
```

### 2. Eventos
```yaml
options:
  - text: "Recibir recompensa"
    pointer: recompensa
    event: give_reward
```

### 3. Condiciones
```yaml
options:
  - text: "Opción especial"
    pointer: especial
    condition: tiene_item_especial
```

## Solución de Problemas

1. **Errores Comunes**
   - Sintaxis YAML incorrecta
   - Punteros inexistentes
   - Condiciones mal formadas

2. **Depuración**
   - Usa /q reload
   - Verifica la consola
   - Prueba cada rama

3. **Optimización**
   - Minimiza el uso de condiciones
   - Organiza las conversaciones
   - Usa eventos eficientemente 