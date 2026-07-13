---
title: Geometric and Stochastic Analysis of Discontinuities in Sparse Mixture-of-Experts
title_zh: 稀疏混合专家模型中不连续性的几何与随机分析
authors: "Tho Tran Huu, Huu-Tuan Nguyen, Thien-Hai Nguyen, Nhat-Tri Ho, Viet-Hoang Tran, Tho Quan, Tan Minh Nguyen"
date: 2026-04-30
pdf: "https://openreview.net/pdf/fd55d198353999c97343436adc4d1d6bac0a1c4c.pdf"
tags: ["query:moe-special"]
score: 8.0
evidence: 稀疏MoE不连续性的几何与随机分析
tldr: 稀疏MoE中Top-k专家选择导致输入空间的非连续响应，即使邻近输入也可能触发完全不同的专家集。本文对不连续面进行了严格的几何与随机分类，按切换事件中并列专家的数量区分阶数，并建立了渐近性质。该工作深化了对MoE路由机制的理论理解。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 稀疏MoE的Top-k选择导致模型映射不连续，影响稳定性和可解释性。
method: 通过测度论切片论证，分类不连续面阶数，并分析渐近行为。
result: 建立了不连续性的理论框架，揭示了路由切换的几何结构。
conclusion: 为理解MoE路由的动态行为提供了理论基础。
---

## Abstract
Sparse Mixture-of-Experts (SMoE) architectures are now widely deployed in state-of-the-art language and vision models, where conditional routing allows scaling to very large networks. However, this very Top-$k$ expert selection that enables conditional routing also renders the SMoE map inherently discontinuous. In the vicinity of these discontinuity surfaces, even inputs that are arbitrarily close may activate substantially different sets of experts resulting in significantly different outputs. In this work we give a rigorous geometric and stochastic analysis of these discontinuities. We first classify them by order, determined by the number of tied experts at a switching event. Using measure-theoretic slicing arguments, we establish asymptotic volume estimates for the thickened discontinuity surfaces, showing that lower-order discontinuity sets dominate, whereas higher-order ones occupy a vanishingly small relative volume. Next, modeling random perturbations in the input space via a diffusion process, we prove that the path eventually encounter a discontinuity, and moreover that the first hit almost surely occurs on an order-1 discontinuity with explicit finite-time probability bounds. We further derive occupation-time bounds that quantify the duration the random path spend in the neighborhoods of each discontinuity order. These theoretical results imply that inputs are more likely to lie near lower order discontinuities. Motivated by this insight, we propose a simple smoothing mechanism that can be directly applied to existing SMoEs, softly incorporating experts near discontinuities; our analysis guarantees that the added computational overhead remains small while providing localized smoothing near discontinuities, and experiments across language and vision tasks show that smoothing not only enforces continuity of the SMoE map but also enhances empirical performance.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **背景**：稀疏混合专家（Sparse Mixture-of-Experts，SMoE）架构已广泛应用于大型语言和视觉模型中，通过条件路由（Top‑k 专家选择）实现模型规模扩展。然而，这种离散的专家选择机制导致模型映射在输入空间中出现不连续面：即使两个输入无限接近，也可能触发完全不同的专家集，产生显著不同的输出，从而影响模型的稳定性和可解释性。
- **核心问题**：本文旨在严格分析 SMoE 中这些不连续面的几何结构与随机行为，揭示其阶数分类、体积渐近性质以及随机路径触发不连续面的概率特性，并为缓解不连续性提供理论指导。

### 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程（用文字说明即可）

