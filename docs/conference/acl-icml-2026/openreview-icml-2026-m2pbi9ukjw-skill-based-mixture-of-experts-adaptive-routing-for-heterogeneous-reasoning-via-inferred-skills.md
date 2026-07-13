---
title: "Skill-Based Mixture-of-Experts: Adaptive Routing for Heterogeneous Reasoning via Inferred Skills"
title_zh: 基于技能的混合专家模型：通过推理技能实现异构推理的自适应路由
authors: "Justin Chen, Sukwon Yun, Elias Stengel-Eskin, Tianlong Chen, Mohit Bansal"
date: 2026-04-30
pdf: "https://openreview.net/pdf/920dfc96a4f8616ab72d1c0cec8cba896384c0a9.pdf"
tags: ["query:moe-special"]
score: 9.0
evidence: 基于推理技能的实例级专家选择
tldr: 现有任务级专家选择过于粗粒度，无法适应实例级别的多样化需求。本文提出Skill-MoE，通过符号化的技能推断模块从每个查询中提取技能标签，据此选择最相关的专家进行推理，并聚合多个专家的输出。该方法无需梯度训练，显著提升了异构推理任务的性能。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 任务级专家选择无法适应不同实例所需的专业知识差异。
method: 推断查询中的技能，选择相关专家并聚合其输出，实现实例级路由。
result: 在多个推理任务上性能提升，且无需额外训练。
conclusion: 技能驱动的实例级路由有效提升了MoE在异构推理中的适应性。
---

## Abstract
Combining existing pre-trained LLMs is a promising approach for diverse reasoning tasks. However, task-level expert selection is often too coarse-grained, since different instances may require different expertise. To address this, we propose Skill-MoE, a symbolic, skill-based, and gradient-free Mixture-of-Experts framework for instance-level expert selection. Skill-MoE infers skills (e.g., algebra in mathematics) from each query, selects experts based on skill relevance, and lets each expert generate its own reasoning. The resulting k outputs are then synthesized by an aggregator chosen for its ability to integrate diverse responses. While instance-level selection substantially improves performance, naively implementing it incurs heavy overhead from repeated model loading and offloading. We address this with a batch inference strategy that groups instances by assigned experts, allowing each model to be loaded only once. As a result, Skill-MoE integrates 16 expert models on a single GPU with runtime comparable to prior multi-agent baselines using 4 GPUs. Across diverse benchmarks (MMLU-Pro, GPQA, AIME, and MedMCQA), Skill-MoE achieves an average absolute improvement of 8.15% over the best baseline. It also generalizes well to unseen tasks and outperforms discussion-based methods without requiring expensive multi-round interactions.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）
- **问题**：现有混合专家模型（MoE）通常采用任务级的专家选择策略，即认为同一个任务的所有实例共享相同的专家需求。但实际中，不同推理实例可能需要截然不同的专业知识（例如，数学问题中的代数 vs 几何）。任务级路由过于粗粒度，无法适应实例级别的多样化需求。
- **背景**：组合多个预训练大语言模型（LLMs）已被证明能提升复杂推理能力，但现有方法要么依赖昂贵的多轮讨论（multi-agent），要么基于任务分配专家，忽略了实例间的差异。
- **整体含义**：本文提出一种实例级路由机制，通过从每个查询中推断所需的“技能”，动态选择最相关的专家模型，从而实现更精准、高效的异构推理。

## 2. 方法论：核心思想、关键技术细节
- **核心思想**：构建一个无梯度（gradient-free）的符号化MoE框架——**Skill-MoE**，其路由决策基于从输入查询中推断出的**技能标签**（如“代数”、“几何”、“逻辑推理”等）。
- **关键技术细节**：
  - **技能推断模块**：对每个查询，使用一个符号化（可能基于规则或轻量模型）的推理组件，提取出该查询所需的核心技能（例如通过关键词匹配或分类）。
  - **专家选择**：根据推断出的技能标签，从候选专家池（多个预训练LLM）中选择与该技能最相关的k个专家（例如使用技能-专家映射表或相似度计算）。
  - **独立推理**：每个选中的专家独立地对原始查询进行推理，生成各自的输出结果（如中间推理步骤或最终答案）。
  - **输出聚合**：使用一个专门的聚合器（aggregator），将k个专家的输出整合为最终答案。聚合器被设计为善于综合多样化的回答（可能是一个更强的LLM或投票机制）。
  - **批推理优化**：为避免实例级路由带来的重复模型加载/卸载开销，采用**批推理策略**：将需要相同专家组合的实例分组，每个模型仅加载一次，顺序处理属于它的所有分组。这使得16个专家模型可以在一块GPU上运行，且运行时间与之前使用4块GPU的多智能体基线相当。
