---
title: Biological Continued Pretraining Reshapes the Capability Profile of a Foundation Model Without Catastrophic Forgetting
title_zh: 生物持续预训练重塑基础模型的能力轮廓而不会发生灾难性遗忘
authors: "Wang, L."
date: 2026-07-16
pdf: "https://www.biorxiv.org/content/10.64898/2026.07.06.736700v1.full.pdf"
tags: ["query:moe-special"]
score: 7.0
evidence: 使用26B参数的MoE模型（Gemma-4-26B-A4B）研究继续预训练对能力的影响。
tldr: 通常认为在狭窄分布语料上继续预训练（CPT）会因灾难性遗忘降低通用能力。本文对Gemma-4-26B-A4B模型进行生物序列CPT（8.7B tokens），发现通用知识、代码和生物医学能力全面上升（MMLU +13，MBPP翻倍，BixBench MCC 0.23→0.92），仅TruthfulQA略有下降。词汇扩展消融实验排除tokenizer干扰。后续SFT使能力回落到接近基线，表明CPT重塑共享能力基座，SFT将其兑现为目标任务，两者互补而非替代。
source: biorxiv
selection_source: fresh_fetch
figures_json: "[{\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-07-06-736700-v1/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1352, \"height\": 795, \"label\": \"Figure\"}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-07-06-736700-v1/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1534, \"height\": 681, \"label\": \"Figure\"}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-07-06-736700-v1/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 964, \"height\": 880, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/biorxiv/biorxiv-10-64898-2026-07-06-736700-v1/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1040, \"height\": 287, \"label\": \"Table\"}, {\"url\": \"assets/tables/biorxiv/biorxiv-10-64898-2026-07-06-736700-v1/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1784, \"height\": 287, \"label\": \"Table\"}, {\"url\": \"assets/tables/biorxiv/biorxiv-10-64898-2026-07-06-736700-v1/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1506, \"height\": 287, \"label\": \"Table\"}]"
motivation: 验证生物领域CPT是否必然导致灾难性遗忘并损害通用能力，重新审视CPT与SFT的关系。
method: 在26B参数MoE模型上，依次进行指令微调、生物CPT（8.7B tokens）和SFT，评估通用、代码和生物医学能力的变化。
result: "生物CPT全面提升三大能力（MMLU +13，MBPP pass@1从0.33到0.63，BixBench MCC从0.23到0.92），仅TruthfulQA下降8.8点；后续SFT使能力回落。"
conclusion: 生物序列是结构化科学数据，CPT重塑模型能力轮廓而无遗忘；CPT与SFT应被视为互补的预算阶段。
---

## 摘要
广泛认为，在窄域、分布外语料（如原始生物序列）上进行持续预训练（CPT）必然牺牲通用模型的广泛能力——即“对齐税”或灾难性遗忘的直觉。我们直接检验了这一假设，无需任何新训练，通过重新分析来自26B参数混合专家模型（Gemma-4-26B-A4B）单一谱系中的三个检查点：指令微调基础点、经生物CPT（87亿tokens的DNA、蛋白质和生物医学文本）后的同一模型，以及后续监督微调（SFT）后的模型。在三个独立的能力轴——通用知识/推理（MMLU、ARC、HellaSwag）、代码生成（MBPP）和生物医学知识（BixBench）上，我们发现生物CPT并未降低模型性能，反而提升：MMLU +13分，MBPP pass@1近乎翻倍（0.33至0.63），BixBench判别力急剧上升（MCC 0.23至0.92）。唯一的测量回归是真实性（TruthfulQA -8.8分），这是一个微小且可解释的领域漂移。一个干净的词汇扩展消融实验（每项通用指标波动<0.4分）证实了提升归因于CPT，而非分词器变化。关键的是，后续SFT使模型回缩：三个轴均回落至接近基础水平，揭示出一致的分工——CPT重新组织并提升共享能力基础；SFT将其兑现到目标任务上。我们认为这重新将生物序列框定为一种结构化科学数据，它重塑了基础模型的能力轮廓，而非与其能力竞争；并且CPT和SFT应被视为互补而非可替代阶段来预算。所有检查点、评估代码及逐示例输出均已公开。

## Abstract
It is widely assumed that continued pretraining (CPT) on a narrow, out-of-distribution corpus such as raw biological sequence must trade away a general-purpose model's broad competence --- the "alignment tax" or catastrophic-forgetting intuition. We test this directly, without any new training, by re-analyzing three checkpoints from a single lineage of a 26B-parameter Mixture-of-Experts model (Gemma-4-26B-A4B): the instruction-tuned base, the same model after biological CPT (8.7B tokens of DNA, protein, and biomedical text), and after subsequent supervised fine-tuning (SFT). Across three independent capability axes --- general knowledge/reasoning (MMLU, ARC, HellaSwag), code generation (MBPP), and biomedical knowledge (BixBench) --- we find that biological CPT does not degrade the model; it lifts it: MMLU +13 points, MBPP pass@1 nearly doubles (0.33 to 0.63), and BixBench discrimination rises sharply (MCC 0.23 to 0.92). The single measured regression is truthfulness (TruthfulQA -8.8 points), a small and interpretable domain drift. A clean vocabulary-expansion ablation (<0.4 pt on every general metric) confirms the gains are attributable to CPT, not tokenizer changes. Crucially, subsequent SFT narrows the model back: all three axes fall to near-base levels, revealing a consistent division of labor --- CPT re-organizes and lifts the shared capability substrate; SFT cashes it out onto target tasks. We argue this reframes biological sequence not as a competitor for a foundation model's capacity but as a form of structured scientific data that reshapes its capability profile, and that CPT and SFT should be budgeted as complementary rather than substitutable stages. All checkpoints, evaluation code, and per-example outputs are public.