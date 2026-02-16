# AgentDrive: An Open Benchmark Dataset for Agentic AI Reasoning

**Paper ID:** arXiv:2601.16964

## Authors
- Mohamed Amine Ferrag, Abderrahmane Lakas (United Arab Emirates University)
- Merouane Debbah (Khalifa University)

## Abstract
300,000개의 LLM 생성 driving 시나리오를 포함하는 벤치마크입니다. 7개 직교 축의 인수분해된 시나리오 공간과 100,000개의 추론 질문이 포함됩니다.

## Method

### 7개 직교 축
1. Scenario Type (차선 변경, 교차로, 합류...)
2. Driver Behavior (규정 준수, 공격적, 산만...)
3. Environment (날씨, 시야, 시간대)
4. Road Layout (고속도로, 도심, 로터리)
5. Objective (안전 항법, 추월, 비상 정지)
6. Difficulty (쉬움, 중간, 복잡)
7. Traffic Density (희소, 중간, 혼잡)

### AgentDrive-MCQ 추론 차원
- Physics: 차량 동역학
- Policy: 교통 규칙 이해
- Hybrid: 물리 + 정책
- Scenario: 상황 인식
- Comparative: 시나리오 간 비교

## Results

### Table 1: Benchmark 비교

| Benchmark | 시나리오 수 | 추론 질문 | 추론 차원 |
|-----------|-------------|-----------|-----------|
| LaMPilot | 10K | 10K | 3 |
| V2V-LLM | 5K | 5K | 2 |
| STSBench | 15K | - | 1 |
| **AgentDrive** | **300K** | **100K** | **5** |

## Key Figures

### Figure 1: AgentDrive Overview
![Overview](AgentDrive_MCQ.png)
- 벤치마크 구성요소

### Figure 2: Results Heatmap
![Heatmap](fig_heatmap_layout_difficulty.png)
- 난이도별 성능 히트맵

### Figure 3: Weather Distribution
![Weather](fig_weather_share.png)
- 날씨별 시나리오 분포

## Main Contributions
1. 300K 시나리오, 100K 질문
2. 7개 축의 포괄적 인수분해
3. 50개 LLM 평가
