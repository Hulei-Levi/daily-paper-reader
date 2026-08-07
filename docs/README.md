<div class="dpr-home-notice-card">
  <h3 class="dpr-home-notice-title">🚀 Start Here</h3>
  <ul class="dpr-home-notice-list">
    <li><a href="#/tutorial/README">使用教程</a></li>
  </ul>
</div>

## 每次日报
- 最新运行日期：2026-08-07
- 运行时间：2026-08-07 02:05:42 UTC
- 运行状态：成功
- 本次总论文数：8
- 精读区：6
- 速读区：2

### 今日简报（AI）
今日聚焦MoE优化：无训练路由插件与内存高效Sinkhorn训练双双获9分高分。  
最值得精读两篇9分论文：Elbow-Based路由实现免训练专家选择，MESH用Sinkhorn降低MoE训练内存开销；另可速览资源感知多语言语音翻译。  
建议先攻克两篇高影响力MoE方法，再跳读语音翻译的编码器混合思路。
- 详情：[/202608/07/README](/202608/07/README)

### 精读区论文标签
1. [Elbow-Based MoE Routing: A Training-Free Inference Time Plugin for Expert Selection](/202608/07/2608.04401v1-elbow-based-moe-routing-a-training-free-inference-time-plugin-for-expert-selection)  
   标签：评分：9.0/10、query:moe-special
   evidence：面向专家选择的免训练推理插件，逐词元动态调整激活专家数量
2. [MESH: Memory-Efficient Sinkhorn Optimization for Mixture-of-Experts Training](/202608/07/2608.04407v1-mesh-memory-efficient-sinkhorn-optimization-for-mixture-of-experts-training)  
   标签：评分：9.0/10、query:moe-special
   evidence：混合专家训练优化，路由专家矩阵分析
3. [Beyond Global Routing Aggregation: Phase-Aware Expert Merging for MoE Vision-Language Models](/202608/07/2608.04454v1-beyond-global-routing-aggregation-phase-aware-expert-merging-for-moe-vision-language-models)  
   标签：评分：9.0/10、query:moe-special
   evidence：研究MoE视觉语言模型中相位感知的专家合并与路由专业化
4. [Semiparametric robust mixture of experts based on nonparametric maximum likelihood](/202608/07/2608.04561v1-semiparametric-robust-mixture-of-experts-based-on-nonparametric-maximum-likelihood)  
   标签：评分：9.0/10、query:moe-special
   evidence：提出一种使用非参数最大似然估计的半参数混合专家模型，用于稳健的专家误差分布
5. [Personalized Federated Sparse Adaptation of Time-Series Foundation Models](/202608/07/2608.04695v1-personalized-federated-sparse-adaptation-of-time-series-foundation-models)  
   标签：评分：9.0/10、query:moe-special
   evidence：使用时序异质MoE适配器，通过top-k路由选择专门化专家
6. [K-EXAONE 2.0 Technical Report](/202608/07/2608.04505v1-k-exaone-20-technical-report)  
   标签：评分：8.0/10、query:moe-special
   evidence：包含750B总参数、约37B激活参数的稀疏混合专家模型

### 速读区论文标签
1. [Breaking the Curse ofMultilinguality inMany-to-Many Speech-to-Text Translation via a Resource-AwareMixture of Speech Encoders](/202608/07/2608.04586v1-breaking-the-curse-ofmultilinguality-inmany-to-many-speech-to-text-translation-via-a-resource-awaremixture-of-speech-encoders)  
   标签：评分：8.0/10、query:moe-special
   evidence：资源感知的混合语音编码器，以语言路由为每个话语分配专家编码器
2. [MobileWAM: Bridging World Action Models to Mobile Manipulation with Chain-of-Foresight](/202608/07/2608.04657v1-mobilewam-bridging-world-action-models-to-mobile-manipulation-with-chain-of-foresight)  
   标签：评分：6.0/10、query:moe-special
   evidence：混合Transformer架构，三专家混合动作专家


<div class="dpr-home-promo-card">
  <h3 class="dpr-home-promo-title">💬 社区与支持</h3>
  <ul class="dpr-home-promo-list">
    <li>欢迎 Star / Fork / Issue / PR</li>
    <li>QQ群：583867967（欢迎交流，已有：1151人）</li>
  </ul>
</div>
