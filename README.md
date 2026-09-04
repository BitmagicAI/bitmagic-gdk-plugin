# Bitmagic GDK for Claude Code

The [Bitmagic GDK](https://bitmagic.ai/gdk/) is a game development kit for agents: a 3D engine vendored into your project as source, asset generation, multiplayer and leaderboards, and one command that puts the game on bitmagic.ai.

This plugin teaches Claude Code to set it up.

Two commands, one at a time — the second needs the first to have finished:

```
/plugin marketplace add BitmagicAI/bitmagic-gdk-plugin
```

```
/plugin install bitmagic-gdk@bitmagic
```

Then say what you want to make. It installs the GDK, signs you in, scaffolds the project and starts the live dev view — after that the project's own `AGENTS.md` takes over, and `bitmagic upgrade` keeps *that* current with the engine.

Requires [Bitmagic Pro](https://bitmagic.ai/pro/) and Node.js 20+.

Licensed under the PolyForm Shield License 1.0.0 with Bitmagic's games permission — the same terms as the GDK itself. See [LICENSE.md](./LICENSE.md).

## Not using Claude Code?

This repo is also an [agent skills](https://agentskills.io) package, so one command installs it into any other agent:

```
npx skills add BitmagicAI/bitmagic-gdk-plugin -g -a cursor
```

Swap `-a` for your own tool — cursor, codex, kiro-cli, github-copilot, windsurf, opencode and ~70 more (`npx skills find` lists them). Keep the `-a`: without it, a non-interactive run installs into every agent the tool knows. `-g` installs it for every project, which is the point — the skill is for the stretch before a project exists.

Claude Code creators should still use the plugin above: it also ships the `/bitmagic-setup` command, which a bare skill install does not.

No npm, or an agent the tool does not know? Paste the block from https://bitmagic.ai/gdk/ into the file your agent reads at startup.
