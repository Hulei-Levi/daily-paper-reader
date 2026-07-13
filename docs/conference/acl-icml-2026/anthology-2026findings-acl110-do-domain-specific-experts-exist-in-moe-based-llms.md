---
title: Do Domain-specific Experts exist in MoE-based LLMs?
title_zh: MoE大语言模型中存在领域特定专家吗？
authors: "Giang Do, Hung Le, Truyen Tran"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.110.pdf"
tags: ["query:moe-special"]
score: 10.0
evidence: 研究MoE大模型中领域特定专家的存在性
tldr: 针对MoE大语言模型中专家专业化的本质理解不足的问题，系统研究了领域特定专家是否存在。在10个不同规模（3.8B-120B参数）的MoE模型上进行实验，提供了领域特定专家存在的实证证据，并提出了领域专业化分析方法。该工作为理解和利用MoE内部专家专业化提供了基础。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.110/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1643, \"height\": 727, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.110/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1621, \"height\": 186, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.110/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1610, \"height\": 290, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.110/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1605, \"height\": 285, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.110/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1630, \"height\": 191, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.110/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1637, \"height\": 1097, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.110/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1623, \"height\": 1083, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.110/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1600, \"height\": 1078, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.110/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1492, \"height\": 1067, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.110/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1658, \"height\": 973, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.110/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 815, \"height\": 1249, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.110/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 814, \"height\": 1084, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.110/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 815, \"height\": 423, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.110/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 746, \"height\": 433, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.110/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 780, \"height\": 436, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.110/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 794, \"height\": 251, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.110/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 792, \"height\": 252, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.110/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1653, \"height\": 576, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.110/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1659, \"height\": 253, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.110/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 799, \"height\": 142, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.110/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 800, \"height\": 192, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.110/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 792, \"height\": 87, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.110/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 800, \"height\": 129, \"label\": \"Table\"}]"
motivation: MoE专家专业化性质尚不明确，缺乏系统性解释。
method: 对10个MoE大模型进行实证分析，验证领域特定专家的存在。
result: 发现确实存在领域特定专家，并提出了分析方法。
conclusion: MoE大模型中存在领域特定专家，为后续利用专家专业化提供依据。
---

## Abstract
In the era of Large Language Models (LLMs), the Mixture of Experts (MoE) architecture has emerged as an effective approach for training extremely large models with improved computational efficiency. This success builds upon extensive prior research aimed at enhancing expert specialization in MoE-based LLMs. However, the nature of such specializations and how they can be systematically interpreted remain open research challenges. In this work, we investigate this gap by posing a fundamental question: *Do domain-specific experts exist in MoE-based LLMs?* To answer the question, we evaluate ten advanced MoE-based LLMs ranging from 3.8B to 120B parameters and provide empirical evidence for the existence of domain-specific experts. Building on this finding, we propose **Domain Steering Mixture of Experts (DSMoE)**, a training-free framework that introduces zero additional inference cost and outperforms both well-trained MoE-based LLMs and strong baselines, including Supervised Fine-Tuning (SFT). Experiments on four advanced open-source MoE-based LLMs across both target and non-target domains demonstrate that our method achieves strong performance and robust generalization without increasing inference cost or requiring additional retraining.

---

## 论文详细总结（自动生成）

以下是对论文 *Do Domain-specific Experts exist in MoE-based LLMs?* 的中文详细总结。

---

## 1. 核心问题与整体含义（研究动机和背景）

- **研究问题**：在基于混合专家（MoE）架构的大语言模型（LLM）中，是否真实存在**领域特定（domain-specific）的专家**？
- **背景与动机**：MoE 通过稀疏激活多个专家来提高计算效率，已有大量工作致力于提升专家专业化。然而，**专家专业化的本质及其可解释性仍不清晰**。本文旨在填补这一空白，系统验证领域特定专家的存在，并以此为基础提出一种无需训练的推理框架，以提升 MoE 模型在特定领域的表现。

## 2. 方法论

### 核心思想
- 定义并识别 **领域特定 token** 和 **领域特定 expert**，然后通过**路由权重放大**（steering）来增强模型对目标领域的适应性，无需任何参数更新或额外训练。

### 关键技术细节

1. **领域特定 token 的定义（Def. 3.1–3.2）**：
   - **Common Token**：移除后对任务指标（如交叉熵损失）影响很小的 token（变化 < ε）。
   - **Domain-specific Token**：移除后导致性能显著下降的 token（变化 ≥ ε）。
   - 为了高效识别，使用**梯度归因**近似计算 token 重要性：\( r_i = \| e_i \odot \nabla_{e_i} \mathcal{L} \|_2 \)，其中 \( e_i \) 是 token 的嵌入向量。

2. **领域特定 expert 的定义（Def. 3.4）**：
   - 每个专家 \( e_j \) 的领域特定分数：\( g(e_j) = P(e_j|D) \cdot [P(s \in \mathcal{S}|e_j) - P(s \in \mathcal{C}|e_j)] \)，其中第一项为专家在该领域的激活频率，第二项表示专家对领域特定 token 与普通 token 的偏好差异。
   - 取排名前 \( K \)（通常约总专家数的 1%）的专家作为领域特定专家集 \( \mathcal{E}^* \)。

