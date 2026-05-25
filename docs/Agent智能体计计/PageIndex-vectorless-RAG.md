# 向量数据库out了？这神器98.7%准确率

> 来源：今日头条 · GitHub项目精选
> 链接：https://m.toutiao.com/is/9zsRS9FBOSE/
> 日期：2026-05-25

> 告别"感觉不对"的向量检索，让 AI 像人类专家一样阅读文档

## 你是不是也遇到过这些问题？

做 RAG（检索增强生成）应用的时候，是不是经常被向量数据库坑？

- 用户问"公司2024年Q4营收多少"，检索出来的却是"2023年Q2的市场分析"
- 明明文档里有答案，但相似度匹配就是捞不出来
- Chunk 切得太大丢信息，切得太小丢上下文，左右为难
- 用户问"对比一下 A 产品和 B 产品的差异"，结果只搜到 A 产品的介绍

问题出在哪？

**相似 ≠ 相关**

向量检索本质是"找相似的文本"，但用户要的是"相关的答案"。这就像你问朋友"哪里有好吃的川菜馆"，他给你推荐了一家"装修风格相似"的日料店——看起来像，但不是你要的。

## PageIndex：让 AI 像人类专家一样读文档

最近发现一个有趣的开源项目 **PageIndex**，它完全颠覆了传统 RAG 的玩法：

**不用向量数据库，不用分块，照样做 RAG，而且准确率更高。**

它的核心思路特别像人类专家读文档的方式：

1. **先构建文档的"目录树"** —— 把长文档（比如几百页的财报）整理成一个层级化的树状结构（类似目录，但是 AI 优化的版本）
2. **推理式检索** —— 用户提问时，AI 沿着这棵树"思考" + "跳转"，像人翻书一样找到最相关的章节

> 人类专家拿到一份几百页的财报，不会逐字逐句读，而是先看目录，找到"营收"章节，再精读相关页面。PageIndex 就是让 AI 学会这个技能。

## 核心优势（对比传统向量 RAG）

| 维度 | 传统向量 RAG | PageIndex |
|------|-------------|-----------|
| 检索方式 | 向量相似度匹配 | LLM 推理 + 树搜索 |
| 是否需要向量数据库 | 是 | **否** |
| 是否需要分块（Chunking） | 是 | **否**（保留自然章节结构） |
| 可解释性 | 差（黑盒） | **强**（可追溯翻页路径） |
| 上下文感知 | 弱 | **强**（结合对话历史） |
| 长文档效果 | 一般 | **优秀** |

## 实战成绩：98.7% 准确率

PageIndex 在金融文档分析基准测试 **FinanceBench** 上达到了 **98.7%** 的准确率，远超传统向量 RAG 方案。

这个成绩是由基于 PageIndex 构建的 **Mafin 2.5** 系统创造的（也是开源的：github.com/VectifyAI/Mafin2.5-FinanceBench）。

适用场景：

- 金融报告（财报、SEC 文件）
- 学术教材
- 法律文档、技术手册
- 任何超过 LLM 上下文限制的长文档

## 快速上手

PageIndex 支持**自托管**（开源版）和**云服务**两种使用方式。

### 方式一：自托管（开源）

```bash
# 1. 安装依赖
pip3 install --upgrade -r requirements.txt

# 2. 配置 API Key（支持 OpenAI / LiteLLM 多模型）
# 创建 .env 文件
OPENAI_API_KEY=your_openai_key_here

# 3. 生成 PageIndex 树结构
python3 run_pageindex.py --pdf_path /path/to/document.pdf

# 可选参数
# --model gpt-4o-2024-11-20 # 使用的 LLM 模型
# --max-pages-per-node 10 # 每个节点最多页数
# --max-tokens-per-node 20000 # 每个节点最多 token 数
```

也支持 Markdown 文件：

```bash
python3 run_pageindex.py --md_path /path/to/document.md
```

### 方式二：云服务（推荐生产使用）

自托管版使用标准 PDF 解析，对复杂 PDF 效果有限。生产环境建议用他们的云服务（支持 MCP 和 API 接入）：

- Chat 平台：chat.pageindex.ai
- MCP 接入：pageindex.ai/developer
- API 接入：pageindex.ai/developer

## 典型使用示例

生成好的 PageIndex 树结构大概长这样（层级化目录）：

```json
{
  "title": "2024 Annual Report",
  "children": [
    {
      "title": "Financial Overview",
      "page": "10-15",
      "children": [
        {"title": "Revenue", "page": "10"},
        {"title": "Cost of Goods Sold", "page": "11"}
      ]
    }
  ]
}
```

然后结合 LLM 做推理式检索，AI 会沿着树结构"跳转"，找到最相关的章节再生成答案，而不是直接拿相似度最高的 Chunk 来用。

他们提供了一个完整的 Agentic RAG 示例（基于 OpenAI Agents SDK）：

```bash
pip3 install openai-agents
python3 examples/agentic_vectorless_rag_demo.py
```

在线 Colab 笔记本：

- [基础 RAG 示例](https://colab.research.google.com/github/VectifyAI/PageIndex/blob/main/cookbook/pageindex_RAG_simple.ipynb)
- [视觉版 RAG（无需 OCR）](https://colab.research.google.com/github/VectifyAI/PageIndex/blob/main/cookbook/vision_RAG_pageindex.ipynb)

## 适合你吗？

**适合：**
- 正在做 RAG 应用，被向量检索准确率折磨的独立开发者
- 需要处理长文档（财报、法律文档、技术手册）的场景
- 想要可解释、可追溯的检索结果

**不适合：**
- 文档很短（几页以内），直接用上下文塞给 LLM 就行
- 对准确率要求不高，能用就行的场景

## 资源链接

- GitHub：github.com/VectifyAI/PageIndex
- 官方文档：docs.pageindex.ai
- Chat 平台（试用）：chat.pageindex.ai
- Mafin 2.5（98.7% 准确率实现）：github.com/VectifyAI/Mafin2.5-FinanceBench

---

**彩蛋：** PageIndex 的灵感来自 AlphaGo —— 就像 AlphaGo 用蒙特卡洛树搜索下棋一样，PageIndex 用树搜索来"下"文档检索这盘棋。这个跨界思路真的很妙。
