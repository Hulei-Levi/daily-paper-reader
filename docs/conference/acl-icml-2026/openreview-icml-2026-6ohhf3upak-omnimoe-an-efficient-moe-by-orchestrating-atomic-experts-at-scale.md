---
title: "OmniMoE: An Efficient MoE by Orchestrating Atomic Experts at Scale"
title_zh: OmniMoE：通过协调原子专家实现高效的混合专家模型
authors: "Jingze Shi, Zhangyang Peng, Yizhang Zhu, Yifan Wu, Guang Liu, Yuyu Luo"
date: 2026-04-30
pdf: "https://openreview.net/pdf/925e4a67bfcb901e19e55a6d38812c1d6e8264ca.pdf"
tags: ["query:moe-special"]
score: 9.0
evidence: 通过原子专家粒度最大化专家专业化
tldr: 为突破专家粒度与硬件效率的权衡，提出OmniMoE，采用向量级原子专家和笛卡尔积路由器，在单层内实现细粒度路由，同时保留共享MLP。有效提升了专家专业化和参数效率。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有MoE在专家粒度精细度与执行效率间存在固有权衡。
method: 提出向量级原子专家和笛卡尔积路由器，系统算法协同设计。
result: 在多个基准上，OmniMoE以更少参数达到或超越现有MoE性能。
conclusion: 极致细粒度的原子专家设计能有效提升MoE专业化与效率。
---

## Abstract
Mixture-of-Experts (MoE) architectures are evolving towards finer granularity to improve parameter efficiency. However, existing MoE designs face an inherent trade-off between the granularity of expert specialization and hardware execution efficiency. In this paper, we propose OmniMoE, a system-algorithm co-designed MoE framework that pushes granularity to the extreme with vector-level Atomic Experts, orchestrating their routing and execution at scale within a single MoE layer, while retaining a shared dense MLP for general-purpose processing. While this atomic design maximizes capacity, it poses severe challenges for routing complexity and memory access. To address these, OmniMoE adopts a system-algorithm co-design: (i) a Cartesian Product Router that decomposes the massive index space to reduce routing complexity from $O(N)$ to $O(\sqrt{N})$; and (ii) Expert-Centric Scheduling that inverts the execution order to turn scattered, memory-bound lookups into efficient dense matrix operations. Validated on seven benchmarks, OmniMoE (with 1.7B active parameters) achieves 50.9\% zero-shot accuracy across seven benchmarks, outperforming coarse-grained (e.g., DeepSeekMoE) and fine-grained (e.g., PEER) baselines. Crucially, OmniMoE reduces inference latency from 73ms to 6.7ms (a 10.9$\times$ speedup) compared to PEER, demonstrating that massive-scale fine-grained MoE can be fast and accurate.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）
混合专家模型（MoE）架构正朝着更细粒度的方向发展，以提升参数效率。然而，现有MoE设计在专家专业化粒度与硬件执行效率之间存在固有的权衡：细粒度专家能提高参数利用率和专业化程度，但会导致路由复杂度剧增和内存访问不连续，从而严重影响推理速度。本文旨在突破这一权衡，提出一种极致细粒度的MoE框架，在保持高硬件效率的同时实现专家最大程度的专业化。

## 2. 方法论：核心思想与关键技术细节
**核心思想**：将专家粒度推至极限——采用**向量级的原子专家（Atomic Experts）**，每个专家只包含一个向量（而非整个MLP层），并在单层内大规模协调路由与执行；同时保留一个共享的稠密MLP层用于通用处理。  
**关键技术**（系统-算法协同设计）：  
- **笛卡尔积路由器（Cartesian Product Router）**：将传统$O(N)$的索引空间分解为两个子空间的笛卡尔积，将路由复杂度从$O(N)$降低到$O(\sqrt{N})$，从而支持大量原子专家的高效选择。  
- **专家中心调度（Expert-Centric Scheduling）**：反转执行顺序，将原本分散、内存受限的查找操作转化为高效的稠密矩阵运算，显著减少推理延迟。

