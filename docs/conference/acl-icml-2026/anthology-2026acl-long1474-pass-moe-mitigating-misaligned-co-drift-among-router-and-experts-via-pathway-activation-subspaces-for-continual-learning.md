---
title: "PASs-MoE: Mitigating Misaligned Co-drift among Router and Experts via Pathway Activation Subspaces for Continual Learning"
title_zh: PASs-MoE：通过路径激活子空间缓解混合专家持续学习中路由器与专家的失调共漂移
authors: "ZhiYan Hou, Haiyun Guo, Haokai Ma, Yandu Sun, Yonghui Yang, Jinqiao Wang"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-long.1474.pdf"
tags: ["query:moe-special"]
score: 9.0
evidence: 解决持续学习中导致专家专业化退化的失调共漂移问题
tldr: 针对持续指令调优中路由器与专家的失调共漂移导致专家专业化模糊的问题，提出PASs-MoE，通过路径激活子空间（PAS）分离路由器与专家更新轨迹，保持输入-专家专业化。实验表明有效缓解遗忘并提升多任务性能。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1474/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 810, \"height\": 268, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1474/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1618, \"height\": 681, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1474/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 796, \"height\": 667, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1474/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 799, \"height\": 601, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1474/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 799, \"height\": 602, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1474/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1661, \"height\": 490, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1474/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 793, \"height\": 443, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1474/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 804, \"height\": 206, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1474/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1652, \"height\": 528, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1474/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1649, \"height\": 231, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1474/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 807, \"height\": 395, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1474/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1474, \"height\": 354, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1474/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1655, \"height\": 340, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1474/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1650, \"height\": 525, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1474/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1647, \"height\": 231, \"label\": \"Table\"}]"
motivation: 现有LoRA-MoE方法在持续学习中导致专家专业化退化，加剧遗忘。
method: 引入路径激活子空间（PAS），在LoRA中分离路由器与专家的更新方向。
result: 在多种持续学习设置下，PASs-MoE显著减少遗忘并保持专家专业化。
conclusion: 路由器与专家的解耦更新是维持持续学习中专家专业化的关键。
---

## Abstract
Continual instruction tuning (CIT) requires multimodal large language models (MLLMs) to adapt to a stream of tasks without forgetting prior capabilities. A common strategy is to isolate updates by routing inputs to different LoRA experts. However, existing LoRA-based Mixture-of-Experts (MoE) methods often jointly update the router and experts in an indiscriminate way, causing the router’s preferences to co-drift with experts’ adaptation pathways and gradually deviate from early-stage input–expert specialization. We term this as ***Misaligned Co-drift***, which blurs expert responsibilities and exacerbates forgetting. To address this, we introduce the ***pathway activation subspace (PASs)***, a LoRA-induced subspace that reflects which low-rank pathway directions an input activates in each expert, providing a capability-aligned coordinate system for routing and preservation. Based on PASs, we propose a fixed-capacity PASs-based MoE–LoRA method with two components: PAS-guided Reweighting, which calibrates routing using each expert’s pathway activation signals, and PAS-aware Rank Stabilization, which selectively stabilizes rank directions important to previous tasks. Experiments on a CIT benchmark show that our approach consistently outperforms a range of conventional continual learning baselines and MoE–LoRA variants in both accuracy and resistance to forgetting, without increasing model parameters. Our code is publicly available at https://github.com/yueluoshuangtian/PASs-MoE .

---

## 论文详细总结（自动生成）

# 论文中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

**研究动机**：多模态大语言模型（MLLMs）在持续指令调优（CIT）中需要顺序学习多个任务，同时避免遗忘已习得能力。一种常见策略是通过路由将不同输入分配给不同的 LoRA 专家，以隔离更新。然而，现有的基于 LoRA 的混合专家（MoE）方法通常不加区分地**联合更新路由器和专家参数**，导致路由器对输入的偏好与专家自身的适应路径发生**共同漂移**（Misaligned Co-drift），从而破坏早期建立的“输入–专家”专业化关系，进而加剧灾难性遗忘。

**整体含义**：论文指出，MoE-LoRA 在持续学习中的根本问题在于**路由决策与专家参数更新方向不耦合**，这种错位会模糊专家职责、降低长期记忆能力。为此，作者从 LoRA 的结构特性出发，提出了一种新的视角和解决方案：利用**路径激活子空间（PASs）** 作为能力对齐的坐标系来指导路由和知识保留，最终实现更好的持续学习性能。

