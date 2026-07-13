---
title: "Specialization without Sparsity: Efficient and Expressive Split-Path Experts for LLM Fine-Tuning"
title_zh: 无需稀疏的专业化：高效且表达力强的分裂路径专家用于大语言模型微调
authors: "Ganghao Liu, Qin Zhou, Zhe Wang, Xuehan Lu, Haihua Huang, Yunfei Tong, Heng Tian"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.975.pdf"
tags: ["query:moe-special"]
score: 9.0
evidence: 通过分裂路径专家增强LLM微调中的专业化
tldr: 针对参数高效微调中表示灵活性受限的问题，提出SparMoE，采用软路由和分裂路径专家，包含缩放路径（促进专业化）和偏置路径（保留专家信号），实现了高效专业化且无需稀疏路由。实验表明在多种任务上优于现有PEFT方法。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.975/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 765, \"height\": 629, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.975/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1570, \"height\": 739, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.975/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 726, \"height\": 599, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.975/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 723, \"height\": 599, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.975/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 756, \"height\": 490, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.975/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 799, \"height\": 650, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.975/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 799, \"height\": 647, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.975/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1655, \"height\": 1318, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.975/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1652, \"height\": 466, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.975/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1650, \"height\": 526, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.975/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1631, \"height\": 169, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.975/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 742, \"height\": 247, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.975/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1507, \"height\": 282, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.975/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 655, \"height\": 358, \"label\": \"Table\"}]"
motivation: 现有PEFT方法缺乏表示灵活性，而MoE硬路由不稳定。
method: 提出SparMoE，用软路由和分裂路径专家（缩放+偏置路径）实现专业化。
result: 在多个NLU任务上，SparMoE以较低参数获得更好性能。
conclusion: 软路由和分裂路径设计能有效提升微调中的专家专业化。
---

## Abstract
Parameter-efficient fine-tuning (PEFT) enables low-cost adaptation of large language models but often suffers from limited representational flexibility. To address this, we incorporate a Mixture-of-Experts (MoE) design and propose Efficient and Expressive split-path experts that enhance specialization while maintaining low resource overhead. Split-Path Adaptive Representation Mixture-of-Experts (SparMoE) replaces discrete hard routing with a soft routing and fully-activated mixture, enabling stable optimization. Each expert is parameterized as a split-path modulation module, consisting of a scaling path that promotes expert specialization and a bias path that preserves expert-specific signals. This design significantly enhances expressive capacity while maintaining strict parameter efficiency and architectural compatibility with PEFT. Extensive evaluations on GLUE, GSM8K, MBPP, and a text rewriting task from SmolTalk show that our approach consistently outperforms or matches state-of-the-art PEFT methods under comparable parameter budgets, achieving a favorable trade-off between adaptability and efficiency.

---

## 论文详细总结（自动生成）

# 基于论文《Specialization without Sparsity: Efficient and Expressive Split-Path Experts for LLM Fine-Tuning》的中文总结

## 1. 核心问题与整体含义（研究动机与背景）

- **背景**：大语言模型（LLM）参数规模巨大，全参数微调成本过高，参数高效微调（PEFT）成为主流方案。但现有PEFT方法（如LoRA、Adapter）受限于极小的可训练参数空间，表示能力不足，难以应对复杂、多方面的下游任务。
- **核心问题**：将混合专家（MoE）思想引入PEFT时存在根本性不匹配：
  - LoRA等基础模块并非为多专家组合设计，复制多个LoRA专家会导致参数随专家数线性增长，侵蚀效率优势。
  - 传统MoE使用离散硬路由（top-k选择），在参数极度受限的PEFT场景中易导致优化不稳定、专家未激活等问题，且需额外的负载平衡损失。
- **整体含义**：需要一种专为PEFT设计的轻量MoE框架，既能提升表示灵活性与专家专业化，又能保持参数效率、训练稳定性和架构兼容性。

## 2. 方法论：核心思想、关键技术细节与公式

