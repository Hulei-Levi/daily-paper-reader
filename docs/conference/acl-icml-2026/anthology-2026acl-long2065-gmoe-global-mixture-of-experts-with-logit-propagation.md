---
title: "GMoE: Global Mixture of Experts with Logit Propagation"
title_zh: GMoE：基于logit传播的全局混合专家
authors: "Geonwoo Hong, Taehwan Kim"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-long.2065.pdf"
tags: ["query:moe-special"]
score: 6.0
evidence: 稀疏MoE架构采用全局专家减少层间冗余
tldr: 本文针对稀疏MoE参数量和冗余大的问题，提出GMoE架构：全局专家跨层共享，每层仅保留一个局部专家进行层特化。同时引入基于GRU的全局路由器。该设计显著减少参数，缓解层间冗余，并在多项任务上达到竞争性能。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.2065/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1374, \"height\": 722, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.2065/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 801, \"height\": 234, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.2065/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 776, \"height\": 227, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.2065/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1463, \"height\": 1359, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.2065/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1551, \"height\": 1361, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.2065/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1538, \"height\": 193, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.2065/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 803, \"height\": 333, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.2065/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 760, \"height\": 231, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.2065/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 828, \"height\": 885, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.2065/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 487, \"height\": 1049, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.2065/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1137, \"height\": 229, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.2065/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1092, \"height\": 233, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.2065/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 804, \"height\": 231, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.2065/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 571, \"height\": 845, \"label\": \"Table\"}]"
motivation: 稀疏MoE每层独立专家集导致参数膨胀和层间冗余。
method: 提出GMoE，使用跨层共享的全局专家和每层一个局部专家，以及基于GRU的全局路由器。
result: 实验表明GMoE在保持性能的前提下大幅减少参数，有效缓解了冗余。
conclusion: 全局专家共享是一种有效的MoE架构优化方向，平衡了效率与性能。
---

## Abstract
Sparse Mixture of Experts (SMoE) architectures reduce computational cost by activating only a subset of experts per token, yet they often retain large memory footprints and exhibit significant redundancy, both within and across layers. We propose GMoE, a sparse MoE architecture designed to explicitly address these inefficiencies. Instead of maintaining separate expert sets for each layer, GMoE uses Global Experts shared across all layers and adds a Local Expert per layer for layer-specific adaptation. This architecture reuses Global Experts across layers, thereby mitigating inter-layer redundancy while substantially reducing model parameters. In addition, we introduce a Global Router with a GRU-based recurrent component shared across layers and layer-specific routing heads that propagate routing logits across layers. This routing mechanism couples routing decisions across layers, progressively refines routing paths, and helps mitigate intra-layer redundancy. Across diverse language modeling corpora and downstream benchmarks, GMoE remains competitive while using substantially fewer parameters. Routing path analyses and an ablation study show that GMoE reduces cross-layer routing concentration and increases path diversity, with the Global Experts, the Local Expert, and the Global Router all contributing to the gains. The code is available at https://github.com/GEONWOOHONG/GMoE.

---

## 论文详细总结（自动生成）

## 论文详细中文总结

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：传统稀疏混合专家（SMoE）架构虽然在每个token仅激活部分专家以降低计算成本，但存在严重的参数冗余问题：**层内冗余**（同一层的专家之间分化不足）和**层间冗余**（不同层的FFN模块学习到重复或近似的变换）。这些冗余导致模型参数量远高于有效计算多样性。
- **整体含义**：作者将层内和层间冗余的共存定义为**复合冗余（compounded redundancy）**，并指出过高的路由路径集中现象（**路径坍缩**）进一步限制了模型有效容量。本文旨在通过架构创新缓解冗余，在保持性能的同时大幅减少参数量，提升参数效率。

### 2. 论文提出的方法论

- **核心思想**：  
  - 提出 **GMoE（Global Mixture of Experts）** 架构，用**全局专家（Global Experts）** 替换每层的独立专家集，全局专家在所有层共享。  
  - 每层额外保留一个**局部专家（Local Expert）**，负责该层特有的适配，始终保持激活。  
  - 引入**全局路由器（Global Router）**，其核心是一个跨层共享的**GRU循环组件**，以及每层特有的**路由头（routing head）**，并通过**logit传播**机制将前一层的路由logit（带停止梯度）传递到当前层。

- **关键技术细节**：
  1. **全局专家与局部专家**：  
     - 全局专家 `{E1, ..., EN}` 被所有层共用，输出为 `∑ⱼ pₜⱼ⁽ˡ⁾ Eⱼ(xₜ⁽ˡ⁾) + E_local⁽ˡ⁾(xₜ⁽ˡ⁾)`，其中 `pₜ⁽ˡ⁾` 仅针对全局专家的softmax分布。  
     - 局部专家始终激活，不参与路由分布。
  2. **全局路由器**：  
     - 隐状态更新：`hₜ⁽ˡ⁾ = GRU(xₜ⁽ˡ⁾, hₜ⁽ˡ⁻¹⁾)`。  
     - 路由logit：`ℓₜ⁽ˡ⁾ = W_route⁽ˡ⁾[hₜ⁽ˡ⁾; sg(ℓ̃ₜ⁽ˡ⁻¹⁾)]`，其中 `ℓ̃ₜ⁽ˡ⁻¹⁾ = Wℓ LN(ℓₜ⁽ˡ⁻¹⁾)` 且 `sg` 为停止梯度算子。  
     - 每个token选择top-1全局专家计算，完整分布仅用于负载平衡损失。  
     - 跨层logit传播使得路由决策从前一层逐步细化，缓解路径坍缩。

