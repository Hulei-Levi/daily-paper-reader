---
title: "ProtSyntax: a protein large language model for decoding post-translational modification syntax and function"
title_zh: ProtSyntax：一种用于解码翻译后修饰语法和功能的蛋白质大语言模型
authors: "Lin, Y."
date: 2026-07-21
pdf: "https://www.biorxiv.org/content/10.64898/2026.07.18.739331v1.full.pdf"
tags: ["query:moe-special"]
score: 8.0
evidence: 使用稀疏混合专家架构构建蛋白质语言模型
tldr: "翻译后修饰（PTM）通过多重依赖调控蛋白质功能，但现有模型独立预测位点且未连接功能后果。本文提出PTM中心语言模型ProtSyntax，基于425万样本覆盖40种PTM，集成双向长程建模与几何门控注意力，通过自适应多目标学习耦合PTM语法与功能。在40个基准上MCC和AP提升12.7%和10.7%，能区分真实位点与诱饵、迁移至稀有PTM、关联酶动力学变化并识别疾病相关破坏。该模型为解码蛋白质组PTM调控提供可解释框架。"
source: biorxiv
selection_source: fresh_fetch
figures_json: "[{\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-07-18-739331-v1/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1538, \"height\": 1169, \"label\": \"Figure\"}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-07-18-739331-v1/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1558, \"height\": 1204, \"label\": \"Figure\"}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-07-18-739331-v1/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1477, \"height\": 1714, \"label\": \"Figure\"}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-07-18-739331-v1/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1511, \"height\": 1427, \"label\": \"Figure\"}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-07-18-739331-v1/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1509, \"height\": 1749, \"label\": \"Figure\"}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-07-18-739331-v1/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1511, \"height\": 1663, \"label\": \"Figure\"}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-07-18-739331-v1/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1505, \"height\": 1173, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/biorxiv/biorxiv-10-64898-2026-07-18-739331-v1/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1501, \"height\": 1255, \"label\": \"Table\"}, {\"url\": \"assets/tables/biorxiv/biorxiv-10-64898-2026-07-18-739331-v1/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1528, \"height\": 1101, \"label\": \"Table\"}]"
motivation: 现有模型独立预测PTM位点，未整合序列-结构-修饰依赖及功能后果，缺乏全局解码能力。
method: ProtSyntax采用稀疏混合专家架构，融合双向长程建模与几何门控注意力，并通过自适应多目标学习联合优化残基与蛋白质级目标。
result: "在40个PTM基准上MCC和AP提升12.7%和10.7%，可区分真实与诱饵位点、迁移至稀有PTM、恢复串扰并关联酶动力学与疾病。"
conclusion: ProtSyntax为解码蛋白质组范围PTM调控提供可解释框架，连接修饰语法与功能后果及疾病关联。
---

## 摘要
翻译后修饰（PTM）通过残基化学性质、序列背景、三维微环境及修饰状态之间的依赖性调控蛋白质功能，但大多数预测模型独立建模位点，且未将修饰倾向与功能后果联系起来。在此，我们提出ProtSyntax，一种以PTM为中心的蛋白质语言模型，该模型在涵盖40种PTM类别的425万个样本上训练，并在激酶特异性、PTM串扰和酶动力学方面进行监督。ProtSyntax采用稀疏混合专家架构，整合了双向长程建模与几何门控注意力，并使用自适应多目标学习将残基水平的PTM语法与蛋白质水平功能耦合。在40个PTM位点基准测试中，相较于最佳基线模型，ProtSyntax的平均MCC和AP分别提高了12.7%和10.7%。它还能区分真实位点与结构不相容的基序诱饵、迁移至稀有PTM、恢复串扰、将PTM扰动与酶动力学变化联系起来，并识别与疾病相关的PTM异常。综上，ProtSyntax为解码整个蛋白质组中的PTM调控提供了一个可解释的框架。

## Abstract
Post-translational modifications (PTMs) regulate protein function through dependencies among residue chemistry, sequence context, three-dimensional microenvironments and modification states, yet most predictors model sites independently and do not connect modification propensity to functional consequences. Here we present ProtSyntax, a PTM-centered protein language model trained on 4.25 million examples spanning 40 PTM classes and supervised for kinase specificity, PTM crosstalk and enzyme kinetics. ProtSyntax integrates bidirectional long-range modeling with geometry-gated attention in a sparse mixture-of-experts architecture and uses adaptive multi-objective learning to couple residue-level PTM syntax to protein-level function. Across 40 PTM-site benchmarks, ProtSyntax improved mean MCC and AP by 12.7% and 10.7%, respectively, relative to the best-performing baselines. It also distinguished authentic sites from structurally incompatible motif decoys, transferred to rare PTMs, recovered crosstalk, linked PTM perturbations to enzyme-kinetic changes and identified disease-associated PTM disruptions. Together, ProtSyntax provides an interpretable framework for decoding PTM regulation across the proteome.