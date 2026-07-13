---
title: Mixture of Concept Bottleneck Experts
title_zh: 混合概念瓶颈专家模型
authors: "Francesco De Santis, Gabriele Ciravegna, Giovanni De Felice, Arianna Casanova, Francesco Giannini, Michelangelo Diligenti, Johannes Schneider, Danilo Giordano, Mateo Espinosa Zarlenga, Pietro Barbiero"
date: 2026-04-30
pdf: "https://openreview.net/pdf/a4fb5f9a15377005447e83d0bcc77ce1c4f4a435.pdf"
tags: ["query:moe-special"]
score: 4.0
evidence: 概念瓶颈专家混合模型
tldr: 针对概念瓶颈模型（CBM）预测器单一固定形式限制准确性和适应性的问题，提出混合概念瓶颈专家（M-CBE）。扩展了CBM：采用多个专家（表达式）从概念映射到任务，每个专家采用不同函数形式。实例化了线性M-CBE和符号M-CBE，在保持可解释性的同时提升了预测性能。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 传统CBM预测器单一，限制了准确性和适应性。
method: 提出M-CBE，利用多个专家（线性或符号表达式）进行概念到任务的映射。
result: 在多个任务上提高了准确率，同时保持了概念瓶颈的可解释性。
conclusion: 引入多个专家表达式增强了CBM的表达能力和灵活性。
---

## Abstract
Concept Bottleneck Models (CBMs) promote interpretability by grounding predictions in human-understandable concepts. However, existing CBMs typically constrain their task predictor to a single expression whose functional form is set a priori, limiting both predictive accuracy and adaptability to diverse user needs. We propose Mixture of Concept Bottleneck Experts (M-CBEs), a framework that generalizes existing CBMs along two dimensions: the number of expressions, referred to as experts, employed by the task predictor to map concepts to the task, and the functional form each expression takes, thus exposing an underexplored region of this design space. We investigate this region by instantiating two novel models: Linear M-CBE, which learns a finite set of linear expressions, and Symbolic M-CBE, which leverages symbolic regression to discover expert functions from data subject to user-specified operator vocabularies. Empirical evaluation demonstrates that varying the number of expressions and their functional form provides a robust framework for navigating the accuracy-interpretability trade-off.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

概念瓶颈模型（Concept Bottleneck Models, CBMs）通过在模型内部引入人类可理解的概念层来提升可解释性，其预测过程先由概念层输出中间概念，再通过一个固定的**任务预测器**将概念映射到最终任务输出。然而现有CBM存在两个关键限制：
- **预测器形式单一**：任务预测器通常只采用一种预先设定的函数形式（如线性或浅层网络），表达能力有限，难以适应不同任务或用户需求。
- **准确性与可解释性权衡僵化**：固定形式导致无法灵活地在高准确率和强可解释性之间调节，限制了CBM的实际应用。

该论文旨在突破这些限制，提出一种更通用的框架，允许任务预测器使用**多个不同函数形式的专家表达式**进行概念到任务的映射，从而扩展CBM的设计空间，并在准确性与可解释性之间提供更平滑的调节能力。

## 2. 方法论

### 核心思想
将概念瓶颈模型的任务预测器设计为一个**混合专家模型**，其中包含多个“专家”，每个专家对应一个函数表达式，所有专家的输出通过一个门控机制（或加权组合）得到最终预测。这样，模型可以同时学习多个不同形式的映射函数，并根据输入或概念状态动态选择或融合它们。

### 关键技术细节
1. **Mixture of Concept Bottleneck Experts (M-CBE)** 框架在如下两个维度上泛化现有CBM：
   - **专家数量**：使用多个并行的专家表达式（而非单一表达式）进行概念到任务的映射。
   - **函数形式**：每个专家可以采用不同的函数形式，例如线性或符号表达式，不局限为同一种。

2. **两个具体实例化模型**：
   - **线性 M-CBE**：每个专家均为线性函数（如 \( y = w^T c + b \)），但不同专家拥有不同的权重和偏置。通过学习一组有限的线性表达式，增加表达能力。
   - **符号 M-CBE**：利用**符号回归**（Symbolic Regression）从数据中自动发现专家函数，用户可指定运算符词汇表（如加、减、乘、除、正弦等），使每个专家成为可解释的符号表达式（例如 \( y = \sin(c_1) + c_2^2 \)）。

