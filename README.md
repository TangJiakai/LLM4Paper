#! https://zhuanlan.zhihu.com/p/678404083

### LLM-Paper

以LLM4Rec方向为主

目录如下

1. [LLM & RS](#1)

   🔷  1.1 [LLM for Feature Engineering](#1.1)

   ​		🔸 1.1.1 [User- and Item-level Feature Augmentation](#1.1.1)

   ​		🔸 1.1.2 [Instance-level Sample Generation](#1.1.2)

   🔷 1.2 [LLM as Feature Encoder](#1.2)

   ​		🔸 1.2.1 [Representation Enhancement](#1.2.1)

   ​		🔸 1.2.2 [Unified Cross-domain Recommendation](#1.2.2)
   
   🔷 1.3 [LLM as Scoring/Ranking Function](#1.3)
   
   ​		🔸 1.3.1 [Item Scoring Task](#1.3.1)
   
   ​		🔸 1.3.2 [Item Generation Task](#1.3.2)
   
   ​		🔸 1.3.3 [Hybrid Task](#1.3.3)

​		🔷 1.4 [LLM for User Interaction](#1.4)

​				🔸 1.4.1 [Task-oriented User Interaction](#1.4.1)

​				🔸 1.4.2 [Open-ended User Interaction](#1.4.2)

​		🔷 1.5 [LLM for RS Pipeline Controller](#1.5)

2. [LLM & Graph](#2)

3. [Datasets & Benchmarks](#3)

   🔷 3.1 [Datasets](#3.1)

   🔷 3.2 [Benchmarks](#3.2)

4. [Related Repositories](#4)

<h2 id="1">1. LLM & RS</h2>

引入LLM到推荐中的常用动机：

- LLM能以prompt方式统一各种下游推荐任务
- LLM将各模态、各特征统一以文本呈现，缓解不同模态/特征异质性问题
- LLM具有强大的语言推理能力，能更好的捕获用户的偏好
- LLM相比于传统推荐算法，具有更好的冷启动和泛化能力，因为文本特征是各用户、物品、领域所共享的
- 只有ID会缺乏世界知识，只有文本会缺乏理解推荐协同/序列交互模式，结合二者（可视为多个模态）才能充分发挥世界知识和行为知识的优势

![](where-framework-1.png)

<details><summary><h3 id="1.1">1.1 LLM for Feature Engineering</h3></summary>
<p>
<h4 id="1.1.1">1.1.1 User- and Item-level Feature Augmentation</h4>

| **Name** | **Paper**                                                                                                           | **LLM Backbone (Largest)** | **LLM Tuning Strategy** | **Publication** |                **Link**                | Main Contributions |
| :------------: | :------------------------------------------------------------------------------------------------------------------------ | :------------------------------: | :----------------------------: | :-------------------: | :------------------------------------------: | ------------------ |
|    LLM4KGC    | Knowledge Graph Completion Models are Few-shot Learners: An Empirical Study of Relation Labeling in E-commerce with LLMs  |       PaLM (540B)/ ChatGPT       |             Frozen             |      Arxiv 2023      |  [[Paper]](https://arxiv.org/abs/2305.09858v1)  |                    |
|     TagGPT     | TagGPT: Large Language Models are Zero-shot Multimodal Taggers                                                            |             ChatGPT             |             Frozen             |      Arxiv 2023      |  [[Paper]](https://arxiv.org/abs/2304.03022v1)  |                    |
|      ICPC      | Large Language Models for User Interest Journeys                                                                          |           LaMDA (137B)           | Full Finetuning/ Prompt Tuning |      Arxiv 2023      |   [[Paper]](https://arxiv.org/abs/2305.15498)   |                    |
|      KAR      | Towards Open-World Recommendation with Knowledge Augmentation from Large Language Models                                  |             ChatGPT             |             Frozen             |      Arxiv 2023      |   [[Paper]](https://arxiv.org/abs/2306.10933)   |                    |
|      PIE      | Product Information Extraction using ChatGPT                                                                              |             ChatGPT             |             Frozen             |      Arxiv 2023      |   [[Paper]](https://arxiv.org/abs/2306.14921)   |                    |
|      LGIR      | Enhancing Job Recommendation through LLM-based Generative Adversarial Networks                                            |           GhatGLM (6B)           |             Frozen             |       AAAI 2024       |   [[Paper]](https://arxiv.org/abs/2307.10747)   |                    |
|      GIRL      | Generative Job Recommendations with Large Language Model                                                                  |            BELLE (7B)            |        Full Finetuning        |      Arxiv 2023      |   [[Paper]](https://arxiv.org/abs/2307.02157)   |                    |
|    LLM-Rec    | LLM-Rec: Personalized Recommendation via Prompting Large Language Models                                                  |         text-davinci-003         |             Frozen             |      Arxiv 2023      |   [[Paper]](https://arxiv.org/abs/2307.15780)   |                    |
|      HKFR      | Heterogeneous Knowledge Fusion: A Novel Approach for Personalized Recommendation via LLM                                  |             ChatGPT             |             Frozen             |      RecSys 2023      |   [[Paper]](https://arxiv.org/abs/2308.03333)   |                    |
|    LLaMA-E    | LLaMA-E: Empowering E-commerce Authoring with Multi-Aspect Instruction Following                                          |           LLaMA (30B)           |              LoRA              |      Arxiv 2023      |   [[Paper]](https://arxiv.org/abs/2308.04913)   |                    |
|    EcomGPT    | EcomGPT: Instruction-tuning Large Language Models with Chain-of-Task Tasks for E-commerce                                 |          BLOOMZ (7.1B)          |        Full Finetuning        |      Arxiv 2023      |   [[Paper]](https://arxiv.org/abs/2308.06966)   |                    |
|    TF-DCon    | Leveraging Large Language Models (LLMs) to Empower Training-Free Dataset Condensation for Content-Based Recommendation    |             ChatGPT             |             Frozen             |      Arxiv 2023      |   [[Paper]](https://arxiv.org/abs/2310.09874)   |                    |
|     RLMRec✅     | Representation Learning with Large Language Models for Recommendation                                                     |             ChatGPT             |             Frozen             |       WWW 2024       |   [[Code]](https://github.com/HKUDS/RLMRec)   | 推荐隐式数据包含噪声和偏差；使用LLM推荐存在扩展性不足、输入长度限制等不足。本文目的是通过LLM强大语言理解能力挖掘用户行为和偏好，同时保留已有推荐器的效率和准确度。贡献有1. 基于推理的用户和物品提示生成；2. 提出对比式和掩码生成式两个方法；3.从互信息角度分析引入文本信号对于提升表示质量的有效性 |
|     LLMRec✅     | LLMRec: Large Language Models with Graph Augmentation for Recommendation                                                  |             ChatGPT             |             Frozen             |       WSDM 2024       | [[Code]](https://github.com/HKUDS/LLMRec) | 数据稀疏可以通过side information解决，但是这些信息也会包含噪声、可用性低和数据质量低等问题，反过来伤害了推荐准确率。本文提出方法从用户-物品交互边、用户画像、物品节点属性三角度增强数据；并提出对增强的交互和特征分别设计剪枝、MAE方法去噪。 |
|     LLMRG     | Enhancing Recommender Systems with Large Language Model Reasoning Graphs                                                  |              GPT4              |             Frozen             |      Arxiv 2023      |   [[Paper]](https://arxiv.org/abs/2308.10835)   |                    |
|      CUP      | Recommendations by Concise User Profiles from Review Text                                                                 |             ChatGPT             |             Frozen             |      Arxiv 2023      |   [[Paper]](https://arxiv.org/abs/2311.01314)   |                    |
|     SINGLE     | Modeling User Viewing Flow using Large Language Models for Article Recommendation                                         |             ChatGPT             |             Frozen             |      Arxiv 2023      |   [[Paper]](https://arxiv.org/abs/2311.07619)   |                    |
|     SAGCN     | Understanding Before Recommendation: Semantic Aspect-Aware Review Exploitation via Large Language Models                  |           Vicuna (13B)           |             Frozen             |      Arxiv 2023      |   [[Paper]](https://arxiv.org/abs/2312.16275)   |                    |
|      UEM      | User Embedding Model for Personalized Language Prompting                                                                  |       FLAN-T5-base (250M)       |        Full Finetuning        |      Arxiv 2024      |   [[Paper]](https://arxiv.org/abs/2401.04858)   |                    |
|     LLMHG     | LLM-Guided Multi-View Hypergraph Learning for Human-Centric Explainable Recommendation                                    |               GPT4               |             Frozen             |      Arxiv 2024      |   [[Paper]](https://arxiv.org/abs/2401.08217)   |                    |
|   Llama4Rec   | Integrating Large Language Models into Recommendation via Mutual Augmentation and Adaptive Aggregation                    |           LLaMA2 (7B)           |        Full Finetuning        |      Arxiv 2024      |   [[Paper]](https://arxiv.org/abs/2401.13870)   |                    |

<h4 id="1.1.2">1.1.2 Instance-level Sample Generation</h4>

|   **Name**    | **Paper**                                                    |      **LLM Backbone (Largest)**      | **LLM Tuning Strategy** | **Publication** |                  **Link**                   | Main Contributions                                           |
| :-----------: | :----------------------------------------------------------- | :----------------------------------: | :---------------------: | :-------------: | :-----------------------------------------: | ------------------------------------------------------------ |
|     GReaT     | Language Models are Realistic Tabular Data Generators        |          GPT2-medium (355M)          |     Full Finetuning     |    ICLR 2023    | [[Paper]](https://arxiv.org/abs/2210.06280) |                                                              |
|     ONCE✅     | ONCE: Boosting Content-based Recommendation with Both Open- and Closed-source Large Language Models | ChatGPT+<br />LLaMA2(7B)/LLaMA2(13B) |          LoRA           |    WSDM 2024    |   [[Code]](https://github.com/Jyonn/ONCE)   | 传统content-based推荐算法停留在捕捉word级别的相似度，而无法实现content级别。本文提出同时利用开源和闭源的LLM帮助增强对物品和用户信息内容的理解。开源LLM用于编码用户和物品表示；闭源LLM用于物品内容丰富、用户兴趣抽象、（冷启动）用户内容生成。并使用LoRA、冻结低层，缓存机制等提高效率。 |
|  AnyPredict   | AnyPredict: Foundation Model for Tabular Prediction          |               ChatGPT                |         Frozen          |   Arxiv 2023    | [[Paper]](https://arxiv.org/abs/2305.12081) |                                                              |
|     DPLLM     | Privacy-Preserving Recommender Systems with Synthetic Query Generation using Differentially Private Large Language Models |              T5-XL (3B)              |     Full Finetuning     |   Arxiv 2023    | [[Paper]](https://arxiv.org/abs/2305.05973) |                                                              |
|     MINT      | Large Language Model Augmented Narrative Driven Recommendations |           text-davinci-003           |         Frozen          |   RecSys 2023   | [[Paper]](https://arxiv.org/abs/2306.02250) |                                                              |
|   Agent4Rec   | On Generative Agents in Recommendation                       |               ChatGPT                |         Frozen          |   Arxiv 2023    | [[Paper]](https://arxiv.org/abs/2310.10108) |                                                              |
|   RecPrompt   | RecPrompt: A Prompt Tuning Framework for News Recommendation Using Large Language Models |                 GPT4                 |         Frozen          |   Arxiv 2023    | [[Paper]](https://arxiv.org/abs/2312.10463) |                                                              |
|    PO4ISR     | Large Language Models for Intent-Driven Session Recommendations |               ChatGPT                |         Frozen          |   Arxiv 2023    | [[Paper]](https://arxiv.org/abs/2312.07552) |                                                              |
|     BEQUE     | Large Language Model based Long-tail Query Rewriting in Taobao Search |             ChatGLM (6B)             |     Full Finetuning     |   Arxiv 2023    | [[Paper]](https://arxiv.org/abs/2311.03758) |                                                              |
| Agent4Ranking | Agent4Ranking: Semantic Robust Ranking via Personalized Query Rewriting Using Multi-agent LLM |               ChatGPT                |         Frozen          |   Arxiv 2023    | [[Paper]](https://arxiv.org/abs/2312.15450) |                                                              |

</p>
</details>

<details><summary><h3 id="1.2">1.2 LLM as Feature Encoder</h3></summary>
<p>
<h4 id="1.2.1">1.2.1 Representation Enhancement</h4>

| **Name** | **Paper**                                                                                                                      | **LLM Backbone (Largest)** | **LLM Tuning Strategy** | **Publication** |                                     **Link**                                     | Main Contributions |
| :------------: | :----------------------------------------------------------------------------------------------------------------------------------- | :------------------------------: | :---------------------------: | :-------------------: | :------------------------------------------------------------------------------------: | ------------------ |
|     U-BERT     | U-BERT: Pre-training User Representations for Improved Recommendation                                                                |         BERT-base (110M)         |        Full Finetuning        |       AAAI 2021       |             [[Paper]](https://ojs.aaai.org/index.php/AAAI/article/view/16557)             |                    |
|     UNBERT     | UNBERT: User-News Matching BERT for News Recommendation                                                                              |         BERT-base (110M)         |        Full Finetuning        |      IJCAI 2021      |                   [[Paper]](https://www.ijcai.org/proceedings/2021/462)                   |                    |
|     PLM-NR     | Empowering News Recommendation with Pre-trained Language Models                                                                      |       RoBERTa-base (125M)       |        Full Finetuning        |      SIGIR 2021      |                        [[Paper]](https://arxiv.org/abs/2104.07413)                        |                    |
| Pyramid-ERNIE | Pre-trained Language Model based Ranking in Baidu Search                                                                             |           ERNIE (110M)           |        Full Finetuning        |       KDD 2021       |                        [[Paper]](https://arxiv.org/abs/2105.11108)                        |                    |
|    ERNIE-RS    | Pre-trained Language Model for Web-scale Retrieval in Baidu Search                                                                   |           ERNIE (110M)           |        Full Finetuning        |       KDD 2021       |                        [[Paper]](https://arxiv.org/abs/2106.03373)                        |                    |
|    CTR-BERT    | CTR-BERT: Cost-effective knowledge distillation for billion-parameter teacher models                                                 |      Customized BERT (1.5B)      |        Full Finetuning        |      ENLSP 2021      | [[Paper]](https://neurips2021-nlp.github.io/papers/20/CameraReady/camera_ready_final.pdf) |                    |
|      SuKD      | Learning Supplementary NLP Features for CTR Prediction in Sponsored Search                                                           |       RoBERTa-large (355M)       |        Full Finetuning        |       KDD 2022       |               [[Paper]](https://dl.acm.org/doi/abs/10.1145/3534678.3539064)               |                    |
|      PREC      | Boosting Deep CTR Prediction with a Plug-and-Play Pre-trainer for News Recommendation                                                |         BERT-base (110M)         |        Full Finetuning        |      COLING 2022      |                  [[Paper]](https://aclanthology.org/2022.coling-1.249/)                  |                    |
|     MM-Rec     | MM-Rec: Visiolinguistic Model Empowered Multimodal News Recommendation                                                               |         BERT-base (110M)         |        Full Finetuning        |      SIGIR 2022      |               [[Paper]](https://dl.acm.org/doi/abs/10.1145/3477495.3531896)               |                    |
|  Tiny-NewsRec  | Tiny-NewsRec: Effective and Efficient PLM-based News Recommendation                                                                  |       UniLMv2-base (110M)       |        Full Finetuning        |      EMNLP 2022      |                        [[Paper]](https://arxiv.org/abs/2112.00944)                        |                    |
|    PLM4Tag    | PTM4Tag: Sharpening Tag Recommendation of Stack Overflow Posts with Pre-trained Models                                               |         CodeBERT (125M)         |        Full Finetuning        |       ICPC 2022       |                        [[Paper]](https://arxiv.org/abs/2203.10965)                        |                    |
|   TwHIN-BERT   | TwHIN-BERT: A Socially-Enriched Pre-trained Language Model for Multilingual Tweet Representations                                    |         BERT-base (110M)         |        Full Finetuning        |      Arxiv 2022      |                        [[Paper]](https://arxiv.org/abs/2209.07562)                        |                    |
|      LSH      | Improving Code Example Recommendations on Informal Documentation Using BERT and Query-Aware LSH: A Comparative Study                 |         BERT-base (110M)         |        Full Finetuning        |      Arxiv 2023      |                       [[Paper]](https://arxiv.org/abs/2305.03017v1)                       |                    |
|  LLM2BERT4Rec  | Leveraging Large Language Models for Sequential Recommendation                                                                       |      text-embedding-ada-002      |            Frozen            |      RecSys 2023      |                        [[Paper]](https://arxiv.org/abs/2309.09261)                        |                    |
|    LLM4ARec    | Prompt Tuning Large Language Models on Personalized Aspect Extraction for Recommendations                                            |           GPT2 (110M)           |         Prompt Tuning         |      Arxiv 2023      |                        [[Paper]](https://arxiv.org/abs/2306.01475)                        |                    |
|     TIGER     | Recommender Systems with Generative Retrieval                                                                                        |           Sentence-T5           |            Frozen            |       NIPS 2023       |                        [[Paper]](https://arxiv.org/abs/2305.05065)                        |                    |
|      TBIN      | TBIN: Modeling Long Textual Behavior Data for CTR Prediction                                                                         |         BERT-base (110M)         |            Frozen            |    DLP-RecSys 2023    |                        [[Paper]](https://arxiv.org/abs/2308.08483)                        |                    |
|     LKPNR     | LKPNR: LLM and KG for Personalized News Recommendation Framework                                                                     |           LLaMA2 (7B)           |            Frozen            |      Arxiv 2023      |                        [[Paper]](https://arxiv.org/abs/2308.12028)                        |                    |
|      SSNA      | Towards Efficient and Effective Adaptation of Large Language Models for Sequential Recommendation                                    |     DistilRoBERTa-base (83M)     |   Layerwise Adapter Tuning   |      Arxiv 2023      |                        [[Paper]](https://arxiv.org/abs/2310.01612)                        |                    |
| CollabContext | Collaborative Contextualization: Bridging the Gap between Collaborative Filtering and Pre-trained Language Model                     |       Instructor-XL (1.5B)       |            Frozen            |      Arxiv 2023      |                        [[Paper]](https://arxiv.org/abs/2310.09400)                        |                    |
|   LMIndexer   | Language Models As Semantic Indexers                                                                                                 |          T5-base (223M)          |        Full Finetuning        |      Arxiv 2023      |                        [[Paper]](https://arxiv.org/abs/2310.07815)                        |                    |
|     Stack     | A BERT based Ensemble Approach for Sentiment Classification of Customer Reviews and its Application to Nudge Marketing in e-Commerce |         BERT-base (110M)         |            Frozen            |      Arxiv 2023      |                        [[Paper]](https://arxiv.org/abs/2311.10782)                        |                    |
|      N/A      | Utilizing Language Models for Tour Itinerary Recommendation                                                                          |         BERT-base (110M)         |        Full Finetuning        |    PMAI@IJCAI 2023    |                        [[Paper]](https://arxiv.org/abs/2311.12355)                        |                    |
|      UEM      | User Embedding Model for Personalized Language Prompting                                                                             |     Sentence-T5-base (223M)     |            Frozen            |      Arxiv 2024      |                        [[Paper]](https://arxiv.org/abs/2401.04858)                        |                    |
|   Social-LLM   | Social-LLM: Modeling User Behavior at Scale using Language Models and Social Network Data                                            |     SBERT-MPNet0base (110M)     |            Frozen            |      Arxiv 2024      |                        [[Paper]](https://arxiv.org/abs/2401.00893)                        |                    |
|     LLMRS     | LLMRS: Unlocking Potentials of LLM-Based Recommender Systems for Software Purchase                                                   |           MPNet (110M)           |            Frozen            |      Arxiv 2024      |                        [[Paper]](https://arxiv.org/abs/2401.06676)                        |                    |

<h4 id="1.2.2">1.2.2 Unified Cross-domain Recommendation</h4>

|    **Name**     | **Paper**                                                    | **LLM Backbone (Largest)** | **LLM Tuning Strategy**  | **Publication** |                       **Link**                        | Main Contributions                                           |
| :-------------: | :----------------------------------------------------------- | :------------------------: | :----------------------: | :-------------: | :---------------------------------------------------: | ------------------------------------------------------------ |
|     ZESRec      | Zero-Shot Recommender Systems                                |      BERT-base (110M)      |          Frozen          |   Arxiv 2021    |      [[Paper]](https://arxiv.org/abs/2105.08318)      |                                                              |
|     UniSRec     | Towards Universal Sequence Representation Learning for Recommender Systems |      BERT-base (110M)      |          Frozen          |    KDD 2022     |      [[Paper]](https://arxiv.org/abs/2206.05941)      |                                                              |
|    TransRec     | TransRec: Learning Transferable Recommendation from Mixture-of-Modality Feedback |      BERT-base (110M)      |     Full Finetuning      |   Arxiv 2022    |      [[Paper]](https://arxiv.org/abs/2206.06190)      |                                                              |
|     VQ-Rec      | Learning Vector-Quantized Item Representation for Transferable Sequential Recommenders |      BERT-base (110M)      |          Frozen          |    WWW 2023     |      [[Paper]](https://arxiv.org/abs/2210.12316)      |                                                              |
| IDRec vs MoRec✅ | Where to Go Next for Recommender Systems? ID- vs. Modality-based Recommender Models Revisited |      BERT-base (110M)      |     Full Finetuning      |   SIGIR 2023    | [[Code]](https://github.com/westlake-repl/IDvs.MoRec) | 研究纯ID-based推荐和纯modality-based推荐。实现发现使用预训练的encoder进行end2end训练，能够持平甚至超过ID-based推荐算法（甚至对于非冷启动物品）。 |
|    TransRec     | Exploring Adapter-based Transfer Learning for Recommender Systems: Empirical Studies and Practical Insights |    RoBERTa-base (125M)     | Layerwise Adapter Tuning |   Arxiv 2023    |      [[Paper]](https://arxiv.org/abs/2305.15036)      |                                                              |
|       TCF       | Exploring the Upper Limits of Text-Based Collaborative Filtering Using Large Language Models: Discoveries and Insights |      OPT-175B (175B)       | Frozen/ Full Finetuning  |   Arxiv 2023    |      [[Paper]](https://arxiv.org/abs/2305.11700)      |                                                              |
| S&R Foundation  | An Unified Search and Recommendation Foundation Model for Cold-Start Scenario |        ChatGLM (6B)        |          Frozen          |    CIKM 2023    |      [[Paper]](https://arxiv.org/abs/2309.08939)      |                                                              |
|     MISSRec     | MISSRec: Pre-training and Transferring Multi-modal Interest-aware Sequence Representation for Recommendation |      CLIP-B/32 (400M)      |     Full Finetuning      |     MM 2023     |      [[Paper]](https://arxiv.org/abs/2308.11175)      |                                                              |
|      UFIN       | UFIN: Universal Feature Interaction Network for Multi-Domain Click-Through Rate Prediction |    FLAN-T5-base (250M)     |          Frozen          |   Arxiv 2023    |      [[Paper]](https://arxiv.org/abs/2311.15493)      |                                                              |
|     PMMRec      | Multi-Modality is All You Need for Transferable Recommender Systems |    RoBERTa-large (355M)    |  Top-2-layer Finetuning  |    ICDE 2024    |      [[Paper]](https://arxiv.org/abs/2312.09602)      |                                                              |
|     Uni-CTR     | A Unified Framework for Multi-Domain CTR Prediction via Large Language Models |    Sheared-LLaMA (1.3B)    |           LoRA           |   Arxiv 2023    |      [[Paper]](https://arxiv.org/abs/2312.10743)      |                                                              |

</p>
</details>

<details><summary><h3 id="1.3">1.3 LLM as Scoring/Ranking Function</h3></summary>
<p>

<h4 id="1.3.1">1.3.1 Item Scoring Task</h4>


| **Name** | **Paper**                                                                                                     | **LLM Backbone (Largest)** |     **LLM Tuning Strategy**     | **Publication** |                         **Link**                         | Main Contributions |
| :------------: | :------------------------------------------------------------------------------------------------------------------ | :------------------------------: | :------------------------------------: | :-------------------: | :-------------------------------------------------------------: | ------------------ |
|    LMRecSys    | Language Models as Recommender Systems: Evaluations and Limitations                                                 |          GPT2-XL (1.5B)          |            Full Finetuning            |      ICBINB 2021      |       [[Paper]](https://openreview.net/forum?id=hFx3fY7-m9b)       |                    |
|      PTab      | PTab: Using the Pre-trained Language Model for Modeling Tabular Data                                                |         BERT-base (110M)         |            Full Finetuning            |      Arxiv 2022      |            [[Paper]](https://arxiv.org/abs/2209.08060)            |                    |
|    UniTRec✅    | UniTRec: A Unified Text-to-Text Transformer and Joint Contrastive Learning Framework for Text-based Recommendation  |           BART (406M)           |            Full Finetuning            |       ACL 2023       |            [[Code]](https://github.com/Veason-silverbullet/UniTRec)            | PLM处理用户历史物品的文本信息存在两种方法，但都有不足：(a). 直接将全部物品历史作为输入文本作为用户全局表示，忽略了不同物品文本之间的关系，而是把所有词都视作同等参与；(b).引入额外聚合网络，这削弱了PLM 编码器的表达能力。本文贡献：(a). 对注意力掩码操作设计word-level和turn-level两种机制 (b).联合训练基于Discriminative Scores和Candidate Text Perplexity的对比损失。 |
|   Prompt4NR   | Prompt Learning for News Recommendation                                                                             |         BERT-base (110M)         |            Full Finetuning            |      SIGIR 2023      |            [[Paper]](https://arxiv.org/abs/2304.05263)            |                    |
|   RecFormer✅   | Text Is All You Need: Learning Language Representations for Sequential Recommendation                               |        LongFormer (149M)        |            Full Finetuning            |       KDD 2023       |           [[Code]](https://github.com/AaronHeee/RecFormer)           | ID-based推荐难以解决冷启动问题；已有跨域推荐工作通常假设有重叠特征、物品或者用户等，这限制了算法应用。基于预训练语言模型的应用存在问题:(a)预训练文本和物品文本存在领域差异;(b)无法建模细粒度用户偏好。本文提出以key-value形式表达物品文本，修改LongFormer通过加入特殊设计Token Embedding，以及预训练+两阶段微调。 |
|     TabLLM     | TabLLM: Few-shot Classification of Tabular Data with Large Language Models                                          |             T0 (11B)             | Few-shot Parameter-effiecnt Finetuning |     AISTATS 2023     |            [[Paper]](https://arxiv.org/abs/2210.10723)            |                    |
| Zero-shot GPT | Zero-Shot Recommendation as Language Modeling                                                                       |        GPT2-medium (355M)        |                 Frozen                 |      Arxiv 2023      |            [[Paper]](https://arxiv.org/abs/2112.04184)            |                    |
|    FLAN-T5    | Do LLMs Understand User Preferences? Evaluating LLMs On User Rating Prediction                                      |         FLAN-5-XXL (11B)         |            Full Finetuning            |      Arxiv 2023      |          [[Paper]](https://arxiv.org/pdf/2305.06474.pdf)          |                    |
|    BookGPT    | BookGPT: A General Framework for Book Recommendation Empowered by Large Language Model                              |             ChatGPT             |                 Frozen                 |      Arxiv 2023      |           [[Paper]](https://arxiv.org/abs/2305.15673v1)           |                    |
|    TALLRec    | TALLRec: An Effective and Efficient Tuning Framework to Align Large Language Model with Recommendation              |            LLaMA (7B)            |                  LoRA                  |      RecSys 2023      |            [[Paper]](https://arxiv.org/abs/2305.00447)            |                    |
|      PBNR      | PBNR: Prompt-based News Recommender System                                                                          |          T5-small (60M)          |            Full Finetuning            |      Arxiv 2023      |            [[Paper]](https://arxiv.org/abs/2304.07862)            |                    |
|    CR-SoRec    | CR-SoRec: BERT driven Consistency Regularization for Social Recommendation                                          |         BERT-base (110M)         |            Full Finetuning            |      RecSys 2023      | [[Paper]](https://dl.acm.org/doi/fullHtml/10.1145/3604915.3608844) |                    |
|   PromptRec   | Towards Personalized Cold-Start Recommendation with Prompts                                                         |            LLaMA (7B)            |                 Frozen                 |      Arxiv 2023      |            [[Paper]](https://arxiv.org/abs/2306.17256)            |                    |
|     GLRec     | Exploring Large Language Model for Graph Data Understanding in Online Job Recommendations                           |         BELLE-LLaMA (7B)         |                  LoRA                  |      Arxiv 2023      |            [[Paper]](https://arxiv.org/abs/2307.05722)            |                    |
|    BERT4CTR✅    | BERT4CTR: An Efficient Framework to Combine Pre-trained Language Model with Non-textual Features for CTR Prediction |       RoBERTa-large (355M)       |            Full Finetuning            |       KDD 2023       |   [[Paper]](https://dl.acm.org/doi/abs/10.1145/3580305.3599780)   | 融合非文本特征（sparse和dense feature）到LM是有挑战性的。本文提出Uni-Attention方法，非文本特征取消位置编码，同时改变其Attention方式，非文本特征作为Q，文本特征作为V和K。 |
|     ReLLa✅     | ReLLa: Retrieval-enhanced Large Language Models for Lifelong Sequential Behavior Comprehension in Recommendation    |           Vicuna (13B)           |                  LoRA                  |       WWW 2024       |            [[Paper]](https://arxiv.org/abs/2308.11131)            | 实验发现推荐场景中，并非用户历史序列越长效果越好。本文提出使用semantic user behavior retrieval (SUBR)代替最近K个交互历史来提升数据质量。对于zero-shot，不tune模型而直接使用SUBR；对于few-shot，除了使用SUBR，还要用原始和SUBR增强的数据来训练模型。SUBR具体是对历史物品和目标物品做PCA降维（实现去噪），然后cosine计算相似度，替换原先的最近K个交互历史。 |
|     TASTE     | Text Matching Improves Sequential Recommendation by Reducing Popularity Biases                                      |          T5-base (223M)          |            Full Finetuning            |       CIKM 2023       |            [[Paper]](https://arxiv.org/abs/2308.14029)            |                    |
|      N/A      | Unveiling Challenging Cases in Text-based Recommender Systems                                                       |         BERT-base (110M)         |            Full Finetuning            | RecSys Workshop 2023 |         [[Paper]](https://ceur-ws.org/Vol-3476/paper5.pdf)         |                    |
|  ClickPrompt✅  | ClickPrompt: CTR Models are Strong Prompt Generators for Adapting Language Models to CTR Prediction                 |       RoBERTa-large (355M)       |            Full Finetuning            |       WWW 2024       |            [[Paper]](https://arxiv.org/abs/2310.09234)            | 传统CTR建模ID信息的方式会失去文本内在的语义信息，而PLM无法建模协同知识（ID特征无语义、特征通过模版填充线性组合为文本而不具备特征交叉能力）。本文提出将ID特征变换为交互感知的soft prompt，再通过传统CTR模型和PLM的pretrain-finetune学习机制，实现对语义知识和协作知识的建模。 |
|  SetwiseRank  | A Setwise Approach for Effective and Highly Efficient Zero-shot Ranking with Large Language Models                  |        FLAN-T5-XXL (11B)        |                 Frozen                 |      Arxiv 2023      |            [[Paper]](https://arxiv.org/abs/2310.09497)            |                    |
|      UPSR      | Thoroughly Modeling Multi-domain Pre-trained Recommendation as Language                                             |          T5-base (223M)          |            Full Finetuning            |      Arxiv 2023      |            [[Paper]](https://arxiv.org/abs/2310.13540)            |                    |
|    LLM-Rec    | One Model for All: Large Language Models are Domain-Agnostic Recommendation Systems                                 |            OPT (6.7B)            |                  LoRA                  |      Arxiv 2023      |            [[Paper]](https://arxiv.org/abs/2310.14304)            |                    |
|   LLMRanker   | Beyond Yes and No: Improving Zero-Shot LLM Rankers via Scoring Fine-Grained Relevance Labels                        |           FLAN PaLM2 S           |                 Frozen                 |      Arxiv 2023      |            [[Paper]](https://arxiv.org/abs/2310.14122)            |                    |
|     CoLLM     | CoLLM: Integrating Collaborative Embeddings into Large Language Models for Recommendation                           |           Vicuna (7B)           |                  LoRA                  |      Arxiv 2023      |            [[Paper]](https://arxiv.org/abs/2310.19488)            |                    |
|      FLIP      | FLIP: Towards Fine-grained Alignment between ID-based Models and Pretrained Language Models for CTR Prediction      |       RoBERTa-large (355M)       |            Full Finetuning            |      Arxiv 2023      |            [[Paper]](https://arxiv.org/abs/2310.19453)            |                    |
| BTRec | BTRec: BERT-Based Trajectory Recommendation for Personalized Tours | BERT-base (110M) | Full Finetuning | Arxiv 2023 | [[Paper]](https://arxiv.org/abs/2310.19886) | |
|    CLLM4Rec    | Collaborative Large Language Model for Recommender Systems                                                          |           GPT2 (110M)           |            Full Finetuning            |      Arxiv 2023      |            [[Paper]](https://arxiv.org/abs/2311.01343)            |                    |
|      CUP      | Recommendations by Concise User Profiles from Review Text                                                           |         BERT-base (110M)         |         Last-layer Finetuning         |      Arxiv 2023      |            [[Paper]](https://arxiv.org/abs/2311.01314)            |                    |
|      N/A      | Instruction Distillation Makes Large Language Models Efficient Zero-shot Rankers                                    |         FLAN-T5-XL (3B)         |            Full Finetuning            |      Arxiv 2023      |            [[Paper]](https://arxiv.org/abs/2311.01555)            |                    |
|    CoWPiRec    | Collaborative Word-based Pre-trained Item Representation for Transferable Recommendation                            |         BERT-base (110M)         |            Full Finetuning            |       ICDM 2023       |            [[Paper]](https://arxiv.org/abs/2311.10501)            |                    |
|  RecExplainer  | RecExplainer: Aligning Large Language Models for Recommendation Model Interpretability                              |         Vicuna-v1.3 (7B)         |                  LoRA                  |      Arxiv 2023      |            [[Paper]](https://arxiv.org/abs/2311.10947)            |                    |
|     E4SRec     | E4SRec: An Elegant Effective Efficient Extensible Solution of Large Language Models for Sequential Recommendation   |           LLaMA2 (13B)           |                  LoRA                  |      Arxiv 2023      |            [[Paper]](https://arxiv.org/abs/2312.02443)            |                    |
|      CER      | The Problem of Coherence in Natural Language Explanations of Recommendations                                        |           GPT2 (110M)           |            Full Finetuning            |       ECAI 2023       |            [[Paper]](https://arxiv.org/abs/2312.11356)            |                    |
|      LSAT      | Preliminary Study on Incremental Learning for Large Language Model-based Recommender Systems                        |            LLaMA (7B)            |                  LoRA                  |      Arxiv 2023      |            [[Paper]](https://arxiv.org/abs/2312.15599)            |                    |
|   Llama4Rec   | Integrating Large Language Models into Recommendation via Mutual Augmentation and Adaptive Aggregation              |           LLaMA2 (7B)           |            Full Finetuning            |      Arxiv 2024      |            [[Paper]](https://arxiv.org/abs/2401.13870)            |                    |

<h4 id="1.3.2">1.3.2 Item Generation Task</h4>

| **Name** | **Paper**                                                                                                 | **LLM Backbone (Largest)** | **LLM Tuning Strategy** |     **Publication**     |                          **Link**                          | Main Contributions |
| :------------: | :-------------------------------------------------------------------------------------------------------------- | :------------------------------: | :---------------------------: | :----------------------------: | :--------------------------------------------------------------: | ------------------ |
|    GPT4Rec    | GPT4Rec: A Generative Framework for Personalized Recommendation and User Interests Interpretation               |           GPT2 (110M)           |        Full Finetuning        |           Arxiv 2023           |             [[Paper]](https://arxiv.org/abs/2304.03879)             |                    |
|      VIP5✅      | VIP5: Towards Multimodal Foundation Models for Recommendation                                                   |          T5-base (223M)          |    Layerwise Adater Tuning    |           EMNLP 2023           |             [[Paper]](https://arxiv.org/abs/2305.14302)             | 如何在不修改原始结构下将多模态推荐模型适用于各种任务和模态缺乏研究。本文提出将物品文本、图像编码为k个token，并冻结P5 backbone，只训练adapter（Attention和FFN之后的新矩阵）实现参数高效微调。下有任务包括直接推荐、序列、可解释。 |
|     P5-ID✅     | How to Index Item IDs for Recommendation Foundation Models                                                      |          T5-small (60M)          |        Full Finetuning        |           SIGIR-AP 2023           |             [[Code]](https://github.com/Wenyueh/LLM-RecSys-ID)             | 关注研究LLM推荐的Item ID index方式。提出序列Index、协同Index、语义Index和混合Index方式。 |
|    FaiRLLM    | Is ChatGPT Fair for Recommendation? Evaluating Fairness in Large Language Model Recommendation                  |             ChatGPT             |            Frozen            |          RecSys 2023          |             [[Paper]](https://arxiv.org/abs/2305.07609)             |                    |
|      PALR      | PALR: Personalization Aware LLMs for Recommendation                                                             |            LLaMA (7B)            |        Full Finetuning        |           Arxiv 2023           |             [[Paper]](https://arxiv.org/abs/2305.07622)             |                    |
|    ChatGPT    | Large Language Models are Zero-Shot Rankers for Recommender Systems                                             |             ChatGPT             |            Frozen            |           ECIR 2024           |             [[Paper]](https://arxiv.org/abs/2305.08845)             |                    |
|      AGR      | Sparks of Artificial General Recommender (AGR): Early Experiments with ChatGPT                                  |             ChatGPT             |            Frozen            |           Arxiv 2023           |             [[Paper]](https://arxiv.org/abs/2305.04518)             |                    |
|      NIR      | Zero-Shot Next-Item Recommendation using Large Pretrained Language Models                                       |           GPT3 (175B)           |            Frozen            |           Arxiv 2023           |             [[Paper]](https://arxiv.org/abs/2304.03153)             |                    |
|     GPTRec     | Generative Sequential Recommendation with GPTRec                                                                |        GPT2-medium (355M)        |        Full Finetuning        |       Gen-IR@SIGIR 2023       |             [[Paper]](https://arxiv.org/abs/2306.11114)             |                    |
|    ChatNews    | A Preliminary Study of ChatGPT on News Recommendation: Personalization, Provider Fairness, Fake News            |             ChatGPT             |            Frozen            |           Arxiv 2023           |             [[Paper]](https://arxiv.org/abs/2306.10702)             |                    |
|      N/A      | Large Language Models are Competitive Near Cold-start Recommenders for Language- and Item-based Preferences     |            PaLM (62B)            |            Frozen            |          RecSys 2023          |             [[Paper]](https://arxiv.org/abs/2307.14225)             |                    |
|  LLMSeqPrompt  | Leveraging Large Language Models for Sequential Recommendation                                                  |         OpenAI ada model         |           Finetune           |          RecSys 2023          |             [[Paper]](https://arxiv.org/abs/2309.09261)             |                    |
|     GenRec     | GenRec: Large Language Model for Generative Recommendation                                                      |            LLaMA (7B)            |             LoRA             |           Arxiv 2023           |             [[Paper]](https://arxiv.org/abs/2307.00457)             |                    |
| UP5✅ | UP5: Unbiased Foundation Model for Fairness-aware Recommendation | T5-base (223M) | Prefix Tuning | Arxiv 2023 | [[Paper]](https://arxiv.org/abs/2305.12090) | 研究LLM推荐的用户公平性。提出prefix prompt和分类器之间对抗训练实现公平性；其中prefix soft prompt分别加在encoder和decoder前面，对于多个敏感属性的混合，使用target-attention机制生成单一prefix prompt。 |
|      HKFR      | Heterogeneous Knowledge Fusion: A Novel Approach for Personalized Recommendation via LLM                        |           ChatGLM (6B)           |             LoRA             |          RecSys 2023          |             [[Paper]](https://arxiv.org/abs/2308.03333)             |                    |
|      N/A      | The Unequal Opportunities of Large Language Models: Revealing Demographic Bias through Job Recommendations      |             ChatGPT             |            Frozen            |           EAAMO 2023           |             [[Paper]](https://arxiv.org/abs/2308.02053)             |                    |
|     BIGRec     | A Bi-Step Grounding Paradigm for Large Language Models in Recommendation Systems                                |            LLaMA (7B)            |             LoRA             |           Arxiv 2023           |             [[Paper]](https://arxiv.org/abs/2308.08434)             |                    |
|     KP4SR     | Knowledge Prompt-tuning for Sequential Recommendation                                                           |          T5-small (60M)          |        Full Finetuning        |           Arxiv 2023           |             [[Paper]](https://arxiv.org/abs/2308.08459)             |                    |
|   RecSysLLM   | Leveraging Large Language Models for Pre-trained Recommender Systems                                            |            GLM (10B)            |             LoRA             |           Arxiv 2023           |             [[Paper]](https://arxiv.org/abs/2308.10837)             |                    |
| POD✅ | Prompt Distillation for Efficient LLM-based Recommendation | T5-small (60M) | Full Finetuning | CIKM 2023 | [[Code]](https://github.com/lileipisces/POD) | 已有LLM4Rec需要将用户和物品信息嵌入到给定的离散模版中，但由于大量的任务信息描述可能导致如LLM误解为另一个任务，或者掩盖了关键信息。本文提出为每个任务设计连续prompt，训练时连续和离散prompt同时出现，目的是将任务知识蒸馏到连续prompt中（推断时只保留连续prompt）；此外设计任务交替训练方法，防止不同任务句子长度不同导致pad时间过长。 |
|      N/A      | Evaluating ChatGPT as a Recommender System: A Rigorous Approach                                                 |             ChatGPT             |            Frozen            |           Arxiv 2023           |             [[Paper]](https://arxiv.org/abs/2309.03613)             |                    |
|      RaRS      | Retrieval-augmented Recommender System: Enhancing Recommender Systems with Large Language Models                |             ChatGPT             |            Frozen            | RecSys Doctoral Symposium 2023 |    [[Paper]](https://dl.acm.org/doi/abs/10.1145/3604915.3608889)    |                    |
|   JobRecoGPT   | JobRecoGPT -- Explainable job recommendations using LLMs                                                        |               GPT4               |            Frozen            |           Arxiv 2023           |             [[Paper]](https://arxiv.org/abs/2309.11805)             |                    |
|     LANCER     | Reformulating Sequential Recommendation: Learning Dynamic User Interest with Content-enriched Language Modeling |           GPT2 (110M)           |         Prefix Tuning         |           Arxiv 2023           |             [[Paper]](https://arxiv.org/abs/2309.10435)             |                    |
|    TransRec    | A Multi-facet Paradigm to Bridge Large Language Model and Recommendation                                        |            LLaMA (7B)            |             LoRA             |           Arxiv 2023           |             [[Paper]](https://arxiv.org/abs/2310.06491)             |                    |
|    AgentCF✅    | AgentCF: Collaborative Learning with Autonomous Language Agents for Recommender Systems                         | text-davinci-003 & gpt-3.5-turbo |            Frozen            |            WWW 2024            |             [[Paper]](https://arxiv.org/abs/2310.09233)             | 将用户和物品都作为agent建模双边关系并实现协同优化各自的memory，reflection等内部结构 |
|      P4LM      | Factual and Personalized Recommendations using Language Models and Reinforcement Learning                       |             PaLM2-XS             |        Full Finetuning        |           Arxiv 2023           |             [[Paper]](https://arxiv.org/abs/2310.06176)             |                    |
|   InstructMK   | Multiple Key-value Strategy in Recommendation Systems Incorporating Large Language Model                        |            LLaMA (7B)            |        Full Finetuning        |        CIKM GenRec 2023        |             [[Paper]](https://arxiv.org/abs/2310.16409)             |                    |
|    LightLM    | LightLM: A Lightweight Deep and Narrow Language Model for Generative Recommendation                             |          T5-small (60M)          |        Full Finetuning        |           Arxiv 2023           |             [[Paper]](https://arxiv.org/abs/2310.17488)             |                    |
|    LlamaRec    | LlamaRec: Two-Stage Recommendation using Large Language Models for Ranking                                      |           LLaMA2 (7B)           |             QLoRA             |         PGAI@CIKM 2023         |             [[Paper]](https://arxiv.org/abs/2311.02089)             |                    |
|      N/A      | Exploring Recommendation Capabilities of GPT-4V(ision): A Preliminary Case Study                                |              GPT-4V              |            Frozen            |           Arxiv 2023           |             [[Paper]](https://arxiv.org/abs/2311.04199)             |                    |
|      N/A      | Exploring Fine-tuning ChatGPT for News Recommendation                                                           |             ChatGPT             |  gpt-3.5-urbo finetuning API  |           Arxiv 2023           |             [[Paper]](https://arxiv.org/abs/2311.05850)             |                    |
|      N/A      | Do LLMs Implicitly Exhibit User Discrimination in Recommendation? An Empirical Study                            |             ChatGPT             |            Frozen            |           Arxiv 2023           |             [[Code]](https://github.com/ljy0ustc/LLaRA)             |                    |
|     LC-Rec     | Adapting Large Language Models by Integrating Collaborative Semantics for Recommendation                        |            LLaMA (7B)            |             LoRA             |           Arxiv 2023           |             [[Paper]](https://arxiv.org/abs/2311.09049)             |                    |
|      DOKE      | Knowledge Plugins: Enhancing Large Language Models for Domain-Specific Recommendations                          |             ChatGPT             |            Frozen            |           Arxiv 2023           |             [[Paper]](https://arxiv.org/abs/2311.10779)             |                    |
|   ControlRec   | ControlRec: Bridging the Semantic Gap between Language Model and Personalized Recommendation                    |          T5-base (223M)          |        Full Finetuning        |           Arxiv 2023           |             [[Paper]](https://arxiv.org/abs/2311.16441)             |                    |
|     LLaRA✅     | LLaRA: Aligning Large Language Models with Sequential Recommenders                                              |           LLaMA2 (7B)           |             LoRA             |           Arxiv 2023           |             [[Paper]](https://arxiv.org/abs/2312.02445)             | 仅利用ID或者文本，无法充分发挥世界知识和行为序列模式。本文将传统模型训练得到的embedding和文本描述embedding都放在prompt中；此外，设计课程学习从简单任务（纯文本）到难任务（文本+ID）实现序列行为知识蒸馏到LLM |
|     PO4ISR     | Large Language Models for Intent-Driven Session Recommendations                                                 |             ChatGPT             |            Frozen            |           Arxiv 2023           |             [[Paper]](https://arxiv.org/abs/2312.07552)             |                    |
|      DRDT      | DRDT: Dynamic Reflection with Divergent Thinking for LLM-based Sequential Recommendation                        |             ChatGPT             |            Frozen            |           Arxiv 2023           |             [[Paper]](https://arxiv.org/abs/2312.11336)             |                    |
|   RecPrompt   | RecPrompt: A Prompt Tuning Framework for News Recommendation Using Large Language Models                        |               GPT4               |            Frozen            |           Arxiv 2023           |             [[Paper]](https://arxiv.org/abs/2312.10463)             |                    |
|      LiT5      | Scaling Down, LiTting Up: Efficient Zero-Shot Listwise Reranking with Seq2seq Encoder-Decoder Models            |            T5-XL (3B)            |        Full Finetuning        |           Arxiv 2023           |             [[Paper]](https://arxiv.org/abs/2312.16098)             |                    |
|     STELLA     | Large Language Models are Not Stable Recommender Systems                                                        |             ChatGPT             |            Frozen            |           Arxiv 2023           |             [[Paper]](https://arxiv.org/abs/2312.15746)             |                    |
|   Llama4Rec   | Integrating Large Language Models into Recommendation via Mutual Augmentation and Adaptive Aggregation          |           LLaMA2 (7B)           |        Full Finetuning        |           Arxiv 2024           |             [[Paper]](https://arxiv.org/abs/2401.13870)             |                    |

<h4 id="1.3.3">1.3.3 Hybrid Task</h4>

| **Name** | **Paper**                                                                                              | **LLM Backbone (Largest)** | **LLM Tuning Strategy** | **Publication** |                **Link**                | Main Contributions                                                                                                                                                                                           |
| :------------: | :----------------------------------------------------------------------------------------------------------- | :------------------------------: | :---------------------------: | :-------------------: | :------------------------------------------: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
|      P5✅      | Recommendation as Language Processing (RLP): A Unified Pretrain, Personalized Prompt & Predict Paradigm (P5) |          T5-base (223M)          |        Full Finetuning        |      RecSys 2022      |    [[Code]](https://github.com/jeykigung/P5)    | 使用相同的语言建模目标实现统一的推荐引擎（序列推荐+直接推荐+解释生成+评论相关+评分预测），实现基于prompt的指令推荐                                                                                           |
|    M6-Rec✅    | M6-Rec: Generative Pretrained Language Models are Open-Ended Recommender Systems                             |          M6-base (300M)          |         Option Tuning         |      Arxiv 2022      |   [[Paper]](https://arxiv.org/abs/2205.08084)   | 用户行为转化为纯文本，训练任务包括CTR/CVR+解释生成+query生成+对话推荐+产品生成+检索任务等（无ID）。同时设计多个优化操作，如option tuning等                                                                   |
| InstructRec✅ | Recommendation as Instruction Following: A Large Language Model Empowered Recommendation Approach            |         FLAN-T5-XL (3B)         |        Full Finetuning        |      Arxiv 2023      |   [[Paper]](https://arxiv.org/abs/2305.07001)   | 设计39粗粒度instruction prompt（Preference+Intention+Task Form+Context）用于不同场景，并基于此自动生成多个细粒度个性化instruction（无ID），将推荐任务转化为instruction following范式，实现用户自由地表达需求 |
|   ChatGPT✅   | Is ChatGPT a Good Recommender? A Preliminary Study                                                           |             ChatGPT             |            Frozen            |      Arxiv 2023      |   [[Paper]](https://arxiv.org/abs/2304.10149)   | 探测ChatGPT在A评分预测、B直接推荐、C序列推荐、D解释生成和E评论总结五方面的能力。结论是A、D和E表现较佳，但是B和C表现差                                                                                        |
|   ChatGPT✅   | Is ChatGPT Good at Search? Investigating Large Language Models as Re-Ranking Agent                           |             ChatGPT             |            Frozen            |      Arxiv 2023      | [[Code]](https://github.com/sunnweiwei/RankGPT) | 已有工作缺乏对LLM对于文档重拍能力的探索，本文验证了GPT4相比于SOTA的优越性，此外本文也将ChatGPT排序能力蒸馏到小模型，实现性能的提升                                                                           |
|   ChatGPT✅   | Uncovering ChatGPT's Capabilities in Recommender Systems                                                     |             ChatGPT             |            Frozen            |      RecSys 2023      |  [[Code]](https://github.com/rainym00d/LLM4RS)  | 探测ChatGPT在point-wise，pair-wise和list-wise下的推荐性能                                                                                                                                                    |
| BDLM✅ | Bridging the Information Gap Between Domain-Specific Model and General LLM for Personalized Recommendation | Vicuna (7B) | Full Finetuning | Arxiv 2023 | [[Paper]](https://arxiv.org/abs/2311.03778) | 大模型以文本形式表达难以区分相似但仍有微小区别的商品，且难以表示复杂的用户行为模式；传统domain-specific模型难以在数据稀疏场景表现好。提出信息共享模块，用户/物品ID token扩充词表，联合模型训练等方法。 |
|  RecRanker✅  | RecRanker: Instruction Tuning Large Language Model as Ranker for Top-k Recommendation                        |           LLaMA2 (13B)           |        Full Finetuning        |      Arxiv 2023      |   [[Paper]](https://arxiv.org/abs/2312.16018)   | 混合排序（point+pair+list）指令构建，prompt位置消偏，自适应用户采样（重要性、cluster-based，重复惩罚），推断时使用三种排序任务的（调整后）分数之和。                                                         |

</p>
</details>

<details><summary><h3 id="1.4">1.4 LLM for User Interaction</h3></summary>
<p>
<h4 id="1.4.1">1.4.1 Task-oriented User Interaction</h4>

| **Name** | **Paper**                                                                                                     | **LLM Backbone (Largest)** | **LLM Tuning Strategy** | **Publication** |              **Link**              | Main Contributions |
| :------------: | :------------------------------------------------------------------------------------------------------------------ | :------------------------------: | :---------------------------: | :-------------------: | :--------------------------------------: | ------------------ |
|   TG-ReDial   | Towards Topic-Guided Conversational Recommender System                                                              |  BERT-base (110M) & GPT2 (110M)  |            Unknown            |      COLING 2020      | [[Paper]](https://arxiv.org/abs/2010.04125) |                    |
|      TCP      | Follow Me: Conversation Planning for Target-driven Recommendation Dialogue Systems                                  |         BERT-base (110M)         |        Full Finetuning        |      Arxiv 2022      | [[Paper]](https://arxiv.org/abs/2208.03516) |                    |
|      MESE      | Improving Conversational Recommendation Systems' Quality with Context-Aware Item Meta-Information                   |  DistilBERT (67M) & GPT2 (110M)  |        Full Finetuning        |       ACL 2022       | [[Paper]](https://arxiv.org/abs/2112.08140) |                    |
|           |                                                              |                                |                         |                     |                                             |                    |
|    UniMIND    | A Unified Multi-task Learning Framework for Multi-goal Conversational Recommender Systems                           |         BART-base (139M)         |        Full Finetuning        |     ACM TOIS 2023     | [[Paper]](https://arxiv.org/abs/2204.06923) |                    |
|     VRICR     | Variational Reasoning over Incomplete Knowledge Graphs for Conversational Recommendation                            |         BERT-base (110M)         |        Full Finetuning        |       WSDM 2023       | [[Paper]](https://arxiv.org/abs/2212.11868) |                    |
|      KECR      | Explicit Knowledge Graph Reasoning for Conversational Recommendation                                                |  BERT-base (110M) & GPT2 (110M)  |            Frozen            |     ACM TIST 2023     | [[Paper]](https://arxiv.org/abs/2305.00783) |                    |
|      N/A      | Large Language Models as Zero-Shot Conversational Recommenders                                                      |               GPT4               |            Frozen            |       CIKM 2023       | [[Paper]](https://arxiv.org/abs/2308.10053) |                    |
|    MuseChat    | MuseChat: A Conversational Music Recommendation System for Videos                                                   |           Vicuna (7B)           |             LoRA             |      Arxiv 2023      | [[Paper]](https://arxiv.org/abs/2310.06282) |                    |
|      N/A      | Conversational Recommender System and Large Language Model Are Made for Each Other in E-commerce Pre-sales Dialogue |        Chinese-Alpaca (7B)        |             LoRA             |  EMNLP 2023 Findings  | [[Paper]](https://arxiv.org/abs/2310.14626) |                    |

<h4 id="1.4.2">1.4.2 Open-ended User Interaction</h4>

| **Name**  | **Paper**                                                    |  **LLM Backbone (Largest)**   |  **LLM Tuning Strategy**   | **Publication** |                  **Link**                   | Main Contributions |
| :-------: | :----------------------------------------------------------- | :---------------------------: | :------------------------: | :-------------: | :-----------------------------------------: | ------------------ |
|  BARCOR   | BARCOR: Towards A Unified Framework for Conversational Recommendation Systems |       BART-base (139M)        | Selective-layer Finetuning |   Arxiv 2022    | [[Paper]](https://arxiv.org/abs/2203.14257) |                    |
| RecInDial | RecInDial: A Unified Framework for Conversational Recommendation with Pretrained Language Models |        DialoGPT (110M)        |      Full Finetuning       |    AACL 2022    | [[Paper]](https://arxiv.org/abs/2110.07477) |                    |
|  UniCRS   | Towards Unified Conversational Recommender Systems via Knowledge-Enhanced Prompt Learning |     DialoGPT-small (176M)     |           Frozen           |    KDD 2022     | [[Paper]](https://arxiv.org/abs/2206.09363) |                    |
|   T5-CR   | Multi-Task End-to-End Training Improves Conversational Recommendation |        T5-base (223M)         |      Full Finetuning       |   Arxiv 2023    | [[Paper]](https://arxiv.org/abs/2305.06218) |                    |
|    TtW    | Talk the Walk: Synthetic Data Generation for Conversational Music Recommendation | T5-base (223M) & T5-XXL (11B) |  Full Finetuning & Frozen  |   Arxiv 2023    |                                             |                    |
|    N/A    | Rethinking the Evaluation for Conversational Recommendation in the Era of Large Language Models |            ChatGPT            |           Frozen           |   EMNLP 2023    | [[Paper]](https://arxiv.org/abs/2305.13112) |                    |

</p>
</details>

<details><summary><h3 id="1.5">1.5 LLM for RS Pipeline Controller</h3></summary>
<p>


| **Name** | **Paper**                                                                                  | **LLM Backbone (Largest)** | **LLM Tuning Strategy** | **Publication** |              **Link**              | Main Contributions |
| :------------: | :----------------------------------------------------------------------------------------------- | :------------------------------: | :---------------------------: | :-------------------: | :--------------------------------------: | ------------------ |
|    Chat-REC    | Chat-REC: Towards Interactive and Explainable LLMs-Augmented Recommender System                  |             ChatGPT             |            Frozen            |      Arxiv 2023      | [[Paper]](https://arxiv.org/abs/2303.14524) |                    |
|     RecLLM     | Leveraging Large Language Models in Conversational Recommender Systems                           |            LLaMA (7B)            |        Full Finetuning        |      Arxiv 2023      | [[Paper]](https://arxiv.org/abs/2305.07961) |                    |
|      RAH      | RAH! RecSys-Assistant-Human: A Human-Central Recommendation Framework with Large Language Models |               GPT4               |            Frozen            |      Arxiv 2023      | [[Paper]](https://arxiv.org/abs/2308.09904) |                    |
|    RecMind    | RecMind: Large Language Model Powered Agent For Recommendation                                   |             ChatGPT             |            Frozen            |      Arxiv 2023      | [[Paper]](https://arxiv.org/abs/2308.14296) |                    |
|  InteRecAgent  | Recommender AI Agent: Integrating Large Language Models for Interactive Recommendations          |               GPT4               |            Frozen            |      Arxiv 2023      | [[Paper]](https://arxiv.org/abs/2308.16505) |                    |
|      CORE      | Lending Interaction Wings to Recommender Systems with Conversational Agents                      |               N/A               |              N/A              |       NIPS 2023       | [[Paper]](https://arxiv.org/abs/2310.04230) |                    |

</p>
</details>

<details><summary><h3 id="1.6">1.6 Other Related Papers</h3></summary>
<p>

<h4 id="1.6.1">1.6.1 Related Survey Papers</h4> 


| **Paper**                                                                                                                |        **Publication**        |              **Link**              | Main Contributions |
| :----------------------------------------------------------------------------------------------------------------------------- | :---------------------------------: | :--------------------------------------: | ------------------ |
| Prompting Large Language Models for Recommender Systems: A Comprehensive Framework and Empirical Analysis                      |             Arixv 2024             | [[Paper]](https://arxiv.org/abs/2401.04997) |                    |
| User Modeling in the Era of Large Language Models: Current Research and Future Directions                                      | IEEE Data Engineering Bulletin 2023 | [[Paper]](https://arxiv.org/abs/2312.11518) |                    |
| A Survey on Large Language Models for Personalized and Explainable Recommendations                                             |             Arxiv 2023             | [[Paper]](https://arxiv.org/abs/2311.12338) |                    |
| Large Language Models for Generative Recommendation: A Survey and Visionary Discussions                                        |             Arxiv 2023             | [[Paper]](https://arxiv.org/abs/2309.01157) |                    |
| Large Language Models for Information Retrieval: A Survey                                                                      |             Arxiv 2023             | [[Paper]](https://arxiv.org/abs/2308.07107) |                    |
| When Large Language Models Meet Personalization: Perspectives of Challenges and Opportunities                                  |             Arxiv 2023             | [[Paper]](https://arxiv.org/abs/2307.16376) |                    |
| Recommender Systems in the Era of Large Language Models (LLMs)                                                                 |             Arxiv 2023             | [[Paper]](https://arxiv.org/abs/2307.02046) |                    |
| A Survey on Large Language Models for Recommendation                                                                           |             Arxiv 2023             | [[Paper]](https://arxiv.org/abs/2305.19860) |                    |
| Pre-train, Prompt and Recommendation: A Comprehensive Survey of Language Modelling Paradigm Adaptations in Recommender Systems |              TACL 2023              | [[Paper]](https://arxiv.org/abs/2302.03735) |                    |
| Self-Supervised Learning for Recommender Systems: A Survey                                                                     |              TKDE 2022              | [[Paper]](https://arxiv.org/abs/2203.15876) |                    |

<h4 id="1.6.2">1.6.2 Other Papers</h4>

| **Paper**                                                                         | **Publication** |                       **Link**                       | Main Contributions |
| :-------------------------------------------------------------------------------------- | :-------------------: | :--------------------------------------------------------: | ------------------ |
| Large Language Model Can Interpret Latent Space of Sequential Recommender               |      Arxiv 2023      |          [[Paper]](https://arxiv.org/abs/2310.20487)          |                    |
| Zero-Shot Recommendations with Pre-Trained Large Language Models for Multimodal Nudging |      Arxiv 2023      |          [[Paper]](https://arxiv.org/abs/2309.01026)          |                    |
| INTERS: Unlocking the Power of Large Language Models in Search with Instruction Tuning  |      Arxiv 2024      |          [[Paper]](https://arxiv.org/abs/2401.06532)          |                    |
| Evaluation of Synthetic Datasets for Conversational Recommender Systems                 |      Arxiv 2023      |         [[Paper]](https://arxiv.org/abs/2212.08167v1)         |                    |
| Generative Recommendation: Towards Next-generation Recommender Paradigm                 |      Arxiv 2023      |          [[Paper]](https://arxiv.org/abs/2304.03516)          |                    |
| Towards Personalized Prompt-Model Retrieval for Generative Recommendation               |      Arxiv 2023      |          [[Paper]](https://arxiv.org/abs/2308.02205)          |                    |
| Generative Next-Basket Recommendation                                                   |      RecSys 2023      | [[Paper]](https://dl.acm.org/doi/abs/10.1145/3604915.3608823) |                    |

</p>
</details>

<details><summary><h3 id="1.7">1.7 Paper Pending List: to be Added to Our Survey Paper</h3></summary>
<p>


|  **Name**  | **Paper**                                                                                                                         | **LLM Backbone (Largest)** | **LLM Tuning Strategy** |     **Publication**     |                       **Link**                       |
| :---------------: | :-------------------------------------------------------------------------------------------------------------------------------------- | :------------------------------: | :---------------------------: | :----------------------------: | :--------------------------------------------------------: |
|                  | A Large Language Model Enhanced Conversational Recommender System                                                                       |                                  |                              |           Arxiv 2023           |          [[Paper]](https://arxiv.org/abs/2308.06212)          |
|                  | User-Centric Conversational Recommendation: Adapting the Need of User with Large Language Models                                        |                                  |                              | RecSys Doctoral Symposium 2023 | [[Paper]](https://dl.acm.org/doi/abs/10.1145/3604915.3608885) |
|                  | Improving Conversational Recommendation Systems via Bias Analysis and Language-Model-Enhanced Data Augmentation                         |                                  |                              |           Arxiv 2023           |          [[Paper]](https://arxiv.org/abs/2310.16738)          |
|                  | Enhancing Recommender Systems with Large Language Model Reasoning Graphs                                                                |                                  |                              |           Arxiv 2023           |          [[Paper]](https://arxiv.org/abs/2308.10835)          |
|                  | Large Language Model based Long-tail Query Rewriting in Taobao Search                                                                   |                                  |                              |           Arxiv 2023           |          [[Paper]](https://arxiv.org/abs/2311.03758)          |
|                  | Knowledge Graphs and Pre-trained Language Models enhanced Representation Learning for Conversational Recommender Systems                |                                  |                              |           Arxiv 2023           |          [[Paper]](https://arxiv.org/abs/2312.10967)          |
|                  | Unlocking the Potential of Large Language Models for Explainable Recommendations                                                        |                                  |                              |           Arxiv 2023           |          [[Paper]](https://arxiv.org/abs/2312.15661)          |
|                  | The Challenge of Using LLMs to Simulate Human Behavior: A Causal Inference Perspective                                                  |                                  |                              |           Arxiv 2023           |          [[Paper]](https://arxiv.org/abs/2312.15524)          |
|                  | Empowering Few-Shot Recommender Systems with Large Language Models -- Enhanced Representations                                          |                                  |                              |          IEEE Access          |          [[Paper]](https://arxiv.org/abs/2312.13557)          |
|                  | dIR -- Discrete Information Retrieval: Conversational Search over Unstructured (and Structured) Data with Large Language Models         |                                  |                              |           Arxiv 2023           |          [[Paper]](https://arxiv.org/abs/2312.13264)          |
| Logic-Scaffolding | Logic-Scaffolding: Personalized Aspect-Instructed Recommendation Explanation Generation using LLMs                                      |           Falcon (40B)           |            Frozen            |           WSDM 2024           |          [[Paper]](https://arxiv.org/abs/2312.14345)          |
|                  | Unveiling Bias in Fairness Evaluations of Large Language Models: A Critical Literature Review of Music and Movie Recommendation Systems |                                  |                              |           Arxiv 2024           |          [[Paper]](https://arxiv.org/abs/2401.04057)          |
|                  | ChatGPT for Conversational Recommendation: Refining Recommendations by Reprompting with Feedback                                        |                                  |                              |           Arxiv 2024           |          [[Paper]](https://arxiv.org/abs/2401.03605)          |
|                  | Combining Embedding-Based and Semantic-Based Models for Post-hoc Explanations in Recommender Systems                                    |                                  |                              |           Arxiv 2024           |          [[Paper]](https://arxiv.org/abs/2401.04474)          |
|                  | Understanding Biases in ChatGPT-based Recommender Systems: Provider Fairness, Temporal Stability, and Recency                           |                                  |                              |           Arxiv 2024           |          [[Paper]](https://arxiv.org/abs/2401.10545)          |
|                  | LLM4Vis: Explainable Visualization Recommendation using ChatGPT                                                                         |                                  |                              |           EMNLP 2023           |          [[Paper]](https://arxiv.org/abs/2310.07652)          |
|                  | Parameter-Efficient Conversational Recommender System as a Language Processing Task                                                     |                                  |                              |           EACL 2024           |          [[Paper]](https://arxiv.org/abs/2401.14194)          |
| | Data-efficient Fine-tuning for LLM-based Recommendation | | | Arxiv 2024 | [[Paper]](https://arxiv.org/abs/2401.17197) |
| | Prompt-enhanced Federated Content Representation Learning for Cross-domain Recommendation | | | WWW 2024 |  |
| | LoRec: Large Language Model for Robust Sequential Recommendation against Poisoning Attacks | | | Arxiv 2024 |  |
| | PAP-REC: Personalized Automatic Prompt for Recommendation Language Model | | | Arxiv 2024 |  |
| | From PARIS to LE-PARIS: Toward Patent Response Automation with Recommender Systems and Collaborative Large Language Models | | | Arxiv 2024 |  |
| | Uncertainty-Aware Explainable Recommendation with Large Language Models | | | Arxiv 2024 | [[Paper]](https://arxiv.org/abs/2402.03366) |

</p>
</details>

<h2 id="2">2. LLM & Graph</h2>

| **Name** | **Paper** | **LLM Backbone (Largest)** | **LLM Tuning Strategy** | **Publication** | **Link** | Main Contributions |
| :------------: | :-------------- | :------------------------------: | :---------------------------: | :-------------------: | :------------: | :----------------: |
|                |                 |                                  |                              |                      |                |                    |

<h2 id="3"> 3. Datasets & Benchmarks </h2>

The datasets & benchmarks for LLM-related RS topics should maintain the original semantic/textual features, instead of anonymous feature IDs.

<h3 id="3.1">3.1 Datasets</h3>

| **Dataset** | **RS Scenario** |                                                               **Link**                                                               | Main Contributions |
| :---------------: | :--------------------: | :----------------------------------------------------------------------------------------------------------------------------------------: | ------------------ |
|   Reddit-Movie   | Conversational & Movie | [[Link]](https://github.com/AaronHeee/LLMs-as-Zero-Shot-Conversational-RecSys#large-language-models-as-zero-shot-conversational-recommenders) |                    |
|     Amazon-M2     |       E-commerce       |                                                  [[Link]](https://arxiv.org/abs/2307.09688)                                                  |                    |
|     MovieLens     |         Movie         |                                            [[Link]](https://grouplens.org/datasets/movielens/1m/)                                            |                    |
|      Amazon      |       E-commerce       |                                   [[Link]](https://cseweb.ucsd.edu/~jmcauley/datasets.html#amazon_reviews)                                   |                    |
|   BookCrossing   |          Book          |                                        [[Link]](http://www2.informatik.uni-freiburg.de/~cziegler/BX/)                                        |                    |
|     GoodReads     |          Book          |                                          [[Link]](https://mengtingwan.github.io/data/goodreads.html)                                          |                    |
|       Anime       |         Anime         |                             [[Link]](https://www.kaggle.com/datasets/CooperUnion/anime-recommendations-database)                             |                    |
|     PixelRec     |      Short Video      |                                              [[Link]](https://github.com/westlake-repl/PixelRec)                                              |                    |
|      Netflix      |         Movie         |                                                   [[Link]](https://github.com/HKUDS/LLMRec)                                                   |                    |

<h3 id="3.2">3.2 Benchmarks</h3>

|   **Benchmarks**   |                                      **Webcite Link**                                      |             **Paper**             | Main Contributions |
| :----------------------: | :-----------------------------------------------------------------------------------------------: | :--------------------------------------: | ------------------ |
| Amazon-M2 (KDD Cup 2023) | [[Link]](https://www.aicrowd.com/challenges/amazon-kdd-cup-23-multilingual-recommendation-challenge) | [[Paper]](https://arxiv.org/abs/2307.09688) |                    |
|          LLMRec          |                           [[Link]](https://github.com/williamliujl/LLMRec)                           | [[Paper]](https://arxiv.org/abs/2308.12241) |                    |
|          OpenP5          |                           [[Link]](https://github.com/agiresearch/OpenP5)                           | [[Paper]](https://arxiv.org/abs/2306.11134) |                    |
|          TABLET          |                             [[Link]](https://dylanslacks.website/Tablet)                             | [[Paper]](https://arxiv.org/abs/2304.13188) |                    |

<h2 id="4">Related Repositories</h2>

|                                                  **Repo Name**                                                  |           **Maintainer**           |           Link           |
| :-------------------------------------------------------------------------------------------------------------------: | :--------------------------------------: | :--------------------------------------: |
|                            [rs-llm-paper-list](https://github.com/wwliu555/rs-llm-paper-list)                            |   [wwliu555](https://github.com/wwliu555)   |      |
| [awesome-recommend-system-pretraining-papers](https://github.com/archersama/awesome-recommend-system-pretraining-papers) | [archersama](https://github.com/archersama) |  |
|                                        [LLM4Rec](https://github.com/WLiK/LLM4Rec)                                        |       [WLiK](https://github.com/WLiK)       |              |
|                       [Awesome-LLM4RS-Papers](https://github.com/nancheng58/Awesome-LLM4RS-Papers)                       | [nancheng58](https://github.com/nancheng58) |  |
|                               [LLM4IR-Survey](https://github.com/RUC-NLPIR/LLM4IR-Survey)                               |  [RUC-NLPIR](https://github.com/RUC-NLPIR)  |    |
| [Awesome-LLM-for-RecSys](https://github.com/CHIANGEL/Awesome-LLM-for-RecSys) | [Jianghao Lin](https://github.com/CHIANGEL) | [[Survey]](https://github.com/CHIANGEL/Awesome-LLM-for-RecSys) |
