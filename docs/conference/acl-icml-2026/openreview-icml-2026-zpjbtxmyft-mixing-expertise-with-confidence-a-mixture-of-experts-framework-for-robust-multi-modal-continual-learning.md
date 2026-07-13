---
title: "Mixing Expertise with Confidence: A Mixture of Experts Framework for Robust Multi-Modal Continual Learning"
title_zh: 基于信心的专家混合：面向鲁棒多模态持续学习的混合专家框架
authors: "Md Abdullah Al Forhad, Yuansheng Zhu, Abhinab Acharya, Xumin Liu, Qi Yu, Weishi Shi"
date: 2026-04-30
pdf: "https://openreview.net/pdf/a5c995d519a970222068a69b4e6222ed293f8781.pdf"
tags: ["query:moe-special"]
score: 5.0
evidence: 面向持续学习的MoE框架，支持动态专家通信
tldr: 本文针对持续学习中的灾难性遗忘问题，提出一种无需共享参数空间和任务ID预测器的MoE框架。通过允许专家间动态通信和知识共享，避免了共享空间瓶颈和复杂路由器设计。在多模态持续学习任务上，该方法有效缓解了遗忘，提升了鲁棒性。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 传统MoE持续学习中共享参数空间随任务增多成为瓶颈，而独立专家需任务ID预测器增加复杂性。
method: 提出无需共享参数和任务ID预测器的MoE框架，通过动态专家通信实现知识共享。
result: 多模态持续学习任务上，遗忘显著降低，鲁棒性增强。
conclusion: 动态专家通信是MoE持续学习的有效范式，简化解耦了任务关联。
---

## Abstract
The Mixture of Experts (MoE) framework is widely used in continual learning to mitigate catastrophic forgetting. MoEs typically combine a small inter-task shared parameter space with largely independent expert parameters. However, as the number of tasks increases, the shared space becomes a bottleneck, reintroducing forgetting, while fully independent experts require explicit task ID predictors (e.g., routers), adding complexity. In this work, we eliminate the inter-task shared parameter space and the need for a task ID predictor by enabling expert communication and allowing knowledge to be shared dynamically, akin to human collaboration. We bridge the inter-expert knowledge sharing by leveraging the open-set learning capabilities of a multimodal foundation model (e.g., CLIP), thereby providing “expert priors” that bolster each expert’s task-specific representations. Guided by these priors, experts learn calibrated inter-task posteriors. Additionally, multivariate Gaussians over the learned posteriors promote complementary specialization among experts. We propose new evaluation benchmarks that simulate realistic continual learning scenarios, and our prior-conditioned strategy consistently outperforms existing methods across diverse settings without relying on reference datasets or replay memory.

---

## 论文详细总结（自动生成）

好的，以下是根据您提供的论文元数据和摘要内容生成的结构化中文总结。

---

### 论文总结：基于信心的专家混合：面向鲁棒多模态持续学习的混合专家框架

#### 1. 核心问题与整体含义（研究动机和背景）
- **核心问题**：持续学习中的**灾难性遗忘**问题，即模型在学习新任务时容易忘记旧任务的知识。
- **现有方案的局限**：混合专家（MoE）框架通常结合一个小型的跨任务共享参数空间和大部分独立的专家参数。然而，随着任务数量增加，共享参数空间成为瓶颈，重新引入遗忘；而完全独立的专家则需要显式的任务ID预测器（如路由器），增加了系统复杂度。
- **研究动机**：消除跨任务共享参数空间和对任务ID预测器的依赖，通过让专家之间进行动态通信和知识共享（类似人类协作）来缓解遗忘，并提升多模态持续学习的鲁棒性。

