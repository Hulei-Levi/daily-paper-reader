---
title: Unifying multimodal single-cell data with a mixture-of-experts β-variational autoencoder framework
title_zh: 利用混合专家β变分自编码器框架统一多模态单细胞数据
authors: "Ashford, A. J., Enright, T., Somers, J., Nikolova, O., Demir, E."
date: 2026-07-21
pdf: "https://www.biorxiv.org/content/10.1101/2025.02.28.640429v3.full.pdf"
tags: ["query:moe-special"]
score: 9.0
evidence: 采用混合专家VAE进行多模态整合
tldr: 多模态单细胞数据整合面临模态不匹配、稀疏性和队列覆盖不均等挑战。UniVI提出混合专家β-VAE框架，学习共享潜空间同时保留模态特定结构，通过对称跨模态对齐目标实现无需特征链接图的配对测量整合。在RNA-蛋白、RNA-染色质及三模态数据上，UniVI产生连贯嵌入，提升标签转移准确率，支持跨模态重建与去噪。在急性髓系白血病镶嵌设计中，利用配对RNA-蛋白桥接锚定独立队列，通过突变感知微调揭示基因型相关邻域，为灵活可解释的多模态整合提供方案。
source: biorxiv
selection_source: fresh_fetch
figures_json: "[{\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-02-28-640429-v3/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1728, \"height\": 2303, \"label\": \"Figure\"}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-02-28-640429-v3/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1765, \"height\": 2122, \"label\": \"Figure\"}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-02-28-640429-v3/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1704, \"height\": 2263, \"label\": \"Figure\"}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-02-28-640429-v3/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1744, \"height\": 2229, \"label\": \"Figure\"}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-02-28-640429-v3/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1600, \"height\": 2173, \"label\": \"Figure\"}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-02-28-640429-v3/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1660, \"height\": 2163, \"label\": \"Figure\"}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-02-28-640429-v3/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1691, \"height\": 2147, \"label\": \"Figure\"}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-02-28-640429-v3/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1761, \"height\": 2198, \"label\": \"Figure\"}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-02-28-640429-v3/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1717, \"height\": 2231, \"label\": \"Figure\"}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-02-28-640429-v3/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1607, \"height\": 2055, \"label\": \"Figure\"}]"
motivation: 现有多模态整合方法依赖预定义特征链接或参考图谱，难以应对模态不匹配和稀疏性，亟需灵活统一的框架。
method: UniVI采用混合专家β-VAE架构，包含模态特定编码/解码器和共享潜先验，通过对称跨模态对齐损失实现一致性整合。
result: 在CITE-seq、10x Multiome、SHARE-seq等数据中，UniVI生成连贯嵌入，标签转移准确率提升，并实现跨模态重建与去噪。
conclusion: UniVI提供可扩展且解释性强的多模态整合框架，支持配对、三模态及镶嵌设计，并适用于参考到查询的投影。
---

## 摘要
多模态单细胞分析技术可测量细胞状态的互补层次，但整合过程受到模态不匹配、稀疏性和队列覆盖不均的阻碍。我们提出UniVI（统一变分推断），一个可扩展的混合专家β变分自编码器，在学习共享潜在空间的同时保留模态特异性结构。UniVI将模态特异性编码器/解码器与共享潜在先验和对称跨模态对齐目标相结合，无需精心设计的特征链接图或预注释参考图谱即可实现配对测量的一致整合；当标签可用时可添加可选监督头。在跨越人类PBMC和小鼠背部皮肤（一种具有连续分化层次的非造血组织）的配对RNA-蛋白（CITE-seq）和RNA-染色质（10x Multiome, SHARE-seq）数据上，UniVI产生连贯的嵌入，改善标签转移，并实现跨模态重建和去噪。扩展到三模态测量，UniVI在RNA、染色质可及性和表面蛋白（TEA-seq）之间保持稳健的三路对齐，并在配对scNMT-seq小鼠原肠胚概念验证中，在β-二项似然下适应DNA甲基化。在严重的细胞类型不平衡和存在模态专属群体时，性能优雅地下降。在急性髓系白血病马赛克设计中，配对的RNA-蛋白桥接锚定独立的仅RNA和蛋白+基因型队列，揭示了与基因型相关的邻域，并通过突变感知微调得到锐化。因此，UniVI为配对、三模态和马赛克研究设计中的多模态整合提供了一个灵活、可解释的框架，并支持部分观测研究中的实用参考到查询投影。

