# Learning Decentralized LLM Collaboration with Multi-Agent Actor Critic

**Paper ID:** arXiv:2601.21972

## Authors
- Shuo Liu, Tianle Chen, Ryan Amiri, Christopher Amato (Northeastern University)

---

## Abstract (400+자)

최근 Multi-Agent Reinforcement Learning (MARL)을 통해 LLM 협력을 최적화하는 연구가 진행되고 있습니다. 그러나 대부분의 MARL fine-tuning 접근법은 사전 정의된 실행 프로토콜에 의존하며, 종종 중앙집중식 실행이 필요합니다. 분산 LLM 협력이 실제로 더 매력적인데, 에이전트가 병렬로 추론을 실행하고 유연하게 배포될 수 있기 때문입니다. 또한 현재 접근법은 Monte Carlo 방법을 사용하는데, 이는 높은 분산으로 인해 더 많은 샘플이 필요합니다. Actor-Critic 방법은 이러한 문제를 해결하기 위해 MARL에서 널리 사용되며, 우리는 분산 LLM 협력을 최적화하기 위한 Multi-Agent Actor-Critic (MAAC) 방법을 개발했습니다. 우리는 CoLLM-CC (중앙 집중식 Critic)와 CoLLM-DC (분산 Critic) 두 가지 접근법을 제안합니다. 글쓰기, 코딩, 게임 영역에 걸친 실험에서 단기/밀집 보상 설정에서 Monte Carlo 방법과 CoLLM-DC가 CoLLM-CC에 필적하는 성능을 달성할 수 있음을 보여줍니다. 그러나 장기/희소 보상 작업에서 Monte Carlo 방법이 훨씬 더 많은 샘플이 필요하고 CoLLM-DC가 수렴하지 못하는 반면 CoLLM-CC가优异합니다.

---

## Method (400+자)

### MA-REINFORCE (Multi-Agent REINFORCE)

MA-REINFORCE는 각 에이전트가 개별 정책 πθi를 유지하고 결합 반환의 Monte-Carlo 추정에 따라 업데이트하는 다중 에이전트 정책 그래디언트 방법입니다. 수학적으로 ∇θi J(θi) = Eπ[Σ ρi,t ∇θi log πθi(ai,t | hi,t) G(ht)]로 표현됩니다. 그러나 이 방법은 장기 호라이존 온라인 학습에 잘 확장되지 않는데, 반환 신호가 대화 종료시에만 사용 가능하고 Monte Carlo 추정이 축적된 확률성으로 인해 높은 분산을 겪기 때문입니다.

### Multi-Agent Actor-Critic (MAAC)

분산성을 줄이고 샘플 효율성을 개선하기 위해 Actor-Critic (AC) 방법은 정책 모델(actor) πθ와 값 모델(critic) Vϕ를 학습합니다. 다중 에이전트 설정에서 AC 방법은 Decentralized Critics (DC) 또는 Centralized Critic (CC)와 함께 사용됩니다. DC에서는 각 에이전트 i가 로컬 critic Vϕi(hi,t)를 유지하고, CC에서는 공유 critic Vϕ(ht)가 joint history를 조건으로 합니다. Critic은 학습 구조일 뿐이므로 실행 시 제거할 수 있습니다.

### CoLLM-CC (Centralized Critic)

CoLLM-CC는 joint history ht를 조건으로 하는 중앙 집중식 critic Vϕ를 학습합니다. 각 에이전트의 정책 πθi(·|hi,t)를 업데이트하기 위해 ∇θi J(θi) = Eπ[Σ ρi,t ∇θi log πθi(ai,t | hi,t) δt]를 사용합니다. 여기서 δt = rt + γVϕ(ht+1) - Vϕ(ht)입니다.

### CoLLM-DC (Decentralized Critic)

CoLLM-DC는 각 에이전트가 자신의 로컬 history hi,t를 조건으로 하는 개별 critic Vϕi를 사용합니다. 이는 학습 중 비정상성이 누적되어 수렴하기 어려울 수 있습니다.

