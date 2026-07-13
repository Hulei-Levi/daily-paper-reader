---
title: Mixture-of-Experts with Intermediate CTC Supervision for Accented Speech Recognition
title_zh: 具有中间CTC监督的混合专家模型用于口音语音识别
authors: "Wonjun Lee, Hyounghun Kim, Gary Geunbae Lee"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-long.1194.pdf"
tags: ["query:moe-special"]
score: 9.0
evidence: 通过口音感知路由促进专家专业化
tldr: 针对口音语音识别中专家专业化不足的问题，提出MoE-CTC架构，采用中间CTC监督和口音感知路由策略，逐步过渡到无标签推理，有效提升了专家对口音模式的捕捉能力和模型的泛化性能。实验表明该方法在多种口音数据集上显著优于基线。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1194/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1429, \"height\": 924, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1194/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 682, \"height\": 718, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1194/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1660, \"height\": 658, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1194/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 812, \"height\": 333, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1194/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 816, \"height\": 355, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1194/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 803, \"height\": 293, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1194/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 811, \"height\": 315, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1194/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 799, \"height\": 315, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1194/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 802, \"height\": 665, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1194/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 803, \"height\": 327, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1194/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 799, \"height\": 278, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1194/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 810, \"height\": 273, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1194/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 812, \"height\": 236, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1194/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 809, \"height\": 298, \"label\": \"Table\"}]"
motivation: 口音语音识别中现有模型对多样口音泛化差，需促进专家专业化。
method: 提出MoE-CTC，使用口音感知路由训练，逐步过渡到无标签路由，每个专家配备CTC分支。
result: 在多个口音数据集上，所提方法显著提升了识别准确率，并展现了更好的跨口音泛化。
conclusion: 中间CTC监督和口音感知路由能有效促进专家专业化，改善口音ASR性能。
---

## Abstract
Accented speech remains a persistent challenge for automatic speech recognition (ASR), as most models are trained on data dominated by a few high-resource English varieties, leading to substantial performance degradation for other accents. Accent-agnostic approaches improve robustness yet struggle with heavily accented or unseen varieties, while accent-specific methods rely on limited and often noisy labels. We introduce MoE-CTC, a Mixture-of-Experts architecture with intermediate CTC supervision that jointly promotes expert specialization and generalization. During training, accent-aware routing encourages experts to capture accent-specific patterns, which gradually transitions to label-free routing for inference. Each expert is equipped with its own CTC head to align routing with transcription quality, and a routing-augmented loss further stabilizes optimization. Experiments on the MCV-Accent benchmark demonstrate consistent gains across both seen and unseen accents in low- and high-resource conditions, achieving up to 29.3% relative WER reduction over strong FastConformer baselines.

---

## 论文详细总结（自动生成）

# 中文论文总结

## 1. 核心问题与整体含义（研究动机和背景）
- **问题**：自动语音识别（ASR）模型在多数训练数据（如英语标准口音）上表现优异，但在口音语音上性能显著下降，存在公平性和包容性问题。
- **现有方法的不足**：
  - 口音无关方法（如wav2vec 2.0、Whisper）虽提升鲁棒性，但对重度口音或未见口音仍效果不佳。
  - 口音特定方法（如微调、适配器、口音嵌入）依赖口音标签，泛化性差，且标签往往有限、有噪声。
  - 混合专家（MoE）方法能通过专家专业化适应多样口音，但现有系统要么需要测试时口音标签，要么无法可靠路由到合适专家。
- **本文目标**：提出一种无需测试时口音标签、能促进专家专业化与泛化平衡的MoE架构，用于口音鲁棒语音识别。

