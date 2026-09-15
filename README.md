<!-- Owner: AGENTS.md (the app), app/modes/ -->

<h1 align="center">Cortina</h1>

<p align="center">Cortico Extension Creator</p>

<p align="center">
  English ｜
  <a href="README_zh.md">简体中文</a>
</p>

<p align="center">
  <a href="https://github.com/Pal-AI-Lab/ThereIsNoApp"><img alt="TINA Spec 0.1" src="https://img.shields.io/badge/TINA%20Spec-0.1-6E56CF"></a>
  <img alt="Node ≥ 22" src="https://img.shields.io/badge/node-%E2%89%A5%2022-00A870">
  <img alt="version 0.1.0" src="https://img.shields.io/badge/version-0.1.0-8A8496">
  <a href="LICENSE"><img alt="MIT" src="https://img.shields.io/badge/license-MIT-00A870"></a>
</p>

<p align="center">
  <a href="#quick-start">Quick Start</a> ｜
  <a href="#what-cortina-builds">What It Builds</a> ｜
  <a href="#workspace">Workspace</a> ｜
  <a href="#definition-of-done">Definition of Done</a> ｜
  <a href="https://github.com/Pal-AI-Lab/Cortico">Cortico</a> ｜
  <a href="https://github.com/Pal-AI-Lab/ThereIsNoApp">TINA Spec</a>
</p>

Cortina writes [Cortico](https://github.com/Pal-AI-Lab/Cortico) extensions with you: a World
(one external environment), a provider (one model-endpoint dialect), a bot, or a migration of
an existing bot onto Cortico.

This folder is a TINA — There Is No App. The program is the text inside it and the runtime is
the coding agent you already use: Claude Code, Gemini CLI, or any agent that reads and writes
files. There is no installer and no interface. You open the folder with your agent and say
"start"; the agent reads `AGENTS.md`, becomes Cortina, and takes the work one step at a time.
It writes most of the code and you review it. At every step it says what it is doing and which
level of verification it has reached.

## Quick Start

Node 22 or newer, corepack with pnpm, and git. Cortico's repository is private for now, so the
clone needs an account with access to it, or a checkout already on your machine.

```bash
git clone https://github.com/Pal-AI-Lab/Cortina.git
```

Open the folder with your coding agent and say **start**.

The first session checks Node, pnpm, git and GitHub reachability and gives a way forward for
each; puts the workspace under git and makes a first commit; clones Cortico into
`state/cortico/` and installs its dependencies; then asks which of the four kinds of work you
want. Close the session whenever you like and say **continue** next time: Cortina recovers
where it left off from `state/JOURNAL.md` and `state/design/`, and reports it back before
asking anything.

## What Cortina Builds

| Kind | Result | What you see when it works |
|---|---|---|
| **World** | a `cortico-world-*` package | the extension card reads loaded; a card appears in the World overview; the World's events show up in the timeline; a tool call comes back with a receipt |
| **provider** | a `cortico-provider-*` package | the dialect appears on the language-model page; a new endpoint filled with base URL, model name and key probes back a status code and a latency; one conversation turn in the terminal |
| **bot** | a `cortico-bot-*` package | the console title is the bot's display name; one conversation turn in the terminal; the Memory directory holds what the bot wrote |
| **migration** | a plan you approve, then the packages it lists | each package as above |

A migration starts from your old bot's directory, which Cortina reads only after you agree and
never writes to. It maps the old implementation onto Cortico's four layers — context assembly
to the Persona, persistent internal state to Memory, each external IO to a World, session
lifecycle to the session declarations — and hands you a plan naming every package, what happens
to the old history data, and which mechanisms are carried over as fallbacks. Nothing is built
until you confirm the plan.

Packages live in `state/packages/`, one git repository each. Where they are published is your
decision; Cortina never connects them to a remote.

## Workspace

| Path | Holds |
|---|---|
| `AGENTS.md` | the app: what Cortina is, how it works, its invariants. The agent's only entry point |
| `app/opening.md` | the opening paragraph, emitted verbatim at the start of every session |
| `app/reading-map.md` | which files in the Cortico clone to read for which kind of work |
| `app/modes/` | one procedure per kind: `world.md`, `provider.md`, `bot.md`, `migrate.md` |
| `app/facts.md` | the facts that expire: Cortico's repository, version requirements, commands |
| `state/JOURNAL.md` | the log, written at every milestone and before a session ends |
| `state/design/<package>.md` | one design record per package: each decision with its reason |
| `state/cortico/` | the Cortico clone, read while building; outside this workspace's git |
| `state/packages/<name>/` | the packages produced, each its own git repository; outside this workspace's git |

`app/` is the program and is read-only while Cortina runs. Changing it means changing the
application, which takes your informed consent and is recorded as its own commit with the
reason for it.

Cortina keeps no second copy of Cortico's rules. Every judgment about how an extension is
written — the layer boundaries, the naming conventions, the templates, the check script — is
read from the clone in `state/cortico/` at the moment it is needed, so it does not go stale as
Cortico moves. A rule that turns out to be missing from Cortico's own documentation becomes a
suggestion to Cortico rather than a note kept here.

## Definition of Done

An extension package is done when all three hold:

1. **It builds.** `pnpm typecheck` and `pnpm test` are green in the package. Cortina runs this.
2. **It loads.** `pnpm check:extension <package dir>` passes in `state/cortico/`, dry mount
   included. Cortina runs this.
3. **It behaves.** Installed in your instance, it shows the behaviour listed above. Only you can
   see this one.

Cortina reports the level it actually reached and never calls an unverified package working.

## Environment and Capabilities

Required: Node 22 or newer, corepack with pnpm, and git. Network access is used to clone
Cortico from GitHub and to install dependencies from the npm registry.

Cortina promises to: read and write nothing outside this workspace, except a directory you name
and agree to; keep your platform credentials out of the workspace; send no part of the
workspace to any remote service; connect to no remote git repository other than the one it
fetches Cortico from. It does not push, publish, or change your running Cortico instance —
those steps it describes and you run, unless you ask it to do them for you.

Extension secrets live in the deployment's `.env` and are reached through `secret(name)`, so
package directories carry none. Cortina searches a package for secret-shaped strings before
handing it over.

## TINA

Cortina conforms to [TINA Spec 0.1](https://github.com/Pal-AI-Lab/ThereIsNoApp). Its
`AGENTS.md` embeds the protocol invariants I1–I7 verbatim: entry through `AGENTS.md`,
sub-workspace READMEs, persistence of state across sessions, the line between working in the
app and modifying it, archival, precedence of instructions, and scope.

One deviation from the default archival policy is declared in `AGENTS.md`: this workspace's git
covers `app/`, `state/design/` and `state/JOURNAL.md`; the Cortico clone and the packages are
git repositories of their own and are never embedded in it.

## Related

- [Cortico](https://github.com/Pal-AI-Lab/Cortico) — the event-stream agent harness these
  extensions are written for.
- [TINA Spec](https://github.com/Pal-AI-Lab/ThereIsNoApp) — the specification Cortina is built
  on.
- [Meta TINA](https://github.com/Pal-AI-Lab/META-TINA) — the reference TINA, which interviews
  domain experts and produces new TINAs.

## License

MIT. See [LICENSE](LICENSE).
