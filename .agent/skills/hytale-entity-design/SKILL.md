---
name: hytale-entity-design
description: Designs and implements Hytale entities with correct lifecycle, ownership, persistence, and server-authoritative behavior.
---

# Hytale Entity Design

This skill provides guidance on defining entities in Hytale using the Entity Component System (ECS), JSON Data Assets, and Java server plugins.

## When to use this skill

- Creating new NPC types, pets, or interactable objects.
- Defining entity behaviors, stats, and appearance.
- Managing entity lifecycle (spawn/despawn) and networking logic.

## Technical Context

Hytale entities are largely data-driven. A typical entity implementation involves:
1. **JSON Data Asset**: Defines the entity's base properties (model, textures, default components).
2. **Java Plugin (ECS)**: Implements custom logic through components and systems.
3. **Codecs**: Used for serializing and deserializing entity state.

## Implementation Patterns

### 1. Defining a Data-Driven Entity
Entities are registered via JSON files in the `data/assets/entities/` directory.

```json
{
  "id": "my_mod:example_entity",
  "model": "my_mod:example_model",
  "components": {
    "hytale:health": { "max": 20 },
    "hytale:physics": { "mass": 1.0 }
  }
}
```

### 2. Component Implementation (Java)
Custom behavior should be encapsulated in components.

```java
public class MyCustomComponent implements IComponent {
    // Define state fields here
    public int loyaltyLevel = 0;

    // Use Codecs for serialization
    public static final MapCodec<MyCustomComponent> CODEC = RecordCodecBuilder.mapCodec(inst -> inst.group(
        Codec.INT.fieldOf("loyaltyLevel").forGetter(c -> c.loyaltyLevel)
    ).apply(inst, MyCustomComponent::new));
}
```

### 3. Server-Authoritative Logic
Always implement logic on the server to prevent cheating and ensure synchronization.
- Use `ent.getComponent(MyCustomComponent.class)` to access state.
- Use `ent.addComponent(...)` or `ent.removeComponent(...)` to modify behavior dynamically.

## Example: Pet Entity
For a pet, you would define a `PetComponent` that tracks the owner's UUID and current training state. The `hytale-entity-design` ensures the pet persists correctly and follows the owner across chunk loads.
