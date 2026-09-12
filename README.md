# RAG 从入门到生产 —— 基于阿里百炼（DashScope）的 41 课实战教程

本仓库用 **41 个 Jupyter Notebook** 系统覆盖 **RAG（Retrieval-Augmented Generation，检索增强生成）** 的完整知识树。
每个 notebook 对应一段知识模块：标题 + 中文讲解 + 密集注释的可运行代码，编号即推荐学习顺序。

- 大模型能力（生成 / Embedding / Rerank / 分词）由 **阿里百炼（DashScope）** 提供；
- API Key **统一通过 `.env` 文件配置**（仓库只提交 `.env.example`，不硬编码）；
- 每个 notebook 第一段 markdown 都标注「**本文件覆盖知识点**」，与下方覆盖表一一对应。

---

## 一、知识树全覆盖映射表

> 表中“覆盖知识点”与你粘贴的 RAG 知识大纲逐点对应；每点说明放在对应 notebook 内。

### 模块 A：LLM 基础与为什么需要 RAG

| # | 文件 | 覆盖知识点 |
|---|------|-----------|
| 01 | [`01_llm_primer.ipynb`](01_llm_primer.ipynb) | Transformer / Attention / Token·Tokenizer / Context Window / 位置编码(RoPE) / 采样(Temperature·Top-P) / Prompt / Function Calling / 幻觉 / 对齐(RLHF·DPO) / 长上下文 |
| 02 | [`02_why_rag.ipynb`](02_why_rag.ipynb) | LLM 知识截止 / 私有知识无法学习 / 幻觉 / 知识更新难 / Context Window 有限 / RAG vs Fine-tuning / RAG + Fine-tuning / RAG + Long Context |
| 03 | [`03_rag_architecture.ipynb`](03_rag_architecture.ipynb) | Document → Loader → Parsing → Cleaning → Chunking → Embedding → Vector DB → Retriever → Reranker → Context → LLM → Answer（整条链路概览） |

### 模块 B：文档加载 / 解析 / 清洗 / 切分 / 元数据

| # | 文件 | 覆盖知识点 |
|---|------|-----------|
| 04 | [`04_document_loading.ipynb`](04_document_loading.ipynb) | PDF / Word / Markdown / HTML / TXT / Excel / CSV / PPT / JSON / 数据库 / 网页 / API / 图片；工具：PyPDF·PyMuPDF·Unstructured·Docling·MinerU·OCR |
| 05 | [`05_document_parsing.ipynb`](05_document_parsing.ipynb) | 文本提取 / 版面提取 / 图片提取 / 表格识别 / 标题层级识别 / 页眉页脚 / 文档结构分割 / OCR / Layout Analysis |
| 06 | [`06_data_cleaning.ipynb`](06_data_cleaning.ipynb) | 噪声去除（页眉页脚 / 页码 / 目录 / 水印）/ 控制字符与 OCR 乱码 / 空白·全半角·Unicode 规整 / 精确去重 / 近重复检测（Jaccard / MinHash）/ 超短·超长·无效内容过滤 / PII 与敏感信息脱敏 / 可复现、可审计的清洗流水线 |
| 07 | [`07_chunking_basics.ipynb`](07_chunking_basics.ipynb) | Fixed-size / Character / Token / Sentence / Recursive Character Splitter；chunk_size / chunk_overlap |
| 08 | [`08_chunking_advanced.ipynb`](08_chunking_advanced.ipynb) | Semantic Chunking / Sentence Window / Parent-Child / Hierarchical / Contextual Chunking / Proposition / Markdown·Code·Table Chunking |
| 09 | [`09_chunk_metadata.ipynb`](09_chunk_metadata.ipynb) | metadata 设计 / Metadata Filtering / Metadata Index / Metadata Retrieval / Source Tracking / Citation |

### 模块 C：Embedding / 向量库 / 索引

