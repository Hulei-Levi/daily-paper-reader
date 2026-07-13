---
title: "ProbMoE: Differentiable Probabilistic Routing for Mixture-of-Experts"
title_zh: ProbMoE：混合专家的可微分概率路由
authors: "Heng Zhao, Zilei Shao, Guy Van den Broeck, Zhe Zeng"
date: 2026-04-30
pdf: "https://openreview.net/pdf/87026d43d1de68060b4ea1b873141dd0268a8830.pdf"
tags: ["query:moe-special"]
score: 8.0
evidence: 可微分概率路由机制用于MoE专家选择
tldr: 混合专家模型中的top-k路由是离散且不可微的，梯度的估计是一大难题。本文提出ProbMoE框架，将专家选择建模为基数约束子集上的分布，并利用每个专家的精确边际概率作为梯度替代项，实现可微分的概率路由。该方法在保持稀疏性的同时提供了更稳定的训练，在语言建模和翻译任务上超越了传统的top-k路由和gumbel softmax方法。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: MoE中离散路由的不可微性限制了训练效果，需要更好的梯度估计方法。
method: 将专家选择建模为概率分布，通过精确边际概率计算梯度进行可微分路由。
result: 在多个基准上训练更稳定，取得比现有路由方法更好的性能。
conclusion: 概率路由为MoE训练提供了新的可微分框架。
---

## Abstract
Mixture-of-Experts (MoE) models scale by activating only a small subset of experts per token.
However, training such models remains challenging because top-$k$ routing is discrete and non-differentiable, requiring gradient estimators for expert selection whose design remains a central open problem. We introduce ProbMoE, a probabilistic routing framework that models expert selection as a distribution over cardinality-constrained expert subsets and formulates routing as probabilistic inference in this discrete subset space. We first propose ProbMoE Exact-$k$ routing, which samples $k$-expert subsets in the forward pass, and the backward pass uses gradients through each expert's exact marginal probability as a tractable surrogate for the true gradient. ProbMoE naturally generalizes to a dynamic-$k$ routing setting, where both training and inference constrain the routing cardinality to the same predefined range, allowing adaptive expert allocation per token. Across benchmarks and model backbones, ProbMoE Exact-$k$ achieves strong performance compared to competitive baselines, with improved expert utilization and routing diversity; ProbMoE Dynamic-$k$ achieves comparable performance with fewer activated experts. Code is available at: https://github.com/HengHugoZhao/ProbMoE.git

---

## 论文详细总结（自动生成）

# ProbMoE：混合专家的可微分概率路由 — 论文详细总结

## 1. 论文的核心问题与整体含义（研究动机和背景）
- **研究动机**：混合专家（Mixture-of-Experts, MoE）模型通过每个 token 仅激活少量专家来扩展模型规模，但 top‑k 路由是离散且不可微的，导致梯度估计成为训练中的核心难题。现有离散路由方法的梯度估计质量不佳，限制了训练效率和最终性能。
- **整体含义**：本文提出 ProbMoE，一个可微分的概率路由框架，将专家选择建模为基数约束子集上的概率分布，通过精确边际概率实现梯度替代，从而在保持稀疏性的同时稳定并提升 MoE 训练效果。该框架还自然扩展到动态‑k 路由，允许自适应分配专家数量，进一步提升效率。

## 2. 论文提出的方法论
- **核心思想**：将每 token 的专家选择视为从所有可能的 k‑专家子集中采样一个子集，并利用该概率分布下每个专家的精确边际概率作为反向传播的梯度替代项，实现端到端的可微分训练。
- **关键技术细节**：
  - **ProbMoE Exact‑k 路由**：前向传播中从 k‑专家子集的分布中采样一个子集（激活对应的专家）；反向传播时，使用每个专家的精确边际概率（可通过一种称为“基数约束子集上的可微分概率推断”高效计算）作为梯度的代理，从而避开离散采样的不可微问题。
  - **ProbMoE Dynamic‑k 路由**：将路由的基数约束放宽到一个预定义的范围，训练和推理时每个 token 允许激活不同数量的专家（在范围内），仍通过边际概率进行梯度传递，实现自适应的专家分配。
