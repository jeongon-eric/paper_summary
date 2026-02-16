# Reinforcement World Model Learning for LLM-based Agents

**Paper ID:** arXiv:2602.05842

## Authors
- Xiao Yu, Zhou Yu (Columbia University)
- Baolin Peng, Yelong Shen, Pengcheng He, Suman Nath, Jiangfeng Gao (Microsoft Research)
- Ruize Xu, Nikhil Singh (Dartmouth College)

---

## Abstract

We propose Reinforcement World Model Learning (RWML), a self-supervised method that learns action-conditioned world models for LLM-based agents to enhance their agentic capabilities. While most LLM-based agent methods rely on next-state token prediction, which prioritizes token-level fidelity, this approach fails to effectively capture the sim-to-real gap between simulated and realized environment states. RWML learns to align simulated next states with realized environment states in a pre-trained embedding space using sim-to-real gap rewards. Unlike LLM-as-a-judge, RWML provides more robust training signals and is less susceptible to reward hacking. Experiments on ALFWorld and τ²Bench show that RWML improves the base model by 19.6 and 7.9 points respectively. When combined with task-success rewards, RWML outperforms direct task-success RL by 6.9 points on ALFWorld and 5.7 points on τ²Bench.

---

## Method

### Problem Definition
LLM-based agents interact with environments using tools. Existing approaches have limitations:
1. **Next-state token prediction**: Predicts simulated next states but lacks deterministic token-level fidelity
2. **LLM-as-a-judge**: Uses LLM as judge but vulnerable to reward hacking

### RWML Key Idea
RWML consists of three stages:
1. **Interaction Learning**: Agents perform rollouts in environments and collect (state, action, next state) triplets
2. **World Model Learning**: Compare predicted next states with actual next states in pre-trained embedding space using cosine similarity
3. **Policy Learning**: Train agents using GRPO with the obtained rewards

---

## Datasets & Experiments

### ALFWorld
ALFWorld is a multi-modal evaluation framework operating in text-based environments. Includes six task types: Pick and place, Clean and place, Heat and place, Cool and place, Toggle switches, Scrub and free.

### τ²Bench
A more challenging benchmark for LLM-based agents with complex task scenarios requiring multi-step reasoning and various tool interactions.

### Experimental Setup
- **Base models**: Qwen2.5-7B, Qwen3-8B, Qwen3-30B-A3B
- **Comparison methods**: Base Model, WM SFT, RWML, RWML + Policy RL

---

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

### Key Findings
1. **RWML effectiveness**: Improves base model by 19.6 points on ALFWorld, 7.9 points on τ²Bench
2. **Catastrophic forgetting reduction**: RWML better preserves general knowledge than SFT
3. **Model scale effect**: Larger base models achieve greater improvements with RWML

---

## Key Figures

### Figure 1: RWML Overview
![Cover](images/wmrl-cover_fig_cropped.png)
- RWML concept: Interaction Learning → World Model Learning → Policy Learning

### Figure 2: Main Algorithm
![Algo](images/wmrl-main_algo_cropped.png)
- RWML algorithm pipeline

### Figure 3: Trajectory Examples
![Examples](images/wmrl-traj_examples_cropped.png)
- Qualitative examples: ALFWorld (left) and τ²Bench (right)

### Figure 4: Model Scaling
![Scaling](images/model_scaling.png)
- Performance by model size: Qwen2.5-7B, Qwen3-8B, Qwen3-30B-A3B

---

## Main Contributions

1. **Self-supervised RWML method** for effective world model learning without expert data
2. **Embedding-based rewards** more robust than token prediction and LLM-as-a-judge
3. **State-of-the-art on ALFWorld and τ²Bench**
4. **Reduced catastrophic forgetting** compared to SFT-based approaches

---

## Key Findings

- RL-based world model learning is more effective than SFT (token prediction)
- RWML maintains parameter landscape compatible with subsequent policy learning
- Larger base models achieve greater improvements with RWML
