# Inferring Latent Intentions: Attributional Natural Language Inference in LLM Agents

**Paper ID:** arXiv:2601.08742

## Authors
- Xin Quan, Jiafeng Xiong (University of Manchester)
- Marco Valentino (University of Sheffield)
- André Freitas (University of Manchester, Idiap Research Institute, CRUK-MI)

---

## Abstract

We introduce Attributional NLI (Att-NLI), a framework that extends traditional NLI with principles from social psychology to assess agents' capacity for abductive intentional inference. Att-NLI consists of two stages: (1) Abduction - inferring latent intentions from observations, and (2) Deduction - deriving logical conclusions from intentions. We evaluate through Undercover-V game and show Neuro-Symbolic Att-NLI achieves 78.29% improvement over Standard NLI.

---

## Introduction

Understanding intentional behavior is crucial for AI systems that interact with humans. Traditional Natural Language Inference (NLI) focuses on entailment, contradiction, and neutral relationships between premise and hypothesis. However, this approach fails to capture the deeper reasoning about WHY someone made a particular claim.

The key question is: Can AI agents infer the latent intentions behind observed actions? This is essential for:
- Trust in AI systems
- Explainable AI
- Multi-agent collaboration
- Social reasoning

We propose Attributional NLI (Att-NLI), which extends NLI with social psychology principles:
1. **Abductive Reasoning**: From observations to possible intentions
2. **Deductive Reasoning**: From intentions to predicted actions

This framework enables agents to not just understand WHAT happened, but WHY it happened - essential for social AI.

---

## Method

### Three Agent Types

1. **Standard NLI Agent**: Deduction only
2. **Standard Att-NLI Agent**: Abduction → Deduction
3. **Neuro-Symbolic Att-NLI**: + Isabelle/HOL theorem prover

---

## Results

### Table 1: Main Results

| Agent Type | Spy Win Rate | Improvement |
|------------|--------------|-------------|
| Standard NLI | 9.58% | baseline |
| Neuro-Symbolic Att-NLI | **17.08%** | **+78.3%** |

---

## Key Figures

### Figure 1: Att-NLI Process
![Intro](figures/att-nli.intro.png)

### Figure 2: Spy Performance
![Spy](figures/gpt_4o_spy_performance_word_similarity.png)

---

## Main Contributions

1. Attributional NLI framework for intention inference
2. Undercover-V verifiable game
3. Demonstrated effectiveness of neuro-symbolic integration
