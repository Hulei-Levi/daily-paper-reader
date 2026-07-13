---
title: "Alloc-MoE: Budget-Aware Expert Activation Allocation for Efficient Mixture-of-Experts Inference"
title_zh: Alloc-MoE：预算感知的专家激活分配用于高效混合专家推理
authors: "Baihui Liu, Kaiyuan Tian, Wei Wang, Zhaoning Zhang, Linbo Qiao, Dongsheng Li"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-long.437.pdf"
tags: ["query:moe-special"]
score: 6.0
evidence: 提出预算感知的专家激活分配用于MoE推理
tldr: 针对MoE推理时专家激活导致的延迟瓶颈，提出Alloc-MoE框架，通过联合优化层和令牌级别的激活预算，在减少激活数的同时最小化性能损失。实验表明在多种模型上保持高准确率。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.437/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 807, \"height\": 421, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.437/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1563, \"height\": 763, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.437/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1657, \"height\": 534, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.437/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1657, \"height\": 536, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.437/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 803, \"height\": 390, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.437/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1648, \"height\": 495, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.437/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 800, \"height\": 469, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.437/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 802, \"height\": 468, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.437/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1660, \"height\": 976, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.437/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1659, \"height\": 978, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.437/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1661, \"height\": 978, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.437/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1449, \"height\": 488, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.437/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 719, \"height\": 289, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.437/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 720, \"height\": 422, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.437/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 765, \"height\": 287, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.437/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 758, \"height\": 336, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.437/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 721, \"height\": 339, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.437/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 722, \"height\": 513, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.437/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 719, \"height\": 343, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.437/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 720, \"height\": 344, \"label\": \"Table\"}]"
motivation: 减少专家激活会严重损害模型性能。
method: 提出统一的预算分配框架，协同优化层和令牌级激活。
result: 在多个MoE模型上，Alloc-MoE在减少激活时性能损失小于基线。
conclusion: 合理的预算分配能有效平衡推理效率与性能。
---

## Abstract
Mixture-of-Experts (MoE) has become a dominant architecture for scaling large language models due to their sparse activation mechanism. However, the substantial number of expert activations creates a critical latency bottleneck during inference, especially in resource-constrained deployment scenarios. Existing approaches that reduce expert activations potentially lead to severe model performance degradation. In this work, we introduce the concept of activation budget as a constraint on the number of expert activations and propose Alloc-MoE, a unified framework that optimizes budget allocation coordinately at both the layer and token levels to minimize performance degradation. At the layer level, we introduce Alloc-L, which leverages sensitivity profiling and dynamic programming to determine the optimal allocation of expert activations across layers. At the token level, we propose Alloc-T, which dynamically redistributes activations based on routing scores, optimizing budget allocation without increasing latency. Extensive experiments across multiple MoE models demonstrate that Alloc-MoE maintains model performance under a constrained activation budget. Especially, Alloc-MoE achieves 1.15× prefill and 1.34× decode speedups on DeepSeek-V2-Lite at half of the original budget.

---

## 论文详细总结（自动生成）

# 论文《Alloc-MoE: Budget-Aware Expert Activation Allocation for Efficient Mixture-of-Experts Inference》中文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **背景**：混合专家模型（Mixture-of-Experts, MoE）通过稀疏激活机制（Top-K路由）大幅扩展模型容量，已成为大语言模型的主流架构。然而，在推理过程中，大量专家激活（每个 token 激活多个专家）导致显著的计算与通信延迟，尤其在资源受限的部署场景下成为瓶颈。
- **问题**：现有减少专家激活的方法（如固定降低 Top-K、层或令牌级别的自适应剪枝）虽然能加速推理，但往往严重损害模型性能。例如，将 DeepSeek-V2-Lite 的每 token 专家数从 6 降至 3 会导致 17% 的性能下降，降至 2 时性能下降近 40%。
- **研究意义**：如何在减少专家激活的同时最小化性能损失，即实现推理效率与模型质量的帕累托最优，是 MoE 推理优化中的关键挑战。

## 2. 方法论：核心思想、关键技术细节

### 核心思想
- 引入 **激活预算（Activation Budget）** 概念：将每 token 在所有 MoE 层中激活的专家总数定义为全局预算，下放到每个层得到层预算。在固定全局预算下，通过联合优化层间分配和令牌间再分配，最小化性能损失。
- 提出 **Alloc-MoE** 统一框架，包含两个组成部分：
  - **Alloc-L（层级别）**：利用敏感性分析和动态规划确定每层最优的专家激活数。
  - **Alloc-T（令牌级别）**：基于路由分数动态地在令牌间重新分配激活，而不增加延迟。

