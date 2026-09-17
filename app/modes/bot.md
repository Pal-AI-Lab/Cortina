# 写一个 bot

开发者想造一个自己的 bot:一个 Persona、它的 Memory、它挂哪些 World。这条线爱好者多,解释
深一点。

1. **先读 PHILOSOPHY.md。** 人格 bot 的审美那三条与 World 那一段,是这条线最常踩的坑;写之前读,
   写完对照。然后读阅读地图的 bot 段。
2. **定边界。** 写进 `state/design/<包名>.md`:Memory 长什么样、放哪;几个 session;声明哪些
   World;默认端口。
3. **起点。** 最小的:复制 `state/cortico/templates/extension/bot/`。完整的:把 `bots/cormini/`
   整个目录复制进包里再改;npm 上的 `cortico` 包只带扩展契约那部分源码,`bots/` 不在里面,
   所以 cormini 只能复制。按模板 README 改名(`package.json` 的 name 与 description、代码里的
   id 与前缀),`git init`;框架类型来自开发依赖 `cortico`,不用改指向。
4. **实现。** 对照 `docs/personas.md` 的契约表。前缀的每个字来自模板文件,Core 不写字;要让
   开发者在控制台里改的提示词,在声明里给部署侧的 `deploymentPath`。
5. **部署。** 装好后一份部署这样用它:`deployment.json` 写 `{ "bot": "<包名>" }`。bot 的 id 不得
   与仓内 `bots/` 目录同名;包目录只读。
6. **验证。** 三级,见 AGENTS.md 完成判据。第三级要开发者看的现象:部署起来,控制台标题是它的
   `displayName`;终端里对话一轮;Memory 目录里有它写的东西。