- **公式简要**（文字说明）：
  - 层输出 `yₜ⁽ˡ⁾ = routed_output + local_output`。
  - 路由器通过GRU整合当前表示与前一层隐藏状态，再与停止梯度的投影logit拼接，经线性层和softmax得到路由分布。

### 3. 实验设计

- **数据集**：
  - **预训练语料**：The Pile（约825GB，22个领域），训练50B token。
  - **评估集**：CC100英文子集、OpenWebText、WikiText-103测试集（语言建模困惑度）；7个下游基准（零样本：ARC-C、ARC-E、BLiMP、HellaSwag、OBQA、PIQA；5-shot：RACE）。

- **Benchmark**：  
  - 对比方法：**Dense**、**Switch**、**Switch-SE**（Switch加每层共享专家）、**GShard**、**Hash**、**DeepSeek-MoE**。
  - 模型规模：Small（45M激活参数）、Base（124M）、Large（355M）。

- **实验设置**：
  - GPT-style decoder-only，用GPT-2 tokenizer，最大序列长度1024，训练95K步。
  - 优化：AdamW，学习率3e-4，cosine decay，负载平衡损失系数0.01，容量因子1.25。
  - GMoE在每层Transformer块都应用MoE层（为保持连续路由动态），而基线按惯例每两层应用一次MoE。

### 4. 资源与算力

- 文中明确说明：所有实验在**单节点**上使用**8张NVIDIA RTX PRO 6000 Blackwell GPU**完成。
- 未说明具体训练总时长或GPU小时数，仅提到预训练50B token耗时95K步（批大小524K tokens）。

### 5. 实验数量与充分性

- **实验数量**：
  - 语言建模：在Small/Base/Large三种规模下，对比6种基线+GMoE多个变体（GMoE-16/32/64/Max），共约30余行结果（表1）。
  - 下游基准：表2同样覆盖所有对比方法和规模。
  - 额外对比：匹配参数量（表8-9）、匹配激活参数量（表10）、Fine-grained variant（表3）。
  - 消融实验（表4）：4个消融（无局部专家、无logit传播、无路由器隐状态、每两层MoE）。
  - 路径分析（表5、图2-3）：路径熵、聚类指标、t-SNE可视化等。
  - 内存效率（表7）、负载平衡（表11）、专家计数缩放（附录G）等。

- **充分性与公平性**：  
  - 基线选择广泛，包括近期代表（DeepSeek-MoE）和经典（Switch, GShard等）。
  - 控制了模型参数量、激活参数量、训练数据量等变量，并做了匹配对比。
  - 消融完整，验证每个组件贡献。
  - 限于计算资源，最大模型仅1.9B参数且训练50B token，未在大规模（>10B）验证，存在一定局限性。

### 6. 论文的主要结论与发现

- GMoE在使用**显著更少的模型参数**（例如Large模型下仅0.26×参数量）条件下，在语言建模和下游基准上达到**与强基线相当甚至更优**的性能。
- 路径分析表明：GMoE比Switch和GShard拥有**更多样化**的路由路径（有效路径数更大），并显著降低路径集中度（Top-1路由质量从25.65%降至11.15%）。
- 路径路径语义**专门化**：同一路径内的token表示聚类更紧凑、分离度更高（kNN Purity达0.9971，远超基线）。
- 消融验证：全局专家、局部专家、logit传播、GRU状态、每层MoE应用均至关重要。

### 7. 优点

- **创新性**：首次系统性地识别并解决MoE中的“复合冗余”，提出跨层共享全局专家+logit传播的路由机制，设计巧妙且有效。
- **参数效率**：在保持或略微提升性能的同时，大幅减少模型参数和内存占用（如Large模型显存仅3.63GB，而传统MoE约12GB）。
- **分析深入**：不仅报告最终指标，还从路径坍缩、路径专门化、负载平衡等多个角度量化解释了算法优势。
- **实验严谨**：覆盖多种规模、多个数据集、多个基线、多种变体，并做消融和匹配参数对比，结论可信。

### 8. 不足与局限

- **规模局限性**：实验最大模型仅1.9B参数、50B token，远小于当前主流大语言模型（如百亿/千亿级），GMoE在大规模下的表现和scaling law尚未验证。
- **架构限制**：GMoE需在**每个Transformer块**都放置MoE层以维持连续路由动态，这与传统隔层放置MoE的习惯不同，可能增加路由开销，且无法灵活调整MoE层密度。
- **计算资源描述不完整**：未报告总训练时间或GPU小时数，不利于复现成本估算。
- **未见任务多样性限制**：下游基准以常识推理和语言理解为主，未涉及长文生成、多轮对话、代码等场景。
- **细粒度专家兼容性仅初步探究**：仅在大模型上测试了fine-grained变体，结论尚不充分。

（完）
