---
name: pet-stats-and-decay
description: Designs and implements time-based stat systems with offline-safe decay for Hytale entities.
---

# Hytale Stats and Decay

This skill covers the implementation of persistent, time-sensitive attributes (like hunger, energy, or happiness) that evolve even when the server is empty or the player is offline.

## When to use this skill

- Implementing survival mechanics for pets or NPCs.
- Creating growth or aging systems.
- Designing non-punitive decay rules for long-term engagement.

## Implementation Strategies

### 1. The Stats Component
Store the raw value and a "Last Updated" timestamp (Server Time / Epoch).

```java
public class StatsComponent implements IComponent {
    public float hunger = 100.0f;
    public long lastProcessedTimestamp; // UTC milliseconds
}
```

### 2. Offline-Safe Delta Calculations
Instead of ticking the stat down every second, calculate the decay whenever the entity is loaded or interacted with.

```java
public float calculateDecay(StatsComponent stats, long currentTime) {
    long elapsedSeconds = (currentTime - stats.lastProcessedTimestamp) / 1000;
    float decayRate = 0.01f; // per second
    return Math.max(0, stats.hunger - (elapsedSeconds * decayRate));
}
```

### 3. Non-Punitive Decay Rules
- **Caps**: Prevent stats from dropping below a "Distressed" state but don't let them reach death/despawn from offline decay alone.
- **Catch-up Logic**: When a player returns after a long absence, provide a "Welcome Back" buff or a grace period before the full effects of decay are felt.

## Usage in Gameplay

- **Hunger**: Affects movement speed or animation state (e.g., lethargic).
- **Happiness**: Controls the frequency of positive emotes or "gifts" given to the player.
- **Energy**: Determines how long a companion can perform tasks before needing sleep.

## Example: Pet Stats
A pet's loyalty might decay if ignored for weeks, but never below a "Base Bond" level. When the owner logs in, the `pet-stats-and-decay` system calculates the delta, updates the pet's mood to "Sad", and triggers a notification.
