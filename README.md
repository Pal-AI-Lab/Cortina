<!-- Owner: AGENTS.md, app/modes/, app/facts.md -->

<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="assets/cortina-banner-dark.png">
    <img src="assets/cortina-banner.png" alt="Cortina" width="600">
  </picture>
</p>

<p align="center">Easily build Cortico extensions tailored to you with Coding AI</p>

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
  <a href="#what-you-can-build">What You Can Build</a> ｜
  <a href="#get-started">Get Started</a> ｜
  <a href="#working-together">Working Together</a> ｜
  <a href="#inside-the-folder">Inside the Folder</a>
</p>

Want your [Cortico](https://github.com/Pal-AI-Lab/Cortico) Bot to join a game platform or call
a new model API? Or want to move an existing bot to Cortico? Cortina helps you turn those
ideas into extension packages.

Cortina's program is a set of text instructions that any coding agent (Codex, DeepSeek
Harness, and others) can run. Clone this repository, open the folder with the agent you
already use, and say “start” to begin.

You don't need to know how to program in TypeScript or understand Cortico's internal
structure. Describe what you want to build, and the agent guides you through the whole
process: clarifying requirements, writing code, testing, and checking the installation.
It explains key designs and changes to help you review the work and confirm the results.

## What You Can Build

| Your idea | Extension | Output |
|---|---|---|
| Connect a bot to a platform, game, or device | **Cortico World**: turns external changes into events the bot can observe, and available actions into tools | A `cortico-world-*` package |
| Call a model API | **Provider**: adapts requests to a model service's format | A `cortico-provider-*` package |
| Create your own bot | **Cortico Bot**: combines a Persona (how context and behavior are organized), Memory (persistent internal state), and Worlds | A `cortico-bot-*` package |
| Move an existing bot to Cortico | **Bot migration**: maps the old code and data, then implements an agreed plan | A migration plan and the extension packages it lists |

For example, start with “I want my bot to notice new messages in a game and send a reply.”
Cortina helps you decide which changes the bot should hear about and which actions it
can take, then builds the Cortico World around those choices.

## Get Started

You will need:

- A coding agent that can edit project files and run terminal commands, such as Codex,
  DeepSeek Harness, or any other coding agent.
- A local clone of this repository:

```bash
git clone https://github.com/Pal-AI-Lab/Cortina.git
cd Cortina
```

Open this directory with your coding agent and send:

> start

It asks what you want to build, then checks your development tools, sets up Git
checkpoints, and downloads Cortico into `state/cortico/` along with the dependencies
it needs.

Unsure which kind of extension you need? Choose the option to learn about Cortico first.
To resume later, open the same directory and say “continue”: Cortina reads the saved
journal and design notes, then tells you where you left off.

## Working Together

**You choose the behavior; the agent implements it.** Describe what you want and provide
relevant platform documentation. The agent reads Cortico's documentation and source,
explains design choices and tradeoffs, then writes code and tests. Review what it produces;
ask it to explain any part you need to understand before making a decision.

**Progress is saved at each milestone.** Design decisions go in `state/design/`, progress
in `state/JOURNAL.md`. Extension packages live in `state/packages/`, each with its own
Git history.

**Migration starts with a plan.** With your permission, the agent reads your old bot's
directory without changing it. It maps the code, memories, and history, then lists the
Cortico Bot and Cortico Worlds to implement.

## Inside the Folder

| Path | Contents |
|---|---|
| [`AGENTS.md`](AGENTS.md) | The agent's entry point, workflow, and permitted operations |
| [`app/`](app/README.md) | Opening text, source-reading guides, four development workflows, and environment requirements |
| `state/JOURNAL.md` | Completed work and next steps |
| `state/design/` | Design decisions and reasons for each package |
| `state/cortico/` | The Cortico repository used during development |
| `state/packages/` | Generated extensions, each with its own Git repository |

The workspace's Git history covers the application files, journal, and design notes; the
Cortico checkout and extension packages are kept outside it. During normal development,
`app/` is read-only; changing its instructions needs your consent and a separate commit
explaining why. The agent reads extension contracts, naming rules, and templates from
`state/cortico/` as needed. If a rule is missing, it suggests raising it with Cortico.

Cortina follows [TINA Spec 0.1](https://github.com/Pal-AI-Lab/ThereIsNoApp) (There Is No App):
text defines the application, a coding agent runs it, and files preserve progress.
See [`AGENTS.md`](AGENTS.md) for the protocol and operating rules.

## Related Projects

- [Cortico](https://github.com/Pal-AI-Lab/Cortico): the framework that runs these extensions.
- [TINA Spec](https://github.com/Pal-AI-Lab/ThereIsNoApp): the specification for text applications.
- [Meta TINA](https://github.com/Pal-AI-Lab/META-TINA): a reference implementation that creates
  TINAs by interviewing domain experts.

## License

MIT. See [LICENSE](LICENSE).
