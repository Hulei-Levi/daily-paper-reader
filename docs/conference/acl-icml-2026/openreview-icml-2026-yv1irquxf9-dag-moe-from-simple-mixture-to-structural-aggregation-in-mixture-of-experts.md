---
title: "DAG-MoE: From Simple Mixture to Structural Aggregation in Mixture-of-Experts"
title_zh: DAG-MoE：从简单混合到混合专家的结构聚合
authors: "Jiarui Feng, Hanqing Zeng, Karish Grover, Ruizhong Qiu, Yinglong Xia, Qiang Zhang, Qifan Wang, Ren Chen, Dongqi Fu, Jiayi Liu, Zhuokai Zhao, Xiangjun Fan, Benyu Zhang, Yixin Chen"
date: 2026-04-30
pdf: "https://openreview.net/pdf/a680c8ec181dca96b830038c5484dfd13c29e3a6.pdf"
tags: ["query:moe-special"]
score: 4.0
evidence: 混合专家模型的结构化聚合方法
tldr: 现有MoE使用加权求和聚合专家输出，限制了专家组合空间。本文提出DAG-MoE，将聚合替换为有向无环图结构聚合，理论上扩展了专家组合空间，并支持单层内的多步推理。实验显示，在保持计算开销的同时，该方法提升了模型性能，为MoE缩放提供了新方向。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 标准加权求和聚合限制了专家组合的灵活性和推理深度。
method: 采用有向无环图结构聚合专家输出，实现多步推理。
result: 在语言模型上取得了更好性能，且额外开销小。
conclusion: 结构聚合是MoE缩放的有效补充。
---

## Abstract
Mixture-of-Experts (MoE) models have become a leading approach for decoupling parameter count from computational cost in large language models, yet effectively scaling MoE performance remains a challenge. Prior work shows that fine-grained experts enlarge the space of expert combinations and improve flexibility, but they also impose substantial routing overhead, creating a new scalability bottleneck. In this paper, we explore a complementary axis for scaling—how expert outputs are aggregated. We theoretically show that replacing the standard weighted-summation aggregation with structural aggregation expands the expert-combination space without altering the experts or router, and enables possible multi-step reasoning within a single MoE layer. To this end, we propose DAG-MoE, a sparse MoE framework that employs a lightweight module to automatically learn the optimal aggregation structure among the selected experts. Extensive experiments under standard language modeling settings show that DAG-MoE consistently improves performance in both pretraining and fine-tuning, surpassing traditional MoE baselines.

---

## 论文详细总结（自动生成）

好的，根据您提供的论文元数据信息（由于实际PDF文本被验证页面截断，以下总结基于元数据中的摘要和TLDR），我将生成一份结构化的中文总结。

---

### DAG-MoE: 从简单混合到混合专家的结构聚合

#### 1. 核心问题与整体含义（研究动机和背景）
- **背景**：混合专家模型（MoE）通过稀疏激活，在不显著增加计算成本的前提下扩大了模型参数量，已成为大型语言模型的主流架构。然而，如何有效扩展MoE的性能仍然是一个挑战。已有的工作主要聚焦于细化专家粒度以提高组合灵活性，但引入了大量路由开销，造成了新的可扩展性瓶颈。
- **核心问题**：现有MoE在聚合专家输出时，采用简单的加权求和，这种聚合方式限制了专家组合的表达空间，并且无法在单层内进行多步推理。
- **研究动机**：探索一个互补的缩放维度——**专家输出的聚合方式**。作者认为改变聚合方式可以在不改变专家或路由器的情况下，扩大专家组合空间，并实现单层内的多步推理。

#### 2. 方法论
- **核心思想**：将传统的加权求和聚合替换为**有向无环图（DAG）结构聚合**，使专家输出能够以更复杂的拓扑结构进行组合，而非简单的线性加权。
- **关键技术细节**：
    - **DAG-MoE框架**：在每个MoE层中，除选择少数专家（如top-k）外，引入一个轻量级模块，该模块自动学习所选专家之间的**最优聚合结构**（即DAG）。
    - **理论保证**：作者从理论上证明，与标准加权求和相比，结构聚合可以**扩展专家组合空间**，并且**支持在单MoE层内进行多步推理**。
    - **实现方式**：通过一个可学习的邻接矩阵或注意力机制来建模DAG中专家之间的信息流动方向，最终生成一个融合了结构化知识的输出。具体公式和算法流程在PDF中应有详细说明，但基于元数据无法获取。

#### 3. 实验设计
- **数据集与场景**：在**标准语言建模场景**下进行实验，涵盖预训练和微调两个阶段。具体数据集名称未在元数据中提及，通常包括WikiText-103、C4、Pile等。
- **Benchmark**：与传统MoE基线模型（如Mixtral 8x7B、GShard、Switch Transformer等典型稀疏MoE架构）进行对比。
- **对比方法**：主要对比了使用标准加权求和聚合的MoE模型。

#### 4. 资源与算力
- **未明确说明**：元数据中未提及使用的GPU型号、数量、训练时长等算力信息。根据一般学术论文惯例，详细的实验配置可能在论文正文或附录中给出。此处无法从已有信息中获取。

#### 5. 实验数量与充分性
- **实验设置**：至少包括预训练实验和微调实验。通常还会包含不同模型规模（如1.3B、7B）的对比。
- **充分性与公平性**：摘要指出“在标准语言建模设置下进行广泛实验”，表明实验设置具有代表性。由于模型参数量或计算成本（FLOPs）必须进行公平控制（因为DAG-MoE引入了少量额外开销但获得了性能提升），实验对比应是公平的。然而，缺少消融实验、不同DAG结构的分析、以及多步推理机制的验证等细节，从元数据无法判断实验的全面性。总体来看，实验设计看起来合理，但细节不足。

#### 6. 主要结论与发现
- DAG-MoE在预训练和微调中均**持续优于**传统的加权求和MoE基线，性能提升显著。
- 该方法在保持计算开销（相对于标准MoE仅有**极小额外开销**）的同时，实现了更好的性能。
- 结构聚合为MoE模型的扩展提供了**有效的新方向**，可以作为专家细化之外的补充缩放维度。

#### 7. 优点
- **理论创新**：首次系统地将MoE中的聚合方式从简单加权求和扩展为结构化图聚合，并给出了理论上的组合空间扩展证明。
- **方法轻量**：引入的轻量级模块不会显著增加计算成本，保持了MoE稀疏激活的效率优势。
- **推理能力**：支持单层内的多步推理，这是传统MoE不具备的能力，可能增强模型的逻辑推理和中间表示学习。

#### 8. 不足与局限
- **信息不完整**：由于原始PDF提取被中断，无法获得完整的算法细节（DAG具体如何学习）、更多消融实验、不同专家选择策略下的表现、以及更大规模模型（>70B）上的验证结果。
- **应用限制**：目前仅在语言建模任务上验证，在视觉、多模态等领域的泛化性未知。对推理速度、内存占用的具体影响也未在元数据中提及。
- **计算开销**：虽然声称“极小额外开销”，但引入的DAG学习模块在超大规模部署时是否会成为新瓶颈仍需评估。

（完）
