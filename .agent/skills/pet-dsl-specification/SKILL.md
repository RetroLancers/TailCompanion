---
name: pet-dsl-specification
description: Defines and validates structured specs used by LLMs to generate pet assets safely.
---

# Hytale DSL Specification

This skill focuses on defining and using a Domain Specific Language (DSL) to bridge the gap between human/AI intention and technical Hytale asset definitions.

## When to use this skill

- Creating a standardized format for AI-generated NPCs or items.
- Implementing guardrails to ensure generated content is technically valid.
- Scaling asset production by using high-level templates.

## DSL Structure

A typical DSL spec is defined in JSON or YAML and covers the "intent" of the asset.

```yaml
entity_id: "mymod:phoenix_v1"
base_type: "bird"
attributes:
  scale: 1.2
  hue_shift: 45
  glow_intensity: 0.8
behaviors:
  - "hytale:flying"
  - "mymod:resurrection"
```

## Workflow

### 1. Specification (The "What")
Define the schema for your DSL. Use tools like JSON Schema to validate inputs.

### 2. Implementation (The "How")
Write "Generators" (Python or Java) that take the DSL spec and output:
- JSON Data Assets (Hytale components).
- Texture overlays or shader parameters.
- Scripted AI transitions.

### 3. AI Collaboration
Provide the DSL schema to an LLM to generate valid, diverse entity variants without the LLM needing to understand the underlying Hytale engine code.

## Best Practices

- **Constraints**: Define strict ranges for numerical values (e.g., `scale` must be between 0.5 and 2.0).
- **Extensibility**: Allow for "Custom Data" blocks in the DSL to support unique mod features.
- **Example (Pet)**: A "Universal Pet Spec" DSL allows a user to describe a "Fire Cat" in a few lines, which is then expanded into a full suite of Hytale assets (model, textures, stats, and AI).
