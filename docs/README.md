<div class="dpr-home-notice-card">
  <h3 class="dpr-home-notice-title">🚀 Start Here</h3>
  <ul class="dpr-home-notice-list">
    <li><a href="#/tutorial/README">使用教程</a></li>
  </ul>
</div>

## 每次日报
- 最新运行日期：2026-10-02
- 运行时间：2026-10-02 22:50:14 UTC
- 运行状态：成功
- 本次总论文数：16
- 精读区：6
- 速读区：10

### 今日简报（AI）
- 今日共生成 16 篇推荐（精读 6 篇，速读 10 篇）
- 精读：《MoRE: Scaling mixture of experts with hardware-aware low-rank routing》（9.0/10）, 《Routing in Gradient Space: Balanced Usage Is Not Expert Specialization》（9.0/10）
- 速读：《ID Balancing: Stable Training of Extremely Sparse MoE via PID-Based Load Control》（8.0/10）, 《Score the Update, Not the Token: Descent-Aligned Routing for Combinatorial LoRA Experts》（8.0/10）, 《Redundancy Meets Synergy: Dependency-aware Expert Selection for MoE via Submodular Optimization》（8.0/10）
- 这些结果覆盖了当下较热的方向，建议先看精读区论文的关键问题与方法。
- 详情：[/202610/02/README](/202610/02/README)

### 精读区论文标签
1. [MoRE: Scaling mixture of experts with hardware-aware low-rank routing](/202610/02/2609.36301v1-more-scaling-mixture-of-experts-with-hardware-aware-low-rank-routing)  
   标签：评分：9.0/10、query:moe-special
   evidence：低秩路由分解降低MoE路由开销
2. [Routing in Gradient Space: Balanced Usage Is Not Expert Specialization](/202610/02/2609.36724v1-routing-in-gradient-space-balanced-usage-is-not-expert-specialization)  
   标签：评分：9.0/10、query:moe-special
   evidence：指出负载均衡不等于专家专业化并提出梯度对齐路由
3. [Harnessing Domain Specialists in Multimodal Mixture-of-Experts for Efficient Adaptation](/202610/02/2610.02123v1-harnessing-domain-specialists-in-multimodal-mixture-of-experts-for-efficient-adaptation)  
   标签：评分：9.0/10、query:moe-special
   evidence：多模态MoE中专家涌现出语义专业化
4. [Emergent Specialization in Populations of Self-Supervised Collaborative Vision Experts Without a Shared Gate or Cross-Agent Gradients](/202610/02/2609.36770v1-emergent-specialization-in-populations-of-self-supervised-collaborative-vision-experts-without-a-shared-gate-or-cross-agent-gradients)  
   标签：评分：8.0/10、query:moe-special
   evidence：无需共享门控或跨智能体梯度的涌现专业化
5. [Cross-Entropy Guided Routing in Mixture-of-Experts Large Language Models](/202610/02/2609.37751v1-cross-entropy-guided-routing-in-mixture-of-experts-large-language-models)  
   标签：评分：8.0/10、query:moe-special
   evidence：以token误差监督对齐MoE路由亲和度与交叉熵
6. [Breaking the Uniformity Trap: Scaling Video Diffusion Model via SplitMoE](/202610/02/2609.38140v1-breaking-the-uniformity-trap-scaling-video-diffusion-model-via-splitmoe)  
   标签：评分：8.0/10、query:moe-special
   evidence：打破均匀性陷阱以促进专家角色专业化

### 速读区论文标签
1. [ID Balancing: Stable Training of Extremely Sparse MoE via PID-Based Load Control](/202610/02/2609.39137v1-id-balancing-stable-training-of-extremely-sparse-moe-via-pid-based-load-control)  
   标签：评分：8.0/10、query:moe-special
   evidence：通过负载控制实现极稀疏MoE稳定训练
2. [Score the Update, Not the Token: Descent-Aligned Routing for Combinatorial LoRA Experts](/202610/02/2610.00493v1-score-the-update-not-the-token-descent-aligned-routing-for-combinatorial-lora-experts)  
   标签：评分：8.0/10、query:moe-special
   evidence：MoE路由应评估专家更新而非Token
3. [Redundancy Meets Synergy: Dependency-aware Expert Selection for MoE via Submodular Optimization](/202610/02/2610.00558v1-redundancy-meets-synergy-dependency-aware-expert-selection-for-moe-via-submodular-optimization)  
   标签：评分：8.0/10、query:moe-special
   evidence：基于次模优化的依赖感知专家选择
4. [SpikeMoE: Brain-Inspired Competitive Routing for Flexible Spiking Mixture-of-Experts](/202610/02/2610.01418v1-spikemoe-brain-inspired-competitive-routing-for-flexible-spiking-mixture-of-experts)  
   标签：评分：8.0/10、query:moe-special
   evidence：基于脉冲的k-WTA路由器选择Top-K专家
5. [MoLE: Mixture of Latent Experts for Complementary Visual Reasoning](/202610/02/2610.01917v1-mole-mixture-of-latent-experts-for-complementary-visual-reasoning)  
   标签：评分：8.0/10、query:moe-special
   evidence：潜在token充当专业化的视觉专家
6. [BASE: Batch-Aware Selection of Experts Using Predicted Removal Error for Efficient MoE Decoding](/202610/02/2609.36222v1-base-batch-aware-selection-of-experts-using-predicted-removal-error-for-efficient-moe-decoding)  
   标签：评分：6.0/10、query:moe-special
   evidence：基于预测移除误差的批量感知专家选择
7. [E-MoE: Enhanced Mixture-of-Experts for Non-Factorized Diffusion Language Models](/202610/02/2609.37533v1-e-moe-enhanced-mixture-of-experts-for-non-factorized-diffusion-language-models)  
   标签：评分：6.0/10、query:moe-special
   evidence：专家混合的路由决策定义共享潜在变量
8. [RouteRec: Behavior-Guided Sparse Routing for Sequential Recommendation](/202610/02/2609.39007v1-routerec-behavior-guided-sparse-routing-for-sequential-recommendation)  
   标签：评分：6.0/10、query:moe-special
   evidence：行为引导的稀疏路由与条件计算
9. [MoRA: MoE Pruning via Router Bias Learning and Expert Approximation](/202610/02/2610.00367v1-mora-moe-pruning-via-router-bias-learning-and-expert-approximation)  
   标签：评分：6.0/10、query:moe-special
   evidence：结合路由偏置学习的MoE结构化专家剪枝
10. [From Task Mixtures to Specialized Experts](/202610/02/2610.00580v1-from-task-mixtures-to-specialized-experts)  
   标签：评分：6.0/10、query:moe-special
   evidence：从任务混合到专业化专家处理复合异构


<div class="dpr-home-promo-card">
  <h3 class="dpr-home-promo-title">💬 社区与支持</h3>
  <ul class="dpr-home-promo-list">
    <li>欢迎 Star / Fork / Issue / PR</li>
    <li>QQ群：583867967（欢迎交流，已有：1151人）</li>
  </ul>
</div>
