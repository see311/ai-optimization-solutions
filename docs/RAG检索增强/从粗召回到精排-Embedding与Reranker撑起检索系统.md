# 从粗召回到精排，Embedding与Reranker撑起检索系统的半壁江山

> 来源：https://m.toutiao.com/is/6J9sLuaj-3A/

## 为什么检索系统必须要有"粗召回+精排"两阶段？

检索系统不能一步到位，核心原因是"成本和效率不允许"。上亿篇文档逐一用大模型判断相关性，工程上几乎不可行。

**第一阶段：粗召回** — 快速筛选，从海量候选中找出top1000条可能相关的结果。不追求极致精准，核心诉求是快、高效、可扩展。

**第二阶段：精排** — 精准排序，对1000条候选做细粒度相关性判断，返回top10或top20最符合需求的结果。不追求速度，核心诉求是精准。

| 模型 | 优势 | 劣势 | 适合阶段 |
|------|------|------|----------|
| Embedding | 快、可离线建索引、适合大规模检索 | 细粒度判断较弱 | 粗召回 |
| Reranker | 判断细、相关性建模强 | 慢、成本高、不适合全库扫描 | 精排 |

典型链路：查询→Embedding编码→ANN向量索引召回top1000→Reranker打分重排→返回top10-20。

## Embedding：向量空间里的"高效筛选器"

核心逻辑：把内容映射到同一向量空间，通过向量相似度判断相关性。score(q,d) = cosine(e_q, e_d)。

**为什么适合粗召回？** 可以离线建索引，线上只需编码查询+ANN检索，千万级库毫秒级返回。

**局限：** 双编码器结构，查询和内容分开编码，无充分交互。对"红色汽车旁边有黑狗"的空间约束、"Transformer缺点"的否定关系等细粒度需求判断不准。

## Reranker：细粒度判断的"精准裁判"

与Embedding的核心区别：交叉编码器（cross-encoder）结构，查询和内容一起输入，模型内部token级充分交互，直接输出相关性分数。

LLM Reranker示例：
- Instruction: 判断Document是否满足Query的需求，只能回答yes或no
- score(q,d) = sigmoid(logit_yes - logit_no)

**三种训练方式：**

| 类型 | 一次训练看什么 | 学习目标 |
|------|---------------|----------|
| Pointwise | 一个query-document pair | 这个内容是否和查询相关 |
| Pairwise | 同一查询下两个内容 | 哪个更相关 |
| Listwise | 同一查询下整个候选列表 | 整个列表应该怎么排序 |

## 训练数据来源

| 数据来源 | 适合Embedding | Pointwise | Pairwise | Listwise |
|----------|:---:|:---:|:---:|:---:|
| 人工相关性标注 | ✅ | ✅ | 可构造 | 可构造 |
| LLM/VLM生成query | ✅ | ✅ | 可构造 | 可构造 |
| Teacher打分 | ✅ | ✅ | ✅ | ✅ |
| 点击日志 | ✅ | ✅ | ✅ | ✅ |
| 完整曝光列表 | 部分 | ✅ | ✅ | 最适合 |

人工标注质量最高但成本高；机器标注规模大但需质量控制；用户行为日志最真实但需去偏处理（位置偏差、展示偏差、选择偏差、流行度偏差）。

## Embedding与Reranker的业务配合

完整检索链路：
查询→Query理解/改写→Embedding召回→多路召回→候选合并→轻量ranker粗排→Reranker精排→业务规则过滤→最终展示

**"召回决定上限，排序逼近上限"** — Embedding召回效果决定系统最高水平，Reranker精排效果逼近这个上限。

**互相增强三种方式：**
1. 用Embedding挖掘hard negatives训练Reranker
2. 用Reranker过滤Embedding训练数据（去假阳性/假阴性）
3. 用Reranker蒸馏Embedding（将细粒度判断能力迁移到Embedding）

## 实战：Qwen3-VL-Embedding/Reranker

**Embedding训练流程：**
1. 大规模合成数据对比预训练
2. 用当前模型挖掘hard negatives
3. 多任务数据继续训练
4. Reranker软分数蒸馏
5. 模型合并

**Reranker：** Pointwise yes/no分类，LLM输入形式（指令+查询+内容→yes/no），推理用logit差值排序。

**三个启发：**
1. Embedding和Reranker分工明确，各司其职
2. Reranker可作为teacher提升Embedding能力
3. 数据pipeline比模型结构更重要

## 总结

| 模型/范式 | 输入形式 | 核心loss | 优化目标 | 系统角色 |
|-----------|---------|---------|---------|---------|
| Embedding | (q, d+, d-) | InfoNCE | 学习语义向量空间 | 粗召回 |
| Pointwise Reranker | (q, d, y) | BCE / yes-no NLL | 判断单个文档是否相关 | 精排 |
| Pairwise Reranker | (q, d+, d-) | -log σ(s+ - s-) | 学习相对顺序 | 精排/排序 |
| Listwise Reranker | (q, [d_i], [y_i]) | ListNet / ListMLE | 优化整个排序列表 | 精排/终排 |

Embedding学的是"如何把相关内容召回来"；Reranker学的是"如何把召回结果排好"；Pointwise、Pairwise、Listwise的区别，在于分别从单个样本、样本对、整个列表三个层面定义"什么叫排得好"。
