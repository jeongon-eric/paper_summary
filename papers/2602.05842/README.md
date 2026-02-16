# Reinforcement World Model Learning for LLM-based Agents

**Paper ID:** arXiv:2602.05842

## Authors
- Xiao Yu, Zhou Yu (Columbia University)
- Baolin Peng, Yelong Shen, Pengcheng He, Suman Nath, Jiangfeng Gao (Microsoft Research)
- Ruize Xu, Nikhil Singh (Dartmouth College)

---

## Abstract

We propose Reinforcement World Model Learning (RWML), a self-supervised method that learns action-conditioned world models for LLM-based agents to enhance their agentic capabilities. While most LLM-based agent methods rely on next-state token prediction, which prioritizes token-level fidelity, this approach fails to effectively capture the sim-to-real gap between simulated and realized environment states. RWML learns to align simulated next states with realized environment states in a pre-trained embedding space using sim-to-real gap rewards. Unlike LLM-as-a-judge, RWML provides more robust training signals and is less susceptible to reward hacking. Experiments on ALFWorld and τ²Bench show that RWML improves the base model by 19.6 and 7.9 points respectively. When combined with task-success rewards, RWML outperforms direct task-success RL by 6.9 points on ALFWorld and 5.7 points on τ²Bench.

우리는 LLM 기반 에이전트의 에이전틱 능력을 향상시키기 위해 작업 조건(world model)을 학습하는 자기 감독 방법인 Reinforcement World Model Learning (RWML)을 제안합니다. 대부분의 LLM 기반 에이전트 방법은 토큰 수준의 충실도를 우선시하는 다음 상태 토큰 예측에 의존하지만, 이 접근법은 시뮬레이션된 환경 상태와 실현된 환경 상태 사이의sim-to-real gap을 효과적으로 포착하지 못합니다. RWML은 sim-to-real gap 보상을 사용하여 사전 훈련된 임베딩 공간에서 시뮬레이션된 다음 상태를 실현된 환경 상태와 정렬하도록 학습합니다. LLM-as-a-judge와 달리, RWML은 더 강력한 학습 신호를 제공하며 reward hacking에 덜 취약합니다. ALFWorld와 τ²Bench에서의 실험은 RWML이 기본 모델을 각각 19.6과 7.9 포인트 향상시킵니다. 작업 성공 보상과 결합될 때, RWML은 ALFWorld에서 직접 작업 성공 RL보다 6.9 포인트, τ²Bench에서 5.7 포인트 더 좋습니다.

---

## Introduction

LLM-based agents have shown remarkable capabilities in understanding natural language and generating human-like responses. Recent advances have enabled these agents to interact with external tools and environments, transforming them into autonomous systems capable of completing complex tasks.

LLM 기반 에이전트는 자연어를 이해하고 인간과 유사한 응답을 생성하는remarkable한 역량을 보여왔습니다. 최근 진전은 이러한 에이전트가 외부 도구 및 환경과 상호작용하여 복잡한 작업을 완료할 수 있는 자율 시스템으로 변환할 수 있게 했습니다.

However, training effective LLM agents remains challenging. Existing approaches fall into several categories: supervised fine-tuning on expert data, next-state token prediction, and LLM-as-a-judge. Each approach has limitations - expert data is expensive, token prediction lacks deterministic fidelity, and LLM-as-a-judge is vulnerable to reward hacking.

그러나 효과적인 LLM 에이전트 훈련은 여전히 도전적입니다. 기존 접근법은 여러 범주, 즉 전문가 데이터에 대한 감독 파인 튜닝, 다음 상태 토큰 예측, LLM-as-a-judge로 나뉩니다. 각 접근법에는 한계가 있습니다 - 전문가 데이터는 비싸고, 토큰 예측은 결정론적 충실도가 없으며, LLM-as-a-judge는 reward hacking에 취약합니다.

The key challenge is that agents need to understand how their actions affect the environment - this is the "world model" problem. Without accurate world models, agents cannot effectively plan or learn from their experiences.

도전의 핵심은 에이전트가 자신의 행동이 환경에 어떤 영향을 미치는지 이해해야 한다는 것입니다 - 이것이 "world model" 문제입니다. 정확한 world model이 없으면 에이전트는 효과적으로 계획하거나 경험에서 학습할 수 없습니다.

This paper introduces Reinforcement World Model Learning (RWML), a self-supervised approach that learns world models without requiring expert data. The key insight is to use pre-trained embeddings to measure sim-to-real gap, providing robust learning signals that are less susceptible to reward hacking compared to LLM-as-a-judge.

이 논문은 전문가 데이터 없이 world model을 학습하는 자기 감독 접근법인 Reinforcement World Model Learning (RWML)을 소개합니다. 핵심 통찰력은 사전 훈련된 임베딩을 사용하여 sim-to-real gap을 측정하여 LLM-as-a-judge보다 reward hacking에 덜 취약한 강력한 학습 신호를 제공하는 것입니다.

---

## Method

### RWML Framework
1. **Interaction Learning**: Collect (state, action, next state) triplets from environment rollouts
2. **World Model Learning**: Compare predicted vs actual next states in embedding space using cosine similarity
3. **Policy Learning**: Train agents using GRPO with embedding-based rewards

RWML 프레임워크:
1. **상호작용 학습**: 환경 롤아웃에서 (상태, 행동, 다음 상태) 트리플릿 수집
2. **World Model Learning**: 코사인 유사도를 사용하여 임베딩 공간에서 예측된 다음 상태와 실제 다음 상태 비교
3. **정책 학습**: 임베딩 기반 보상으로 GRPO를 사용하여 에이전트 훈련

---

## Results

### Table 1: ALFWorld Results

| Method | Success Rate (%) |
|--------|------------------|
| Base Model | 70.5 |
| + RWML | 90.1 |

### Table 2: τ²Bench Results

| Method | Score |
|--------|-------|
| Base Model | 80.0 |
| + RWML | 87.9 |

---

## Key Figures

### Figure 1: RWML Overview
![Cover](images/wmrl-cover_fig_cropped.png)

### Figure 2: Algorithm
![Algo](images/wmrl-main_algo_cropped.png)

---

## Main Contributions

1. Self-supervised RWML method without expert data
2. Embedding-based rewards more robust than token prediction
3. State-of-the-art on ALFWorld and τ²Bench
4. Less catastrophic forgetting than SFT-based approaches

주요 기여:
1. 전문가 데이터 없이 자기 감독 RWML 방법
2. 토큰 예측보다 더 강력한 임베딩 기반 보상
3. ALFWorld와 τ²Bench에서의 최첨단 성능
4. SFT 기반 접근법보다 더 적은灾难적 망각
