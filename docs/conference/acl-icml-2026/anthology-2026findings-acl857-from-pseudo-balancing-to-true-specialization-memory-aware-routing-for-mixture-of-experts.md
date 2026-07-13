---
title: "From Pseudo-Balancing to True Specialization: Memory-Aware Routing for Mixture-of-Experts"
title_zh: 从伪平衡到真正专业化：混合专家的记忆感知路由
authors: "Peixuan Hou, Yunbo Hou, Bin Chen, Li He (何丽), Jian Xu, Weiping Li, Bo Zheng, Guojie Song"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.857.pdf"
tags: ["query:moe-special"]
score: 9.0
evidence: 解决伪平衡问题，通过记忆感知路由实现真正的专家专业化
tldr: 标准的混合专家模型（MoE）训练中，负载均衡策略会导致伪平衡现象，即相同输入在不同训练步骤中被随机路由到不同专家，造成知识重叠和表示冗余。本文提出记忆感知路由方法，通过引入专家内存机制，在路由时考虑历史分配信息，促进令牌与专家之间的语义对齐，从而从伪平衡走向真正的专家专业化。实验表明该方法有效提升了专家利用效率和模型性能，为MoE路由提供了新思路。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.857/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 805, \"height\": 608, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.857/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 794, \"height\": 485, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.857/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 804, \"height\": 281, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.857/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1474, \"height\": 369, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.857/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1662, \"height\": 670, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.857/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1653, \"height\": 477, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.857/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 804, \"height\": 340, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.857/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1663, \"height\": 710, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.857/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1002, \"height\": 690, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.857/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1666, \"height\": 624, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.857/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1491, \"height\": 408, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.857/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1663, \"height\": 657, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.857/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1662, \"height\": 651, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.857/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1644, \"height\": 827, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.857/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 793, \"height\": 288, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.857/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 795, \"height\": 288, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.857/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1643, \"height\": 991, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.857/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1309, \"height\": 232, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.857/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1649, \"height\": 192, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.857/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1650, \"height\": 236, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.857/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1215, \"height\": 218, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.857/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 924, \"height\": 532, \"label\": \"Table\"}]"
motivation: 现有MoE负载均衡策略导致伪平衡，专家知识重叠严重，需实现真正的语义对齐。
method: 设计记忆感知路由机制，在专家选择时结合历史路由信息，增强令牌与专家的匹配度。
result: 在语言建模任务上减少了专家冗余，提升了模型准确率和路由稳定性。
conclusion: 记忆感知路由可有效促进专家专业化，优于传统负载均衡方法。
---

## Abstract
Mixture-of-Experts (MoE) efficiently trains large models by using sparse activation to lower costs, selecting a few experts based on data characteristics. For MoE, an unbalanced expert load will lead to inefficient expert utilization and routing collapse. Existing methods commonly achieve an expert-centered balancing strategy to solve it, prioritizing equal utilization of experts over semantic alignment between tokens and experts. However, this can lead to a pseudo-balance phenomenon: To ensure expert load balancing, the same input is randomly routed to different experts across training steps instead of the most matching one. It introduces two critical issues: (1) Severe knowledge overlap among experts, resulting in redundant representations and inefficient parameter utilization. (2) Difficulty in forming and stabilizing expert specialization. These issues limit the scalability of models, especially large language models (LLM). To address these limitations, we introduce Memory-Aware Routing (MAR), a training-phase approach that enhances existing load-balancing strategies. By equipping each expert with a memory buffer, our method explicitly models their long-term preferences, allowing historical experience to guide routing. This ensures that tokens are routed more consistently to compatible experts, mitigating the pseudo-balance problem while maintaining global load balance and fostering expert specialization. Experimental results show that MAR improves expert specialization by 35% and downstream accuracy by 2%-25%, doubles parameter efficiency, and matches baseline performance with only half the experts.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：现有的混合专家模型（MoE）在训练中广泛采用专家中心的负载均衡策略（如辅助损失），虽然实现了专家使用率的均匀分布，但导致了 **“伪平衡”现象**——同一输入在不同训练步骤中被随机路由到不同专家，而非稳定地分配给语义最匹配的专家。这引发两个严重问题：
  - 专家间知识严重重叠，参数冗余，不利于模型扩展。
  - 专家难以形成稳定的专业化，路由不稳定，限制了大语言模型的性能与规模。
- **研究动机**：从伪平衡走向真正的专家专业化，在保持负载均衡的同时，实现令牌与专家之间语义对齐的稳定路由。
- **整体含义**：论文揭示了传统负载均衡策略的隐性代价，并提出了一个轻量级、即插即用的训练阶段方案，显著提升MoE的参数效率和下游性能，对大规模MoE模型训练具有重要指导意义。

## 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：为每个专家配备一个记忆缓冲区，记录其近期处理过的令牌表示，从而建模专家的长期偏好；在路由时引入“专家-令牌匹配分数”，让历史经验参与路由决策，促进令牌被一致地路由到最匹配的专家。
- **关键技术细节**：
  1. **记忆缓冲区**：每个专家 `i` 维护一个容量为 `N` 的 FIFO 队列 `B_i`，存储最近路由到该专家的令牌特征向量 `h`。
  2. **偏好向量**：通过平均缓冲区内所有特征得到专家的偏好向量 `d_i = (1/|B_i|) ∑ h`，反映该专家擅长处理的输入类型。
  3. **专家-令牌匹配分数**：计算输入令牌 `x` 与偏好向量 `d_i` 的余弦相似度 `s_match_i = cos(x, d_i)`。
  4. **融合路由分数**：将原始路由器分数 `s_base_i` 与匹配分数加权融合：`s_i = s_base_i + α·s_match_i`，其中 α 为超参数控制影响强度。
  5. **训练/推理分离**：MAR 仅在训练时启用，推理时恢复为标准 top-k 路由，避免额外开销。
  6. **高效实现**：更新偏好向量时采用增量计算（O(d) 复杂度），无需遍历整个缓冲区。

