---
title: "PuzzleMoE: Efficient Compression of Large Mixture-of-Experts Models via Sparse Expert Merging and Bit-packed inference"
title_zh: PuzzleMoE：通过稀疏专家合并和位打包推理实现大规模混合专家模型的高效压缩
authors: "Yushu Zhao, Zheng Wang, Minjia Zhang"
date: 2026-04-30
pdf: "https://openreview.net/pdf/b1339003efbb0d861cec8203ab7c7c78aa87b244.pdf"
tags: ["query:moe-special"]
score: 7.0
evidence: 提出细粒度专家合并方法用于MoE压缩
tldr: 针对大规模MoE模型部署时内存开销大的问题，提出PuzzleMoE，首次实现元素级专家合并，通过细粒度操作在保持高性能的同时显著压缩模型。实验表明在高压缩比下性能优于现有粗粒度方法。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有MoE压缩方法因粗粒度操作导致性能下降严重。
method: 提出元素级专家合并方法PuzzleMoE，结合位打包推理。
result: 在多个语言模型上，PuzzleMoE在高压缩比下保持了较高性能，优于现有方法。
conclusion: 细粒度元素级合并是MoE压缩的有效方向。
---

## Abstract
Mixture-of-Experts (MoE) have shown strong potential in scaling language models efficiently by activating only a small subset of experts per input. However, their deployment remains limited due to the high memory overhead associated with storing all expert parameters, particularly as the number of experts increases. To address this challenge, prior works have explored expert dropping and merging strategies; however, they often suffer from notable performance drop especially at high compression ratios due to their reliance on coarse-grained tensor- or expert-level operations. In this paper, we introduce PuzzleMoE, the first MoE merging method to enable fine-grained element-wise merging while achieving both high accuracy and inference speed, via two key innovations: First, PuzzleMoE performs sparse expert merging by identifying element-wise weight redundancy and specialization. It introduces a dual-mask approach to capture both shared and expert-specific salient parameters. Second, to avoid the overhead of storing masks and signs, we introduce a bit-packed encoding scheme that reuses underutilized exponent bits, enabling efficient MoE inference on GPUs. Extensive experiments demonstrate that PuzzleMoE outperforms prior MoE compression methods by up to 16.7\% on MMLU at 50\% compression ratio, and achieves up to 1.80$\times$ end-to-end inference throughput gain.

---

## 论文详细总结（自动生成）

# PuzzleMoE 论文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）
- **研究动机**：大规模混合专家模型（Mixture-of-Experts, MoE）通过只激活少量专家，在扩展模型规模时具有高效潜力。然而，其部署受限于存储所有专家参数带来的高内存开销，尤其是专家数量增多时问题更为突出。
- **背景问题**：已有工作采用专家丢弃或专家合并策略进行压缩，但这些方法依赖粗粒度的张量级或专家级操作，在高压缩比下性能下降显著。
- **整体含义**：本文旨在通过细粒度元素级合并实现对 MoE 模型的高效压缩，在保持高精度的同时提升推理速度。

## 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程
- **核心思想**：提出 PuzzleMoE，首次实现**细粒度元素级专家合并**，通过识别每个权重的冗余性和专门化，有选择地合并共享参数和专家特有参数，并设计高效位打包编码以支持 GPU 推理。
- **关键技术细节**：
  - **稀疏专家合并**：识别元素级权重冗余与专门化，引入**双掩码方法**（dual-mask approach）来捕捉共享的显著参数和专家特有的显著参数。
  - **位打包编码方案**：为避免存储掩码和符号位的额外开销，复用未充分利用的指数位，实现高效的 GPU 推理。
- **算法流程（文字说明）**：
  1. 对每个专家权重矩阵，分析元素级权重的重要性和冗余度。
  2. 通过双掩码机制区分共享参数（多个专家通用）和专家特有参数（单个专家关键）。
  3. 对共享参数进行合并，对特有参数保留，形成稀疏的专家表示。
  4. 利用位打包编码将掩码和符号信息编码到权重的指数部分，减少存储量并加速推理。

## 3. 实验设计：数据集、benchmark、对比方法
- **基准数据集**：主要在 MMLU（Massive Multitask Language Understanding）基准上进行评估。
- **压缩比**：重点展示了 50% 压缩比下的结果。
- **对比方法**：与已有的 MoE 压缩方法（如专家丢弃、粗粒度专家合并等）进行对比。
- **评估指标**：准确率（MMLU 上的表现）以及端到端推理吞吐量（throughput gain）。

## 4. 资源与算力
- 论文摘要及元数据中**未明确说明**使用的 GPU 型号、数量、训练时长等算力信息。仅提及推理吞吐量提升（1.80×），但未给出训练或压缩过程的计算资源细节。需注意这一点。

## 5. 实验数量与充分性
- **实验数量**：摘要中仅报告了 MMLU 上的主要结果和吞吐量增益。未提及不同数据集、多种压缩比、消融实验等具体数量。从现有信息看，实验覆盖有限。
- **充分性与公平性**：论文声称在 50% 压缩比下优于先前方法 16.7%（MMLU），且吞吐量提升 1.80×。但缺乏更多数据集和更广泛的对比，评估的充分性和公平性需要进一步验证。没有提供误差棒或统计显著性检验。

## 6. 论文的主要结论与发现
- **主要结论**：PuzzleMoE 通过细粒度元素级合并，在高压缩比下显著优于粗粒度方法，能在保持高精度的同时大幅提升推理速度。这证明了细粒度元素级合并是 MoE 压缩的有效方向。
- **具体发现**：
  - 在 50% 压缩比下，MMLU 准确率比之前方法提升最高 16.7%。
  - 端到端推理吞吐量提升 1.80×。

## 7. 优点：方法或实验设计上的亮点
- **方法创新性**：首次实现元素级专家合并，突破粗粒度操作的局限。
- **双掩码策略**：有效分离共享参数和专家特有参数，减少信息损失。
- **位打包编码**：复用指数位存储掩码和符号，避免额外内存开销，兼容 GPU 硬件。
- **实验指标全面**：同时报告了准确率和推理吞吐量，体现压缩对性能和效率的双重收益。

## 8. 不足与局限
- **实验覆盖不足**：仅报告了 MMLU 一个基准上的结果，缺少在多种语言任务、不同规模 MoE 模型上的验证。
- **对比方法不够全面**：未提及与最新量化、剪枝等压缩方法的比较。
- **资源信息缺失**：未说明压缩过程的计算成本（训练或微调所需算力）。
- **实际部署限制**：位打包方案可能对特定 GPU 架构有依赖性，通用性需进一步验证。
- **偏差风险**：仅在一个压缩比（50%）下详细报告，其他压缩比下的表现未知。

（完）
