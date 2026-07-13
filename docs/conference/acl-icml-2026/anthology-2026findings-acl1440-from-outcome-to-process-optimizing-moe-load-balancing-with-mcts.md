---
title: "From Outcome to Process: Optimizing MoE Load Balancing with MCTS"
title_zh: 从结果到过程：利用MCTS优化MoE负载均衡
authors: "Wenjun Ke, Hengyuan Xu, Ziyu Shang, Yao He, Jiahao Wang, Zijie Xu, Peng Wang, Yuhang Lou, Jiajun Liu"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.1440.pdf"
tags: ["query:moe-special"]
score: 8.0
evidence: 用蒙特卡洛树搜索优化MoE路由以实现负载均衡
tldr: 本文针对LoRA-MoE中专家利用不均、部分专家过载而多数闲置的问题，提出基于蒙特卡洛树搜索的逐层路由优化方法，从过程层面而非仅结果约束来平衡专家使用。通过MCTS搜索最优路由路径，有效防止负载逐层累积失衡。实验表明该方法能显著降低负载方差，提升模型性能与专家专业化程度。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1440/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 809, \"height\": 553, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1440/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1653, \"height\": 687, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1440/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 799, \"height\": 478, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1440/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 805, \"height\": 554, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1440/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 812, \"height\": 615, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1440/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 802, \"height\": 402, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1440/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 797, \"height\": 518, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1440/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 808, \"height\": 222, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1440/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 784, \"height\": 723, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1440/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1650, \"height\": 765, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1440/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 793, \"height\": 282, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1440/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1733, \"height\": 394, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1440/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 791, \"height\": 1002, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1440/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 827, \"height\": 457, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1440/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1550, \"height\": 671, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1440/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 749, \"height\": 411, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1440/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1200, \"height\": 383, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1440/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1226, \"height\": 1295, \"label\": \"Table\"}]"
motivation: LoRA-MoE中专家利用不均导致部分专家过载而多数闲置，现有平衡策略仅约束最终分布，忽视逐层路由累积失衡。
method: 提出基于蒙特卡洛树搜索的逐层路由优化方法，在每层选择专家时搜索全局最优路径以实现负载均衡。
result: 实验表明该方法显著降低专家负载方差，缓解了负载失衡问题，提升了模型性能。
conclusion: 从过程层面优化路由能有效改善MoE负载均衡，间接促进专家专业化。
---

## Abstract
Mixture of Experts (MoE) dynamically routes inputs to specialized expert networks, enabling large language models to scale capacity with low inference overhead. To further improve MoE’s parameter efficiency in resource-constrained scenarios, LoRA–MoE integrates LoRA for lightweight adaptation while preserving MoE’s specialization. Despite these benefits, the effectiveness of LoRA–MoE still hinges on balanced expert utilization, where certain experts dominate activations while most remain underutilized. Existing balancing strategies focus on constraining the final distribution of expert usage, but overlook the routing decisions made at each layer. As a result, imbalances gradually accumulate across the routing hierarchy. To address this challenge, we propose LayerMoE, a novel three-stage framework that leverages process-level rewards to guide balanced expert routing. Specifically, to overcome the limitation of focusing only on final losses and ignoring intermediate routing, we introduce Monte Carlo Tree Search (MCTS)-based sampling that decomposes outcome-level supervision into layer-wise reward signals, guiding expert choices throughout the routing process. For efficiency, we organize Transformer layers into groups, which constrain the search space of MCTS and keep exploration overhead tractable while retaining the hierarchical structure. Extensive experiments on representative datasets (e.g., ARC, RACE, OBQA) show that applying LayerMoE consistently improves the performance of state-of-the-art LoRA-MoE baselines, yielding an average accuracy gain of 1.39%. Notably, the maximum improvement reaches 2.50%.

---

## 论文详细总结（自动生成）

# 论文中文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **问题**：LoRA-MoE 模型面临严重的专家利用不均（expert collapse）现象——少数专家被频繁激活，多数专家闲置，导致参数效率低下。现有平衡策略（如局部平衡约束、分布匹配）只关注最终分布（outcome-level），忽视逐层路由决策的累积效应。
- **动机**：类比强化学习中从结果奖励模型（ORM）到过程奖励模型（PRM）的转变，本文提出将 MoE 路由视为逐层决策过程，在每层引入过程级奖励信号，防止负载失衡逐层积累。
- **意义**：通过过程级优化路由，实现更均衡的专家利用，提升 LoRA-MoE 性能与可解释性。

## 2. 方法论：核心思想、关键技术细节

- **核心思想**：利用蒙特卡洛树搜索（MCTS）将专家选择建模为序列决策过程，MCTS 通过选择、扩展、模拟、反向传播四个步骤探索路由空间，收集层级的奖励统计，并与原始门控分数融合，形成奖励正则化的门控机制。
- **三阶段框架（LayerMoE）**：
  1. **分组层实例化**：将 Transformer 层划分为非重叠组（group），每个组视为一个决策步，组内共享路由决策。组内专家聚合为宏专家（macro-expert），降低 MCTS 搜索复杂度。
  2. **MCTS 专家采样**：在每个组，根据 UCB 准则选择专家，扩展子节点，模拟完整路由路径，计算奖励（基于训练损失，设置阈值 γ 防止早期过大损失主导），反向传播更新 Q 值、访问次数等统计。
  3. **MCTS 引导的 LoRA-MoE 训练**：将 MCTS 统计量（UCB 分数）与原始门控分数加权融合（权重 λ），形成最终门控分数，用于前向传播和损失计算，更新模型参数。
