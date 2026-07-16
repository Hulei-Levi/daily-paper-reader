---
title: Discovering Heterogeneous Neurodegenerative Disease Patterns From MRI Data for Improved Prediction
title_zh: 从MRI数据中发现异质性神经退行性疾病模式以提高预测能力
authors: "Zhang, Y., Li, H., Fan, Y."
date: 2026-07-16
pdf: "https://www.biorxiv.org/content/10.64898/2026.07.10.737869v1.full.pdf"
tags: ["query:moe-special"]
score: 9.0
evidence: 提出包含路由器的混合专家框架用于亚型识别
tldr: 神经退行性疾病如阿尔茨海默病存在显著异质性，但现有无监督亚型识别方法无法保证所得亚型对诊断或预后有信息量。本文提出混合专家（MoE）框架，通过路由器将患者分配到多个专家网络，同时进行预测建模和亚型发现。在轻度认知障碍（MCI）数据上，该方法准确预测向阿尔茨海默病的进展，并识别出临床有意义的亚型。该工作确保了亚型既有统计差异又能提升预测精度，为异质性疾病的精准分型和预测提供了新途径。
source: biorxiv
selection_source: fresh_fetch
figures_json: "[{\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-07-10-737869-v1/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1135, \"height\": 278, \"label\": \"Figure\"}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-07-10-737869-v1/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1141, \"height\": 265, \"label\": \"Figure\"}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-07-10-737869-v1/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1122, \"height\": 551, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/biorxiv/biorxiv-10-64898-2026-07-10-737869-v1/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1270, \"height\": 380, \"label\": \"Table\"}, {\"url\": \"assets/tables/biorxiv/biorxiv-10-64898-2026-07-10-737869-v1/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 773, \"height\": 310, \"label\": \"Table\"}, {\"url\": \"assets/tables/biorxiv/biorxiv-10-64898-2026-07-10-737869-v1/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1087, \"height\": 234, \"label\": \"Table\"}]"
motivation: 现有无监督亚型识别方法仅捕获个体间变异，未能发现对诊断或预后有信息量的亚型，限制了临床应用。
method: 提出混合专家（MoE）框架，学习路由器将患者分配给不同专家网络，联合优化亚型识别与预测任务。
result: 在真实MCI和半模拟数据集上，该方法准确预测疾病进展并识别出具有临床意义的不同亚型，性能优于传统方法。
conclusion: 该框架发现的亚型兼具统计差异和临床信息性，有效提升了预测精度，为异质性疾病分型提供了新工具。
---

## 摘要
神经退行性疾病表现出显著的异质性，给诊断和预后都带来了复杂性。识别具有临床意义的亚型对于理解疾病机制至关重要，并且可以提高诊断和预后的准确性。现有的亚型划分方法主要依赖于对患者数据的无监督学习来捕获个体间差异，但往往无法发现对诊断或预后有信息量的亚型。为了解决这一局限性，我们提出了一种新颖的混合专家（MoE）框架，将预测建模与亚型识别相结合。与传统的亚型划分方法不同，我们的方法学习一个路由器，将个体分配到专门的专家网络中，每个网络对应一个不同的亚型，以提高预测准确性。这种MoE框架确保所发现的亚型不仅在统计上具有区分度，而且在临床上有信息量。我们在一个真实世界的轻度认知障碍（MCI）受试者数据集和一个半模拟数据集上评估了该框架，展示了在预测MCI受试者进展为阿尔茨海默病方面的优越性能，同时识别出了不同的、具有临床意义的MCI亚型。代码可在 https://github.com/Kateridge/MoESubtyping 获取。

## Abstract
Neurodegenerative diseases exhibit substantial heterogeneity, complicating both diagnosis and prognosis. Identifying clinically meaningful subtypes is crucial for understanding disease mechanisms and can also improve diagnostic precision and prognostic accuracy. Existing subtyping approaches primarily rely on unsupervised learning of patient data for capturing inter-individual variability, often failing to uncover subtypes that are informative for diagnosis or prognosis. To address this limitation, we propose a novel mixture-of-experts (MoE) framework that integrates predictive modeling with subtype identification. Unlike traditional subtyping methods, our approach learns a router to assign individuals to specialized expert networks, each corresponding to a distinct subtype, to improve predictive accuracy. This MoE framework ensures that the discovered subtypes are not only statistically distinct but also clinically informative. We evaluate the framework on a real-world dataset of mild cognitive impairment (MCI) subjects and a semi-simulated dataset, demonstrating superior performance for predicting MCI subjects progression to Alzheimers disease while identifying distinct clinically meaningful MCI subtypes. Code is available at https://github.com/Kateridge/MoESubtyping

