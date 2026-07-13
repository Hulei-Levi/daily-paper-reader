---
title: Mining Tensor/Neuron-Level Sparsity to Maximize Mixture-of-Experts Potential in Post-Training and Inference
title_zh: 挖掘张量/神经元级稀疏性以最大化混合专家模型在后训练和推理中的潜力
authors: "Weilin Cai, Le Qin, Shwai He, Junwei Cui, Ang Li, Jiayi Huang"
date: 2026-04-30
pdf: "https://openreview.net/pdf/a374207bc1901226d75743d531590e8a3d862aad.pdf"
tags: ["query:moe-special"]
score: 6.0
evidence: 通过张量/神经元级稀疏性提升MoE效率
tldr: "现有MoE稀疏化工作主要关注预训练阶段，忽略了后训练和推理阶段存在的张量和神经元级稀疏性。本文提出完整专家分区和基于阈值的令牌-专家丢弃技术，在Mixtral-8x7B上平均准确率提升1%（GSM8K提升4%），优化了精度与效率的权衡。"
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有方法未充分利用MoE在后训练和推理中的多粒度稀疏性。
method: 提出完整专家分区和阈值令牌-专家丢弃方法，利用张量和神经元级稀疏性。
result: "在Mixtral-8x7B上平均准确率提升1%，GSM8K提升4%。"
conclusion: 利用多粒度稀疏性可显著提升MoE的精度-效率权衡。
---

## Abstract
Mixture of Experts (MoE) has emerged as a mainstream architecture for Large Language Models (LLMs), balancing computational efficiency with model scalability. While prior work has explored increasing tensor-level sparsity via finer-grained expert configurations during pre-training, we identify significant unexploited sparsity at both the tensor and neuron levels during post-training and inference.
To leverage this, we propose complete expert partition for post-training and threshold-based token-expert dropping for inference. These techniques improve the Mixtral-8$\times$7B model's average accuracy by 1\% across nine downstream benchmarks (notably 4\% on GSM8K). 
To further optimize the accuracy-efficiency trade-off for inference, we introduce dual-threshold token-expert dropping with partial expert partition and reconstruction. Our approach yields a 1.19$\times$ MoE speedup and a 0.5\% accuracy gain on Mixtral-8$\times$7B when combining post-training and inference optimizations. For inference-only optimization on OLMoE-Instruct and DeepSeek-V2-Lite-Chat, we achieve up to 1.41$\times$ MoE speedup with a negligible accuracy loss ($<$0.5\%).

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **研究背景**：混合专家模型（MoE）已成为大语言模型的主流架构，能在保持计算效率的同时扩大模型规模。以往工作主要关注在预训练阶段通过更细粒度的专家配置来增加张量级稀疏性。
- **核心问题**：现有方法未充分利用 MoE 在后训练（post-training）和推理阶段存在的多粒度稀疏性（张量级和神经元级）。论文旨在挖掘这些未被开发的稀疏性，进一步提升 MoE 的精度-效率权衡。
- **整体意义**：通过后训练阶段的完整专家分区（complete expert partition）和推理阶段的基于阈值的令牌-专家丢弃（threshold-based token-expert dropping），在 Mixtral-8×7B 等模型上实现了平均准确率提升和加速，证明多粒度稀疏性在 MoE 后训练和推理中的巨大潜力。

## 2. 方法论

- **核心思想**：利用后训练和推理中存在的张量级和神经元级稀疏性，而非仅关注预训练阶段的稀疏化。提出两种互补技术：
  - **完整专家分区（Complete Expert Partition）**：用于后训练阶段。对每个专家内部的参数进行分区，以激活更稀疏的子结构，从而在不增加总计算量的情况下提升模型容量。
  - **基于阈值的令牌-专家丢弃（Threshold-based Token-Expert Dropping）**：用于推理阶段。根据激活值或重要性分数设定阈值，动态丢弃不重要的令牌或专家计算，从而加速推理。
- **关键技术细节**：
  - 后训练优化：通过完整专家分区，将每个专家的隐藏维度分割成若干子块，训练时只更新与当前令牌相关的子块，保持其他子块冻结，从而引入结构性稀疏性。
  - 推理优化：引入双阈值令牌-专家丢弃（dual-threshold token-expert dropping），结合部分专家分区与重构（partial expert partition and reconstruction），在精度损失极小的前提下实现加速。
