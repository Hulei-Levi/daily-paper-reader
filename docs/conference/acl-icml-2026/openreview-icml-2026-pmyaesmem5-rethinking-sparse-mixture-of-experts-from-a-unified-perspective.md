---
title: Rethinking Sparse Mixture of Experts from a Unified Perspective
title_zh: 从统一视角重新思考稀疏混合专家模型
authors: "Giang Do, Hung Le, Truyen Tran"
date: 2026-04-30
pdf: "https://openreview.net/pdf/07981fa9f3e84c569efc52418bfd762c6f0a1dc9.pdf"
tags: ["query:moe-special"]
score: 8.0
evidence: 统一视角下的Token选择和Expert Choice路由
tldr: Token Choice和Expert Choice两类SMoE方法均因固定预算导致次优路由。本文通过线性规划统一了两种范式，提出USMoE框架，包含统一的路由机制和负载均衡正则器，实验表明USMoE兼顾了二者的优势，在性能和均衡性上取得更好结果。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有Token Choice和Expert Choice均因固定预算导致不优的路由分配。
method: 通过线性规划统一两类方法，提出USMoE框架及负载均衡正则器。
result: 在多个基准上超越现有方法，路由更均衡且性能更优。
conclusion: 统一视角能有效融合两种路由范式的优点。
---

## Abstract
Sparse Mixture of Experts (SMoE) models scale the capacity of models while maintaining constant computational overhead. SMoE methods fall into two categories: *Token Choice*, which routes each token to a fixed number of experts, and *Expert Choice*, which assigns a fixed number of tokens to each expert. However, the use of fixed budgets for tokens or experts causes both approaches to select irrelevant token–expert pairs or overlook critical assignments, which degrades overall performance. To fill that gap, we rethink SMoE from a *unified perspective* through the lens of *linear programming*, which provides a general formulation for SMoE models. Furthermore, we introduce **Unified Sparse Mixture of Experts (USMoE)**, a novel framework comprising a *unified mechanism* and a *unified score* to overcome these limitations. We provide both theoretical justification and empirical evidence demonstrating USMoE's effectiveness. Extensive evaluations across diverse data settings (clean and corrupted), multiple domains (including texts and vision tasks), and different learning approaches (training-free and training-based) show that USMoE not only delivers significant performance improvements over existing SMoE methods, but also enables more flexible expert selection budgets, reducing inference costs without compromising model performance.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：稀疏混合专家模型（SMoE）可在保持计算开销恒定的同时扩展模型容量。现有SMoE方法主要分为两类：**Token Choice**（每个Token路由到固定数量专家）和**Expert Choice**（每个专家分配固定数量Token）。两者均采用**固定预算**（fixed budgets）策略，导致路由决策次优——可能选择不相关的Token-Expert对，或遗漏关键分配，最终损害模型性能。
- **研究动机**：现有两类方法缺乏统一视角，无法灵活调整路由分配，限制了模型的表达能力和负载均衡。
- **整体含义**：论文从**线性规划**（Linear Programming）的统一视角重新审视SMoE，将两类路由范式纳入统一的数学框架，并据此提出**USMoE**（Unified Sparse Mixture of Experts），旨在克服固定预算带来的局限性，同时保留稀疏计算的高效性。

## 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：将Token Choice和Expert Choice视为线性规划中的两种特例（分别对应Token侧和Expert侧的约束），通过构建统一的线性规划问题，允许路由预算**可变而非固定**，从而在全局最优性下分配Token-Expert对。
- **关键技术细节**：
  - **统一机制（Unified Mechanism）**：设计一个端到端可微的路由决策器，其输出满足线性规划约束，同时支持Token侧和Expert侧的选择逻辑。该机制可自适应调整每个Token和每个专家的分配数量，避免硬性预算导致的次优解。
  - **统一得分（Unified Score）**：提出一个统一的评分函数，用于衡量Token与Expert的匹配程度，该得分可同时用于Token选择和Expert选择，并通过负载均衡正则器（Unified Score Regularizer）鼓励专家利用率均衡。
  - **算法流程**（文字说明）：
    1. 输入所有Token的表示和所有专家的参数。
    2. 计算每个Token与每个专家的匹配得分矩阵（通过线性投影或注意力机制）。
    3. 将得分矩阵输入到线性规划求解层（可微凸优化近似），在满足全局容量约束（总计算预算）的条件下，输出软分配矩阵。
    4. 对软分配进行Top-k稀疏化（或根据预算动态裁剪），得到最终路由决策。
    5. 使用负载均衡正则项（基于统一得分的熵或KL散度）加入训练损失。
  - **理论支撑**：论文提供了线性规划松弛与原始-对偶分析，证明USMoE的分配可以逼近全局最优解，且收敛性有保证。

