# AI Agent不再失忆的新思路

每次打开新的 AI Coding 对话，我都要重新解释一遍项目的技术栈、代码结构、之前的 bug 修到哪里了。这种"每次重启都是陌生人"的感觉，你一定懂。

**agentmemory**  这个项目，就是来解决这个问题的。

# 它是什么

agentmemory 是一个**持久化记忆系统** ，专门给 AI Coding 代理（Agent）用。它能悄无声息地记录你在项目里做了什么、发现了什么、决定选了什么方案，然后在下一次对话时把这些信息自动注入进来。

一句话总结：**它让 AI Agent 有长期记忆，不再每次都失忆。**

GitHub 数据：

- ⭐ **3,454**  总 Stars

- **今日 +533** （增速相当猛）

# 解决什么问题

你可能试过用 CLAUDE.md、.cursorrules 这类内置记忆文件。它们有两个硬伤：

1. **容量上限** ——200 行之后就塞不下了

2. **容易过时** ——每次手动更新，很容易和实际代码脱节

agentmemory 的做法是**自动化** ：它自动追踪 AI Agent 的操作、压缩成可检索的记忆，在下次会话时主动注入正确的上下文。

官方的例子很生动：

> Session 1 你配置了 JWT 认证。Session 2 你要求加 Rate Limiting。Agent 直接知道你的 auth 模块用的是 `jose` 中间件，在 `src/middleware/auth.ts`，测试覆盖了 token 验证，而且选 jose 是因为 Edge 兼容性。不需要你再说一遍。

# 三个值得关注的点

**1. 数字说话，不是情怀**

在 LongMemEval-S（ICLR 2025，500题基准测试）上，agentmemory 达到了 R@5 = 95.2%、R@10 = 98.6% 的检索准确率，碾压 BM25-only 基线。

**2. Token 成本节省惊人**

| 方案 | 年消耗 Tokens | 年成本 |
|------|-------------|-------|
| 粘贴完整上下文 | 19.5M+ | 超出窗口上限 |
| LLM 摘要 | ~650K | ~$500 |
| agentmemory | ~170K | ~$10 |
| + 本地 Embedding | ~170K | **$0** |

用的 Embedding 模型是 `all-MiniLM-L6-v2`，本地运行，完全免费，不需要 API Key。

**3. 几乎支持所有主流 Agent**

Claude Code、Cursor、Copilot、Windsurf、Codex CLI、Gemini CLI、Cline、Goose、OpenCode……只要支持 MCP 或 REST API，就能接上。一个记忆服务，所有 Agent 共享。

# 个人启发

最让我意外的不是"记忆"这个功能本身，而是**它切入的角度** 。

Agent 赛道现在大部分在做"能力增强"——更强的推理、更长的上下文、更复杂的规划。但 agentmemory 做的是**减少重复摩擦** ：你不需要每次都重新建立上下文，这个价值更接近"开发效率工具"，而不是"AI 黑科技"。

从商业视角看，这类工具的天花板可能比底层模型低，但落地路径清晰——开发者付钱买的是"省时间"，而不是"更智能"。付费意愿反而可能更强。

感兴趣的可以直接试：

```
npx @agentmemory/agentmemory
```

官网：agent-memory.dev

> 来源：今日头条 | 原文链接：https://m.toutiao.com/is/pDS9yds6s6A/