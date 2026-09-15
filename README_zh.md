<!-- Owner: AGENTS.md(应用本体)、app/modes/ -->

<h1 align="center">Cortina</h1>

<p align="center">Cortico Extension Creator</p>

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
  <a href="#快速开始">快速开始</a> ｜
  <a href="#能做出什么">能做出什么</a> ｜
  <a href="#工作区">工作区</a> ｜
  <a href="#完成判据">完成判据</a> ｜
  <a href="https://github.com/Pal-AI-Lab/Cortico">Cortico</a> ｜
  <a href="https://github.com/Pal-AI-Lab/ThereIsNoApp">TINA Spec</a>
</p>

Cortina 陪你写 [Cortico](https://github.com/Pal-AI-Lab/Cortico) 的扩展:一个 World(接一个外部
环境)、一个 provider(接一种模型端点的方言)、一个 bot,或者把现有的 bot 迁到 Cortico 上。

这个文件夹是一个 TINA(There Is No App):程序是里面的文本,运行时是你手边的 coding agent
(Claude Code、Gemini CLI,或任何能读写文件的对话式 agent)。没有安装程序,没有界面。用 agent
打开这个文件夹,说「开始」,它读 `AGENTS.md`,成为 Cortina,一步一步带你做完。代码主要由它写,
你审;每一步它都会说在做什么、验证到了哪一级。

## 快速开始

需要 Node 22 以上、corepack 与 pnpm、git。Cortico 的仓库暂未公开,clone 需要有权限的账号,或者
你本机已有的 checkout。

```bash
git clone https://github.com/Pal-AI-Lab/Cortina.git
```

用你的 coding agent 打开这个文件夹,说 **开始**。

第一次运行时它会检查 Node、pnpm、git 与 GitHub 的可达性,每一项不通都给出路;把工作区纳入 git
并做首次提交;把 Cortico 取到 `state/cortico/` 并装依赖;然后问你要做四件事里的哪一件。中途关掉
没关系,下次说 **继续**:Cortina 从 `state/JOURNAL.md` 与 `state/design/` 恢复进度,先报告上次
做到哪,再问你下一步。

## 能做出什么

| 入口 | 产出 | 做成了你会看见 |
|---|---|---|
| **World** | 一个 `cortico-world-*` 包 | 扩展页卡片显示「已加载」;World 总览多一张卡;时间线里出现这个 World 的事件;让 bot 调一个工具,回执回来 |
| **provider** | 一个 `cortico-provider-*` 包 | 「语言模型」页多出这个方言;新建端点填好 baseUrl、模型名与密钥后探活回状态码与耗时;终端里对话一轮 |
| **bot** | 一个 `cortico-bot-*` 包 | 控制台标题是这个 bot 的 displayName;终端里对话一轮;Memory 目录里有它写的东西 |
| **迁移** | 先是一份你确认的预案,然后是预案列出的包 | 每个包同上 |

迁移从你旧 bot 的目录开始,那个目录在工作区之外,Cortina 经你同意才读,而且只读不改。它把旧实现
映射到 Cortico 的四层——上下文怎么拼归 Persona、内部状态怎么持久化归 Memory、每一路外部 IO 归
一个 World、会话生命周期归 session 声明——交给你一份预案,写明包清单、旧历史数据怎么处理、哪些
机制照搬并标成 fallback。预案确认前不动手写包。

包住在 `state/packages/`,每个是自己的 git 仓库。发到哪里由你决定;Cortina 不给它们接任何远端。

## 工作区

| 路径 | 装什么 |
|---|---|
| `AGENTS.md` | 应用本体:Cortina 是什么、怎么工作、不变量。agent 的唯一入口 |
| `app/opening.md` | 开场白原文,每次会话第一段原样输出 |
| `app/reading-map.md` | 阅读地图:每种活读 Cortico clone 里的哪几份文件 |
| `app/modes/` | 四种入口各一份流程:`world.md`、`provider.md`、`bot.md`、`migrate.md` |
| `app/facts.md` | 会过期的事实:Cortico 仓库地址、版本要求、命令 |
| `state/JOURNAL.md` | 日志,里程碑与会话结束前写 |
| `state/design/<包名>.md` | 每个包一份设计记录,一条决定一段,写理由 |
| `state/cortico/` | Cortico 的 clone,构建期现读,不进本工作区的 git |
| `state/packages/<包名>/` | 做出来的扩展包,每个是自己的 git 仓库,不进本工作区的 git |

`app/` 是程序本体,运行期间只读。改它等于改应用本身,要你知情同意,并把改动与理由单独记一次
提交。

Cortina 不另存一份 Cortico 的规矩。关于「扩展该怎么写」的一切判断——层的边界、命名约定、模板、
校验脚本——都在用到时从 `state/cortico/` 的 clone 里现读,所以不会随 Cortico 的变化过期。发现
Cortico 文档里没有的规矩,它提议你提给 Cortico,而不是记在这里。

## 完成判据

一个扩展包做完,当且仅当三条都成立:

1. **构建过。** 包内 `pnpm typecheck` 与 `pnpm test` 绿。Cortina 自己跑。
2. **装载过。** 在 `state/cortico/` 下 `pnpm check:extension <包目录>` 通过,含干装载。Cortina
   自己跑。
3. **行为目击。** 装进你的实例,看见上表写的现象。这一级只有你能看。

Cortina 报到哪一级就说到哪一级,不会把没验过的包说成能用。

## 环境与能力声明

需要:Node 22 以上、corepack 与 pnpm、git。网络只用于从 GitHub 取 Cortico 与从 npm registry 装
依赖。

Cortina 承诺:不在本工作区之外读写,除了你明确指定并同意的目录;你的平台凭证不进工作区;不把
工作区内容发给任何远端服务;除取 Cortico 外不连接任何远程 git 仓库。它不 push、不 publish、不改
你跑着的 Cortico 实例——这些动作它只描述步骤,由你执行,除非你明确要它做。

扩展的密钥住在部署的 `.env`,代码经 `secret(名字)` 取,包目录里不带。交付前 Cortina 会搜一遍包
里有没有密钥形状的字符串。

## TINA

Cortina 遵循 [TINA Spec 0.1](https://github.com/Pal-AI-Lab/ThereIsNoApp)。它的 `AGENTS.md` 逐字
嵌入协议不变量 I1–I7:从 `AGENTS.md` 进入、子工作区的 README、状态跨会话持久化、在应用里工作与
修改应用本身的分界、存档、指令优先级、行动范围。

对默认存档策略的一处偏离写在 `AGENTS.md` 里:本工作区的 git 存档 `app/`、`state/design/` 与
`state/JOURNAL.md`;Cortico 的 clone 与做出来的包是它们自己的 git 仓库,从不作为内嵌仓库进来。

## 相关

- [Cortico](https://github.com/Pal-AI-Lab/Cortico) —— 这些扩展所服务的事件流 Agent Harness。
- [TINA Spec](https://github.com/Pal-AI-Lab/ThereIsNoApp) —— Cortina 遵循的规范。
- [Meta TINA](https://github.com/Pal-AI-Lab/META-TINA) —— 参考实现:一个访谈领域专家、产出新
  TINA 的 TINA。

## 许可

MIT,见 [LICENSE](LICENSE)。
