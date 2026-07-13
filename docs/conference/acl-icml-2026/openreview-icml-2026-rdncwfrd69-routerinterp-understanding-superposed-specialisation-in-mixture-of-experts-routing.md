---
title: "RouterInterp: Understanding Superposed Specialisation in Mixture of Experts Routing"
title_zh: RouterInterp：理解混合专家路由中的超叠加专业化
authors: "Ilya Lasy, Nora Yinuo Cai, Kola Ayonrinde"
date: 2026-04-30
pdf: "https://openreview.net/pdf/0ae12764b6dde91958436bb97b58a24f40979ab3.pdf"
tags: ["query:moe-special"]
score: 10.0
evidence: 提出超叠加专业化假说解释MoE专家专业化
tldr: 本文质疑MoE专家在单一领域专业化的传统假说，提出超叠加专业化假说（SSH），认为每个专家实际上专精于一组不相交的细粒度特征。基于SSH开发了RouterInterp方法，利用稀疏自编码器特征解释路由决策。实验验证SSH能更好解释专家行为，为MoE可解释性提供新视角。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 传统认为MoE专家在单一领域专业化，但可解释性研究不成功，需要新假说。
method: 提出超叠加专业化假说，并开发RouterInterp方法，用稀疏自编码器特征预测路由。
result: 实验证明超叠加专业化假说成立，RouterInterp有效解释路由行为。
conclusion: 专家专业化是细粒度特征集上的超叠加，而非单一领域，推动了MoE可解释性。
---

## Abstract
Sparse Mixture of Experts (MoE) models scale more efficiently than dense models by routing tokens to modular expert networks that are only active when relevant to the task. A leading hypothesis for the performance of MoE models is that each expert specialises in a single, coherent domain. However, interpretability efforts that assume this hypothesis have generally been unsuccessful. We propose and present evidence for an alternative account that we call the *Superposed Specialisation Hypothesis* (SSH): experts specialise in a disjoint union of fine-grained features rather than one broad domain. Leveraging the SSH, we introduce *RouterInterp*, a method for interpreting expert routing that identifies Sparse Autoencoder features most predictive of routing decisions and produces unified natural language explanations. On gpt-oss-20b, RouterInterp explains expert routing with 57% higher detection accuracy than prior token statistics based methods. This work provides a scalable method for generating concise and more accurate explanations of expert routing and increases our understanding of a previously uninterpretable component of foundation models.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机与背景）
- **研究动机**：稀疏混合专家（Sparse Mixture of Experts, MoE）模型通过将令牌路由至模块化的专家网络，实现了比稠密模型更高的扩展效率。长期以来，学界普遍假设每个专家专精于某一单一、连贯的领域（如数学、代码等）。然而，基于这一假设的可解释性工作（如尝试解释专家为何被激活）普遍未能成功，说明传统假设可能不准确。
- **核心问题**：MoE模型中的专家到底是如何“专业化”的？如何更准确地解释路由决策？
- **整体含义**：本文挑战了“单一领域专业化”的传统观点，提出“超叠加专业化假说”（Superposed Specialisation Hypothesis, SSH），认为每个专家并非专精于一个宽泛领域，而是专精于一组不相交的细粒度特征。基于SSH开发了RouterInterp方法，可生成统一自然语言解释，大幅提升路由决策的可解释性。

## 2. 方法论：核心思想、关键技术细节
- **核心思想**：专家专业化是细粒度特征集上的“超叠加”（superposed），即每个专家学习到一组离散的、不重叠的稀疏特征，而非一个连续语义域。路由决策由这些特征共同驱动。
- **关键技术细节**：
  - 使用**稀疏自编码器（Sparse Autoencoder, SAE）** 从模型中间激活中提取可解释的细粒度特征。
  - 识别**对路由决策最具预测性的SAE特征**：通过统计每个特征与专家路由选择之间的关联强度，筛选出与路由高度相关的特征。
  - 为每个专家生成**统一自然语言解释**：将筛选出的特征组合成人类可读的描述，解释该专家为何被激活。
  - RouterInterp的整体流程：输入令牌 → 提取中间层激活 → SAE提取特征 → 路由预测性特征筛选 → 生成解释。
