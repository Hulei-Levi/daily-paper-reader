---
title: "Awakening Dormant Experts:Counterfactual Routing to Mitigate MoE Hallucinations"
title_zh: 唤醒沉睡专家：反事实路由减轻混合专家模型幻觉
authors: "Wentao Hu, Yanbo Zhai, Xiaohui Hu, Mingkuan Zhao, Shanhong yu, Xue Liu, Kaidong Yu, Shuangyong Song (宋双永), Xuelong Li"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-long.2187.pdf"
tags: ["query:moe-special"]
score: 10.0
evidence: 唤醒休眠的专家以减少幻觉
tldr: 针对MoE模型在处理长尾知识时因静态路由导致专家沉睡而引发幻觉的问题，提出Counterfactual Routing，结合逐层扰动分析和反事实解释，在推理时重新激活沉睡的专业化专家。实验表明有效减少幻觉，提升长尾事实准确性。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.2187/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1487, \"height\": 693, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.2187/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1663, \"height\": 380, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.2187/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 664, \"height\": 853, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.2187/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 781, \"height\": 581, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.2187/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 790, \"height\": 559, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.2187/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 782, \"height\": 579, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.2187/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 780, \"height\": 574, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.2187/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1664, \"height\": 751, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.2187/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1660, \"height\": 304, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.2187/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1661, \"height\": 540, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.2187/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 859, \"height\": 303, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.2187/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1655, \"height\": 1481, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.2187/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 763, \"height\": 262, \"label\": \"Table\"}]"
motivation: 静态Top-k路由导致拥有长尾知识的专家被低估，引发幻觉。
method: 提出无训练的反事实路由框架，通过扰动分析识别并激活沉睡专家。
result: 在多个LLM上，CoR显著减少了幻觉，特别是对长尾知识。
conclusion: 反事实路由是激活休眠专家、提升MoE事实性的有效方法。
---

## Abstract
Sparse Mixture-of-Experts (MoE) models have achieved remarkable scalability, yet they remain vulnerable to hallucinations, particularly when processing long-tail knowledge. We identify that this fragility stems from static Top-k routing: routers tend to favor high-frequency patterns over rare factual associations. Consequently, "specialist experts" possessing critical long-tail knowledge are often assigned low gating scores and remain "dormant"—under-prioritized for specific tokens despite their proven causal importance on other inputs. To address this, we propose Counterfactual Routing (CoR), a training-free inference framework designed to awaken these dormant experts. CoR integrates layer-wise perturbation analysis with the Counterfactual Expert Impact (CEI) metric to dynamically shift computational resources from syntax-dominant to knowledge-intensive layers while maintaining a constant total activation count, effectively retrieving causally decisive experts via virtual ablation. Extensive experiments on TruthfulQA, FACTOR, and TriviaQA demonstrate that CoR improves factual accuracy by 3.1% on average without increasing the inference budget, establishing a superior Pareto frontier compared to static scaling strategies.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **问题**：稀疏混合专家（MoE）大语言模型虽然可扩展性强，但在处理**长尾知识**时容易产生幻觉（hallucination）。标准 Top‑k 静态路由倾向于选择处理高频模式的通用专家，而真正拥有长尾知识的**专用专家**（specialist experts）往往被赋予低门控分数，成为“沉睡专家”（dormant experts）。模型“知道”事实（存储在专用专家参数中），但“记不起来”（因路由决策而未被激活），从而导致幻觉。
- **背景**：现有幻觉缓解方法（如 DoLa、ITI）作用于输出分布或残差流，属于路由决策后的修正；检索增强生成（RAG）等训练时方法资源需求大。MoE 路由导致的幻觉问题此前未被专门研究。
- **动机**：通过因果引导的专家选择来唤醒沉睡专家，在不增加推理预算的前提下提升事实准确性。

## 2. 方法论：核心思想、关键技术细节

### 核心思想
**反事实路由（Counterfactual Routing, CoR）**：一个**零训练、推理时**框架。通过离线因果分析识别知识密集层和因果关键的专家，然后在推理时进行**计算量保持的专家重分配**，将同一激活总数从语法主导层转移到知识密集层，并用因果先验修正路由选择。

### 关键技术细节

#### (1) 离线因果分析阶段（分三层）

**a. Token 分层**：  
- 在校准集（C4）上计算每个 token 的负对数似然损失 ℓ(t)。
- 根据损失百分位分为**硬样本**（长尾知识，ℓ(t) > τ_high）和**易样本**（通用语法，ℓ(t) < τ_low）。

**b. 层分析——对比敏感性归一化（Contrastive Sensitivity Normalization）**  
- 对每一层 l 施加乘法扰动 δ，计算硬样本和易样本的损失变化 S_l(D_hard) 和 S_l(D_easy)。
- 定义**相对知识强度（RKI）**：R_l = S_l(D_hard) / (S_l(D_easy) + ε)。高 R_l 表示该层对硬样本至关重要，即知识密集层。
- 理论推导证明 R_l 可消除由网络深度带来的结构性放大偏差。

**c. 专家分析——反事实专家影响（CEI）**  
- 对于知识密集层中的每个专家 e，考虑其曾被激活的硬样本子集 T_{l,e}。
- 构造反事实场景：通过将该专家的门控概率按比例重分配给其他专家，模拟虚拟消融。
- 计算移除专家 e 后的损失增加量 Δℓ^{(t)}_{l,e}，定义**CEI_{l,e} = E_{t∈T_{l,e}} [Δℓ^{(t)}_{l,e}]**。高 CEI 意味着该专家对该 token 的真实性具有因果必要性。