---

## 论文详细总结（自动生成）

好的，这是对您提供的论文《Discovering Heterogeneous Neurodegenerative Disease Patterns From MRI Data for Improved Prediction》的详细中文总结。

### 论文核心问题与研究动机

- **核心问题**：神经退行性疾病（如阿尔茨海默病）具有显著的异质性，即不同患者的生物标志物（如脑部MRI测量的皮层厚度与脑区体积）变化模式差异巨大。这种异质性给疾病的精准诊断和预后预测带来了巨大挑战。
- **研究动机**：现有的识别疾病亚型的方法主要依赖于**无监督学习**（如K-Means，高斯混合模型）。这些方法虽然能根据图像特征的相似性对患者进行分组，但其聚类结果往往不服务于后续的诊断或预测任务，导致所发现的亚型缺乏临床信息性。换言之，单纯基于特征相似性的聚类，不一定能产生对预测疾病进展有价值的亚型。本文旨在解决这个“聚类与预测脱节”的局限性。

### 方法论：预测驱动的混合专家（MoE）框架

- **核心思想**：提出一个**预测驱动**的疾病亚型发现框架。它不是先聚类再预测，而是将亚型发现嵌入到预测模型中，确保所发现的亚型能最好地服务于预测任务。
- **技术细节**：
    1.  **架构**：该框架基于**混合专家（Mixture-of-Experts, MoE）** 架构，包含一个**路由器网络（Router）** 和**多个专家网络（Expert Networks）**。
    2.  **路由机制**：路由器网络接收每个受试者的MRI特征（96个脑区的测量值），并输出一个概率向量，指示该受试者应被分配到哪个专家。受试者最终被分配到概率最高的那个专家。
    3.  **专家网络**：每个专家网络都是一个独立的预测模型（例如，用于分类的MLP分类器，或用于生存分析的Cox回归模型），负责处理特定亚型的受试者数据。
    4.  **联合优化**：MoE框架通过**预测任务损失**（L_task）进行端到端训练。对于分类任务，损失是二元交叉熵；对于发病风险预测任务，损失是Cox比例风险模型的偏似然函数。**每个专家只在自己负责的受试者子集上计算损失，从而使其专注于学习该亚型的特有模式**。
- **关键技术与正则化**：
    - 为防止模型退化（如所有受试者都只被分到一个专家，或路由概率模糊不清），引入了三项正则化损失：
        1.  **负载平衡损失 (L_lb)**：通过最小化专家平均分配概率的负熵，鼓励所有专家被均匀利用，防止专家崩溃。
        2.  **稀疏分配损失 (L_sp)**：通过最小化每个受试者路由概率的熵，鼓励每个受试者被清晰地分配到一个专家，使路由决策更明确。
        3.  **聚类引导损失 (L_guide)**：在训练初期，用K-Means聚类结果作为伪标签来指导路由器训练，帮助模型快速收敛，该损失的权重在20个epoch后衰减至0。
- **总结**：该方法通过学习一个能根据预测任务优化分配策略的路由器，将一个高度异质性的群体拆分成多个相对同质的子群体（亚型），然后由专门的专家模型分别处理。**预测任务直接驱动了亚型的形成**。

### 实验设计

- **数据集**：
    1.  **真实数据集**：整合了ADNI、OASIS-3、AIBL三个大型纵向研究队列，共3,458名受试者的11,602次扫描。从中构建了两个下游任务：
        - **MCI分类任务**：668名基线诊断为MCI的受试者，标签为稳定MCI（sMCI，3年以上未进展）和进展性MCI（pMCI，3年内进展为痴呆）。
        - **MCI进展风险预测任务**：1,243名基线诊断为MCI的受试者，有多次随访，使用时间到事件数据做Cox回归。
    2.  **半模拟数据集**：在真实的认知正常（CU）扫描数据上人工叠加三种不同的脑萎缩模式（皮层萎缩、皮层下萎缩、混合萎缩），生成具有已知真实亚型标签的“患者”数据。该数据集用于评估模型的聚类性能。萎缩强度分为三个等级（10-30%，10-20%，5-15%）。
- **Benchmark与方法对比**：
    - **预测性能对比**：对比了“单一模型”（Single, Single* 扩大参数版）、随机森林、TabPFN（表格基础模型）、DeepSurv（生存分析模型）。
    - **聚类性能对比**：对比了K-Means、高斯混合模型（GMM）、DecoNet（一种深度自监督学习方法）。
- **评价指标**：
    - **分类任务**：准确率和敏感性。
    - **风险预测任务**：C-Index和时间依赖性AUC。
    - **半模拟数据集**：调整兰德指数 (ARI) 和归一化互信息 (NMI)。