## Abstract
Multimodal single-cell assays profile complementary layers of cell state, but integration is complicated by modality mismatch, sparsity, and uneven cohort coverage. We present UniVI (\Unified Variational Inference), a scalable mixture-of-experts {beta}-variational autoencoder that learns a shared latent space while preserving modality-specific structure. UniVI couples modality-specific encoders/decoders with a shared latent prior and a symmetric cross-modal alignment objective, enabling consistent integration of paired measurements without curated feature-link graphs or pre-annotated reference atlases; optional supervised heads can be added when labels are available. Across paired RNA--protein (CITE-seq) and RNA--chromatin (10x Multiome, SHARE-seq) data spanning human PBMCs and mouse back skin---a non-hematopoietic tissue with continuous differentiation hierarchies---UniVI produces coherent embeddings, improves label transfer, and enables cross-modal reconstruction and denoising. Extending to tri-modal measurements, UniVI maintains robust three-way alignment among RNA, chromatin accessibility, and surface proteins (TEA-seq), and accommodates DNA methylation in a paired scNMT-seq mouse gastrulation proof-of-concept under beta-binomial likelihoods. Performance degrades gracefully under severe cell-type imbalance and in the presence of modality-exclusive populations. In an acute myeloid leukemia mosaic design, a paired RNA--protein bridge anchors independent RNA-only and protein+genotype cohorts, revealing genotype-associated neighborhoods that sharpen with mutation-aware fine-tuning. UniVI thus provides a flexible, interpretable framework for multimodal integration across paired, tri-modal, and mosaic study designs and supports practical reference-to-query projection in partially observed studies.

---

## 论文详细总结（自动生成）

### 1. 核心问题与整体含义（研究动机和背景）

- **研究动机**：多模态单细胞测序技术（如CITE-seq、10x Multiome、TEA-seq等）能够同时测量细胞的不同分子层次（如RNA、蛋白质、染色质可及性、DNA甲基化），但整合这些数据面临三大挑战：**模态不匹配**（各模态特征维度不同）、**数据稀疏性**（尤其是染色质和甲基化数据）、**队列覆盖不均**（不同实验可能只测量部分模态）。现有方法要么依赖预定义的特征链接图，要么需要注释好的参考图谱，缺乏灵活统一的框架。
- **整体含义**：UniVI旨在提供一个**可扩展、解释性强**的整合框架，能够处理**配对、三模态和镶嵌（mosaic）设计**，并支持**参考到查询的投影**，从而揭示不同模态下细胞状态的一致性表征。

### 2. 方法论：核心思想、关键技术细节

- **核心思想**：采用**混合专家（Mixture-of-Experts）β-VAE**架构，学习一个共享的潜在空间，同时保留模态特异性结构。
- **关键技术细节**：
  - **架构**：每个模态配备专用的编码器和解码器（即“专家”），所有模态共享一个潜在先验分布（通常为标准正态分布）。
  - **对齐目标**：引入**对称跨模态对齐损失**（symmetric cross-modal alignment objective），使不同模态的编码表示在潜在空间中一致，无需手动设计特征链接图或预注释参考。
  - **可选监督头**：当细胞类型标签可用时，可添加监督分类头辅助学习。
  - **似然函数**：对不同模态采用合适的分布假设：RNA用负二项或Poisson，蛋白质用正态或负二项，染色质用Bernoulli或负二项，DNA甲基化用β-二项分布（在scNMT-seq概念验证中）。
- **流程说明**：输入各模态数据经过各自编码器得到潜在表示，通过共享先验和跨模态对齐损失迫使它们对齐，解码器再分别重建原始数据。训练完成后，任意模态的细胞均可映射到统一潜在空间，实现整合、标签转移和跨模态重建。

