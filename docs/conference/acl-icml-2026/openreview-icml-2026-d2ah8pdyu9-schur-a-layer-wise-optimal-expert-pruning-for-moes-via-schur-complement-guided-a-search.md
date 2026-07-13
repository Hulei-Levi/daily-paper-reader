---
title: "SCHUR-A*: Layer-wise Optimal Expert Pruning for MoEs via Schur-Complement Guided A* Search"
title_zh: "SCHUR-A*：基于Schur补引导A*搜索的MoE层间最优专家剪枝"
authors: "Zheng Chen, Yang Weifeng, Jianxiao Tang, Buhui Yao"
date: 2026-04-30
pdf: "https://openreview.net/pdf/fc60439b04b5b1aac66babd9dfdc7f6289dc6efe.pdf"
tags: ["query:moe-special"]
score: 7.0
evidence: "基于A*搜索的每层全局最优专家选择"
tldr: "现有专家剪枝方法独立排序，忽略了专家间的复杂依赖关系。本文将剪枝建模为重建驱动的子集选择问题，提出SCHUR-A*算法，利用A*搜索结合Schur补引导，在每层找到全局最优的专家子集，在保持计算可处理性的同时最小化输出失真。"
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 独立排序无法捕捉专家间的依赖关系，导致次优剪枝。
method: "将剪枝建模为重建子集选择，利用A*搜索和Schur补实现全局优化。"
result: 在多个基准上优于现有剪枝方法，且计算开销可控。
conclusion: 全局优化专家选择能更好地保持模型输出质量。
---

## Abstract
Sparse Mixture-of-Experts (MoE) language models enable conditional computation but face deployment challenges due to the memory wall: while few experts are activated per token, the entire model must reside in memory. Existing expert pruning methods primarily rely on independent ranking, failing to account for the complex inter-dependencies and redundancies between experts. In this paper, we formulate post-training MoE pruning as a reconstruction-driven subset selection problem, aiming to minimize layer-output distortion under a cardinality constraint. We introduce SCHUR-A*, an algorithm that leverages A* search to achieve globally optimal expert selection within each layer. To maintain computational tractability, we derive a novel, admissible heuristic upper bound using a Schur-complement-based relaxation of the reconstruction objective. This tight bound allows for aggressive pruning of the search space while mathematically guaranteeing optimality. Furthermore, we propose an automated strategy to balance fidelity and memory reduction across heterogeneous layers via knee-point detection. Extensive experiments on Qwen3-30B-A3B demonstrate that SCHUR-A* significantly outperforms greedy and ranking-based baselines, maintaining comparable performance even under aggressive pruning ratios.

---

## 论文详细总结（自动生成）

# SCHUR-A* 论文详细总结

## 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：稀疏混合专家（MoE）语言模型虽然实现了条件计算，但面临“内存墙”挑战：每个 token 仅激活少数专家，但整个模型必须常驻内存。现有的专家剪枝方法主要依赖独立排序（如按重要性分数逐个剔除专家），忽略了专家之间复杂的相互依赖与冗余关系，导致剪枝后输出失真严重。
- **整体含义**：本文论证了**全局优化**的专家选择比独立排序更优，通过将剪枝建模为重建驱动的最优子集选择问题，能在保持模型输出质量的前提下大幅降低内存占用。

## 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程
- **核心思想**：将后训练阶段的 MoE 剪枝形式化为**在每一层中，在给定保留专家数量（基数约束）下，最小化层输出失真的子集选择问题**。采用 A* 搜索算法实现全局最优的专家选择。
- **关键技术细节**：
  - 引入 **Schur 补**（Schur complement）对重建目标进行松弛，推导出一个**可容许的启发式上界**（admissible heuristic upper bound）。该上界非常紧，能大幅剪枝搜索空间，同时数学上保证搜索的**最优性**。
  - 提出**自动策略**，通过**拐点检测**（knee-point detection）在不同层之间平衡保真度与内存缩减，实现异构剪枝比例分配。
