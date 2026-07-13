---
title: "SARA: Unlocking Multilingual Knowledge in Mixture-of-Experts via Semantically Anchored Routing Alignment"
title_zh: SARA：通过语义锚定路由对齐解锁混合专家模型中的多语言知识
authors: "Tianyu Dong, Yangyang Liu, Jiang Zhou, Xinwei Wu, Xiaohu Zhao, Hao Wang, Heng Liu, Linlong Xu, Longyue Wang, Weihua Luo, Shaolin Zhu, Deyi Xiong (德意 熊)"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.136.pdf"
tags: ["query:moe-special"]
score: 7.0
evidence: 对齐跨语言路由分布以促进专家共享
tldr: 针对多语言MoE中低资源语言路由偏离的问题，提出SARA框架，通过语义锚定路由对齐，将高资源语言的专业能力迁移到低资源语言。实验表明提升了跨语言专家共享和下游任务性能。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.136/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1645, \"height\": 1010, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.136/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1651, \"height\": 413, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.136/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 779, \"height\": 591, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.136/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 783, \"height\": 520, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.136/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1536, \"height\": 871, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.136/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1538, \"height\": 874, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.136/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 783, \"height\": 492, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.136/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1604, \"height\": 1262, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.136/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1597, \"height\": 615, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.136/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 801, \"height\": 173, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.136/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 417, \"height\": 464, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.136/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 804, \"height\": 346, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.136/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1117, \"height\": 344, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.136/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1453, \"height\": 617, \"label\": \"Table\"}]"
motivation: 低资源语言与高资源语言路由不一致，限制了跨语言专家共享。
method: 提出SARA，使用高资源语言作为锚点，显式对齐路由分布。
result: 在多语言任务上，SARA提升了低资源语言性能并保持了高资源性能。
conclusion: 语义锚定路由对齐能有效促进MoE中的跨语言知识迁移。
---

## Abstract
Sparse Mixture-of-Experts (MoE) architectures have emerged as an increasingly influential paradigm as they offer a strategic balance between parameter scalability and computational efficiency. However, low-resource language tokens are often routed to different experts than those predominantly activated by high-resource inputs, which limits cross-lingual expert sharing. This cross-lingual routing divergence consequently hinders their efficacy in multilingual contexts. To address this issue, we propose SARA (Semantically Anchored Routing Alignment), a framework designed to transfer specialized capabilities from high-resource languages as anchors to low-resource languages. SARA explicitly aligns the routing distribution of multilingual inputs with high-resource semantic anchors using a symmetric Jensen-Shannon (JS) divergence constraint. Unlike traditional distillation methods that operate on output logits, SARA directly aligns the internal routing distributions of MoE layers, encouraging mechanistic consistency in expert selection across languages. We conduct experiments on 2 LLMs across 5 low-resource languages and 3 benchmarks. Experiment results demonstrate that SARA outperforms standard instruction tuning (e.g., +0.8% on Qwen3-30B-A3B and +1.2% on Phi-3.5-MoE-instruct on Global-MMLU benchmark). Further analyses show that SARA effectively addresses performance bottlenecks in low-resource languages, providing a scalable pathway to enhance multilingual capabilities in sparse architectures.

---

## 论文详细总结（自动生成）

# 论文总结：SARA: 通过语义锚定路由对齐解锁混合专家模型中的多语言知识

## 1. 核心问题与整体含义（研究动机和背景）

- **核心问题**：稀疏 Mixture-of-Experts（MoE）架构在参数扩展性和计算效率之间取得了良好平衡，但在多语言场景下存在**跨语言路由发散**问题——低资源语言（如斯瓦希里语、泰卢固语等）的 tokens 往往被路由到与高资源语言（如英语）不同的专家，导致低资源语言无法充分利用高资源语言专家的专门能力，性能显著下降。
- **研究背景**：现有方法（如持续预训练、指令微调、专家剪枝或负载均衡）主要优化计算吞吐量或通用效率，未能直接解决跨语言语义一致性导致的路由错位问题。MoE 模型内部存在“超级专家”，但低资源语言因词汇表差异而无法正确激活这些专家。
- **整体含义**：本文旨在通过显式对齐跨语言的路由分布，将高资源语言的专业化能力迁移至低资源语言，从而提升 MoE 模型的多语言性能，且不损害高资源语言自身的能力。

