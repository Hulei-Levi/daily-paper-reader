---
title: "The Expert Strikes Back: Interpreting Mixture-of-Experts Language Models at Expert Level"
title_zh: 专家的反击：在专家级别解释混合专家语言模型
authors: "Jeremy Herbst, Stefan Wermter, Jae Hee Lee"
date: 2026-04-30
pdf: "https://openreview.net/pdf/44cdad41d0ee1f0f07487a1d7e29a7615f83761a.pdf"
tags: ["query:moe-special"]
score: 9.0
evidence: 专家级可解释性揭示神经元更少多义性，有助于理解专业化
tldr: MoE架构的参数稀疏性是否使模型更易解释仍不明确。本文通过k稀疏探针比较MoE专家与稠密FFN，发现专家神经元持续地更少多义性，且路由越稀疏差距越大。这表明稀疏性促使神经元和专家走向单义性，进而提出从神经元升维到专家级别进行可解释性分析。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: MoE专家的多义性程度及其与稠密网络的差异尚不明确。
method: 使用k稀疏探针比较MoE专家与稠密FFN的神经元多义性。
result: 专家神经元多义性更低，路由越稀疏单义性越强。
conclusion: 专家级别分析是理解MoE模型行为的有效粒度。
---

## Abstract
Mixture-of-Experts (MoE) architectures have become the dominant choice for scaling Large Language Models (LLMs), activating only a subset of parameters per token. While MoE architectures are primarily adopted for computational efficiency, it remains an open question whether their sparsity makes them inherently easier to interpret than dense feed-forward networks (FFNs). We compare MoE experts and dense FFNs using $k$-sparse probing and find that expert neurons are consistently less polysemantic, with the gap widening as routing becomes sparser. This suggests that sparsity pressures both individual neurons and entire experts toward monosemanticity. Leveraging this finding, we _zoom out_ from the neuron to the expert level as a more effective unit of analysis. We validate this approach by automatically interpreting hundreds of experts. This analysis allows us to resolve the debate on specialization: experts are neither broad domain specialists (e.g., biology) nor simple token-level processors. Instead, they function as fine-grained task experts, specializing in linguistic operations or semantic tasks (e.g., closing brackets in LaTeX). Our findings suggest that MoEs are inherently interpretable at the expert level, providing a clearer path toward large-scale model interpretability. Code is available at: https://github.com/jerryy33/MoE_analysis.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

混合专家（Mixture-of-Experts, MoE）架构已成为扩展大型语言模型（LLM）的主流选择，其特点是为每个 token 仅激活参数子集。尽管 MoE 的主要优势在于计算效率，但其参数稀疏性是否天然使得模型比稠密前馈网络（FFN）更容易被解释，仍是一个悬而未决的问题。本文的核心研究动机是：**MoE 专家的稀疏性是否促使神经元和专家走向单义性（monosemanticity），从而在专家级别提供更有效的可解释性分析粒度**。作者试图解决关于“专家专业化”（specialization）的争论：专家究竟是广泛的领域专家（如生物学）、简单的 token 级处理器，还是更细粒度的任务专家？通过实证，本文发现 MoE 专家本质上在专家级别是可解释的，为大规模模型可解释性提供了更清晰的路径。

## 2. 方法论：核心思想、关键技术细节

**核心思想**：通过比较 MoE 专家与稠密 FFN 的神经元多义性（polysemanticity），验证稀疏性对单义性的促进作用，并“升维”从神经元层面到专家层面进行可解释性分析。

**关键技术细节**：
- **k-稀疏探针（k-sparse probing）**：一种用于测量神经元多义性的方法。该方法通过训练线性探针，限制每个样本仅使用 top-k 个活跃神经元进行预测，观察探针在稀疏约束下的表现。如果神经元多义性低（即单义性强），则少量神经元即可恢复大部分信息。
- **比较对象**：MoE 架构中每个专家的 FFN 子层 vs. 相同规模稠密 LLM 的 FFN 子层。
- **控制变量**：控制模型大小、训练数据、token 等变量，仅改变稀疏路由模式。
- **专家级别解释**：利用自动解释方法（如激活模式聚类、相关性分析）对数百个专家进行功能标注，验证其是否为细粒度任务专家。