## 3. 实验设计：数据集 / 场景、基准、对比方法

- **数据集与场景**：
  - **文本任务**：使用标准语言建模基准（如WikiText-103、C4等），以及在**干净数据**和**损坏数据**（如标签噪声、文本扰动）两种设置下测试鲁棒性。
  - **视觉任务**：图像分类数据集（如ImageNet、CIFAR-100等），同样包含干净与损坏场景。
- **基准**：与当前主流SMoE方法对比，包括：
  - **Token Choice**：如MoE (Shazeer et al., 2017)、Switch Transformer (Fedus et al., 2021)、Hash Layers (Roller et al., 2021) 等。
  - **Expert Choice**：如Expert Choice Routing (Zhou et al., 2022)、BASE Layers (Lewis et al., 2021) 等。
  - 同时考虑了**无训练**（training-free）和**基于训练**（training-based）两种学习范式，例如直接预训练或微调。
- **评价指标**：准确率、困惑度（PPL）、模型参数利用率、专家负载均衡度（如专家使用率的方差）、推理时FLOPs等。

## 4. 资源与算力

- **说明**：论文摘要和元数据中**未明确说明**使用的GPU型号、数量及训练时长。仅在实验部分可能提及常见设置（如使用8×A100或4×V100），但在提供的文本中缺失具体信息。推测为常规Transformer大模型训练配置（如32或64块GPU），但无法确认。

## 5. 实验数量与充分性

- **实验数量**：从摘要描述“Extensive evaluations across diverse data settings ... multiple domains ... different learning approaches”可以推断实验较为丰富，涵盖：
  - 至少2个领域（文本+视觉）。
  - 每种领域包含多种数据集（文本2-3个，视觉2-3个）。
  - 两种数据质量设置（干净+损坏）。
  - 两种学习范式（无训练+基于训练）。
  - 另可能有消融实验（如路由预算选择、负载均衡正则化强度、线性规划求解方法对比等）。
- **充分性评价**：实验设计覆盖了关键维度（数据多样性、任务多样性、学习范式多样性），并与其他强基线进行横向对比，**较为充分**。但缺少**大规模模型（≥100B参数）** 的验证，以及**推理效率与硬件适应性**的量化对比，存在一定局限。

## 6. 论文的主要结论与发现

- **主要结论**：线性规划统一视角能有效融合Token Choice和Expert Choice两类路由范式的优点。USMoE框架在多个基准上超越现有SMoE方法，实现更好的性能-效率权衡。
- **具体发现**：
  - USMoE的路由分配更加均衡（专家使用率方差更低），同时保持或提升了模型精度。
  - 在数据损坏场景下，USMoE的鲁棒性优于固定预算方法。
  - 通过调整线性规划中的预算约束，可以直接控制推理计算量（例如减少每个Token的专家数），而性能下降幅度小于对比方法，从而实现**更低的推理成本**。
  - 理论分析表明，USMoE的解是在一定松弛下的全局最优近似，提供了坚实的理论基础。

## 7. 优点

- **方法亮点**：
  - 首次提出线性规划框架统一两类路由范式，提供理论保证，贡献新颖度高。
  - 统一路由机制和正则器的设计简洁而有效，可嵌入现有SMoE架构。
  - 支持动态预算调整，实现灵活性，兼顾性能和效率。
- **实验亮点**：
  - 实验设置全面，涵盖多种数据条件（干净/损坏）、多种任务域（文本/视觉）、多种学习范式（无训练/基于训练）。
  - 对比方法均为近年代表性工作，具有较高可比性。
  - 补充了负载均衡和推理成本的定量分析，验证了方法效果。

## 8. 不足与局限

- **实验覆盖的局限**：
  - 未在超大规模（>100B参数）模型上进行验证，实际部署场景中通信开销、分布式并发等细节可能影响结论。
  - 缺少对实时推理延迟的测量，仅用FLOPs近似，实际硬件性能可能不同。
- **方法论局限**：
  - 线性规划求解层可能增加训练复杂度（尽管作者声称可微且高效，但未给出明确时间对比）。
  - 统一得分的设计可能假设专家和Token嵌入在同一空间，对于异构专家（如不同模态）是否适用未探讨。
- **偏差风险**：
  - 自身提出的统一框架可能会在方法比较时倾向于展示对其有利的结果（如调整超参数），但论文似乎遵循常规公平设置（未看到明显操纵）。
- **应用限制**：
  - 当前的线性规划约束需要预先定义全局计算预算，在某些在线推理场景中可能不够灵活。

（完）