### 3. 实验设计：数据集、基准与对比方法

- **数据集与场景**：
  - **配对RNA-蛋白**：CITE-seq（人类PBMC）。
  - **配对RNA-染色质**：10x Multiome、SHARE-seq（人类PBMC和小鼠背部皮肤——一种具有连续分化层次的非造血组织）。
  - **三模态**：TEA-seq（RNA、染色质可及性、表面蛋白）。
  - **配对scNMT-seq**：小鼠原肠胚（RNA、DNA甲基化、染色质可及性概念验证）。
  - **镶嵌设计**：急性髓系白血病（AML）队列，包含配对的RNA-蛋白桥接数据、仅RNA数据和蛋白+基因型数据，用于桥接整合。
- **基准与对比方法**：
  - 对比方法未在摘要中明确列出，但根据方法定位（无需特征链接图），可能包括传统VAE、β-VAE、以及现有的多模态整合工具如Seurat的Weighted Nearest Neighbor (WNN）、MIRA、scVI、MultiVI等（论文正文应有详细对比，摘要未提及）。
- **实验评估指标**：嵌入的连贯性（通过可视化）、标签转移准确率、跨模态重建与去噪效果。

### 4. 资源与算力

- **文中未明确说明**使用的GPU型号、数量或训练时长。摘要和元数据中均无相关提及。需要指出这一点。

### 5. 实验数量与充分性

- **实验数量**：覆盖了多种模态组合（RNA-蛋白、RNA-染色质、三模态、配对+镶嵌）、多个数据集（PBMC、小鼠背部皮肤、小鼠原肠胚、AML）、以及概念验证（DNA甲基化）。还进行了**镶嵌设计**中的桥接整合和突变感知微调。
- **充分性与客观性**：实验场景较全面，包括造血和非造血组织、连续分化、严重细胞类型不平衡和模态专属群体（performance gracefully degrades）。但对比方法在摘要中未列出，消融实验（如去掉对齐损失、去掉MoE等）也未提及，因此客观性和公平性需依赖全文的详细比较。

### 6. 论文的主要结论与发现

- **主要发现**：
  1. UniVI生成连贯的潜在嵌入，改善标签转移准确率，实现跨模态重建和去噪。
  2. 在三模态测量中维持稳健的三路对齐。
  3. 适应DNA甲基化（β-二项似然）。
  4. 在细胞类型严重不平衡或存在模态专属群体时，性能优雅下降（即仍具一定鲁棒性）。
  5. 在AML镶嵌设计中，通过配对RNA-蛋白桥接锚定独立队列，揭示了与基因型相关的邻域，并可通过突变感知微调进一步锐化。
- **结论**：UniVI提供了灵活、可解释的多模态整合框架，适用于多种研究设计，并支持部分观测数据的参考到查询投影。

### 7. 优点

- **无需预定义特征链接图或参考图谱**：降低了使用门槛。
- **混合专家架构**：保留模态特异性结构，避免过度统一。
- **对称跨模态对齐**：使不同模态对称地相互学习。
- **可扩展性强**：支持配对、三模态、镶嵌设计，且能适应不同似然函数（如β-二项用于甲基化）。
- **可解释性**：潜在空间可直接用于下游分析，且可通过突变感知微调强化特定生物学发现。

### 8. 不足与局限

- **实验覆盖**：未在更多样的组织类型或大型图谱数据集上验证，仅限于PBMC、皮肤、原肠胚和AML样本。
- **对比方法不明确**：摘要中未列出与现有方法（如Seurat WNN、MultiVI、MIRA等）的定量比较，可能削弱说服力。
- **计算资源未报告**：无法评估可扩展性。
- **局限性明确提及**：在严重细胞类型不平衡和模态专属群体存在时性能下降，但未详细讨论解决方案。
- **缺少消融实验**：未在摘要中说明对MoE组件、对齐损失、监督头等的消融研究，使得贡献点归因不够充分。

（完）
