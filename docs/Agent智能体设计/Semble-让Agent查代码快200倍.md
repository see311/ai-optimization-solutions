# 2.9K Star！这个工具让 Agent 查代码快了 200 倍！节省 98% Token 消耗！

> 来源：https://m.toutiao.com/is/jOQicMpUg4c/

当下，Agent 正在越来越多地介入我们的代码工作流。从代码补全到代码审查，从重构建议到自动生成测试，AI 已经成了很多开发者的得力助手。

但 Agent 需要在大型代码库中找东西时，要么瞎猜关键词，要么把整个项目的文件都读一遍——Token像流水一样哗哗地流。

## Semble：专为 Agent 打造的代码搜索库

Semble 由 MinishLab 团队开发（也是 Model2Vec 的团队），核心理念：**让 Agent 能快速、精准地找到它需要的代码片段，而不必浪费大量 Token 在不相干的内容上。**

解决三大问题：
1. **精准性**：不用瞎猜关键词，用自然语言就能找到准确的代码
2. **Token 效率**：只返回相关的代码块，节省 98% 的 Token
3. **速度**：索引快（~250ms）、查询快（~1.5ms），毫秒级响应

## 核心亮点

### 快到离谱的速度
- 索引一个普通仓库仅需约 250 毫秒
- 回答查询仅需约 1.5 毫秒
- NDCG@10 达到 0.854
- 达到 CodeRankEmbed Hybrid 99% 的性能，但索引快了 218 倍，查询快了 11 倍
- 全部在 CPU 上运行，不需要 GPU/API 密钥/外部服务

### 节省 98% Token
- Semble 用 2k Token 就能达到 94% 的召回率
- grep+read 需要塞满 100k Token 窗口才到 85%

### 智能分块
用 Chonkie 按代码结构智能切分，每个块都是有意义的代码单元（函数、类、独立逻辑块），绝不会拦腰斩断。

### 语义+词法双路检索
- **语义路**：Model2Vec + potion-code-16M 生成静态嵌入
- **词法路**：BM25 做标识符和 API 名称匹配
- 用 Reciprocal Rank Fusion (RRF) 融合

### 代码感知重排序
- 自适应加权：符号类查询给词法更多权重，自然语言查询保持平衡
- 定义优先：定义符号的块排在仅引用它的块前面
- 标识符词干匹配：查 parse config 会提升包含 parseConfig、ConfigParser 的块
- 文件连贯性：同文件多块匹配时整体提升
- 噪声惩罚：测试文件、兼容层代码、示例代码降权

## 快速上手

```bash
pip install semble
```

```python
from semble import SembleIndex

# 索引本地项目
index = SembleIndex.from_path("./my-project")

# 索引远程仓库
index = SembleIndex.from_git("https://github.com/MinishLab/model2vec")

# 搜索相关代码
results = index.search("save model to disk", top_k=3)

# 查找相似代码
related = index.find_related(results[0], top_k=3)
```

## MCP 服务器集成

Semble 可作为 MCP 服务器运行，支持 Claude Code、Cursor、Codex、OpenCode 等：

```bash
# Claude Code
claude mcp add semble -s user -- uvx --from "semble[mcp]" semble

# CLI 搜索
semble search "authentication flow" ./my-project
semble search "save_pretrained" ./my-project
```

## 总结

Semble 代表了 Agent 代码搜索的新方向：不需要庞大的 transformer 模型也能获得高质量代码搜索结果，速度更快、Token 效率更高、部署更简单。

GitHub：https://github.com/MinishLab/semble
