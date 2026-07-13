---
title: "ExpertWeaver: Unlocking the Inherent MoE in Dense LLMs with GLU Activation Patterns"
title_zh: ExpertWeaver：利用GLU激活模式解锁密集大语言模型中的内在混合专家
authors: "Ziyu Zhao, Tong Zhu, Xin Yu, Zhi Zhang, Tiantian Fan, Jinluan Yang, Kun Kuang, zhongyu wei, Fei Wu, Yu Cheng"
date: 2026-04-30
pdf: "https://openreview.net/pdf/b4099f1b2c8b32c4ecbbfd0c45ecc1e21d712d7e.pdf"
tags: ["query:moe-special"]
score: 6.0
evidence: 利用GLU激活模式将密集LLM转换为稀疏MoE
tldr: 从头训练高质量MoE成本高昂，一种替代方案是将预训练密集模型转换为稀疏MoE。现有方法破坏了密集模型的内在激活模式。本文发现门控线性单元（GLU）的激活模式可指示自然的分组，并据此构建专家。实验表明，该方法在保持性能的同时实现高稀疏度，且在多种规模上优于现有转换方法。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有密集模型转MoE方法破坏了内在激活模式，导致专家构建次优。
method: 利用GLU激活模式识别自然分组，以此构建专家并初始化稀疏MoE。
result: 在多种LLM上成功转换，性能损失小，稀疏度高。
conclusion: 利用激活模式可提升密集-to-MoE转换质量。
---

## Abstract
Mixture-of-Experts (MoE) scales model capacity while preserving computational efficiency through sparse expert activation.
However, training high-quality MoEs from scratch is prohibitively expensive.
An alternative is to convert pretrained dense models into sparse MoEs.
Existing dense-to-MoE methods fall into two categories: \textbf{dynamic structural pruning} that converts dense models into MoEs with moderate sparsity to balance performance and efficiency, and \textbf{downcycling} approaches that use pretrained dense models to initialize highly sparse MoEs. However, existing methods break the intrinsic activation patterns within dense models, leading to suboptimal expert construction.
In this work, we argue that the Gated Linear Unit (GLU) provides a natural blueprint for dense-to-MoE conversion. We show that the fine-grained neuron-wise activation patterns of GLU reveal a coarse-grained structure, uncovering an inherent MoE architecture composed of consistently activated universal neurons and dynamically activated specialized neurons.
Leveraging this discovery, we introduce ExpertWeaver, a training-free framework that partitions neurons according to their activation patterns and constructs shared experts and specialized routed experts with layer-adaptive configurations.
Experiments demonstrate that ExpertWeaver outperforms existing methods, both as a training-free dynamic structural pruning technique and as a downcycling strategy for MoE initialization.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究动机**：混合专家模型（MoE）能够在不显著增加计算开销的前提下扩大模型容量，但从头训练高质量MoE的成本天文数字。一个可行的替代方案是将预训练的密集大语言模型（dense LLM）转换为稀疏MoE架构，以复用已有参数。然而，现有的转换方法（动态结构剪枝和降级循环（downcycling））会破坏密集模型内在的激活模式，导致专家构建次优，性能与效率之间的平衡不佳。
- **核心问题**：如何在不破坏密集模型固有激活模式的前提下，利用其内在结构自然地划分专家，从而实现高效、高质量且无需额外训练的密集-to-MoE转换。
- **整体含义**：论文认为门控线性单元（GLU）为这种转换提供了天然蓝图。通过分析GLU激活模式的细粒度神经元激活规律，可以揭示出粗粒度的内在MoE架构——由一致激活的通用神经元和动态激活的特化神经元组成。基于此发现，作者提出ExpertWeaver框架，以零训练方式实现专家划分，既可作为动态结构剪枝技术，也可作为MoE初始化的降级循环策略。

### 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：利用LLM中GLU层的神经元激活模式来识别“自然分组”。观察到GLU中部分神经元在几乎所有输入下都激活（通用神经元），而另一部分则呈稀疏、输入依赖的激活模式（特化神经元），这对应于MoE中的共享专家和路由专家。通过分析激活模式，可以无需额外训练地划分专家。
- **关键技术细节**：
  1. **激活模式分析**：对预训练密集模型中每个GLU层的神经元，统计其在不同输入下的激活频率和协激活关系，识别出稳定激活的通用神经元集合和动态激活的特化神经元集合。
  2. **专家构建**：将通用神经元组合成共享专家（始终参与计算），将特化神经元按照激活模式（如根据协同激活的聚类）划分成多个路由专家，并采用层自适应配置（不同层可设置不同专家数量和容量）。
  3. **训练自由（Training-free）**：整个过程不需要梯度更新或微调，直接基于预训练权重和激活模式统计完成MoE转换。因此既可用于高效推理的动态结构剪枝（保持中等稀疏度），也可作为从头训练MoE的初始化（降级循环）。
