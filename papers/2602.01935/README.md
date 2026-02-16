# COLT: Lightweight Multi-LLM Collaboration through Shared MCTS Reasoning

**Paper ID:** arXiv:2602.01935

## Authors
- Albert Shyuan Tang, Carey Priebe, Qin (Luna) Lu, Hadi Esmaeilzadeh (Johns Hopkins University)

---

## Abstract

We propose COLT (Collaborative Optimization via Lightweight Threads), a lightweight multi-LLM collaboration framework for compiler optimization. While recent LLMs have proven effective for code generation and transformation, a single LLM struggles to make complex optimization decisions. COLT implements multi-LLM collaboration through Monte Carlo Tree Search (MCTS) reasoning sharing. The key innovation is that the current model generates a reasoning tree which collaborating models use to select arms. Information communication is performed through shared KV cache, reducing communication overhead. Compared to LLMCompiler, COLT achieves 53% latency reduction and 87% cost reduction while achieving equal or better performance.

우리는 컴파일러 최적화를 위한 경량 multi-LLM 협력 프레임워크인 COLT (Collaborative Optimization via Lightweight Threads)를 제안합니다. 최근 LLM이 코드 생성 및 변환에 효과적인 것으로 입증되었지만, 단일 LLM은 복잡한 최적화 결정을 내리는 데 어려움을 겪습니다. COLT는 Monte Carlo Tree Search (MCTS) reasoning 공유를 통해 multi-LLM 협력을 구현합니다. 핵심 혁신은 현재 모델이 협력 모델이 arms를 선택하는 데 사용하는 reasoning 트리를 생성한다는 것입니다. 정보 통신은 공유 KV 캐시를 통해 수행되어 통신 오버헤드를 줄입니다. LLMCompiler와 비교하여 COLT는 동등하거나 더 나은 성능을 달성하면서 53% 지연 시간 감소와 87% 비용 감소를 달성합니다.

---

## Introduction

Compiler optimization is complex and traditionally relies on expert-designed heuristics. Recent LLMs can help but single models struggle with complex optimization decisions.

컴파일러 최적화는 복잡하며 전통적으로 전문가 설계 휴리스틱에 의존합니다. 최근 LLM이 도움이 될 수 있지만 단일 모델은 복잡한 최적화 결정에서 어려움을 겪습니다.

Key challenges include: single model limitations where one model cannot handle all optimization types, communication overhead where multi-agent approaches are often expensive, and reasoning complexity where optimization requires deep reasoning.

핵심 도전에는 단일 모델 한계(하나의 모델이 모든 최적화 유형을 처리할 수 없음), 통신 오버헤드(multi-agent 접근법이 종종 비싸며), 최적화가 깊은 추론을 필요로 하는 추론 복잡성이 포함됩니다.

COLT addresses these by sharing reasoning trees between models, using MCTS for structured exploration, and leveraging complementary model strengths through collaborative decision-making.

COLT는 모델 간 reasoning 트리 공유, 구조화된 탐사를 위한 MCTS 사용, 협력적 의사결정을 통한 보완적 모델 강점 활용을 통해这些问题을 해결합니다.

---

## Method

### COLT Architecture
1. **Reasoning Tree Generation**: Master model generates decision tree
2. **Arm Selection**: Collaborating models select optimal branches
3. **Shared KV Cache**: Reduces communication overhead

COLT 아키텍처:
1. **추론 트리 생성**: 마스터 모델이 결정 트리 생성
2. **Arm 선택**: 협력 모델이 최적 branch 선택
3. **공유 KV 캐시**: 통신 오버헤드 감소

---

## Results

### Table 1: Performance Comparison

| Method | Latency | Cost |
|--------|---------|------|
| LLMCompiler | baseline | baseline |
| COLT | **-53%** | **-87%** |

---

## Key Figures

### Figure 1: Overview
![Overview](figs/overview.png)

---

## Main Contributions

1. MCTS-based lightweight collaboration framework
2. Shared KV cache for efficiency
3. Both latency and cost improvements
4. Practical compiler optimization application

주요 기여:
1. MCTS 기반 경량 협력 프레임워크
2. 효율성을 위한 공유 KV 캐시
3. 지연 시간과 비용 모두 개선
4. 실용적인 컴파일러 최적화 적용