### K-Sampling MA-REINFORCE

K-샘플링은 그래디언트 추정의 분산을 줄이지만, 추론 호출 수가 기하급수적으로 증가합니다. 전체 K-ary rollout 트리의 경우 필요한 추론 호출 수는 Ncall(n, K, H) = nK(K^(H-1) - 1)/(K-1)입니다.

---

## Datasets & Experiments (400+자)

### TLDR Summarization (글쓰기 협업)

TLDR 요약에서 2개의 Qwen3-1.7B 에이전트가 Reddit 게시물을 요약합니다. 하나는 높은 수준의 요약자로 간결한 단락을 생성하고, 다른 하나는 더 포괄적인 정보를 제공하는 상세 요약자 역할을 합니다. 글쓰기 품질은 3가지 메트릭의 가중 합으로 평가됩니다: 구조(응답 길이 비율), 스타일 일관성(Jaccard 유사도), 논리적 일관성(전환어 빈도).

### arXiv Expansion (논문 확장)

동일한 에이전트가 arXiv 초안을 완전한 서론으로 확장합니다. 하나는 연구 배경과 동기를 설명하고 다른 하나는 제안된 방법과 실험을 제시합니다. 이는 장문 처리의 효율성을 테스트합니다.

### CoopHE (협력적 코드 생성)

CoopHumanEval 데이터셋은 자연스럽게 협력적 분해가 가능한 문제를 포함합니다. 보조 에이전트 aux 함수로 지원하고 주 에이전트가 핵심 로직을 생성합니다. 에이전트는 AST(추상 구문 트리) 또는 동적 실행(샌드박스 테스트)의 피드백을 받고 다음 턴으로 진행합니다.

### StrBuild (Minecraft 문자 건축)

각 에이전트의 리소스가 제한됩니다. 목표 건물은 동일한 텍스처 분포를 유지하면서 정확한 문자열과 일치해야 합니다. IoU(Intersection over Union)가 평가 지표로 사용됩니다.

### HouseBuild (Minecraft 집 건설)

더 높은 수준의 상호작용과 확률성을 가집니다. 동일 에이전트가 사전 정의된 건축 사양(예: 집)을 준수하는 집을 협업적으로 구축하면서 적대적 몹(거미)의 공격을 방어해야 합니다. 공격이 성공적으로 막했는지 여부를 나타내는 평균 체력 포인트가 지표로 사용됩니다.

---

## Results (800+자)

### Table 1: Overall Performance Comparison

| Method | TLDR Time | TLDR Cost | TLDR Score | arXiv Time | arXiv Cost | arXiv Score | StrBuild Time | StrBuild Cost | StrBuild Adj | StrBuild IoU |
|--------|-----------|-----------|------------|------------|------------|-------------|---------------|---------------|--------------|--------------|
| Raw Model | 5.0 | 465 | 30.3 | 5.1 | 472 | 44.0 | 10.6 | 427 | 0.9 | 36.6 |
| GRPO | 4.1 | 387 | 91.7 | 4.2 | 398 | 91.0 | 10.3 | 411 | 0.4 | 46.1 |
| AC | 4.0 | 374 | 94.7 | 4.3 | 392 | 95.3 | 10.3 | 413 | 0.4 | 49.8 |
| Parallel | 2.3 | 244 | 22.7 | 2.3 | 246 | 49.0 | 9.4 | 232 | 15.7 | 5.9 |
| Pipeline | 4.3 | 238 | 21.7 | 3.9 | 203 | 57.0 | 9.8 | 246 | 12.9 | 18.7 |
| Discussion | 4.6 | 234 | 22.3 | 4.8 | 251 | 54.3 | 10.3 | 236 | 16.2 | 6.5 |
| MAGRPO | 1.8 | 178 | 93.5 | 2.0 | 201 | 93.1 | 9.4 | 226 | 13.3 | 50.6 |
| CoLLM-DC | 1.9 | 194 | 95.4 | 2.0 | 196 | 94.1 | 9.3 | 182 | 7.6 | 44.6 |
| **CoLLM-CC** | **1.8** | **181** | **95.2** | **1.9** | **188** | **95.0** | **9.5** | **239** | **7.3** | **68.5** |

