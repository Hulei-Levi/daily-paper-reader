---
title: "CoMoL: Efficient Mixture of LoRA Experts via Dynamic Core Space Merging"
title_zh: CoMoL：通过动态核心空间合并的高效LoRA专家混合
authors: "Jie Cao, Zhenxuan Fan, Zhuonan Wang, Tianwei Lin, Ziyuan Zhao, Rolan Yan, Wenqiao Zhang, Feifei Shao, Hongwei Wang, Jun Xiao, Siliang Tang"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.811.pdf"
tags: ["query:moe-special"]
score: 6.0
evidence: 基于核心空间专家和路由的MoE-LoRA框架
tldr: 本文针对MoE-LoRA架构中参数效率低和适应粗粒度的问题，提出核心空间混合LoRA（CoMoL）框架。每个专家存储在紧凑的核心矩阵中，通过核心空间路由实现细粒度适应，同时保持专家多样性。实验表明CoMoL在参数效率和下游任务性能上均优于现有方法。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.811/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1640, \"height\": 453, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.811/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1662, \"height\": 417, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.811/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1517, \"height\": 342, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.811/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1652, \"height\": 407, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.811/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1653, \"height\": 409, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.811/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1675, \"height\": 585, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.811/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 797, \"height\": 654, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.811/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 818, \"height\": 435, \"label\": \"Table\"}]"
motivation: MoE-LoRA存在专家参数冗余和实例级路由粗粒度的问题。
method: 提出核心空间专家和核心空间路由，每个专家用紧凑核心矩阵表示，路由在核心空间进行。
result: 在参数更少的情况下达到更好或相当的性能，专家多样性保持。
conclusion: 核心空间方法有效平衡了MoE-LoRA的参数效率与专家多样性。
---

## Abstract
Large language models (LLMs) achieve remarkable performance on diverse downstream and domain-specific tasks via parameter-efficient fine-tuning (PEFT). However, existing PEFT methods, particularly MoE-LoRA architectures, suffer from limited parameter efficiency and coarse-grained adaptation due to the proliferation of LoRA experts and instance-level routing. To address these issues, we propose Core Space Mixture of LoRA ( CoMoL ), a novel MoE-LoRA framework that incorporates expert diversity, parameter efficiency, and fine-grained adaptation. Specifically, CoMoL introduces two key components: core space experts and core space routing. Core space experts store each expert in a compact core matrix, preserving diversity while controlling parameter growth. Core space routing dynamically selects and activates the appropriate core experts for each token, enabling fine-grained, input-adaptive routing. Activated core experts are then merged via a soft-merging strategy into a single core expert, which is combined with a shared LoRA to form a specialized LoRA module. Besides, the routing network is projected into the same low-rank space as the LoRA matrices, further reducing parameter overhead without compromising expressiveness. Extensive experiments demonstrate that CoMoL retains the adaptability of MoE-LoRA architectures while achieving parameter efficiency comparable to standard LoRA, consistently outperforming existing methods across multiple tasks. Our code is available at https://github.com/DCDmllm/CoMoL .

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

大语言模型（LLM）通过参数高效微调（PEFT）适应下游任务取得了显著成功。然而，现有PEFT方法，尤其是混合专家（MoE）与LoRA结合的架构（MoE-LoRA），存在两大关键缺陷：
- **参数效率低**：MoE-LoRA引入了大量LoRA专家和路由网络，导致可训练参数膨胀（通常为标准LoRA的N倍），背离了PEFT的初衷。
- **适应粗粒度**：多数方法采用实例级路由（一个样本共享同一个路由选择），而非token级路由，无法对序列内不同token进行差异化适应，限制了模型表达能力。

论文提出**CoMoL（Core Space Mixture of LoRA）**，旨在同时实现**专家多样性**、**参数高效**和**细粒度自适应**，推动MoE-LoRA向更实用、更高效的方向发展。

### 2. 论文提出的方法论

#### 核心思想
将每个LoRA专家解耦为**共享的奇异子空间**（U_B, V_A^T）和**专家特定的紧凑核心矩阵**（M_i ∈ R^{r×r}）。专家多样性完全由核心矩阵承载，而共享矩阵在所有专家间共用。通过**软合并策略**在核心空间内完成专家融合，实现token级路由，同时保持计算量接近单个LoRA。

#### 关键技术细节
1. **核心空间专家**  
   对标准LoRA的权重更新ΔW = BA进行SVD分解：
   \[
   B = U_B \Sigma_B V_B^T,\quad A = U_A \Sigma_A V_A^T
   \]
   定义核心矩阵：
   \[
   M = \Sigma_B V_B^T U_A \Sigma_A \in \mathbb{R}^{r \times r}
   \]
   则ΔW = U_B M V_A^T。CoMoL中共享U_B和V_A^T（在训练时微调），每个专家仅保留M_i。参数量从O((m+n)r)降为O(r^2)，当r ≪ m,n时接近标准LoRA。

2. **核心空间路由（Core Space Routing）**  
   将输入x投影到低秩空间：\(\hat{x} = V_A^T x \in \mathbb{R}^r\)，作为路由网络的输入。路由网络输出权重G(\(\hat{x}\)) ∈ ℝ^N，用于软合并核心矩阵：
   \[
   M_{\text{merged}} = \sum_{i=1}^N G(\hat{x})_i M_i
   \]
   最终输出：
   \[
   h = Wx + U_B M_{\text{merged}} \hat{x}
   \]
   路由网络参数量从O(N·n)降为O(N·r)，显著减参。