| # | 文件 | 覆盖知识点 |
|---|------|-----------|
| 10 | [`10_embedding_basics.ipynb`](10_embedding_basics.ipynb) | Dense Embedding / 向量表示 / 语义相似度 / Cosine·Dot Product·欧氏距离 |
| 11 | [`11_embedding_models.ipynb`](11_embedding_models.ipynb) | BGE / E5 / GTE / Jina / OpenAI / Qwen Embedding；多语言 / 领域模型选择 / 微调(预告) |
| 12 | [`12_embedding_advanced.ipynb`](12_embedding_advanced.ipynb) | Query vs Document Embedding / 前缀 / Matryoshka / 维度 / Normalization / Multilingual / Domain-specific |
| 13 | [`13_vector_database.ipynb`](13_vector_database.ipynb) | FAISS / Milvus / Qdrant / Weaviate / Chroma / Elasticsearch / OpenSearch / pgvector（选型对比） |
| 14 | [`14_vector_index.ipynb`](14_vector_index.ipynb) | Flat / IVF / HNSW / PQ / IVF-PQ / ANN / 精确 vs 近似 / Recall·Speed·Memory 权衡 |
| 15 | [`15_dense_retrieval.ipynb`](15_dense_retrieval.ipynb) | Top-K / 相似度阈值 / Candidate Pool / 稠密检索实现与局限 |

### 模块 D：检索 / 融合 / 查询理解 / 重排

| # | 文件 | 覆盖知识点 |
|---|------|-----------|
| 16 | [`16_sparse_retrieval.ipynb`](16_sparse_retrieval.ipynb) | BM25 / TF-IDF / 倒排索引 / 关键词检索；为什么 Dense+Sparse 要结合 |
| 17 | [`17_hybrid_search.ipynb`](17_hybrid_search.ipynb) | Dense+Sparse / Score Fusion / Weighted Fusion / Reciprocal Rank Fusion(RRF) / Weighted RRF / Relative Score Fusion |
| 18 | [`18_query_rewriting.ipynb`](18_query_rewriting.ipynb) | Query Rewrite / Query Expansion / Query Normalization / Query Decomposition（含重写触发） |
| 19 | [`19_multi_query.ipynb`](19_multi_query.ipynb) | Multi-Query / 并行检索 / 多查询融合 |
| 20 | [`20_query_decomposition.ipynb`](20_query_decomposition.ipynb) | Query Decomposition / Sub-question 生成 / Parallel & Sequential Retrieval / Step-back Prompting |
| 21 | [`21_rag_fusion.ipynb`](21_rag_fusion.ipynb) | RAG-Fusion 全流程 / Multi-query / RRF / Weighted RRF / Fusion 策略 |
| 22 | [`22_rerank.ipynb`](22_rerank.ipynb) | 检索-重排-生成三段式 / Cross-Encoder / Bi-Encoder / Late Interaction / LLM Reranker / qwen3-rerank |

### 模块 E：上下文工程 / 提示词 / 幻觉 / 引用

| # | 文件 | 覆盖知识点 |
|---|------|-----------|
| 23 | [`23_context_engineering.ipynb`](23_context_engineering.ipynb) | Context Selection / Compression / Filtering / 去重 / Ordering / Truncation |
| 24 | [`24_advanced_context_retrieval.ipynb`](24_advanced_context_retrieval.ipynb) | Contextual Retrieval / Contextual Chunk·Embedding·BM25 / Parent-Child Retrieval / Sentence Window Retrieval |
| 25 | [`25_rag_prompt_citation.ipynb`](25_rag_prompt_citation.ipynb) | Context Injection / System Prompt / Grounding Prompt / Citation Prompt / Don't-Know Prompt / 上下文隔离 / 引用溯源 |
| 26 | [`26_hallucination.ipynb`](26_hallucination.ipynb) | 检索错误→上下文→生成错误→幻觉 / Grounded Generation / Citation·Attribution / Faithfulness / 回答校验 |

### 模块 F：高级范式（Graph / Agentic / 多模态 / SQL / Code）