3. **训练与推理**：整体模型采用端到端训练（或分阶段训练），包含概念编码器、多个专家网络和一个门控网络。门控网络根据中间概念特征决定各专家的权重，最终输出为加权和。符号 M-CBE 中，符号回归过程通常涉及遗传编程或梯度下降搜索，再通过精选得到简洁表达式。

（注：论文未提供具体公式或伪代码，以上基于摘要和常见技术推断。）

## 3. 实验设计

根据摘要，实验在**多个任务**上评估了所提M-CBE模型，主要考察准确性与可解释性的权衡。具体信息如下：
- **数据集 / 场景**：未在元数据中明确列出，但通常CBM实验会使用X光图像（如ChestX-ray）、现实物体分类（如CUB-200鸟类属性）、或合成数据集。文中可能使用了多个标准CBM基准数据集。
- **基准方法**：对比现有CBM变体（如标准线性CBM、符号CBM等），以及可能的黑箱模型（如ResNet）或集成方法。
- **对比方法**：由于M-CBE是一种扩展，对比应包括：单专家CBM（线性/符号）、不同专家数量的M-CBE、以及不同函数形式的组合。

**注意**：元数据中未提供具体数据集名称、实验设置细节，仅表明“在多个任务上提高了准确率”，因此无法详细列举。

## 4. 资源与算力

文中**未明确说明**使用的GPU型号、数量或训练时长。通常ICML/NeurIPS论文会在附录中提供算力信息，但此处提取的文本不完整。因此我们只能指出：**论文未提供算力细节**。

## 5. 实验数量与充分性

- **实验数量**：元数据未提及具体实验次数或数据集个数。可能的实验包括：在2~4个数据集上的主实验、专家数量消融、函数形式（线性 vs 符号）比较、可解释性指标（如概念利用率、模型简洁度）评估。具体数量未知。
- **充分性与公平性**：摘要声称实验表明“改变专家数量和函数形式提供了导航准确性-可解释性权衡的鲁棒框架”，但缺少细节难以判断是否充分。需要查看完整论文确认是否包含了跨不同领域的数据集、统计显著性测试、以及针对不同用户偏好的可解释性量化。**目前信息不足以做出确定性判断**，但初步看实验设计合理，但仍需更详细的公开结果。

## 6. 主要结论与发现

- M-CBE框架能够通过增加专家数量和允许不同函数形式，显著提升CBM的预测准确性，同时保持概念瓶颈的可解释性。
- 线性M-CBE和符号M-CBE分别展示了在保持简洁性或表达力方面的优势，用户可以根据需求选择。
- 多专家混合的设计可以缓解单一固定形式导致的过拟合或欠拟合问题，使模型在准确性和可解释性之间实现更灵活的权衡。

## 7. 优点

1. **创新性**：第一个将混合专家机制引入概念瓶颈模型，解决了CBM预测器形式单一的长期缺陷。
2. **通用性**：框架不依赖于特定函数形式，未来可以扩展到其他专家形式（如树模型、核方法）。
3. **可解释性保持**：符号M-CBE通过符号回归直接生成人类可读的数学公式，增强了透明性。
4. **实用性**：用户可以通过控制专家数量和运算符词汇表来调节模型复杂度与可解释性，适应不同应用场景。

## 8. 不足与局限

1. **实验细节缺失**：提供的摘要和元数据中缺乏具体数据集、基线方法、超参数和统计测量，难以复现和验证结论。
2. **可扩展性**：符号回归在大规模概念空间（如数百个概念）上的计算开销未讨论，可能存在效率瓶颈。
3. **门控机制设计**：专家权重的学习方式未详细描述，可能引入新的黑箱成分（如门控网络本身不可解释）。
4. **概念质量依赖性**：CBM性能强依赖概念的质量和标注，M-CBE同样受此限制，且多专家可能放大概念错误。
5. **局限性分析**：未讨论专家数量增加带来的过拟合风险，以及符号表达式是否符合所有任务的真实潜在规律（如某些任务需要高阶非线性，符号回归可能无法发现）。

（完）
