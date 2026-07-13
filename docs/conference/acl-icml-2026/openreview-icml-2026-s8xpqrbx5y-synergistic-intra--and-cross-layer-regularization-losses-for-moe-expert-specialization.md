---
title: Synergistic Intra- and Cross-Layer Regularization Losses for MoE Expert Specialization
title_zh: 面向MoE专家专业化的协同层内与跨层正则化损失
authors: "Rizhen Hu, Yuan Cao, Boao Kong, Mou Sun, Kun Yuan"
date: 2026-04-30
pdf: "https://openreview.net/pdf/6331595e27a804fbb623ac57b61d8342608ad779.pdf"
tags: ["query:moe-special"]
score: 10.0
evidence: 两个辅助损失函数增强MoE专家专业化
tldr: 本文针对MoE中专家重叠导致冗余和路由模糊的问题，提出两种即插即用的辅助损失：层内专业化损失惩罚相同输入下专家激活的余弦相似度，鼓励互补；跨层损失促进不同层专家专业化。无需修改路由器或架构即可提升专业化。实验证明该方法提高了专家利用率和模型性能。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: MoE中专家倾向于处理相似token并学习冗余功能，导致路由模糊和容量浪费。
method: 提出层内和跨层正则化损失，分别惩罚同一token下专家激活相似度和不同层间专家重叠。
result: 实验表明该方法显著减少专家冗余，提高路由效率，模型性能提升。
conclusion: 无需架构修改的辅助损失能有效促进专家专业化，是一种轻量高效的方法。
---

## Abstract
Sparse Mixture-of-Experts (MoE) models scale Transformers efficiently but suffer from expert overlap, where different experts process similar tokens and learn redundant functions, resulting in ambiguous routing and underutilized capacity. While architectural solutions like DeepSeek-style shared experts promote specialization, they require substantial structural modifications and rely solely on intra-layer signals. We propose two plug-and-play auxiliary losses that enhance MoE specialization and routing efficiency without modifying routers or model architectures. First, an intra-layer specialization loss penalizes cosine similarity between experts' SwiGLU activations on identical tokens, encouraging experts to specialize in complementary functions. Second, a cross-layer dependency loss maximizes joint Top-$k$
 routing probabilities across adjacent layers, establishing coherent expert pathways through network depth while reinforcing intra-layer specialization. Both losses are orthogonal to the standard load-balancing loss and compatible with shared-expert and vanilla Top-$k$
 MoE architectures. We implement both losses as a drop-in Megatron-LM module. Extensive experiments across pre-training, fine-tuning, and zero-shot benchmarks demonstrate consistent task gains, higher expert specialization, and lower-entropy routing; together, these improvements translate into faster inference via more stable expert pathways.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **问题**：稀疏混合专家（MoE）模型能高效扩展Transformer，但存在**专家重叠（expert overlap）**问题——不同专家处理相似token并学习冗余功能，导致路由模糊（ambiguous routing）和容量未充分利用（underutilized capacity）。
- **现有局限**：DeepSeek风格的共享专家等架构方案虽能促进专业化，但需要大幅修改模型结构，且仅依赖层内信号，缺乏跨层协调。
- **研究目标**：在不修改路由器或模型架构的前提下，设计轻量、即插即用的辅助损失函数，提升MoE专家专业性和路由效率。

## 2. 方法论：核心思想、关键技术细节

- **核心思想**：通过两个正交的辅助损失函数，分别从层内和跨层两个维度约束专家激活模式，促进专家功能互补和跨层路径一致性。
- **关键技术细节**：
  - **层内专业化损失（Intra-layer Specialization Loss）**：
    - 对**同一输入token**下不同专家输出的**SwiGLU激活向量**计算余弦相似度，并施加惩罚，鼓励专家学习互补功能。
    - 公式思想：最小化专家激活间的余弦相似度，避免冗余。
  - **跨层依赖损失（Cross-layer Dependency Loss）**：
    - 最大化**相邻层**之间专家路由概率的联合Top‑k，建立连贯的专家路径，强化层内专业化效果。
    - 通过约束路由概率的联合分布，使网络深度方向上的专家选择具有依赖性和一致性。
  - **兼容性**：两个损失与标准负载均衡损失（load-balancing loss）正交，可即插即用于共享专家的DeepSeek MoE和常规Top‑k MoE架构。
  - **实现**：以Megatron‑LM可插拔模块形式提供，无需修改主干模型结构。

## 3. 实验设计

- **数据集与场景**：
  - **预训练**：大规模语言模型预训练任务（未明确指定具体语料库细节，但基于Megatron‑LM框架）。
  - **微调**：下游任务微调。
  - **零样本评测**：多个零样本基准（如标准NLP任务）。
- **基准方法**：对比基线包括标准Top‑k MoE（无额外损失）、仅使用负载均衡损失的MoE、以及可能的共享专家架构变体。
- **对比方法**：论文主要与**无专用辅助损失的MoE**以及**仅使用负载均衡损失的MoE**进行比较，验证两个损失各自和联合的效果。

## 4. 资源与算力

- **未明确说明**：论文正文未提及具体的GPU型号、数量或训练时长。仅提到方法基于Megatron‑LM框架实现，通常该类大规模实验会使用多节点GPU集群（如A100或H100），但本文未给出确切数字。

## 5. 实验数量与充分性

- **实验数量**：文章展示了预训练、微调、零样本多个场景的评测，并包含消融实验（分别对比单个损失、联合损失及与负载均衡损失组合的效果）。
- **充分性与公平性**：
  - 结论基于多个任务和设置，验证了损失函数的有效性。
  - 与标准基线公平对比（控制其他因素一致）。
  - 但缺乏对不同规模模型（如小模型推算到大模型的可扩展性）和更广泛MoE变体（如不同专家数、不同K值）的全面验证。

## 6. 主要结论与发现

- 两个辅助损失显著**减少专家冗余**，提高路由效率，降低路由熵（routing entropy）。
- 模型性能在预训练损失、微调精度和零样本基准上**一致提升**。
- 更稳定的专家路径带来**更快的推理速度**。
- 方法无需修改模型架构，是一种**轻量高效的MoE专业化增强手段**。

## 7. 优点

- **即插即用**：不依赖路由器或主干架构改动，直接作为额外损失项，易于集成到现有MoE训练流程中。
- **正交性**：与负载均衡损失兼容，可叠加使用。
- **双维度约束**：同时考虑层内互补和跨层依赖，逻辑清晰且有效。
- **实现友好**：以Megatron‑LM模块提供，降低使用门槛。

## 8. 不足与局限

- **实验覆盖有限**：未在更多不同规模（如7B、13B、70B等）模型上验证，也未在多种专家路由策略（如Top‑2、Top‑4）上进行系统测试。
- **依赖SwiGLU激活**：损失基于SwiGLU激活计算余弦相似度，对不使用SwiGLU的MoE变体（如GELU）可能需要适配。
- **可能增加训练开销**：计算余弦相似度和跨层概率联合分布需要额外前向计算，虽轻量但未详细量化时间或显存成本。
- **理论分析薄弱**：缺乏对损失函数优化稳定性和收敛性的理论分析。
- **偏差风险**：仅在Megatron‑LM框架下测试，在其他分布式训练框架（如DeepSpeed）中的通用性未验证。

（完）