### 关键技术细节

#### Alloc-L：层级别预算分配
1. **层敏感性分析**：采用隔离分配策略（Allocation-Isolating Profiling）逐层测量性能受激活数变化的影响。具体地，对目标层 i，将其 Top-K 从原始值逐步降至 1，同时固定所有更深层为最小激活（Top-K=1），保持前面层为原始值。用困惑度（PPL）作为指标，构建全局敏感性矩阵 \( S \in \mathbb{R}^{L \times K_{\text{orig}}} \)，每行表示该层在不同预算下的相对损失。
2. **优化问题**：选择每层预算 \( K_i \)（1 ≤ Ki ≤ Korig）使总敏感度最小化，受限于全局预算 \( B \)。
   \[
   \arg\min \sum_{i=0}^{L-1} S[i, K_i] \quad \text{s.t.} \quad \sum_i K_i \le B, \quad 1 \le K_i \le K_{\text{orig}}
   \]
3. **求解**：转化为分组背包问题，使用动态规划（DP）精确求解，复杂度 \( O(L \cdot B \cdot K_{\text{orig}}) \)。DP 状态 \( DP[i,b] \) 表示前 i 层使用预算 b 的最小累计敏感度，转移方程为：
   \[
   DP[i,b] = \min_{k \le b} (DP[i-1,b-k] + S[i,k])
   \]
   通过回溯得到最优分配 \( \mathbf{K}^* \)。

#### Alloc-T：令牌级别自适应再分配
1. **目标**：在给定层预算 \( K_l \) 下，将专家激活在令牌间重新分配，最大化总路由分数（即最高优先分配给路由分布最不集中的令牌）。
2. **形式化**：构建令牌-专家候选集 \( C_l = \{(t,e) \mid e \in \text{Top-K}(w_t)\} \)，选择子集满足：
   - 总激活数 ≤ \( T \times K_l \)（T 为令牌数）
   - 每个令牌至少激活 \( K_{\text{base}} \) 个专家（防止某些令牌无激活）
   - 最大化所选路由分数之和
3. **高效实现**：先保留每个令牌的 Top-\( K_{\text{base}} \) 专家，然后收集剩余候选分数，全局选择得分最高的 \( (K_l - K_{\text{base}}) \times T \) 个激活。此操作仅涉及 masking 和全局 top-selection，不增加推理延迟。标准 Top-K 是 \( K_{\text{base}}=K_l \) 的特例。

## 3. 实验设计

### 使用的模型
- **DeepSeek-V2-Lite**（26层 MoE，6/64 激活专家，2.4B/15.7B 参数）
- **Qwen1.5-MoE-A2.7B**（24层，4/60 激活，2.7B/14.3B 参数）
- **OLMoE-1B-7B-0924**（16层，8/64 激活，1.0B/7.0B 参数）

### 预算设置
- DeepSeek: 全局预算 52, 78, 104, 130（对应平均每层 2,3,4,5 专家，原始为 6）
- Qwen: 48, 60, 72, 84（对应 2,2.5,3,3.5，原始为 4）
- OLMoE: 64, 80, 96, 112（对应 4,5,6,7，原始为 8）

### 数据集与任务
- **校准数据集**：WikiText-2（主要），还验证了 C4 和 Pile 的鲁棒性。
- **评估基准**：20个数据集，分为三大类：
  - NLU：BoolQ、LAMBADA、RACE、SciQ、MNLI、QNLI、RTE
  - 推理：ARC-E、ARC-C、HellaSwag、LogiQA、MMLU、PIQA、TruthfulQA、ACP、BBH、GroundedCocoa、SWAG
  - 数学：GSM8K、ASDiv、MathQA
- **指标**：准确率（大多数），GSM8K/ACP/BBH 为 Exact Match。

### 对比方法
- **层级别基线**：Uniform（均匀分配）、LExI（层自适应剪枝）、Ascending（递增分配）、Descending（递减分配）
- **令牌级别基线**：Dynamic-MoE（自适应 Top-P 路由）、NAEE（动态专家跳过，仅 Top-2 扩展至 Top-K）
- **评估框架**：lm-eval + vllm 后端，在单张 NVIDIA H100 80GB GPU 上进行。

