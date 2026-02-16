# MATA: A Trainable Hierarchical Automaton System for Multi-Agent Visual Reasoning

**Paper ID:** arXiv:2601.19204 (ICLR 2026)

## Authors
- Zhixi Cai, Fucai Ke, Kevin Leo, Sukai Huang, Maria Garcia de la Banda, Peter J. Stuckey, Hamid Rezatofighi (Monash University)

---

## Abstract

We present MATA (Multi-Agent hierarchical Trainable Automaton), a novel multi-agent system for visual reasoning. While existing methods often follow rigid execution orders or have complex inter-agent communication protocols, providing only limited reasoning capabilities, MATA is presented as a hierarchical finite-state automaton. The top-level transitions are chosen by a trainable hyper agent, while each agent runs a rule-based sub-automaton for micro-control. The key innovation is that the hyper agent's state transition policy can be trained. We build MATA-SFT-90K, a dataset of 90,854 training examples. MATA achieves state-of-the-art results on GQA, OK-VQA, and Referring Expression Comprehension benchmarks, significantly outperforming previous methods.

---

## Method

### Hierarchical Automaton Structure

MATA consists of two-level hierarchical architecture:

1. **Hyper Automaton**: 
   - Trainable state transition policy
   - Each state represents a specific agent type
   - LLM-based controller selects next state

2. **Sub Automata**:
   - Rule-based micro-control
   - Defines fine-grained behaviors for each agent
   - Ensures efficient execution

### State Types
1. **INITIAL**: Initial state
2. **ONESHOT**: One-shot reasoning (for simple queries)
3. **STEPWISE**: Step-by-step reasoning (for complex multi-step tasks)
4. **SPECIALIZED**: Specialized agent (for specific domains)
5. **FINAL**: Final result derivation
6. **FAILURE**: Failure state

---

## Datasets & Experiments

### MATA-SFT-90K Dataset
90,854 training examples including:
- Various visual reasoning tasks
- Transition-trajectory tree format
- Explicit labels for state transitions

### Evaluation Benchmarks
1. **GQA**: Large-scale benchmark for visual reasoning
2. **OK-VQA**: Visual question answering requiring external knowledge
3. **Referring Expression Comprehension**: RefCOCO, RefCOCO+, RefCOCOg

---

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

### Key Findings
1. **+27% improvement on GQA** over ViperGPT
2. **Strong cross-domain generalization** with <1% performance degradation
3. **Effective even with small LLMs** when using domain-specific SFT
4. **3 agents optimal** with diminishing returns beyond

---

## Key Figures

### Figure 1: MATA Overview
![Teaser](image/teaser.png)
- Automaton structure: Linear pipeline vs Hierarchical automaton

### Figure 2: Pipeline
![Pipeline](image/pipeline.png)
- Training pipeline: Transition-trajectory → SFT

### Figure 3: Accuracy vs Model Size
![Size](image/accuracy_vs_size.png)
- Performance by model size: 0.6B ~ 8B

### Figure 4: Number of Agents
![Agents](image/accuracy_vs_num_agents.png)
- Performance by number of agents

---

## Main Contributions

1. **Hierarchical automaton design**: Combining neuro-symbolic framework with multi-agent design
2. **Trainable transition mechanism**: Data-driven decision making
3. **MATA-SFT-90K dataset**: 90,854 training examples
4. **State-of-the-art performance** on GQA, OK-VQA, Referring Expression

---

## Key Findings

- Learned transition policies outperform rule-based approaches
- 3 agents provide optimal tradeoff
- Strong cross-domain transfer (<1% difference)
- Small LLMs effective with domain-specific SFT