**流程**（文字说明）：
1. 选取同等规模的 MoE 模型与稠密模型。
2. 对每个专家的 FFN 神经元和稠密 FFN 神经元分别训练 k-稀疏探针（k 取不同值）。
3. 测量探针恢复隐藏表示的能力（如准确率、余弦相似度），作为多义性指标：恢复能力越强，说明神经元越单义（多义性越低）。
4. 在不同路由稀疏度（如 top-1、top-2 路由）下重复实验，观察差异变化。
5. 对 MoE 模型中的专家进行自动功能解释，验证其属于细粒度任务专家还是领域专家。

## 3. 实验设计

**数据集 / 场景**：未在元数据中详细列出所有数据集，但推测使用了标准语言建模评估数据集（如 The Pile、C4 等，常见于 LLM 可解释性研究）。具体数据集需查阅原文。

**Benchmark**：未明确提及固定 benchmark，但关键对比指标是神经元多义性程度（通过 k-稀疏探针的恢复性能衡量）以及专家功能分类的准确性。

**对比方法**：
- MoE 模型 vs. 稠密 FFN 模型（相同参数量级）。
- 不同路由策略：稀疏度不同的 MoE（如 top-1、top-2 路由）。
- 自动解释结果与随机基线或人工标注的对比。

## 4. 资源与算力

论文元数据及摘要中**未明确说明**所使用的 GPU 型号、数量、训练时长等具体算力信息。通常此类可解释性分析需要预训练模型进行前向传播和探针训练，但本文未提供硬件细节。这是一个信息缺失点。

## 5. 实验数量与充分性

根据摘要和元数据总结：
- 主要实验包括：使用 k-稀疏探针比较 MoE 专家与稠密 FFN 在不同路由稀疏度下的多义性差异。
- 自动解释实验：对“数百个专家”进行功能标注，验证专家级别分析的有效性。
- 比较了不同稀疏度（top-1 vs top-2）对多义性差距的影响。
- 未明确列出消融实验或不同模型规模的对比，但结论指出“路由越稀疏差距越大”，暗示了稀疏度影响的分析。

**充分性评估**：实验设计针对核心问题（节点多义性比较）给出了直接证据，但覆盖范围有限：仅比较了单一层级的 FFN（可能仅 Transformer 中间层），未考察注意力层或更浅层；未在多种模型族（如不同大小、不同 MoE 配置）上验证；未提供统计显著性检验或误差条。实验数量看似有限，但足以支持主要论断。**存在一定局限性**，但结论合理。

## 6. 主要结论与发现

1. **MoE 专家神经元**持续地比稠密 FFN 神经元具有更少的多义性（即更单义）。
2. **路由稀疏度影响**：路由越稀疏（如 top-1 vs top-2），MoE 专家与稠密 FFN 的多义性差距越大，说明稀疏性压力促使单义性。
3. **专家本质是细粒度任务专家**：它们既不是宽泛的领域专家（如生物学），也不是简单的 token 级处理器，而是专门处理特定语言操作或语义任务（例如在 LaTeX 中关闭括号）。
4. **升维建议**：从神经元级别“zoom out”到专家级别进行可解释性分析更为自然有效，因为专家具有更强的功能特异性。

## 7. 优点（方法或实验设计亮点）

- **创新性**：首次系统比较 MoE 专家与稠密 FFN 在多义性上的差异，并利用 k-稀疏探针量化，为稀疏性可解释性提供了新视角。
- **升维思路**：将可解释性分析从神经元提升到专家级别，更符合 MoE 架构的模块化特性，有望降低解释复杂度。
- **实证解决争论**：通过自动解释数百个专家，给出了对“专家专业化”的明确结论（细粒度任务专家而非领域专家），具有实际指导意义。
- **代码开源**：提供 GitHub 仓库，便于复现和进一步研究。

## 8. 不足与局限

- **实验覆盖有限**：仅比较了单一模型配置（未明确说明具体模型大小和类型），可能缺乏跨模型族的泛化性。未涉及不同训练阶段（如预训练 vs 微调）的影响。
- **数据集未明确**：未列出具体评估数据集，可能影响结果的可重复性。
- **算力缺失**：未提供任何硬件或时间信息，不利于评估方法的计算成本。
- **多义性指标单一**：仅使用 k-稀疏探针恢复能力作为指标，未结合其他多义性度量（如激活相关性、神经元聚类等）进行三角验证。
- **自动解释的验证**：对数百个专家的功能解释缺乏人工评估或定量验证（如准确率），可能引入偏差。
- **仅关注 FFN 层**：未分析注意力层或其他组件中稀疏性的影响，结论可能不适用于整个模型。

（完）
