---
icon: octicons/book-16
---

# Ejemplo de Quest: TreeShelter

Este tutorial te guiará paso a paso en la creación de una quest simple pero completa usando BetonQuest.

## Descripción de la Quest

En esta quest, el jugador debe:
1. Hablar con un NPC
2. Recolectar madera
3. Construir un refugio
4. Recibir una recompensa

## Estructura de Archivos

```
plugins/BetonQuest/
└── quests/
    └── TreeShelter/
        ├── conversations.yml
        ├── events.yml
        ├── objectives.yml
        └── conditions.yml
```

## Paso 1: Configuración Inicial

### conversations.yml
```yaml
quester: TreeShelter
first: "Hola, necesito tu ayuda. ¿Podrías construirme un refugio?"
options:
  - text: "Por supuesto, ¿qué necesito?"
    pointer: accept_quest
  - text: "Lo siento, estoy ocupado."
    pointer: reject_quest
```

### events.yml
```yaml
accept_quest: "objective start collect_wood"
reject_quest: "cancel"
quest_complete: "give diamond 1"
```

### objectives.yml
```yaml
collect_wood: "block OAK_LOG -10 events:quest_complete"
```

### conditions.yml
```yaml
has_wood: "item OAK_LOG 10"
```

## Paso 2: Desarrollo de la Quest

1. El jugador habla con el NPC
2. Si acepta, recibe el objetivo de recolectar madera
3. Al recolectar 10 troncos, recibe un diamante
4. La quest se completa

## Elementos Avanzados

- Uso de condiciones para verificar el inventario
- Sistema de recompensas
- Objetivos de recolección
- Diálogos interactivos

## Mejores Prácticas

1. Mantén los archivos organizados
2. Usa nombres descriptivos
3. Comenta tu código
4. Prueba cada paso
5. Verifica las condiciones

## Extensión de la Quest

Puedes expandir esta quest añadiendo:
- Más objetivos
- Diferentes tipos de madera
- Recompensas variables
- Diálogos adicionales 