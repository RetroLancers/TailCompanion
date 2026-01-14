---
name: cosmetic-monetization-safety
description: Enforces EULA-safe, non-pay-to-win cosmetic constraints for Hytale mods and marketplaces.
---

# Hytale Monetization Safety

This skill ensures that modded content complies with Hytale's EULA and marketplace guidelines, focusing on maintaining game balance and player fairness.

## When to use this skill

- Preparing mods for public release or marketplace submission.
- Designing monetization strategies for custom servers.
- Reviewing content to prevent "Pay-to-Win" (P2W) mechanics.

## Core Rules

### 1. No Gameplay Advantage
Cosmetics must never grant a competitive edge.
- **ALLOWED**: A neon-glowing skin for a pet.
- **FORBIDDEN**: A neon-glowing skin that also doubles the pet's movement speed.

### 2. Clarity of intent
Paid content should be clearly distinguished from earned content.
- Use distinct naming conventions or rarity tags for marketplace items.

### 3. Technical Constraints
Ensure that high-poly or high-res marketplace assets do not cause performance issues for other players (preventing "Griefing via lag").

## Validation Checklist

- [ ] Does this item modify any `hytale:health`, `hytale:attack`, or `hytale:speed` components? (Should be No)
- [ ] Is the item purely visual or audio-based? (Should be Yes)
- [ ] Does it violate Hytale's community standards or copyrights? (Should be No)

## Best Practices

- **Rarity Systems**: Use cosmetic-only rarities (Common, Epic, Legendary) to provide value without affecting balance.
- **Batch Validation**: Use the `asset-validation-and-qc` skill to automatically check for P2W component couplings.
- **Example (Pet)**: A "Premium Golden Retriever" skin is released. The `cosmetic-monetization-safety` skill verifies that it uses the same base stats as the standard retriever, ensuring the purchase is purely for aesthetic preference.
