# Reinforcement World Model Learning for LLM-based Agents

**Paper ID:** arXiv:2602.05842

## Authors
- Xiao Yu, Zhou Yu (Columbia University)
- Baolin Peng, Yelong Shen, Pengcheng He, Suman Nath, Jiangfeng Gao (Microsoft Research)
- Ruize Xu, Nikhil Singh (Dartmouth College)

## Abstract
RWML (Reinforcement World Model Learning)을 제안합니다. 사전 훈련된 임베딩 공간에서 시뮬레이션된 다음 상태를 실제 환경 상태와 정렬하는 자기 감독 방법입니다. 작업 성공 보상과 결합 시 ALFWorld에서 6.9, τ²Bench에서 5.7 포인트 향상합니다.

## Method

### RWML 핵심 아이디어
1. 환경에서 롤아웃 수집
2. (상태, 행동, 다음 상태) 트리플릿 생성
3. 사전 훈련된 임베딩 공간에서 예측된 다음 상태와 실제 다음 상태 비교
4. cosine similarity 기반 보상으로 GRPO 훈련

## Results

### Table 1: ALFWorld Results

| Method | Success Rate (%) |
|--------|------------------|
| Base Model | 70.5 |
| + WM SFT | 85.2 |
| + RWML | 90.1 |
| + RWML + Policy RL | **90.1** |

### Table 2: τ²Bench Results

| Method | Score |
|--------|-------|
| Base Model | 80.0 |
| + WM SFT | 84.5 |
| + RWML | 87.9 |
| + RWML + Policy RL | **87.9** |

## Key Figures

### Figure 1: RWML Overview
![Cover](images/wmrl-cover_fig_cropped.png)
- RWML 개념도

### Figure 2: Main Algorithm
![Algo](images/wmrl-main_algo_cropped.png)
- RWML 알고리즘 파이프라인

### Figure 3: Trajectory Examples
![Examples](images/wmrl-traj_examples_cropped.png)
- 질적 예시 (ALFWorld, τ²Bench)

### Figure 4: Model Scaling
![Scaling](images/model_scaling.png)
- 모델 규모별 성능

## Main Contributions
1. 자기 감독 RWML 방법
2. 임베딩 기반 보상 (LLM-as-a-judge보다 Robust)
3. ALFWorld + τ²Bench에서 최첨단 성능
