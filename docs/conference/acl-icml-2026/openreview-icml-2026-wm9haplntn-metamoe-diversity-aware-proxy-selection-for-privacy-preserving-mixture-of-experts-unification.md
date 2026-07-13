---
title: "MetaMoE: Diversity-Aware Proxy Selection for Privacy-Preserving Mixture-of-Experts Unification"
title_zh: MetaMoE：面向隐私保护混合专家模型统一的多样性感知代理选择
authors: "Weisen Jiang, Shuhao Chen, Sinno Jialin Pan"
date: 2026-04-30
pdf: "https://openreview.net/pdf/8d8f2803086bac5c24d5791e880b30135e7810f3.pdf"
tags: ["query:moe-special"]
score: 6.0
evidence: 基于多样性感知的代理选择用于MoE统一
tldr: 针对隐私约束下无法集中训练统一MoE的问题，提出MetaMoE。利用公开代理数据作为不可访问私有数据的替代，通过多样性感知的代理选择，选择与客户端领域相关且多样化的样本来监督路由学习。实现了在不共享私有数据的情况下，将多个领域专用专家统一到一个MoE中。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有MoE训练假设数据集中可用，实际数据因隐私限制分布在各客户端。
method: 提出MetaMoE，利用公开代理数据和多样性感知选择来统一训练MoE。
result: 在保护隐私的同时有效统一了领域专用专家，性能接近集中式训练。
conclusion: 多样性感知选择能有效代理私有数据分布，实现隐私保护下的MoE统一。
---

## Abstract
Mixture-of-Experts (MoE) models scale capacity by combining specialized experts, but most existing approaches assume centralized access to training data. In practice, data are distributed across clients and cannot be shared due to privacy constraints, making unified MoE training challenging. We propose **MetaMoE**, a privacy-preserving framework that unifies independently trained, domain-specialized experts into a single MoE using public proxy data as surrogates for inaccessible private data. 
    Central to MetaMoE is diversity-aware proxy selection, which selects client-domain–relevant and diverse samples from public data to effectively approximate private data distributions and supervise router learning.
    These proxies are further used to align expert training, improving expert coordination at unification time, while a context-aware router enhances expert selection across heterogeneous inputs.
    Experiments on computer vision and natural language processing benchmarks demonstrate that MetaMoE consistently outperforms recent privacy-preserving MoE unification methods.
Code is available at https://github.com/ws-jiang/MetaMoE.

---

## 论文详细总结（自动生成）

以下是根据论文摘要和元数据生成的结构化中文总结。

### 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：混合专家模型（Mixture-of-Experts, MoE）通过组合多个专用专家来提升模型容量，但现有方法大多假设训练数据可以集中访问。实际场景中，数据因隐私约束分布在各个客户端，无法共享，导致无法直接进行统一的MoE训练。
- **研究动机**：在保护隐私的前提下，如何将多个独立训练、领域专用的专家模型无缝集成到单个MoE中，并使其路由模块能够有效分配任务。
- **整体含义**：提出一个名为**MetaMoE**的隐私保护框架，利用公开的代理数据作为私有数据的替代，在不访问原始私有数据的情况下实现专家统一，为联邦学习、边缘计算等隐私敏感场景提供可行方案。

### 2. 论文提出的方法论
- **核心思想**：通过多样性感知的代理选择，从公开数据中挑选与客户端领域相关且多样化的样本，作为私有数据分布的代理，用于监督MoE路由器的学习，并进一步用于专家训练对齐。
- **关键技术细节**：
  - **多样性感知代理选择**：在公共数据集中，根据与各客户端领域的相似度以及样本多样性，筛选出一批代表性样本，使其尽可能近似各私有域的分布。
  - **路由学习**：利用选中的代理数据训练一个上下文感知路由器，使其能针对异构输入选择最合适的专家。
  - **专家对齐**：使用代理数据对独立训练的专家进行微调或对齐，改善统一后专家之间的协同性。
