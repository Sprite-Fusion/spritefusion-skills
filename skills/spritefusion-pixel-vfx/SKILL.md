---
name: spritefusion-pixel-vfx
description: Add pixel art visual effects to a game from Sprite Fusion's open source library of effects as code - explosions, hits, slashes, fire, lightning, ice, energy, shields, pickups, weather, and more. Use when the user wants a visual effect, impact feedback, or spell effects in a pixel art game.
---

# Pixel art VFX with Sprite Fusion

Requires the Sprite Fusion MCP server. If its tools aren't available, see the `spritefusion-pixel-art` skill to connect it.

Sprite Fusion's [pixel art VFX library](https://www.spritefusion.com/pixel-art-vfx) is an open source library of game effects as code.

## 1. Find the closest effect

Call `list_vfx`: every effect with its category, a one-line description, and its situations with animated previews. Pick the effect and situation closest to what the user wants.

## 2. Get it

Call `get_vfx` with the effect's `slug`. It returns:

- its recipe: timeline, layers, palette, and the numbers that make it look right, enough to rebuild it in any engine
- its situations as ready calls
- its options and hooks
- its complete TypeScript source: one file, no dependencies

## 3. Build it into the game

- When the game runs JavaScript or TypeScript, run the file as is.
- Otherwise, port it to the user's engine from its recipe and source, keeping its timings, layers, and palette.
- Adapt its size, colors, and timing to the game.
- Show the user the effect's preview.

When nothing matches exactly, combine or adapt the closest effects rather than starting from scratch.
