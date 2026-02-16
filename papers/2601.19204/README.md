# MATA: A Trainable Hierarchical Automaton System for Multi-Agent Visual Reasoning

**Paper ID:** arXiv:2601.19204 (ICLR 2026)

## Authors
- Zhixi Cai, Fucai Ke, Kevin Leo, Sukai Huang, Maria Garcia de la Banda, Peter J. Stuckey, Hamid Rezatofighi (Monash University)

## Abstract
MATA (Multi-Agent hierarchical Trainable Automaton)는 시각적 추론을 위한 계층적 유한 상태 오토마톤입니다. 최상위 전이는 학습 가능한 하이퍼 에이전트가 선택하고, 각 에이전트는 규칙 기반 서브 오토마톤을 실행합니다.

## Method

### 계층적 오토마톤 구조
- **Hyper Agent**: 상태 전이 선택 (학습 가능)
- **Sub Automata**: 규칙 기반 마이크로 컨트롤

### 상태 종류
1. INITIAL
2. ONESHOT (일회 추론)
3. STEPWISE (단계별 추론)
4. SPECIALIZED (전문 에이전트)
5. FINAL
6. FAILURE

## Results

### Table 1: GQA Performance

| Method | Accuracy (%) |
|--------|--------------|
| ViperGPT | 37.9 |
| VisRep | 51.4 |
| HYDRA | 52.8 |
| **MATA** | **64.9** |

### Table 2: OK-VQA Performance

| Method | Accuracy (%) |
|--------|--------------|
| GPT-4o | 75.7 |
| DWIM | 62.8 |
| **MATA** | **76.5** |

## Key Figures

### Figure 1: MATA Overview
![Teaser](image/teaser.png)
- 오토마톤 구조 개요

### Figure 2: Pipeline
![Pipeline](image/pipeline.png)
- 학습 파이프라인

### Figure 3: Accuracy vs Model Size
![Size](image/accuracy_vs_size.png)
- 모델 크기별 성능

### Figure 4: Number of Agents
![Agents](image/accuracy_vs_num_agents.png)
- 에이전트 수별 성능

## Main Contributions
1. 계층적 오토마톤 설계
2. 학습 가능한 전이 메커니즘
3. MATA-SFT-90K 데이터셋
4. SOTA 성능 달성

## Key Findings
- 학습된 전이가 규칙 기반 우위
- 3개 에이전트가 최적 tradeoff
