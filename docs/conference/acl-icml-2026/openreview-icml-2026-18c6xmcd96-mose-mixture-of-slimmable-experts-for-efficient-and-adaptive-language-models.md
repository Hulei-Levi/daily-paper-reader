---
title: "MoSE: Mixture of Slimmable Experts for Efficient and Adaptive Language Models"
title_zh: MoSE：面向高效自适应语言模型的可瘦身专家混合
authors: "Nurbek Tastan, Stefanos Laskaridis, Karthik Nandakumar, Samuel Horváth"
date: 2026-04-30
pdf: "https://openreview.net/pdf/1a67107bc5fe640d678298c5698d359f5ada103a.pdf"
tags: ["query:moe-special"]
score: 5.0
evidence: 可瘦身专家实现可变宽度的条件计算
tldr: 本文针对MoE模型在精度-计算权衡上存在大跳跃的问题，提出可瘦身专家混合（MoSE）架构，每个专家包含可嵌套的子结构，能以不同宽度执行。这使得条件计算不仅局限于选择哪些专家，还能控制每个专家使用多少计算量。单一预训练模型即可支持更连续的精度-计算权衡谱，且训练稳定。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: MoE一旦选定专家则全量执行，精度-计算权衡存在不连续跳跃。
method: 每个专家采用可瘦身结构，支持可变宽度执行；提出稳定训练方案。
result: 单一模型可覆盖多个精度-计算权衡点，性能优于独立模型。
conclusion: 细粒度条件计算可提升MoE部署灵活性，便于资源自适应。
---

## Abstract
Mixture-of-Experts (MoE) models scale large language models efficiently by sparsely activating experts, but once an expert is selected, it is executed fully. Hence, the trade-off between accuracy and computation in an MoE model typically exhibits large discontinuities. We propose Mixture of Slimmable Experts (MoSE), an MoE architecture in which each expert has a nested, slimmable structure that can be executed at variable widths.  This enables conditional computation not only over which experts are activated but also over how much of each expert is utilized. Consequently, a single pretrained MoSE model can support a more continuous spectrum of accuracy-compute trade-offs at inference time. We present a simple and stable training recipe for slimmable experts under sparse routing, combining multi-width training with standard MoE objectives. During inference, we explore strategies for runtime width determination, including a lightweight test-time training mechanism that learns how to map router confidence/probabilities to expert widths under a fixed budget. Experiments on GPT-style models, various routing regimes, zero-shot downstream reasoning benchmarks, and continual pre-training adaptation of DeepSeek model show that MoSE matches or improves standard MoE at full width and consistently shifts the compute-quality frontier toward lower inference FLOPs. The code can be found at: https://github.com/tnurbek/mose.

---

## 论文详细总结（自动生成）

# 论文详细总结：MoSE: Mixture of Slimmable Experts for Efficient and Adaptive Language Models

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **背景**：混合专家（Mixture-of-Experts, MoE）模型通过稀疏激活专家实现大型语言模型的高效扩展。但传统MoE在选定专家后，该专家会被**完全执行**（full width），导致精度与计算量之间的权衡呈现**大而不连续的跳跃**。例如，调整路由策略（如激活专家数量）只能离散地改变计算量，无法在单一模型中灵活适应不同资源约束。
- **核心问题**：如何实现更连续的精度-计算权衡，使单一预训练模型能够动态调整计算量以匹配运行时资源预算，同时保持或提升性能。
- **整体含义**：本文提出**MoSE（Mixture of Slimmable Experts）**，将每个专家设计为可“瘦身”（slimmable）的嵌套子结构，支持以**可变宽度**执行。这使得条件计算不仅控制激活哪些专家，还控制每个专家**使用多少计算量**，从而实现更细粒度的自适应计算，提升MoE模型在资源受限场景下的部署灵活性。

## 2. 论文提出的方法论

- **核心思想**：继承MoE的稀疏路由机制，但将每个专家替换为**可瘦身的子网络**（slimmable expert）。每个专家包含多个嵌套的宽度子集（例如，不同大小的隐藏层维度），可在推理时按需选择不同的宽度执行，从而连续调节每个专家的计算量。
- **关键技术细节**：
  - **多宽度训练**：在训练过程中，每个专家同时学习不同宽度下的表现。具体做法是随机采样宽度并前向传播，使得所有宽度子网络都能得到优化。
  - **训练稳定性**：结合标准MoE的负载均衡损失和辅助损失，提出简单且稳定的多宽度训练方案，避免稀疏路由下不同专家宽度不一致导致的收敛问题。
  - **推理时宽度决策**：研究多种运行时宽度确定策略，包括基于路由置信度/概率的映射函数，以及一种**轻量级测试时训练**（test-time training）机制：学习一个轻量级预测器，将路由器的输出概率映射到各专家的最优宽度，以在固定计算预算下最小化性能损失。