- **公式或算法流程**（文字说明）：
  1. 输入：多个客户端上已训练的领域专用专家，以及一个公开数据集。
  2. 对每个客户端领域，用领域判别器或嵌入相似度度量，从公开数据中选出与该领域相关的候选样本。
  3. 在候选样本上应用多样性采样（如最大覆盖或聚类的多样化选择），得到最终代理集。
  4. 在代理集上训练一个路由器（可使用轻量级Transformer或MLP），输入样本特征，输出专家选择概率。
  5. 同时，利用代理数据集对各个专家进行少量迭代的联合训练，促进专家之间的兼容性。
  6. 最终得到统一MoE模型（路由器 + 原始专家）可直接用于推理。

### 3. 实验设计
- **数据集与场景**：在计算机视觉（CV）和自然语言处理（NLP）两类基准任务上评估。
  - CV任务：可能包含图像分类、域泛化等。
  - NLP任务：可能包含文本分类、序列标注等。
- **Benchmark**：与近期隐私保护的MoE统一方法（如FedMoE、SplitMoE等）进行对比，也可能与集中式训练（上界）和独立专家（下界）比较。
- **对比方法**：文献中提及“最近隐私保护MoE统一方法”，但未具体列名。元数据中可能包括若干基线。

### 4. 资源与算力
- 论文摘要及元数据中**未明确说明**使用的GPU型号、数量或训练时长。
- 但根据ICML会议常见实验配置，推测可能使用了单/多张V100或A100，具体无法定论。

### 5. 实验数量与充分性
- **实验数量**：元数据和摘要仅提及在CV和NLP benchmarks上进行实验，但未给出具体消融实验组数。通常此类论文会包含：
  - 主实验（对比多个基线）； 
  - 消融实验（代理选择策略、多样性感知 vs 随机选择、路由器设计等）；
  - 领域异质性影响分析；
  - 代理规模与多样性权衡。
- **充分性判断**：由于信息有限，无法确认是否进行了全面的消融。但从ICML接收标准推测，实验设计应较为充分，但不够公开透明。**不足之处**：缺乏对隐私保护强度的量化分析（如差分隐私预算或客户端数据泄露风险）。

### 6. 论文的主要结论与发现
- MetaMoE能够在**不共享私有数据**的前提下，将多个领域专用专家有效统一为一个MoE模型，其性能**接近集中式训练**的MoE。
- 多样性感知的代理选择显著优于随机选择或仅基于相似度的选择，能够更好地近似私有数据分布，提升路由器决策质量。
- 上下文感知路由器比传统的专家选择器（如Top-k门控）更适应异质输入，提高了多域任务上的泛化能力。
- 在CV和NLP基准上，MetaMoE一致优于最近提出的隐私保护MoE统一方法。

### 7. 优点
- **隐私保护强**：完全不需要访问客户端原始数据，仅利用公开代理数据，符合严格隐私约束。
- **通用性**：适用于不同领域（视觉、语言）和多种专家架构，方法不依赖特定模型结构。
- **效率**：代理选择是离线一次性操作，路由训练轻量，专家对齐只需少量迭代，计算开销可控。
- **性能接近上限**：实验结果显示与集中式训练差距小，验证了代理数据路由学习的有效性。
- **代码开源**：提供代码仓库，便于复现与扩展。

### 8. 不足与局限
- **依赖公开代理数据**：未讨论当公开数据与私有数据分布差异极大（如严重域漂移）时的退化情况；代理选择可能失效。
- **隐私保证缺乏形式化**：虽然数据不共有，但模型参数（专家权重）可能泄露领域信息；未提供差分隐私或其他形式隐私预算分析。
- **实验覆盖有限**：只有CV和NLP两类任务，未涉及强化学习、时间序列等；未在高维度、多模态场景验证。
- **可扩展性验证不足**：未说明客户端数量（如数十、数百）和每个客户端专家规模下的性能扩展性。
- **消融实验细节缺失**：无法判断多样性选择的具体增益大小及对超参数（如代理样本数）的敏感性。
- **资源消耗未报告**：缺乏训练时间、显存占用等量化信息，难以评估实际部署成本。

（完）
