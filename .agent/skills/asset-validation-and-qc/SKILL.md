---
name: asset-validation-and-qc
description: Validates generated assets against technical and marketplace constraints.
---

# Hytale Asset Validation and QC

This skill provides a set of Quality Control (QC) checks to ensure that modded assets are technically sound, optimized, and ready for release.

## When to use this skill

- Testing new models or textures before importing them into the game.
- Auditing existing assets for performance regressions.
- Preparing content for marketplace submission.

## Technical Checks

### 1. Mesh Validation
- **Poly Count**: Verify the triangle count is within acceptable limits for the entity type (e.g., pets < 2000 tris).
- **Bone Count**: Ensure the number of bones doesn't exceed engine limits (usually 64 or 128 per entity).
- **Pivots**: Check that all bones have valid pivot points within the bounding box.

### 2. Texture Optimization
- **File Size**: Check that textures are compressed and sized appropriately (e.g., 256x256 or 512x512).
- **Power of Two**: Ensure dimensions are powers of two (32, 64, 128, etc.) for GPU compatibility.

### 3. Registration Integrity
- **Missing Paths**: Verify that all JSON references to textures and models actually exist in the file system.
- **Component Validity**: Ensure all component IDs used in entity files are registered in the server plugins.

## Automation Logic

Use a script to run these checks in bulk.

```python
def run_qc(asset_path):
    results = []
    if get_poly_count(asset_path) > MAX_POLYS:
        results.append("ERROR: Polycount too high")
    if not is_power_of_two(get_texture_dims(asset_path)):
        results.append("WARNING: Texture not power of two")
    return results
```

## Best Practices

- **Continuous Integration**: Run validation scripts automatically on every git commit.
- **Severity Levels**: Distinguish between "Critical Errors" (game crashes) and "Style Warnings" (optimization tips).
- **Example (Pet)**: Before releasing a "Dino Pack", the `asset-validation-and-qc` skill identifies a T-Rex model that has 5000 triangles and a missing `eye_glow` texture, preventing a buggy release.
