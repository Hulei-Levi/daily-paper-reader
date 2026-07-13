---
title: "LiME: Lightweight Mixture of Experts for Efficient Multimodal Multi-task Learning"
title_zh: LiME：面向高效多模态多任务学习的轻量混合专家
authors: "Md Kowsher, Haris Mansoor, Nusrat Jahan Prottasha, Ozlem Garibay, Victor Zhu, Zhengping Ji, Chen Chen"
date: 2026-04-30
pdf: "https://openreview.net/pdf/f646b2975f6e3045c5ee5e94d2ea1b7c0fd64b63.pdf"
tags: ["query:moe-special"]
score: 9.0
evidence: 通过轻量调制实现MoE中的专家专业化
tldr: 现有的MoE参数高效微调方法为每个专家配备独立适配器，导致参数量随专家数线性增长。本文提出LiME，使用共享的PEFT模块，并通过轻量专家向量调制其输出，实现专家专业化。同时引入零参数路由，利用冻结和适应后的表示差异进行路由选择。在多种多任务场景下，LiME以更少参数取得更好性能。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: MoE-PEFT中每个专家需独立适配器，参数过多且限制架构。
method: 使用共享PEFT模块加轻量专家向量调制，并采用零参数路由。
result: 在多模态多任务上以更少参数超越现有MoE-PEFT方法。
conclusion: 轻量调制可实现高效专家专业化。
---

## Abstract
MoE-PEFT methods combine Mixture of Experts with parameter-efficient fine-tuning for multi-task adaptation, but require separate adapters per expert—causing trainable parameters to scale linearly with expert count and limiting applicability to adapter-based architectures. We propose LiME (Lightweight Mixture of Experts), which achieves expert specialization through lightweight modulation rather than adapter replication. Instead of separate adapters, LiME uses a single shared PEFT module and modulates its output with lightweight expert vectors, reducing expert parameters while generalizing to any PEFT method. Notably, LiME introduces zero-parameter routing by leveraging existing frozen and adapted representations—eliminating learned router parameters typically required per layer. Theoretically, we prove that (i) more experts preserve more task-relevant information and (ii) modulation approximates full expert-specific PEFT with bounded error. LiME further incorporates n-gram windowed routing and adaptive expert selection (Auto Top-K) based on routing confidence. Experiments on MMT-47, a multimodal multi-task benchmark with 47 tasks spanning text, image, and video, demonstrate that LiME achieves competitive or superior performance while using up to 4× fewer trainable parameters and up to 29% faster training compared to corresponding MoE-PEFT baselines.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究动机**：现有的混合专家（MoE）参数高效微调（PEFT）方法在应对多任务学习时，为每个专家配备独立的适配器（adapter），导致训练参数量随专家数线性增长，且局限于适配器架构，泛化性差。
- **背景**：多模态多任务学习需要同时处理文本、图像、视频等任务，高效微调至关重要。MoE-PEFT虽能实现任务特异性适应，但参数冗余和架构限制成为瓶颈。
- **核心问题**：能否在不复制适配器、不增加路由参数的前提下，实现专家的高效专业化，并适用于任意PEFT方法？

### 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：通过轻量调制（lightweight modulation）而非适配器复制来达成专家专业化。使用单个共享PEFT模块，配合轻量专家向量（expert vectors）调制其输出，从而减少专家相关参数并泛化到任何PEFT方法。
- **关键技术细节**：
  - **共享PEFT + 专家向量调制**：共享PEFT（如LoRA）输出基础适应结果，每个专家学习一个极小的向量（维度等于PEFT输出维度），对共享输出进行逐元素缩放或添加偏置，实现差异化。
  - **零参数路由（Zero-parameter Routing）**：利用冻结表示（预训练模型的输出）与适应后表示（共享PEFT输出）之间的差异作为路由依据，无需额外学习路由参数。具体通过比较每个token经过共享PEFT前后的表示差异，选择激活差异最大的专家。
  - **n-gram窗口路由**：考虑到多模态序列中邻近token的任务相关性，在连续窗口内聚合路由决策，提高平滑性。
  - **自适应Top-K（Auto Top-K）**：基于路由置信度动态选择每个token激活的专家数量，而非固定K值。
  - **理论证明**：证明了（i）更多专家能保留更多任务相关信息；（ii）调制近似于全专家专用PEFT，且误差有界。

### 3. 实验设计：数据集、基准、对比方法

- **数据集与场景**：使用MMT-47多模态多任务基准，包含47个任务，覆盖文本、图像、视频三种模态。
- **基准（Benchmark）**：MMT-47官方评估标准，包括每个任务的准确率/指标。
- **对比方法**：
  - 全参数微调（Full FT）
  - 单任务PEFT（如LoRA）
  - 多种MoE-PEFT基线：MoE-LoRA、MoE-Adapter等，每个专家配备独立适配器。
  - 消融变体：去掉n-gram窗口、去掉Auto Top-K、替换为零调制等。

### 4. 资源与算力

- 论文中未明确说明使用的GPU型号、数量、训练时长等具体算力信息，仅提及训练速度比对应MoE-PEFT基线快29%。未提供硬件细节，属于信息缺失。

### 5. 实验数量与充分性

- **实验数量**：主实验在47个任务上进行，报告了平均性能；此外进行了多组消融实验（如路由策略、专家向量维度、Top-K机制等），以及不同PEFT后端的对比（LoRA、Adapter等）。
- **充分性**：实验覆盖多模态场景，对比方法全面（包括多种MoE-PEFT变体），消融设计合理。但缺乏跨更大规模模型（如LLaMA-65B）或更多数据集的验证；未报告统计显著性检验，可能受随机性影响。

### 6. 论文的主要结论与发现

- LiME使用**4倍更少的训练参数**，训练速度**快29%**，在MMT-47上达到与或优于现有MoE-PEFT方法的性能。
- 轻量专家向量调制足以实现有效的专家专业化，且远低于独立适配器的参数开销。
- 零参数路由基于表示差异有效，n-gram窗口和Auto Top-K进一步提升了路由质量和任务适应性。
- 证明了更多专家有助于保留任务信息，且调制误差有界，支持方法有效性。

### 7. 优点

- **参数高效**：专家向量参数量可忽略，且共享PEFT模块统一，整体参数量不随专家数线性增长。
- **架构无关**：可附加于任何PEFT方法（LoRA、Adapter、Prefix Tuning等），通用性强。
- **路由零参数**：无需学习路由网络，避免额外参数量和训练成本，同时利用冻结/适应差异具备可解释性。
- **自适应机制**：n-gram窗口和Auto Top-K提高了路由的稳定性和灵活性。
- **理论支撑**：提供了收敛性和近似误差的理论保证，增强了可信度。

### 8. 不足与局限

- **计算资源未披露**：缺少GPU型号、数量、训练总时长等，影响可复现性和效率评估。
- **实验规模有限**：仅在MMT-47（47个任务）上验证，未在更大规模多任务或多模态数据集（如MetaWorld、VL-Checklist）上测试。
- **仅对比MoE-PEFT基线**：未与近期其他高效多任务方法（如AdapterFusion、Hyperformer、ProTuning）全面比较。
- **路由设计依赖表示差异**：在任务差异极小的场景下，可能路由区分度不足，论文未分析此边缘情况。
- **缺乏对专家粒度的深入分析**：如专家向量维度对性能的影响仅在单一实验中涉及，未系统探讨。

（完）
