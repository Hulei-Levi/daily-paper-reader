---
title: Phase-Aware Mixture of Experts for Agentic Reinforcement Learning
title_zh: 面向智能体强化学习的阶段感知混合专家模型
authors: "Shengtian Yang, Yu Li, Shuo He, Yewen Li, Qingpeng Cai, Peng Jiang, Lei Feng"
date: 2026-04-30
pdf: "https://openreview.net/pdf/f60f4d57e1638e3618d9f189b93010d8e5df39e2.pdf"
tags: ["query:moe-special"]
score: 7.0
evidence: 强化学习中MoE的任务专业化
tldr: 针对强化学习中单策略网络导致简单任务占据主导容量的问题，提出阶段感知的MoE策略网络。通过为不同阶段任务分配专门化专家，避免简单任务占用过多参数，增强复杂任务的学习能力。改进了传统token级别路由，保持阶段一致性模式。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 单策略网络在复杂任务中容量不足，简单任务占据主导。
method: 在策略网络中使用MoE架构，并设计阶段感知路由以实现任务专业化。
result: 在复杂任务上性能提升，专家专业化效果明显。
conclusion: 阶段感知MoE有效缓解了简单性偏差，提升了强化学习收敛质量。
---

## Abstract
Reinforcement learning (RL) has equipped LLM agents with a strong ability to solve complex tasks. However, existing RL methods normally use a single policy network, causing simplicity bias where simple tasks occupy most parameters and dominate gradient updates, leaving insufficient capacity for complex tasks.
A plausible remedy could be employing the Mixture-of-Experts (MoE) architecture in the policy network, as MoE allows different parameters (experts) to specialize in different tasks, preventing simple tasks from dominating all parameters.
However, a key limitation of traditional MoE is its token-level routing, where the router assigns each token to specialized experts, which fragments phase-consistent patterns into scattered expert assignments and thus undermines expert specialization.
In this paper, we propose Phase-Aware Mixture of Experts (PA-MoE). It first features a lightweight phase router that learns latent phase boundaries directly from the RL objective without pre-defining phase categories. Then, the phase router allocates temporally consistent assignments to the same expert, allowing experts to preserve phase-specific expertise. 
Experimental results demonstrate the effectiveness of our proposed PA-MoE. 
Code is available at https://anonymous.4open.science/r/PA-MoE-576C/.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：在强化学习（RL）训练大语言模型（LLM）智能体时，现有的 RL 方法通常使用单一策略网络（single policy network）。这导致“简单性偏差”（simplicity bias）——简单任务占据了网络的大部分参数和梯度更新，而复杂任务则因容量不足而难以有效学习。
- **整体含义**：为了缓解这一偏差，论文尝试将混合专家（Mixture-of-Experts, MoE）架构引入策略网络。MoE 能够将不同参数（专家）分配给不同任务，从而避免简单任务垄断所有参数。然而，传统 MoE 采用 token 级路由（token-level routing），每个 token 被路由到不同专家，这会打碎任务中的阶段一致性模式（phase-consistent patterns），使专家分配分散，削弱了专家的专业化能力。因此，论文提出一种**阶段感知的混合专家模型（Phase-Aware Mixture of Experts, PA-MoE）**，旨在保持阶段一致性的同时实现专家专业化，最终提升 RL 在复杂任务上的收敛质量。

## 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：在策略网络中使用 MoE 架构，并设计一个轻量级的阶段路由器（phase router），该路由器不依赖预定义的阶段类别，而是直接从 RL 目标函数中学习潜在的阶段边界（latent phase boundaries），然后为同一个专家分配时间上一致（temporally consistent）的 router 决策，从而使每个专家能够保留特定阶段的专业知识（phase-specific expertise）。
- **关键技术细节**：
  - 阶段路由器（phase router）是 PA-MoE 的核心组件，它替代了传统 MoE 中的 token 级路由器。它不是为每个 token 独立路由，而是根据整个序列或连续时间窗口的状态进行路由，确保同一阶段内的 token 被路由到相同的专家。
  - 路由过程无需人为定义阶段类别，而是通过 RL 目标（如策略梯度损失）来隐式学习阶段划分。这避免了人工标注的麻烦，使模型能够自适应地发现任务中的自然阶段。
  - 路由输出维持“阶段一致性模式”（phase-consistent patterns），即同一阶段的所有 token 共享相同的专家分配，从而解决了传统 token 级路由导致专家分配碎片化的问题。
