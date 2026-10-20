# Pixel Engine for Claude

Make game-ready pixel art from Claude and drop it straight into your project. Describe a character, item or tile and get a sprite at an exact pixel size. Describe a motion and get a looping animation or a sprite sheet. Turn an existing image into clean pixel art with a capped palette, and remove the background when an asset is ready for your engine.

The plugin connects Claude to [Pixel Engine](https://pixelengine.ai)'s hosted server and adds a skill that walks Claude through the whole flow, from generating a sprite to saving the file and setting it up in Godot, Unity or a web game.

## What you can do

- Generate pixel-art sprites, characters, items and tiles, including sprites at an exact size (16–128 px) with the background already removed.
- Animate a sprite into a looping animation or a game-ready sprite sheet, with room to move for attacks and jumps.
- Convert any image into pixel art on a real pixel grid, free.
- Remove the background from a finished animation or image.
- Check your credit balance and the status of any job.

## Install

From the Claude directory, add **Pixel Engine**. Or in Claude Code:

```text
/plugin marketplace add pixel-engine-ai/claude-plugin
/plugin install pixel-engine@pixel-engine
```

The first time Claude calls a Pixel Engine tool, your browser opens pixelengine.ai. Sign in and approve the connection. Claude never sees your password, and you can disconnect it any time under Account → Connect an agent.

You need a Pixel Engine account. New accounts start with free credits; each tool states its cost before it runs, and every result reports what it charged and what's left.

## Try it

- "Make a 48x32 pixel-art fox, side view facing right, then animate a run cycle as a sprite sheet and save it in my project."
- "Turn this image into pixel art with 16 colors."
- "Make a small red potion bottle sprite and remove the background."
- "How many Pixel Engine credits do I have?"

## What the plugin sends, and where

The plugin declares one remote server, `https://api.pixelengine.ai/functions/v1/mcp`, operated by Pixel Engine. It runs nothing on your machine. When Claude uses a tool, the server receives what that tool needs: your prompt, the settings you choose, and any image or image URL you give it. Each result's download link works for about an hour, and the file can be fetched again for 24 hours after the job. How Pixel Engine handles your data is described in the [Privacy Policy](https://pixelengine.ai/privacy), and use is covered by the [Terms of Service](https://pixelengine.ai/terms).

## What's included

- [`.claude-plugin/plugin.json`](.claude-plugin/plugin.json): the plugin manifest
- [`.claude-plugin/marketplace.json`](.claude-plugin/marketplace.json): lets Claude Code add this repository as a marketplace
- [`.mcp.json`](.mcp.json): the hosted Pixel Engine server
- [`skills/pixel-engine-game-assets`](skills/pixel-engine-game-assets/SKILL.md): the workflow guide Claude follows

## Support

Write to [hello@pixelengine.ai](mailto:hello@pixelengine.ai), or see the [setup guide](https://pixelengine.ai/guides/connect).

## License

[MIT](LICENSE)
