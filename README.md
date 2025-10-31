# RAG-cache-papers
RAG Semantic Cache Papers

## 论文

1. **[RAGCache]** Chao Jin, Zili Zhang, Xuanlin Jiang, Fangyue Liu, Xin Liu, Xuanzhe Liu, Xin Jin: RAGCache: Efficient Knowledge Caching for Retrieval-Augmented Generation. ACM Transactions on Computer Systems, online September (2025) 
- 该论文发现RAG存在两个主要的优化机会：
  - 知识重用模式：RAG请求中常出现相同的文档，且少量文档占据了大多数检索，这表明可以通过缓存频繁访问文档的中间状态（即key-value tensors）来减少重复计算。
  - 流式搜索行为：向量搜索算法在搜索过程中会持续更新top-k候选结果，最终的top-k文档往往在搜索过程的早期就已经确定，这为检索与LLM生成之间的重叠执行提供了可能。
- 据此，RAGCache提出了两点新的设计：
  - 高效知识缓存：为了解决长序列生成问题和LLM对文档顺序的敏感性，RAGCache引入了知识树（knowledge tree）结构来组织和缓存检索文档的中间状态。知识树是一个基于文档ID的前缀树，每个节点存储文档KV cache的元数据（如内存页索引）。它将KV cache分布在GPU和主机内存层级中：频繁访问的节点存储在快速的GPU内存中，而访问较少的节点则置于较慢的主机内存。为了有效地管理这个多级缓存，RAGCache设计了前缀感知型贪婪双尺寸频率（Prefix-aware Greedy-Dual-Size-Frequency, PGDSF）替换策略。
  - 动态推测性流水线（Dynamic Speculative Pipelining）：为了消除检索与生成之间的数据依赖，RAGCache利用向量搜索的流式特性，实现了动态推测性流水线。它将向量搜索过程划分为多个阶段：在每个阶段结束时，RAGCache将临时的top-k文档发送给LLM推理引擎进行推测性生成。如果新的临时结果与上一次的不同，LLM会终止先前的推测并启动新的生成；如果相同，则继续当前生成。当最终的top-k文档确定并与最新的推测性生成匹配时，直接返回结果；否则进行重新生成。
- 测试基准：RAGCache在vLLM和Faiss基础上实现了一个原型系统，并在开源数据集（MMLU、Natural Questions）和生产数据集（Dataset-X）上进行了评估
2. **[Proximity]** Shai Aviram Bergman, Zhang Ji, Anne-Marie Kermarrec, Diana Petrescu, Rafael Pires, Mathis Randl, and Martijn de Vos. 2025. [Leveraging Approximate Caching for Faster Retrieval-Augmented Generation](https://arxiv.org/pdf/2503.05530). EuroMLSys'25. [**Github链接**](https://github.com/sacs-epfl/instruct-qa-proximity)
- 该论文提出一种名为 Proximity 的近似键值缓存系统，核心思想是：
  - 相似查询复用：当用户查询相似时，复用之前检索的文档，减少重复访问向量数据库。
  - 近似缓存机制：构建一个基于查询相似度的缓存系统，而非精确匹配。
  - 性能权衡分析：通过调整相似度阈值，在速度与召回率之间取得平衡。
- 测试基准：MMLU和MedRAG

## 测试基准
  - MMLU（Massive Multitask Language Understanding）是一个多任务语言理解评估基准，涵盖 57 个学科的多项选择题评估基准，用于测试语言模型在广泛知识领域的理解和推理能力。约 15,000 道题目，覆盖历史、法律、数学、医学等领域。广泛用于评估 GPT、Claude、LLaMA 等主流模型的综合能力。🔗 [MMLU 中文介绍与排行榜](https://www.datalearner.com/benchmarks/mmlu)（DataLearner） 🔗 [MMLU 英文维基百科](https://en.wikipedia.org/wiki/MMLU) 🔗 [MMLU 原始论文与 GitHub](https://zhuanlan.zhihu.com/p/677583745)
  - MedRAG（Medical Retrieval-Augmented Generation）是一个专为医学问答任务设计的 RAG 系统评估工具，旨在解决传统 RAG 在医学领域的幻觉和知识滞后问题。支持多种 RAG 模型配置评估，包含医学知识图谱与主动诊断机制，使用 DDXPlus 等大型医学数据集进行测试。🔗[ MedRAG 官方论文](https://arxiv.org/abs/2402.13178)（arXiv） 🔗[ MedRAG GitHub 工具包](https://github.com/Teddy-XiongGZ/MedRAG/blob/main/README.md) 🔗 [MedRAG 中文解读](https://blog.csdn.net/qq_41739364/article/details/145646641)（CSDN）
  - CRUD-RAG（中文 RAG 评估基准），由复旦大学 IAAR 团队发布，专为中文场景设计的 RAG 评估基准。包括问答、摘要、分类、排序、生成等 6 类任务。支持多种 RAG 模型对比（如 ChatGPT-RAG、BM25-RAG），提供标准化评估流程和数据集，适用于中文信息检索与生成任务。🔗 [GitHub 项目地址](https://github.com/IAAR-Shanghai/CRUD_RAG)
  - RAGBench（可解释性与系统评估），由 CMU 和微软研究院联合发布，旨在评估 RAG 系统的可解释性、准确性和系统行为。提供统一的评估框架和注释数据集，支持多种检索器和生成模型组合，包含用户满意度与响应合理性评估。🔗 [arXiv 论文页面](https://arxiv.org/abs/2407.11005)，🔗 [Github链接](https://github.com/dollyreddy650/RAGbench)
  - Open-RAGBench（开放领域评估基准），由 Vectara 发布的开源 RAG 评估数据集，托管在 Hugging Face 上。包含开放领域问答任务，提供真实用户问题与文档对，可用于训练和评估 RAG 模型。🔗 [Hugging Face 数据集页面](https://huggingface.co/datasets/vectara/open_ragbench)，🔗 [GitHub 项目地址](https://github.com/vectara/open-rag-bench)