3. **Token级软合并优势**  
   利用矩阵乘法分配律，先合并小尺寸核心矩阵，再执行一次U_B和V_A^T的运算，避免了对每个专家计算高维输出的开销。FLOPs从输出级融合的O(N·r·(2n+r))降为O(r·(2n+r) + r^2(N-1))，几乎与单个LoRA持平，且保留了token级动态性。

### 3. 实验设计

#### 任务与数据集
- **数学推理**：训练集Math14k（GSM8K+AQuA的子集加CoT），测试集包括GSM8K、SVAMP、MultiArith、AddSub、AQuA、SingleEq。
- **代码生成**：训练集CodeAlpaca-20k，测试集HumanEval（pass@1,5,10）。

#### 基准模型
- **Qwen3-8B、Qwen3-14B**（数学推理+代码）
- **Llama3.1-8B**（代码生成）

#### 对比方法
- 标准LoRA
- 软加权MoE-LoRA：MoLoRA、HydraLoRA
- 稀疏MoE-LoRA：MoLA、AdaMoLE、SparseMoA
- 其他LoRA变体：DenseLoRA、FlyLoRA
- 消融变体：CoMoL w/o CR（不使用核心空间路由）

#### 实验设置
- 所有方法使用统一框架（Transformers），相同超参配置。
- LoRA rank=8（除标准LoRA设rank=16），专家数N=8/4（根据不同模型内存限制）。
- 数学推理训练1 epoch，代码生成调优5 epoch（Qwen3-8B）或1 epoch（Llama3.1-8B）以选出最优检查点。
- 报告三次随机种子的均值与标准差。

### 4. 资源与算力

文中**未明确说明**使用的GPU型号、数量以及训练硬件的具体配置。仅在第4.5节给出了训练和推理的**wall-clock时间**（例如，在CodeAlpaca-20k上，batch size=1，CoMoL训练1 epoch耗时约2小时19分；双卡？未说明）。因此无法确切分析其算力需求，但相较于稀疏MoE方法（MoLA、AdaMoLE），CoMoL的训练时间可减少约3–4倍，效率优势明显。

### 5. 实验数量与充分性

- 实验涵盖**两个任务领域**（数学推理、代码生成），**3个骨干模型**（Qwen3-8B/14B、Llama3.1-8B），**6种数学测试集**，**2种代码评价指标**（pass@1/5/10）。
- 执行了**缩放实验**（不同rank、不同专家数量）和**计算效率分析**（全方法wall-clock时间对比）。
- 消融实验（CoMoL vs CoMoL w/o CR）清晰展示了核心空间路由的贡献。
- 所有对比方法均在同一框架下实现，超参尽可能一致，**公平性较好**。
- **充分性评价**：实验设计较为全面，覆盖了不同模型规模、任务类型、专家数量、rank变化，统计意义上（均值和标准差）可靠。但**缺乏自然语言理解、翻译、对话等常见NLP下游任务**的评估，对方法泛化性的验证仍有限。

### 6. 论文的主要结论与发现

1. CoMoL在参数效率接近标准LoRA（参数量约1×）的情况下，**显著优于**所有对比的MoE-LoRA方法，在数学推理上比LoRA平均提升1.7个百分点，比MoLoRA（参数多4倍）更高。
2. 专家数量从8增至64时，性能并未持续提升，说明在数据有限时存在“专家饱和”现象，并非越多越好。
3. 核心空间路由有效减少了路由参数，且不损失性能。
4. 计算效率方面，训练时间约为其他MoE-LoRA的1/2至1/4，推理延迟与标准LoRA相当。
5. 方法具有跨模型、跨任务的鲁棒性，在Qwen3和Llama3.1上均稳定领先。

### 7. 优点：方法或实验设计上的亮点

- **创新性强**：首次提出在LoRA的核心空间内进行专家存储、路由和软合并，从根本上解决了MoE-LoRA的参数量和计算量膨胀问题。
- **参数效率与专家多样性兼得**：每个核心矩阵仅需r²参数（r≤8），远小于完整LoRA专家，且通过不同核心矩阵保持专家差异。
- **细粒度适应**：实现token级路由，比实例级路由（如SMEAR）更具表达力。
- **实验严谨**：多随机种子、多模型、多任务、多种对比方法，且统一框架下进行，结果可信。
- **效率实测**：提供了wall-clock时间对比，而非仅理论FLOPs，更具工程参考价值。
- **代码开源**：提升可复现性。

### 8. 不足与局限

- **任务覆盖不全**：仅测试了数学推理和代码生成，缺乏对通用自然语言理解、翻译、问答等常见NLP任务的评估，泛化性有待进一步验证。
- **缺乏容量与泛化边界的系统分析**：论文自身指出当前缺乏PEFT方法学习能力的系统性基准，如FlyLoRA在不同模型上表现差异巨大，CoMoL是否对模型族敏感尚不清楚。
- **专家数量饱和现象**：在数据量有限的设定下，增加专家数并未提升性能，说明方法受数据规模制约较大。
- **秩r的选择敏感性**：核心空间尺寸由LoRA秩r决定，实验仅固定r=8，未探讨r变化对专家特性的影响。
- **路由信息损失风险**：将路由输入压缩到低维核心空间（V_A^T x）可能导致信息丢失，尽管实验表明无显著下降。
- **可解释性不足**：核心矩阵M_i的物理意义不明确，专家多样化难以直观解释。
- **硬件资源未披露**：缺少训练GPU型号和数量，难以评估方法在不同规模部署下的复现成本。

（完）