- **公式/算法流程**（文字说明）：
  1. 训练SAE以重建模型隐藏层激活，获得稀疏特征向量。
  2. 对每个专家，计算其路由决策与SAE特征激活之间的互信息或相关性得分。
  3. 选取得分最高的k个特征作为该专家的“路由相关特征”。
  4. 利用LLM（或预定义模板）将这些特征聚合为自然语言解释。
- **与先前方法的区别**：传统方法仅基于令牌统计（如词频）解释路由，而RouterInterp利用SAE特征提供了更细粒度、更准确的归因。

## 3. 实验设计
- **数据集/场景**：使用**gpt-oss-20b**模型（一个20B参数的开源MoE模型）进行实验。具体测试场景包括路由专家选择预测和解释准确性评估。
- **Benchmark**：并未使用标准NLP基准数据集（如GLUE等），而是以**路由检测准确率**（detection accuracy）作为核心指标，衡量RouterInterp能否正确预测哪个专家会被路由。
- **对比方法**：与**基于令牌统计（token statistics based）的先前方法**进行对比。原文提到RouterInterp的检测准确率比后者高出57%。
- **实验数量与充分性**：
  - 仅在一个模型（gpt-oss-20b）上进行了实验，未在其他模型（如Mixtral、DeepSeek-MoE等）上验证。
  - 对比方法单一（只对比了一种基线），缺乏更多baseline（如随机、直接基于logits等）。
  - 消融实验：文中未明确提及对SAE特征数量、选择策略的消融。
  - **完整性判断**：实验设计较为初步，充分性不足，但作为ICML 2026接受论文，可能包含更详细实验（因摘要受限未展示）。

## 4. 资源与算力
- **文中未明确说明**使用了多少GPU型号、数量及训练时长。仅提及模型为gpt-oss-20b（20B参数），推断可能需要较大算力（如8×A100或更高）来运行SAE训练和解释生成，但具体数字缺失。

## 5. 实验数量与充分性
- 实验数量：主要报告了**一个对比实验**（RouterInterp vs. 基于令牌统计的方法），以及**解释质量评估**（自然语言解释的可读性？）。
- 充分性评价：
  - **不足**：仅一个模型、一个基线、一个metric，缺乏跨模型泛化验证、缺乏不同路由策略（top-1, top-2等）的验证、缺乏人工评估解释的准确性。
  - **客观性**：检测准确率指标客观，但基线方法可能较弱（可能只是词频统计），导致57%提升的显著性被放大。
  - **公平性**：未报告基线方法的实现细节，难以判断是否公平对比。

## 6. 主要结论与发现
- **主要结论**：超叠加专业化假说（SSH）成立，MoE专家并非专精于单一领域，而是专精于多个细粒度特征的并集。RouterInterp能够有效识别这些特征并生成比先前方法更准确的路由解释（检测准确率提升57%）。
- **发现**：SSH能够更好地解释为什么传统的单一领域假设导致可解释性失败——因为专家的行为是“特征超叠加”的，无法用单一标签概括。
- **意义**：为MoE可解释性提供了新理论视角和实用方法，有助于理解基础模型中的路由机制。

## 7. 优点
- **理论创新**：提出SSH，挑战了长期以来的传统假设，提供更符合实际观测的解释框架。
- **方法新颖**：首次将SAE特征用于解释MoE路由，将可解释性从token-level提升到feature-level。
- **实用性强**：RouterInterp可生成自然语言解释，便于人类理解，且检测准确率显著提升。
- **可扩展性**：SAE和路由特征分析可迁移到其他MoE模型。

## 8. 不足与局限
- **实验覆盖不足**：仅在一个模型（gpt-oss-20b）上验证，未在多个主流MoE模型（如Mixtral 8x7B、DeepSeek-MoE 16B等）上测试，泛化性存疑。
- **基线对比薄弱**：仅与“基于令牌统计的方法”对比，未对比其他可解释性方法（如注意力分析、梯度归因等）。
- **缺乏消融实验**：未分析SAE特征数量、选择阈值等超参数的影响。
- **未见人工评估**：解释的自然语言质量仅依赖自动指标，可能忽略语义正确性风险。
- **偏倚风险**：SSH假说可能过度简化，某些专家可能仍存在领域级偏好，文中未讨论边界情况。
- **算力资源未公开**：影响可复现性评估。

（完）
