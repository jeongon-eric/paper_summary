# A Comprehensive Evaluation of LLM Reasoning: From Single-Model to Multi-Agent Paradigms

**Paper ID:** arXiv:2601.13243

## Authors
- Yapeng Li, Jiakuo Yu, Zhixin Liu, Xinnan Liu, Jing Yu, Songze Li, Tonghua Su (Harbin Institute of Technology)

---

## Abstract

We conduct a comprehensive evaluation of reasoning paradigms spanning direct single-model generation, Chain-of-Thought (CoT) augmented reasoning, and Multi-Agent Systems (MAS). While existing studies often evaluate single reasoning modalities or compare only specific MAS workflows, we analyze these in a unified manner and introduce MIMeBench, a new benchmark targeting semantic abstraction and contrastive discrimination. Our findings reveal that increased structural complexity does not consistently improve reasoning performance, with benefits highly dependent on paradigm properties and task suitability. We also show that CoT is not always beneficial, and MAS workflows can be effective or ineffective depending on task types.

---

## Introduction

LLM reasoning has evolved through multiple paradigms: Direct Generation for simple input-output mapping, Chain-of-Thought for step-by-step reasoning, and Multi-Agent Systems for collaborative reasoning.

However, we lack understanding of when each paradigm works best, how paradigm choice affects performance, and cost-benefit tradeoffs between approaches.

This paper provides systematic comparison across paradigms to understand which paradigm suits which task, when additional complexity is worthwhile, and optimal configurations for different scenarios.

---

## Method

### Paradigms Evaluated
1. **Direct Generation**: Simple input-output
2. **Chain-of-Thought**: Step-by-step reasoning
3. **Plan-and-Execute**: Planning then execution
4. **Reflection**: Self-correction
5. **Debate**: Multi-agent discussion

---

## Results

### Table 1: Benchmark Selection

| Category | Benchmarks |
|----------|------------|
| Math | AQUA, GSM8K, AIME-2024 |
| Understanding | ARC, CommonsenseQA |
| Code | HumanEval |

---

## Key Figures

### Figure 1: Overview
![Overview](images/Overview.png)

---

## Main Contributions

1. Comprehensive unified evaluation of reasoning paradigms
2. MIMeBench for semantic abstraction testing
3. Cost-accuracy tradeoff analysis
4. Guidelines for paradigm selection
