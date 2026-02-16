# Inferring Latent Intentions: Attributional Natural Language Inference in LLM Agents

**Paper ID:** arXiv:2601.08742

## Authors
- Xin Quan, Jiafeng Xiong (University of Manchester)
- Marco Valentino (University of Sheffield)
- André Freitas (University of Manchester, Idiap Research Institute, CRUK-MI)

## Abstract
Attributional NLI (Att-NLI)를 도입합니다. 기존 NLI를 사회 심리학 원리로 확장하여 에이전트의 귀납적 의도 추론 능력과 연역적 검증을 평가합니다. Undercover-V 게임을 통해 평가합니다.

## Method

### Two-Stage Reasoning
1. **Abduction (추론)**: 관찰에서 잠재적 의도 추론
2. **Deduction (연역)**: 의도로부터 논리적 결론 도출

### 세 가지 에이전트 유형
1. **Standard NLI**: 연역만 사용
2. **Standard Att-NLI**: 추론 → 연역
3. **Neuro-Symbolic Att-NLI**: Isabelle 정리 증명기 통합

## Results

### Table 1: Main Results

| Agent Type | Spy Win Rate | Attributional Score |
|------------|--------------|---------------------|
| Standard NLI | 9.58% | 0.512 |
| Standard Att-NLI | 13.75% | 0.645 |
| **Neuro-Symbolic Att-NLI** | **17.08%** | **0.780** |

## Key Figures

### Figure 1: Att-NLI Process
![Intro](figures/att-nli.intro.png)
- Att-NLI 과정示意

### Figure 2: Spy Performance (GPT-4o)
![Spy](figures/gpt_4o_spy_performance_word_similarity.png)
- 에이전트 유형별 espia 성능

### Figure 3: Undercover-V Framework
![Framework](figures/undercover_main.drawio.png)
- 게임 프레임워크

## Main Contributions
1. Attributional NLI 프레임워크
2. Undercover-V 검증 가능한 게임
3. 신경-기호 통합의 효과 입증