- **关键公式**：
  - UCB 选择：\( a_t = \arg\max_a \left[ Q(h_{t-1},a) + w \sqrt{\frac{\ln N(h_{t-1})}{N(h_{t-1},a)}} \right] \)
  - 奖励：\( R_i = 0 \) 若损失 > γ，否则 \( R_i = -\text{loss}_i \)
  - Q 值更新：\( Q(h_t,a) \leftarrow Q(h_{t-1},a) + \delta R_i \)（δ 为平滑因子）
  - 门控融合：\( \tilde{g}_{lj}(x_i) = \lambda g_{lj}(x_i) + (1-\lambda) \text{UCB}_{lj} \)

## 3. 实验设计

- **数据集与场景**：8 个数据集覆盖 5 个域：
  - 语言理解与推理：ARC-Challenge、ARC-Easy
  - 阅读理解：RACE-middle、RACE-high
  - 代码生成：HumanEval
  - 闭卷问答：OBQA、BoolQ
  - 数学推理：GSM8K
- **Benchmark**：在 LLaMA3.2-1B 和 LLaMA3-8B 两个基座模型上进行监督微调（SFT）。
- **对比方法**：HydraLoRA、LoRAMoE、MoSLoRA、MixLoRA、MoLA、GMoE 等六种当前最优的 MoE 风格 LoRA 微调方法。

## 4. 资源与算力

- **硬件**：所有实验在 1 块 L20 (48GB) GPU 上进行。
- **训练时长**：附录给出具体时间（如 LLaMA3-8B 在 GSM8K 上 LayerMoE 约 4h56m，Base 约 4h41m；ARC-E 上 6h04m vs 5h47m）。总体计算开销略有增加，但可接受。
- **模型规模**：实验限于 1B 和 8B 参数模型，未在更大模型（如 70B）上验证。

## 5. 实验数量与充分性

- **主要结果**（表1）：在 8 个数据集上对比 6 种基线 × 2 种基座模型，共约 96 组实验，显示 LayerMoE 平均提升 1.39%，最大 2.50%。
- **消融实验**：
  - 不同采样大小（batch size 2~32）：MCTS 持续优于基线，且随 batch size 增大提升更明显。
  - 不同探索参数 w（0.1~2.5）：w=1.4 最佳，过大/过小均降低性能。
  - 不同组大小 s（2/4/8/16）：s=4 在精度与效率间取得最佳权衡。
  - 不同专家数量 E（2~10）：专家增多提升性能，但边际递减。
- **案例研究**：静态参数分析（专家权重范数、多样性、平衡性）和动态推理分析（激活热图），定量展示 MCTS 提升专家多样性和负载均衡。
- **补充实验**：附录中在 Qwen3-0.6B 和 Qwen3-4B 上验证了架构无关性；与随机专家重分配、无辅助损失负载均衡等简单基线对比，MCTS 效果更优。
- **充分性评估**：实验设计较全面，覆盖多种任务、基座、基线和消融变量，对比公平（使用相同设置）。但缺乏在更大规模模型上的验证，可能影响泛化性结论。

## 6. 主要结论与发现

- LayerMoE 在所有测试数据集和基座上一致提升 LoRA-MoE 性能，平均准确率提升 1.39%，最大达 2.50%。
- 更弱的基座（1B）和更复杂的推理任务（如 RACE-m、HumanEval、GSM8K）受益更明显。
- MCTS 引导的路由显著提高专家多样性（最多 +48.89% 在 GSM8K）和负载均衡，同时专家权重范数轻微下降（隐式正则化）。
- 过程级优化比结果级约束更有效，能防止负载失衡逐层累积。

## 7. 优点

- **方法论创新**：首次将 MCTS 引入 MoE 路由优化，实现从 outcome-level 到 process-level 的范式转换。
- **高效可行**：通过分组策略大幅降低搜索空间，MCTS 额外开销仅占总训练时间的约 6%（见附录）。
- **可解释性**：MCTS 提供层级路由路径和统计量，使专家选择过程更透明。
- **广泛验证**：在多个域、多种基线和基座上验证，消融实验充分，结果一致。
- **鲁棒性**：对不同超参数（采样大小、探索参数、组大小、专家数）敏感度合理。

## 8. 不足与局限

- **模型规模局限**：仅实验 1B 和 8B 模型，未在更大模型（如 LLaMA-70B、Mixtral-12x7B）上验证，可扩展性未知。
- **计算开销**：虽然相对较小，但 MCTS 采样仍引入额外计算，可能限制在实时或资源极度受限场景的部署。
- **超参数依赖**：性能对探索参数 w、组大小 s、融合系数 λ 等敏感，需要调参。
- **任务覆盖**：虽含多域，但缺少真实世界长文本、多模态或对话任务评估。
- **泛化偏差风险**：实验中基座均为 LLaMA/Qwen 系列，可能无法完全推广到其他架构。
- **路由动态分析仅限于静态参数和少量案例**，缺乏大规模、多轮对话下的动态行为分析。

（完）
