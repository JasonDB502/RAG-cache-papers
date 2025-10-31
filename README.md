# RAG-cache-papers
RAG Semantic Cache Papers

1. **[GPTCache]** Fu Bang. [GPTCache: An Open-Source Semantic Cache for LLM Applications Enabling Faster Answers and Cost Savings](https://aclanthology.org/2023.nlposs-1.24/) The 3rd Workshop for Natural Language Processing Open Source Software (NLP-OSS 2023) [Github page](https://github.com/zilliztech/GPTCache)
2. Shai Aviram Bergman, Zhang Ji, Anne-Marie Kermarrec, Diana Petrescu, Rafael Pires, Mathis Randl, and Martijn de Vos. 2025. Leveraging Approximate Caching for Faster Retrieval-Augmented Generation. EuroMLSys'25
- 该论文提出一种名为 Proximity 的近似键值缓存系统，核心思想是：
  - 相似查询复用：当用户查询相似时，复用之前检索的文档，减少重复访问向量数据库。
  - 近似缓存机制：构建一个基于查询相似度的缓存系统，而非精确匹配。
  - 性能权衡分析：通过调整相似度阈值，在速度与召回率之间取得平衡。
- 测试基准：MMLU和MedRAG。两者都是评估大语言模型性能的重要参考标准
  - [MMLU（Massive Multitask Language Understanding）](https://zhuanlan.zhihu.com/p/677583745)是一个多任务语言理解评估基准，涵盖 57 个学科的多项选择题评估基准，用于测试语言模型在广泛知识领域的理解和推理能力。约 15,000 道题目，覆盖历史、法律、数学、医学等领域。广泛用于评估 GPT、Claude、LLaMA 等主流模型的综合能力。
  - MedRAG（Medical Retrieval-Augmented Generation）是一个专为医学问答任务设计的 RAG 系统评估工具，旨在解决传统 RAG 在医学领域的幻觉和知识滞后问题。支持多种 RAG 模型配置评估，包含医学知识图谱与主动诊断机制，使用 DDXPlus 等大型医学数据集进行测试。🔗[ MedRAG 官方论文](https://arxiv.org/abs/2402.13178)（arXiv） 🔗[ MedRAG GitHub 工具包](https://github.com/Teddy-XiongGZ/MedRAG/blob/main/README.md) 🔗 [MedRAG 中文解读](https://blog.csdn.net/qq_41739364/article/details/145646641)（CSDN）
3. 
