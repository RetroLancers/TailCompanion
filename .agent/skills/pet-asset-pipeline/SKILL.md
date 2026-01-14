---
name: pet-asset-pipeline
description: Defines conventions for models, textures, animations, and attachment points in Hytale.
---

# Hytale Asset Pipeline

This skill provides a structured workflow for creating and importing visual assets into Hytale using official and community tools.

## When to use this skill

- Creating custom 3D models and textures.
- Defining animation sets for NPCs or items.
- Establishing naming conventions and folder structures for large asset packs.

## Core Tools

- **Hytale Model Maker (HMM)**: The browser-based tool for collaborative modeling and animation.
- **Blockbench**: An alternate, powerful 3D editor with a Hytale-specific plugin.
- **JSON Manifests**: Used to register assets and their properties in the game.

## Export & Registration Workflow

### 1. Naming Conventions
Always use a unique namespace for your mod's assets.
- GOOD: `mymod:iron_hat`, `mymod_assets/textures/items/`
- BAD: `iron_hat`, `assets/textures/`

### 2. Model Structure
- **Bones/Groups**: Organize your model into logical groups (e.g., `body`, `head`, `left_arm`).
- **Pivot Points**: Ensure pivots are correctly placed for natural animation (e.g., at the base of the neck for the head).
- **Socket Points**: Add empty bones or specific markers where cosmetics or VFX will attach (e.g., `socket_hat`, `socket_vfx_hand`).

### 3. Registration (JSON)
Assets must be registered in the `data/assets/` folder of your mod.

```json
{
  "id": "mymod:custom_creature",
  "type": "hytale:entity_model",
  "file": "mymod:models/creature.bbmodel",
  "textures": {
    "default": "mymod:textures/creature_base.png"
  }
}
```

## Best Practices

- **Polycount Awareness**: Keep models within Hytale's aesthetic limits to maintain performance.
- **Texture Resolution**: Use consistent pixel density across all models in a pack.
- **Example (Pet)**: A pet asset requires a model with specific animation tags (`idle`, `walk`, `eat`) and a socket on the neck for collars.
