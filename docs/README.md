<div class="dpr-home-notice-card">
  <h3 class="dpr-home-notice-title">🚀 Start Here</h3>
  <ul class="dpr-home-notice-list">
    <li><a href="#/tutorial/README">使用教程</a></li>
  </ul>
</div>

## 每次日报
- 最新运行日期：2026-08-12
- 运行时间：2026-08-12 19:55:21 UTC
- 运行状态：成功
- 本次总论文数：11
- 精读区：5
- 速读区：6

### 今日简报（AI）
今日处理11篇论文（精读5篇/速读6篇），聚焦模型稀疏化、联邦学习与多模态生成方向。  
最值得关注两篇9分工作：模块化稀疏路由《SpecDrop》与时间序列基础模型的联邦稀疏适应《Personalized Federated Sparse Adaptation》。  
建议普通读者优先看“稀疏专家路由”这一趋势，可兼顾性能与效率；顺带速读水下图像增强等应用侧进展。
- 详情：[/202608/12/README](/202608/12/README)

### 精读区论文标签
1. [SpecDrop: Parameter-Free Category-Conditioned Routing for Modular Specialization](/202608/12/2608.04084v1-specdrop-parameter-free-category-conditioned-routing-for-modular-specialization)  
   标签：评分：9.0/10、query:moe-special
   evidence：直接研究MoE专家专业化瓶颈；提出无参数类别条件路由，不学路由参数与辅助损失即可提升模块特化
2. [Personalized Federated Sparse Adaptation of Time-Series Foundation Models](/202608/12/2608.04695v1-personalized-federated-sparse-adaptation-of-time-series-foundation-models)  
   标签：评分：9.0/10、query:moe-special
   evidence：使用异构时序MoE适配器，专家分别特化周期、长程交互、局部变化与趋势，序列级路由器选择top-k专家
3. [Disentangling Co-Occurring Retinal Pathologies with Saliency-Guided Sparse Expert Routing](/202608/12/2608.09752v1-disentangling-co-occurring-retinal-pathologies-with-saliency-guided-sparse-expert-routing)  
   标签：评分：9.0/10、query:moe-special
   evidence：稀疏路由专家混合块且专家分配依赖疾病类型；直接体现专家专业化
4. [Share First, Route What Remains: A Unified Framework for Token-Adaptive MoE Computation](/202608/12/2608.10392v1-share-first-route-what-remains-a-unified-framework-for-token-adaptive-moe-computation)  
   标签：评分：8.0/10、query:moe-special
   evidence：标记自适应MoE路由框架
5. [MammoMix: Leveraging Mixture of Experts for Robust Mammogram Breast Detection](/202608/12/2608.10437v1-mammomix-leveraging-mixture-of-experts-for-robust-mammogram-breast-detection)  
   标签：评分：8.0/10、query:moe-special
   evidence：采用MoE框架使各专家专精于特定域，体现专家专业化

### 速读区论文标签
1. [CoRe-UIE: Rethinking Coexisting and Region-wise Degradation for Underwater Image Enhancement](/202608/12/2608.08965v1-core-uie-rethinking-coexisting-and-region-wise-degradation-for-underwater-image-enhancement)  
   标签：评分：7.0/10、query:moe-special
   evidence：用于水下图像区域退化修复的路由专家协作框架
2. [SonicWeave: Chunk-Routed Mixture-of-Experts for Unified Audio Scene Generation](/202608/12/2608.09571v1-sonicweave-chunk-routed-mixture-of-experts-for-unified-audio-scene-generation)  
   标签：评分：7.0/10、query:moe-special
   evidence：用于统一音频场景生成的分块路由混合专家流匹配模型
3. [Compute-Optimal Is Not Cluster-Optimal: Systems-Aware Scaling for Sparse Mixture-of-Experts](/202608/12/2608.10605v1-compute-optimal-is-not-cluster-optimal-systems-aware-scaling-for-sparse-mixture-of-experts)  
   标签：评分：7.0/10、query:moe-special
   evidence：稀疏MoE的系统感知扩展
4. [Trigger the Straggler: Load Hijack on Mixture-of-Experts LLMs](/202608/12/2608.10614v1-trigger-the-straggler-load-hijack-on-mixture-of-experts-llms)  
   标签：评分：7.0/10、query:moe-special
   evidence：研究MoE服务中路由器决策与token到专家的分配，揭示专家路由机制的攻击面
5. [Triple Expert Learning from Noisy Labels for Semi-Supervised Vision Foundation Model Adaptation](/202608/12/2608.09052v1-triple-expert-learning-from-noisy-labels-for-semi-supervised-vision-foundation-model-adaptation)  
   标签：评分：6.0/10、query:moe-special
   evidence：按置信度区域将未标注样本路由给三个LoRA专家；专家路由与分工
6. [Mixture-of-Experts-based Entropy Model for Learned Image Compression](/202608/12/2608.10947v1-mixture-of-experts-based-entropy-model-for-learned-image-compression)  
   标签：评分：6.0/10、query:moe-special
   evidence：将MoE模型用于图像压缩，选择性激活参数子集


<div class="dpr-home-promo-card">
  <h3 class="dpr-home-promo-title">💬 社区与支持</h3>
  <ul class="dpr-home-promo-list">
    <li>欢迎 Star / Fork / Issue / PR</li>
    <li>QQ群：583867967（欢迎交流，已有：1151人）</li>
  </ul>
</div>