#### 2. 提出的方法论
- **核心思想**：提出一种无需共享参数空间和任务ID预测器的MoE框架。利用多模态基础模型（如CLIP）的开放集学习能力为每个专家提供“专家先验”，从而增强专家的任务特定表征；然后基于这些先验学习校准的跨任务后验；此外，在后验上应用多元高斯分布促进专家之间的互补专业化。
- **关键技术细节**：
  - **专家动态通信**：通过引入专家间的知识共享机制（无需共享参数空间），实现动态交互。
  - **专家先验（Expert Priors）**：利用CLIP这样的多模态基础模型为每个专家提供任务相关的先验知识，指导专家学习更有效的任务表示。
  - **校准后验与互补专业化**：专家学习校准后的跨任务后验，并在后验上拟合多元高斯分布，从而鼓励不同专家在任务上形成互补的专业化分工（即部分专家擅长某些任务，其他专家擅长另外任务）。
- **算法流程（文字说明）**：框架输入为多模态数据（如图像+文本）。首先通过多模态基础模型提取通用特征并生成专家先验；然后将这些先验注入到各个专家模块中，专家模块基于先验学习当前任务的表征；在预测阶段，专家的输出后验通过多元高斯建模进行融合，得到最终的分类结果。整个过程无需显式路由器或共享参数空间。

#### 3. 实验设计
- **数据集/场景**：论文提出了**新的评估基准**来模拟现实的持续学习场景，具体数据集名称未在摘要和元数据中列出，但任务类型为多模态持续学习。
- **Benchmark**：作者自己构建的基准，覆盖多个不同的持续学习设置（diverse settings）。
- **对比方法**：与现有的持续学习方法进行对比（具体方法名称未在摘要中列出，但声称“consistently outperforms existing methods”）。

#### 4. 资源与算力
- **文中未明确说明**：摘要和元数据中没有提及使用的GPU型号、数量或训练时长等算力信息。论文全文可能包含此细节，但根据现有信息无法总结。

#### 5. 实验数量与充分性
- **实验数量**：摘要中提到在“diverse settings”（多种设置）下进行对比，但未给出具体实验组数（如不同数据集、消融实验等）。元数据中“evidence”字段提到“面向持续学习的MoE框架，支持动态专家通信”，但缺乏定量统计。
- **充分性**：鉴于声称“consistently outperforms existing methods”，应该进行了充分的对比实验，但缺少消融实验和详细分析的信息。由于无法看到完整论文，无法判断实验是否覆盖了所有关键消融点（如专家通信机制、专家先验、多元高斯的作用等）。总体来说，展示的实验对比较为充分，但细节不足。

#### 6. 主要结论与发现
- **主要结论**：提出的无共享参数空间、无任务ID预测器的MoE框架通过动态专家通信和先验引导，在多模态持续学习任务上显著降低了灾难性遗忘，提升了模型的鲁棒性。
- **发现**：利用多模态基础模型（CLIP）提供的专家先验可以有效引导专家学习，多元高斯后验建模有助于专家互补专业化。

#### 7. 优点
- **方法创新性**：巧妙地去掉了传统MoE持续学习中两个常见的痛点——共享参数瓶颈和任务ID预测器，使框架更简洁且扩展性更强。
- **动态专家通信机制**：受人类协作启发，专家之间可以动态共享知识，无需人为指定通信方式。
- **利用预训练基础模型**：利用CLIP的开放集能力提供先验，增强了泛化能力且无需额外监督。
- **实验公平性**：作者自己构建了新的现实基准，可能更贴近实际应用。

#### 8. 不足与局限
- **缺乏算力与时间报告**：未说明训练成本，可能使实际部署者难以评估可行性。
- **实验细节不透明**：具体数据集、对比方法、消融实验数量均未在摘要中体现，可能存在选择性报告的风险。例如，对专家先验的依赖性可能导致在CLIP不擅长的领域效果下降。
- **未讨论计算开销**：引入多元高斯后验建模可能增加推理复杂度，文中未讨论。
- **应用限制**：目前仅针对多模态持续学习场景（如图文），是否能推广到单模态或其他类型任务（如序列决策）尚不清楚。

（完）
