---
name: spritefusion-palettes
description: Use color palettes with Sprite Fusion - generate pixel art in a palette (a preset such as PICO-8, Game Boy, NES, or C64, a saved palette, or the game's own colors), keep it through edits, styles, and 8 directions, recolor existing sprites with a palette, and manage saved palettes. Use when the user names a palette, wants sprites in their game's colors, or wants a sprite in fewer colors.
---

# Palettes with Sprite Fusion

Requires the Sprite Fusion MCP server. If its tools aren't available, see the `spritefusion-pixel-art` skill to connect it.

Use a palette only when the user asks for one or asks you to choose one. Don't infer it from a theme, a style, or a wish for consistency.

## Give a palette

Every tool that takes a palette accepts exactly one source:

| Source | Example |
| --- | --- |
| One-off colors, not saved | `{"colors": ["#182818", "#486840", "#f0e8c0"]}` |
| A built-in preset | `{"preset": "pico-8"}`: slugs from `list_palettes` |
| A saved palette | `{"id": "..."}`: from `list_palettes` |

One-off colors are 2 to 256 different six-digit hex colors, with or without `#`. Named colors, three-digit shorthand, and alpha hex values aren't accepted. When the user's palette is a file in the project, such as `palette.hex`, pass its colors.

## New sprites in a palette

Pass `palette` to `generate_sprites`, `edit_sprite`, `generate_sprites_in_style`, or `create_8_directions`: every result uses only its colors.

- A sprite made with a palette and passed by `asset_id` keeps it through edits and 8 directions: no `palette` needed. A style keeps it when every reference shares the same palette.
- A `palette` in the request replaces the sprite's palette. `"palette": null` drops it: send it only when the user wants the palette dropped.
- Palettes aren't detected from images. To keep the exact colors of any other sprite, such as one from the user's project, pass its colors as `palette`.
- Animations keep the colors of their sprite and don't accept a palette.

## Recolor existing sprites

With `snap_to_palette`, every opaque pixel takes one of the palette's colors, and transparency is kept.

- One sprite per call, up to 1024×1024 pixels.
- `mode`, with a palette: `nearest`, the default, gives each pixel the closest palette color; `lightness` maps by lightness alone, which suits a single ramp such as four greens.
- Without a palette, it reduces the sprite's colors instead: near-identical colors merge, then at most `max_colors` remain, from 1 to 256 (32 by default). The colors left are the sprite's own.
- It returns the PNG and saves nothing to the library: save the result into the project.

For new sprites, pass the palette to the generation tool instead.

## Saved palettes

`list_palettes` lists the user's saved palettes and the built-in presets. `save_palette`, `rename_palette`, and `delete_palette` manage the saved ones, which the Sprite Fusion web app, API, and MCP server share. Use them only when the user asks.

- To change a palette's colors, save a new one.
- Renaming or deleting a saved palette doesn't change sprites already generated with it.
