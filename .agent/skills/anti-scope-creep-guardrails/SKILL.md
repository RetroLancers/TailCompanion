---
name: anti-scope-creep-guardrails
description: Enforces strict scope boundaries to keep the pet system shippable. Prevents feature explosion.
---

# Hytale Anti-Scope Creep Guardrails

This skill provides a framework for making difficult decisions to ensure a mod project remains manageable and actually reaches a "Shippable" state.

## When to use this skill

- During the planning phase of a new feature.
- When the "Backlog" is growing faster than the "Done" pile.
- Deciding whether to pivot or cut features before a deadline.

## Decision Guardrails

### 1. The "Is it Core?" Test
If a feature doesn't directly support the primary gameplay loop (e.g., "Owning and caring for a companion"), it should be deferred or cut.

### 2. The Multiplier Effect
Beware of features that double the work for every existing asset.
- Adding "Custom Combat" to pets requires specific animations and stats for *every* creature. This is a high-scope feature.

### 3. Technical Debt Check
Will this new feature require a complete rewrite of an existing system? If so, is the trade-off worth a 2-week delay?

## Implementation Tactics

- **Minimum Viable Product (MVP)**: Release the smallest possible version of a feature first.
- **Phase-Gate Process**: Define "V1", "V2", and "Future" buckets for all ideas.

## Best Practices

- **"No" by Default**: New ideas are rejected unless they prove their essential value.
- **Fixed-Time, Variable-Scope**: If a release date is fixed, be ready to cut features to meet it.
- **Example (Pet)**: A request for "Player-to-Pet Breeding" is made. The `anti-scope-creep-guardrails` skill leads to deferring this to "V3" because it would require new genetic algorithms, cross-breed models, and maturity states, which are not essential for the "V1" release of a simple follow-and-status mod.