**算法流程（文字说明）**：  
1. 输入token经过共享的稠密MLP（通用处理）。  
2. 同时，笛卡尔积路由器对每个token选择两组子专家索引（来自两个子空间），通过笛卡尔积组合得到最终激活的原子专家集合。  
3. 专家中心调度器将原子专家的计算重组为稠密矩阵乘法，避免不规则内存访问。  
4. 将稠密MLP输出与原子专家的加权输出求和得到最终输出。

## 3. 实验设计
- **数据集/场景**：在7个基准（benchmarks）上进行评估，涵盖零样本（zero-shot）任务。  
- **对比方法**：  
  - 粗粒度MoE基线：DeepSeekMoE  
  - 细粒度MoE基线：PEER  
- **性能指标**：零样本准确率（zero-shot accuracy）与推理延迟（inference latency）。  
- **模型规模**：OmniMoE使用1.7B活跃参数（active parameters）。

## 4. 资源与算力
文中未明确说明所使用的GPU型号、数量、训练时长等算力信息。因此，无法提供具体资源细节。

## 5. 实验数量与充分性
- 实验数量：仅报告了7个基准上的零样本准确率平均值（50.9%）以及与PEER的推理延迟对比（从73ms降至6.7ms）。  
- 充分性评估：缺乏消融实验（如逐组件贡献、原子专家数量影响、路由策略变体等）和对不同任务类型的细分结果；也未提供训练阶段的效率对比。实验覆盖较窄，不足以充分验证方法的普适性和稳定性。  
- 公平性：与DeepSeekMoE和PEER相比，模型参数规模可能不同，但未明确控制变量（如总参数量、活跃参数比例）。推理延迟对比仅与PEER进行，未与DeepSeekMoE对比，可能存在选择偏差。

## 6. 主要结论与发现
- OmniMoE（1.7B活跃参数）在7个基准上取得50.9%的零样本准确率，优于粗粒度（DeepSeekMoE）和细粒度（PEER）基线。  
- 推理延迟比PEER降低10.9倍（从73ms到6.7ms），证明极致细粒度的原子专家设计可以同时实现高精度和高速度。  
- 验证了系统-算法协同设计（笛卡尔积路由器+专家中心调度）是克服细粒度MoE硬件效率瓶颈的有效途径。

## 7. 优点
- **专家专业化最大化**：向量级原子专家使每个专家专注于极少数特征，理论上达到最大专业化。  
- **路由复杂度降低**：笛卡尔积路由器将指数级搜索空间分解为两个线性空间，支持大规模原子专家而路由开销可控。  
- **硬件友好**：专家中心调度将稀疏不规则访问转化为稠密计算，大幅提升GPU执行效率。  
- **精度-速度双赢**：在相同活跃参数下，比当前最先进的细粒度MoE（PEER）推理速度快一个数量级，同时零样本准确率更高。

## 8. 不足与局限
- **实验覆盖有限**：仅报告7个基准的零样本平均准确率，缺乏对多样任务（如微调、多语言、多模态）的验证。  
- **消融研究缺失**：未提供原子专家数量、共享MLP比例、路由维度等关键超参数的影响分析。  
- **训练效率未知**：论文仅提及推理性能，未展示训练时间、显存占用或收敛速度等训练相关指标。  
- **对比不够全面**：仅对比DeepSeekMoE和PEER两种基线，未与其他主流MoE（如Switch Transformer、GShard）比较。  
- **潜在偏差风险**：零样本准确率可能对特定基准有过拟合风险；延迟测试环境未明确（硬件、batch size等）。  
- **应用限制**：原子专家设计可能增加模型总参数量（尽管活跃参数少），对存储和通信带宽仍有较高要求，部署在大规模分布式系统时需额外优化。

（完）
