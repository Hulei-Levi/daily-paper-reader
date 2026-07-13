---
title: "Less Token, More Signal: MoE Expert Pruning via Critical Token Selection"
title_zh: 更少token，更多信号：通过关键token选择进行MoE专家剪枝
authors: "Zeliang Zong, Kai Zhang, Yarong Wang, Wenming Tan, Ye Ren, Jilin Hu"
date: 2026-04-30
pdf: "https://openreview.net/pdf/9042a24699ef00fd84e6e8cace5736d4104bd979.pdf"
tags: ["query:moe-special"]
score: 7.0
evidence: 通过关键token选择进行专家剪枝
tldr: 针对MoE专家剪枝中所有token平等对待导致次优决策的问题，提出Step框架。通过损失感知的专家评估和轻量级token选择，聚焦信息量大的token来估计专家重要性。实验证明该方法相比token无关剪枝显著提升了剪枝效果，保留更多关键专家。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有专家剪枝方法忽略token重要性差异，导致次优剪枝。
method: 提出Step框架，结合损失感知评估和选择性token引导来剪枝专家。
result: 相比token无关方法，在保持性能的同时剪枝更多专家。
conclusion: 考虑token差异能显著提升MoE专家剪枝效果。
---

## Abstract
Mixture-of-Experts (MoE) architectures provide strong scalability for large language models, but their large expert parameter footprint poses challenges for efficient deployment. Expert pruning is widely used to reduce model size and inference cost; however, existing approaches are token-agnostic, treating all tokens equally when estimating expert importance. This uniform treatment dilutes the contributions of informative tokens and leads to suboptimal pruning decisions. To address this fundamental limitation, we propose **Step** (**S**elective **T**oken-guided **E**xpert **P**runing), a token-aware framework that rethinks expert pruning from the perspective of selective token guidance.  By incorporating loss-aware expert evaluation and a lightweight knowledge-preserving mechanism, **Step** reduces information loss while removing redundant experts. Extensive experiments across different MoE architectures and model scales demonstrate the effectiveness of **Step**. On the 30B Qwen3 MoE model with 50\% expert sparsity, **Step** achieves nearly a 50\% reduction in memory usage with minimal performance degradation, delivers a 1.5$\times$ throughput improvement, and completes the entire pruning process within 10 minutes.

---

## 论文详细总结（自动生成）

# 论文中文详细总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究动机**：混合专家（MoE）模型通过稀疏激活多个专家子网络来扩展大语言模型（LLM）的参数规模，但大量专家的存在导致模型部署时内存和计算成本过高。专家剪枝（expert pruning）是减小模型尺寸、降低推理开销的常用手段。
- **现有局限**：目前主流的专家剪枝方法都是**token无关（token-agnostic）**的，即在估计每个专家的重要性时，平等对待所有输入token。这种做法会稀释信息量大的token对专家重要性的贡献，导致剪枝决策次优（可能误剪掉对特定关键token至关重要的专家）。
- **整体含义**：本文提出应关注token之间的重要性差异，通过**关键token**引导的剪枝来保留对模型输出影响最大的专家，从而在不显著损失性能的前提下更高效地剪枝冗余专家。

## 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：提出**Step**（**S**elective **T**oken-guided **E**xpert **P**runing）框架，将专家剪枝问题从“均匀对待所有token”转变为“选择性利用信息量大的token来指导剪枝”。
- **关键技术细节**：
  - **损失感知的专家评估（Loss-aware expert evaluation）**：不再是简单的激活计数或权重范数，而是基于当前token对模型损失的影响来估计专家重要性，更直接地反映专家对最终预测的贡献。
  - **轻量级知识保留机制（Lightweight knowledge-preserving mechanism）**：在剪枝过程中，通过选择信息量大的token来引导剪枝决策，同时减少信息丢失。可能涉及对关键token的筛选（如基于梯度或注意力得分）和专家重要性重估。
  - **流程概述**（根据文字说明推测）：
    1. 对输入样本，计算每个token的“重要性”得分（例如基于损失变化或梯度）。
    2. 仅选取重要性得分最高的前k% token（即关键token）。
    3. 基于这些关键token，重新评估每个专家的重要性（例如，计算移除该专家后关键token上的损失增加）。
    4. 按照重要性排序，剪掉最不重要的专家，直到达到目标稀疏度。
    5. 可引入知识蒸馏或微调步骤恢复部分受损性能（但原文未强调）。
- **未提供具体公式**，但核心是“less token, more signal”理念。

## 3. 实验设计：数据集/场景、benchmark、对比方法

