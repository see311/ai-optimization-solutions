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

### AI编程工具-Skills (5篇)

| 文章 | 简介 |
|------|------|
| 浏览器自动化 - 从GUI到OpenCLI | 放弃不稳定的UI自动化，用API请求复现解决浏览器自动化难题 |
| 7个AI前端设计Skill去AI味 | 去除 AI 生成界面的"AI味"，7个实测好用的设计 Skill |
| AgentSkills-谷歌工程规范封装 | 谷歌开源 23000+ Star 的 Agent Skills 技能包 |
| Book2Skill重新定义RAG把PDF变成Claude的skill | 把PDF文档转化为AI可调用的结构化技能包 |
| MiniMax-Skills-AI编程技能包 | MiniMax 官方的生产级开发技能包 |
| [Anthropic-12个生产级Agent-MCP设计模式](./docs/AI工具/Anthropic-12个生产级Agent-MCP设计模式/) | Anthropic官方MCP设计模式，Agent生产级连接，5组12个模式 |

### Agent智能体设计 (4篇)

| 文章 | 简介 |
|------|------|
| Claude Code - 13个Agentic设计模式 | 从 Claude Code 源码拆解的 13 个可直接复用的设计模式 |
| 一文讲清Agent-Model-Harness | Agent = Model + Harness，Harness 工程的本质与核心组件解析 |
| Codex 数据智能体 | OpenAI 内部数据智能体的六层上下文架构 |
| 吃透Agent三大范式 | ReAct、Plan-and-Execute、Reflection三大范式深度解析 |

### 记忆系统Memory (3篇)

| 文章 | 简介 |
|------|------|
| Cognee - 6行代码搞定AI记忆 | 16K Star 的开源知识引擎，向量+图双引擎驱动 |
| MemOS - Hermes记忆外挂插件 | Hermes Agent 的记忆系统外挂方案 |
| Memory架构与思考 | Agent Memory 的本质与核心设计思路 |

### RAG检索增强 (10篇)

| 文章 | 简介 |
|------|------|
| PageIndex无向量RAG-目录树搜索 | 无向量、基于推理的 RAG 系统，98.7%准确率颠覆传统方案 |
| RAG落地核心难点 | 从工程落地角度系统性梳理 RAG 三大核心难点：文档预处理、检索调优、效果评估 |
| 分层Agentic-RAG系统-多模态推理与自主纠错 | Supervisor-Worker分层拓扑 + Reflective Retry，84.5%准确率 |
| Agentic RAG正成为新范式 | 传统 RAG 到 Agentic RAG 的范式转变，智能检索让模型主动探索 |
| RAG-Anything | 港大开源万能 RAG 框架，支持 PDF、图片、视频等多模态 |
| RAG检索失效全链路排查 | 检索失效的四大根源及全链路排查方法 |
| 封神级RAG优化实战 | Query 改写与 Prompt 构建的实战技巧 |
| 超越RAG | Spring Boot 构建上下文感知 AI 系统 |
| RAG深度解析与五大框架对比 | RAG核心原理、技术拆解及Haystack/LlamaIndex/LangChain/Dify/FAISS五大框架对比 |
| 从60到94-11个进阶RAG策略 | 11个进阶RAG策略，从60%提升到94%准确率 |

### LLM网关架构 (1篇)

| 文章 | 简介 |
|------|------|
| LLM-Gateway生产级架构设计 | 三层架构、四大路由策略、四层故障降级 |

### AI工具 (5篇)

| 文章 | 简介 |
|------|------|
| hugohe3-ppt-master - AI PPT制作利器 | 11681 Stars，AI PPT 一键生成，支持 Microsoft PowerPoint |
| PaddleOCR - 国产OCR神器 | 75.8K Star 的国产 OCR 开源项目 |
| TigerFS | 将 PostgreSQL 挂载为文件系统 |
| Kami - AI文档排版利器 | 4.6K Star 的开源 AI 排版项目，让文档精致又好看 |

## 贡献

欢迎提交 AI 优化相关的解决方案和实战经验！

格式要求：
- 每篇文章按 `原文.md` + `总结.md` 结构保存
- 总结末尾标注使用的模型（如"总结使用: xxx模型"）
- 文件夹名称用简短总结命名
