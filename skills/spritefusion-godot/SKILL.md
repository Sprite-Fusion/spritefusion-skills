---
name: spritefusion-godot
description: Use Sprite Fusion art in a Godot project - normal maps for 2D lights, and tilemaps exported for Godot 4 or Godot 3. Use when the project is a Godot game and the user wants Sprite Fusion sprites, animations, normal maps, VFX, or tilemaps.
---

# Sprite Fusion in Godot

Make the art with the other Sprite Fusion skills and save it into the project: sprites, edits, style matching, 8 directions, animations, palettes, normal maps, and pixel art VFX. Start with `spritefusion-pixel-art`.

## Normal maps and lights

Create the maps with `spritefusion-normal-maps`, in the default `opengl` format. Import them without sRGB, compression, or filtering. Then put the sprite and its normal map in a `CanvasTexture`, assign it to the `Sprite2D`, and add a `PointLight2D`.

## Tilemaps

Sprite Fusion's Tilemap Editor exports maps:

- to Godot 4 as `TileMapLayer` scenes, with collision layers and per-tile attributes as TileSet custom data: see https://www.spritefusion.com/docs/tilemap-editor/exporting-maps/godot-4
- to Godot 3 as `TileMap` scenes, with per-tile attributes in `tile_data.json` and no generated collision shapes: see https://www.spritefusion.com/docs/tilemap-editor/exporting-maps/godot-3

## Godot plugin

If the user asks about Sprite Fusion's Godot plugin, see https://www.spritefusion.com/docs/pixel-art-generator/integrations/godot. Don't install it unless they ask.
