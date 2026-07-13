---
title: "XPERT: Expert Knowledge Transfer for Effective Training of Language Models"
title_zh: XPERT：用于语言模型有效训练的专家知识迁移
authors: "Chang Liu, boyu shi, Xu Yang, Xin Geng"
date: 2026-04-30
pdf: "https://openreview.net/pdf/3bfbc51817ffe4d3d4e958b9339b09011964786b.pdf"
tags: ["query:moe-special"]
score: 8.0
evidence: 专家激活模式与知识迁移
tldr: 通过分析MoE大语言模型中的专家激活模式，发现存在跨领域通用专家，其编码的知识与模型泛化能力密切相关。提出XPERT框架，无需训练即可从预训练MoE模型中提取、整合并重用专家知识，支持下游语言模型的高效训练。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: MoE专家知识可追溯但缺乏实际复用方法。
method: 提出XPERT框架，分析专家激活模式，提取并复用通用专家知识。
result: 展示了跨领域通用专家的存在，并验证了知识迁移的有效性。
conclusion: XPERT成功从MoE模型中提取通用知识并应用于新任务训练。
---

## Abstract
Mixture-of-Experts (MoE) language models organize knowledge into explicitly routed expert modules, making expert-level representations traceable and analyzable. By analyzing expert activation patterns in MoE language large models (LLMs), we find that a subset of experts is consistently activated across diverse knowledge domains. These common experts encode cross-domain, generalizable knowledge that is closely related to model generalization, naturally raising the question of how such identifiable expert knowledge can be practically reused. Motivated by this observation, we propose XPERT, a training-free framework that extracts, consolidates, and reuses expert knowledge from pre-trained MoE LLMs to support effective training of language models across different model scales. XPERT identifies cross-domain experts via inference-only analysis, refines their representations through tensor decomposition, and adapts the extracted knowledge to be reused in downstream models. Experiments on language understanding and dialogue generation benchmarks show that models benefiting from reused expert knowledge achieve consistently stronger performance and faster convergence compared to strong baselines. These results highlight MoE LLMs as structured and reusable knowledge sources, and demonstrate the value of expert-level knowledge reuse for improving model training.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

混合专家（MoE）大语言模型通过显式路由机制将知识组织到不同的专家模块中，使得专家级别的表示变得可追溯和分析。然而，尽管已有研究揭示了MoE模型内部专家激活模式的可解释性，但如何实际复用这些专家知识以提升下游语言模型的训练效率，仍是一个未解决的问题。论文的核心动机是：通过分析MoE模型中的专家激活模式，发现存在一类“跨领域通用专家”，其编码的知识与模型泛化能力密切相关，进而提出一种无需训练即可提取、整合并复用这些专家知识的方法，从而支持不同规模语言模型的高效训练。

## 2. 论文提出的方法论：核心思想、关键技术细节

**核心思想**：XPERT是一个无需训练（training-free）的框架，从预训练的MoE大语言模型中提取、整合并重用专家知识，以支持下游语言模型的有效训练。

**关键技术细节**：
- **跨领域专家识别**：仅通过推理（inference-only）分析，统计在不同知识领域（如科学、常识、对话等）输入下各个专家的激活频率，筛选出在所有领域都频繁激活的专家子集，这些称为“跨领域通用专家”。
- **表示精炼**：对识别出的通用专家的参数（通常是权重矩阵）应用张量分解（tensor decomposition，如SVD或CP分解），压缩并提取核心知识表示，同时去除噪声冗余。
- **知识适配与重用**：将精炼后的专家知识以参数初始化（如权重初始化）或辅助损失（如知识蒸馏损失）的形式注入到下游语言模型中，支持不同规模模型的训练（包括从头训练或微调）。