#### (2) 在线推理阶段（计算量保持的专家重分配）

**a. 自适应预算分配**：  
- 总计算预算 K_total = L × k_baseline（k_baseline 为标准激活数）。
- 按每层 R_l 比例分配 k_l = Round( K_total × R_l / ΣR_j )，确保总激活数不变。

**b. 唤醒路由——上下文-先验融合**：  
- 融合得分 Score_{l,i}(x) = G_l(x)_i (上下文门控值) + λ · CEI_{l,i} (因果先验)，λ 为干预强度（实验中取 0.1）。
- 先对 CEI 进行层内 Min-Max 归一化以对齐尺度。
- 最终选择 Top-k_l 个专家。对普通 token 上下文分数主导，对不确定 token 因果先验可“唤醒”沉睡专家。

### 算法流程（文字描述）
1. 在校准集上计算 token 损失，分出硬/易子集。
2. 对每一层计算扰动敏感度 R_l。
3. 对知识密集层中的每个专家计算 CEI 值。
4. 推理时：根据 R_l 重新分配每层激活专家数；对每个 token，用式 (9) 计算融合分数并选择 Top-k_l 专家。

## 3. 实验设计

### 数据集/场景
- **事实性基准**：TruthfulQA (MC1, MC2, Gen)、FACTOR (News, Wiki)、TriviaQA
- **通用能力基准**：ARC-C, ARC-E, MMLU (Human, Social, STEM, Others)、GSM8K
- 校准集：C4 验证集随机采样 1000 token

### Benchmark 对比方法
- Standard Top‑k 路由（默认）
- Random Routing（随机激活专家）
- DoLa（解码时对比层间 logits）
- ITI（激活方向干预）
- （消融实验中还有 Layer‑wise Only、Expert‑wise Only）

### 模型
- Qwen‑3‑30B‑A3B
- DeepSeek‑V2‑Lite
- GPT‑OSS‑20B
- 额外验证：TeleChat3‑105B‑A4.7B‑Thinking（附录 A.6）

## 4. 资源与算力

- 文中明确指出：**所有推理和分析均在单张 NVIDIA H100 80G GPU 上完成**。
- **训练时长**：未明确给出具体时间，但强调离线因果分析是一次性过程，在线推理零额外延迟（CEI 预先缓存）。
- 算力开销相对较小，属于训练后轻量级干预。

## 5. 实验数量与充分性

### 实验数量概览
- **主实验**（表1）：3 个模型 × 6 个事实性子指标 × 4 个对比方法 = 大量对比。
- **消融实验**（表2）：在 Qwen‑3 上对比 Full CoR vs. Layer‑wise Only vs. Expert‑wise Only。
- **通用能力实验**（表3）：3 个模型 × 多个子任务，验证无退化。
- **效率分析**（图5）：CoR (Top‑8 等价) vs. Static Top‑9~12。
- **可视化**（图4、图6）：展示沉睡专家现象。
- **正交性分析**（表4）：CoR + DoLa 组合。
- **大规模验证**（表6）：TeleChat3‑105B。
- **定性案例**（表5）：6 个不同领域例子。

### 充分性与公平性
- 实验覆盖多架构（Qwen、DeepSeek、GPT‑OSS、TeleChat），规模从 20B 到 105B。
- 对比方法涵盖了标准路由、随机路由、主流推理时干预方法。
- 消融实验验证了各组件贡献。
- 通用能力实验表明 CoR 不损伤一般推理能力。
- 效率分析展示了帕累托最优前沿。
- 总体设计合理、客观，实验数量充分。

## 6. 主要结论与发现

1. MoE 模型存在**沉睡专家**现象：即对某些 token 因果关键的专家因路由偏好而未被激活。
2. CoR 通过**离线因果分析 + 计算量保持的重分配**，唤醒沉睡专家，平均提升事实准确性 **3.1%**，且不增加推理预算。
3. 在等价计算量下，CoR 优于静态增加 Top‑k 数量的策略，帕累托前沿更优。
4. CoR 与 DoLa 等后处理方法是**正交**的，联用可获累加收益。
5. CoR 在通用能力任务上保持性能，表明是安全干预。

## 7. 优点

- **零训练、仅推理时干预**：无需额外训练，无需修改模型参数，适用于已部署模型。
- **计算量保持**：总 FLOPs 与标准推理一致，不增加成本。
- **因果驱动**：通过反事实消融直接衡量专家必要性，有效区分相关性与因果性。
- **通用性**：在多种 MoE 架构及规模上验证。
- **可解释性**：通过可视化清晰展示沉睡专家现象及矫正效果。
- **正交性**：可与现有解码策略结合进一步提升性能。

## 8. 不足与局限

- **依赖模型已有知识**：CoR 只能优化对已存储知识的检索，无法补偿预训练中完全缺失的事实（out‑of‑pretraining knowledge）。
- **离线分析开销**：计算 CEI 涉及虚拟消融，虽为一次性且在校准小集上完成，但在极大规模模型（如万亿参数）上可能需要工程优化。
- **超参数 λ**：虽实验显示在 [0.05,0.2] 内稳健，但最佳值仍需简单调参。
- **校准集依赖**：使用 C4 数据集，虽然通用，但若目标领域偏移较大，可能需要针对性校准。
- **未在极端低资源场景测试**：如仅有少量 token 的校准集时性能如何未探讨。
- **未与 RAG 等知识注入方法对比**：作者提到未来可集成 RAG，但当前未做直接比较。

（完）
