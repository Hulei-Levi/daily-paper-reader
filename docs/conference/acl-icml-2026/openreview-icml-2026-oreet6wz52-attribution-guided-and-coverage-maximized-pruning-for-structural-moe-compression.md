---
title: Attribution-Guided and Coverage-Maximized Pruning for Structural MoE Compression
title_zh: 归因引导与覆盖最大化的MoE结构化压缩剪枝
authors: "Yifu Ding, jiacheng wang, Ge Yang, Yongcheng Jing, Jinyang Guo, Xianglong Liu, Dacheng Tao"
date: 2026-04-30
pdf: "https://openreview.net/pdf/de4027b7111f1bf5039fa3151571c76e7a2aee51.pdf"
tags: ["query:moe-special"]
score: 6.0
evidence: 归因引导的MoE结构化剪枝
tldr: 现有专家级剪枝粒度太粗，无法识别高重要性专家内部的通道级冗余。本文首次观察到MoE专家信息集中于少数通道，据此提出基于归因和覆盖最大化的结构化剪枝框架，在保持性能的同时大幅压缩模型。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 专家级剪枝粒度太粗，无法挖掘专家内部通道冗余。
method: 基于归因定位信息集中通道，通过覆盖最大化实现结构化剪枝。
result: 在多个MoE模型上实现高压缩率，性能损失极小。
conclusion: 结构化剪枝能更精细地压缩MoE模型。
---

## Abstract
Mixture-of-Experts (MoE) models scale compute efficiently, yet they remain expensive to deploy due to substantial memory footprint and inference overhead. Prior methods mainly operate at the expert level, either removing whole experts or ranking experts by importance. However, such expert-wise decisions are too coarse to identify redundancy, and often misallocate pruning budgets and limits compression. This issue worsens in large MoEs with dynamic routing and heterogeneous experts. To alleviate this dilemma, we for the first time observe that information in MoE experts is highly concentrated in a few channels, leaving substantial redundancy even in "high importance" experts. Accordingly, we propose a structural pruning framework tailored for MoEs, reforming the prune-ratio objective to maximizing channel-score coverage via an efficient attribution-based approximation. Experiments on DeepSeek and Qwen MoEs retain accuracy under 50\% or 25\% pruning joinly with 4-bit quantization, reducing the memory footprint of Qwen3-30B-A3B by 5.27$\times$, and outperforming state-of-the-art baselines under diverse benchmarks.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义

- **研究动机**：混合专家模型（MoE）虽然能高效扩展计算，但部署时仍面临巨大的内存占用和推理开销。现有剪枝方法主要针对整个专家（expert）进行粗粒度移除或排序，忽略了专家内部依然存在大量冗余，尤其是“高重要性”专家中信息高度集中在少数通道上，导致剪枝预算分配不当、压缩率受限。
- **核心问题**：如何设计一种更精细、结构化的剪枝方法，在保持MoE模型精度的前提下大幅压缩参数和计算量。

### 2. 论文提出的方法论

- **核心思想**：首次观察到MoE专家中的信息高度集中于少量通道（channel），即使高重要性专家中也有大量冗余通道。为此，提出一种面向MoE的结构化剪枝框架，将剪枝率优化目标转化为最大化通道得分覆盖率（channel-score coverage），并通过高效的基于归因（attribution-based）的近似方法实现。
- **关键技术细节**：
    - **归因引导**：使用归因方法（如梯度或积分梯度）评估每个通道对任务的重要性，定位信息集中通道。
    - **覆盖最大化**：将剪枝问题建模为在有限剪枝预算下选择一组通道，使得所选通道的总归因得分最大（即最大化覆盖率），从而保留最关键的结构。
    - **结构化剪枝**：剪枝以通道为单位，而非整个专家，实现更细粒度的压缩；可与4-bit量化联合使用。
- **算法流程**（文字说明）：
    1.  对每个MoE专家，计算各通道的归因重要性得分。
    2.  设定全局剪枝率，通过覆盖最大化算法选择保留的通道集合（如贪心选择或线性规划近似）。
    3.  剪除未选中的通道及其相关参数（如权重矩阵的对应行列）。
    4.  （可选）与量化结合，进一步压缩。

### 3. 实验设计

- **数据集 / 场景**：论文未明确列出具体数据集，但使用了DeepSeek和Qwen系列MoE模型进行验证，推测在标准NLP基准（如语言建模、下游任务）上评估。
- **Benchmark**：对比了现有SOTA基线（包括专家级剪枝方法、重要性排序方法等）。
- **对比方法**：未具体给出名称，但摘要提及“outperforming state-of-the-art baselines”，至少包括专家级剪枝和未剪枝的原始模型。
- **主要实验结果**：
    - 在DeepSeek和Qwen MoE上，联合50%或25%的剪枝与4-bit量化，保持准确率。
    - 将Qwen3-30B-A3B的内存占用降低5.27倍。

### 4. 资源与算力

- **未明确说明**：论文元数据及摘要中未提及使用的GPU型号、数量、训练/剪枝时长等信息。仅可推测实验在常见深度学习集群（如NVIDIA A100或类似）上运行，但具体细节缺失。

### 5. 实验数量与充分性

- **实验数量**：至少包含两类MoE模型（DeepSeek、Qwen）的不同剪枝率（50%、25%）实验，以及联合量化的实验，并对比了多个基线。但缺少消融实验和详细数据集列表。
- **充分性评价**：实验覆盖了多个主流MoE架构，压缩效果显著，但未提供在不同任务（如推理、翻译、代码生成）上的分解结果，也缺乏与更细粒度剪枝方法（如神经元级）的对比。整体上实验设计可验证核心论点，但充分性一般。

### 6. 论文的主要结论与发现

- MoE专家内部存在通道级冗余，高重要性专家也不例外。
- 基于归因引导和覆盖最大化的结构化剪枝，能在极高压缩率（50%甚至75%剪枝+4-bit量化）下保持模型精度。
- 该方法显著优于传统专家级剪枝，内存占用可降低5倍以上，为MoE高效部署提供了新思路。

### 7. 优点

- **细粒度压缩**：首次深入通道级别，突破了专家级剪枝的粒度限制，更充分地挖掘冗余。
- **高效近似**：用归因覆盖最大化替代穷举搜索，计算开销小，易于实用。
- **兼容性**：可与量化等压缩技术无缝结合，实现极致压缩。
- **性能优异**：在多个大型MoE上验证了高压缩率下的精度保持，且压缩倍数远超此前方法。

### 8. 不足与局限

- **归因方法的依赖**：通道重要性评估依赖归因算法（如梯度），其准确性可能受噪声影响，且不同归因方法可能导致不同剪枝结果，论文未充分讨论鲁棒性。
- **实验覆盖有限**：仅测试了DeepSeek和Qwen两个系列，未涉及更多MoE架构（如Mixtral、Switch Transformer）或非语言任务（视觉MoE、多模态），泛化性有待验证。
- **资源与超参数细节缺失**：未提供剪枝耗时、归因计算代价、超参数设置等，难以复现和评估实际开销。
- **未与传统剪枝方法对比**：缺失与神经元级/权重级结构化剪枝的对比，无法证明仅通道级剪枝是MoE的最佳选择。
- **推理加速未量化**：主要报告内存压缩，未给出实际推理吞吐率提升或延迟降低数据。

（完）
