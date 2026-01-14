---
name: pet-ai-state-machine
description: Implements lightweight AI and state machines for Hytale entities, focusing on non-combat/companion behaviors.
---

# Hytale AI State Machine

This skill guides the implementation of modular AI behaviors using state machines within the Hytale ECS framework.

## When to use this skill

- Implementing complex NPC routines (idle, follow, patrol).
- Managing entity moods or emotional states.
- Handling behavior transitions based on world events or player interactions.

## Core Concepts

Hytale's AI uses an Entity Component System (ECS) where "Systems" process entities with specific "Components". A state machine is typically implemented as a component tracking the current state and a system that executes logic based on that state.

## Implementation Patterns

### 1. Defining States
Use an Enum to define possible AI states.

```java
public enum AIState {
    IDLE,
    FOLLOWING,
    SAD,
    HAPPY
}
```

### 2. The AI Component
Store the current state and transition timers in a component attached to the entity.

```java
public class AIStateComponent implements IComponent {
    public AIState currentState = AIState.IDLE;
    public long stateTimer = 0;
}
```

### 3. State Transition Logic
Implement transitions in a server system that runs every tick or at a lower frequency.

```java
public class AISystem extends EntitySystem {
    @Override
    protected void tick(Entity ent) {
        var ai = ent.getComponent(AIStateComponent.class);
        var stats = ent.getComponent(PetStatsComponent.class);

        // Evaluation Logic
        if (stats.hunger > 80 && ai.currentState != AIState.SAD) {
            transitionTo(ent, ai, AIState.SAD);
        }
    }

    private void transitionTo(Entity ent, AIStateComponent ai, AIState next) {
        ai.currentState = next;
        // Trigger visual feedback (emotes/animations)
    }
}
```

## Best Practices

- **Lightweight Ticking**: Don't run complex logic every tick for every entity. Use interval-based checks for mood evaluations.
- **Sensory Input**: Use Hytale's built-in sensory components to detect nearby players or food items.
- **Example (Pet)**: A pet might transition from `IDLE` to `FOLLOWING` when its owner moves beyond a certain radius, or to `HAPPY` when fed.
