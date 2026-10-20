---
name: pixel-engine-game-assets
description: "Make game-ready pixel art with the Pixel Engine tools and put it into a game project: sprites at exact sizes, looping animations, sprite sheets, pixel-art conversion and transparent backgrounds, saved as files and set up for Godot, Unity or a web game. Use when the user asks for sprites, characters, items, tiles, animations or sprite sheets for a game."
---

# Pixel Engine game assets

Use this skill with the Pixel Engine MCP tools: `generate_sprite`, `animate_sprite`, `pixelate_image`, `remove_background`, `get_job` and `check_balance`. Each tool's description states its current credit cost, and every result reports the credits charged and the balance left.

**Requires:** a connected Pixel Engine server and a Pixel Engine account. If the tools are missing, tell the user to connect Pixel Engine and sign in at pixelengine.ai; don't install anything or change settings as part of an art task.

## Pick the path

| The user wants | Do this |
| - | - |
| A sprite at an exact pixel size, e.g. "a 48x32 fox" | `generate_sprite` with `model: "pe_image_v1"`, `width` and `height` (16–128; the first number of "48x32" is the width). It comes back on its pixel grid with the background already removed. Text only, no reference image. |
| A sprite to match a reference, or an edit of an earlier one | `generate_sprite` with the default model and `source_job_id` (an earlier result) or `reference_image_url`. Ask for a plain, flat, single-colour background. |
| An existing image turned into pixel art | `pixelate_image` (free). `colors` is a maximum, not a target. |
| A character animated | `generate_sprite`, then `animate_sprite` with the sprite's `source_job_id`. |
| A transparent animation | Animate first, then `remove_background` on the animation. Removing the background before animating gives worse results. |

## Animating

- Describe the motion in order: how it starts, the action, how it ends, naming the direction and the limb ("swings the sword from overhead down to the right, then returns to guard").
- Give the character room. A `pe_image_v1` sprite is cut to its exact size with no margin, so always pass `canvas: {scale: 1.5}` for idle, walk and run, and 1.5–1.8 for attacks, jumps and dashes. Anchor `"bottom"` for jumps, and for attacks put the sprite on the side it faces away from (facing right → `"left"`).
- Frames: attack 8–12, idle and run 4–8, walk and death 6–8.
- For a game, ask for `output_format: "spritesheet"`: one PNG with every frame in a single row, left to right. The result states the frame count and the size of each frame.
- Two to four takes is normal. Say so before retrying, and stop when credits run low.

## Saving into the project

Results come back with an Output URL that works for about an hour; `get_job` can fetch a fresh link for 24 hours after the job. Save what the user wants to keep straight away:

1. Pick the project's existing art folder, such as `assets/sprites/`, `res://art/` in Godot or `Assets/Sprites/` in Unity, or ask.
2. Download with a plain HTTPS request, for example `curl -L -o assets/sprites/slime_idle.png "<Output URL>"`. Give files descriptive names: subject, action, and `_sheet` for sprite sheets.
3. If the link has expired, call `get_job` with the job id for a fresh one.
4. Note the job id next to the file, so the asset can be reused with `source_job_id` later.

## Setting it up in an engine

Pixel art needs nearest-neighbour filtering, or it turns blurry.

- **Godot 4:** set the texture filter to Nearest (Project Settings → Rendering → Textures → Default Texture Filter, or per node). For a sprite sheet, use a `Sprite2D` with `hframes` equal to the frame count, or build `SpriteFrames` for an `AnimatedSprite2D`.
- **Unity:** in the texture's import settings set Filter Mode to Point (no filter) and Compression to None. Set Sprite Mode to Multiple, open the Sprite Editor and slice with Grid By Cell Count: one row, columns equal to the frame count.
- **Web / canvas:** set `imageSmoothingEnabled = false` on the 2D context, and `image-rendering: pixelated` in CSS.

Draw each frame at a whole-number scale (2×, 3×, 4×) so pixels stay square.
