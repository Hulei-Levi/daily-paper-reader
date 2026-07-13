<div class="dpr-home-notice-card">
  <h3 class="dpr-home-notice-title">🚀 Start Here</h3>
  <ul class="dpr-home-notice-list">
    <li><a href="#/tutorial/README">使用教程</a></li>
  </ul>
</div>

## 每次日报
- 最新运行日期：2026-06-14 ~ 2026-07-13
- 运行时间：2026-07-13 13:47:06 UTC
- 运行状态：成功
- 本次总论文数：24
- 精读区：13
- 速读区：11

### 今日简报（AI）
本期日报聚焦MoE路由优化与机器人操控扩散模型，精读《SoftMoE》和《CoRDE》均获9.0高分。最值得看的是混合专家模型的可微分路由机制，以及利用概念先验驱动扩散模型实现机器人结构泛化。建议优先精读《SoftMoE》理解软路由原理，再结合速读中关于MoE剪枝与初始化的工作（如《SPRI》《几何分析》）深化认识。
- 详情：[/20260614-20260713/README](/20260614-20260713/README)

### 精读区论文标签
1. [SoftMoE: Soft Differentiable Routing for Mixture-of-Experts in LLMs](/20260614-20260713/2606.17952v1-softmoe-soft-differentiable-routing-for-mixture-of-experts-in-llms)  
   标签：评分：9.0/10、query:moe-special
   evidence：MoE的软可微分路由
2. [CoRDE: Concept-Prior Routed Diffusion Experts for Structural Generalization in Robot Manipulation](/20260614-20260713/2606.21935v1-corde-concept-prior-routed-diffusion-experts-for-structural-generalization-in-robot-manipulation)  
   标签：评分：9.0/10、query:moe-special
   evidence：基于概念先验的路由避免扩散专家路由坍缩
3. [How Modular Is a Frontier Mixture-of-Experts? A Pre-registered Causal Test in Which Apparent Expert Modularity Mostly Dissolves](/20260614-20260713/2606.25092v1-how-modular-is-a-frontier-mixture-of-experts-a-pre-registered-causal-test-in-which-apparent-expert-modularity-mostly-dissolves)  
   标签：评分：9.0/10、query:moe-special
   evidence：对专家模块性和专业化的因果测试
4. [Learning Subset-Shared Invariances for Domain Generalization with Mixture-of-Experts](/20260614-20260713/2606.25665v1-learning-subset-shared-invariances-for-domain-generalization-with-mixture-of-experts)  
   标签：评分：9.0/10、query:moe-special
   evidence：使用混合专家架构学习子集共享不变性，实现专家专业化
5. [SARA: Unlocking Multilingual Knowledge in Mixture-of-Experts via Semantically Anchored Routing Alignment](/20260614-20260713/2606.25821v1-sara-unlocking-multilingual-knowledge-in-mixture-of-experts-via-semantically-anchored-routing-alignment)  
   标签：评分：9.0/10、query:moe-special
   evidence：跨语言专家专业化的路由对齐方法
6. [Fisher-Routed Mixture of Experts for Federated Class-Incremental Learning](/20260614-20260713/2606.28835v1-fisher-routed-mixture-of-experts-for-federated-class-incremental-learning)  
   标签：评分：9.0/10、query:moe-special
   evidence：联邦类增量学习中的自适应专家专业化与Fisher路由
7. [TF-MoE: Time-Frequency Mixture-of-Experts for Efficient Speech Separation](/20260614-20260713/2606.29575v2-tf-moe-time-frequency-mixture-of-experts-for-efficient-speech-separation)  
   标签：评分：9.0/10、query:moe-special
   evidence：时间和频率维度的动态专家专业化
8. [Does Role Specialization Matter for Explanation Faithfulness in Mixture-of-Experts?](/20260614-20260713/2606.29613v1-does-role-specialization-matter-for-explanation-faithfulness-in-mixture-of-experts)  
   标签：评分：9.0/10、query:moe-special
   evidence：角色专业化及其对MoE解释忠实性的影响
9. [Residual-Guided Expert Specialization for Incomplete Multimodal Learning](/20260614-20260713/2606.30355v1-residual-guided-expert-specialization-for-incomplete-multimodal-learning)  
   标签：评分：9.0/10、query:moe-special
   evidence：基于残差引导的专家专业化用于不完整多模态学习
10. [Learning to Select, Not Relearn: Hard-Routed Mixtures of Reasoning LoRAs](/20260614-20260713/2606.31413v1-learning-to-select-not-relearn-hard-routed-mixtures-of-reasoning-loras)  
   标签：评分：9.0/10、query:moe-special
   evidence：推理LoRA专家的硬路由选择
11. [Generic Expert Coverage for Pruning SparseMixture-of-Experts Language Models](/20260614-20260713/2607.01710v1-generic-expert-coverage-for-pruning-sparsemixture-of-experts-language-models)  
   标签：评分：9.0/10、query:moe-special
   evidence：稀疏MoE专家剪枝方法
