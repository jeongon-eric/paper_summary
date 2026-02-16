# M3-BENCH: Process-Aware Evaluation of LLM Agents Social Behaviors

**Paper ID:** arXiv:2601.08462

## Authors
- Siyuan Xie, Ziming Shi, Haibo Shen, Guoyu Huang, Yuxin Ma, Xinyu Jing (Zhejiang University)

---

## Abstract

We introduce M3-BENCH, a benchmark for process-aware evaluation of LLM agents' social behaviors in mixed-motive games. While existing evaluations focus on outcome-based assessment where agents are only evaluated on final results, this approach fails to capture agents' decision-making processes and social behaviors. M3-BENCH analyzes agents through three evaluation modules: (1) Behavioral Trend Analysis (BTA), (2) Reasoning Process Analysis (RPA), and (3) Communication Content Analysis (CCA). We evaluate agents across three opponent types (cooperative, competitive, mixed) and two communication conditions. Experimental results reveal misalignment between behavior, reasoning, and communication, suggesting agents may select behaviors without understanding why.

---

## Introduction

Understanding social behaviors in AI agents is crucial for real-world deployment. Existing evaluations focus on outcomes, not processes - we know WHAT agents do, but not WHY or HOW they decide.

This limits our ability to: build trustworthy AI systems, understand agent decision-making, and ensure reliable social behaviors.

M3-BENCH addresses this with three modules: BTA to track what behaviors emerge over time, RPA to analyze what reasoning leads to those behaviors, and CCA to understand how agents communicate. This reveals internal consistency and helps build more reliable social AI.

---

## Method

### Three Evaluation Modules
1. **BTA**: Behavioral Trend Analysis
2. **RPA**: Reasoning Process Analysis
3. **CCA**: Communication Content Analysis

---

## Results

### Table 1: Results by Opponent Type

| Opponent | Success Rate |
|----------|-------------|
| Cooperative | 85% |
| Competitive | 45% |

---

## Key Figures

### Figure 1: Framework
![Framework](figures/jiagou.png)

---

## Main Contributions

1. Process-aware evaluation framework
2. Three-module analysis (BTA, RPA, CCA)
3. Behavior-reasoning-communication alignment study
4. Insights into multi-agent social behaviors