### 核心思想
提出 **SparMoE（Split-Path Adaptive Representation Mixture-of-Experts）**，采用 **软路由（soft routing）** 和 **分裂路径专家（split-path expert）** 设计，替代离散硬路由与重型前馈专家，实现全激活、无辅助损失的稳定优化。

### 关键技术细节
- **模块位置**：在每个Transformer块的FFN之后插入SparMoE层。
- **软路由机制**：使用一个小型门控网络 \( G(h) \) 为每个token生成所有E个专家的软权重（softmax），所有专家均被激活并参与加权求和，无需top-k选择或负载平衡损失。
  - \( p = \text{softmax}(G(h)) \in \mathbb{R}^{S \times E} \)
  - \( h' = \sum_{e=1}^{E} p_{:,e} \odot z^{(e)} \)
- **分裂路径专家设计**：每个专家由两个并行路径组成：
  - **缩放路径（scaling path）**：\( z_{\text{scaling}}^{(e)} = \frac{1}{1-\rho} (h \odot l_{\text{scaling}}^{(e)} \odot m) \)，其中 \( m \) 为dropout掩码，\( l_{\text{scaling}}^{(e)} \in \mathbb{R}^H \) 为可学习的缩放向量。
  - **偏置路径（bias path）**：\( z_{\text{bias}}^{(e)} = h + l_{\text{bias}}^{(e)} \)，其中 \( l_{\text{bias}}^{(e)} \in \mathbb{R}^H \) 为可学习的偏置向量。
  - 专家输出：\( z^{(e)} = z_{\text{scaling}}^{(e)} + z_{\text{bias}}^{(e)} \)
- **配方特点**：缩放路径通过乘性调制和dropout促进专家多样化，偏置路径在dropout掩蔽时保留专家特定信号，共同增强表达力。

### 公式流程（文字说明）
1. 输入隐藏表示 \( h \)。
2. 对每个专家e，并行计算缩放路径（包含元素乘、dropout、缩放）和偏置路径（加性偏置），相加得 \( z^{(e)} \)。
3. 通过软路由网络 \( G \) 计算每个token对专家的权重 \( p \)。
4. 加权求和所有专家输出，得到最终表示 \( h' \)。
5. 仅训练专家参数（\( l_{\text{scaling}}, l_{\text{bias}} \)）和路由网络 \( G \)，骨干网络冻结。

## 3. 实验设计：数据集、Benchmark与对比方法

- **数据集与场景**：
  - **GLUE**（自然语言理解）：CoLA, SST-2, MRPC, QQP, STS-B, MNLI, QNLI, RTE。
  - **GSM8K**（数学推理）：多步算术文字题。
  - **MBPP**（程序合成）：Python编程问题。
  - **SmolTalk**（文本重写）：explore-instruct-rewriting子集，涵盖改写、释义、控制文本变换。
- **骨干模型**：
  - GLUE: RoBERTa-base / RoBERTa-large。
  - GSM8K: LLaMA2-7B-base。
  - MBPP: LLaMA2-13B-base。
  - SmolTalk: Qwen2.5-0.5B-Instruct, Qwen3-0.6B-Base, Qwen3-8B-Base, Qwen3-14B-Base。
- **对比方法**：
  - 全微调（FT）、LoRA、DoRA、QLoRA、LoRA+、MoELoRA、MoV、Adapter、Adapter-FFN、BitFit、IA³、RED 等。
- **评价指标**：GLUE各任务专用指标（ACC、MCC、CORR），GSM8K/MBPP准确率，重写任务BLEU、ROUGE-1/2/L、METEOR。

## 4. 资源与算力

- **GPU型号**：NVIDIA 4090、L20 GPU（文中明确提及），但未说明具体数量。
- **训练时长与内存**（具体数值来自表2）：
  - LLaMA2-7B GSM8K: SparMoE 峰值内存16.3 GB，训练时间14.7分钟（对比LoRA r=8 25.3GB, 18.2min）。
  - LLaMA2-13B MBPP: SparMoE 28.1 GB, 57.3秒（对比DoRA 46.2GB, 181.9s）。
- **参数规模**：SparMoE在RoBERTa-base仅0.11M参数（对比LoRA 0.3M、FT 125M），在LLaMA2-7B仅1.6M参数（对比LoRA r=8 8.4M）。
- 论文未提供总GPU卡·小时数，但训练效率数据清晰。

## 5. 实验数量与充分性

- **实验组数**：
  - 两个骨干上（base/large）共16个GLUE任务实验。
  - GSM8K和MBPP各一组，包含多个参数规模的LoRA/DoRA对比。
  - 4个Qwen模型上的重写任务实验（含MoELoRA对比）。
  - 消融研究：8个GLUE任务上测试dropout、scaling路径、bias路径、路由移除，共4组×8任务=32次比较。
  - 专家数量影响：GLUE上2/4/6/8专家，Qwen上4/8专家。
  - 超参敏感性分析（附录B）：在CoLA、MRPC上变化学习率和dropout。
- **充分性与公平性**：覆盖多种类型任务（分类、推理、代码、生成）、多种骨干（RoBERTa、LLaMA、Qwen），对比方法包括主流PEFT及其MoE变体，参数预算设定合理（类似参数规模下比较）。对于部分方法（如MoV、MoELoRA）因参数/超参复杂导致某些任务结果缺失，作者明确指出，保证了透明度。总体实验充分、客观、公平。

## 6. 论文的主要结论与发现

- SparMoE在几乎所有评估任务上以更少的可训练参数达到了与全微调相当或更优的性能（例如GLUE平均分86.1 vs FT 85.6 on RoBERTa-base）。
- 相比LoRA、DoRA等经典PEFT方法，SparMoE在数学推理（GSM8K 23.12% vs LoRA r=8 22.29%）、程序合成（MBPP 29.18 vs LoRA+ 30.35）、指令重写（BLEU/ROUGE/METEOR全面领先）上表现更优或接近。
- 软路由设计避免了硬路由的优化不稳定，且无需辅助损失。
- 分裂路径（缩放+偏置）显著提升专家多样性：消融实验证明去除任一路径都会导致明显性能下降（尤其偏置路径缺失导致CoLA下降12.5%）。
- 专家权重分析（图5）显示不同任务自然激活不同专家，证明功能性专业化已形成。
- SparMoE对超参数（学习率、dropout）稳健，在较宽范围内保持高性能。

## 7. 优点

- **设计巧妙**：分裂路径专家在几乎不增加参数（仅两个向量）的前提下提升了表达力；缩放路径+dropout促进多样性，偏置路径保留关键信息，互补配合。
- **参数极致高效**：以0.11M（base）、0.29M（large）的参数数超越或持平全微调，远低于LoRA MoE变体。
- **无需辅助工程**：软路由全激活无需负载平衡损失、top-k选择、专家区分标签，训练简单稳定。
- **跨架构、跨任务泛化性强**：在RoBERTa（分类）、LLaMA（推理/代码）、Qwen（生成）上均验证有效。
- **消融分析深入**：逐一验证每个组件的必要性，并理论分析专家差异来源（公式6）。
- **资源效率透明**：提供了内存和训练时间的对比，证明实际部署友好。

## 8. 不足与局限

- **知识遗忘问题**：未讨论在指令微调模型上的预训练知识遗忘，也未进行模型知识保留测试。
- **鲁棒性测试不足**：未涉及对抗样本、分布偏移等鲁棒性评估。
- **模型规模限制**：因资源有限，未在30B以上参数模型上实验，大规模模型上的扩展性有待验证。
- **路由机制简单**：软路由虽稳定，但可能限制对极端稀疏场景（如超多任务）的适应能力；专家数增加后性能提升边际递减（某些任务甚至下降，如CoLA）。
- **对比方法覆盖**：虽然对比了多种PEFT和MoE-PEFT方法，但未包含最新的低秩分解或多阶段微调方法（如VeRA、SSF等），时间覆盖可能不够全面。
- **超参搜索深度**：敏感性分析仅在两个任务上进行，更多任务上的超参鲁棒性未报告。

（完）
