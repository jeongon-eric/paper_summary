# COLT: Lightweight Multi-LLM Collaboration through Shared MCTS Reasoning

**Paper ID:** arXiv:2602.01935

## Authors
- Albert Shyuan Tang, Carey Priebe, Qin (Luna) Lu, Hadi Esmaeilzadeh (Johns Hopkins University)

---

## Abstract

We propose COLT, a lightweight multi-LLM collaboration framework using MCTS reasoning sharing. COLT achieves 53% latency reduction and 87% cost reduction over LLMCompiler while maintaining quality.

---

## Introduction

Compiler optimization is complex and traditionally relies on expert-designed heuristics. Recent LLMs can help but single models struggle with complex optimization decisions.

Key challenges:
1. **Single model limitations**: Cannot handle all optimization types
2. **Communication overhead**: Multi-agent approaches often expensive
3. **Reasoning complexity**: Optimization requires deep reasoning

COLT addresses these by:
- Sharing reasoning trees between models
- Using MCTS for structured exploration
- Leveraging complementary model strengths

---

## Method

### MCTS-based collaboration with shared KV cache

---

## Results

### Table 1: Performance

| Method | Latency | Cost |
|--------|---------|------|
| LLMCompiler | baseline | baseline |
| COLT | **-53%** | **-87%** |

---

## Key Figures

### Figure 1: Overview
![Overview](figs/overview.png)

---

## Main Contributions

1. MCTS-based collaboration
2. Shared KV cache efficiency
3. Both latency and cost improvement
