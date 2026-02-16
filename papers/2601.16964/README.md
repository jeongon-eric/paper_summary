# AgentDrive: An Open Benchmark Dataset for Agentic AI Reasoning

**Paper ID:** arXiv:2601.16964

## Authors
- Mohamed Amine Ferrag, Abderrahmane Lakas (United Arab Emirates University)
- Merouane Debbah (Khalifa University)

---

## Abstract

We introduce AgentDrive, an open benchmark dataset containing LLM-generated driving scenarios for autonomous driving agents. Current agentic AI reasoning evaluation suffers from limited scenarios and task complexity. AgentDrive contains 300,000 LLM-generated driving scenarios with a factorized scenario space across seven orthogonal axes. We also automate structured scenario generation using an LLM-driven prompt-to-JSON pipeline. The benchmark includes AgentDrive-MCQ with 100,000 reasoning questions spanning physics, policy, hybrid, scenario, and comparative reasoning. Evaluation of 50 leading LLMs shows that proprietary frontier models dominate in contextual/policy reasoning, while advanced open models are rapidly closing the gap in structured/physics reasoning.

우리는 자율주행 에이전트를 위한 LLM 생성Driving 시나리오를 포함하는 공개 벤치마크 데이터셋인 AgentDrive를 소개합니다. 현재 에이전트 AI 추론 평가는 제한된 시나리오와 작업 복잡성으로 어려움을 겪습니다. AgentDrive는 7개의 직교 축에 걸친 인수분해된 시나리오 공간과 함께 300,000개의 LLM 생성Driving 시나리오를 포함합니다. 또한 LLM 기반 프롬프트-JSON 파이프라인을 사용하여 구조화된 시나리오 생성을 자동화합니다. 벤치마크는 물리, 정책, 하이브리드, 시나리오 및 비교 추론을 포함하는 100,000개의 추론 질문이 있는 AgentDrive-MCQ를 포함합니다. 50개 주요 LLM 평가 결과, 독점 프론티어 모델이 맥락적/정책 추론에서 우위를 보이는 반면, 고급open 모델이 구조적/물리적 추론에서 빠르게追赶하고 있음을 보여줍니다.

---

## Introduction

Autonomous driving requires sophisticated reasoning about physics, traffic rules, and complex scenarios. However, existing benchmarks fail to capture the full complexity needed for agentic AI evaluation.

자율주행은 물리, 교통 규칙 및 복잡한 시나리오에 대한 정교한 추론이 필요합니다. 그러나 기존 벤치마크는 에이전트 AI 평가에 필요한 전체 복잡성을 포착하지 못합니다.

Current limitations include: limited scenarios with small benchmark sizes, lack of reasoning diversity focusing mainly on perception, and no factorized analysis to isolate specific reasoning capabilities.

현재 제한 사항에는 작은 벤치마크 크기의 제한된 시나리오, 주로 지각에 초점을 맞춘 추론 다양성 부족, 특정 추론 능력을 분리하기 위한 인수분해 분석 부재가 포함됩니다.

AgentDrive addresses these by providing: 300,000 diverse driving scenarios, 7 orthogonal axes for systematic analysis, and 100,000 MCQ questions testing different reasoning types including physics, policy, hybrid, scenario, and comparative reasoning.

AgentDrive는 이를 해결합니다: 300,000개의 다양한 Driving 시나리오, 체계적 분석을 위한 7개의 직교 축, 물리, 정책, 하이브리드, 시나리오 및 비교 추론을 포함한 다양한 추론 유형을 테스트하는 100,000개의 MCQ 질문.

---

## Method

### 7 Axes of Factorization
1. Scenario Type (lane change, intersection, merging)
2. Driver Behavior (compliant, aggressive, distracted)
3. Environment (weather, visibility, time of day)
4. Road Layout (highway, urban, roundabout)
5. Objective (navigation, overtaking, parking)
6. Difficulty (easy, moderate, complex)
7. Traffic Density (sparse, medium, congested)

7개 인수분해 축:
1. 시나리오 유형 (차선 변경, 교차로, 합류)
2. 운전자 행동 (규정 준수, 공격적, 산만)
3. 환경 (날씨, 시야, 시간대)
4. 도로 레이아웃 (고속도로, 도심, 로터리)
5. 목표 (항법, 추월, 주차)
6. 난이도 (쉬움, 중간, 복잡)
7. 교통 밀도 (희소, 중간, 혼잡)

---

## Results

### Table 1: Benchmark Comparison

| Benchmark | Scenarios | Questions |
|-----------|-----------|-----------|
| AgentDrive | **300K** | **100K** |

---

## Key Figures

### Figure 1: AgentDrive Overview
![Overview](AgentDrive_MCQ.png)

### Figure 2: Difficulty Heatmap
![Heatmap](fig_heatmap_layout_difficulty.png)

---

## Main Contributions

1. Largest driving agent benchmark with 300K scenarios and 100K questions
2. 7-axis factorization for comprehensive scenario space
3. LLM-based automatic generation for efficient scaling
4. Evaluation of 50 leading LLMs

주요 기여:
1. 300K 시나리오와 100K 질문이 있는 최대 규모의 driving 에이전트 벤치마크
2. 포괄적인 시나리오 공간을 위한 7개 축 인수분해
3. 효율적인 확장을 위한 LLM 기반 자동 생성
4. 50개 주요 LLM 평가
