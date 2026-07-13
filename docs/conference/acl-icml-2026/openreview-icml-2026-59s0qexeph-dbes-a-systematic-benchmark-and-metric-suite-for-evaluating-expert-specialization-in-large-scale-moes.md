---
title: "DBES: A Systematic Benchmark and Metric Suite for Evaluating Expert Specialization in Large-Scale MoEs"
title_zh: DBES：大规模MoE中专家专业化评估的系统基准与指标套件
authors: "Jing Wang, Jazze Young, Hongxuan Lu, Zhimin Xin, Shu Wang"
date: 2026-01-23
pdf: "https://openreview.net/pdf/475bdb6dc94c35ae01af8c13b63782164759418d.pdf"
tags: ["query:moe-special"]
score: 9.0
evidence: 评估专家专业化的基准和指标
tldr: 当前MoE模型缺乏对专家专业化程度的有效评估，传统路由统计指标无法确认专家是否真正发展了上下文感知的专业能力。本文构建了多领域基准DBES，并提出了包括路由专业化在内的新指标体系，为大规模MoE的专家专业化评估提供了系统框架。
source: ICML-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有MoE评估无法确认专家是否真正专业化，存在架构意图与实证验证的脱节。
method: 构建多领域基准DBES，设计路由专业化等新指标来量化专家专业化程度。
result: 在多个领域验证了指标有效性，能区分真正专业化与冗余专家。
conclusion: DBES框架为MoE专家专业化评估提供了可靠工具，促进理解专家行为。
---

## Abstract
Mixture-of-Experts (MoE) architectures scale LLM capacity efficiently, however, a fundamental disconnect remains between their architectural intent and the empirical verification of expert specialization. Conventional evaluations primarily utilize aggregate routing statistics, which often obfuscate whether experts develop genuine, context-aware proficiency or merely act as redundant computational units. To bridge this gap, we introduce a rigorous, multi-faceted framework for assessing MoE specialty. We first construct Domain Bench for Experts Specialty(DBES), a multi-domain benchmark derived from open-source and real-world application data. We then propose a suite of novel metrics—including Routing Specialization, Normalized Effective Rank, Domain Isolation, Rademacher Complexity, and N-gram Routing Ratio and Group N-gram Ratio—to analyze expert behavior at both token and sequence levels. These metrics move beyond load distribution to quantify the structural and functional specialization of experts. We apply this framework to conduct a comprehensive analysis of prominent MoE models, including Qwen3-MoE, GLM-4.6, and DeepSeek-R1. Our experiments reveal distinct specialization strategies: Qwen-series models exhibit high specialization and domain isolation, while DeepSeek and GLM employ more generalized, collaborative expert usage. However, all models show limited n-gram expertise($n=10$), falling between $0.12\\%$ and $1.67\\%$. Furthermore, we establish a positive correlation between architectural specialization and performance on complex, domain-specific downstream tasks. This work provides the first systematic methodology for evaluating and interpreting expert specialty, offering crucial insights for the design, model selection, and efficient post-training of next-generation MoE systems.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：当前大规模混合专家（Mixture-of-Experts，MoE）模型虽然旨在通过路由机制让不同专家学习不同领域的专业知识，但现有评估方法仅依赖聚合路由统计（如负载均衡），无法确认专家是否真正形成了上下文感知的专业化技能。这导致架构设计意图与实证验证之间存在根本性脱节。
- **研究动机**：弥补这一评估空白，提出系统性方法来量化专家专业化程度，从而理解MoE内部工作机制、指导模型选择和后训练优化。
- **整体含义**：首次为MoE专家专业化提供系统性的基准和指标套件，有助于推动下一代MoE系统的可解释性和设计改进。

## 2. 论文提出的方法论

