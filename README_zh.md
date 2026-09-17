<!-- Owner: AGENTS.md、app/modes/、app/facts.md -->

<h1 align="center">Cortina</h1>

<p align="center">使用 Coding AI 轻松编写为你量身定制的 Cortico 扩展</p>

<p align="center">
  <a href="README.md">English</a> ｜
  简体中文
</p>

<p align="center">
  <a href="https://github.com/Pal-AI-Lab/ThereIsNoApp"><img alt="TINA Spec 0.1" src="https://img.shields.io/badge/TINA%20Spec-0.1-6E56CF"></a>
  <img alt="Node ≥ 22" src="https://img.shields.io/badge/node-%E2%89%A5%2022-00A870">
  <img alt="version 0.1.0" src="https://img.shields.io/badge/version-0.1.0-8A8496">
  <a href="LICENSE"><img alt="MIT" src="https://img.shields.io/badge/license-MIT-00A870"></a>
</p>

<p align="center">
  <a href="#能做什么">能做什么</a> ｜
  <a href="#开始使用">开始使用</a> ｜
  <a href="#怎么一起做">怎么一起做</a> ｜
  <a href="#目录结构">目录结构</a>
</p>

想让你的 [Cortico](https://github.com/Pal-AI-Lab/Cortico) Bot 接上游戏平台、调用新的模型接口，
或者把已有的 bot 迁到 Cortico？Cortina 陪你把这些想法做成扩展包。

Cortina 的程序是一组文本指令，使用任意 Coding Agent（例如：Codex, DeepSeek Harness等等）即可执行。
Clone 本库到本地，用你已有的 Agent 打开这个文件夹，说「开始」，就能开始开发流程。

你不需要了解具体的 TypeScript 编程，也不必先熟悉 Cortico 的内部结构。只需要说明你想做什么，Agent
会引导你完成从需求确认、代码编写到测试和安装验证的全程，并解释关键设计和改动，帮助你审阅和确认效果。

## 能做什么

| 你的想法 | 对应的扩展 | 产出 |
|---|---|---|
| 让 bot 接入一个平台、游戏或设备 | **Cortico World**：把外部变化变成 bot 能观察的事件，把可执行的操作变成工具 | `cortico-world-*` 包 |
| 让 bot 调用一种模型接口 | **Provider**：适配模型服务的请求格式 | `cortico-provider-*` 包 |
| 做一个自己的 bot | **Cortico Bot**：组合 Persona（上下文与行为组织方式）、Memory（持久保存的内部状态）和 World | `cortico-bot-*` 包 |
| 把已有的 bot 迁到 Cortico | **Bot 迁移**：梳理旧代码与数据，确认方案后逐个实现 | 迁移方案及其中列出的扩展包 |

比如，你可以从「我想让 bot 看见游戏里的新消息，还能发一句话」开始。Cortina 会和你确认哪些
变化需要通知 bot、允许它做哪些操作，再据此编写符合规范的 Cortico World。

## 开始使用

准备好：

- 一个能读写项目文件、运行终端命令的 Coding Agent，例如 Codex 或 DeepSeek Harness，或者任何 Coding Agent。
- 克隆此仓库到本地:

```bash
git clone https://github.com/Pal-AI-Lab/Cortina.git
cd Cortina
```

用 coding agent 打开这个目录，发送：

> 开始

它会先问你想做什么，再检查开发环境、准备 Git 存档，并将 Cortico 下载到 `state/cortico/`
，同时检查并安装必须的依赖。

还没想好做哪种扩展？可以先选「我还是不太懂？」来了解 Cortico。中途离开后，下次在同一目录说「继续」：Cortina
会读取保存的日志和设计记录，告诉你上次做到哪里。

## 怎么一起做

**你定用途，agent 负责实现。** 你说明想要的行为，提供必要的平台资料；agent 查阅 Cortico 的文档
和源码，提出设计选择、解释取舍，再写代码和测试。你需要审阅产出；不理解的地方，可以让它解释
到你能判断为止。

**每个阶段都有存档。** 设计决定保存在 `state/design/`，进度保存在 `state/JOURNAL.md`。
扩展包放在 `state/packages/`，各自用 Git 保存版本。

**迁移先看方案。** 经你同意后，agent 只读旧 bot 的目录，梳理代码、记忆和历史数据，整理出需要实现的Cortico Bot，
和 Cortico World 清单。

## 目录结构

| 路径 | 内容 |
|---|---|
| [`AGENTS.md`](AGENTS.md) | agent 的入口、工作方式与操作范围 |
| [`app/`](app/README.md) | 开场白、源码阅读指引、四种开发流程和环境要求 |
| `state/JOURNAL.md` | 已完成的工作与下一步 |
| `state/design/` | 每个包的设计决定和理由 |
| `state/cortico/` | 开发时参考的 Cortico 仓库 |
| `state/packages/` | 生成的扩展包，每个包有独立的 Git 仓库 |

工作区的 Git 保存应用文件、日志和设计记录；Cortico 仓库和扩展包不纳入这份存档。`app/` 在日常
开发中只读，修改其中的指令需要你同意，并单独提交改动和理由。关于扩展的契约、命名和模板，agent
会在需要时读取 `state/cortico/` 中的版本；发现规则缺失时，会建议向 Cortico 反馈。

Cortina 采用 [TINA Spec 0.1](https://github.com/Pal-AI-Lab/ThereIsNoApp)（There Is No App）：
用文本定义应用，由 coding agent 执行，并将进度保存在文件中。协议与操作规则见
[`AGENTS.md`](AGENTS.md)。

## 相关项目

- [Cortico](https://github.com/Pal-AI-Lab/Cortico)：扩展所运行的框架。
- [TINA Spec](https://github.com/Pal-AI-Lab/ThereIsNoApp)：文本应用的规范。
- [Meta TINA](https://github.com/Pal-AI-Lab/META-TINA)：通过访谈领域专家创建 TINA 的参考实现。

## 许可

MIT，见 [LICENSE](LICENSE)。
