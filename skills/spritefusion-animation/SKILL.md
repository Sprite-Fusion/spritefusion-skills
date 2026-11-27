---
name: spritefusion-animation
description: Animate pixel art sprites with Sprite Fusion, such as idle, walk, run, attack, or jump animations, starting from a pose suited to the motion, and save the animation and its sprite sheet into the game project. Use when the user asks to animate a sprite or character, or needs a sprite sheet animation.
---

# Animate pixel art with Sprite Fusion

Requires the Sprite Fusion MCP server. If its tools aren't available, see the `spritefusion-pixel-art` skill to connect it.

## 1. Start from the right image

The animation must be cohesive with its starting image.

- For walking, running, attacking, jumping, and similar actions, first use `edit_sprite` to create a starting pose suited to the motion, such as `Walk pose`, then animate the edited sprite.
- Idle and other subtle animations can usually use the original sprite directly.

If the still image is standing straight, it can't correctly loop a running animation.

Use the version the user means. If that version was edited locally, send the current file as input.

## 2. Before you animate

- Clean the still image first: fixing small details and outline gaps often helps create a better animation.
- If the motion goes past the sprite's edges, like an attack or a jump, the animation gets cropped. Add room around the sprite first with `Canvas size` in the [Pixel Art Generator](https://www.spritefusion.com/pixel-art-generator/editor) editor.
- A sprite the user imported must be genuine pixel art, with a clean, consistent grid and a pose suited to the motion.
- The sprite to animate can be up to 256×256 pixels.

## 3. Describe the motion

Call `animate_sprite` with a prompt that describes the motion, its energy, and whether it should loop, such as `A relaxed idle bounce, seamless loop` or `Walking animation`.

- Set the number of frames with `output_frames`, an even number from 2 to 16, and the number of colors with `colors`, from 2 to 256, not in the prompt.
- Don't describe a sprite sheet layout in the prompt.
- Animations keep the colors of their sprite and don't accept a palette.

## 4. Save the animation

The result is one animation, saved to the user's library:

- `assetUrl`: the animation
- `spritesheetUrl`: its sprite sheet, one row of frames
- `sourceImageUrl`: its starting image
- its frame count and FPS

Download the files the project needs into it.

If the animation is wrong, go back to the still image, adjust the pose or silhouette, then generate a new animation.

## Several animations

- Create each pose as a separate edit of the character, then animate each one. Don't ask one edit for a sprite sheet of several poses.
- Tag them with the game's name when the user asks.

## Normal maps

`create_normal_map` with the animation's `asset_id` returns a normal map sprite sheet with the same frames: see `spritefusion-normal-maps`.
