---
title: "AEA: Adaptive Expert Allocation Improves Sentence Embeddings from Mixture-of-Experts LLM"
title_zh: AEA：自适应专家分配提升混合专家大模型的句子嵌入
authors: "Shufan Yang, Zifeng Cheng, Zhiwei Jiang, Qingfeng Qi, Yafeng Yin, Cong Wang, Ao Zhou, Qing Gu"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-long.1331.pdf"
tags: ["query:moe-special"]
score: 7.0
evidence: 逐层与逐token的自适应专家分配用于句子嵌入
tldr: 本文观察到MoE模型中不同层和不同token对专家需求不同，提出自适应专家分配方法：根据层内专家同质性和token贡献不平衡，动态调整每层和每token的专家数量。无需额外训练即可从MoE LLM中提取更优质的句子嵌入，显著提升了下游任务性能。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1331/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 806, \"height\": 649, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1331/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 799, \"height\": 332, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1331/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1645, \"height\": 602, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1331/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 679, \"height\": 359, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1331/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 758, \"height\": 350, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1331/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 761, \"height\": 408, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1331/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 765, \"height\": 607, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1331/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 764, \"height\": 623, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1331/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1641, \"height\": 577, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1331/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1642, \"height\": 578, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1331/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1622, \"height\": 576, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1331/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1618, \"height\": 777, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1331/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1647, \"height\": 303, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1331/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1643, \"height\": 326, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1331/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 762, \"height\": 364, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1331/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 725, \"height\": 428, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1331/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1643, \"height\": 454, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1331/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1645, \"height\": 554, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1331/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 798, \"height\": 614, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1331/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 798, \"height\": 544, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1331/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 798, \"height\": 485, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1331/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 800, \"height\": 507, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1331/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 794, \"height\": 223, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1331/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1645, \"height\": 285, \"label\": \"Table\"}]"
motivation: MoE提取句子嵌入时固定分配专家数，忽略了层间和token间异质性。
method: 提出自适应专家分配，根据层内专家同质性和token贡献动态调整专家预算。
result: 无需训练即可提升句子嵌入质量，多个任务性能显著提高。
conclusion: 自适应专家分配能更高效利用MoE容量，提升嵌入表示能力。
---

## Abstract
Extracting embeddings directly from Mixture-of-Experts (MoE) models is a promising yet underexplored direction that requires no additional data or fine-tuning. While previous studies have utilized semantic compression prompts or expert routing information to improve sentence embeddings, they typically allocate a fixed number of experts uniformly across all layers and tokens, ignoring inter-layer and inter-token heterogeneity. In this work, we identify two key observations in MoE models: (1) layer-wise variations in expert homogeneity, suggesting that different layers require different expert budgets, and (2) token-wise contribution imbalance, indicating that different tokens should also be allocated different numbers of experts. To address these issues, we propose an Adaptive Expert Allocation (AEA) framework that dynamically performs both layer-wise and token-wise expert allocation to enhance embedding quality. Specifically, AEA allocates fewer experts to layers with higher homogeneity and to tokens with lower attention importance, where layer-wise homogeneity is determined by the similarity among embeddings produced by the experts in each layer. Notably, our method is plug-and-play, seamlessly integrates with existing prompt engineering methods, and introduces no additional time overhead. Experiments on the STS tasks demonstrate that AEA consistently improves embedding quality across multiple MoE models.

---

## 论文详细总结（自动生成）

好的，作为一名资深学术论文分析助手，现根据您提供的论文内容，进行结构化、深入、客观的中文总结。

## 论文总结：AEA: Adaptive Expert Allocation Improves Sentence Embeddings from Mixture-of-Experts LLM

### 1. 核心问题与整体含义（研究动机和背景）
- **研究背景：** 从大型语言模型（LLMs）中提取高质量的句子嵌入是一项基础任务。无需额外数据或微调的“零样本”方法越来越受关注。随着混合专家（MoE）架构LLMs的兴起，直接利用其内部状态提取嵌入成为一种高效、实用的方法。
- **核心问题：** **现有方法存在“专家分配不均”的问题**。无论是利用路由权重的MoEE，还是其他基于提示的方法，它们均对**所有层和所有token统一分配固定数量（Top-K）的专家**。这种方法忽略了两个关键观察：
    1.  **层间专家同质性（Layer-wise Expert Homogenization）：** MoE模型的不同层，其内部专家输出的相似度存在显著差异（如图2所示，中间层专家更多样，顶部和底部层更同质）。
    2.  **Token贡献不均衡（Token-wise Contribution Imbalance）：** 在自注意力机制中，不同token对最终语义的贡献是不均衡的（如图2所示，注意力高度稀疏，只有少数token主导信息流）。