## 2. 方法论：核心思想、关键技术细节
- **核心思想**：将MoE与专家级别的中间CTC监督结合，采用两阶段训练策略：第一阶段使用口音感知路由（accent-aware routing）使专家学习口音特定模式，第二阶段过渡到无标签路由（accent-agnostic），使模型对未见口音泛化。每个专家配备独立CTC头，将路由决策与转录质量对齐；并引入路由增强损失稳定优化。
- **关键组件**：
  - **MoE模块**：插入在FastConformer编码器层之间，每个MoE层包含N个专家（前馈网络），采用Top-K路由，K=2，N=5（默认匹配训练集中已见口音数）。输入序列先做时间步平均池化，路由网络基于池化表示产生专家分布。
  - **口音感知路由（Accent-Aware Routing）**：训练时每个样本有口音标签，通过偏置项（bias term）`α·1[j=ai]` 和口音分类损失 `Laccent` 引导样本路由到对口专家，促进专业化。
  - **专家级CTC监督（MoE-CTC）**：每个专家配备独立CTC头，计算专家特定CTC损失 `L_CTC^(ℓ,j)`，并通过路由概率加权得到局部损失 `Llocal = Σ_ℓ Σ_j g_j^(ℓ) L_CTC^(ℓ,j)`。同时，CTC头的logits经过投影后按路由权重回加到MoE输出，形成自条件残差路径，使CTC信息向下层传播。
  - **两阶段训练**：第一阶段（口音感知阶段）使用 `L = L_CTC + β Llocal + γ Laccent`；第二阶段（口音无关阶段）移除偏置和 `Laccent`，仅使用 `L_CTC + β Llocal` 微调20个epoch，使路由器自行根据转录质量选择专家。
- **算法流程**（文字说明）：
  1. 输入音频帧经FastConformer编码器前几层，在特定层（第4、8、12层）后插入MoE模块。
  2. 在MoE模块中，对编码器输出做时间平均池化，路由网络生成专家分布，取Top-K专家，输出为所选专家输出的加权和。
  3. 每个专家的输出通过其CTC头计算局部CTC损失，投影后加权叠加回主路径。
  4. 总损失包含全局CTC损失、局部CTC损失（路由加权）和口音分类损失（仅在阶段一）。
  5. 第一阶段训练至收敛，第二阶段继续微调（无口音监督）20个epoch，选最佳验证WER的模型。

## 3. 实验设计
- **数据集**：
  - **MCV-Accent基准**（源自Mozilla CommonVoice英语部分）：训练集有100h和600h两个子集，包含5个已见口音（澳大利亚、加拿大、英格兰、苏格兰、美国）。验证集同前5个口音；测试集额外包含9个未见口音（非洲、香港、印度、爱尔兰、马来西亚、新西兰、菲律宾、新加坡、威尔士）。
  - **LibriSpeech-960h**用于预训练。
- **基准方法**：
  - FastConformer（Small/Medium/Large三个规模，参数12.78M~115.60M）
  - Inter-CTC（在FastConformer基础上加中间CTC损失）
  - MoE（无口音监督的标准MoE）
  - Accent-MoE（带口音感知路由，无专家CTC头）
  - 与先前基准Prabhu et al. (2023, 2024)的方法对比（MTL、DAT、HuBERT等）
- **评估指标**：词错误率（WER）。
- **设置**：
  - 所有模型先预训练于LibriSpeech-960h，再微调于MCV-Accent-100h或600h。解码采用贪心CTC，无语言模型。
  - MoE相关模型均插入3个MoE层（第4、8、12层），N=5，K=2，α=2，β=1/(2×L×N)，γ=0.1。

## 4. 资源与算力
- **显式说明**：论文明确提到所有实验在**8张NVIDIA A100 GPU（80GB）**上实现，使用NeMo框架，混合精度（FP16）训练，全局batch size 1024。
- 最大训练epoch 500，但具体总训练时长和GPU小时数未报告。

