# Reinforcement World Model Learning for LLM-based Agents

**Paper ID:** arXiv:2602.05842

## Authors
- Xiao Yu, Zhou Yu (Columbia University)
- Baolin Peng, Yelong Shen, Pengcheng He, Suman Nath, Jiangfeng Gao (Microsoft Research)
- Ruize Xu, Nikhil Singh (Dartmouth College)

---

## Abstract

We propose Reinforcement World Model Learning (RWML), a self-supervised method that learns action-conditioned world models for LLM-based agents to enhance their agentic capabilities. While most LLM-based agent methods rely on next-state token prediction, which prioritizes token-level fidelity, this approach fails to effectively capture the sim-to-real gap between simulated and realized environment states. RWML learns to align simulated next states with realized environment states in a pre-trained embedding space using sim-to-real gap rewards. Unlike LLM-as-a-judge, RWML provides more robust training signals and is less susceptible to reward hacking.

---

## Introduction

LLM-based agents have shown remarkable capabilities in understanding natural language and generating human-like responses. Recent advances have enabled these agents to interact with external tools and environments, transforming them into autonomous systems capable of completing complex tasks.

However, training effective LLM agents remains challenging. Existing approaches fall into several categories:

1. **Supervised Fine-tuning on Expert Data**: Requires expensive expert demonstrations
2. **Next-state Token Prediction**: Predicts next states but lacks deterministic fidelity
3. **LLM-as-a-judge**: Uses LLM as reward signal but vulnerable to reward hacking

The key challenge is that agents need to understand how their actions affect the environment - this is the "world model" problem. Without accurate world models, agents cannot effectively plan or learn from their experiences.

This paper introduces Reinforcement World Model Learning (RWML), a self-supervised approach that learns world models without requiring expert data. The key insight is to use pre-trained embeddings to measure sim-to-real gap, providing robust learning signals.

---

## Method

### RWML Key Idea
1. **Interaction Learning**: Collect (state, action, next state) triplets from environment rollouts
2. **World Model Learning**: Compare predicted vs actual next states in embedding space using cosine similarity
3. **Policy Learning**: Train agents using GRPO with embedding-based rewards

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

### Figure 3: Examples
![Examples](images/wmrl-traj_examples_cropped.png)

---

## Main Contributions

1. Self-supervised RWML method without expert data
2. Embedding-based rewards more robust than token prediction
3. State-of-the-art on ALFWorld and τ²Bench
