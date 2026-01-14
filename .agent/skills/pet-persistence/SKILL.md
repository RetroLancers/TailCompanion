---
name: pet-persistence
description: Handles saving and loading entity state safely across sessions and server restarts in Hytale.
---

# Hytale Entity Persistence

This skill ensures that custom entity data is correctly serialized, stored, and migrated across game versions.

## When to use this skill

- Saving custom component data (stats, ownership, AI state).
- Handling schema changes when updating your mod.
- Ensuring data integrity during server crashes or migrations.

## Technical Details

Hytale uses **Codecs** (DataFixerUpper pattern) for serialization. This allows for powerful versioning and data mapping.

### 1. Serializing Components
Every custom component that needs to persist must define a `MapCodec`.

```java
public static final MapCodec<PetPersistenceComponent> CODEC = RecordCodecBuilder.mapCodec(inst -> inst.group(
    Codec.STRING.fieldOf("ownerUuid").forGetter(c -> c.ownerUuid),
    Codec.INT.fieldOf("level").forGetter(c -> c.level),
    Codec.unboundedMap(Codec.STRING, Codec.FLOAT).fieldOf("stats").forGetter(c -> c.stats)
).apply(inst, PetPersistenceComponent::new));
```

### 2. Versioning and Migrations
When changing the structure of your data:
1. Increment the data version in your mod manifest.
2. Provide a `DataFixer` to transform old JSON structures into new ones.

### 3. Save Frequency
- **Auto-save**: Hytale handles entity saving when chunks are unloaded or the server shuts down.
- **Manual Save**: For critical data (e.g., marketplace transactions), use the persistence API to force a sync to the database.

## Best Practices

- **Backward Compatibility**: Always provide default values for new fields to handle older entity saves.
- **UUIDs over Names**: Always persist player identifiers as UUIDs, as names can change.
- **Validation**: Sanitize data on load to prevent corrupted states from crashing the server.

## Example: Pet Serialization
The `pet-persistence` skill manages the `PetState` object, ensuring the "Golden Collar" cosmetic and "Level 50" status are preserved even if the server is updated or the pet is transferred between servers.