## 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程

**核心思想**：每个 LoRA 专家由一个下投影矩阵 \(A_e \in \mathbb{R}^{r \times d_{in}}\) 和上投影矩阵 \(B_e \in \mathbb{R}^{d_{out} \times r}\) 组成。对于输入 \(h\)，专家产生的低秩响应为 \(z_e = A_e h \in \mathbb{R}^r\)。论文定义**PASs** 为 \(A_e^{\top}\) 的行空间，即专家能感知的输入方向集。这一子空间天然地和专家的功能（对哪些输入模式敏感）绑定。基于 PASs，论文提出两个关键组件：

1. **PASs-guided Reweighting (PASs-RW)**  
   - 不依赖独立的可学习路由器，而是直接利用每个专家的**激活能量** \(s_e(h) = \frac{1}{r} \|A_e h\|_2^2\) 作为专家权重的依据。
   - 混合系数通过 softmax 计算：\(\pi_e(h) = \frac{\exp(s_e(h))}{\sum_{e'}\exp(s_{e'}(h))}\)。
   - 优势：将路由决策锚定在专家自身的低维响应上，避免路由与专家参数错位。

2. **PASs-aware Rank Stabilization (PASs-RS)**  
   - 在顺序训练中，记录每个秩方向 \((e,k)\) 的重要性：\(I_{e,k}(t) = \mathbb{E}_{h \sim D_t}\left[ \pi_e(h) (a_{e,k}^\top h)^2 \right]\)。
   - 累积历史重要性 \(I_{e,k}^{\text{agg}}(t-1)\)，并据此对 \(A_e\) 和 \(B_e\) 中相应列施加**加权 L2 正则化**，使得学习新任务时，对先前任务重要的秩方向变化更小。
   - 正则化项：\(\mathcal{L}_{\text{stab}}^A = \sum_{e,k} w_{e,k} \|a_{e,k}^{(t)} - a_{e,k}^{(t-1)}\|_2^2\)，对 \(B\) 同理。总损失 = 任务损失 + \(\lambda_A \mathcal{L}_{\text{stab}}^A + \lambda_B \mathcal{L}_{\text{stab}}^B\)。

**算法流程**：  
- 初始化固定数量的 LoRA 专家（如 6 个）。  
- 顺序训练每个任务时：
  1. 通过冻结的骨干网络获得隐藏表示 \(h\)。
  2. 计算每个专家的激活能量 \(s_e(h)\)，得到软路由权重 \(\pi_e(h)\)。
  3. 混合专家输出：\(\Delta W(h) = \sum_e \pi_e(h) B_e A_e h\)。
  4. 同时，基于当前任务的激活统计更新秩重要性累积。
  5. 在优化时加入 PASs-RS 正则项，稳定重要秩方向。

## 3. 实验设计：数据集、基准、对比方法

**数据集**：使用 **MLLM-CTBench ENCH**（一个面向多模态持续指令调优的基准），包含 7 个任务：Math QA, Arts VQA, Math VQA, Economics QA, Medicine VQA, OCR VQA, Science VQA。任务涵盖文本 QA 和视觉 VQA，数据量经过平衡（每个任务训练样本约 5K–12K）。官方提供了两种任务顺序（Order-A 和 Order-B）。

**基准**：对比方法包括：  
- 传统方法：SeqFT, SeqLoRA, EWC, LwF, L2P, MAS, O-LoRA, HiDe-LLaVA。  
- MoE-LoRA 变体：DDAS, MoELoRA (Top-k), MoELoRA (Softmax)。  
- 消融：随机秩正则化、不同专家数量、不同正则化强度。

**评估指标**：  
- **AP**（平均最终准确率）= \(\frac{1}{T} \sum_t \text{Acc}_{\text{final}}^t\)  
- **BWT**（平均遗忘）= \(\frac{1}{T} \sum_t (\text{Acc}_{\text{final}}^t - \text{Acc}_{\text{after}}^t)\)，值越接近 0 遗忘越少。

## 4. 资源与算力

