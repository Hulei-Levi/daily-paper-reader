---
title: "COMPEL: Compensated Mixture-of-Experts Pruning with Expert-Layer distribution"
title_zh: COMPEL：基于专家层分布进行补偿的混合专家模型剪枝
authors: "Seohee Yoon, Yong Suk Choi"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.1521.pdf"
tags: ["query:moe-special"]
score: 7.0
evidence: 基于Fisher信息的层自适应专家剪枝
tldr: 现有MoE剪枝方法在各层采用统一策略，忽略了层间专家重要性和冗余的变化。本文提出COMPEL，通过Fisher信息估计专家重要性，实现层自适应剪枝，在保持性能的同时减少内存占用。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1521/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 814, \"height\": 323, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1521/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1627, \"height\": 632, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1521/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1608, \"height\": 673, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1521/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1670, \"height\": 1373, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1521/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1600, \"height\": 1549, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1521/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1659, \"height\": 512, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1521/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 829, \"height\": 805, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1521/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 821, \"height\": 255, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1521/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 791, \"height\": 337, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1521/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 807, \"height\": 138, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1521/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 702, \"height\": 958, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1521/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 847, \"height\": 525, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1521/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1187, \"height\": 1509, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1521/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 474, \"height\": 445, \"label\": \"Table\"}]"
motivation: 统一剪枝无法捕捉层间专家重要性差异和冗余。
method: 利用Fisher信息逐层估计专家重要性，实现层自适应专家剪枝。
result: 在多个LLM上减少了内存占用，同时保持或提升了性能。
conclusion: 层自适应剪枝优于统一剪枝，更有效地利用专家冗余。
---

## Abstract
Mixture-of-Experts (MoE) architectures have emerged as an effective approach for scaling Large Language Models (LLMs) by activating only a subset of experts during inference. Despite their computational efficiency, MoE models incur a substantial memory bottleneck from maintaining all expert parameters during inference. To address this challenge, numerous MoE pruning methods have been proposed. However, most existing methods adopt uniform pruning across layers, which fails to capture layer-wise variations in expert importance and redundancy. In this paper, we propose COmpensated MoE Pruning with Expert-Layer distribution (COMPEL). COMPEL performs layer-adaptive expert pruning by estimating expert importance using Fisher information and deriving layer importance from layer-wise outlier distributions, enabling pruning decisions that capture layer-wise heterogeneity. Furthermore, to mitigate performance degradation resulting from expert pruning, we propose a Fisher information guided expert weight compensation method. Experimental results on the Qwen1.5-MoE-A2.7B achieve near lossless performance at 25% expert pruning and maintains performance within a 4% margin even at 50% pruning. Moreover, COMPEL consistently outperforms existing pruning methods while substantially reducing inference latency and peak GPU memory usage.

---

## 论文详细总结（自动生成）

# 论文详细总结：COMPEL: Compensated Mixture-of-Experts Pruning with Expert-Layer distribution

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **背景**：混合专家（MoE）架构通过仅激活部分专家来降低大语言模型（LLM）的推理计算量，但推理时仍需将所有专家参数加载到内存中，导致严重的内存瓶颈。现有MoE剪枝方法多采用**跨层统一剪枝**，忽略了不同层在专家重要性和冗余性上的显著差异（如层间专家相似度热图CKA显示深层专家冗余高，浅层专家差异大）。
- **核心问题**：如何实现**层自适应**的专家剪枝，并有效补偿剪枝带来的性能损失，从而在保持模型性能的同时显著降低内存占用和推理延迟。
- **整体含义**：本文提出的COMPEL将剪枝决策转化为连续优化问题，通过Fisher信息估计专家级重要性，通过激活异常值分布估计层级重要性，并引入Fisher引导的权重补偿机制，在多个MoE模型上实现了近无损的25%专家剪枝和50%剪枝下性能损失<4%，优于现有方法。

## 2. 论文提出的方法论：核心思想、关键技术细节

### 核心技术思想
将剪枝分为两个维度：**专家级重要性**（使用Fisher信息近似Hessian对角线）和**层级重要性**（使用层内激活异常值比例）。两者分别作为目标分布，通过最小化KL散度学习可参数化的重要性参数（α和β）。剪枝后，利用Fisher信息将剪除专家的权重加权补偿到幸存专家，缓解性能退化。

### 关键步骤细节
1. **专家级重要性估计**：
   - 对每个专家 `θ_{l,i}` 计算 Fisher 信息：
     ```
     Fl,i = E_{x,y~D_cal}[ ||∇θ_{l,i} log p(y|x; θ)||^2_2 ]
     ```
   - 归一化得到目标分布 `π_F`，再用可学习参数 `α` 的Softmax分布 `q_α` 拟合，通过最小化KL散度优化 `α`。

2. **层级重要性估计**：
   - 定义层内异常值比例 `D_l`：激活值大于 `M * 层均值` 的专家比例（设M=5.0）。
   - 归一化 `D_l` 得到目标分布 `π_out`，用可学习参数 `β` 的分布 `q_β` 拟合，优化 `β`。

3. **联合剪枝准则**：
   - 专家 `i` 在层 `l` 的剪枝得分 = `α_{l,i} * β_l`（乘积形式，保持层内排序，同时实现跨层比较）。

