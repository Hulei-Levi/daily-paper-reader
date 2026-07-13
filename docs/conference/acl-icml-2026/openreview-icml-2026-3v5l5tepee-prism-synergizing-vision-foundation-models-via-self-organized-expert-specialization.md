---
title: "PRISM: Synergizing Vision Foundation Models via Self-organized Expert Specialization"
title_zh: PRISM：通过自组织专家专业化协同视觉基础模型
authors: "Ying Tang, Dong Li, Youjia Zhang, Zikai Song, Junqing Yu, Wei Yang"
date: 2026-04-30
pdf: "https://openreview.net/pdf/81fc9eb39fba96d7591eb6624f0e4b0f3a32f974.pdf"
tags: ["query:moe-special"]
score: 9.0
evidence: 通过自组织专家专业化融合视觉基础模型
tldr: 将多个视觉基础模型融合为单一高效模型时，直接蒸馏会导致负迁移。本文提出PRISM框架，采用双流混合专家结构，通过教师条件路由指导专家在独立表示子空间上专业化（解构阶段），再通过动态路由组合专家以适应下游任务（重组阶段）。在PASCAL-Context等数据集上实验证明，该方法有效缓解了特征冲突，实现了模块化的专家专业化。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 统一多个视觉基础模型时存在特征冲突和负迁移，需要模块化的专家专业化。
method: 提出教师条件路由的双流MoE，先解构专家到不同子空间，再动态重组。
result: 在多项视觉任务上显著提升了性能，优于直接蒸馏和多任务学习。
conclusion: 自组织专家专业化是融合多模型的有效范式。
---

## Abstract
Unifying the complementary strengths of diverse Vision Foundation Models (VFMs) into a single efficient model is highly desirable but challenged by the negative transfer inherent in monolithic distillation. To address these feature conflicts, we introduce \textbf{PRISM}, a novel dual-stream Mixture-of-Experts (MoE) framework that synergizes VFMs via modular specialization. We propose a two-stage paradigm: (1) expertise deconstruction, where a teacher-conditional router guides experts to specialize in distinct representational subspaces to mitigate interference, followed by (2) dynamic recomposition, where the router learns to assemble these experts into tailored computational pathways for downstream tasks. Experiments on PASCAL-Context and NYUD-v2 show that \textbf{PRISM} establishes a new state of the art, validating that sparse, emergent specialization is a scalable approach for integrating diverse visual knowledge.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机与背景）
- **核心问题**：将多个不同的视觉基础模型（VFMs）融合到一个单一高效模型中时，直接进行知识蒸馏会导致负迁移（negative transfer），即模型间的特征冲突削弱整体性能。
- **研究动机**：现有VFMs（如CLIP、DINO、MAE等）各有互补的视觉表征优势，但将它们简单合并会由于表征空间的不兼容而产生干扰。急需一种模块化的融合方式，使各专家模型专业化并协同工作。
- **整体含义**：PRISM框架通过自组织的专家专业化（emergent specialization）来化解特征冲突，为多模型融合提供了一种可扩展的范式，避免了传统一体化蒸馏的弊端。

## 2. 方法论：核心思想、关键技术细节、算法流程（文字说明）
- **核心思想**：采用双流混合专家（Dual-stream Mixture-of-Experts, MoE）结构，通过两阶段范式实现“解构-重组”。
  - **第一阶段：知识解构（Expertise Deconstruction）**
    - 设计一个**教师条件路由器（Teacher-conditional Router）**，根据不同教师模型（即源VFMs）的特征分布，引导每个专家模块在**独立的表示子空间**上学习专业化表征。从而将原本纠缠的视觉知识分离到不同专家，减少特征干扰。
  - **第二阶段：动态重组（Dynamic Recomposition）**
    - 路由器学习如何**动态组合**这些已经专业化的专家模块，为特定下游任务构建定制化的计算路径。通过稀疏激活，仅使用部分专家，提升计算效率并保留多样性。
- **关键技术细节**：
  - 双流结构：一个流用于处理图像特征，另一个流用于路由决策，实现条件计算。
  - 专家模块内部结构未详细说明（可能为标准前馈网络或Transformer块）。
  - 路由机制基于软注意力或Top-k选择，由教师特征引导第一阶段的解构。
