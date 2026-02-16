# Inferring Latent Intentions: Attributional Natural Language Inference in LLM Agents

**Paper ID:** arXiv:2601.08742

## Authors
- Xin Quan, Jiafeng Xiong (University of Manchester)
- Marco Valentino (University of Sheffield)
- André Freitas (University of Manchester, Idiap Research Institute, CRUK-MI)

---

## Abstract

We introduce Attributional NLI (Att-NLI), a framework that extends traditional NLI with principles from social psychology to assess agents' capacity for abductive intentional inference. While traditional NLI only judges relationships between premise and hypothesis (entailment, contradiction, neutral), Att-NLI applies abductive reasoning from social psychology. The framework consists of two stages: (1) Abduction - inferring latent intentions from observations, and (2) Deduction - deriving logical conclusions from intentions. We evaluate three agent types through Undercover-V, a verifiable social-deduction game: Standard NLI, Standard Att-NLI, and Neuro-Symbolic Att-NLI. Experimental results show that Neuro-Symbolic Att-NLI achieves 78.29% spy win rate improvement over Standard NLI.

우리는 사회 심리학의 원리를 적용하여 에이전트의 귀납적 의도 추론 능력을 평가하는 프레임워크인 Attributional NLI (Att-NLI)를 소개합니다. 기존의 NLI가 전제와 가설 간의 관계(함의, 모순, 중립)만을 판단하는 반면, Att-NLI는 사회 심리학의 귀납적 추론을 적용합니다. 프레임워크는 두 단계로 구성됩니다: (1) 관찰에서 잠재적 의도 추론, (2) 의도에서 논리적 결론 도출. 우리는 검증 가능한 사회적 추론 게임인 Undercover-V를 통해 세 가지 에이전트 유형을 평가합니다: 표준 NLI, 표준 Att-NLI, 신경-기호 Att-NLI. 실험 결과는 신경-기호 Att-NLI가 표준 NLI보다 78.29% espia 승률 향상을 달성함을 보여줍니다.

---

## Introduction

Understanding intentional behavior is crucial for AI systems that interact with humans. Traditional Natural Language Inference (NLI) focuses on entailment, contradiction, and neutral relationships between premise and hypothesis. However, this approach fails to capture the deeper reasoning about WHY someone made a particular claim.

의도적 행동을 이해하는 것은 인간과 상호작용하는 AI 시스템에게 중요합니다. 기존의 자연어 추론(NLI)는 전제와 가설 간의 함의, 모순, 중립 관계에 중점을 둡니다. 그러나 이 접근법은 누군가 특정 주장을 한 이유에 대한 더 깊은 추론을 포착하지 못합니다.

The key question is: Can AI agents infer the latent intentions behind observed actions? This is essential for trust in AI systems, explainable AI, multi-agent collaboration, and social reasoning.

핵심 질문은: AI 에이전트가 관찰된 행동 뒤에 숨겨진 잠재적 의도를 추론할 수 있는가? 이것은 AI 시스템에 대한 신뢰, 설명 가능한 AI, multi-agent 협력 및 사회적 추론에 필수적입니다.

We propose Attributional NLI (Att-NLI), which extends NLI with social psychology principles: (1) Abductive Reasoning - from observations to possible intentions, and (2) Deductive Reasoning - from intentions to predicted actions. This framework enables agents to understand not just WHAT happened, but WHY it happened - essential for social AI.

우리는 사회 심리학 원리로 NLI를 확장한 Attributional NLI (Att-NLI)를 제안합니다: (1) 귀납적 추론 - 관찰에서 가능한 의도로, (2) 연역적 추론 - 의도에서 예측된 행동으로. 이 프레임워크는 에이전트가 무슨 일이 있었는지뿐 아니라 왜 발생했는지 이해할 수 있게 합니다 - 사회적 AI에 필수적입니다.

---

## Method

### Three Agent Types
1. **Standard NLI Agent**: Uses deduction only
2. **Standard Att-NLI Agent**: Implements abduction → deduction pipeline
3. **Neuro-Symbolic Att-NLI Agent**: Integrates Isabelle/HOL theorem prover for validation

세 가지 에이전트 유형:
1. **표준 NLI 에이전트**: 연역만 사용
2. **표준 Att-NLI 에이전트**: 귀납 → 연역 파이프라인 구현
3. **신경-기호 Att-NLI 에이전트**: 검증을 위해 Isabelle/HOL 정리 증명기 통합

---

## Results

### Table 1: Main Results

| Agent Type | Spy Win Rate | Improvement |
|------------|--------------|-------------|
| Standard NLI | 9.58% | baseline |
| Neuro-Symbolic Att-NLI | **17.08%** | **+78.3%** |

---

## Key Figures

### Figure 1: Att-NLI Process
![Intro](figures/att-nli.intro.png)

### Figure 2: Spy Performance
![Spy](figures/gpt_4o_spy_performance_word_similarity.png)

---

## Main Contributions

1. Attributional NLI framework extending NLI with social psychology
2. Undercover-V verifiable game for empirical testing
3. Demonstrated effectiveness of neuro-symbolic integration
4. 78.3% improvement over baseline

주요 기여:
1. 사회 심리학으로 NLI를 확장한 Attributional NLI 프레임워크
2. 경험적 테스트를 위한 검증 가능한 Undercover-V 게임
3. 신경-기호 통합의 효과 입증
4. baseline 대비 78.3% 향상
