---
name: spritefusion-style-consistency
description: Create new pixel art in the style of existing sprites (the user's own art or earlier results) with Sprite Fusion. Use when the user wants new assets in the same style as their game's art, such as matching enemies, items, or props.
---

# Match an existing style with Sprite Fusion

Requires the Sprite Fusion MCP server. If its tools aren't available, see the `spritefusion-pixel-art` skill to connect it.

## Style or edit?

- **A new subject in the style of existing art**: `generate_sprites_in_style`, with 1 to 20 reference images. It returns 9 sprites up to 80 pixels, and 4 from 96.
- **A targeted change that should preserve the original sprite**: `edit_sprite` instead. Its first input is the sprite to edit, and later inputs, up to 9 in total, are visual references, as in `Give the hero from the first image the sword and shield from the other images`.

## Choose the references

- A small sprite sheet of 4 to 8 sprites works well as a style reference. Larger sets may confuse the results.
- Explain the role of each reference in the prompt when it isn't obvious.
- Pass library sprites by `asset_id`, and project files as a `data_url` or through `create_upload`.

## Write the prompt

- Describe only the new subject, such as `A small forest shrine` or `A set of alien weapons`: the references provide the style.
- Keep the prompt neutral: thematic terms like "giant" may overpower the reference style.
- Reinforce key style traits in the prompt when needed, such as `no outlines`.
- Leave `size` out to match the references' size, or set it for another size.

## Keep the colors

- References made with a Sprite Fusion palette and passed by `asset_id` keep it when they all share the same palette.
- Pass a palette only when the user asks for one or asks you to choose one, not for a wish for consistency. Palettes aren't detected from images: when the user asks to keep the exact colors of their own art, pass its colors as `palette: {"colors": [...]}`.
- To make sprites that already exist match a palette, use `snap_to_palette`: see `spritefusion-palettes`.

Tag the results with the game's name when the user asks, so they can find them again with `list_assets`.