## 3. 实验设计

- **数据集**：
  - **预训练**：Penn Treebank (PTB)、WikiText-2、OpenWebText（用于大模型）
  - **下游微调**：PTB（语言建模）、MMLU（知识应用）、BBH（常识推理）、GSM8K / SVAMP（数学推理）
- **基准模型**：Mixtral-MoE、LLaMA-MoE、GPT2-MoE（3层和12层变体）、OLMoE 1B-7B
- **对比方法**：
  - 基线：标准负载均衡损失（LBL）
  - 其他负载均衡策略：Global Batch LBL (Qiu et al.)、Aux Free (Wang et al.)、Lo+Lv (Guo et al.)、SimBal (Omi et al.)、Shared Experts (DeepSeek-V2)
  - 自身消融：不同 α 值、不同缓冲大小、不同更新策略（FIFO vs. LRU vs. LFU vs. RAND）
- **评估指标**：困惑度（PPL）、关键专家依赖度（KED，越高表示专家专业化越强）、下游任务准确率

## 4. 资源与算力

- **硬件**：论文明确提到实验在 **5×RTX 4090** 和 **2×L20 GPUs** 上运行。
- **训练时长**：未给出具体训练时间，仅提及使用早期停止（patience=3 个 epoch）和梯度累积等常规技术。
- **说明**：算力描述较简略，缺乏对大规模实验（如12层GPT2-MoE）的总耗时统计。

## 5. 实验数量与充分性

- **实验数量**：相当充分，主要包括：
  - 3种基础架构 + 2种数据集 × 2种专家数（4/8）的预训练对比（共约12组主要结果）
  - 12层GPT2-MoE在 OpenWebText 上的扩展实验（2组）
  - 多种专家数（4/8/16）的缩放实验
  - 与5种负载均衡策略的兼容性实验（4种架构 × 2数据集 × 3-4种策略，约20+组）
  - 下游微调实验（5个任务）
  - 消融实验：α（5个值）、缓冲大小（3个值）、更新策略（4种）、匹配度量选择
- **充分性与公平性**：实验设计较为全面，覆盖了不同规模、不同架构、不同训练阶段。对比实验中保持超参数一致，仅切换路由策略，结论可信。但未涉及多任务学习、跨模态或更大规模（如百亿参数）模型的验证，可视为初步充分。

## 6. 论文的主要结论与发现

1. **伪平衡现象确实存在**：定量实验表明，负载均衡模型的路由一致性比无负载均衡模型下降68%，且路由熵和专家切换率随负载均衡强度增大而显著增加。
2. **MAR 有效缓解伪平衡**：MAR 使路由更加稳定，专家选择在训练后期几乎不再切换。
3. **性能大幅提升**：
   - 专家专业化程度（KED）平均提升 **35%**
   - 下游任务准确率提升 **2% ~ 25%**（数学推理任务提升最显著）
   - 参数效率提升：仅用 **一半专家**（参数减少25%）即可达到基线性能
   - 收敛速度加快约 **20%**
4. **与现有负载均衡策略兼容**：将 MAR 应用于 Global Batch、Aux Free、Lo+Lv、SimBal、Shared Experts 等策略后，均有额外收益。
5. **推理零开销**：MAR 仅在训练阶段生效，不增加推理时的计算和内存负担。

## 7. 优点

- **方法新颖且简洁**：首次系统揭示伪平衡问题，并提出记忆缓冲区这一直觉直观且实现简单的解决方案。
- **即插即用**：可直接增强现有 MoE 训练流程，无需改动模型核心结构。
- **推理友好**：训练结束后完全去除额外组件，不增加部署成本。
- **实验全面**：覆盖多种架构、数据集、任务类型，消融分析细致，对比基线丰富。
- **高效实现**：FIFO 更新和增量平均保证了 O(d) 复杂度，实际开销极小（峰值内存增加仅0.3GB，路由延迟增加0.8ms）。

## 8. 不足与局限

- **额外超参数引入**：记忆缓冲大小 `N` 和融合系数 `α` 需要针对不同模型/数据集进行调优，论文仅在单一设置下探索最优值，缺乏跨场景的鲁棒性验证。
- **静态偏好假设**：MAR 假设专家偏好相对稳定，在数据分布剧烈变化（如领域持续迁移、多任务混合训练）时，历史记忆可能过时，导致路由适应变慢。
- **可扩展性疑虑**：虽然论文声称扩展到大量专家集时内存维护成本可控，但实际实验中专家数最高仅16，未验证数百或数千专家的极端场景。
- **缺乏理论分析**：未对 MAR 为何能提升专业化的梯度机制提供严格的数学证成，仅做了直观解释。
- **应用范围局限**：仅测试了语言建模和推理类任务，未涉及图像、多模态、代码生成等常见 MoE 应用领域。

（完）
