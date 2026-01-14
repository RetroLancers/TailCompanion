---
name: marketplace-packaging
description: Prepares mods and assets for distribution and sale. Handles versioning and SKU separation.
---

# Hytale Marketplace Packaging

This skill focuses on the technical and organizational steps required to prepare a mod for public distribution, either through community sites or the official Hytale Marketplace.

## When to use this skill

- Creating final build artifacts (.jar, .zip).
- Managing version numbers and changelogs.
- Separating "Free" and "Premium" content for SKU management.

## Packaging Process

### 1. Mod Manifest (metadata.json)
Ensure your manifest is complete and follows official versioning standards (Semantic Versioning).

```json
{
  "id": "mymod:pets_pro",
  "version": "1.2.0",
  "author": "YourName",
  "dependencies": ["hytale:core"]
}
```

### 2. Resource Obfuscation (Optional)
Depending on your platform, you may want to obfuscate Java code or protect unique assets. Always check marketplace rules regarding obfuscation.

### 3. Documentation and Assets
- **Changelog**: Provide clear notes on what's new/fixed.
- **Storefront Assets**: High-quality screenshots (16:9) and a compelling icon (512x512).

## Best Practices

- **Zero-Dependency Core**: Design large mods so that optional modules can be enabled/disabled without breaking the base game.
- **Compatibility Layers**: Ensure your mod doesn't conflict with common library mods.
- **Example (Pet)**: Packaging a "Legendary Pet Pack" involves bundling the `.bbmodels`, 4K textures, and the `.jar` containing the custom AI logic into a single, signed distribution file with a clear `README.md`.
