# Bitmagic GDK for Claude Code

The [Bitmagic GDK](https://bitmagic.ai/gdk/) is a game development kit for agents: a 3D engine vendored into your project as source, asset generation, multiplayer and leaderboards, and one command that puts the game on bitmagic.ai.

This plugin teaches Claude Code to set it up.

```
/plugin marketplace add BitmagicAI/bitmagic-gdk-plugin
/plugin install bitmagic-gdk@bitmagic
```

Then say what you want to make. It installs the GDK, signs you in, scaffolds the project and starts the live dev view — after that the project's own `AGENTS.md` takes over, and `bitmagic upgrade` keeps *that* current with the engine.

Requires [Bitmagic Pro](https://bitmagic.ai/pro/) and Node.js 20+.

Licensed under the PolyForm Shield License 1.0.0 with Bitmagic's games permission — the same terms as the GDK itself. See [LICENSE.md](./LICENSE.md).

## Not using Claude Code?

Codex, Cursor and OpenCode have no plugin marketplace, so installing this means putting the same text in the file your agent reads at startup. Copy the block from https://bitmagic.ai/gdk/ into `~/.codex/AGENTS.md`, `.cursor/rules/bitmagic.mdc`, or your project's `AGENTS.md`.

## Editing

Nothing here is written by hand — it is rendered from `agent-plugin/bootstrap.md` in the Bitmagic monorepo. Send changes there.
