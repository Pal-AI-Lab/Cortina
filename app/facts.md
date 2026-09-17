# 事实(2026-09-17)

会过期的东西都在这里,过期只改这一份。

## Cortico

- 仓库:https://github.com/Pal-AI-Lab/Cortico,公开,跟 main,不钉版本。本工作区里没有随框架过期的
  东西:原则、模板、校验脚本都在 clone 里现读。
- 开发者本机已有 checkout 的,直接从本地路径 clone,不做链接:`git clone <本地路径> state/cortico`。
- 取:`git clone https://github.com/Pal-AI-Lab/Cortico.git state/cortico`,然后在 `state/cortico/`
  下 `corepack pnpm install`。
- 更新:在 `state/cortico/` 下 `git pull`,再 `corepack pnpm install`。
- 扩展契约版本不记在这里,读 `state/cortico/src/extensions/manifest.ts` 的 `EXTENSION_API_VERSION`。

## 环境

- Node 22 以上;pnpm 由 corepack 按 `package.json` 的 `packageManager` 钉版本(现在是 11);git。
- 出路:Node 装 nodejs.org 的 LTS;corepack 没启用就 `corepack enable`;GitHub 到不了就从本地
  路径 clone。

## 命令

| 在哪 | 命令 | 作用 |
|---|---|---|
| 包目录 | `corepack pnpm install` | 装依赖 |
| 包目录 | `pnpm typecheck && pnpm test` | 第一级 |
| `state/cortico/` | `pnpm check:extension <包目录>` | 第二级,含干装载 |
| 开发者的实例 | 控制台「扩展」页「手动安装」填包目录的绝对路径,重启进程 | 第三级的前置,由开发者做 |
