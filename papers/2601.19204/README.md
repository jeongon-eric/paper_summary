# MATA: A Trainable Hierarchical Automaton System for Multi-Agent Visual Reasoning

**Paper ID:** arXiv:2601.19204 (ICLR 2026)

## Authors
- Zhixi Cai, Fucai Ke, Kevin Leo, Sukai Huang, Maria Garcia de la Banda, Peter J. Stuckey, Hamid Rezatofighi (Monash University)

---

## Abstract

We present MATA (Multi-Agent hierarchical Trainable Automaton), a novel multi-agent system for visual reasoning. While existing methods often follow rigid execution orders or have complex inter-agent communication protocols, providing only limited reasoning capabilities, MATA is presented as a hierarchical finite-state automaton. The top-level transitions are chosen by a trainable hyper agent, while each agent runs a rule-based sub-automaton for micro-control. The key innovation is that the hyper agent's state transition policy can be trained. We build MATA-SFT-90K, a dataset of 90,854 training examples. MATA achieves state-of-the-art results on GQA, OK-VQA, and Referring Expression Comprehension benchmarks, significantly outperforming previous methods.

---

## Introduction

Visual reasoning remains a challenging task for AI systems, requiring understanding of complex scenes, spatial relationships, and contextual information. While LLMs have shown impressive reasoning capabilities, applying them to visual tasks introduces unique challenges.

Existing approaches include monolithic VLMs, compositional methods, and multi-agent systems. However, these approaches often suffer from rigid execution orders, complex communication protocols, and limited reasoning capabilities.

MATA addresses these issues by introducing a hierarchical automaton where: a hyper agent decides which specialized agent to use, each sub-agent handles specific reasoning tasks, and the system can be trained to optimize transition decisions. This allows the system to learn when to use which type of reasoning, rather than relying on fixed rules.

---

## Method

### Hierarchical Automaton
1. **Hyper Automaton**: Trainable state transition policy (which agent to use)
2. **Sub Automata**: Rule-based micro-control (how each agent behaves)

### States: INITIAL, ONESHOT, STEPWISE, SPECIALIZED, FINAL, FAILURE

---

## Results

### Table 1: GQA Performance

| Method | Accuracy (%) |
|--------|--------------|
| ViperGPT | 37.9 |
| MATA | **64.9** |

### Table 2: OK-VQA Performance

| Method | Accuracy (%) |
|--------|--------------|
| GPT-4o | 75.7 |
| MATA | **76.5** |

---

## Key Figures

### Figure 1: MATA Overview
![Teaser](image/teaser.png)

### Figure 2: Pipeline
![Pipeline](image/pipeline.png)

---

## Main Contributions

1. Hierarchical automaton design combining neuro-symbolic and multi-agent approaches
2. Trainable transition mechanism replacing hand-written rules
3. MATA-SFT-90K dataset with 90,854 training examples
4. State-of-the-art on GQA, OK-VQA, RefCOCO