## 5. 实验数量与充分性
- **实验组数**：丰富，覆盖多个维度。
  1. **主实验**：三个规模（Small/Medium/Large）下对比5种模型（FastConformer、Inter-CTC、MoE、Accent-MoE、MoE-CTC），在100h数据微调的结果（表1）。
  2. **基准复制**：与先前结果比较（表2、表3），分别使用46M/76M模型在100h/600h数据上（未预训练）做加权平均WER。
  3. **消融实验**：
     - 口音感知训练两阶段效果（表4）。
     - 路由性能分析（混淆矩阵图2）。
     - Oracle口音路由上限（表5）。
     - 专家数量（5 vs 8，表10）。
     - CTC头共享策略（全分离、层共享、全局共享，表11）。
     - MoE插入位置（早、中、晚、平衡，表12）。
  4. **模型配置细节**（附录表格8-9）。
- **充分性评价**：
  - **实验充分**：覆盖不同参数规模、不同训练数据量、多种消融场景，并与多个强基线公平对比（参数匹配）。
  - **客观公平**：控制参数规模（如表1中MoE系列参数相当）；使用相同预训练和微调流程；对比基线和先前工作均按原文设置。
  - **可重复性**：提供了关键超参数（α、β、γ、K、N、MoE层数等）、模型配置表，有利于复现。

## 6. 主要结论与发现
- **MoE-CTC在所有设置下取得最低WER**：
  - 在Small编码器上，相对FastConformer基线在已见口音降低29.3% WER，未见口音降低17.3%；在Large编码器上分别为20.3%和27.8%。
  - 在600h训练数据、76M模型下，比先前最佳（Prabhu et al., 2024）在已见口音降低18.4% WER，未见口音降低5.9%。
- **口音感知训练的两阶段有效性**：
  - 从口音感知阶段到口音无关微调，MoE-CTC在已见口音WER进一步下降5.2%，未见口音下降12.0%（相对），而Accent-MoE降幅较小（3.8%和6.0%）。
- **路由质量**：
  - 口音无关训练后，路由器仍保持66.2% top-1口音分类准确率，且混淆模式符合口音相似性（如加拿大→美国，苏格兰→英格兰），表明路由自发倾向声学/地理相近口音。
- **Oracle实验**：提供测试时真实口音标签可达5.2% WER（已见平均），比无标签时5.5%更低，印证了口音标签的信息增益，但差距不大，说明MoE-CTC已很好泛化。

## 7. 优点
- **方法创新**：
  - 首次将中间CTC监督扩展到MoE专家的个体CTC头，实现路由与转录质量直接对齐。
  - 两阶段训练（口音感知→口音无关）巧妙平衡专业化与泛化，无需测试时口音标签。
  - 路由增强损失 `Llocal` 简单有效，无需额外推断策略。
- **实验设计规范**：
  - 控制参数规模进行公平对比。
  - 覆盖已见/未见口音、低/高资源场景，消融全面（专家数、CTC头共享、模块位置等）。
  - 提供Oracle分析以探讨上限，结果合理可信。
- **性能显著**：在多个设置下均实现一致的WER降低，尤其在未见口音上泛化能力突出。

## 8. 不足与局限
- **实验覆盖**：
  - 仅基于MCV-Accent英语口音，未在跨语言或多语种口音数据集上验证。
  - 训练数据量最大600h，尚未在更大规模（如几千小时）条件下测试。
- **方法假设**：
  - 序列级别路由假设口音是离散的、整句不变的，无法直接处理混合口音或代码转换场景。
  - 依赖口音标签进行初始训练，限制了在无监督场景下的应用。
- **效率问题**：
  - 专家CTC头带来额外参数（约14%~16%参数增长，表9），且路由计算增加训练和推理延迟（虽为稀疏激活）。
  - 未详细报告推理速度和内存占用对比。
- **解释性不足**：
  - 专家内部机制未可视化，不同专家究竟学到了何种口音模式未做深入分析。
- **风险**：
  - 若口音标签有噪声或偏斜，可能导致不合理的初始路由，影响最终性能（论文未讨论此情况）。

（完）
