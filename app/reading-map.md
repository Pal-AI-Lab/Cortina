# 阅读地图

关于「Cortico 的扩展该怎么写」的判断都在 `state/cortico/` 里,这份只说去读哪几份。路径以 clone
里此刻的为准,文件搬了就搜。读到的规矩与你的常识冲突时,以文档为准,并把冲突告诉开发者。

## 所有入口先读

| 文件 | 读什么 |
|---|---|
| `PHILOSOPHY.md` | Cortico 是什么、不是什么;四层;三条工程准则;人格 bot 的审美 |
| `AGENTS.md` §1–3 | 设计立场、命名约定、边界 |
| `docs/extensions.md` | manifest、安装、三种 kind 的写法、自描述、校验、契约版本 |
| `templates/extension/README.md` | 三个模板怎么复制、改名、验证,发布前做什么,装进实例后该看见什么 |

## World

| 文件 | 读什么 |
|---|---|
| `docs/worlds.md` | 契约与触发档位;环境提示词与工具 description 的分工;PWSR |
| `src/core/types.ts` 里的 `World`、`WorldHost`、`ToolDef`、`EventEnvelope` | 契约原文与注释 |
| `src/world.ts` | `WorldDefinition`、`WorldContext`,装配层怎么对待一个定义 |
| `src/worlds/websearch/` | 最短的 World,只有工具 |
| `src/worlds/console/` | 有事件、有环境提示词的 World |
| `templates/extension/world/` | 起点 |
| `tests/helpers/fake-host.ts` | 测试用的假宿主,模板里有一份副本 |
| 要面板时:`docs/webui.md`、`src/web/shared/client-panel.ts`、`src/worlds/qq/webui/client.ts` | 面板契约与一个实例;打包脚本看任一外部扩展包的 `scripts/build-webui.mjs`(旧包叫 `build-console.mjs`) |

## provider

| 文件 | 读什么 |
|---|---|
| `docs/providers.md` | 端点表、内建两个模块能做什么、传输、计价 |
| `src/providers/README.md` | 三个接口、注册与解析、transport 各文件的分工 |
| `src/providers/base.ts` | `ProviderModule`、`ProviderInstance`、`ProviderHost` 原文 |
| `src/providers/transport/chat.ts`、`src/providers/transport/responses-input.ts` | Chat 与 Responses 两种投影;方言只写请求体与请求头 |
| `src/providers/openai-responses-compat/`、`src/providers/llamacpp/` | 内建两个模块 |
| `templates/extension/provider/` | 起点 |

## bot

| 文件 | 读什么 |
|---|---|
| `docs/personas.md` | Persona 契约、bot 定义、包里有什么 |
| `bots/README.md` | 包与部署的分界;加一个新 bot 的两条路 |
| `src/core/types.ts` 里的 `Persona`、`SessionDecl`、`CoreApi` | 契约原文 |
| `src/bot.ts` 里的 `BotDefinition`、`BotParts`、`WebUiContribution` | 装配定义 |
| `docs/sessions.md`、`docs/configuration.md`、`docs/deployment.md` | session、配置四层、部署目录 |
| `bots/cormini/` | 最小完整实现;要完整参考就复制它,扩展包 import 不到它 |
| `templates/extension/bot/` | 起点 |

## 迁移

上面 bot 与 World 两节全部,再加:

| 文件 | 读什么 |
|---|---|
| `bots/cormini/persona/memory.ts` | 「工作区即记忆」的一种做法 |
| `docs/runs.md` | 事件库与日志的落盘形状,历史数据往哪搬 |

## 校验与排错

| 文件 | 读什么 |
|---|---|
| `scripts/extension-check.ts`、`src/extensions/dry-mount.ts` | `pnpm check:extension` 查什么、怎么判 |
| `scripts/extension-describe.ts`、`src/extensions/describe-export.ts` | `pnpm describe:extension` 导出什么 |
| `docs/upgrading.md` | 旧契约的包怎么改到当前版本 |
| `docs/development.md` | 命令、两份 tsconfig、测试布局 |
| `docs/runs.md` | `pnpm logq`;装进实例后出问题看哪里 |

## 发布

| 文件 | 读什么 |
|---|---|
| 包里的 `AGENTS.md`(原件 `templates/extension/<kind>/AGENTS.md`) | 发布清单 |
| `docs/extensions.md` 的 manifest 可选字段、「自描述」与「市场的官方索引」两节 | `tags`、`locales`、`screenshots`、`describe`、`CHANGELOG.md`;市场从哪读这些 |
| `src/extensions/author-guide.ts` | `check:extension` 最后「Tags」「Before publishing」两段查什么,申请格式从哪来 |
