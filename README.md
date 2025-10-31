# RAG-cache-papers
RAG Semantic Cache Papers

1. **[GPTCache]** Fu Bang. [GPTCache: An Open-Source Semantic Cache for LLM Applications Enabling Faster Answers and Cost Savings](https://aclanthology.org/2023.nlposs-1.24/) The 3rd Workshop for Natural Language Processing Open Source Software (NLP-OSS 2023) [Github page](https://github.com/zilliztech/GPTCache)
2. Shai Aviram Bergman, Zhang Ji, Anne-Marie Kermarrec, Diana Petrescu, Rafael Pires, Mathis Randl, and Martijn de Vos. 2025. Leveraging Approximate Caching for Faster Retrieval-Augmented Generation. EuroMLSys'25
- 该论文提出一种名为 Proximity 的近似键值缓存系统，核心思想是：
  - 相似查询复用：当用户查询相似时，复用之前检索的文档，减少重复访问向量数据库。
  - 近似缓存机制：构建一个基于查询相似度的缓存系统，而非精确匹配。
  - 性能权衡分析：通过调整相似度阈值，在速度与召回率之间取得平衡。
3. 
