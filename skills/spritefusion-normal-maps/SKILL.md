---
name: spritefusion-normal-maps
description: Create normal maps for pixel art sprites and animations with Sprite Fusion, for 2D dynamic lighting in Godot, Unity, or Unreal Engine. Use when the user wants moving lights on 2D sprites, normal maps, or _n textures.
---

# Normal maps with Sprite Fusion

Requires the Sprite Fusion MCP server. If its tools aren't available, see the `spritefusion-pixel-art` skill to connect it.

A normal map tells a game engine which way each pixel faces, so moving lights can shade a flat sprite as if it had volume.

## Create the maps

`create_normal_map` takes one sprite or animation per call and returns its normal map PNG.

- Input: an `asset_id`, an animation's included, a `data_url`, or an `upload_id`. Each sprite or frame can be up to 1024×1024 pixels.
- The map keeps the sprite's size and transparency. An animation's map is a sprite sheet with the same frames as its `spritesheetUrl`.
- `strength` sets the relief, from 0 to 8: 1.5 by default.
- `format`: `opengl`, the default, is the convention Godot and Unity expect. Use `directx` for Unreal Engine.

Nothing is saved to the library: save each map into the project next to its sprite, such as `knight_n.png`.

## Use them in the engine

Import normal maps without sRGB, compression, or filtering.

- **Godot**: put the sprite and its normal map in a `CanvasTexture`, assign it to the `Sprite2D`, and add a `PointLight2D`.
- **Unity** (URP 2D): add the normal map to the sprite as a secondary texture named `_NormalMap`, and set the 2D lights' normal map quality to Fast or Accurate.
- **Unreal Engine**: use the `directx` format.
