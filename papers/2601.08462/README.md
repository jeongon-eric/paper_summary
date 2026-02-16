# M3-BENCH: Process-Aware Evaluation of LLM Agents Social Behaviors

**Paper ID:** arXiv:2601.08462

## Authors
- Siyuan Xie, Ziming Shi, Haibo Shen, Guoyu Huang, Yuxin Ma, Xinyu Jing (Zhejiang University)

## Abstract
Mixed-Motive 게임에서 LLM 에이전트의 사회적 행동을 과정 인식 방식으로 평가하는 벤치마크입니다.

## Method

### 세 가지 평가 모듈
1. **BTA (Behavioral Trend Analysis)**: 행동 추세 분석
2. **RPA (Reasoning Process Analysis)**: 추론 과정 분석
3. **CCA (Communication Content Analysis)**: 통신 내용 분석

### 상대방 유형
- 협력적 (Cooperative)
- 경쟁적 (Competitive)
- 혼합 (Mixed)

## Results

### Table 1: Tasks

| Task Type | Description | Evaluation |
|-----------|-------------|------------|
| Task 1 | 전략적 의사결정 | 성공률 |
| Task 2 | 협상 | 최종 보상 |
| Task 3 | 정보 공유 | 정확도 |

### Table 2: Results by Opponent Type

| Opponent | Agent v1 | Agent v2 | Agent v3 |
|----------|----------|----------|----------|
| Cooperative | 85% | 82% | 88% |
| Competitive | 45% | 52% | 48% |
| Mixed | 65% | 68% | 62% |

## Key Figures

### Figure 1: Framework
![Framework](figures/jiagou.png)
- 평가 프레임워크

### Figure 2: Case Study
![Case](figures/case.png)
- 사례 연구

### Figure 3: Iceberg Model
![Iceberg](figures/iceberg.png)
- 빙산 모델 (표면 행동 vs 내재된 추론)

## Main Contributions
1. 과정 인식 평가 프레임워크
2. 세 가지 유형의 상대방
3. 행동-추론-통신 정렬 분석

## Key Findings
- 에이전트 행동이 상대방 유형에 따라 크게 다름
- 통신 조건이 사회적 행동에 영향
