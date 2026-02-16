# AgentDrive: An Open Benchmark Dataset for Agentic AI Reasoning with LLM-Generated Scenarios in Autonomous Systems

**Paper ID:** arXiv:2601.16964

## Authors
- Mohamed Amine Ferrag, Abderrahmane Lakas (United Arab Emirates University)
- Merouane Debbah (Khalifa University)

---

## Abstract

We introduce AgentDrive, an open benchmark dataset containing LLM-generated driving scenarios for autonomous driving agents. Current agentic AI reasoning evaluation suffers from limited scenarios and task complexity. AgentDrive contains 300,000 LLM-generated driving scenarios with a factorized scenario space across seven orthogonal axes. We also automate structured scenario generation using an LLM-driven prompt-to-JSON pipeline. The benchmark includes AgentDrive-MCQ with 100,000 reasoning questions spanning physics, policy, hybrid, scenario, and comparative reasoning. Evaluation of 50 leading LLMs shows that proprietary frontier models dominate in contextual/policy reasoning, while advanced open models are rapidly closing the gap in structured/physics reasoning.

---

## Method

### Factorized Scenario Space (7 Axes)

1. **Scenario Type**: Lane change, intersection, merging, turning, U-turn

2. **Driver Behavior**: Compliant, aggressive, distracted, impaired

3. **Environment**: Weather (clear, rain, snow, fog), visibility, time of day

4. **Road Layout**: Highway, urban, roundabout, tunnel, bridge

5. **Objective**: Safe navigation, overtaking, emergency stop, parking

6. **Difficulty**: Easy, moderate, complex

7. **Traffic Density**: Sparse, medium, congested

### LLM-based Scenario Generation
Prompt-to-JSON pipeline:
1. Define scenario templates
2. LLM generates parameters
3. Structure as JSON schema
4. Validate in simulation

---

## Datasets & Experiments

### AgentDrive-Gen
300,000 generated scenarios:
- Diverse situation combinations
- Structured JSON format
- Simulation compatible

### AgentDrive-Sim
Simulation dataset:
- Surrogate safety metrics
- Interpretable outcome labels
- safe_goal, safe_stop, inefficient, unsafe

### AgentDrive-MCQ
100,000 reasoning questions:
1. **Physics**: Vehicle dynamics physical reasoning
2. **Policy**: Traffic rule and policy understanding
3. **Hybrid**: Combined physics + policy reasoning
4. **Scenario**: Situational assessment
5. **Comparative**: Cross-scenario comparison

---

## Results

### Table 1: Benchmark Comparison

| Benchmark | Scenarios | Questions | Dimensions |
|-----------|-----------|-----------|------------|
| LaMPilot | 10K | 10K | 3 |
| V2V-LLM | 5K | 5K | 2 |
| STSBench | 15K | - | 1 |
| **AgentDrive** | **300K** | **100K** | **5** |

### Key Findings
1. **Proprietary model advantage**: Frontier models lead in contextual/policy reasoning
2. **Open model catch-up**: Rapid improvement in structured/physics reasoning
3. **First principled benchmark**: Combining generative synthesis with structured reasoning

---

## Key Figures

### Figure 1: AgentDrive Overview
![Overview](AgentDrive_MCQ.png)
- Benchmark components: Gen, Sim, MCQ

### Figure 2: Difficulty Heatmap
![Heatmap](fig_heatmap_layout_difficulty.png)
- Performance by difficulty

### Figure 3: Weather Distribution
![Weather](fig_weather_share.png)
- Scenario distribution by weather

---

## Main Contributions

1. **300K scenarios, 100K questions**: Largest driving agent benchmark
2. **7-axis factorization**: Comprehensive scenario space formalization
3. **LLM-based automatic generation**: Efficient scenario scaling
4. **50 LLM evaluation**: Comprehensive model comparison

---

## Key Findings

- Proprietary models lead in contextual/policy reasoning
- Open models catching up in physics reasoning
- Model performance varies by reasoning dimension
