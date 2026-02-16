# Learning Decentralized LLM Collaboration with Multi-Agent Actor Critic

**Paper ID:** arXiv:2601.21972

## Authors
- Shuo Liu, Tianle Chen, Ryan Amiri, Christopher Amato (Northeastern University)

---

## Abstract

Recent work has explored optimizing LLM collaboration through Multi-Agent Reinforcement Learning (MARL). However, most MARL fine-tuning approaches rely on predefined execution protocols, which often require centralized execution. Decentralized LLM collaboration is more appealing in practice, as agents can run inference in parallel with flexible deployments. Also, current approaches use Monte Carlo methods for fine-tuning, which suffer from high variance and thus require more samples to train effectively. Actor-critic methods are prevalent in MARL for dealing with these issues, so we developed Multi-Agent Actor-Critic (MAAC) methods to optimize decentralized LLM collaboration. In this paper, we analyze when and why these MAAC methods are beneficial. We propose 2 MAAC approaches: CoLLM-CC with a Centralized Critic and CoLLM-DC with Decentralized Critics. Our experiments across writing, coding, and game-playing domains show that Monte Carlo methods and CoLLM-DC can achieve performance comparable to CoLLM-CC in short-horizon and dense-reward settings. However, they both underperform CoLLM-CC on long-horizon or sparse-reward tasks, where Monte Carlo methods require substantially more samples and CoLLM-DC struggles to converge.

---

## Method

### MA-REINFORCE (Multi-Agent REINFORCE)
MA-REINFORCE is a class of multi-agent policy gradient methods where each agent maintains an individual policy πθi and updates it according to Monte-Carlo estimates of joint returns. However, this method does not scale well to long-horizon online learning because return signals are only available at dialog termination and Monte Carlo estimates suffer from high variance.

### Multi-Agent Actor-Critic (MAAC)
To reduce variance and improve sample efficiency, Actor-Critic methods learn a policy model (actor) πθ and a value model (critic) Vϕ. In the multi-agent setting, AC methods are used with Decentralized Critics (DC) or Centralized Critic (CC).

### CoLLM-CC (Centralized Critic)
CoLLM-CC learns a shared value function Vϕ(ht) that conditions on the joint history ht to update each agent's policy. Since the critic is just a training construct, it can be removed during execution, allowing agents to execute in a decentralized manner.

### CoLLM-DC (Decentralized Critic)
CoLLM-DC uses individual critics Vϕi(hi,t) that condition on each agent's local history. This may be harder to converge due to non-stationarity accumulating during training.

---

## Datasets & Experiments

### TLDR Summarization
Two Qwen3-1.7B agents summarize Reddit posts. One acts as a high-level summarizer producing a concise paragraph, and one serves as a detailed summarizer. Quality is evaluated using weighted sum of structure, style consistency, and logical coherence metrics.

### arXiv Expansion
Same agents expand paper abstracts into full introductions. One outlines research background and motivation, the other presents proposed methods and experiments.

### CoopHE (Cooperative Code Generation)
The CoopHumanEval dataset focuses on problems that naturally admit cooperative decomposition. An auxiliary agent implements lightweight utilities supporting the primary agent to produce core logic.

### StrBuild (Minecraft String Building)
Agents collaboratively build structures matching exact strings while maintaining even material distribution. IoU is used as evaluation metric.

### HouseBuild (Minecraft House Building)
Agents collaboratively construct houses conforming to architectural specifications while defending against hostile mobs. Average health points indicate successful defense.

---

## Results

### Table 1: Overall Performance

| Method | TLDR Score | arXiv Score | StrBuild IoU | HouseBuild IoU |
|--------|------------|-------------|--------------|----------------|
| Raw Model | 30.3 | 44.0 | 36.6 | 43.2 |
| GRPO | 91.7 | 91.0 | 46.1 | 54.6 |
| CoLLM-CC | **95.2** | **95.0** | **68.5** | **52.7** |

### Key Findings
1. In short-horizon writing tasks, all methods achieve similar performance
2. In long-horizon Minecraft tasks, CoLLM-CC significantly outperforms others
3. Monte Carlo methods require substantially more samples
4. CoLLM-DC fails to converge in long-horizon settings due to non-stationarity

---

## Key Figures

### Figure 1: CoLLM-CC Framework
![Framework](figs/framework.png)
- (a) Agent model structure with Transformer blocks and KV-Cache
- (b) Overall centralized-critic architecture
- (c) Critic model structure

### Figure 2: CoLLM-DC Framework
![Framework-DC](figs/framework-dc.png)
- Decentralized critic architecture: each agent has individual critic

### Figure 3: TLDR Results
![TLDR](figs/writing_tldr.png)
- Learning curves on TLDR summarization task

### Figure 4: arXiv Results
![arXiv](figs/writing_arxiv.png)
- Learning curves on arXiv expansion task

### Figure 5: Code Generation
![CodeGen](figs/codegen_coophe.png)
- Results on CoopHE code generation task

### Figure 6: Minecraft StrBuild
![Minecraft](figs/minecraft_str.png)
- Example of ICML-shaped building task

### Figure 7: Minecraft HouseBuild
![HouseBuild](figs/minecraft_box.png)
- Example of house construction with enemy defense

---

## Main Contributions

1. **Developed MAAC methods for decentralized LLM collaboration** and analyzed their advantages
2. **Proposed two approaches**: CoLLM-CC with centralized critic and CoLLM-DC with decentralized critics
3. **Comprehensive evaluation** across writing, coding, and game-playing domains
4. **Demonstrated CoLLM-CC's superiority** in long-horizon and sparse-reward tasks

---

## Key Findings

- CoLLM-CC achieves lowest variance and best sample efficiency
- Monte Carlo methods require substantially more samples in long-horizon tasks
- CoLLM-DC struggles to converge due to non-stationarity
- Centralized critic provides more stable gradient estimates than decentralized
