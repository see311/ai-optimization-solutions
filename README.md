# AI 优化解决方案
AI 相关优化技术的实战经验与解决方案合集，涵盖 Agent 设计、RAG 检索、记忆系统、LLM 网关等多个方向。
## 目录结构
```
ai-optimization-solutions/
└── docs/
    ├── AI编程工具-Skills/         # AI 编程工具与 Skills 技能包
    ├── Agent智能体设计/           # Agent 智能体架构与设计模式
    ├── 记忆系统Memory/            # Agent 记忆系统与持久化方案
    ├── RAG检索增强/               # RAG 检索增强与优化实战
    ├── LLM网关架构/               # LLM 网关与生产级架构
    └── AI工具/                    # AI 相关工具与开源项目
```
每篇文章目录下包含：
- `原文.md` — 原始文章内容
- `总结.md` — 整理后的核心要点
## 内容概览
### AI编程工具-Skills (6篇)
| 文章 | 简介 |
|------|------|
| 浏览器自动化-从GUI到OpenCLI | 放弃不稳定的UI自动化，用API请求复现解决浏览器自动化难题 |
| 7个AI前端设计Skill去AI味 | 去除 AI 生成界面的"AI味"，7个实测好用的设计 Skill |
| AgentSkills-谷歌工程规范封装 | 谷歌开源 23000+ Star 的 Agent Skills 技能包 |
| Book2Skill重新定义RAG把PDF变成Claude的skill | 把PDF文档转化为AI可调用的结构化技能包 |
| Alumnium-AI端到端自动化测试 | AI 驱动端到端测试框架，支持自然语言生成测试用例和断言 |
| MiniMax-Skills-AI编程技能包 | MiniMax 官方的生产级开发技能包 |
| Alumnium-AI端到端自动化测试 | AI 驱动端到端测试框架，支持自然语言生成测试用例和断言，覆盖 Playwright/Selenium/Appium |

### Agent智能体设计 (16篇)
| 文章 | 简介 |
|------|------|
| NekroAgent跨平台Agent框架 | 开源跨平台多用户Agent框架，支持QQ/Discord/Minecraft/Bilibili等多平台接入 |
| ClaudeCode-13个Agentic设计模式 | 从 Claude Code 源码拆解的 13 个可直接复用的设计模式 |
| 一文讲清Agent-Model-Harness | Agent = Model + Harness，Harness 工程的本质与核心组件解析 |
| Codex数据智能体-六层上下文架构 | OpenAI 内部数据智能体的六层上下文架构 |
| 吃透Agent三大范式 | ReAct、Plan-and-Execute、Reflection三大范式深度解析 |
| Subagents指南-Agent-Registry与Task-Dispatcher | LangChain Subagents模式，中心化多智能体协作架构详解 |
| [深入源码Hermes-Agent如何实现Self-Improving](docs/Agent%E6%99%BA%E8%83%BD%E4%BD%93%E8%AE%BE%E8%AE%A1/%E6%B7%B1%E5%85%A5%E6%BA%90%E7%A0%81Hermes-Agent%E5%A6%82%E4%BD%95%E5%AE%9E%E7%8E%B0Self-Improving/%E6%80%BB%E7%BB%93.md) | Hermes Agent Self-Improving 机制，Memory/Skill/Nudge Engine 三大子系统深度解析 |
| Harness之后-Skills与可控工程化落地 | Agent Skills与Harness Engineering，Agent工程化落地方案 |
| [从AgentLoop深度拆解MiniCode](docs/Agent%E6%99%BA%E8%83%BD%E4%BD%93%E8%AE%BE%E8%AE%A1/%E4%BB%8EAgentLoop%E6%B7%B1%E5%BA%A6%E6%8B%86%E8%A7%A3MiniCode/总结.md) | Mini Code深度拆解Claude Code核心架构，Agent Loop三大机制设计解析 |
| [深度解析ClaudeCode-AI编码助手的底层架构与工作原理](docs/Agent%E6%99%BA%E8%83%BD%E4%BD%93%E8%AE%BE%E8%AE%A1/%E6%B7%B1%E5%BA%A8%E6%9E%90ClaudeCode-AI%E7%BC%96%E7%A0%81%E5%8A%A9%E6%89%8B%E7%9A%84%E5%BA%95%E5%B1%82%E6%9E%B6%E6%9E%84%E4%B8%8E%E5%B7%A5%E4%BD%9C%E5%8E%9F%E7%90%86/总结.md) | 深度解析Claude Code核心架构，Agent系统、Prompt系统、Memory系统、上下文管理、Hooks扩展机制 |
| Anthropic-12个生产级Agent-MCP设计模式 | Anthropic官方MCP设计模式，Agent生产级连接，5组12个模式 |
| SkillClaw-高德团队开源技能进化框架 | 高德团队开源的技能集体进化框架，双循环架构实现Agent自动进化 |
| [Agent总跑偏从Prompt到Harness彻底搞懂AI执行稳定的核心逻辑](docs/Agent%E6%99%BA%E8%83%BD%E4%BD%93%E8%AE%BE%E8%AE%A1/Agent%E6%80%BB%E8%B5%B0%E5%81%8F%E4%BB%8EPrompt%E5%88%B0Harness%E5%BD%BB%E5%BA%95%E6%90%9E%E6%87%82AI%E6%89%A7%E8%A1%8C%E7%A8%B3%E5%AE%9A%E7%9A%84%E6%A0%B8%E5%BF%83%E9%80%BB%E8%BE%91/%E6%80%BB%E7%BB%93.md) | 从Prompt到Harness，三层工程化手段让Agent稳定执行 |
| [从PRD到可运行代码-AI软件开发全流水线重构实践](docs/Agent%E6%99%BA%E8%83%BD%E4%BD%93%E8%AE%BE%E8%AE%A1/%E4%BB%8EPRD%E5%88%B0%E5%8F%AF%E8%BF%90%E8%A1%8C%E4%BB%A3%E7%A0%81-AI%E8%BD%AF%E4%BB%B6%E5%BC%80%E5%8F%91%E5%85%A8%E6%B5%81%E6%B0%B4%E7%BA%BF%E9%87%8D%E6%9E%84%E5%AE%9E%E8%B7%B5/%E6%80%BB%E7%BB%93.md) | 九层分层架构+五大专属Agent，从PRD到可交付的全链路自动化闭环 |
| [Qoder工程实践-Harness-Engineering指南](docs/Agent%E6%99%BA%E8%83%BD%E4%BD%93%E8%AE%BE%E8%AE%A1/Qoder%E5%B7%A5%E7%A8%8B%E5%AE%9E%E8%B7%B5-Harness-Engineering%E6%8C%87%E5%8D%97/%E6%80%BB%E7%BB%93.md) | 仓库是Agent的操作系统，层级约束验证、上下文管理、子代理调度等Harness工程核心机制解析 |