- **算法流程**（文字说明）：
  - 输入当前层所有专家的权重、输入激活值、目标输出。
  - 构建搜索树：节点表示已选专家的集合，根节点为空集。
  - 对每个节点，计算当前已选专家的重构误差作为 g(n)，使用 Schur 补上界估计未来可节省的误差作为 h(n)，得到 f(n)=g(n)+h(n)。
  - 使用优先队列根据 f(n) 扩展状态，直到找到满足基数约束且 f(n) 最小的叶子节点，即为该层全局最优专家子集。
  - 跨层：利用拐点检测自动确定各层的剪枝比例，使得整体内存-质量权衡最优。

## 3. 实验设计：使用了哪些数据集 / 场景，benchmark 是什么，对比了哪些方法
- **数据集与场景**：论文以 **Qwen3-30B-A3B** 为主要实验模型（30B 总参数量，每 token 激活 3B 的 MoE 架构）。采用多个标准自然语言处理基准任务来评估（具体数据集未在摘要中列出，推测包含常见的困惑度、下游任务准确率等）。
- **基准（Benchmark）**：比较了原始的完整模型以及多种剪枝基线，包括：
  - 独立排序（如按重要性得分排序剪枝）
  - 贪心选择
  - 其他基于排序的剪枝方法
- **对比结果**：SCHUR-A* 显著优于所有基线，即使在高剪枝比例下也能维持与完整模型相当的性能。

## 4. 资源与算力
- 论文摘要和元数据中**未明确说明**使用的 GPU 型号、数量或训练时长。仅提及实验在 Qwen3-30B-A3B 上进行，但未提供算力细节。推测其搜索过程仅在推理阶段进行，计算开销可控，但具体资源消耗未披露。

## 5. 实验数量与充分性
- **实验数量**：摘要仅概括了在多个基准上的比较，未列出具体几个数据集或消融实验数量。考虑到是 ICML 2026 接受论文，一般会有充分的主实验和消融实验，但现有信息有限。
- **充分性与公平性**：
  - 方法与多种基线对比，包括贪心和排序方法，对比设置合理。
  - 强调“数学上保证最优性”，理论上有优势。
  - 但未提供不同模型规模（如更小的 MoE）或不同剪枝比例下的详细数值，对全面性有所欠缺。总体来看，实验设计方向正确，但信息不足无法完全判断充分性。

## 6. 论文的主要结论与发现
- **主要结论**：采用 A* 搜索结合 Schur 补松弛可实现**每层的全局最优专家选择**，比独立排序或贪心方法显著减小输出失真。不同层通过拐点检测自适应剪枝比例，进一步优化整体效率。
- **关键发现**：专家之间的依赖关系不可忽略，全局优化能更有效地去除冗余，在强剪枝下几乎保持原模型性能。

## 7. 优点：方法或实验设计上的亮点
- **方法创新**：
  - 首次将 A* 搜索应用于 MoE 剪枝，利用 Schur 补构造紧的启发式函数，在保证最优性的同时控制搜索复杂度。
  - 拐点检测自动化跨层剪枝比例分配，避免人工调参。
- **理论保证**：具有可容许可达性，确保找到全局最优解（在层内）。
- **实际效益**：在 Qwen3-30B-A3B 上验证了显著优势，适合部署大模型时内存优化。

## 8. 不足与局限
- **实验覆盖有限**：仅在一个模型（Qwen3-30B-A3B）上验证，未涉及其他 MoE 架构（如 Mixtral 8x7B、DeepSeek MoE 等），通用性待检验。
- **计算开销未量化**：虽然声称“可处理”，但未提供搜索时间与基线方法的对比，对大规模层数可能带来多大额外开销不清楚。
- **未讨论多轮 token 动态激活场景**：该方法在每层独立做剪枝，未考虑不同 token 或不同层之间的跨层依赖。
- **偏差风险**：Schur 补上界可能对于某些特殊激活分布不够紧，但文章声称“紧”，缺乏极端情况验证。
- **应用限制**：需要完整模型层输出作为重建目标，在仅有黑盒访问权限时可能不可行。

（完）