12. [RoME: Robust Mixture of Low-Rank Experts against Multiple Adversarial Perturbations](/20260614-20260713/2607.06109v1-rome-robust-mixture-of-low-rank-experts-against-multiple-adversarial-perturbations)  
   标签：评分：9.0/10、query:moe-special
   evidence：低秩专家混合增强对抗鲁棒性，解决专家专业化
13. [On the Design of Mixture-of-Experts for Dynamic Gaussian Splatting](/20260614-20260713/2607.08250v1-on-the-design-of-mixture-of-experts-for-dynamic-gaussian-splatting)  
   标签：评分：9.0/10、query:moe-special
   evidence：利用混合专家实现多变形建模以重建动态3D场景

### 速读区论文标签
1. [How to Score Experts for One-Shot MoE Expert Pruning: A Unified Formulation and Selection Principle](/20260614-20260713/2606.15716v1-how-to-score-experts-for-one-shot-moe-expert-pruning-a-unified-formulation-and-selection-principle)  
   标签：评分：8.0/10、query:moe-special
   evidence：统一的一步专家剪枝准则公式
2. [SPRI: SVD-Partitioned Residual Initialization for Data-Constrained MoE Upcycling](/20260614-20260713/2606.16456v1-spri-svd-partitioned-residual-initialization-for-data-constrained-moe-upcycling)  
   标签：评分：8.0/10、query:moe-special
   evidence：SVD分区残差初始化提升MoE上循环中的专家多样性
3. [Geometric and Stochastic Analysis of Discontinuities in Sparse Mixture-of-Experts](/20260614-20260713/2606.19036v1-geometric-and-stochastic-analysis-of-discontinuities-in-sparse-mixture-of-experts)  
   标签：评分：8.0/10、query:moe-special
   evidence：对Top-k专家选择导致的不连续性进行几何和随机分析
4. [Grouped Query Experts: Mixture-of-Experts on GQA Self-Attention](/20260614-20260713/2606.20945v2-grouped-query-experts-mixture-of-experts-on-gqa-self-attention)  
   标签：评分：8.0/10、query:moe-special
   evidence：自注意力中查询头专家路由的MoE层
5. [MoECa: Aligning Feature Reuse with Expert Decomposition in Diffusion Transformers](/20260614-20260713/2606.15615v1-moeca-aligning-feature-reuse-with-expert-decomposition-in-diffusion-transformers)  
   标签：评分：7.0/10、query:moe-special
   evidence：DiT-MoE中专家分支级别的特征重用
6. [Conflict-Aware Federated Fine-Tuning of Large Language Models with Mixture-of-Experts](/20260614-20260713/2606.15625v1-conflict-aware-federated-fine-tuning-of-large-language-models-with-mixture-of-experts)  
   标签：评分：7.0/10、query:moe-special
   evidence：联邦MoE中数据异构导致专家优化冲突
7. [Attribution-Guided and Coverage-Maximized Pruning for Structural MoE Compression](/20260614-20260713/2606.18304v1-attribution-guided-and-coverage-maximized-pruning-for-structural-moe-compression)  
   标签：评分：7.0/10、query:moe-special
   evidence：结构剪枝分析专家通道重要性
8. [Toward Calibrated Mixture-of-Experts Under Distribution Shift](/20260614-20260713/2606.20544v1-toward-calibrated-mixture-of-experts-under-distribution-shift)  
   标签：评分：7.0/10、query:moe-special
   evidence：研究分布偏移下路由机制与专家校准的交互
9. [Tying the Loop -- Tied Expert Layers in Mixture-of-Experts Language Models](/20260614-20260713/2606.16825v1-tying-the-loop----tied-expert-layers-in-mixture-of-experts-language-models)  
   标签：评分：6.0/10、query:moe-special
   evidence：在MoE语言模型中跨层共享专家参数
10. [MODE: Modality-Decomposed Expert-Level Mixed-Precision Quantization for MoE Multimodal LLMs](/20260614-20260713/2606.17118v1-mode-modality-decomposed-expert-level-mixed-precision-quantization-for-moe-multimodal-llms)  
   标签：评分：6.0/10、query:moe-special
   evidence：多模态MoE量化中的专家重要性估计
11. [Systematic Exploration of 4-Expert Heterogeneous Mixture-of-Experts via Automated Pipeline Search](/20260614-20260713/2606.23739v1-systematic-exploration-of-4-expert-heterogeneous-mixture-of-experts-via-automated-pipeline-search)  
   标签：评分：6.0/10、query:moe-special
   evidence：异构MoE架构的自动搜索


<div class="dpr-home-promo-card">
  <h3 class="dpr-home-promo-title">💬 社区与支持</h3>
  <ul class="dpr-home-promo-list">
    <li>欢迎 Star / Fork / Issue / PR</li>
    <li>QQ群：583867967（欢迎交流，已有：1151人）</li>
  </ul>
</div>