### 资源与算力

- 论文**未明确说明**所使用的GPU型号、数量或具体的训练时长。

### 实验数量与充分性

- **实验数量**：论文进行了较为全面的实验。包括：
    1. 在真实数据集上的主实验结果（表1），与5种方法对比。
    2. 不同专家数量（K=2,3,4,5）的消融实验（表1）。
    3. 在半模拟数据集上，使用不同初始聚类方法（K-Means, GMM, DecoNet）的聚类性能比较（表2）。
    4. 针对不同强度的萎缩模式（弱、中、强）进行的聚类性能评估（表2），验证了方法的鲁棒性。
    5. 对三个正则化损失函数进行的消融实验（表3），证明了每个组件的贡献。
- **充分性与客观性**：
    - 实验设计较为充分，覆盖了预测和聚类两大核心能力。
    - 采用 **10折交叉验证**，结果报告了均值及95%置信区间，具有较强的统计稳健性。
    - 在半模拟数据上进行定量验证，弥补了真实数据缺乏真实亚型标签的不足，使评估更客观、更有说服力。
    - 与多种传统和前沿方法（包括深度学习基础模型TabPFN和生存分析专用模型DeepSurv）进行了对比，对比基准较为全面。
    - 但需要注意，比较的基线方法（如Single*）虽然扩大了参数，但并非专门为MoE设计的最大化容量基线，对比公平性上存在细微的不完全性。

### 主要结论与发现

1.  **预测性能提升显著**：MoE框架在MCI分类（准确率76.9%）和进展风险预测（C-Index 0.763）两个任务上，**显著优于**单模型和多数基准方法。其性能与性能极其强大的TabPFN相当，验证了方法的有效性。
2.  **内在聚类能力**：通过半模拟实验证实，MoE框架的性能提升来源于其对输入数据的**内在聚类能力**。它将数据分组，让专家学习更同质化的模式，从而提升预测精度。其聚类效果（ARI, NMI）优于或不弱于大多数传统的无监督聚类方法。
3.  **正则化项至关重要**：消融实验证明，负载平衡、稀疏分配和聚类引导这三个正则化损失对MoE模型同时实现良好的聚类和预测能力**至关重要**。缺少任一损失均会导致性能下降或模型退化。
4.  **识别出具有临床意义的亚型**：在MCI群体中识别出4种神经影像学亚型：
    - **亚型1**：轻度萎缩（类似早期MCI）。
    - **亚型2**：显著的内侧颞叶萎缩（类似遗忘型MCI）。
    - **亚型3**：广泛的皮层萎缩。
    - **亚型4**：皮层和皮层下均严重萎缩（类似晚期MCI或早期痴呆）。
    这些亚型与已知的疾病阶段和病理亚型高度吻合，证明了该方法发现的亚型具有临床解释性。

### 优点

- **创新性**：核心亮点是**将预测任务与亚型发现进行端到端联合优化**。不同于传统的“先无监督聚类，再独立预测”两步法，本文提出的“预测驱动亚型发现”范式能直接发现对临床决策（预后预测）最有价值的亚型。
- **方法有效性**：MoE架构优雅地将样本路由、聚类、预测融为一体。实验设计严谨，通过半模拟数据证明了模型性能提升源于其聚类能力，而非单纯的模型参数增加。
- **临床相关性**：识别出的亚型不仅提高了预测性能，而且能够从神经解剖学角度进行解读，与已知的MCI临床亚型相对应，具备潜在的临床应用价值。
- **通用性**：该框架被设计为通用框架，可以轻松适应不同的预测任务（分类、生存分析）和不同的输入特征（如体素级图像）。

### 不足与局限

- **依赖聚类引导**：目前方法需要依赖K-Means等传统聚类方法作为训练的引导（L_guide），虽然作者指出这是为了提供初始化，但这也意味着其最终性能在一定程度上受限于初始聚类结果。未来可探索完全端到端的可优化聚类目标。
- **实验范围有限**：
    - 仅使用了基于FreeSurfer提取的96个ROI特征，没有验证在**全脑体素级MRI数据**上的性能。作者承认了这一点，并表示这是未来工作。
    - 实验数据主要来自欧美队列，其在不同种族、不同扫描仪参数的数据集上的**泛化性**有待验证。
- **未提供计算资源细节**：缺少关于训练时间、GPU型号和数量等训练成本的描述，不利于其他研究者复现或评估方法的计算效率。
- **对比基线**：虽然对比了多个方法，但对于扩大容量的基线模型（Single*）的调优过程描述不够详细，无法完全排除性能差异仅仅是模型容量增加导致的可能性。

（完）