## 2. 方法论：核心思想、关键技术细节与算法流程

### 核心思想
- 将高资源语言（如英语）的路由概率分布视为**语义锚点**，通过最小化低资源语言路由分布与锚点分布之间的 Jensen-Shannon 散度（JS divergence），强迫语义等价的输入在不同语言下激活相似的专家子集。

### 关键技术细节（三阶段流程）
1. **语义锚定数据构建（Stage 1）**：
   - 对高资源语言训练集进行推理，仅保留模型正确回答的样本（通过正则提取 `\boxed{}` 验证）。
   - 将验证后的样本（包括 prompt 和推理步骤）通过 GPT-5 mini 翻译为目标低资源语言，构建平行指令数据，确保内容语义严格一致。

2. **捕获目标路由先验（Stage 2）**：
   - 对高资源语言的完整序列（prompt + 正确响应）进行前向传播，提取每层 token 级的软路由概率分布（softmax-normalized）。
   - 通过有效掩码（过滤 [PAD] 标记）聚合为序列级路由分布 $\bar{P}^{(l,i)}_{\text{anchor}}$。

3. **序列级路由对齐（Stage 3）**：
   - 对低资源语言序列同样计算序列级路由分布 $\bar{Q}^{(l,i)}_{\text{lang}}$。
   - 对齐损失：$L_{JS} = \frac{1}{|L_{\text{target}}|} \sum_{l=L_{\text{start}}}^{L_{\text{end}}} JS(\bar{P}^{(l,i)}_{\text{anchor}} \parallel \bar{Q}^{(l,i)}_{\text{lang}})$，其中 JS 散度采用对称形式 $JS(P\|Q)=\frac{1}{2}KL(P\|M)+\frac{1}{2}KL(Q\|M)$，$M=\frac{1}{2}(P+Q)$。
   - 总损失：$L_{\text{total}} = L_{CE} + \lambda_{LB} L_{LB} + \lambda_{JS} L_{JS}$，其中 $L_{CE}$ 为任务交叉熵损失，$L_{LB}$ 为负载均衡损失（来自 Switch Transformer）。
- **关键选择**：仅对中间层（Qwen3-30B-A3B 的 7-34 层）施加路由对齐，避免干扰浅层（处理表层语言特征）和深层（生成特定语言输出）。

## 3. 实验设计

### 数据集与基准
- **训练数据**：基于 MMLU-ProX 和 GSM8K 的高资源语言子集，经 GPT-5 mini 翻译为 5 种低资源语言：印地语 (hi)、尼泊尔语 (ne)、孟加拉语 (bn)、泰卢固语 (te)、斯瓦希里语 (sw)。每条语言约 7000 个 MMLU-ProX 样本和 7000 个 GSM8K 样本（共约 14,000 条/语言）。
- **评测基准**：
  - **Global-MMLU**（约 14,000 题/语言）：多语言选择题。
  - **BELEBELE**（约 900 题/语言）：阅读理解选择题。
  - **MGSM**（约 250 题/语言）：数学推理。
- **评估方式**：零样本（移除与测试集重叠的训练样本），Top-p=1, temperature=0.1，报告 3 次独立运行的平均值±标准差。

### 对比方法
- **Vanilla LM**：原始指令微调后的稀疏 MoE 模型。
- **FFT**：标准全参数微调（仅在相同翻译数据上，不加路由对齐损失）。
- **AES**：添加正交化损失和方差损失以促进专家专门化。
- **ShifCon**：对齐非主导语言与主导语言子空间的表示级方法。
- **SARA (ours)**：本文方法。
- **两种锚点设置**：英文锚点、中文锚点，分别独立训练。

### 被测模型
- **Qwen3-30B-A3B**（主模型）
- **Phi-3.5-MoE-instruct**（验证泛化性）

## 4. 资源与算力

- 文中明确提及：使用 **PyTorch 框架**，在 **16 × NVIDIA H100 80GB GPU** 上训练 Qwen3-30B-A3B，每个训练会话约 **15 小时**。
- 全局 batch size 256，学习率 2e-5（余弦衰减），训练 2 个 epoch。
- 损失系数：$\lambda_{LB}$ 遵循模型默认配置，$\lambda_{JS}=1.5$。