### 记忆系统Memory (4篇)
| 文章 | 简介 |
|------|------|
| 腾讯开源Agent-Memory-Token降低61% | 上下文卸载+Mermaid任务画布，Token消耗降低61% |
| Cognee-6行代码搞定AI记忆 | 16K Star 的开源知识引擎，向量+图双引擎驱动 |
| MemOS-Hermes记忆外挂插件 | Hermes Agent 的记忆系统外挂方案 |
| memory-architecture-thinking | Agent Memory 的本质与核心设计思路 |
### RAG检索增强 (12篇)
| 文章 | 简介 |
|------|------|
| PageIndex无向量RAG-目录树搜索 | 无向量、基于推理的 RAG 系统，98.7%准确率颠覆传统方案 |
| 20种RAG优化方法 | 20种实用的 RAG 优化策略与技巧 |
| 分层Agentic-RAG系统-多模态推理与自主纠错 | Supervisor-Worker分层拓扑 + Reflective Retry，84.5%准确率 |
| Agentic_RAG正成为新范式 | 传统 RAG 到 Agentic RAG 的范式转变，智能检索让模型主动探索 |
| RAG-Anything-港大开源万能RAG框架 | 港大开源万能 RAG 框架，支持 PDF、图片、视频等多模态 |
| rag-retrieval-troubleshooting | 检索失效的四大根源及全链路排查方法 |
| 封神级RAG优化实战-query改写与prompt构建 | Query 改写与 Prompt 构建的实战技巧 |
| 超越RAG-SpringBoot构建上下文感知AI系统 | Spring Boot 构建上下文感知 AI 系统 |
| Corpus2Skill-告别检索直接导航知识库 | "编译时换查询时"的设计哲学，给 Agent 一张地图让它自己导航 |
| 从60到94-11个进阶RAG策略 | 11个进阶RAG策略，从60%提升到94%准确率 |
| codegraph-rust-纯Rust实现的代码GraphRAG | 100% Rust 实现代码知识图谱，AST高速解析 + SurrealDB，打造AI代码助手超强大脑 |
| RAG深度解析与五大框架对比 | RAG核心原理、技术拆解及Haystack/LlamaIndex/LangChain/Dify/FAISS五大框架对比 |
### LLM网关架构 (1篇)
| 文章 | 简介 |
|------|------|
| LLM-Gateway生产级架构设计 | 三层架构、四大路由策略、四层故障降级 |
### AI工具 (8篇)
| 文章 | 简介 |
|------|------|
| CloakBrowser-10K-Stars反爬虫Stealth浏览器 | 10K Stars开源反检测Chromium浏览器，30/30 Bot检测全过 |
| context-mode-上下文压缩方案 | GitHub 2天暴涨13k，98%上下文压缩，MCP Server解决上下文爆炸 |
| hugohe3-ppt-master | 11681 Stars，AI PPT 一键生成，支持 Microsoft PowerPoint |
| PaddleOCR-国产OCR神器 | 75.8K Star 的国产 OCR 开源项目 |
| TigerFS-PostgreSQL挂载为文件系统 | 将 PostgreSQL 挂载为文件系统 |
| Claude-Design开源替代Open-Design | Claude Design 的开源替代方案 |
| Kami-AI排版项目 | 4.6K Star 的开源 AI 排版项目，让文档精致又好看 |
| beautiful-html-templates开源PPT模板库 | 32 套专业 HTML 幻灯片模板，Zara Zhang 和 Claude 联合开发 |
## 贡献
欢迎提交 AI 优化相关的解决方案和实战经验！
格式要求：
- 每篇文章按 `原文.md` + `总结.md` 结构保存
- 总结末尾标注使用的模型（如"总结使用: xxx模型"）
- 文件夹名称用简短总结命名
