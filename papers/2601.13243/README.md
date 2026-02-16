# A Comprehensive Evaluation of LLM Reasoning: From Single-Model to Multi-Agent Paradigms

**Paper ID:** arXiv:2601.13243

## Authors
- Yapeng Li, Jiakuo Yu, Zhixin Liu, Xinnan Liu, Jing Yu, Songze Li, Tonghua Su (Harbin Institute of Technology)

---

## Abstract

We conduct a comprehensive evaluation of reasoning paradigms spanning direct single-model generation, Chain-of-Thought (CoT) augmented reasoning, and Multi-Agent Systems (MAS). While existing studies often evaluate single reasoning modalities or compare only specific MAS workflows, we analyze these in a unified manner and introduce MIMeBench, a new benchmark targeting semantic abstraction and contrastive discrimination. Our findings reveal that increased structural complexity does not consistently improve reasoning performance, with benefits highly dependent on paradigm properties and task suitability. We also show that CoT is not always beneficial, and MAS workflows can be effective or ineffective depending on task types.

---

## Method

### Reasoning Paradigm Types

1. **Direct Generation (DG)**:
   - LLM directly generates answers
   - Simplest form
   - Limited for complex reasoning tasks

2. **Chain-of-Thought (CoT)**:
   - Explicit step-by-step reasoning
   - Self-regressive reasoning
   - Effective for math and logical reasoning

3. **Plan-and-Execute (PE)**:
   - Planner: Task planning
   - Executor: Execute plan
   - Reviser: Review results
   - Suitable for multi-step tasks

4. **Reflection (Ref)**:
   - Agent reviews its own reasoning
   - Self-correction ability
   - Effective for error correction

5. **Debate (Deb)**:
   - Multiple agents interact
   - Aggregator or Judge makes final decision
   - Effective for complex judgments

---

## Datasets & Experiments

### Closed-form Benchmarks

1. **Mathematical Reasoning**:
   - AQUA, GSM8K, GSM-Hard, AIME-2024

2. **General Understanding**:
   - ARC-Easy, ARC-Challenge
   - CommonsenseQA, GPQA-Diamond

3. **Code Generation**:
   - HumanEval, HumanEval+

### MIMeBench (New Benchmark)
Main-idea multiple choice question generation:
- Tests semantic abstraction ability
- Tests contrastive discrimination
- 100 samples with dynamic evaluation criteria

---

## Results

### Table 1: Benchmark Selection

| Category | Benchmarks | Metric |
|----------|------------|--------|
| Math | AQUA, GSM8K, AIME-2024 | Accuracy |
| Understanding | ARC, CommonsenseQA, GPQA-Diamond | Accuracy |
| Code | HumanEval, HumanEval+ | Pass@1 |
| Open-ended | MIMeBench | Avg Score |

### Key Findings
1. **Structural complexity limitation**: Additional complexity does not always lead to performance improvement
2. **CoT task dependency**: Effective for math but limited effect for code
3. **MAS workflow diversity**: Different workflows optimal for different task types
4. **Cost-accuracy tradeoff**: More complex methods incur higher costs

---

## Key Figures

### Figure 1: Study Overview
![Overview](images/Overview.png)
- Evaluation framework overview

### Figure 2: MAS Workflows
![Workflow](images/mas-workflow.png)
- MAS workflow types

---

## Main Contributions

1. **Comprehensive paradigm evaluation**: Unified evaluation of direct generation, CoT, and MAS
2. **MIMeBench benchmark**: Semantic abstraction and contrastive discrimination testing
3. **Role-specific analysis**: Capability demands analysis in MAS
4. **Cost-accuracy tradeoff analysis**: Fine-grained cost-performance analysis

---

## Key Findings

- Structural complexity does not consistently improve reasoning
- CoT is task-dependent: effective for some, not for others
- MAS workflows show task-dependent effectiveness
- Open-ended evaluation reveals capabilities not captured by closed-form benchmarks
