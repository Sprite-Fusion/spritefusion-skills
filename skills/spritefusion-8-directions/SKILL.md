---
name: spritefusion-8-directions
description: Turn one pixel art sprite into eight directional views with Sprite Fusion. Use when the user wants a character or another sprite facing eight directions (north, north-east, east, and the others).
---

# 8 directions with Sprite Fusion

Requires the Sprite Fusion MCP server. If its tools aren't available, see the `spritefusion-pixel-art` skill to connect it.

Call `create_8_directions` with exactly one sprite and no prompt:

```json
{ "input": { "asset_id": "..." } }
```

- It returns exactly eight directional sprites, one per direction, saved to the user's library.
- `size` is optional: the directions come out at the size closest to the sprite, from 16 to 128 pixels.
- A sprite made with a palette and passed by `asset_id` keeps it: no `palette` needed.
- Palettes aren't detected from images. When the user asks to keep the exact colors of any other sprite, such as one from their project, pass its colors as `palette`.

Download the eight sprites into the project, such as into `assets/hero`. To animate a direction, see `spritefusion-animation`.
