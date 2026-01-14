---
name: blender-python-generation
description: Uses Blender’s Python API to generate and modify deterministic 3D assets for Hytale.
---

# Blender Python Generation

This skill leverages Python scripting within Blender to automate the creation of Hytale-compatible assets, variants, and batch exports.

## When to use this skill

- Generating procedural variations of a base model (e.g., horns, tails).
- Automating the application of textures or materials across multiple assets.
- Batch exporting models to `.bbmodel` or other Hytale-supported formats.

## Core API Usage

### 1. Object Manipulation
Use `bpy.ops` and `bpy.data` to create and modify mesh data.

```python
import bpy

# Create a simple cube as a base for a block
bpy.ops.mesh.primitive_cube_add(size=1, location=(0, 0, 0))
block = bpy.context.active_object
block.name = "HytaleBlock"
```

### 2. Procedural Variations
Define parameters to create deterministic variants.

```python
def add_horn(length, twist):
    # Logic to create a horn mesh based on parameters
    pass

# Generate 5 different variants
for i in range(5):
    add_horn(length=i, twist=i*0.1)
```

### 3. Batch Export
Automate the export process to ensure all assets follow the same technical standards.

```python
for obj in bpy.data.objects:
    if obj.type == 'MESH':
        # Select object and export
        bpy.ops.export_scene.obj(filepath=f"/path/to/exports/{obj.name}.obj")
```

## Best Practices

- **Headless Mode**: Run Blender in the background (`blender --background --python script.py`) for automated pipelines.
- **Unit Scale**: Ensure Blender is set to "Metric" with a scale of 1.0 to match Hytale's coordinate system.
- **Example (Pet)**: A script generates 100 unique collar variants by procedurally adjusting the width of a base band and swapping out "charms" from a pre-defined library of assets.