| # | 文件 | 覆盖知识点 |
|---|------|-----------|
| 27 | [`27_graph_rag.ipynb`](27_graph_rag.ipynb) | Knowledge Graph / 实体·关系·节点·边 / 实体·关系抽取 / 图遍历 / Graph Retrieval / Microsoft GraphRAG（社区发现、全局/局部检索） |
| 28 | [`28_agentic_rag.ipynb`](28_agentic_rag.ipynb) | Agentic RAG / 查询规划 / Tool Calling / 迭代检索 / Retrieval Decision / Stop Condition |
| 29 | [`29_corrective_self_adaptive_rag.ipynb`](29_corrective_self_adaptive_rag.ipynb) | CRAG / Retrieval Grader / Web Search / Self-RAG（Retrieval·Relevance·Support·Critique）/ Adaptive RAG |
| 30 | [`30_multimodal_rag.ipynb`](30_multimodal_rag.ipynb) | Text / Image / PDF / Table / Video / Audio RAG / Multimodal Embedding / Vision LLM |
| 31 | [`31_sql_rag.ipynb`](31_sql_rag.ipynb) | 自然语言→SQL / Schema Retrieval / SQL Generation / SQL Validation / SQL Execution / SQL Correction |
| 32 | [`32_code_rag.ipynb`](32_code_rag.ipynb) | Code Chunking / AST / 函数·类检索 / 依赖检索 / Call Graph / Repository RAG |

### 模块 G：评估 / 安全 / 性能 / 工程化

| # | 文件 | 覆盖知识点 |
|---|------|-----------|
| 34 | [`34_retrieval_evaluation.ipynb`](34_retrieval_evaluation.ipynb) | Recall / Precision / Hit Rate / Recall@K / Precision@K / MRR / NDCG / MAP |
| 35 | [`35_generation_evaluation.ipynb`](35_generation_evaluation.ipynb) | Faithfulness / Answer Relevance / Context Relevance / LLM-as-a-Judge / RAGAS / DeepEval / TruLens / LangSmith / MS MARCO / BEIR |
| 36 | [`36_security.ipynb`](36_security.ipynb) | Security / Prompt Injection / Data Security / Access Control / PII / Redaction / Guardrails / 合规 |
| 37 | [`37_cache_latency.ipynb`](37_cache_latency.ipynb) | Cache / Semantic Cache / Latency / TTFT / Throughput / Cold Start / 优化清单 |
| 38 | [`38_serving_observability.ipynb`](38_serving_observability.ipynb) | Serving / FastAPI 部署 / 观测 / Tracing / Logging / Metrics / CI-CD / 版本与回滚 |

### 模块 H：微调 / 前沿模型 / 生产总览

| # | 文件 | 覆盖知识点 |
|---|------|-----------|
| 39 | [`39_finetuning.ipynb`](39_finetuning.ipynb) | Embedding 微调 / Reranker 微调 / LLM 微调 / SFT / LoRA / RLHF / DPO / 合成数据 |
| 40 | [`40_advanced_retrieval_models.ipynb`](40_advanced_retrieval_models.ipynb) | ColBERT / MaxSim / Late Interaction / SPLADE / 稀疏+稠密结合 / Long Context / Lost in the Middle |
| 41 | [`41_production_rag.ipynb`](41_production_rag.ipynb) | Production RAG 全景 / 十模块总复习 / 端到端串联 / 上线检查清单 / 高频坑 / 演进路径 |

---

## 二、快速开始

### 1. 安装依赖

```bash
pip install -r requirements.txt
```

> `faiss-cpu`、`PyMuPDF`、`rank-bm25`、`numpy` 等已在环境中；`dashscope`、`python-dotenv` 在 requirements.txt 中声明。

### 2. 用 `.env` 配置 API Key（必须）