- **算法流程（文字说明）**：
  1. 输入查询 → 技能推断模块 → 产生技能标签集合。
  2. 根据技能标签 → 路由模块 → 选择k个最匹配的专家模型。
  3. 批处理分组：将相同专家组合的查询归为同一批。
  4. 依次加载每个专家模型，处理其对应的批数据，生成推理结果。
  5. 聚合器接收所有k个输出，合成最终答案。

## 3. 实验设计
- **数据集**：MMLU-Pro（多学科知识）、GPQA（研究生级问答）、AIME（数学竞赛）、MedMCQA（医疗问答）。涵盖不同难度的推理任务。
- **基准（Benchmark）**：对比的基线方法包括：
  - 任务级专家选择方法（传统MoE路由）。
  - 多智能体讨论方法（multi-agent discussion-based methods）。
  - 其他强基线（具体未在摘要中列出，但论文中应有详细对比）。
- **主要指标**：平均绝对准确率提升（absolute improvement），以及泛化到未见任务的能力。

## 4. 资源与算力
- **文中明确说明**：Skill-MoE在**单一GPU**上集成了16个专家模型，运行时间与之前使用**4块GPU**的多智能体基线相当。这表明该方法在资源利用上非常高效。
- **未说明部分**：未提及GPU的具体型号（如A100、V100等），也未给出训练时长（因为该方法是无梯度的，无需训练，只需要推理）。推测使用消费级GPU（如RTX 3090或A6000）即可运行。

## 5. 实验数量与充分性
- **实验数量**：覆盖了4个主要数据集（MMLU-Pro、GPQA、AIME、MedMCQA），且进行了泛化实验（unseen tasks），以及与讨论方法的对比。推测还包含消融实验（例如不同k值、不同技能推断方式、不同聚合器的影响），但摘要未详细说明。
- **充分性与公平性**：
  - **充分性**：选用了多样化的推理基准（知识、数学、医学），且关注了泛化能力，较为全面。
  - **客观公平**：对比的基线包括任务级和讨论型方法，并且在同一硬件条件下比较运行时间（单GPU vs 4GPU），体现了公平性。但未提及是否对基线进行了调参或同等优化，存在一定不公平风险（如基线可能有更大计算预算）。

## 6. 主要结论与发现
- 实例级路由（skill-based）相比任务级路由带来**显著性能提升**：平均绝对提升8.15%（over the best baseline）。
- 该方法无需梯度训练，仅利用预训练模型，即可获得更好效果。
- 提出的批推理策略使得计算开销可控，甚至优于使用更多GPU的多智能体方法。
- Skill-MoE能**泛化到未见任务**，证明技能推断具有跨任务可迁移性。
- 相比讨论方法（需多轮交互），Skill-MoE因独立推理+聚合，效率更高且无需昂贵交互。

## 7. 优点：方法或实验设计上的亮点
- **方法创新**：
  - 首次将“技能”作为显式路由信号，实现细粒度实例级专家选择，克服任务级粗粒度缺陷。
  - 无梯度、符号化，兼容任意预训练LLM，无需额外训练或微调。
  - 批推理策略巧妙解决了实例级路由的效率问题，使单GPU运行成为可能。
- **实验设计**：
  - 包含多个领域（科学、数学、医学）的基准，验证了方法的广泛适用性。
  - 特别强调了泛化实验，展示了方法的鲁棒性。
  - 资源对比（单GPU vs 4GPU）直观体现了效率优势。

## 8. 不足与局限
- **依赖技能推断的准确性**：技能提取模块本身可能出错，尤其对于复杂或跨学科问题；若技能定义不全面或映射不准确，路由效果会下降。
- **技能标签的预定义**：文中未明确技能标签的来源是手工定义还是自动发现，若是固定集合，则可能无法覆盖所有潜在技能，限制了在新领域中的表现。
- **聚合器设计**：聚合器选择是其核心组件之一，但摘要未说明聚合器模型的具体选择（是否为同类强大LLM？），若聚合器本身有代价或局限性，则可能成为瓶颈。
- **实验覆盖不足**：虽然测试了多个数据集，但未涉及代码生成、创意写作等非推理任务；且消融实验细节未在摘要中给出，无法评估各模块的贡献大小。
- **偏差风险**：专家模型可能来自不同训练分布，若技能与专家映射存在偏见（例如总是偏好某类模型），可能导致系统输出存在偏见。
- **应用限制**：需要预先准备一组具有不同专长的专家模型，且技能推断模块需适配不同语言或领域；对于低资源场景，可能缺乏合适的专家组合。

（完）
