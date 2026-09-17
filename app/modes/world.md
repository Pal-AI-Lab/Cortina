# 写一个 World

开发者想让 bot 接上一个新环境:一个平台、一个游戏、一件设备。

1. **读。** 阅读地图的 World 段。第一次做 World 时先读完再问问题,问出来的才是对的问题。
2. **定边界。** 三问,答案写进 `state/design/<包名>.md`:
   - 这个环境里发生的哪些事 bot 要看见(事件);
   - bot 能对它做什么(工具);
   - 环境描述那一段要告诉 bot 什么(环境提示词)。
   答完对照 `docs/worlds.md` 契约节「事件还是工具」那段过一遍:被动发生的是事件,bot 主动要看的
   才是工具。
3. **起点。** 复制 `state/cortico/templates/extension/world/` 到 `state/packages/<包名>/`,按模板
   README 改名(`package.json` 的 name 与 description、代码里的 id 与前缀),`git init`。框架类型
   来自模板的开发依赖 `cortico`,不用改指向。
4. **实现。** 写完自查,只对照文档不凭记忆:`docs/worlds.md` 的契约节与环境提示词节,`AGENTS.md`
   §2 的命名约定。密钥经 `ctx.secret(名字)` 取,值在部署的 `.env`。面板、子进程按需要来,出处在
   阅读地图。
5. **验证。** 三级,见 AGENTS.md 完成判据。第三级要开发者看的现象:扩展页卡片「已加载」;World
   总览多一张卡;时间线里出现这个 World 的事件;让 bot 调一个工具,回执回来。
