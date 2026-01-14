---
name: command-driven-interactions
description: Implements command-based player interactions as a UI-light gameplay layer. Use when registering custom slash commands to interact with entities or systems.
---

# Hytale Command-Driven Interactions

This skill focuses on creating text-based commands to interact with modded systems, which is ideal for early prototyping or maintaining a clean UI.

## When to use this skill

- Creating interaction layers (e.g., `/pet feed`, `/home tp`, `/clan invite`).
- Providing administrative tools for mod testing.
- Implementing complex logic triggers that don't need a dedicated UI menu.

## Technical Implementation

### 1. Registering a Command
Register commands in your Java plugin's initialization phase. Use the Command API to define arguments and permissions.

```java
public class MyModPlugin extends HytalePlugin {
    @Override
    public void onEnable() {
        this.getCommandManager().register("action", (sender, args) -> {
            // Logic here
            return true;
        })
        .setPermission("mymod.use")
        .addArgument(ArgumentType.STRING, "subcommand");
    }
}
```

### 2. Context-Aware Interactions
Commands should often target the entity the player is looking at or an entity they "own".

```java
Entity target = player.getLookTarget(10.0f); // Range of 10 blocks
if (target != null && target.hasComponent(MyModComponent.class)) {
    // Perform action
}
```

### 3. Feedback and Tab Completion
- **Feedback**: Use the chat system to provide immediate confirmation (e.g., "You fed the wolf!").
- **Tab Completion**: Implement `TabCompleter` to make commands user-friendly.

## Best Practices

- **Minimalism**: Use commands to replace complex UIs during early development.
- **Safety**: Always validate permissions and distance before executing world-modifying commands.
- **Example (/pet)**: `/pet status` displays the pet's current levels in chat, while `/pet stay` toggles the AI state between `FOLLOWING` and `IDLE`.
