---
name: bitmagic-gdk-setup
description: Use when someone asks to build, make, or ship a game with Bitmagic or the Bitmagic GDK, mentions the bitmagic command or Bitmagic Pro, or is starting a Bitmagic game and has no project yet. Installs the GDK, signs them in, scaffolds the project and starts the live dev view, then hands off to the project's own AGENTS.md.
---

# Setting up the Bitmagic GDK

The Bitmagic GDK is a game development kit for agents: a 3D engine vendored into the project
as source, asset generation for characters, vehicles and skyboxes, multiplayer and
leaderboards on Bitmagic's servers, and one command that puts the game on bitmagic.ai. Every
command is `bitmagic <verb>`; the npm package is still named `@bitmagic/cli`.

This skill covers exactly one stretch of that: getting from nothing to a scaffolded project
with the dev view running. Everything after the scaffold is written down inside the project
itself and supersedes this file.

**Already inside a Bitmagic project?** If `bitmagic.json` sits in this directory or a parent,
setup is done — go straight to step 6.

## 1. Is the GDK installed?

```
bitmagic --version
```

Not found? Install it, then **check again**:

```
npm install -g @bitmagic/cli
bitmagic --version
```

The second check is not a formality. Your shell is non-interactive and sources no profile, so
under nvm the `npm` you just ran can belong to a different node than the one on `PATH`: the
install lands in a prefix nothing points at, reports success, and leaves `bitmagic` missing.
If the re-check still fails, report the directory `npm prefix -g` names and ask the human to
run the install line in their own terminal. Do not route around it with a second package
manager, and do not carry on to step 2 — every command below would fail for a reason that
looks nothing like this one.

The GDK needs Node.js 20 or newer; check `node --version` if the install itself fails.

From here on it updates itself with `bitmagic self-update`, which reinstalls into the place it
actually lives. Never `npm i -g` a second time.

## 2. Are they signed in, and subscribed?

```
bitmagic whoami --json
```

**Exit code 2 means not logged in.** Then:

```
bitmagic login
```

Run it **in the background**, and show the human the URL and the code it prints. `bitmagic
login` deliberately never opens a browser — handing over that code is the whole job of the
command — and it blocks polling for approval, so a foreground run buries the code in output
nobody is reading. Wait for them to approve.

The GDK is what a Bitmagic Pro subscription opens, and there is no other way in. If they do
not have one, `login` carries straight on into checkout, which *does* open a browser, and
where they either subscribe or redeem a voucher. Wait for that too, then confirm with
`bitmagic whoami`.

## 3. Ask what they want to make

One line, in their words, before you scaffold anything. Do not invent a concept and do not
skip ahead: that line seeds `GAME-DESIGN.md` **and** picks the starting template. "A
doom-like corridor shooter" scaffolds first-person; "jump between floating islands"
scaffolds a sidescroller.

## 4. Scaffold the project

```
bitmagic init my-game --idea "<their line>" --original-prompt "<their line>"
```

Name the directory after their idea. This mints the game, vendors the engine, and writes
`AGENTS.md`, `GAME-DESIGN.md` and the project's own skills. Work inside that directory from
now on. `--original-prompt` carries their words, verbatim, to the people who make the GDK
better — the project's own skills ask for it on every later command too.

The skills land where your agent looks without being told: `.agents/skills/` (Cursor, Codex,
Copilot, Cline, OpenCode) and `.claude/skills/` are both written every time. **If you are
Kiro**, add `--agent kiro` so `.kiro/skills/` and a steering file are written too.

## 5. Start the dev view — now, not at the end

```
bitmagic dev
```

**Run it as a background task.** It never exits: in the foreground it blocks until the
session is killed, and left until last it is a server nobody needed.

Then tell the human the URL, once, in your reply. Take it from what the command printed
rather than assuming 3011 — each project on the machine has its own fixed ports, and
`.bitmagic/dev.json` records what it actually bound. Everything `bitmagic dev` prints goes
into a background log the human never opens, so a URL you do not say out loud is a URL
nobody got.

That page is the point of the whole arrangement: the game reloads itself on every change and
the assets panel lists each character, vehicle and skybox as it is generated. A game that
appears in one silent hour is worth less than a rough one they watched arrive, because they
could steer the first.

## 6. Hand off — this skill is finished

Read `AGENTS.md` at the project root. It names the skills directory your own agent loads —
`bitmagic init` writes one for each — and both describe this engine and this version of the
GDK. `bitmagic upgrade` keeps them current, and **they outrank everything here**. Follow them
from now on and stop consulting this file.

## While you are doing the above

- **Never** run `bitmagic allowance --allow-sparks`. It authorises spending the human's own
  money, and refuses to run outside a real terminal for that reason.
- **Never** run `bitmagic reset-account`. It deletes their account.
- Ask before `bitmagic publish`.
- Under `--json`, stdout carries exactly one JSON document and everything else goes to
  stderr. Branch on the exit code, not on prose: `2` not logged in, `3` verify missing or
  failed, `5` not the owner.
- A `.bitmagic-env` file here or in a parent aims these projects at a non-production server
  on purpose. Leave it alone, and do not pass `--env` to anything.
