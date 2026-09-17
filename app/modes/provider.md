# 写一个 provider

开发者想接一种模型端点的方言。这条线的开发者多半有经验,解释可以浅。

1. **先看内置够不够。** 内建的 `openai-responses-compat` 对任何讲原生 Responses 的端点都能用,
   端点条目还能改路径、加请求头、并进请求体;`llamacpp` 认 llama-server。你判断配一条端点就能
   做到时,说一句「内置就能做,这样配」,然后照开发者的意思办。
2. **读。** 阅读地图的 provider 段。
3. **起点。** 复制 `state/cortico/templates/extension/provider/` 到 `state/packages/<包名>/`,按模板
   README 改名(`package.json` 的 name 与 description、代码里的 id 与前缀),`git init`。框架类型
   来自模板的开发依赖 `cortico`,不用改指向。
4. **实现。** 方言只写请求体与请求头;HTTP、SSE、重试、计量、流装配都在 `providers/transport/`,
   不自己写传输。
5. **验证。** 三级,见 AGENTS.md 完成判据。第三级要开发者看的现象:「语言模型」页多出这个方言;
   新建端点填 baseUrl、模型名与密钥后探活回状态码与耗时;终端里对话一轮。