4. **Fisher引导的权重补偿**：
   - 剪枝后，对幸存专家 `j ∈ S(l)` 进行补偿：
     ```
     θ_{l,j} ← θ_{l,j} + γ * ( Fl,j / Σ_{k∈S(l)} Fl,k + ε ) * Σ_{i∈R(l)} θ_{l,i}
     ```
   - 补偿权重与幸存专家的Fisher重要性成正比，默认γ=0.1。

## 3. 实验设计

### 数据集和场景
- **校准数据集**：C4（Colossal Clean Crawled Corpus），128条序列，每条1024 tokens。
- **语言建模评估**：WikiText-2（主要PPL）、PTB、LAMBADA（附录）。
- **零样本下游任务**：8个基准（ARC-e、ARC-c、BoolQ、HellaSwag、PIQA、OBQA、RTE、WinoGrande），使用LM Evaluation Harness。

### 基准方法
- NAEE、STUN、MoE-I2、DiEP（均为最近发表的MoE剪枝/压缩方法）。

### 模型
- Qwen1.5-MoE-A2.7B（24层，60路由专家+4共享专家，总14.3B，激活2.7B）
- DeepSeek-V2-Lite（27层，64路由专家+2共享，16B总，激活2.4B）
- OLMoE-1B-7B-0924（16层，64路由专家，7B总，激活1B）

### 剪枝强度
- 0%、25%、50% 专家剪枝（按数量比例）。

## 4. 资源与算力

- **硬件**：4块 NVIDIA RTX 3080 GPU。
- **优化时长**：对Qwen1.5-MoE-A2.7B，完整COMPEL流程约0.66小时；其中优化（重要性估计）占78.8%，补偿占19.7%。
- **对比**：DiEP在相同设置下需2.21小时。
- **内存**：COMPEL修剪阶段GPU内存峰值6.20GB（低于DiEP的7.78GB，甚至低于未修剪模型的9.48GB）。

## 5. 实验数量与充分性

### 实验数量
- **主实验结果**（表1）：在3个模型×3种稀疏度×4种基线+COMPEL，共45个配置，分别报告PPL和8个任务平均分。
- **效率分析**（表2）：各模型推理TTFT、ITL、吞吐量、峰值内存。
- **消融实验**（表5）：比较仅专家级、仅层级、联合、加补偿四种配置。
- **补偿影响**（表3）：对比有/无补偿的PPL。
- **相关性分析**（图3）：α与π_F、β与π_out的Pearson相关系数（0.74和0.77）。
- **校准集大小影响**（附录表10）：1~256条序列，确定128最优。
- **专家冗余可视化**（图4）：3个层的加权余弦相似度热图。

### 充分性与公平性
- **充分**：涵盖了典型MoE模型（Qwen、DeepSeek、OLMoE），多种稀疏度，多个基线，且包含消融、效率、补偿必要性、参数相关性等多角度验证。
- **客观**：使用公开基准（LM Harness）和标准度量（PPL、准确率）。
- **公平**：基线方法均采用原文推荐设置或默认配置，实验环境一致。

## 6. 论文的主要结论与发现

1. **层自适应剪枝显著优于统一剪枝**：COMPEL在25%稀疏度下达到近无损（Qwen上Avg=68.34 vs 未修剪68.37），50%稀疏度下性能损失<4%（Avg=64.53）。
2. **Fisher引导补偿有效**：补偿后PPL降低（如Qwen 50%剪枝从8.97降至8.03）。
3. **推理效率大幅提升**：内存降至约0.8×，吞吐量提升约1.5×。
4. **剪枝优化成本低**：COMPEL修剪时间仅0.66小时（Qwen），远低于DiEP的2.21小时。
5. **专家冗余随层加深而增加**：热图显示深层专家相似度更高，验证了层自适应剪枝的必要性。

## 7. 优点：方法或实验设计上的亮点

- **方法创新点**：
  - 将剪枝度量为**连续优化问题**（KL散度拟合），比硬阈值或贪心策略更灵活。
  - 联合考虑**专家级和层级**重要性，利用Fisher信息≈Hessian近似，计算高效。
  - 提出**补偿机制**，利用Fisher重要性加权分配剪除专家的参数，而非简单丢弃。
- **实验亮点**：
  - 在多模型、多稀疏度下对比多个最新基线，公平且全面。
  - 通过Pearson相关性验证了学习的重要性参数与目标分布对齐良好。
  - 详细分析了校准集大小、超参数(M, γ)的影响。

## 8. 不足与局限

- **实验覆盖有限**：仅测试了总参数量≤16B的MoE模型，未在更大规模（如Mixtral 8x7B、DeepSeek-V2原始版）上验证，泛化性存疑。
- **缺乏联合微调**：未对学习到的α、β与模型权重进行联合微调，可能限制了潜在性能提升。
- **补偿为启发式**：Fisher引导的补偿是基于常识的加权平均，而非基于二阶优化的OBS精确解（作者承认MoE条件下难以直接应用OBS），可能无法完全恢复信息。
- **校准依赖性**：重要性估计依赖于有限校准数据（128条C4序列），可能对分布外数据鲁棒性不足。
- **未讨论路由器的剪枝**：仅移除专家，未考虑对路由器进行相应调整，可能导致路由负载不均。

（完）
