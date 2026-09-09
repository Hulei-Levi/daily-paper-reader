<div class="dpr-home-notice-card">
  <h3 class="dpr-home-notice-title">🚀 Start Here</h3>
  <ul class="dpr-home-notice-list">
    <li><a href="#/tutorial/README">使用教程</a></li>
  </ul>
</div>

## 每次日报
- 最新运行日期：2026-09-09
- 运行时间：2026-09-09 22:03:14 UTC
- 运行状态：成功
- 本次总论文数：13
- 精读区：6
- 速读区：7

### 今日简报（AI）
1. 今日推荐13篇MoE论文，精读6篇、速读7篇，核心聚焦混合专家模型的训练、微调与系统优化。
2. 最值得精读的是《RAPTOR》与《ACE》（均9.0/10），分别解决角色感知私有训练与跨专家适配器合并；另外《Hyperparameter Scaling Laws》（8.0/10）可辅助理解稀疏度与超参数规律。
3. 建议优先精读上述两篇高分工作，速读可补超参数缩放律，以兼顾模型训练效率与资源调度。
- 详情：[/202609/09/README](/202609/09/README)

### 精读区论文标签
1. [RAPTOR: Role-Aware Private Training for Mixture-of-Experts](/202609/09/2609.05770v1-raptor-role-aware-private-training-for-mixture-of-experts)  
   标签：评分：9.0/10、query:moe-special
   evidence：面向稀疏混合专家模型设计角色感知私有训练，区分共享层与被路由专家并处理低负载专家
2. [ACE: Adapter Consolidation across Experts for Parameter-Efficient Fine-Tuning of MoE LLMs](/202609/09/2609.06072v1-ace-adapter-consolidation-across-experts-for-parameter-efficient-fine-tuning-of-moe-llms)  
   标签：评分：9.0/10、query:moe-special
   evidence：研究MoE中各专家独立低秩适配器的冗余与趋同，通过合并相似专家适配器实现参数高效微调
3. [From Concentration to Differentiation and Back: Routing Effective Rank in MoE Reasoning Cohorts](/202609/09/2609.06403v1-from-concentration-to-differentiation-and-back-routing-effective-rank-in-moe-reasoning-cohorts)  
   标签：评分：9.0/10、query:moe-special
   evidence：量化MoE专家路由相似性的有效秩以刻画路由分化
4. [Latent-MoE: Domain-Aware Mixture-of-Experts for PDEs with Multi-Regime Physics](/202609/09/2609.07814v1-latent-moe-domain-aware-mixture-of-experts-for-pdes-with-multi-regime-physics)  
   标签：评分：9.0/10、query:moe-special
   evidence：面向PDE多区域物理的域感知MoE与紧支撑路由设计
5. [Router Prior Bias: Preserving Base Routing Structure in MoE Post-Training](/202609/09/2609.08115v1-router-prior-bias-preserving-base-routing-structure-in-moe-post-training)  
   标签：评分：9.0/10、query:moe-special
   evidence：通过路由器先验偏置保存MoE专家协同激活的路由结构；提出软路由锚定
6. [MoEMB: Scaling Universal Multimodal Embeddings with Efficient Mixture-of-Experts Models](/202609/09/2609.08663v1-moemb-scaling-universal-multimodal-embeddings-with-efficient-mixture-of-experts-models)  
   标签：评分：8.0/10、query:moe-special
   evidence：提出MoEMB，用混合专家架构扩展通用多模态嵌入，降低冗余计算并保持高效检索

### 速读区论文标签
1. [Hyperparameter Scaling Laws Across MoE Sparsity](/202609/09/2609.08690v1-hyperparameter-scaling-laws-across-moe-sparsity)  
   标签：评分：8.0/10、query:moe-special
   evidence：系统研究MoE稀疏度与激活比例下的超参数缩放，与稀疏混合专家模型直接相关
2. [Evidence-Aligned Local Composition of Discrete Experts for Sequence Restoration](/202609/09/2609.05801v1-evidence-aligned-local-composition-of-discrete-experts-for-sequence-restoration)  
   标签：评分：7.0/10、query:moe-special
   evidence：在无训练路由与区域标签下，依据去噪损失估计证据并做逐位置专家加权
3. [HDA-MoE: Hybrid Parallelism and Dynamic, Adaptive Scheduling for Mixture-of-Experts with 3D Near-Memory Processing](/202609/09/2609.08682v1-hda-moe-hybrid-parallelism-and-dynamic-adaptive-scheduling-for-mixture-of-experts-with-3d-near-memory-processing)  
   标签：评分：7.0/10、query:moe-special
   evidence：提出面向3D近内存处理的MoE混合并行与动态自适应调度系统，核心对象是混合专家模型部署
4. [Chimaera: A Mixture-of-Graph-Experts Architecture for Cross-Task and Cross-Dataset Graph Learning](/202609/09/2609.08709v1-chimaera-a-mixture-of-graph-experts-architecture-for-cross-task-and-cross-dataset-graph-learning)  
   标签：评分：7.0/10、query:moe-special
   evidence：将混合专家机制引入图基础模型，支持跨任务和跨数据集图学习
5. [Different Changes Require Different Reasoning: Change-Type-Specialized Experts for Robust Change Captioning](/202609/09/2609.01136v1-different-changes-require-different-reasoning-change-type-specialized-experts-for-robust-change-captioning)  
   标签：评分：6.0/10、query:moe-special
   evidence：在图像变化描述任务中使用变化类型专用记忆专家并动态检索，体现显式的专家专业化设计
6. [Online Learning with LLM Experts from Limited Feedback](/202609/09/2609.05820v1-online-learning-with-llm-experts-from-limited-feedback)  
   标签：评分：6.0/10、query:moe-special
   evidence：将提示请求在多个LLM专家中的在线路由建模为有限反馈赌博机选择问题
7. [ExpertLens: Visualizing Embedding Spaces for Post-Hoc Explainability in MoE Enhanced Retrievers](/202609/09/2609.06155v1-expertlens-visualizing-embedding-spaces-for-post-hoc-explainability-in-moe-enhanced-retrievers)  
   标签：评分：6.0/10、query:moe-special
   evidence：通过专家嵌入空间可视化，为MoE增强稠密检索器提供事后可解释性


<div class="dpr-home-promo-card">
  <h3 class="dpr-home-promo-title">💬 社区与支持</h3>
  <ul class="dpr-home-promo-list">
    <li>欢迎 Star / Fork / Issue / PR</li>
    <li>QQ群：583867967（欢迎交流，已有：1151人）</li>
  </ul>
</div>