## 5. 实验数量与充分性

- **主要实验**：在 2 个模型、3 个基准、5 种低资源语言上，对比了 4 种基线（Vanilla, FFT, AES, ShifCon），并报告了英文和中文两种锚点的结果。表 1 展示了全部结果。
- **消融实验**（表 2）：系统研究了路由先验来源（模型自身 vs 外部 GPT 数据）、锚点语言（英文 vs 斯瓦希里语）、层选择策略（选中间层 vs 所有层 vs 随机层）。
- **敏感性分析**（附录 A.3）：调整 $\lambda_{JS}$ 从 0.5 到 2.0，确认 1.5 最优。
- **翻译质量影响**（图 4、表 3）：使用 CometKiwi 评估 GPT-5 mini 和 GPT-5 nano 翻译质量，并比较下游性能。
- **路由一致性可视化**（图 2）：展示基模型、FFT、SARA 后各层 JS 散度变化。
- **训练动态**（图 3）：对比 SARA 与 FFT 在数据量增长时的性能曲线。
- **统计显著性**（附录 A.4）：对 Qwen3 的 Global-MMLU 进行单尾配对 t 检验，p < 0.01，证明 SARA 显著优于 FFT；BELEBELE 和 MGSM 因样本量较小未达统计显著，但趋势一致。
- **结论**：实验设计较为全面，消融覆盖了关键模块，统计检验增强了可信度。但 BELEBELE 和 MGSM 的统计效力不足是客观限制。

## 6. 主要结论与发现

- SARA 在所有三个基准上均优于标准全参数微调（FFT），在 Global-MMLU 上平均提升 +0.8% (Qwen3) / +1.2% (Phi-3.5)。
- 路由对齐损失明确降低了低资源语言与高资源语言之间的 JS 散度（图 2c），中间层尤其明显。
- 使用模型自身的高资源推理路由先验（自锚定）优于外部教师模型（GPT-5 mini）提供的先验（-g-en-s 变体在 MGSM 上仅 53.00% vs 87.40%），说明机制一致性至关重要。
- 仅对齐中间层（而非全部层）效果最好，强制对齐浅层和深层会损害语言灵活性和生成质量。
- 锚点语言质量决定了性能上限：英文锚点优于中文锚点，后者因模型本身中文路由稳定性较低。
- 翻译质量影响对齐效果：GPT-5 mini 翻译质量更高，带来更好性能。

## 7. 优点

- **方法创新**：首次提出将路由概率分布作为跨语言语义锚点进行显式对齐，区别于传统 logit 蒸馏或表示对齐，直接作用 MoE 路由机制。
- **对称 JS 散度**：与 KL 散度相比，JS 散度对称且对低概率尾部更稳健，适合稀疏路由场景。
- **自锚定策略**：利用模型自身推理轨迹而非外部数据，避免了教师-学生不一致问题。
- **实验充分**：覆盖多种语言、多个基准、多模型，消融实验系统，统计检验严谨。
- **可扩展性**：方法独立于语言和架构，可迁移至其他 MoE 模型。

## 8. 不足与局限

- **数据多样性**：训练数据主要来自 MMLU-ProX 和 GSM8K，风格较单一，可能限制对多样化文本风格的泛化。
- **翻译噪声**：依赖 GPT-5 mini 生成平行数据，翻译伪影可能引入噪声，对齐性能受限于翻译质量。
- **文化偏见风险**：强制路由对齐可能导致模型偏向高资源语言的认知模式，抑制低资源语言的独特文化表达。
- **层选择启发式**：当前基于观测到的 U 型发散曲线选择中间层，对于门控机制或深度配置不同的 MoE 架构可能需要重新调整。
- **实验覆盖**：仅测试了 5 种低资源语言，且 hi 是否应归为低资源存在争议（文中也标注了社区讨论）。对更多语系（如西欧小语种、非洲语言等）的泛化尚待验证。
- **计算开销**：需要先对高资源数据做前向传播提取路由分布，并额外计算 JS 损失，训练时间可能略长于标准 FFT。

（完）