- **核心思想**：对不连续面按切换事件中并列专家（tied experts）的数量进行阶数（order）分类，并利用测度论和随机分析刻画各阶不连续面的几何与随机性质。
- **关键技术细节**：
  - **不连续面分类**：将切换事件中恰好有 \(k\) 个专家得分相等（并列）的不连续面称为阶 \(k\) 不连续面。阶数越高，并列专家越多。
  - **几何分析**：采用测度论中的切片论证（slicing arguments），对加厚的不连续面（thickened discontinuity surfaces）进行渐近体积估计。结果表明：低阶不连续面占据主导体积，高阶不连续面相对体积趋于零。
  - **随机分析**：将输入空间中的随机扰动建模为扩散过程。证明该随机路径几乎必然会在有限时间内首次碰到某个不连续面，并且首次击中几乎必然发生在阶‑1 不连续面上。同时给出了有限时间内的概率上界。
  - **占用时间界**：推导了随机路径在各阶不连续面邻域内停留时间的界限，量化了输入更可能靠近低阶不连续面这一直觉。
  - **平滑机制**：基于上述发现，提出一种简单的平滑方法，在不改变原有 SMoE 路由结构的前提下，柔性地将邻近不连续面的专家软性融合，保证额外计算开销很小，同时局部平滑不连续性。

### 3. 实验设计：使用了哪些数据集 / 场景，它的 benchmark 是什么，对比了哪些方法

- **数据集与场景**：论文提及在语言和视觉任务上进行实验，但具体数据集名称（如 WMT、ImageNet 等）未在摘要或元数据中给出。
- **Benchmark**：未明确说明，但可以推断为常见的 LLM 基准（如语言建模困惑度）和图像分类准确率等。
- **对比方法**：仅提到“直接应用于现有 SMoE”的平滑机制，未列出具体对比基线（如原始 SMoE、gMLP 或其他平滑路由变体）。实验部分细节缺失。

### 4. 资源与算力：如果文中有提到，请总结使用了多少算力（GPU 型号、数量、训练时长等）。若未明确说明，也请指出这一点。

- **未明确说明**：摘要和元数据中未提及任何具体算力资源（GPU 型号、数量、训练时长等）。根据常见 ICML 论文惯例，可能实验部分会有描述，但此处未提供。

### 5. 实验数量与充分性：大概做了多少组实验（如不同数据集、消融实验等），这些实验是否充分、是否客观、公平。

- **实验数量**：元数据中只提及“语言和视觉任务”，未给出具体实验组数或消融实验细节。从摘要推测可能包括至少两组任务（语言 + 视觉），并可能包含对平滑机制的超参数或阈值的消融分析，但无法确认。
- **充分性与客观性**：由于缺少详细实验设计，难以评估实验的充分性。理论部分（几何与随机分析）较为严谨，但实验验证部分信息不足，可能存在覆盖不全面的风险。

### 6. 论文的主要结论与发现

- **几何结论**：SMoE 的不连续面可按阶数分类，低阶不连续面在体积上占主导，高阶不连续面相对体积趋近于零，说明实际输入更可能靠近低阶不连续面。
- **随机结论**：随机路径几乎必然首次击中某个不连续面，且首次击中几乎总是发生在阶‑1 不连续面上；占有时长同样表明低阶不连续面邻域内停留时间更长。
- **实践结论**：提出的轻量级平滑机制能有效局部平滑不连续性，且不增加显著计算开销，在语言和视觉任务上改善模型性能（从“enhances empirical performance”推断）。

### 7. 优点：方法或实验设计上有哪些亮点

- **理论深度**：首次对 SMoE 不连续性进行了严格的几何与随机分类，使用测度论和扩散过程等数学工具，提供了可验证的渐近性质。
- **可应用性**：基于理论洞察提出的平滑机制简单、即插即用，计算开销小，易于集成到现有 SMoE 模型中。
- **跨领域验证**：在语言和视觉两个领域均进行了实验，展示了方法的通用性。

### 8. 不足与局限：包括实验覆盖、偏差风险、应用限制等

- **实验细节缺失**：摘要中未提供具体数据集、基准测试、对比方法和实验配置，导致难以复现或评估实际增益的大小。
- **算力信息空白**：未说明训练资源，难以判断方法在实际大模型上的可扩展性。
- **理论假设局限**：随机分析假设输入扰动为扩散过程，实际中可能并非理想扩散，需验证其鲁棒性。
- **平滑机制适用范围**：仅针对不连续面进行局部平滑，可能无法处理全局路由的奇异行为；对极高阶不连续（如大量专家并列）效果可能有限（因其体积已可忽略）。
- **对照实验不足**：未与传统平滑方法（如 softmax 路由、噪声辅助路由）进行定量对比，可能削弱说服力。

（完）