3. **DSMoE 框架**：
   - 推理时，对属于 \( \mathcal{E}^* \) 的专家的原始路由权重（logit）乘以一个**放大系数** \( \alpha \in (0,100) \)，然后重新归一化。公式：\( \tilde{w}_j = \alpha \cdot w_j \)（如果 \( e_j \in \mathcal{E}^* \)），否则不变。
   - 整个过程**无需训练、无需额外推理成本**（一次识别后可缓存放大后的权重）。

## 3. 实验设计

- **数据集（Benchmarks）**：
  - **MMLU-Pro**：12K 多领域多选题（10 选 1），用于目标领域评估（Math, Biology, Physics, Chemistry）。
  - **GPQA Diamond**：198 道博士生级别科学问题，用于评估跨领域泛化。
  - **AIME**（2024 和 2025）：30 道数学竞赛题，用于高难度推理测试。

- **对比方法**：
  - 原始 MoE 模型（Base）
  - **RICE**：现有的训练-free 推理引导方法（针对思维专家）
  - **SFT (LoRA)**：监督微调（约 2.7% 可训练参数）

- **评估模型**：10 个开源 MoE 模型，参数从 3.8B 到 120B，包括 PhiMoE-Tiny、OLMoE、Qwen1.5-MoE、DeepSeek-MoE、GPT-OSS-20B/120B、ERNIE-4.5、Qwen3-MoE 系列等。

- **实验场景**：目标领域（MMLU-Pro 四个子域）和非目标领域（GPQA、AIME）的泛化测试，消融实验（专家数量 K、放大系数 α），小模型验证，专家协作分析。

## 4. 资源与算力

- 文中明确提及：
  - GPT-OSS-120B 使用 **2 × NVIDIA H200 GPU**。
  - GPT-OSS-20B 和 Qwen3-MoE 使用 **2 × NVIDIA H100 GPU**。
  - 推理加速使用 **vLLM 0.11.0**。
- **训练时长**：未明确给出，因为 DSMoE 是训练-free 方法，只有一次识别领域特定专家（前向传播）的成本，该成本与样本数成线性关系。
- **SFT 基线**：使用 LoRA（2.7% 参数），但未给出具体训练时长。

## 5. 实验数量与充分性

- **实验组数**：
  - 存在性验证：10 个模型 × 1 个领域（Math）→ 10 组（Figure 1）。
  - 目标领域评估：4 个模型 × 4 个领域 × 对比方法（Orig., RICE, SFT, DSMoE）→ 64 组（Table 2）。
  - 非目标领域（GPQA）：4 个模型 × 3 个领域 → 48 组（Table 3）。
  - 非目标领域（AIME）：2 个模型 × 2 个年份 → 8 组（Table 4）。
  - 消融实验：K 和 α 的消融（Table 5, 6）。
  - 小模型（PhiMoE-Tiny）：4 个领域 × 2 种方法 → 8 组（Table 10）。
  - 专家协作分析（Table 12）。
- **充分性评估**：实验**覆盖全面**，包括不同规模模型、多个领域、多种基线，并进行了消融和泛化测试。对比公平（沿用相同超参数设置到泛化数据集）。**结论可靠**。

## 6. 主要结论与发现

1. **领域特定专家确实存在**：在全部 10 个 MoE 模型中，通过领域特定 token 识别并激活单个专家即可带来性能提升（3%–45%）。
2. **DSMoE 在目标领域上显著优于基线**：在 MMLU-Pro 上，DSMoE 平均绝对提升 +1.5%（Qwen3-30B-Instruct）到 +14.5%（GPT-OSS-120B），**超过 RICE 和 SFT**。
3. **强泛化能力**：在 GPQA 和 AIME 上，DSMoE 保持领先，尤其在小模型（GPT-OSS-20B）上提升高达 +27.1%（GPQA 平均）。
4. **零额外推理成本**：一次识别后，推理时与原模型成本相同，且往往能**减少思考 token 数量**，提高效率。
5. **小模型同样受益**（PhiMoE-Tiny 平均 +6.3%）。
6. 协作专家（非领域特定专家）仍对性能有贡献，不可完全移除。

## 7. 优点

- **简洁高效**：方法无需训练，不增加推理开销，易于落地。
- **可解释性强**：明确定义领域特定 token/expert，并使用梯度归因和频率偏好差量化，逻辑清晰。
- **实验全面且公平**：覆盖多规模、多领域、多基线，超参数迁移至非目标数据集，避免过拟合。
- **消融充分**：探究了 K、α 的影响，以及专家协作角色，深化了对 MoE 内部机制的理解。
- **代码开源**：提供 GitHub 仓库，保证可复现。

## 8. 不足与局限

- **模型规模受限**：实验最大模型为 120B，未测试 400B 以上（如 DeepSeek-R1），作者也指出未来需扩大范围。
- **数据偏差风险**：使用网络数据，可能包含性别、种族偏见，文中提及但未做专门去偏。
- **应用限制**：DSMoE 需要先对目标领域做一次识别，对于全新领域没有现成的专家集，需重新做一遍梯度归因（计算成本虽可控，但对实时场景仍不便）。
- **仅关注特定专家放大**：未考虑专业化和协作专家之间的动态平衡，过度放大可能损害通用能力（实验中也发现 α 过大导致性能下降）。
- **计算资源有限**：未在更大集群上进行实验，可能影响统计显著性。

---

（完）