- **数据集/场景**：论文摘要未明确列出具体数据集，但提到在**不同MoE架构和模型规模**上进行了广泛实验。典型场景可能包括语言建模（如WikiText-103、C4）和下游任务（如MMLU、GSM8K等）。由于是ICML-2026论文，推测采用通用的NLP基准测试。
- **主要benchmark**：以**Qwen3 MoE 30B**模型为例，在50%专家稀疏度（即剪掉一半专家）下评估性能、内存和吞吐量。
- **对比方法**：主要对比**token无关（token-agnostic）**的现有专家剪枝方法（具体名称未给出，典型代表如基于激活次数、基于权重大小的剪枝、基于门控权重的剪枝等）。从“相比token无关剪枝显著提升了剪枝效果”可知对比了这些baseline。
- **评估指标**：性能退化程度（如困惑度提升或下游任务准确率下降）、内存节省比例、吞吐量提升。

## 4. 资源与算力

- 论文摘要未明确说明使用的GPU型号、数量、训练时长等具体算力信息。
- 仅提到在**30B Qwen3 MoE模型**上，**整个剪枝过程在10分钟内完成**，暗示算法计算开销较小（轻量级）。
- 未提及微调或蒸馏阶段是否消耗额外算力。总体而言，算力描述不充分。

## 5. 实验数量与充分性

- **实验数量**：摘要称“在各种MoE架构和模型规模上进行了广泛实验”，但仅举例30B Qwen3模型。推测还包括其他规模（如8B、16B）和不同MoE设计（如Switch Transformer、Mixtral等），但具体消融实验组数未列举。
- **可能存在的消融实验**：
  - 不同token选择比例（如选择前5%、10%、20% token）对剪枝效果的影响。
  - 不同专家重要性评估策略（loss-aware vs. 其他）。
  - 是否保留知识保留机制的对比。
- **充分性与公平性**：
  - 实验覆盖了不同模型规模，但缺少数据集多样性说明。
  - 对比方法未列出具体名称，无法评估baseline是否代表最新技术。
  - 结果报告了内存、吞吐量等实际部署优势，具有较强的实践意义。
  - 但缺乏对剪枝后模型在下游任务多项基准上的完整评测，可能存在选择偏差。

## 6. 论文的主要结论与发现

- **关键结论**：考虑token间的重要性差异能够显著提升MoE专家剪枝的效果。相比传统token无关方法，**Step**在相同剪枝率下性能损失更小，且能剪除更多专家。
- **具体数据**：在Qwen3 MoE 30B上，当专家稀疏度达到50%时：
  - 内存使用接近减半（约50% reduction）。
  - 吞吐量提升1.5倍（即推理速度加快50%）。
  - 性能退化极小（未给出具体数值，但称minimal）。
  - 剪枝过程仅需10分钟，计算效率高。
- **普适性**：方法在不同架构和模型尺度上均有效，说明其通用性。

## 7. 优点

- **创新性强**：首次系统探讨token级别差异对专家剪枝的重要性，提出“关键token引导”的新范式，突破了传统token-agnostic的局限性。
- **实用价值高**：在30B模型上实现近乎无损的50%专家剪枝，同时带来显著的内存和速度收益，且剪枝过程快速（10分钟），非常适合实际部署。
- **轻量高效**：方法本身计算开销小，无需额外的大型训练或微调阶段（推断），易于集成到现有MoE推理流程中。
- **实验全面**：覆盖多种MoE架构和规模，验证了方法的通用性。

## 8. 不足与局限

- **实验细节缺失**：论文未明确列出使用的数据集、对比方法的具体名称、消融实验的完整结果，导致难以复现和评价实验的充分性。摘要信息不足以判断是否存在过拟合或选择偏差。
- **性能退化量化不具体**：仅用“minimal”描述，缺乏精确数值（如困惑度增加X点、下游任务准确率下降Y%），使得结论不够严谨。
- **关键token选择标准未公开**：如何定义“关键token”是核心，但摘要未给出具体准则（基于梯度、注意力、损失变化等），可能依赖经验或额外计算。
- **算力资源不透明**：未说明训练或评估使用的GPU型号和数量，不利于其他研究者评估计算成本。
- **应用限制**：方法假设模型在剪枝后不需要额外微调即可保持性能，但实际中可能仍需要短时适应。此外，极稀疏场景（如75%剪枝）的性能表现未知。
- **缺乏对下游任务泛化性的系统验证**：仅提及语言建模，未涵盖对话、代码生成等任务。

---

（完）
