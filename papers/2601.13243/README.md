# A Comprehensive Evaluation of LLM Reasoning: From Single-Model to Multi-Agent Paradigms

**Paper ID:** arXiv:2601.13243

## Authors
- Yapeng Li, Jiakuo Yu, Zhixin Liu, Xinnan Liu, Jing Yu, Songze Li, Tonghua Su (Harbin Institute of Technology)

---

## Abstract

We conduct a comprehensive evaluation of reasoning paradigms spanning direct single-model generation, Chain-of-Thought (CoT), and Multi-Agent Systems (MAS). We introduce MIMeBench for semantic abstraction and contrastive discrimination. Our findings reveal that increased structural complexity does not consistently improve reasoning, with benefits dependent on task suitability.

---

## Introduction

LLM reasoning has evolved through multiple paradigms:
1. **Direct Generation**: Simple input-output mapping
2. **Chain-of-Thought**: Step-by-step reasoning
3. **Multi-Agent Systems**: Collaborative reasoning

However, we lack understanding of:
- When each paradigm works best
- How paradigm choice affects performance
- Cost-benefit tradeoffs between approaches

This paper provides systematic comparison across paradigms to understand:
- Which paradigm suits which task
- When additional complexity is worthwhile
- Optimal configurations for different scenarios

---

## Method

### Paradigms: Direct, CoT, Plan-and-Execute, Reflection, Debate

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

1. Comprehensive paradigm evaluation
2. MIMeBench benchmark
3. Cost-accuracy tradeoff analysis
