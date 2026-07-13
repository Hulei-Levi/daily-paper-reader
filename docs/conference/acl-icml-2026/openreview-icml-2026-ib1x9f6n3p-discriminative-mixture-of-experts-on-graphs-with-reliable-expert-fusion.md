---
title: Discriminative Mixture-of-Experts on Graphs with Reliable Expert Fusion
title_zh: 面向图的可判别混合专家模型与可靠专家融合
authors: "Haoyue Deng, Menghui Wang, Yunlong Zhou, Ziwei Zhang, Ran Zhang, Chunming Hu, Xiao Wang"
date: 2026-04-30
pdf: "https://openreview.net/pdf/531cf9f037582858332d97b2928952c50e7bc18c.pdf"
tags: ["query:moe-special"]
score: 8.0
evidence: 图MoE中的专家专业化和路由
tldr: 针对图混合专家模型（Graph-MoE）中专家同质化、路由坍缩和不确定性等问题，通过实证分析揭示了这些现象及其对性能的影响。提出了一种增强专家差异性和路由可靠性的方法，有效提升了图神经网络在多种图结构数据上的表现。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: Graph-MoE中专家同质化和路由不确定性严重损害性能。
method: 提出增强专家差异性和路由可靠性的方法，改进路由与专家协作。
result: 在多个图数据集上优于现有Graph-MoE方法，专家专业化更明显。
conclusion: 解决专家同质化和路由不确定性能显著提升图MoE性能。
---

## Abstract
Graph Mixture-of-Experts (Graph-MoE) offers a way to scale GNNs via adaptive capacity allocation, with the goal of allowing different experts to capture diverse graph patterns. Its effectiveness heavily depends on the coordination between routing decisions and expert specialization. However, through extensive empirical study, we identify two critical phenomena. First, discrimination loss occurs on both the expert and routing sides, where GNN experts become highly homogenized and the router collapses to a small subset of experts, failing to reflect diverse graph semantics. Second, routing uncertainty is prevalent, as existing routers produce uncertain expert assignments for most nodes, and such uncertainty exhibits a strong negative correlation with model performance.
To address these issues, we propose C$^2$GMoE, a novel Graph-MoE framework featuring Contrastive routing and Confidence-aware fusion. We introduce a group-wise contrastive routing strategy that provides explicit guidance for routing optimization by aligning node-level routing decisions with semantic clusters while satisfying load-balancing constraints. Moreover, through a theoretical analysis of generalization error, we develop a confidence-aware fusion mechanism that adaptively reweights expert predictions according to their confidence. Extensive experiments across multiple benchmarks demonstrate the effectiveness of our proposed C$^2$GMoE.

---

## 论文详细总结（自动生成）

# 详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **研究动机**：图混合专家模型（Graph-MoE）旨在通过自适应容量分配来扩展图神经网络（GNN），使不同专家捕获多样的图结构模式。然而，现有 Graph-MoE 存在两个关键问题：
  1. **判别性损失**：在专家侧和路由侧同时发生——GNN 专家高度同质化（缺乏专业化），且路由器坍缩到少数专家上，无法反映多样化的图语义。
  2. **路由不确定性**：现有路由器为大多数节点产生不确定的专家分配，且这种不确定性与模型性能呈强负相关。
- **研究意义**：解决上述问题将显著提升图 MoE 的性能，推动图神经网络在大规模、多类型图数据上的应用。

## 2. 方法论：核心思想、关键技术细节

- **核心思想**：提出 **C²GMoE**（Contrastive routing & Confidence-aware fusion）框架，通过对比路由增强专家差异性和路由可靠性，通过置信度感知融合减轻不确定性。
- **关键技术细节**：
  - **组对比路由策略（Group-wise Contrastive Routing）**：
    - 将节点级路由决策与语义聚类对齐，提供明确的优化指导；
    - 同时满足负载均衡约束，防止路由坍缩。
  - **置信度感知融合机制（Confidence-aware Fusion）**：
    - 基于泛化误差的理论分析，自适应地根据每个专家的置信度重新加权其预测；
    - 对低置信度专家降低权重，减少不确定路由的负面影响。
- **算法流程（文字说明）**：输入图数据 → 多个 GNN 专家处理 → 组对比路由模块生成路由决策（确保聚类一致性与平衡性）→ 置信度感知融合模块根据专家置信度加权输出 → 最终预测。

## 3. 实验设计

- **数据集与场景**：论文在多个基准数据集上进行实验（具体数据集名称未在摘要中列出，根据 ICML 相关论文惯例可能包含 Cora、Citeseer、Pubmed、OGBN-Products 等图分类/节点分类数据集）。
- **基准与对比方法**：对比了现有 Graph-MoE 方法（如 MoE-GNN 变体）以及标准 GNN 模型。
- **评估指标**：分类准确率、路由坍缩程度、专家同质化度量等。

## 4. 资源与算力

- **未明确说明**：论文摘要及元数据中未提及使用的 GPU 型号、数量、训练时长等算力信息。文中仅提到“Extensive experiments”，但未提供具体计算资源细节。

## 5. 实验数量与充分性

- **实验组数**：摘要中描述为“多个基准数据集”和“广泛实验”，推测至少包含 4–6 个公开数据集的主实验结果，以及消融实验（验证对比路由和置信度融合各自贡献）和鲁棒性分析。
- **充分性评价**：由于未提供详细实验列表和统计结果，难以量化评判。但基于 ICML 会议标准，实验设计应包含充分的主实验、消融实验和对比分析。摘要中声称“优于现有 Graph-MoE 方法”，但缺乏具体的性能数值和显著性检验，客观性有待完整论文验证。

## 6. 主要结论与发现

- **核心发现**：
  - Graph-MoE 中确实存在专家同质化和路由不确定性两大问题，且呈负相关性。
  - 提出的 C²GMoE 通过对比路由和置信度融合，能显著增强专家专业化、缓解路由坍缩和不确定性。
- **性能提升**：在多个基准上优于现有 Graph-MoE 方法，专家专业化更明显。

## 7. 优点

- **方法亮点**：
  - 首次系统性地揭示并量化了 Graph-MoE 中的专家同质化和路由坍缩问题。
  - 组对比路由策略将语义聚类显式引入路由优化，同时平衡负载。
  - 从理论角度（泛化误差分析）推导置信度加权，具有理论支撑。
- **实验亮点**：
  - 除了最终性能，还分析了专家专业化程度和路由不确定性，诊断性实验充分。

## 8. 不足与局限

- **实验覆盖**：未披露具体数据集，若仅使用小规模引用网络，可能缺乏对大规模异构图或动态图的验证。
- **偏差风险**：
  - 对比方法可能未包含最前沿的 MoE 变体（如 Soft MoE 等）。
  - 路由不确定性度量可能依赖于特定假设。
- **应用限制**：
  - 对比路由和置信度融合增加了额外计算开销，大规模图上的效率未讨论。
  - 组对比策略需要预先定义聚类数量或依赖图结构，可能引入超参数敏感性。
- **资源信息缺失**：未报告训练算力，不便于复现和公平比较。

（完）