- **公式或算法流程**（文字说明）：
  1. 输入序列经过共享层后，路由器为每个token计算专家权重。
  2. 对于被路由选中的专家，根据预算决定其执行宽度（例如从1/4, 1/2, 3/4, 1倍宽度中选择）。
  3. 各专家按选定宽度前向，输出加权聚合。
  4. 训练时采用多宽度采样+标准MoE损失（包括平衡损失）。
  5. 推理时，利用离线学习的宽度预测器或在线启发式规则动态调整宽度。

## 3. 实验设计

- **数据集与场景**：
  - **GPT风格语言模型**：在文本生成任务上预训练并评估。
  - **多种路由机制**：包括Top-1、Top-2等不同稀疏路由策略。
  - **零样本下游推理基准**：如常识推理、问答等标准零样本评估数据集（论文未具体列出全部名称，但通常包含如HellaSwag、WinoGrande等）。
  - **持续预训练适应**：将MoSE应用于DeepSeek模型，进行持续预训练适应实验。
- **基准（Benchmark）**：以标准MoE模型作为主要基线，对比不同宽度/计算量下的性能-计算量前沿（compute-quality frontier）。同时对比独立预训练的具有不同宽度的模型。
- **对比方法**：
  - 标准MoE（全宽专家）。
  - 独立训练的变宽度MoE模型（每个宽度单独训练）。
  - 可能还包括其他条件计算方法（如动态层跳过等，但摘要未详细列举）。

## 4. 资源与算力

- 论文中**未明确说明**使用的具体GPU型号、数量及训练时长。仅提及实验涉及GPT风格模型和DeepSeek的持续预训练适应，推测可能使用多个GPU（例如A100或H100），但具体算力细节不透明。这一点需要在总结中明确指出。

## 5. 实验数量与充分性

- **实验组数**：涵盖多个维度——不同模型规模（GPT风格）、不同路由模式（Top-1、Top-2等）、多个零样本基准、以及一个外部模型适配实验（DeepSeek）。整体实验较为丰富。
- **充分性评估**：
  - **优点**：涵盖了从标准预训练到持续预训练的场景，验证了方法的通用性；对比了多种推理策略；消融实验（如有）应包含了多宽度训练、宽度预测器等组件的效果。
  - **不足**：缺少对超大规模模型（如千亿参数）的验证；零样本基准数量未详细列出，可能覆盖面不够全面；未与最近的其他动态计算MoE方法（如Switch Transformer的变体、LegoMoE等）进行对比；缺乏在图像或多模态任务上的验证。
  - **公平性**：作者声称单一MoSE模型匹配或优于标准MoE（全宽），且在与独立模型比较时，MoSE用更少的参数或FLOPs达到相同性能，比较是合理的。但缺少对计算预算分配策略的公平性分析（例如宽度选择开销是否计入总FLOPs）。

## 6. 论文的主要结论与发现

- MoSE在**全宽**匹配或改进标准MoE性能，同时在**较低计算预算**下显著优于标准MoE（因为标准MoE无法降低单个专家计算量，只能通过减少专家数量离散调节）。
- 单一MoSE模型可以覆盖多个精度-计算权衡点，比独立训练多个不同宽度模型更高效。
- 轻量级测试时训练机制可以有效学习宽度映射，在固定预算下实现接近最优的性能。
- 持续预训练适应实验表明MoSE可以无缝迁移到现有大模型（如DeepSeek）上，带来部署灵活性的提升。

## 7. 优点

- **方法新颖性**：首次将可瘦身结构与稀疏MoE结合，实现细粒度条件计算，解决了MoE计算跳变问题。
- **实用性强**：单一预训练模型即可支持多种计算约束，便于部署到不同硬件平台。
- **训练稳定**：提出的多宽度训练方案简单有效，不引入过多额外复杂性。
- **实验覆盖较广**：涵盖多种路由策略、零样本任务及模型迁移场景，验证了泛化性。
- **开放代码**：提供GitHub仓库，利于复现和后续研究。

## 8. 不足与局限

- **实验细节缺失**：未提供具体计算资源（GPU型号、数量、训练时间），可能影响可复现性。
- **基准对比不完全**：缺少与近期动态计算MoE方法（如分块路由、层级稀疏化）的比较，说服力可能受限。
- **规模验证不足**：仅实验了GPT风格中等规模模型和DeepSeek模型，未在百亿/千亿超大规模MoE上测试，可扩展性存疑。
- **推理开销**：宽度决策本身（尤其是测试时训练模型）可能引入额外计算，文中未详细分析这一开销是否纳入总预算。
- **稀疏路由下的宽度分配问题**：不同专家宽度不一致可能导致负载不均衡加剧，文中未充分讨论。
- **下游任务局限**：零样本任务多为常识推理，缺乏复杂推理、生成质量等评估。
- **长期部署适用性**：测试时训练机制需要额外样本和计算，对于实时场景可能不实用。

（完）