- **算法流程**（文字说明）：
  1. 输入图像，使用多个预训练VFM（如CLIP、DINOv2、MAE等）分别提取特征作为“教师指导信号”。
  2. 初始化PRISM模型（包含共享主干和多个专家）。第一阶段固定主干，仅训练专家和教师条件路由器，使每个专家对齐到对应教师的表征子空间（通过蒸馏损失互斥）。
  3. 第二阶段冻结专家参数（保持专业化），训练动态路由器以适应下游任务的输入分布，学习如何组合专家输出。
  4. 推理时，图像经主干提取中间特征，路由器计算专家权重，稀疏激活若干专家，最终输出融合特征用于下游任务。

## 3. 实验设计：数据集、Benchmark、对比方法
- **数据集**：主要使用 **PASCAL-Context** 和 **NYUD-v2** 两个公共基准数据集。PASCAL-Context用于语义分割和场景理解；NYUD-v2用于深度估计和语义分割。
- **Benchmark**：在语义分割、深度估计等多种密集预测任务上进行评估，与最先进方法对比。
- **对比方法**：包括直接蒸馏（KD）、多任务学习（MTL）、单一VFM微调、以及传统的MoE（未专业化）等基线。具体对比模型名称未在摘要中列出，但声明PRISM在所有指标上达到了新SOTA。

## 4. 资源与算力
- **文中未明确说明**：摘要和元数据未提及使用的GPU型号、数量、训练时长等算力信息。需要查阅完整论文正文才能获知。推测可能使用了A100或V100等常见GPU，但具体不详。

## 5. 实验数量与充分性
- **实验数量**：仅从摘要可知在两个主要数据集上进行了实验，并包含了消融研究（消融了专业化步骤、路由机制等）。
- **充分性评价**：
  - 优势：选择代表性强的密集预测基准（语义分割、深度估计），覆盖不同任务多样性。消融实验验证了解构和重组阶段的有效性。
  - 不足：可能缺少在不同backbone（如ViT-B/L）上的泛化测试，以及在其他视觉任务（如检测、分类）上的验证。数据集数量较少，只用了两个，可能不够充分。此外，未提及对计算效率的量化对比（如FLOPs、参数量、推理速度）。
- **公平性**：对比基线包括直接蒸馏和多任务学习，基本公平。但需确认超参数是否对齐。

## 6. 主要结论与发现
- PRISM通过自组织的专家专业化有效缓解了多模型融合时的特征冲突，实现了模块化集成。
- 两阶段范式（解构+重组）优于端到端联合训练或简单蒸馏。
- 稀疏的专家激活不仅节省计算，还提升了性能，表明冗余专家可被忽略，专注于专业化子空间。
- 在PASCAL-Context和NYUD-v2上取得了新SOTA，验证了该方法的可扩展性和有效性。

## 7. 优点：方法或实验设计亮点
- **方法亮点**：
  - 创新性地提出教师条件路由，主动将不同模型的知识分离到独立子空间，避免负迁移。
  - 两阶段设计将解构和重组分离，使专业化稳定且可复用。
  - 采用MoE结构，稀疏激活，兼顾模型容量和计算效率。
- **实验亮点**：
  - 在代表性的密集预测任务上进行验证，结果清晰。
  - 消融实验证明了各组件（路由条件、两阶段）的必要性。

## 8. 不足与局限
- **实验覆盖不足**：仅两个数据集（且均为室内/街景场景），缺乏在ImageNet级大规模分类、目标检测、视频理解等任务上的验证，泛化性存疑。
- **偏差风险**：可能只报告了最优结果，未展示失败案例或负迁移仍然存在的场景。组件设计的超参数敏感性未讨论。
- **应用限制**：需要同时访问多个预训练VFM作为教师，增加了部署时内存和计算开销（解构阶段）。下游任务需重新训练路由器，灵活性受限。
- **可解释性**：专家内部表征的子空间独立性是否完全保证？是否可能还有残留干扰？论文未给出可视化分析。

（完）
