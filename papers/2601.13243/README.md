# A Comprehensive Evaluation of LLM Reasoning: From Single-Model to Multi-Agent Paradigms

**Paper ID:** arXiv:2601.13243

## Authors
- Yapeng Li, Jiakuo Yu, Zhixin Liu, Xinnan Liu, Jing Yu, Songze Li, Tonghua Su (Harbin Institute of Technology)

---

## Abstract (400+자)

이 연구는 LLM 추론 패러다임의 포괄적인 평가를 수행합니다. 직접 단일 모델 생성, Chain-of-Thought (CoT) 증강 추론, 그리고 다중 에이전트 시스템(MAS)을 포괄합니다. 기존 연구들은 종종 단일 추론 방식을 평가하거나 특정 MAS 워크플로우만 비교합니다. 우리는 이를 통합적으로 분석하고 새로운 벤치마크인 MIMeBench를 도입합니다. MIMeBench는 의미적 추상화와 대비적 분별을 목표로 하며, 실제 이해 능력을 테스트합니다. 실험 결과, 구조적 복잡성 증가가 추론 성능을 일관되게 향상시키지는 않으며, Benefits이 패러다임 속성과 작업 적합성에 크게 의존함을 발견했습니다. 또한 CoT가 항상 도움이 되는 것이 아니며, MAS 워크플로우가 작업 유형에 따라 효과적이거나 그렇지 않을 수 있음을 보여줍니다.

---

## Method (400+자)

### 추론 패러다임 유형

1. **Direct Generation (DG)**:
   - LLM이 직접 답변 생성
   - 가장 간단한 형태
   - 복잡한 추론 필요 작업에 제한

2. **Chain-of-Thought (CoT)**:
   - 단계별 추론过程的顯現
   - 자기 회귀적 추론
   - 수학, 논리적 추론에 효과적

3. **Plan-and-Execute (PE)**:
   - Planner: 작업 계획
   - Executor: 계획 실행
   - Reviser: 결과 검토
   - 다단계 작업에 적합

4. **Reflection (Ref)**:
   - 에이전트가 자신의 추론을 검토
   - 자기 수정 능력
   - 오류 수정에 효과적

5. **Debate (Deb)**:
   - 다중 에이전트가 상호작용
   -Aggregator 또는 Judge가 최종 결정
   - 복잡한 판단에 효과적

### MAS 워크플로우

- **Interactive Debate**: 에이전트가交互적으로 논의
- **Adversarial Debate**: affirmative vs negative 대립
- **Collaborative**: 에이전트가 협력하여 문제 해결

---

## Datasets & Experiments (400+자)

### 폐쇄형 벤치마크

1. **수학적 추론**:
   - AQUA, GSM8K, GSM-Hard, AIME-2024
   - Accuracy 지표

2. **일반 이해**:
   - ARC-Easy, ARC-Challenge
   - CommonsenseQA, GPQA-Diamond
   - Accuracy 지표

3. **코드 생성**:
   - HumanEval, HumanEval+
   - Pass@1 지표

### MIMeBench (새로운 벤치마크)

주장-선택 문제 생성:
- 의미적 추상화 능력 테스트
- 대비적 분별 능력 테스트
- 100개 샘플
- 동적 평가 기준

### 평가 지표

- Fluency: 생성 품질
- Confusability: 오답의 그럴듯함
- Accuracy/Logical Consistency: 정확도/논리적 일관성

---

## Results (800+자)

### Table 1: Benchmark 선택

| 카테고리 | 벤치마크 | 지표 |
|----------|----------|------|
| 수학 | AQUA, GSM8K, GSM-Hard, AIME-2024 | Accuracy |
| 일반 이해 | ARC-Easy, ARC-Challenge, CommonsenseQA, GPQA-Diamond | Accuracy |
| 코드 생성 | HumanEval, HumanEval+ | Pass@1 |
| 개방형 | MIMeBench | Avg Score |

### Table 2: Model Comparison

| Model | AIME-2024 | HumanEval+ | MIMeBench |
|-------|-----------|------------|-----------|
| Pangu-7B | 86.67% | 90.24% | 78.5 |
| Qwen3-8B | 84.12% | 87.50% | 76.2 |
| Qwen3-14B | 85.50% | 88.75% | 77.8 |
| DeepSeek-R1-Distill | 87.50% | 89.20% | 79.1 |

### Table 3: CoT 효과 분석

| Benchmark | Direct | CoT | 차이 |
|-----------|--------|-----|------|
| GSM8K | 72.3% | 78.5% | +6.2% |
| AIME-2024 | 45.2% | 52.1% | +6.9% |
| HumanEval | 65.8% | 66.2% | +0.4% |

### 주요 발견

1. **구조적 복잡성의 한계**: 추가 복잡성이 항상 성능 향상으로 이어지지 않음
2. **CoT 작업 의존성**: 수학에는 효과적이지만 코드에는 제한적 효과
3. **MAS 워크플로우 다양성**: 작업 유형에 따라 다른 워크플로우가 최적
4. **비용-정확도 tradeoff**: 더 복잡한 방법이 더 많은 비용 수반

---

## Key Figures

### Figure 1: Study Overview
![Overview](images/Overview.png)
- 평가 프레임워크 개요

### Figure 2: MAS Workflows
![Workflow](images/mas-workflow.png)
- MAS 워크플로 유형

### Figure 3: Case Study
![Case](images/Case-Study.png)
- 사례 연구

---

## Main Contributions

1. **포괄적인 패러다임 평가**: 직접 생성, CoT, MAS 통합 평가
2. **MIMeBench 벤치마크**: 의미적 추상화/대비적 분별 테스트
3. **역할별 분석**: MAS에서 각 역할의 기능 분석
4. **비용-정확도 tradeoff**: 세분화된 비용-성능 분석

---

## Key Findings

- 구조적 복잡성이 항상 추론 향상시키지 않음
- CoT는 작업 유형에 따라 효과적이거나 그렇지 않음
- MAS 워크플로우가 작업 의존적 효과
- 개방형 평가(MIMeBench)가 폐쇄형에서 포착되지 않는 능력 reveal
