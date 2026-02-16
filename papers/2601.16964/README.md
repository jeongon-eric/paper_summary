# AgentDrive: An Open Benchmark Dataset for Agentic AI Reasoning

**Paper ID:** arXiv:2601.16964

## Authors
- Mohamed Amine Ferrag, Abderrahmane Lakas (United Arab Emirates University)
- Merouane Debbah (Khalifa University)

---

## Abstract

We introduce AgentDrive, an open benchmark dataset containing LLM-generated driving scenarios for autonomous driving agents. Current agentic AI reasoning evaluation suffers from limited scenarios and task complexity. AgentDrive contains 300,000 LLM-generated driving scenarios with a factorized scenario space across seven orthogonal axes. We also automate structured scenario generation using an LLM-driven prompt-to-JSON pipeline. The benchmark includes AgentDrive-MCQ with 100,000 reasoning questions spanning physics, policy, hybrid, scenario, and comparative reasoning. Evaluation of 50 leading LLMs shows that proprietary frontier models dominate in contextual/policy reasoning, while advanced open models are rapidly closing the gap in structured/physics reasoning.

---

## Introduction

Autonomous driving requires sophisticated reasoning about physics, traffic rules, and complex scenarios. However, existing benchmarks fail to capture the full complexity needed for agentic AI evaluation.

Current limitations include: limited scenarios with small benchmark sizes, lack of reasoning diversity focusing mainly on perception, and no factorized analysis to isolate specific reasoning capabilities.

AgentDrive addresses these by providing: 300,000 diverse driving scenarios, 7 orthogonal axes for systematic analysis, and 100,000 MCQ questions testing different reasoning types including physics, policy, hybrid, scenario, and comparative reasoning.

---

## Method

### 7 Axes of Factorization
1. Scenario Type (lane change, intersection, merging)
2. Driver Behavior (compliant, aggressive, distracted)
3. Environment (weather, visibility, time of day)
4. Road Layout (highway, urban, roundabout)
5. Objective (navigation, overtaking, parking)
6. Difficulty (easy, moderate, complex)
7. Traffic Density (sparse, medium, congested)

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

### Figure 2: Difficulty Heatmap
![Heatmap](fig_heatmap_layout_difficulty.png)

---

## Main Contributions

1. Largest driving agent benchmark with 300K scenarios and 100K questions
2. 7-axis factorization for comprehensive scenario space
3. LLM-based automatic generation for efficient scaling
4. Evaluation of 50 leading LLMs
