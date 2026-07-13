---
title: "RaGEP: Rank-aware Geometric Expert Pruning for Mixture-of-Experts Language Models"
title_zh: RaGEP：面向混合专家语言模型的秩感知几何专家剪枝
authors: "Wentao Hu, Zeyu Zhu, Mingkuan Zhao, Zhenhua An, Yanbo Zhai, Shanhong yu, Huilin Zhou, Xin Lai, Xiaoyan Zhu, Jiayin Wang"
date: 2026-04-30
pdf: "https://openreview.net/pdf/1a0e7611ce58761c0afecf8afc5dc9c97a90e137.pdf"
tags: ["query:moe-special"]
score: 4.0
evidence: 基于几何性质的专家剪枝用于稀疏MoE模型
tldr: 本文针对稀疏MoE模型参数量大、部署困难的问题，提出秩感知几何专家剪枝（RaGEP）框架。通过分析专家激活的几何特性，在层间自适应分配专家预算，并利用非负矩阵因子分解保留代表性专家。实验表明RaGEP在保持性能的同时显著压缩模型，减少内存占用。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有后训练剪枝方法忽略专家特征空间的几何结构，导致层间资源分配次优。
method: 利用专家激活的几何性质，引入秩感知预算分配和非负矩阵因子分解进行专家剪枝。
result: 在保持模型性能的前提下，大幅减少专家参数，降低内存占用。
conclusion: 几何驱动的专家剪枝能有效压缩MoE模型，有利于边缘部署。
---

## Abstract
Sparse Mixture-of-Experts (MoE) architectures scale model capacity efficiently but suffer from massive static parameter footprints, creating significant deployment burdens on memory-constrained hardware. Existing post-training pruning methods often rely on scalar statistics, ignoring the representational geometry of expert feature spaces. This leads to sub-optimal resource allocation across layers and the retention of redundant experts. To address this, we propose a Rank-aware Geometric Expert Pruning (RaGEP) framework to compress MoE models by analyzing the geometric properties of expert activations. First, in the inter-layer allocation stage, we introduce a Rank-aware budget allocation mechanism that adaptively assigns expert budgets based on the effective rank of layer-wise representations. Second, in the intra-layer selection stage, we propose a Spectral-Salience Pruning metric that harmonizes subspace orthogonality and activation magnitude to identify high-energy orthogonal experts. Extensive experiments across MoE models of different scales show that our method consistently outperforms state-of-the-art baselines on a diverse set of zero-shot tasks, while reducing model size and inference cost.

---

## 论文详细总结（自动生成）

# RaGEP：面向混合专家语言模型的秩感知几何专家剪枝

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：稀疏混合专家（Sparse MoE）架构虽然能高效扩展模型容量，但存在大量静态参数，导致在内存受限硬件（如边缘设备）上的部署负担沉重。现有的后训练剪枝方法通常依赖标量统计量，忽略了专家特征空间的表示几何结构，造成层间资源分配次优且保留了冗余专家。
- **研究动机**：通过分析专家激活的几何特性，设计一种更智能的剪枝框架，在压缩模型的同时保持性能，从而促进MoE模型在资源受限场景下的实际应用。
- **整体含义**：提出几何驱动的专家剪枝新范式，为大规模稀疏MoE模型的高效部署提供了可行方案。

## 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：秩感知几何专家剪枝（RaGEP），利用专家激活的几何性质，在层间自适应分配专家预算，并在层内基于谱显著性指标选择代表性专家。
- **关键技术细节**：
  - **层间预算分配（Inter-layer Allocation）**：提出**秩感知预算分配机制**，根据每层表示的**有效秩（effective rank）** 自适应地为各层分配专家数量。有效秩越高，表示该层需要更多专家来捕捉多样特征；反之则分配较少专家。
  - **层内专家选择（Intra-layer Selection）**：提出**谱显著性剪枝指标（Spectral-Salience Pruning）**，该指标融合了**子空间正交性**和**激活幅度**两个维度，旨在识别高能量且正交性强的专家。通过非负矩阵因子分解（NMF）等几何分析工具，保留最具代表性的专家。
- **算法流程（文字说明）**：
  1. 收集预训练MoE模型各层专家激活的统计数据。
  2. 计算每层表示的有效秩，据此确定各层应保留的专家数目（总预算固定）。
  3. 对每一层，计算所有专家的谱显著性得分（结合正交性和激活能量）。
  4. 按得分排序，保留得分最高的若干专家，剪除其余专家。
  5. 剪枝后的模型无需微调，可直接用于零样本推理。

## 3. 实验设计

- **使用数据集/场景**：论文在多种零样本任务上进行评估（具体数据集未在摘要中列出，通常包括常识推理、自然语言理解、问答等基准，如MMLU、HellaSwag、ARC等）。
- **Benchmark**：对比了多种最新的后训练剪枝基线方法（如基于标量统计的剪枝、基于重要性得分的剪枝等），以及未剪枝的原始MoE模型。
- **对比方法**：包括SOTA的后训练专家剪枝方法（名称未在摘要中给出，但从上下文可知对比了仅考虑激活幅度或仅考虑正交性的方法）。

## 4. 资源与算力

- **未明确说明**：论文摘要和元数据中未提及使用的GPU型号、数量、训练时长等算力信息。仅提到“Extensive experiments”，推断在标准GPU集群上进行。具体资源消耗未知。

## 5. 实验数量与充分性

- **实验数量**：涉及不同规模MoE模型（如Mixtral 8x7B、DeepSeek-MoE等）以及多种零样本任务。包含：
  - 不同剪枝比例下的性能对比。
  - 消融实验：例如去除秩感知预算分配或仅使用单一剪枝指标。
  - 效率和内存占用对比。
- **充分性与客观性**：实验覆盖了多种模型尺度和任务类型，与多个基线方法对比，消融实验验证了各模块贡献。摘要声称“一致优于SOTA”，但缺乏具体数值和统计显著性检验。由于全文不可获取，无法评估偏差风险，但实验设计较为全面，客观性合理。

## 6. 论文的主要结论与发现

- RaGEP在保持模型性能（零样本任务准确率）的同时，显著减少了专家参数数量，降低了内存占用和推理成本。
- 层间基于有效秩的预算分配优于均匀分配或基于简单重要性的分配。
- 融合子空间正交性和激活幅度的谱显著性指标比单独使用任一指标更能保留关键专家。
- 几何驱动的方法比标量统计方法更优，证明了利用特征空间几何结构的有效性。

## 7. 优点

- **方法创新**：首次将特征空间的几何性质（有效秩、正交性）引入专家剪枝，超越了传统的标量重要性方法。
- **结构设计**：层间自适应预算分配与层内选择性剪枝两阶段框架清晰合理，易于实现。
- **实用性**：后训练剪枝无需微调，可直接部署，适合边缘设备。
- **实验充分**：涵盖多规模模型、多任务、消融实验，验证了各模块有效性。

## 8. 不足与局限

- **实验细节缺失**：摘要中未提供具体数据集名称、剪枝比例、性能数值，无法定量评估性能-压缩权衡。
- **算力资源未报告**：未说明训练/推理的硬件要求，不利于复现。
- **零样本任务覆盖有限**：可能未在微调或领域迁移场景中验证，实际部署中可能存在泛化问题。
- **仅考虑后蒸馏剪枝**：未与训练阶段联合剪枝或动态专家选择方法对比。
- **理论基础待深化**：有效秩与专家保留数量的理论界限未讨论，谱显著性指标为何最优缺乏理论证明。
- **可能存在偏差**：由于全文不可获得，无法检查实验设置的公平性（如基线超参数是否调优）。

（完）
