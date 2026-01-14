---
name: pet-framework-architecture
description: Generalizes a single entity into a reusable, multi-entity system. Useful for creating extensible NPC or item frameworks.
---

# Hytale Framework Architecture

This skill focuses on designing mod systems that are extensible and data-driven, allowing for easy addition of new content without modifying core logic.

## When to use this skill

- Expanding a single pet/NPC into a multi-species system.
- Designing modular item systems (e.g., weapons with swappable modules).
- Building registry patterns for custom mod features.

## Design Patterns

### 1. Abstract Component Logic
Instead of hardcoding behavior for a "Wolf", create a "MammalAI" component that takes parameters for speed, aggression, and diet.

### 2. Registry Systems
Use a central registry to manage custom types. This allows other mods to hook into your framework easily.

```java
public class SpeciesRegistry {
    private static final Map<String, SpeciesData> REGISTRY = new HashMap<>();

    public static void register(String id, SpeciesData data) {
        REGISTRY.put(id, data);
    }
}
```

### 3. Inheritance in Data Assets
Leverage JSON inheritance (if supported) or template patterns to reduce duplication in asset files.

## Architectural Goals

- **Decoupling**: Keep visual assets (models) separate from gameplay logic (components).
- **Scalability**: Ensure the system can handle 100+ different entities without significant performance degradation.
- **Example (Pet)**: Transitioning from a single "Dog" mod to a "Universal Pet Framework" where adding a "Cat" only requires a new JSON asset and a few texture variations, reusing 90% of the code.
