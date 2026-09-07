<div class="dpr-home-notice-card">
  <h3 class="dpr-home-notice-title">🚀 Start Here</h3>
  <ul class="dpr-home-notice-list">
    <li><a href="#/tutorial/README">使用教程</a></li>
  </ul>
</div>

## 每次日报
- 最新运行日期：2026-09-07
- 运行时间：2026-09-07 22:39:49 UTC
- 运行状态：成功
- 本次总论文数：6
- 精读区：3
- 速读区：3

### 今日简报（AI）
今日聚焦混合专家（MoE）模型优化，6篇论文中3篇精读，围绕专家跳过、剪枝与高效路由展开。

最值得关注的方向：ACE实现免校准的自适应专家跳过（9.0/10），以及无需训练即可减半激活专家的方法（8.0/10），均能显著提升推理效率。

建议普通读者下步留意负载均衡过度可能引发的专家剪枝风险，以及跨领域MoE如蛋白语言建模中的条件记忆路由。
- 详情：[/202609/07/README](/202609/07/README)

### 精读区论文标签
1. [ACE: Adaptive Calibration-Free Expert Skipping for MoE-based LLMs](/202609/07/2609.05228v1-ace-adaptive-calibration-free-expert-skipping-for-moe-based-llms)  
   标签：评分：9.0/10、query:moe-special
   evidence：面向MoE大语言模型的自适应免校准专家跳过
2. [Training-Free Halving of Activated Experts in Fine-Grained Mixture-of-Experts Models](/202609/07/2609.04575v1-training-free-halving-of-activated-experts-in-fine-grained-mixture-of-experts-models)  
   标签：评分：8.0/10、query:moe-special
   evidence：细粒度MoE上减半激活专家并通过k2归一化保持精度，直接关联稀疏专家激活
3. [Cache-Aware Joint Router Adaptation for Memory-Efficient MoE Inference](/202609/07/2609.04895v1-cache-aware-joint-router-adaptation-for-memory-efficient-moe-inference)  
   标签：评分：8.0/10、query:moe-special
   evidence：面向MoE提出缓存感知的联合路由器适配，保留Top-K专家选择并预测专家复用

### 速读区论文标签
1. [When Load-Balancing Goes Too Far: Expert Pruning in Over-Dispersed Mixture-of-Experts Models](/202609/07/2609.04453v1-when-load-balancing-goes-too-far-expert-pruning-in-over-dispersed-mixture-of-experts-models)  
   标签：评分：7.0/10、query:moe-special
   evidence：分析MoE中过分散路由对基于路由器的专家剪枝的影响
2. [ProtLingo: Efficient Protein Language Modeling via Conditional Memory and Expert Routing](/202609/07/2609.04793v1-protlingo-efficient-protein-language-modeling-via-conditional-memory-and-expert-routing)  
   标签：评分：7.0/10、query:moe-special
   evidence：条件记忆与稀疏专家路由的高效蛋白质语言建模
3. [A Verifier-Guided Explainable Reasoning Framework with Gold-Anchored QLoRA, Task-Aware Mixture-of-Experts, and Group-Relative RLVR](/202609/07/2609.05221v1-a-verifier-guided-explainable-reasoning-framework-with-gold-anchored-qlora-task-aware-mixture-of-experts-and-group-relative-rlvr)  
   标签：评分：6.0/10、query:moe-special
   evidence：使用轻量级任务感知路由器将逻辑/物理问题分派给不同符号求解专家


<div class="dpr-home-promo-card">
  <h3 class="dpr-home-promo-title">💬 社区与支持</h3>
  <ul class="dpr-home-promo-list">
    <li>欢迎 Star / Fork / Issue / PR</li>
    <li>QQ群：583867967（欢迎交流，已有：1151人）</li>
  </ul>
</div>
