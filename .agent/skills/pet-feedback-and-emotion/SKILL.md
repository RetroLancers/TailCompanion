---
name: pet-feedback-and-emotion
description: Maps internal entity state to visible player feedback (animations, emotes, messages). Use to enhance player attachment and immersion.
---

# Hytale Feedback and Emotion

This skill guides the translation of abstract entity states (like mood or health) into tangible visual and auditory signals that players can easily interpret.

## When to use this skill

- Making NPCs feel "alive" through reactive animations.
- Implementing emote systems (particles, text bubbles).
- Building emotional reinforcement loops between players and companions.

## Implementation Patterns

### 1. State-to-Animation Mapping
Use a system to monitor component changes and trigger client-side animation overrides.

```java
public class FeedbackSystem extends EntitySystem {
    @Override
    protected void tick(Entity ent) {
        var mood = ent.getComponent(MoodComponent.class);
        var anim = ent.getComponent(AnimationComponent.class);

        if (mood.isHappy()) {
            anim.play("hytale:idle_happy", LoopType.ONCE);
        } else if (mood.isAggressive()) {
            anim.setBaseLayer("hytale:stance_ready");
        }
    }
}
```

### 2. Particle and Emote Triggers
Use particles for non-verbal feedback (e.g., hearts for love, steam for anger).

```java
public void playEmote(Entity ent, EmoteType type) {
    var pos = ent.getPosition().add(0, 2, 0); // Above head
    World.spawnParticle(type.getParticle(), pos);
    World.playSound(type.getSound(), pos);
}
```

### 3. Messaging and Dynamic Text
Sometimes a simple chat message or floating text bubble is the most effective feedback.
- "Buddy looks hungry..."
- "Buddy nudges your hand eagerly."

## Design Principles

- **Clarity**: Feedback should be unmistakable. A "Sad" state should look drastically different from an "Idle" state.
- **Consistency**: Use the same colors and icons for the same emotions across different entities.
- **Example (Pet)**: When a pet's food level drops below 20%, it triggers a "Whining" sound effect and a thought bubble particle containing a bone icon.