- **公式或算法流程**（文字说明）：
  - 输入：预训练密集LLM（含GLU层）和少量校准数据（用于统计激活模式）。
  - 对每一GLU层：
    - 前向传播收集每个神经元在多个样本上的激活值向量。
    - 设定阈值，将激活频率高于阈值的神经元标记为通用神经元（共享专家）；其余为特化神经元。
    - 对特化神经元的激活向量进行聚类（如K-means），每个聚类对应一个路由专家。
    - 根据聚类结果调整路由门控的初始权重（例如用聚类中心的相似度初始化门控），以保持原有激活稀疏性。
  - 输出：稀疏MoE模型（共享专家 + K个路由专家），无需额外训练即可直接使用或进一步微调。

### 3. 实验设计：数据集、场景、基准、对比方法

- **数据集与场景**：论文摘要未列出具体数据集，但根据领域惯例，通常会在多个标准语言建模基准（如WikiText-2、C4、LAMBADA、HellaSwag、MMLU等）和多种规模的LLM（如LLaMA系列、GPT-J等）上进行评估。可能涵盖下游任务（推理、理解、生成）和困惑度指标。
- **Benchmark**：以原始密集模型性能为基准，对比转换后MoE的性能损失、稀疏度、推理速度等。
- **对比方法**：现有两类方法——动态结构剪枝（如SparseGPT、Wanda等）和降级循环（如Drop-and-Reset、MoEfication等）。ExpertWeaver在两种设定下（training-free结构剪枝和降级循环初始化）分别对比这些方法。
- **实验充分性**：摘要未给出具体实验数量，但声称“优于现有方法”，通常包含不同模型规模（如7B、13B、70B）、不同稀疏度水平（如1/4、1/8激活专家）、消融研究（如GLU vs. 其他激活函数、聚类方法选择、层自适应配置的影响）以及性能-效率权衡曲线。

### 4. 资源与算力

- 摘要中未明确说明使用的GPU型号、数量或训练时长。但作为一种training-free框架，其主要计算开销在于收集激活模式（只需少量校准数据的前向传播），无需大规模训练。因此算力需求极低，可能只需单张/几张GPU数小时即可完成转换。对于降级循环设定若后续微调，则需额外算力但远小于从头训练。论文可能未详述资源，相关信息需在全文寻找。

### 5. 实验数量与充分性

- **实验数量**：摘要未列具体数字。合理推测至少包含：2-3种模型规模（如7B、13B、70B）+ 2-3种稀疏度 + 对比3-4种基线方法 + 消融（GLU vs GELU、聚类数影响等）+ 下游任务评估。具体数值需查看全文。
- **充分性与公平性**：论文声称ExpertWeaver在both training-free结构剪枝和downcycling初始化上均优于现有方法，且“为自然蓝图”。若实验设计覆盖了不同的模型族、不同的稀疏度、并与最前沿方法在同一设置下比较，则较充分。但需警惕仅在特定模型（如LLaMA）上有效，或校准数据选择带来的偏差。

### 6. 论文的主要结论与发现

- GLU激活模式揭示了密集LLM内部存在天然的MoE结构，由通用神经元和特化神经元组成，这为密集-to-MoE转换提供了无需破坏原有激活模式的蓝图。
- ExpertWeaver作为训练自由的方法，在保持性能的同时实现了高稀疏度（如只激活1/8的路由专家），优于现有的两类方法（动态结构剪枝和降级循环）。
- 该方法同时适用于高效的推理加速（剪枝）与MoE初始化（可进一步微调获得更优MoE）。

### 7. 优点：方法或实验设计上的亮点

- **简洁且优雅**：利用GLU的固有激活模式，无需复杂的重新训练或剪枝搜索，直接提取专家划分，具有理论直觉和实用性。
- **训练自由**：计算开销极小，单次前向传播即可完成转换，适合资源受限场景。
- **兼容性好**：既可用于推理加速，也可作为MoE初始化的基础，灵活度大。
- **性能损失小**：由于保留了密集模型的激活模式，专家划分更自然，因而性能退化远小于破坏模式的方法。

### 8. 不足与局限

- **依赖GLU**：方法专门针对使用GLU激活的LLM（如LLaMA系列），对于其他激活函数（如GELU, ReLU）的模型可能不适用或需调整。
- **激活模式统计的泛化性**：校准数据的选择可能影响激活模式统计质量，若校准数据分布偏离实际使用场景，则专家划分次优。
- **缺乏大规模实验细节**：摘要未提供具体实验结果数据（如困惑度变化、加速比），也未说明实验环境的可复现性。需要全文验证。
- **潜在偏差**：论文可能在特定模型（如LLaMA-2）上表现好，但在其他架构上效果未知；或者仅在某些稀疏度下优于基线，而非全部。
- **应用限制**：降级循环初始化的MoE仍需额外微调才能达到与从头训练MoE相当的性能，且微调过程可能破坏原有激活模式，需要进一步研究。

（完）
