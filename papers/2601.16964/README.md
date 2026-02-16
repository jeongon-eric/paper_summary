# AgentDrive: An Open Benchmark Dataset for Agentic AI Reasoning

**Paper ID:** arXiv:2601.16964

## Authors
- Mohamed Amine Ferrag, Abderrahmane Lakas (United Arab Emirates University)
- Merouane Debbah (Khalifa University)

---

## Abstract

We introduce AgentDrive, an open benchmark with 300,000 LLM-generated driving scenarios across 7 orthogonal axes. The benchmark includes AgentDrive-MCQ with 100,000 reasoning questions spanning physics, policy, hybrid, scenario, and comparative reasoning. Evaluation of 50 LLMs shows proprietary models lead in contextual reasoning while open models catch up in physics reasoning.

---

## Introduction

Autonomous driving requires sophisticated reasoning about physics, traffic rules, and complex scenarios. However, existing benchmarks fail to capture the full complexity needed for agentic AI evaluation.

Current limitations:
1. **Limited scenarios**: Most benchmarks have small numbers of scenarios
2. **Lack of reasoning diversity**: Focus mainly on perception
3. **No factorized analysis**: Cannot isolate specific reasoning capabilities

AgentDrive addresses these by providing:
- 300,000 diverse driving scenarios
- 7 orthogonal axes for systematic analysis
- 100,000 MCQ questions testing different reasoning types

This enables comprehensive evaluation of how AI systems reason about driving situations.

---

## Method

### 7 Axes: Scenario Type, Driver Behavior, Environment, Road Layout, Objective, Difficulty, Traffic Density

---

## Results

### Table 1: Benchmark Comparison

| Benchmark | Scenarios | Questions |
|-----------|-----------|-----------|
| AgentDrive | **300K** | **100K** |

---

## Key Figures

### Figure 1: AgentDrive Overview
![Overview](AgentDrive_MCQ.png)

---

## Main Contributions

1. 300K scenarios, 100K questions
2. 7-axis factorization
3. 50 LLM evaluation