### 주요 발견

1. **Writing Tasks (TLDR, arXiv)**: 단기/밀집 보상 설정에서 모든 MARL 방법이 유사한 성능을 달성합니다. CoLLM-CC가 최고 성능을 달성하면서도 낮은 분산을 보입니다.

2. **Coding Tasks (CoopHE)**: 협업적 코드 생성에서 CoLLM-CC가 75.2% 통과율을 달성합니다.

3. **Minecraft Tasks (StrBuild, HouseBuild)**: 장기 호라이존 설정에서 CoLLM-CC가 다른 방법들을 크게 앞서며, 특히 StrBuild에서 IoU 68.5%를 달성합니다. Monte Carlo 방법(MAGRPO)은 더 많은 샘플이 필요하고 CoLLM-DC는 수렴하지 못합니다.

4. **Cost Efficiency**: CoLLM-CC는 다른 방법 대비 더 낮은 토큰 비용으로 더 나은 성능을 달성합니다.

---

## Key Figures

### Figure 1: CoLLM-CC Framework
![Framework](figs/framework.png)
- (a) 에이전트 모델 구조: Transformer 블록 + KV-Cache
- (b) 중앙 집중식 Critic 아키텍처 전체
- (c) Critic 모델 구조

### Figure 2: CoLLM-DC Framework
![Framework-DC](figs/framework-dc.png)
- 분산 Critic 아키텍처: 각 에이전트가 개별 Critic 보유

### Figure 3: TLDR Results
![TLDR](figs/writing_tldr.png)
- TLDR 요약 작업에서 학습 곡선 비교

### Figure 4: arXiv Results
![arXiv](figs/writing_arxiv.png)
- arXiv 확장 작업에서 학습 곡선

### Figure 5: Code Generation
![CodeGen](figs/codegen_coophe.png)
- CoopHE 코드 생성 작업 결과

### Figure 6: Minecraft StrBuild
![Minecraft](figs/minecraft_str.png)
- StrBuild 작업 예시 (ICML 형태 건축)

### Figure 7: Minecraft HouseBuild
![HouseBuild](figs/minecraft_box.png)
- HouseBuild 작업 예시 (집 건설 + 적 방어)

---

## Main Contributions

1. **분산 LLM 협력을 위한 MAAC 방법 개발**: 다중 에이전트 Actor-Critic 방법을 분산 LLM 협력에 적용하고 그 장점을 분석했습니다.

2. **CoLLM-CC와 CoLLM-DC 두 가지 접근법 제안**: 중앙 집중식 Critic(CC)과 분산 Critic(DC) 두 가지 방법을 제안하고 비교했습니다.

3. **포괄적인 실험 평가**: 글쓰기, 코딩, 게임 영역에 걸친 다양한 작업에서 광범위한 실험을 수행했습니다.

4. **장기/희소 보상 작업에서 CoLLM-CC의 우위 입증**: Monte Carlo 방법과 비교하여 CoLLM-CC가 장기 작업에서 훨씬 뛰어난 성능을 보임을 입증했습니다.

---

## Key Findings

- CoLLM-CC가最低 분산과 최고 샘플 효율성을 달성합니다.
- 장기 작업에서 Monte Carlo 방법(MAGRPO)이 훨씬 더 많은 샘플이 필요합니다.
- CoLLM-DC는 장기 설정에서 비정상성 누적으로 인해 수렴하기 어렵습니다.
- 중앙 집중식 Critic이 분산 Critic보다 안정적인 그래디언트 추정을 제공합니다.
