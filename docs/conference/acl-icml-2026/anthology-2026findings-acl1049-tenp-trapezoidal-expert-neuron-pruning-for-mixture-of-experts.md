---
title: "TENP: Trapezoidal Expert Neuron Pruning For Mixture-of-Experts"
title_zh: TENP：针对混合专家模型的梯形专家神经元剪枝
authors: "Jiangyang He, Shaolin Zhu, Deyi Xiong (德意 熊)"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.1049.pdf"
tags: ["query:moe-special"]
score: 7.0
evidence: 专家重要性评估用于剪枝
tldr: 针对MoE大语言模型部署中专家参数过多的问题，提出TENP梯形专家神经元剪枝框架。通过少量样本联合评估专家重要性，保留重要专家，对不重要专家进行神经元剪枝，形成从浅到深的梯形参数保留模式。实验表明该方法在压缩模型的同时保持了性能，为MoE模型压缩提供了新思路。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1049/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1620, \"height\": 835, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1049/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1652, \"height\": 936, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1049/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 793, \"height\": 500, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1049/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 791, \"height\": 451, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1049/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1645, \"height\": 889, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1049/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1639, \"height\": 1317, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1049/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1640, \"height\": 526, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1049/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 763, \"height\": 305, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1049/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1642, \"height\": 374, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1049/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1234, \"height\": 254, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1049/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 817, \"height\": 1009, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1049/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1565, \"height\": 723, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1049/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1556, \"height\": 341, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1049/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1563, \"height\": 258, \"label\": \"Table\"}]"
motivation: 现有MoE大模型压缩方法要么移除整个专家破坏路由拓扑，要么依赖非结构化剪枝效率低。
method: 提出TENP，通过样本评估专家重要性，对重要专家保留，对不重要专家进行结构化神经元剪枝，形成梯形保留模式。
result: 在保持性能的同时有效减少了参数量，优于现有压缩方法。
conclusion: TENP通过专家重要性驱动的剪枝，实现了高效的MoE模型压缩。
---

## Abstract
Mixture-of-Experts large language models (LLMs) scale efficiently through sparse activation, yet their deployment is fundamentally constrained by the large static parameter footprint of experts. Existing compression approaches either remove entire experts, disrupting routing topology and harming performance, or rely on unstructured weight pruning with limited practical efficiency. To address the limitations, we propose TENP, a structured **T**rapezoidal **E**xpert **N**euron **P**runing framework. Using a few samples, we identify and retain important experts, while applying expert neuron pruning (ENP) to less important experts, preserving model parameters in a trapezoidal pattern from shallow to deep layers. When evaluating expert importance, we jointly consider both the magnitude of the expert output and its ability to change the direction of the input vector. For ENP, we measure each neuron’s projected contribution to the expert output to identify and retain important neurons. We conduct extensive experiments on the Qwen and DeepSeek models. Under a routing expert sparsity of 40% and an average of 63.76% activated expert parameters, the DeepSeek model suffers only a 1-point drop in accuracy compared to the full-parameter model. Moreover, it outperforms the full-parameter model by 10% on code generation tasks.

---

## 论文详细总结（自动生成）

# TENP: Trapezoidal Expert Neuron Pruning For Mixture-of-Experts 论文详细总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：混合专家（MoE）大语言模型通过稀疏激活实现高效扩展，但其静态参数足迹过大，导致部署困难，尤其在内存受限环境中。现有压缩方法要么移除整个专家，破坏路由拓扑、损害性能；要么采用非结构化权重剪枝，效率有限且需专用硬件支持。
- **整体含义**：论文旨在设计一种结构化剪枝方法，在不改变路由拓扑的前提下减少MoE模型的参数冗余，从而平衡模型大小与性能，提升部署可行性。

## 2. 论文提出的方法论

- **核心思想**：提出TENP框架，通过两阶段剪枝：第一阶段保留重要专家，第二阶段对不重要专家进行神经元剪枝（ENP），形成从浅层到深层的梯形参数保留模式（浅层高冗余多剪，深层保留更多参数）。
- **关键技术细节**：
  - **专家重要性评估**：联合考虑专家输出向量的模长（长度贡献）和方向改变能力（1 - 余弦相似度），计算综合得分 \( I(E_l^i) = \sum_t c_{l,t}^i \cdot s_{l,t}^i \)，其中 \( c_{l,t}^i = g_{l,t}^i \|h_{l,t}^i\| \)，\( s_{l,t}^i = 1 - \text{Sim}(h_t^l, h_{l,t}^i) \)。跨领域时使用ℓ2归一化聚合。
  - **神经元重要性评估**：对每个专家，将每个神经元的输出向量投影到专家总输出上，用投影长度作为重要性指标（或可用ℓ2范数替代）。保留Top-K神经元，对应删除 \( W_{\text{up}} \)、\( W_{\text{gate}} \) 的行和 \( W_{\text{down}} \) 的列。
  - **梯形分布策略**：浅层保留较少参数（高剪枝率），深层保留更多参数，与全参数模型的矩形分布不同。第一阶段保留的重要专家占比随层数增加而增加。
- **算法流程**：使用少量（128个）验证样本进行重要性估算 → 按得分保留一定比例重要专家 → 对剩余专家按神经元重要性保留Top-K神经元 → 得到剪枝后的TENP模型。也可跳过专家选择直接对所有专家做ENP。

