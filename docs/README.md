<div class="dpr-home-notice-card">
  <h3 class="dpr-home-notice-title">🚀 Start Here</h3>
  <ul class="dpr-home-notice-list">
    <li><a href="#/tutorial/README">使用教程</a></li>
  </ul>
</div>

## 每次日报
- 最新运行日期：2026-08-11
- 运行时间：2026-08-11 21:24:11 UTC
- 运行状态：成功
- 本次总论文数：14
- 精读区：7
- 速读区：7

### 今日简报（AI）
今日聚焦MoE高效推理与模型优化，共推荐14篇论文，其中7篇精读、7篇速读。最值得关注的是满分技术报告《Motif 3》及揭示轻量微调可识别可剪枝专家的研究，另有负载均衡与专家合并加速方案值得速览。建议优先精读前两篇，把握MoE结构分析与剪枝核心思路，再拓展速读内容。
- 详情：[/202608/11/README](/202608/11/README)

### 精读区论文标签
1. [Motif 3: Technical Report](/202608/11/2608.09119v1-motif-3-technical-report)  
   标签：评分：10.0/10、query:moe-special
   evidence：明确针对稀疏混合专家模型中的专家专业化，采用384个路由专家
2. [Router Sensitivity Under Lightweight Fine-Tuning Identifies Prunable Experts in Mixture-of-Experts Models](/202608/11/2608.07890v1-router-sensitivity-under-lightweight-fine-tuning-identifies-prunable-experts-in-mixture-of-experts-models)  
   标签：评分：9.0/10、query:moe-special
   evidence：利用轻量微调下的路由器敏感性对MoE专家排序并剪除变化最小的专家
3. [The Evolution of Mixture-of-Experts Architectures in Large Language Models: Routing, Topology, Load Balancing, and Expert Parallelism](/202608/11/2608.08650v1-the-evolution-of-mixture-of-experts-architectures-in-large-language-models-routing-topology-load-balancing-and-expert-parallelism)  
   标签：评分：9.0/10、query:moe-special
   evidence：综述从路由、拓扑、负载均衡和专家并行等维度组织MoE系统，直接涵盖专家路由机制
4. [AdapterMoE: A Two-Stage Hard-Routing Mixture-of-Experts Architecture for Multi-Crop Disease Recognition with Calibrated Rejection and Incremental Learning](/202608/11/2608.08808v1-adaptermoe-a-two-stage-hard-routing-mixture-of-experts-architecture-for-multi-crop-disease-recognition-with-calibrated-rejection-and-incremental-learning)  
   标签：评分：9.0/10、query:moe-special
   evidence：提出带RouterHead的硬路由MoE，解决专家崩溃并建立作物与专家的语义对应
5. [Beyond Routing: Decoupling Expert Dispatch and Aggregation in Sparse Mixture-of-Experts](/202608/11/2608.08853v1-beyond-routing-decoupling-expert-dispatch-and-aggregation-in-sparse-mixture-of-experts)  
   标签：评分：9.0/10、query:moe-special
   evidence：稀疏MoE路由；解耦专家调度与聚合权重
6. [MoRSE: Task-Oriented Multi-Agent System with Mixture of Role-Subtask Experts](/202608/11/2608.09251v1-morse-task-oriented-multi-agent-system-with-mixture-of-role-subtask-experts)  
   标签：评分：9.0/10、query:moe-special
   evidence：在混合专家启发的多智能体系统中，从任务结构和参数层面引入(角色、子任务)条件化专业化
7. [DistMoE: Private-data Rehearsal-free Routing in Mixture-of-Experts for Distributed Instruction Tuning](/202608/11/2608.09907v1-distmoe-private-data-rehearsal-free-routing-in-mixture-of-experts-for-distributed-instruction-tuning)  
   标签：评分：9.0/10、query:moe-special
   evidence：MoE中面向客户端的私有专家专业化与免回放路由

### 速读区论文标签
1. [EasyBalance: Cross-Layer Load Balancing in Distributed MoE Inference](/202608/11/2608.07964v1-easybalance-cross-layer-load-balancing-in-distributed-moe-inference)  
   标签：评分：8.0/10、query:moe-special
   evidence：面向分布式MoE推理中专家路由分布的跨层负载均衡
2. [UniMoMo: Expert Merging-Based MoE Acceleration for Large Recommendation Models](/202608/11/2608.08627v1-unimomo-expert-merging-based-moe-acceleration-for-large-recommendation-models)  
   标签：评分：8.0/10、query:moe-special
   evidence：稀疏MoE层、条件计算与基于功能相似性的专家分组
3. [A Context-aware Gated Convex Mixtures of LSTM Experts for Nonlinear System Identification](/202608/11/2608.08980v1-a-context-aware-gated-convex-mixtures-of-lstm-experts-for-nonlinear-system-identification)  
   标签：评分：8.0/10、query:moe-special
   evidence：LSTM专家混合与门控凸组合
4. [Shape Mutating Expert Compression:LorExperts and BTExperts](/202608/11/2608.07814v1-shape-mutating-expert-compressionlorexperts-and-btexperts)  
   标签：评分：7.0/10、query:moe-special
   evidence：提出MoE专家压缩方法，保留专家权重和路由，并分析专家共激活功能社区
5. [FreSH: Frequency-Segmented Hierarchical Multi-Expert Framework for Multivariate Time Series Classification](/202608/11/2608.08207v1-fresh-frequency-segmented-hierarchical-multi-expert-framework-for-multivariate-time-series-classification)  
   标签：评分：7.0/10、query:moe-special
   evidence：面向时间序列的多专家框架，具有局部专业化，与混合专家模型相关
6. [Hierarchical Quantization with Domain-Adaptive Sparse Routing for Generative Cross-Domain Recommendation](/202608/11/2608.06997v1-hierarchical-quantization-with-domain-adaptive-sparse-routing-for-generative-cross-domain-recommendation)  
   标签：评分：6.0/10、query:moe-special
   evidence：面向异构跨域推荐的域自适应稀疏路由机制
7. [When Does Trace-Driven Evaluation Mislead MoE Expert Caching? Replay Semantics, Workload Contamination, and Operating Regimes](/202608/11/2608.07911v1-when-does-trace-driven-evaluation-mislead-moe-expert-caching-replay-semantics-workload-contamination-and-operating-regimes)  
   标签：评分：6.0/10、query:moe-special
   evidence：MoE专家缓存与基于轨迹的评估


<div class="dpr-home-promo-card">
  <h3 class="dpr-home-promo-title">💬 社区与支持</h3>
  <ul class="dpr-home-promo-list">
    <li>欢迎 Star / Fork / Issue / PR</li>
    <li>QQ群：583867967（欢迎交流，已有：1151人）</li>
  </ul>
</div>