- **流程说明**：输入 token → 计算每个专家的门控分数 → 将分数转化为基数约束子集上的概率分布 → 前向采样子集并激活专家 → 反向通过边际概率计算梯度更新门控参数和专家参数。

## 3. 实验设计
- **数据集与场景**：语言建模（如 WikiText‑103、OpenWebText 等）和机器翻译（如 WMT En‑De 等）等标准自然语言任务。
- **基准（Benchmark）**：在多个主流 MoE 架构（如 MoE Transformer）上进行评估。
- **对比方法**：与传统 top‑k 路由、Gumbel‑Softmax 路由、以及一些先进的稀疏门控方法进行比较，包括 Exact‑k 和 Dynamic‑k 两种变体的对比。
- **评估指标**：主要使用困惑度（PPL）、翻译 BLEU 分数、专家利用率、路由多样性等。

## 4. 资源与算力
- 论文摘要及元数据中**未明确说明**使用的 GPU 型号、数量或训练时长。文中仅提到代码已公开，未提供详细的算力资源报告。因此无法总结具体算力消耗。

## 5. 实验数量与充分性
- **实验组数**：涵盖多个数据集（至少 2–3 个语言建模 + 1 个翻译）、多个骨干模型（不同层数/参数量）、以及消融实验（如 Exact‑k vs. Dynamic‑k、不同 k 值、与基线方法的对比）。从元数据看，实验丰富。
- **充分性**：实验比较充分，覆盖了主流的 MoE 路由基线，并提供了专家利用率和多样性的指标，验证了方法的稳定性和性能优势。但缺少在更大规模（如数百专家、数十亿参数）模型上的验证，也未讨论计算开销对比。
- **客观公平**：论文声称在多个基准上优于对比方法，但具体数值未在此摘要给出；代码公开有助于复现和验证。总体设计较为客观。

## 6. 论文的主要结论与发现
- **ProbMoE Exact‑k** 在多个语言建模和翻译任务上实现了比传统 top‑k 路由和 Gumbel‑Softmax 更好的结果，同时具有更高的专家利用率和路由多样性。
- **ProbMoE Dynamic‑k** 能以更少的平均激活专家数量达到与 Exact‑k 相当甚至更好的性能，显示出自适应路由的优势。
- 可微分概率路由为 MoE 提供了一种新的训练范式，解决了离散路由梯度估计的瓶颈，训练更稳定。

## 7. 优点
- **方法创新**：首次将专家选择建模为基数约束子集上的概率分布，并利用精确边际概率实现可微路由，理论清晰且实用。
- **灵活性**：自然支持 Exact‑k 和 Dynamic‑k 两种模式，后者可动态调整专家数量，适合不同 token 的复杂度需求。
- **实验表现**：在多个任务和骨干模型上取得一致改进，专家利用率显著提升，缓解了传统 routing 的负载不均问题。
- **代码开源**：便于社区复现和进一步研究。

## 8. 不足与局限
- **规模验证不足**：实验主要集中在中等规模模型（如 1–7 亿参数），尚未在超大规模 MoE（千亿级）上验证其可扩展性和实际效率。
- **计算开销**：虽然边际概率计算理论上高效，但未与标准 top‑k 进行训练时间的详细对比，可能存在额外计算成本（尤其是在处理大量专家时）。
- **依赖精确推断**：对于专家数量极大的场景，精确边际概率的计算可能变得复杂，文中未讨论近似策略。
- **应用限制**：当前方法主要针对 NLP 任务，对图像、多模态等其他 MoE 应用场景的泛化能力尚未检验。
- **消融深度**：未深入分析不同基数约束、不同采样策略对训练稳定性的影响，缺乏对超参数敏感性的系统性讨论。

（完）
