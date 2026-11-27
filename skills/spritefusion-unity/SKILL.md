---
name: spritefusion-unity
description: Use Sprite Fusion art in a Unity project - normal maps for URP 2D lights, and tilemaps exported as a .unitypackage. Use when the project is a Unity game and the user wants Sprite Fusion sprites, animations, normal maps, VFX, or tilemaps.
---

# Sprite Fusion in Unity

Make the art with the other Sprite Fusion skills and save it into the project: sprites, edits, style matching, 8 directions, animations, palettes, normal maps, and pixel art VFX. Start with `spritefusion-pixel-art`.

## Normal maps and URP 2D lights

Create the maps with `spritefusion-normal-maps`, in the default `opengl` format. Import them without sRGB, compression, or filtering. Then add each normal map to its sprite as a secondary texture named `_NormalMap`, and set the 2D lights' normal map quality to Fast or Accurate.

## Tilemaps

Sprite Fusion's Tilemap Editor exports maps to Unity as a `.unitypackage` with the needed game objects, collision layers, and per-tile attributes: see https://www.spritefusion.com/docs/tilemap-editor/exporting-maps/unity.

## Unity plugin

If the user asks about Sprite Fusion's Unity plugin, see https://www.spritefusion.com/docs/pixel-art-generator/integrations/unity. Don't install it unless they ask.