### 实验数量与充分性
- 在3个模型、4个预算水平下进行主要实验，每个模型报告三个任务组的平均准确率（总共约 3×4×3=36 个主结果）。
- 消融实验：
  - Alloc-L 与 Ascend/Descend/LExI/Uniform 对比（3模型×4预算×3任务 = 36组）
  - Alloc-T 与 Dynamic-MoE/NAEE 对比（同上）
  - 联合消融（+L、+T、+L+T）对比（3模型×4预算，平均指标）
  - Kbase 敏感性分析（在 Uniform 分配下调整 Kbase 值）
  - 校准数据集鲁棒性（WikiText2、C4、Pile 对比）
  - 专家负载平衡分析（Spearman 秩相关、熵差、JS散度）
  - 推理效率实验（prefill/decode 速度提升）
  - 层分配与令牌-熵关系可视化
- 实验覆盖多种模型、任务和预算范围，消融充分，基线设定合理（包括层和令牌两个维度的基线），结论具有统计可靠性。

## 4. 资源与算力

- 文中明确说明所有实验在 **单张 NVIDIA H100 80GB GPU** 上运行。
- 未提及训练时长或总 GPU 小时数。由于 Alloc-MoE 是后训练优化（仅需少量校准数据和短时间敏感性分析），推测资源需求不高。但论文未提供具体耗时数据，这是细节上的不足。

## 5. 实验数量与充分性

- **数量**：覆盖3种MoE架构、4个预算水平、20个下游任务、多种基线对比、详尽的消融分析。
- **充分性**：实验设计考虑了层和令牌两个维度的正交性，分别验证每个组件的贡献，并分析超参数（Kbase）、校准数据集、负载均衡等细节。结论有充分证据支撑（如联合消融表显示+L+T平均性能最高）。
- **公平性**：所有基线在相同预算下比较，推理效率实验用相同输入配置，校准数据集使用相同 token。然而，一些基线（如 LExI）本身也是后训练方法，但原文未重复训练；对比时可能忽略了某些方法需要额外训练（如 Dynamic-MoE 需训练时正则化），但论文采用了校准后的阈值模拟，总体上公平。

## 6. 主要结论与发现

- Alloc-MoE 在 12 个评估设置中的 10 个上优于所有基线，尤其在严格预算和复杂任务（数学）上优势明显（平均提升 2.15%）。
- 联合层和令牌优化比单独使用任何一者效果更好，证明两个维度正交互补。
- 在 DeepSeek-V2-Lite 上，当预算减半时，Alloc-MoE 实现 1.15× prefill 加速和 1.34× decode 加速，同时保持与原始模型相近的性能（而简单均匀减少会导致 17% 性能下降）。
- 专家负载均衡性保持良好（Spearman 秩相关>0.93，JS 散度<0.014），说明 Alloc-MoE 未破坏专家专业化模式。
- 最佳 Kbase 为 1（即每令牌至少保留 1 个专家），过大的 Kbase 会限制再分配空间。

## 7. 优点

- **创新性**：首次形式化激活预算概念，并提出联合层-令牌两阶段优化，不同于以往单一层面的工作。
- **高效性**：Alloc-L 使用 DP 求解精确解，复杂度低；Alloc-T 仅需简单 masking 和全局选择，不增加推理延迟。整体为后训练方法，无需重新训练模型。
- **通用性**：在三种不同架构、不同参数量和 Top-K 设置的模型上均有效，且对校准数据集不敏感。
- **解释性**：通过敏感性矩阵和熵分析，提供了层间和令牌间分配的可解释性（如深层保留更少专家、高熵令牌获得更多专家）。
- **实验严谨**：涵盖多个任务类型、多个基线、超参数枚举、可视化分析，消融实验完整。

## 8. 不足与局限

- **硬件因素缺失**：方法未考虑专家在分布式系统中的物理放置和通信开销，其实际加速可能受硬件拓扑影响（文中明确提及）。
- **未与其它效率方法结合**：Alloc-MoE 是正交的，可与剪枝、量化等方法组合，但论文未做实验验证协同效果。
- **训练阶段忽略**：仅限于预训练模型，未探索在训练时融入激活预算意识（如正则化），论文也承认这是未来方向。
- **Kbase 设定依赖经验**：虽然从实验得出 Kbase=1 最佳，但理论上最优值可能随模型和预算变化，缺乏自适应选择机制。
- **评估模型规模有限**：尽管三种模型有代表性，但最大参数量仅 15.7B（总参数量），未在更大规模（如 DeepSeek-V3、Mixtral 8x22B）上验证，泛化性有待确认。
- **推理效率测量简单**：仅报告平均速度提升，未区分批处理大小、序列长度等影响因素；且使用随机生成的 dummy prompt，可能与真实分布有偏差。

（完）