1. 登录[阿里云百炼（Model Studio）控制台](https://bailian.console.aliyun.com/)，在「API-KEY 管理」创建 Key；
2. 复制 `.env.example` 为 `.env` 并填入 Key：

```bash
# .env
DASHSCOPE_API_KEY=sk-xxxxxxxxxxxxxxxx
```

3. 每个 notebook 的代码单元统一用下面的方式加载（无需改代码）：

```python
from dotenv import load_dotenv; load_dotenv()
import os
API_KEY = os.getenv('DASHSCOPE_API_KEY', '')
```

> `.env` 已被 `.gitignore` 忽略，不会提交；没配置 Key 时 notebook 会打印提示并走“演示分支”，仍可看懂全流程。

### 3. 运行

```bash
jupyter notebook
```

建议按编号顺序、逐单元格运行，先读注释再执行。

---

## 三、核心模型

| 用途 | 模型 | 说明 |
|------|------|------|
| 生成（LLM） | `qwen-plus` | 默认；可换 `qwen-max` / `qwen-turbo` / `qwen-long` |
| 向量化 | `text-embedding-v3` | 1024 维；另有 v1/v2（1536 维） |
| 重排序 | `qwen3-rerank` | 对召回结果精排；也可换 `gte-rerank-v2` |

> 百炼还提供 **OpenAI 兼容接口**：`base_url = "https://dashscope.aliyuncs.com/compatible-mode/v1"`，可复用 `openai`/LangChain。

---

## 四、目录结构

```
RagAll/
├── README.md                    # 本文件（知识树覆盖映射）
├── .env.example                 # API Key 配置模板（复制为 .env 使用）
├── .gitignore                   # 忽略 .env / __pycache__ 等
├── requirements.txt             # 依赖清单
├── .cache/                      # 向量缓存（真实调用的 embedding 落盘，重复运行不重复花 token）
├── data/                        # 示例知识库：一套「星云智能客服」的仿真语料
│   ├── 星云智能产品手册.md      #   产品/部署/计费/安全    ← 04 05 07 15 34 41 主干检索
│   ├── 星云客服FAQ.md           #   一问一答式客服语料    ← 18 19 20 24 查询改写
│   ├── 部署与运维手册.md        #   环境要求/升级/排障    ← 23 24 25 上下文工程
│   ├── API文档.md               #   接口/鉴权/错误码      ← 31 32 SQL/代码 RAG
│   ├── 计费与SLA.md             #   版本价格/服务等级      ← 22 重排
│   ├── 故障排查.md              #   常见故障与处置        ← 26 29 幻觉与 CRAG
│   ├── 向量数据库.md            #   索引类型/选型          ← 06 13 14
│   ├── 评测集.md                #   人工标注（问题→相关文档/小节），不进检索索引 ← 34 35 41
│   ├── 星云产品手册.pdf         #   由上面 md 生成的样例 PDF ← 05 PyMuPDF 真解析
│   └── 样例工单.csv / 样例帮助中心.html / 样例知识库元数据.json   ← 04 多格式加载
└── 01_llm_primer.ipynb … 41_production_rag.ipynb   # 41 个知识点 notebook
```

> 除第 34/35/41 课的人工标注评测集外，各课的检索、重排、生成都跑在同一套真实语料上：
> `data/` → 真切分 → 真 embedding（`text-embedding-v3`）→ 真索引（FAISS + BM25）→ 真重排（`qwen3-rerank`）→ 真生成（`qwen-plus`）。
> 没配 `.env` 时也不影响阅读：向量从 `.cache/` 读（真实调用的结果），需要现场调用的部分会打印历史录制结果。

---

## 五、学习建议

- **动手优先**：改 chunk 大小、top-k、是否混合检索 / 重排，观察指标变化（配合第 34/35 课评估）；
- **先机制后封装**：前期用 `numpy`/`dashscope` 手写理解，生产化再上框架；
- **带着“上亿文本怎么办”的视角学**：每一步都想想扩展性与评估（第 38/41 课收尾）；
- **别跳级**：01→22 是主干必学；23→40 可按需选学（每课都能单独插回主干），最后回到 41 做总复习。