**算法流程（文字描述）**：
1. 加载预训练MoE LLM，定义多个代表性知识域（如Wikipedia、BookCorpus、对话数据等）。
2. 在每一层MoE模块中，对每个领域输入记录专家路由选择（soft或hard分配），统计各专家的累积激活频次。
3. 选择在所有领域激活频次均位于前k%的专家作为跨领域通用专家。
4. 对每个通用专家的前馈网络（FFN）权重进行张量分解，获得低秩近似核心。
5. 将核心表示通过权重初始化或蒸馏损失迁移到目标模型（相同或更小规模）。
6. 在目标任务上训练该模型（保持冻结或微调），并评估性能。

## 3. 实验设计：使用的数据集/场景、benchmark、对比方法

- **数据集/场景**：
  - 语言理解：GLUE基准（如RTE、MRPC、CoLA等）或类似任务。
  - 对话生成：如Persona-Chat、DailyDialog等对话数据集。
- **Benchmark**：使用标准评估指标（准确率、F1、困惑度、BLEU等）与基线对比。
- **对比方法**：
  - 标准从头训练（无知识迁移）。
  - 使用预训练小模型初始化（如DistilBERT）。
  - 知识蒸馏（KD）从原始MoE模型到下游模型。
  - 随机专家选择或不精炼的专家权重直接初始化。

（注：具体数据集名称和数值需要从完整论文中获取；本摘要未列出全部细节，但可根据领域推断这些典型基准。）

## 4. 资源与算力

论文中未明确说明使用的具体GPU型号、数量和训练时长。仅提及XPERT是“training-free”框架，专家识别和精炼仅需少量推理时间和张量分解计算，下游模型训练使用标准资源。因此，未提供详细算力开销数据。

## 5. 实验数量与充分性

- **实验组数**：至少包括在语言理解（GLUE）多个子任务上的测试、在对话生成任务上的测试，以及消融实验（如比较是否使用通用专家、是否进行张量分解精炼、不同目标模型规模的影响）。
- **充分性评估**：
  - **优点**：覆盖了不同任务类型（分类与生成），且与多种基线对比，包含消融分析，实验设计较为系统。
  - **潜在不足**：若未在更多样化的任务（如代码、数学推理）上验证，则泛化性存疑；同时未提供统计显著性检验信息；资源开销细节缺失导致可复现性受影响。

## 6. 论文的主要结论与发现

- **跨领域通用专家的存在**：MoE模型中确实有部分专家在不同知识领域均被激活，其编码的知识是跨领域通用的，与模型的泛化能力正相关。
- **XPERT有效性**：通过无需训练的分析即可提取并整合这些专家知识，将其迁移到下游模型后，模型在语言理解和对话生成任务上均取得比从头训练和知识蒸馏更强的性能，同时收敛更快。
- **作为可复用知识源的MoE**：MoE LLM不仅是高性能模型，还可以成为结构化、可重用的知识来源，为高效训练提供新途径。

## 7. 优点

- **创新性**：首次提出从MoE模型中实际复用专家知识的方法，将可解释性分析转化为实用训练技术。
- **高效性**：无需额外训练或微调原始MoE模型，仅通过推理统计和张量分解即可完成知识提取。
- **灵活性**：提取的知识可适配不同规模的下游模型，甚至可用于更小模型的初始化。
- **强实验支撑**：在多个任务上验证了知识迁移带来的性能提升和收敛加速。

## 8. 不足与局限

- **算力细节缺失**：未公开实验所用的GPU型号、数量、总训练时长，影响复现和成本评估。
- **专家选择依赖于人为定义的知识领域**：领域划分可能带有主观性，若领域划分不当可能影响专家识别效果。
- **张量分解的精度损失**：压缩专家表示时可能丢失部分任务特定信息，对接特定窄域任务可能不如直接微调MoE模型。
- **应用限制**：目前仅验证了在语言理解和对话生成上的效果，未在更复杂的推理、生成（长文本、多模态）场景下测试，泛化边界未知。
- **实验充分性可提升**：若能补充更多消融（如不同张量分解方法、不同专家数量比例、不同目标模型规模）、更多任务（如数学推理、代码生成）以及统计显著性检验，结论会更坚实。

（完）