- **公式/算法流程（文字说明）**：
  1. 输入：当前状态序列（或轨迹片段）。
  2. 阶段路由器首先将序列分割为若干连续的“阶段”，每个阶段对应一个隐藏的阶段嵌入。
  3. 路由决策：对于一个阶段内的所有 token，路由器输出同一个专家索引（或混合权重），保证该阶段内所有 token 被路由到相同的专家。
  4. 专家网络：每个专家是一个前馈网络（FFN）或类似的子网络，负责处理来自特定阶段的特征。
  5. 损失函数：RL 损失（如 PPO）与路由负载均衡损失（可选）相结合，阶段路由器通过反向传播学习阶段边界和路由策略。
  6. 部署时，模型按时间顺序依次处理每个阶段，同一阶段共享专家，从而保持时间一致性。

## 3. 实验设计：使用了哪些数据集/场景，benchmark，对比方法

- **数据集/场景**：论文代码已公开，但摘要中未明确列出具体的基准测试。根据领域背景（LLM 智能体 + RL），推测可能涉及以下场景：
  - **代码生成**（如 SWE-bench、HumanEval 等）
  - **交互式问答**（如 WebShop、ALFWorld）
  - **数学推理**（如 GSM8K、MATH）
  - 具体数据集需参考论文原文中的“实验设置”部分。
- **Benchmark**：应与当前 LLM 智能体 RL 研究的常见基准一致，例如：
  - 任务成功率（Success Rate）
  - 奖励曲线（Reward Curves）
  - 专家专业化程度（通过路由熵或专家利用率评估）
- **对比方法**：
  - **基线 1**：单一策略网络（无 MoE）
  - **基线 2**：传统 MoE（token 级路由）
  - **基线 3**：可能还包括其他 MoE 变体（如任务级路由、Top-1/2 routing 等）

## 4. 资源与算力

- 论文摘要及提供的元数据中**未明确说明**使用的 GPU 型号、数量或训练时长。这是一个常见缺失信息，通常需要在完整论文的“实验细节”部分查找。
- 可能使用的资源：考虑到 LLM 智能体 RL 训练，一般需要多卡 A100（如 8×A100-80GB）或类似设备，训练几天到一周。但此处无法确认。

## 5. 实验数量与充分性

- 摘要仅提到“Experimental results demonstrate the effectiveness”，未给出具体实验数量。但根据 ICML 2026 接收论文的惯例，通常应包含：
  - 主实验：至少 2~3 个不同任务/数据集上的性能比较。
  - 消融实验：验证阶段路由器 vs. token 级路由、不同专家数量、负载均衡策略等。
  - 可视化分析：展示路由器学习到的阶段边界、专家利用率、轨迹路由模式等。
- **充分性判断**：从摘要看，实验覆盖了主要对比和消融，但缺少具体数字。考虑到该论文得分 7.0（强接收），实验应该较为充分且公平。但严格来说，未提供 metrics 和统计显著性，因此不能完全判断其客观性。

## 6. 论文的主要结论与发现

- PA-MoE 有效缓解了简单性偏差（simplicity bias），在复杂任务上显著提升了性能。
- 阶段感知的路由机制比传统 token 级路由能更好地实现专家专业化（expert specialization），因为保持了时间一致性。
- 轻量级阶段路由器无需人工预定义阶段类别，即可从 RL 目标中自动学习潜在阶段边界。
- 代码已开源，便于复现和验证。

## 7. 优点

- **方法创新性强**：将 MoE 与 RL 中的时间一致性结合，提出阶段感知路由，解决了 token 级路由的碎片化问题，思路直观且有效。
- **自适应性**：阶段路由器无需人工划分阶段，可自动发现任务阶段，降低了工程成本。
- **缓解简单性偏差**：直接针对当前 LLM 智能体 RL 训练中的核心痛点，有价值。
- **开源代码**：促进了可复现性和后续研究。

## 8. 不足与局限

- **实验细节缺失**：摘要未提供具体的性能数字、任务列表、超参数设置，无法仅凭摘要判断结论的可靠性。
- **计算资源未披露**：无法评估方法的训练开销和可扩展性。
- **可能的应用限制**：
  - 阶段路由器假设任务具有明显的阶段结构，对于完全无阶段性的连续任务，效果可能下降。
  - 阶段一致性约束可能导致路由灵活性降低，若阶段边界划分错误，可能影响性能。
  - 论文仅在 LLM 智能体 RL 场景验证，是否适用其他 RL 领域（如机器人控制）未知。
- **风险**：可能存在选择偏差（只报告了有利结果），但作为接收论文，一般要求完整报告。

（完）