论文提到：“All methods are trained with a batch size of 12 on NVIDIA H20 GPUs, and all experiments are conducted with a fixed random seed of 42.”  
**但未明确说明使用的 GPU 数量、每个实验的训练总时长**。因此仅能确认使用了 NVIDIA H20 GPU，批量大小为 12。具体算力投入未公开。

## 5. 实验数量与充分性

论文设计了多组实验，较为充分：

- **主表 1**：在 Order-A 上对比 13 种方法，报告每个任务的最终准确率和遗忘。
- **消融实验**：
  - 结构消融（表 2）：逐步添加 PASs-RW 和 PASs-RS，验证各组件贡献。
  - 专家数量消融（表 3）：\(E=2,4,6,8\)，观察性能变化。
  - 正则化强度消融（图 4 和图 5）：变化 \(\lambda_A\) 和 \(\lambda_B/\lambda_A\) 比值，分析稳定性-塑性权衡。
- **替代任务顺序**（附录 A.2，表 6）：Order-B 上验证方法对任务顺序的鲁棒性。
- **随机正则化对比**（附录 A.3，表 7）：证明 PASs-RS 带来的提升源于选择重要秩方向而非随机约束。
- **路由稳定性分析**（图 3）：比较基线方法与 PASs-MoE 在路由分布漂移上的差异。
- **秩重要性分布可视化**（图 8）：展示重要性集中在少量秩方向。
- **更新方向与重要性关系**（图 6）：不同层中，重要性高的秩方向更新幅度更小。
- **训练损失曲线**（图 7）：证明训练过程稳定，无过拟合或崩溃。

**评价**：实验覆盖了多个维度（不同方法、超参数、任务顺序、机制验证），设计合理，比较公平（相同骨干、相同训练协议）。结论可信。

## 6. 论文的主要结论与发现

- **PASs-MoE 在 MLLM-CTBench ENCH 上显著优于所有对比方法**：AP 达到 48.46%，超过第二名 MoELoRA (Softmax) 的 43.36%（提高 5.1%），同时 BWT 从 -6.64 改善至 -2.15，遗忘更少。
- **PASs-RW 单独即可带来增益**（表 2），说明将路由与专家低维响应耦合比独立路由器更稳定。
- **PASs-RS 通过保护重要秩方向进一步提升性能**，且其对 A 的稳定效果比 B 更关键（A 是结构锚点）。
- **路由漂移与遗忘正相关**：基线方法产生更大的路由器分布变化，对应旧任务性能下降。
- **重要性集中在少量秩方向**，为选择性稳定提供了依据。

## 7. 优点

- **方法创新性**：首次从 LoRA 的路径激活子空间角度分析 MoE-LoRA 中的失调共漂移，并提出无需额外参数的解决方案。
- **高度耦合**：路由（PASs-RW）和知识保持（PASs-RS）共享同一 PASs 信号，形成统一框架，避免分别在独立空间设计带来的开销和冲突。
- **无需增加模型容量**：在固定专家池上进行操作，不增加参数量，利于部署。
- **实验充分且分析深入**：不仅报告指标，还通过路由稳定性、秩方向重要性、更新幅度等多个角度解释方法为何有效，提供了坚实的理论和实验支持。
- **鲁棒性验证**：在两种任务顺序下均表现优异，消融实验全面。

## 8. 不足与局限

- **适用范围有限**：方法针对固定容量 MoE-LoRA 设计，未在容量动态增长或有经验回访的场景下验证；可能不直接适用于其他 PEFT 形式（需要重新定义子空间）。
- **PASs-RW 的鲁棒性**：使用低维激活能量作为兼容性信号，在极端分布漂移或复杂指令下可能不够稳健，文中未深入探讨其校准问题。
- **PASs-RS 的实现代价**：需要维护历史统计量并调节两个额外的超参数 \(\lambda_A, \lambda_B\)，增加了实现复杂度和调参成本。
- **缺失直接的路由错位测量**：评估主要依靠 AP/BWT 这类整体指标，缺乏对专家职责演变、路由重新分配等细粒度的量化分析。
- **资源算力细节不透明**：未说明具体 GPU 数量、单次训练耗时，限制他人复现时成本评估。
- **结论可能受限于基准**：仅在 MLLM-CTBench 一个基准上评估（尽管有两个顺序），更多任务领域（如长尾任务、非英语任务）的效果未知。

（完）