## 3. 实验设计

- **数据集/场景**：
  - 数学推理：GSM8K（8-shot）
  - 代码生成：MBPP（3-shot）、HumanEval（0-shot）
  - 科学问答：ARC-Easy、ARC-Challenge（25-shot）
  - 通用知识：MMLU（用于泛化性测试）
- **Benchmark**：以上五个标准数据集。
- **对比方法**：
  - 随机专家选择（Random）
  - 频率专家剪枝（Frequency）
  - 门控分数专家剪枝（Gating Score）
  - EASY-EP（Dong et al., 2025）
  - 自身变体：仅ENP、仅EP、随机选择专家和神经元等消融实验。
  - 其他：MoDeGPT（BI）、ShortGPT排名等层选择方法（附录E）。
- **模型**：Qwen1.5-MoE-A2.7B（14B参数，24层，60路由专家+4共享）、DeepSeek-V2-Lite（16B参数，27层，64路由专家+2共享）、Qwen3-Next-80B-A3B-Instruct（80B参数，附录F）。

## 4. 资源与算力

- 论文**未明确说明**使用的GPU型号、数量、训练时长或推理时间等算力资源。
- 仅在表5中报告了静态内存消耗和吞吐量对比：使用单张A100-SXM-80GB GPU测试Qwen模型，ENP方法将静态内存从32.95 GB降至16.37 GB，总吞吐量提升至全参数模型的1.47倍。
- 未提及训练/剪枝过程的计算资源。

## 5. 实验数量与充分性

- **实验数量**：主实验覆盖2个模型×2种路由专家稀疏度（30%、60%）×5个基准数据集，每种条件对比5种基线方法，共计大量实验点。此外还包括：
  - 消融实验（表2）：对比仅EP、仅ENP、随机选择、不同重要性度量（ℓ2 vs 投影长度）等7种变体。
  - 路由分析（图2）：对专家选择频率变化可视化。
  - 误差分析（图3）：各层输出欧氏距离。
  - 泛化性实验（表3、表4）：跨领域（数据从单一领域剪枝，评估其他领域表现）。
  - 不同数据量影响（图4）：从1到128样本测试。
  - 不同稀疏度（15%~90%）实验（图5）。
  - 重要专家保留比例调优（表6）。
  - 其他层选择方法对比（表7）。
  - 更大模型验证（表8，80B参数）。
- **充分性**：非常充分，覆盖了多个维度（不同稀疏度、模型架构、数据量、消融、泛化、路由行为等），对比方法全面，结果统计平均（3次运行）。实验设计客观公平，与同类方法在同一条件下比较。

## 6. 论文的主要结论与发现

- TENP在保持甚至提升性能的同时显著减少了静态参数和激活参数。在DeepSeek-V2-Lite上，60%专家稀疏度下仅损失约1%平均准确率，代码生成任务甚至超过全参数模型10%。
- 相较专家剪枝方法（如EASY-EP），TENP在所有基准上平均提升约16%。
- 保留原始路由拓扑是关键优势：TENP几乎不改变专家选择频率（图2），错误累积更慢（图3），泛化能力更强（跨领域剪枝后平均优于专家剪枝）。
- 梯形参数分布比均匀分布更优：浅层可承受更多剪枝，深层需保留更多参数以维持推理能力。
- 投影长度作为神经元重要性度量优于单纯ℓ2范数。
- 仅需少量样本（8个即可达到性能平台）即可完成剪枝，无需额外微调。

## 7. 优点

- **方法创新**：首次将“保留专家+神经元剪枝”结合，并提出深度感知的梯形分配策略。
- **实用性强**：结构化剪枝，无需特殊硬件，可适配现有推理框架（ENP无需修改框架，TENP需微调）。
- **路由拓扑保持**：避免专家剪枝导致的路径破坏，这是性能优于其他专家的核心原因。
- **低数据需求**：仅需少量样本即可确定重要性，实际部署友好。
- **实验全面**：多种模型、稀疏度、数据集、消融和泛化实验，证据充分。

## 8. 不足与局限

- **未在超大规模MoE模型上验证**：论文承认未对DeepSeek-V3.2等千亿参数模型进行实验，虽然推测更大模型可获更大收益，但缺乏直接证据。
- **推理框架适配**：TENP需要修改推理框架以支持不同大小的专家，虽然ENP无此问题，但完整方法部署复杂度高于纯专家剪枝。
- **仅针对SwiGLU激活的FFN**：公式基于SwiGLU，对其他FFN变体（如ReLU、GEGLU）需调整，虽论文提到可适配，但未实验验证。
- **未与微调基础上的剪枝方法（如MoE-I2）比较**：论文排除了需要微调的方法，但此类方法可能通过少量训练获得更好效果，缺少直接对比。
- **未提供训练/剪枝的具体算力消耗**：无法直接评估计算成本。
- **仅验证Qwen和DeepSeek两个系列**：其他MoE架构（如Mixtral、Kimi）未测试，泛化性有限。
- **数据量影响实验中仅使用模型自身生成回答**：可能存在数据噪声，但论文未讨论其与真实标注的差异影响。

（完）