- **根本不合理性：** 为高度冗余的层和贡献低的token分配同样多的专家是一种资源浪费，未能有效利用MoE模型的容量来提升嵌入质量。

### 2. 提出的方法论
- **核心思想：** 提出一种名为**自适应专家分配（AEA）** 的即插即用框架，动态地在**层级别**和**token级别**重新分配专家预算，以优化嵌入质量。总专家预算（L × K）保持不变，只改变分配方式。
- **关键技术细节：**
    1.  **层级别专家分配（Layer-wise Expert Allocation）：**
        - **同质性分数计算：** 首先，使用一个校准数据集（本文采用STS-B验证集）预先计算每层的专家同质性分数 **s^(ℓ)**。该分数定义为该层内所有专家输出嵌入之间的平均余弦相似度。分数越高，层内专家冗余度越高。
        - **预算重分配：** 根据同质性分数，将每层的专家数 **k^(ℓ)** 与 **(1 - s^(ℓ))** 的次幂（由缩放因子α控制）成比例地分配。冗余度高的层（s高）获得更少的专家，更多样化的层（s低）获得更多专家。
        - **预算校正与早退策略：** 通过一个迭代修正步骤确保总专家数不变。同时，采用**早退策略（Early-exit）**，从第m层（实验中确定为倒数第二层）提取嵌入，并将后续层的专家预算**再分配**到前面的层，以提升中间层的表征质量。
    2.  **Token级别专家分配（Token-wise Expert Allocation，推理时动态进行）：**
        - **Token重要性度量：** 在每个MoE层，对于当前输入序列，计算每个token i的注意力强度**a_i^(ℓ)**。这是通过取所有注意力头（h）和所有查询token（j）对该token的最大注意力得分来衡量的（`a_i^(ℓ) = max_h max_j A^(ℓ,h)_{j,i}`）。这个操作突出了最关键的交互信号。
        - **预算分配：** 将归一化后的注意力强度 **p_i^(ℓ)** 作为比例，将分配给该层的总预算 **B^(ℓ) = k^(ℓ) · T** 按比例分配给T个token，即 `~k_i^(ℓ) = floor(B^(ℓ) · p_i^(ℓ))`。这确保重要的token获得更多专家，不重要的token获得更少。
- **公式与流程要点：**
    - **层分配：** `k^(ℓ) = ... ∝ (1 - s^(ℓ))^α`，核心是成反比于同质性。
    - **Token分配：** `~k_i^(ℓ) = floor( (k^(ℓ) · T) · (a_i^(ℓ) / sum_j a_j^(ℓ)) )`，核心是正比于注意力重要性。
    - 整个AEA框架不引入额外时间开销，因为其核心逻辑（预计算层分配和计算注意力强度）计算量微乎其微，且早退策略会抵消部分计算成本。

### 3. 实验设计
- **数据集：**
    - **主要任务：** 7个语义文本相似度（STS）基准数据集：**STS 2012-2016, STS-B, SICK-R**。
    - **全面评估：** **MTEB（Massive Text Embedding Benchmark）** 基准，涵盖6大类任务：分类、聚类、句子对分类、重排序、检索、摘要等。
- **基准模型（Baselines）:**
    - **HS：** 直接提取最终层的隐藏状态（视为基准）。
    - **HS + Echo/TP：** 集成现有的无需训练的提示工程方法（重复文本、前置token）。
    - **MoEE：** 唯一针对MoE模型的训练自由嵌入提取方法，利用了路由权重（包括concat和sum两种融合方式）。
- **对比方法：** 将AEA分别与上述所有基线方法（HS, Echo, TP, MoEE）及其组合进行对比。
- **被评估的MoE模型：** 三种代表性的MoE LLMs：
    - **DeepSeekMoE-16B**
    - **Qwen1.5-MoE-A2.7B**
    - **OLMoE-1B-7B**
