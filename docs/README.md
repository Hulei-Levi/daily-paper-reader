<div class="dpr-home-notice-card">
  <h3 class="dpr-home-notice-title">🚀 Start Here</h3>
  <ul class="dpr-home-notice-list">
    <li><a href="#/tutorial/README">使用教程</a></li>
  </ul>
</div>

## 每次日报
- 最新运行日期：2026-09-21
- 运行时间：2026-09-21 22:46:16 UTC
- 运行状态：成功
- 本次总论文数：5
- 精读区：1
- 速读区：4

### 今日简报（AI）
今日精读1篇、速读4篇，主题集中在 MoE 路由与专家组合优化，外加一篇城市交通预测应用。

最值得看的是 9.0 分的《Attention-Aware Routing》——把路由与注意力耦合进 MoE，以及 7.0 分的《The Other Half of the Memory Wall》——用可训练的路由预测从 SSD 服务 35B MoE，两条线都指向"让路由更聪明"。

普通读者可先读精读那篇理解路由与注意力耦合的思路，再顺着 SSD 服务与 IntBMoE 两篇看工程落地与块级条件化的不同取舍。
- 详情：[/202609/21/README](/202609/21/README)

### 精读区论文标签
1. [Attention-Aware Routing: Coupling Routing and Attention in MoEs](/202609/21/2609.20974v1-attention-aware-routing-coupling-routing-and-attention-in-moes)  
   标签：评分：9.0/10、query:moe-special
   evidence：改进MoE路由器，基于注意力特征优化专家路由

### 速读区论文标签
1. [The Other Half of the Memory Wall: Serving 35B MoEs from SSD with Trained Routing Prediction](/202609/21/2609.18063v1-the-other-half-of-the-memory-wall-serving-35b-moes-from-ssd-with-trained-routing-prediction)  
   标签：评分：7.0/10、query:moe-special
   evidence：预路由器提前一个token预测下一层专家路由
2. [IntBMoE: Integrating Block-Level Conditioning into Expert Composition for Full-Participation Mixture-of-Experts](/202609/21/2609.21346v1-intbmoe-integrating-block-level-conditioning-into-expert-composition-for-full-participation-mixture-of-experts)  
   标签：评分：7.0/10、query:moe-special
   evidence：混合专家中参与度、执行与物化的专家组合权衡
3. [STHMoE: Hypergraph-Enhanced Heterogeneous Dependency Coordination for LLM-Based Urban Traffic Data Forecasting](/202609/21/2609.15172v1-sthmoe-hypergraph-enhanced-heterogeneous-dependency-coordination-for-llm-based-urban-traffic-data-forecasting)  
   标签：评分：6.0/10、query:moe-special
   evidence：用于时空交通预测的混合专家框架
4. [Who Teaches Which Token? Verifier-Gated Multi-Expert On-Policy Distillation for Scientific Reasoning](/202609/21/2609.15404v2-who-teaches-which-token-verifier-gated-multi-expert-on-policy-distillation-for-scientific-reasoning)  
   标签：评分：6.0/10、query:moe-special
   evidence：验证器门控多专家蒸馏决定哪个专家教哪个token


<div class="dpr-home-promo-card">
  <h3 class="dpr-home-promo-title">💬 社区与支持</h3>
  <ul class="dpr-home-promo-list">
    <li>欢迎 Star / Fork / Issue / PR</li>
    <li>QQ群：583867967（欢迎交流，已有：1151人）</li>
  </ul>
</div>
