---
name: cosmetic-attachment-system
description: Implements cosmetic-only attachments that never affect gameplay in Hytale.
---

# Hytale Cosmetic Attachment System

This skill focuses on the technical implementation of "Wearables" — items that attach to an entity's model without modifying its core stats or hitbox.

## When to use this skill

- Creating hats, collars, wings, or skins for pets and players.
- Implementing "Equip/Unequip" logic for cosmetic items.
- Syncing cosmetic state across multiplayer clients.

## Technical Implementation

### 1. Bone Sockets
Cosmetics rely on "Sockets" defined in the base entity model. A socket is a specific bone or coordinate where an attachment can be parented.

```json
{
  "entity": "mymod:example_pet",
  "attachments": {
    "head": {
      "item": "mymod:party_hat",
      "offset": [0, 0.5, 0],
      "rotation": [0, 0, 0]
    }
  }
}
```

### 2. The Cosmetic Component
Track equipped cosmetics in a dedicated component.

```java
public class CosmeticComponent implements IComponent {
    // Map of Socket Name -> Item ID
    public Map<String, String> equipped = new HashMap<>();
}
```

### 3. Multiplayer Syncing
Ensure that when a player equips a cosmetic, the change is broadcasted to all nearby clients. Hytale's ECS automatically syncs component data if marked correctly in the codec.

## Design Patterns

- **Separation of Concerns**: Never bundle gameplay stats (like +10 Health) into a cosmetic item. Use this system strictly for visual flair.
- **Validation**: Check if the base entity model actually has the required socket before attempting to attach a cosmetic.
- **Example (Pet)**: A "Red Bow" is attached to the `socket_neck` bone of a cat model. The `cosmetic-attachment-system` handles the positioning and lifecycle of the bow asset.
