---
title: "Rewiring Experts on the Fly: Continuous Rerouting for Better Online Adaptation in Mixture-of-Expert Models"
title_zh: 即时应变专家重路由：混合专家模型中在线适应的连续路由调整
authors: "Guinan Su, Yanwu Yang, Li Shen, Lu Yin, Shiwei Liu, Jonas Geiping"
date: 2026-04-30
pdf: "https://openreview.net/pdf/5ef3f1852abe33996089a6849728c61f6cf6f207.pdf"
tags: ["query:moe-special"]
score: 8.0
evidence: 提出用于MoE在线适应的连续重路由
tldr: 针对MoE模型部署时因分布漂移导致的次优路由，提出无数据在线测试时适应框架，在文本生成过程中持续优化专家选择。实验表明该方法有效提升了鲁棒性，且无需外部数据。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有测试时适应方法不适用于MoE架构或需外部数据。
method: 提出基于输入上下文的在线重路由，无需数据或监督。
result: 在多种分布漂移场景下，所提方法提升了模型性能和路由质量。
conclusion: 在线持续重路由是处理MoE分布漂移的有效轻量方案。
---

## Abstract
Mixture-of-Experts (MoE) models achieve efficient scaling through sparse expert activation, but often suffer from suboptimal routing decisions due to distribution shifts in deployment. While existing test-time adaptation methods could potentially address these issues, they primarily focus on dense models and require access to external data, limiting their practical applicability to MoE architectures. However, we find that, instead of relying on reference data, we can optimize MoE expert selection on-the-fly based only on input context. As such, we propose *a data-free, online test-time framework* that continuously adapts MoE routing decisions during text generation without external supervision or data. Our method cycles between two phases: During the prefill stage, and later in regular intervals, we optimize the routing decisions of the model using self-supervision based on the already generated sequence. Then, we generate text as normal, maintaining the modified router until the next adaption. We implement this through lightweight additive vectors that only update router logits in selected layers, maintaining computational efficiency while preventing over-adaptation. The results show consistent performance gains on challenging reasoning tasks while maintaining robustness to context shifts. For example, our method achieves a 5.5\% improvement on HumanEval with OLMoE. Furthermore, owing to its plug-and-play property, our method complements existing test-time scaling techniques, e.g., achieving 6\% average gains when incorporated with self-consistency on DeepSeek-V2-Lite.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

混合专家（Mixture-of-Experts，MoE）模型通过稀疏激活专家实现高效扩展，但在部署时因**分布漂移**（distribution shift）导致路由决策次优，从而影响模型性能。现有的测试时适应方法主要针对稠密模型设计，且通常需要外部数据或监督信号，限制了它们在MoE架构上的实际应用。本文旨在解决MoE模型在在线部署中缺乏轻量、无数据的路由优化方法的问题。

## 2. 方法：核心思想与关键技术细节

- **核心思想**：提出一种**无数据、在线测试时适应框架**，在文本生成过程中仅基于输入上下文对MoE路由决策进行连续优化，无需外部数据或监督。
- **关键技术细节**：
  - 框架在两个阶段之间循环：
    - **预填充（prefill）阶段及后续固定间隔**：利用自监督信号（基于已生成序列）优化模型的路由决策。
    - **正常生成阶段**：保持修改后的路由器，直到下一次适应。
  - 实现方式：在选定层中添加**轻量级加法向量（additive vectors）**，仅更新路由logits，从而维持计算效率并防止过度适应。
- **算法流程**（文字说明）：
  1. 模型接收输入，执行预填充阶段。
  2. 在预填充结束后及后续每间隔若干生成步，对路由器进行自监督优化（通过梯度下降更新加法向量，目标是改善路由选择）。
  3. 更新后的路由器用于后续文本生成，直到下一适应周期。
  4. 重复步骤2-3直至生成完成。

## 3. 实验设计

- **数据集与场景**：
  - 挑战性推理任务（如代码生成、数学推理等），具体提及**HumanEval**（代码生成基准）。
  - 分布漂移场景：包括上下文漂移、领域切换等。
- **Benchmark**：与原始MoE模型（无适应）及现有测试时适应方法对比。
- **对比方法**：未在摘要中列出具体方法名称，但提到与现有的测试时缩放技术（如自一致性（self-consistency））互补。
- **主要结果**：
  - 在OLMoE模型上，HumanEval任务提升**5.5%**。
  - 与DeepSeek-V2-Lite结合自一致性时，平均提升**6%**。

## 4. 资源与算力

文中**未明确说明**使用的GPU型号、数量、训练时长等具体算力信息。仅提及方法计算高效（轻量加法向量），但未提供实际资源消耗数据。需要进一步查阅全文或附录。

## 5. 实验数量与充分性

- 实验数量：从摘要可见至少涉及两个模型（OLMoE、DeepSeek-V2-Lite）和多个任务（HumanEval、可能还有其他推理任务），并包含与自一致性的结合实验。但未提及消融实验的具体数量或完整数据集列表。
- 充分性与公平性：摘要声称结果一致提升，且方法即插即用。但缺少与多种现有测试时适应方法的详细对比，也未报告方差或统计显著性。实验覆盖可能不够全面（例如未涉及视觉或多模态MoE场景）。总体而言，实验初步验证了有效性，但充分性有待全文补充。

## 6. 主要结论与发现

- 在线持续重路由是处理MoE模型部署时分布漂移的有效轻量方案，**无需外部数据**。
- 该方法在挑战性推理任务上取得一致性能提升，同时保持对上下文漂移的鲁棒性。
- 即插即用特性使其可与现有测试时缩放技术（如自一致性）互补，获得进一步收益。

## 7. 优点：方法与实验亮点

- **无数据/无监督**：无需标注数据或外部数据集，仅利用输入上下文自监督，实用性高。
- **轻量高效**：仅通过加法向量微调路由logits，计算开销低，适合在线部署。
- **即插即用**：可无缝集成到现有MoE模型及测试时缩放技术中。
- **连续适应**：在生成过程中间隔优化，而非一次性适应，更适应动态分布变化。
- **防止过适应**：通过限制更新范围和幅度（仅路由logits）避免灾难性遗忘。

## 8. 不足与局限

- **实验覆盖有限**：仅在少数模型（OLMoE、DeepSeek-V2-Lite）和任务（代码生成、推理）上验证，缺乏对更大规模MoE（如Mixtral 8x22B）或不同领域（如自然语言理解、翻译）的评估。
- **缺乏算力报告**：未提供实际GPU时间等资源消耗，难以评估方法在真实部署中的成本。
- **未与基线充分对比**：未列出具体的现有测试时适应方法（如Tent、SHOT等）的对比结果，仅提及可与自一致性结合，未说明相对优势。
- **潜在偏差风险**：自监督信号（基于已生成序列）可能引入噪声或错误累积，尤其在长文本生成中。
- **应用限制**：方法要求模型支持路由logits修改，对非MoE或固定路由模型不适用；且间隔适应策略的间隔长度可能敏感，需要调参。

（完）