- **评价指标：** 主要使用**斯皮尔曼等级相关系数（Spearman's correlation）** 来衡量预测相似度与人类标注排名的相关性。

### 4. 资源与算力
- 论文明确提到，层级别专家同质性分数的计算只需要一次，**在单个V100 GPU上，在包含1500个样本的STS-B验证集上仅需1-2分钟**。
- 推理时，token级别分数的计算引入的额外成本极小（约1.5%），但由于早退策略可以抵消一部分注意力计算，整体推理时间**没有增加**。
- **（总结）** 论文并未报告模型全量微调或大型预训练实验的算力，但其提出的方法本身**计算开销极低**。

### 5. 实验数量与充分性
- **实验数量：** 非常充分。
    - **主实验：** 在3个MoE模型 * 7个STS数据集上进行，对比了多种方法组合（共约40+个配置），证明AEA的普适性。
    - **消融实验：** 分别验证了层级别和token级别分配的贡献，并对比了二者的组合效果。
    - **超参数分析：** 探索了缩放因子α和早退层m对性能的影响。
    - **假设验证：** 通过“反向分配”实验（给冗余层/低注意token分配更多专家）验证了其核心假设的正确性。
    - **泛化性测试：**
        - 在不同Prompt设置下（Pretended CoT, Knowledge）测试AEA的有效性。
        - 在更广泛的**MTEB**基准上进行了全面评估。
- **客观性与公平性：** 实验设计公平，对比了所有相关基线（包括专为MoE设计的方法和即插即用的Prompt方法），并在多个模型上验证。消融实验和假设验证实验增强了结果的因果性和可靠性。

### 6. 主要结论与发现
- **AEA显著提升了嵌入质量：** 在所有三个MoE模型和所有STS基准测试中，AEA持续优于所有基线方法。例如，在DeepSeekMoE-16B上，`HS + AEA` 相对于 `HS` 平均提升了**11.52**个点。
- **AEA可以与现有方法互补：** 它可以无缝集成到Echo、TP和Prompt方法中，进一步提升性能。
- **层级别分配是关键：** 消融实验显示，单独的层级别分配带来的性能提升（+11.25）远大于token级别（+0.78），说明预算在深度上的重新分配是主要驱动力。
- **资源利用率更优：** 相比于直接使用路由权重（MoEE），AEA通过更优的专家分配，使得仅依赖隐藏状态就能达到甚至超越结合了路由权重的表现，简化了流程。
- **早退策略有效：** 确认了从倒数第二层提取嵌入比从最后一层提取效果更好。

### 7. 优点
- **方法论创新：** 首次系统性地揭示了MoE模型中“层间专家冗余”和“token间贡献不均”两大问题，并据此提出了自适应分配策略，思想新颖且合理。
- **即插即用，高效实用：** 无需对模型进行任何微调或训练，仅通过改变推理时的专家选择策略即可提升性能。计算开销几乎为零，具有很强的实用价值。
- **通用性强：** 不依赖特定模型架构或任务，在多个不同大小的MoE模型和不同基准（STS, MTEB）上都表现出一致且显著的提升。
- **假设验证严谨：** 通过“反向分配”实验，有力地验证了其设计假设的核心逻辑，使结论更具说服力。
- **实验设计全面：** 不仅在主任务上表现优异，还在MTEB上进行了广泛评估，并做了充分的消融、泛化性和假设验证实验。

### 8. 不足与局限
- **对闭源模型的依赖：** 该方法需要访问MoE模型中**每一层的专家输出**和**注意力映射**。对于一些仅提供API接口的封闭源（closed-source）MoE LLMs（如GPT-4等），无法直接应用，因为无法获取这些中间状态。
- **评估范围有限：** 实验主要集中在**英文**基准测试上。该方法在多语言场景下的有效性尚待探索和验证。
- **校准数据集的依赖：** 层级别分配的计算依赖于一个校准数据集（STS-B验证集）。虽然实验证明其在不同任务间有良好的泛化性，但若该数据集与下游任务领域差异过大，其最优性是否会受影响，文中未做深入探讨。

（完）