- **核心思想**：构建多领域基准数据集，并设计一套超越传统路由统计的指标，从token和序列两个层面量化专家的结构性和功能性专业化。
- **关键技术细节**：
  - **基准构建**：Domain Bench for Experts Specialty（DBES）——从开源和真实应用数据中提取的多领域基准，覆盖不同专业领域。
  - **新指标体系**：
    - **路由专业化（Routing Specialization）**：度量专家在特定领域被激活的集中程度。
    - **归一化有效秩（Normalized Effective Rank）**：评估专家参数矩阵的多样性，反映专业化深度。
    - **领域隔离（Domain Isolation）**：衡量不同专家处理不同领域数据的分离程度。
    - **Rademacher复杂度（Rademacher Complexity）**：量化专家函数族的表达能力，揭示其处理特定任务的能力。
    - **N-gram路由比率（N-gram Routing Ratio）**和**组N-gram比率（Group N-gram Ratio）**：在序列级别分析专家对连续n-gram的偏好。
  - **算法流程**：基于DBES基准，对每个MoE模型的前向传播进行监控，收集每层每个token的路由选择，然后计算上述指标，最后与下游任务性能进行相关性分析。

## 3. 实验设计

- **数据集/场景**：使用自构建的DBES基准数据集（来自开源和真实应用数据，覆盖多个领域）。
- **基准（Benchmark）**：DBES本身作为标准化评估基准。
- **对比方法**：传统路由统计（如负载均衡、路由熵等）作为基线。
- **评估模型**：三个主流大规模MoE模型——Qwen3-MoE、GLM-4.6、DeepSeek-R1。

## 4. 资源与算力

- 论文摘要及元数据中**未明确说明**使用的GPU型号、数量、训练时长等算力信息。仅提及对现有预训练模型进行推理分析，未涉及从头训练过程，因此算力需求可能集中在模型推理和指标计算上。如有需求，需要查阅论文全文获取具体细节。

## 5. 实验数量与充分性

- **实验数量**：根据摘要，对三个MoE模型进行了全面分析，计算了路由专业化、归一化有效秩、领域隔离、Rademacher复杂度、n-gram比率等共至少7个指标，并在多领域场景下评估了专业化与下游任务性能的相关性。实验组数较多（每个模型×每个指标×每个领域），但具体数值未列出。
- **充分性评估**：实验覆盖了不同厂商、不同架构风格的模型（Qwen、GLM、DeepSeek），验证了指标区分能力，并建立了正相关性。但缺乏对更多模型（如小规模MoE、不同专家数量/层数的模型）的对比，也缺少消融实验（如移除某个指标的影响）。总体而言，**实验设计较充分且公平**，但可能因篇幅限制未展示所有细节。

## 6. 论文的主要结论与发现

- Qwen系列模型表现出**高专业化和强领域隔离**，即不同专家倾向于集中处理特定领域数据。
- DeepSeek和GLM-4.6采用**更通用、协作式**的专家使用策略，专家之间重叠较多。
- 所有模型在n-gram（n=10）级别的专家专业度均**非常有限**，范围仅为0.12%到1.67%，说明专家对长连续序列的专业化不足。
- 架构专业化程度与**复杂领域下游任务性能呈正相关**，即专家越专业化，模型在相关任务上表现越好。

## 7. 优点

- **首创性**：首次为MoE专家专业化评估构建系统框架（基准+指标），填补领域空白。
- **指标全面**：从token级（路由专业化、有效秩）到序列级（n-gram比率），从结构（域隔离）到功能（Rademacher复杂度），多角度刻画专业化。
- **实用性强**：提出的指标易于计算，可直接应用于现有MoE模型分析，对模型选型、后训练策略优化有明确指导意义。
- **实验对比清晰**：不同模型之间的专业化模式差异被显著揭示，验证了指标的区分能力和解释性。

## 8. 不足与局限

- **实验覆盖有限**：仅评估了三个MoE模型，缺乏对更多不同规模、不同训练方式（如正则化技术、辅助损失）的模型进行对比，泛化性有待验证。
- **未涉及训练过程**：论文仅分析已训练好的模型，未探讨训练过程中专业化的演化规律，对理解专家形成的动态过程帮助有限。
- **n-gram度量局限**：n=10的粒度可能过粗或过细，未能提供不同n值下的全面分析。
- **基准规模未知**：DBES基准的领域数量、样本大小未在摘要中说明，若规模较小可能影响结论稳健性。
- **算力资源缺乏说明**：未报告计算消耗，不利于可重复性评估。
- **潜在偏差风险**：下游任务性能与专业化的相关性可能受模型原有训练数据分布影响，因果关系需谨慎推断。

（完）