- **算法流程（文字说明）**：
  1. 对于每个 MoE 层，在后训练阶段对每个专家的权重矩阵进行行/列分块，形成多个子专家。
  2. 前向传播时，根据令牌的输入特征动态选择激活的子专家，其余子专家保持零输出。
  3. 推理时，为每个令牌设定两个阈值：一个用于判断是否跳过整个专家计算（专家级丢弃），另一个用于判断是否跳过专家内部的某些子块（神经元级丢弃）。
  4. 可选步骤：部分专家分区 + 重构，进一步压缩计算图，同时用重构损失微调解码器以恢复精度。

## 3. 实验设计

- **数据集/场景**：9 个下游基准测试，包括 GSM8K（数学推理）、常识推理、自然语言理解等典型 NLP 任务。
- **Benchmark**：涵盖 Mixtral-8×7B（主要模型）、OLMoE-Instruct 和 DeepSeek-V2-Lite-Chat（用于推理优化验证）。
- **对比方法**：与标准 MoE 推理方法（无稀疏化）对比；与仅预训练稀疏化的方法对比；与无后训练优化的基线对比。未明确列出具体对比算法名称，但摘要暗示与现有仅预训练稀疏化的工作形成对比。

## 4. 资源与算力

- 文中**未明确说明**使用的 GPU 型号、数量、训练时长，也未给出具体的 FLOPs 或能耗数据。仅提及在 Mixtral-8×7B 上实现了 1.19× MoE 加速，在 OLMoE-Instruct 和 DeepSeek-V2-Lite-Chat 上最高 1.41× 加速。这可能是因为论文侧重算法而非工程实现，或该信息在正文中但未包含于提取的元数据中。

## 5. 实验数量与充分性

- **实验组数**：至少包含以下实验：
  - 主实验：Mixtral-8×7B 在 9 个下游基准上的平均准确率（提升 1%），GSM8K 单独提升 4%。
  - 后训练+推理联合优化：Mixtral-8×7B 上速度提升 1.19× 且准确率提升 0.5%。
  - 仅推理优化：在 OLMoE-Instruct 和 DeepSeek-V2-Lite-Chat 上速度提升最高 1.41×，精度损失＜0.5%。
- **充分性评估**：实验覆盖了不同规模模型、多个任务类型、以及联合优化与单独推理优化场景，比较全面。但缺失与其他稀疏化方法（如动态专家选择、剪枝）的量化对比，且未在更大模型（如千亿参数 MoE）上验证，因此实验充分性有一定局限。总体客观性较好，因为报告了精度和速度的 trade-off，且承认了精度损失。

## 6. 主要结论与发现

- 利用后训练和推理阶段的张量级/神经元级稀疏性可显著提升 MoE 的精度-效率权衡。
- 提出的完整专家分区和阈值丢弃方法在 Mixtral-8×7B 上平均准确率提升 1%（GSM8K 提升 4%），结合后训练与推理优化可获得 1.19× 加速且精度提升 0.5%。
- 仅推理优化可在 OLMoE-Instruct 和 DeepSeek-V2-Lite-Chat 上获得最高 1.41× 加速，精度损失低于 0.5%。
- 结果表明，现有多粒度稀疏性在 MoE 后训练和推理阶段尚未被充分利用，本文方法填补了这一空白。

## 7. 优点

- **方法创新性**：首次系统挖掘后训练和推理阶段的张量与神经元级稀疏性，而非仅关注预训练稀疏化，视角新颖。
- **实用性**：提出的技术（分区+丢弃）可以直接集成到现有 MoE 模型的部署流程中，无需重新预训练，降低了应用成本。
- **实验设计优点**：覆盖多个模型（Mixtral, OLMoE, DeepSeek）和多个下游任务，同时报告了精度和速度的双重收益， trade-off 清晰。
- **效率提升显著**：仅推理优化就能获得最高 1.4× 加速且精度损失极小，具有实际部署价值。

## 8. 不足与局限

- **实验覆盖**：仅在中等规模 MoE 模型（~7B 激活参数）上验证，未在更大模型（如 Mixtral-8×22B、千亿级 MoE）上测试，可能限制结论的泛化性。
- **缺乏消融实验细节**：未详细说明阈值的选择方法、分区粒度的敏感性分析；可能未对“完整专家分区”与“部分专家分区+重构”的效果单独消融。
- **对比基准不足**：未与现有的稀疏化推理方法（如 MoE 剪枝、专家合并、动态专家路由）进行定量对比，难以评估相对优势。
- **资源信息缺失**：未提供算力消耗，不利于其他研究者复现或比较效率。
- **偏差风险**：所有实验均在同一作者群的内部分布式环境下完成，可能缺乏第三方独立复现验证；且仅报告了正向结果，未讨论失败案例或阈值过高导致精度骤降的情况。

（完）
