---
name: spritefusion-pixel-art
description: Generate and edit game-ready pixel art sprites at exact sizes with Sprite Fusion, and save them into the game project. Use when the user asks for pixel art sprites, items, icons, props, characters or enemies, wants to change an existing sprite, or wants to find earlier Sprite Fusion results.
---

# Sprite Fusion pixel art

Sprite Fusion creates game-ready pixel art sprites and animations. Every generation is saved to the user's Sprite Fusion library, and you download the files into their project.

## Connect first

This skill uses the Sprite Fusion MCP server's tools (`generate_sprites`, `edit_sprite`, and the others below). If they aren't available, tell the user how to connect, then continue their request once they have. They sign in to Sprite Fusion in their browser: no API key is needed.

- Every agent on their machine at once: `npx spritefusion setup`
- Claude Code: `claude mcp add --transport http spritefusion https://www.spritefusion.com/mcp` adds it to the current project; add `--scope user` before `spritefusion` to use it in every project. Then run `/mcp`, choose `spritefusion`, and sign in.
- Codex: `codex mcp add spritefusion --url https://www.spritefusion.com/mcp`, then `codex mcp login spritefusion`
- Claude, ChatGPT, Cursor, VS Code, and any MCP client: https://www.spritefusion.com/docs/pixel-art-generator/api/mcp

Don't install software or change the user's MCP configuration yourself unless they ask you to.

For scripts, CI jobs, or clients that can't add an MCP server, use the HTTP API with an API key (`SPRITE_FUSION_API_KEY`), following https://www.spritefusion.com/mdx/docs/pixel-art-generator/api/agent-guide.mdx.

## Choose the tool

| User goal | Tool |
| --- | --- |
| A new sprite, without an input image | `generate_sprites` |
| A targeted change to an existing sprite, such as its equipment, outfit, or pose | `edit_sprite` |
| A new sprite guided by one or more visual examples | `generate_sprites_in_style` |
| Eight directional views of one sprite | `create_8_directions` |
| Animating one sprite | `animate_sprite` |
| A normal map of a sprite or animation, for dynamic lighting | `create_normal_map` |
| An existing sprite recolored with a palette, or in fewer colors without one | `snap_to_palette` |
| A pixel art effect in the game | `list_vfx`, `get_vfx` |

Don't substitute a different tool when the request clearly maps to one of these. Use `edit_sprite` for a targeted change that should preserve the original sprite, and `generate_sprites_in_style` when the examples should guide a new sprite.

## Pick the size

The `size` field is a square sprite size: `16`, `24`, `32`, `48`, `64`, `80`, `96`, `112`, or `128` pixels. Set the size with the `size` field, not in the prompt. Ask which size to use only when it can't be inferred from the request.

- `edit_sprite` keeps the size of its first input and takes no `size`.
- `generate_sprites_in_style` and `create_8_directions` infer the size from their input sprites when `size` is omitted.
- If a sprite comes back a few pixels off the size asked for (or off its input's, for an edit), such as 117 for 112, don't count it as a failure, and don't retry, rescale, crop, or pad it on your own.

## Write the prompt

- Describe one item or subject and the visual details that matter, such as `A clockwork fox carrying a brass lantern`.
- Don't ask for a number of outputs: variations come automatically. Use `Icons of a magic potion`, not `15 icons of a magic potion`.
- Don't ask for a grid, contact sheet, atlas, or sprite sheet that packs several assets into one image. `Make multiple boats` is fine; `make a grid of 24 items` isn't.
- Leave out pixel dimensions and noisy phrases such as "transparent background", "crisp pixel art", or "pixel-perfect pixel art".
- For an edit, state the change and anything important that should stay the same. Create each pose as a separate edit, not as a sprite sheet of poses.
- Don't add visual requirements that conflict with the user's request.

## Results and retries

- `generate_sprites` returns 12 sprites up to 80 pixels, and 4 from 96.
- With `count: 1`, `generate_sprites` returns a single sprite instead. Use it when the user doesn't need variations; leave `count` out for the full set.
- Never retry a generation automatically after a timeout or interruption: results may already be saved. Check `list_assets` first.

## Save results into the project

- Download each result from its `assetUrl` into the project. Don't depend on hotlinking the hosted URLs indefinitely: keep project-owned copies of the files you ship.
- Results include image previews you can see. When presenting choices, use stable labels tied to the request and the asset. Continue without a selection step when the user's intent is clear.
- Keep a small record per request: its ID, the operation, the prompt, and each output's asset ID, URL, and local path once downloaded.
- Reuse an image output's `id` as an `asset_id` input for follow-up work, and use `list_assets` to find earlier results.
- For edits and animations, use the version the user means. If that version was edited locally, send the current file as input.

## Input images

Tools that take images accept each one in one of three forms:

- `{"asset_id": "..."}`: a sprite already in the user's library
- `{"data_url": "data:image/png;base64,..."}`: a small local file, up to 1 MB, and 2.5 MB across a request's inline images
- `{"upload_id": "..."}`: a larger file, up to 20 MiB, uploaded with `create_upload`. PUT the exact file bytes to its `upload_url` with every returned header within 5 minutes. Never log `upload_url` or `upload_id`.

Inputs can be still PNG, JPEG, WebP, GIF, BMP, TIFF, or AVIF images. Images attached to the chat can't be passed to tools directly: send the file itself when you have access to it, or ask the user to import the sprite in the [Pixel Art Generator](https://www.spritefusion.com/pixel-art-generator/editor), then find it with `list_assets`.

## Organize with tags

- Tag results when the user asks for it or names a group for them. The basic, recommended use is one tag per game or project, such as `dungeon-crawler`; tags can also group a character or a kind of asset.
- Pass `tags` to the generation tool. Check `list_tags` first, and reuse an existing tag rather than creating a near-duplicate such as `weapon` next to `weapons`.
- Name the group, not the individual sprite.
- `set_asset_tags` replaces every tag on an asset: to add one, send its current tags plus the new one.
- Find a group with `list_assets` and its `tag` field.

## Ask only what matters

Ask a short question only when a missing choice would materially change the result: what to create or change, which image is the primary subject when several are given, what role each supporting image should have, which size to use when it can't be inferred, or what motion to animate. If the request and inputs already answer those, proceed without asking for confirmation. Don't ask the user to choose technical or implementation details.

## Related skills

- `spritefusion-animation`: animate a sprite from the right starting pose
- `spritefusion-8-directions`: eight directional views of a sprite
- `spritefusion-style-consistency`: new sprites in the style of existing art
- `spritefusion-palettes`: sprites in a palette, and recoloring existing ones
- `spritefusion-normal-maps`: normal maps for 2D lighting
- `spritefusion-pixel-vfx`: pixel art effects as code
- `spritefusion-godot` and `spritefusion-unity`: Sprite Fusion in Godot and Unity
