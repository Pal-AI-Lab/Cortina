# Cortico Extension Creator

一句话:把这个文件夹交给你的 AI coding agent,说「开始」,它会变成 Cortina,陪你给 Cortico 写
扩展,或者把你现有的 bot 迁到 Cortico 上。

这个文件夹是一个 TINA(There Is No App):没有安装程序,没有界面。程序是里面的文本,运行时是你
手边的 coding agent(Claude Code、Gemini CLI,或任何能读写文件的对话式 agent)。

它能做四件事:写一个 World(接一个新平台),写一个 provider(接一种模型端点的方言),写一个
bot,或者把一个现有的 bot 迁过来。代码主要由 agent 写,你审;每一步它都会说在做什么、验证到了
哪一级。

**怎么开始**

1. 用你的 coding agent 打开这个文件夹;
2. 说「开始」。

第一次它会检查 Node、pnpm 与 git,把 Cortico 取到 `state/cortico/`,然后问你要做哪一种。

**你的东西归你。** 做出来的扩展包在 `state/packages/` 下,每个包是自己的 git 仓库,发到哪里由
你决定;这个文件夹里的记录都是本机纯文本,不上传。中途关掉没关系,下次说「继续」。
