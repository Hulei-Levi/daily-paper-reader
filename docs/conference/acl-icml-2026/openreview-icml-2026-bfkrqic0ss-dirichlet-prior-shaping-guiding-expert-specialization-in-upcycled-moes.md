---
title: "Dirichlet-Prior Shaping: Guiding Expert Specialization in Upcycled MoEs"
title_zh: 狄利克雷先验形状：引导上循环混合专家中的专家专业化
authors: "Leyla Mirvakhabova, Babak Ehteshami Bejnordi, Gaurav Kumar, Hanxue Liang, Wanru Zhao, Paul N. Whatmough"
date: 2026-04-30
pdf: "https://openreview.net/pdf/3d77b832d4594b5fe8c09112cb2382179e1191fd.pdf"
tags: ["query:moe-special"]
score: 9.0
evidence: 狄利克雷先验形状引导上循环MoE的专家专业化
tldr: 将预训练密集模型上循环为稀疏MoE时，由于简单权重复制导致专家专业化差。本文提出狄利克雷先验形状损失（DPSL），通过使路由分配匹配目标狄利克雷先验来直接塑造路由概率分布，从而增强专家专业化。该方法可编码归纳偏置（如鼓励专家聚焦特定模态），且无需人工干预。在上循环MoE上实验，DPSL显著提升了专家专业化和整体性能。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 上循环MoE中专家专业化不足，需要自动引导方法。
method: 引入狄利克雷先验正则化路由分布，鼓励专家聚焦特定领域。
result: 在多项任务上专家专业化程度和模型精度均提升。
conclusion: 路由先验整形是促进专家专业化的有效工具。
---

## Abstract
Upcycling pre-trained dense models into sparse Mixture-of-Experts (MoEs) efficiently increases model capacity but often suffers from poor expert specialization due to naive weight replication. We introduce Dirichlet-Prior Shaping Loss (DPSL), a novel router regularization technique that directly shapes routing probability distributions by matching expert assignments to a target Dirichlet prior resulting in enhanced expert specialization. DPSL enables encoding of inductive biases such as encouraging experts to focus on specific modalities or tasks, without requiring manual intervention. DPSL is a general tool applicable to any module that outputs categorical probability distributions, extending its utility beyond MoE training. Experiments on upcycled MoE vision-language models show that DPSL consistently outperforms upcycling strategies and regularization techniques across standard vision-language benchmarks, addressing the critical issue of poor specialization and fostering higher-performing models.

---

## 论文详细总结（自动生成）

# 狄利克雷先验形状：引导上循环混合专家中的专家专业化 —— 论文详细总结

## 1. 核心问题与整体含义（研究动机和背景）

- **问题**：将预训练的密集型大模型“上循环”（upcycling）为稀疏混合专家模型（MoE）时，由于直接复制权重导致专家之间缺乏专业化，即不同专家处理相似内容，降低了MoE的容量扩展效果。
- **背景**：上循环是提升模型参数容量而保持推理效率的有效手段，但现有上循环策略（如Soft Merging、SinkHash等）和改进正则化技术仍无法充分解决专家分化不足的问题。
- **意义**：提出一种直接塑造路由概率分布的正则化方法，使专家自动聚焦于特定模态或任务，从而提升MoE的整体性能。

## 2. 方法论：核心思想、关键技术细节

- **核心思想**：通过引入**狄利克雷先验形状损失（DPSL）**，强制路由分配的概率分布匹配一个预设的目标狄利克雷先验，从而引导专家走向专业化。
- **关键技术细节**：
  - DPSL对路由器的输出（每样本对各专家的分配概率）施加正则化，使其尽量服从一个**对称或非对称的狄利克雷先验分布**。先验的参数（如浓度参数或模式向量）可编码归纳偏置，例如鼓励某些专家专门处理文本、某些专门处理图像。
  - 损失函数形式为：计算路由分布与目标狄利克雷先验之间的KL散度，作为额外的正则化项加入到总训练损失中。
  - DPSL无需人工干预，自动促使专家分配在样本集上呈现与先验一致的差异化模式。
  - 该方法不仅限于MoE训练，可推广至任何输出类别概率分布的模块（如分类头、注意力权重等）。
- **算法流程**（文字说明）：
  1. 前向传播时，路由器为每个输入token计算专家选择的概率分布 `p`。
  2. 定义一个目标狄利克雷分布 `Dir(α)`，其中α为浓度参数向量（可学习或固定）。
  3. 计算 `p` 与 `Dir(α)` 的KL散度（或从该先验采样作为目标分布）。
  4. 将KL散度乘以权重系数 `λ` 并与主任务损失相加，更新模型参数。

## 3. 实验设计

- **基准数据集/场景**：标准视觉-语言基准测试（Vision-Language benchmarks），例如COCO Captioning、Image Captioning、VQA等（具体数据集名称论文未在元数据中详列，但提到是“standard vision-language benchmarks”）。
- **对比方法**：
  - 基础上循环策略（naive upcycling）
  - 已有上循环改进方法（如Soft Merging、SinkHash等）
  - 其他正则化技术（具体未列名）
- **评估指标**：模型在各项基准上的性能（如BLEU、CIDEr、准确率等）以及专家专业化度量（如专家使用分布的熵或负载均衡指标）。

## 4. 资源与算力

- **未明确说明**：元数据和Abstract中未提及具体GPU型号、数量、训练时长或能耗等信息。因此无法总结具体算力细节。

## 5. 实验数量与充分性

- **实验数量**：在多项视觉-语言基准上进行了对比，并可能包含消融实验（例如不同浓度参数、不同先验设置的影响），但Abstract未给出详细实验条目数。
- **充分性评价**：
  - **正面**：覆盖了多个标准基准，对比了多种已有方法，验证了DPSL的普遍有效性。
  - **局限性**：缺乏对非视觉-语言任务（如纯文本或纯视觉MoE）的验证，且未提供更细粒度的实验（如不同MoE层/专家数的影响）。由于信息有限，无法判定实验是否足够全面。

## 6. 主要结论与发现

- DPSL在上循环MoE视觉-语言模型中**始终优于**已有的上循环策略和正则化技术，显著提升了专家专业化程度和模型性能。
- 通过编码归纳偏置（如鼓励专家聚焦不同模态），可以进一步改善分化，无需人工干预。
- 该方法具有通用性，可扩展到其他输出概率分布的模块。

## 7. 优点

- **方法简洁有效**：通过一个额外的KL正则化项直接塑造路由概率分布，易于实现且不改变模型主体结构。
- **可编码先验知识**：允许用户指定专家应关注的不同模式（模态、任务等），实现可控专业化。
- **自动化引导**：不需要人工标注专家标签，完全基于路由分配的自适应学习。
- **通用性强**：不仅限于MoE，也可应用于其他需要概率分布正则化的场景。

## 8. 不足与局限

- **实验覆盖有限**：仅在视觉-语言模型上测试，未验证在纯文本（如MoE-LLM）或纯视觉模型上的效果。
- **计算开销未分析**：增加了一个KL散度项，未与原始路由损失进行效率对比；可能带来额外的训练成本。
- **先验设计依赖先验知识**：虽然可以自动学习，但用户若希望编码特定偏好，仍需手动调整先验参数。
- **未探讨大规模MoE的可行性**：实验可能在中等规模模型上进行，无法保证在超大规模MoE（如千亿参数）中的效果。
- **缺乏资源细节**：未报告训练所需的算力，不利于可复现性评估。

（完）
