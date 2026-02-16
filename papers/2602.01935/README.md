# COLT: Lightweight Multi-LLM Collaboration through Shared MCTS Reasoning for Model Compilation

**Paper ID:** arXiv:2602.01935

## Authors
- Albert Shyuan Tang, Carey Priebe, Qin (Luna) Lu, Hadi Esmaeilzadeh (Johns Hopkins University)

---

## Abstract

We propose COLT (Collaborative Optimization via Lightweight Threads), a lightweight multi-LLM collaboration framework for compiler optimization. While recent LLMs have proven effective for code generation and transformation, a single LLM struggles to make complex optimization decisions. COLT implements multi-LLM collaboration through Monte Carlo Tree Search (MCTS) reasoning sharing. The key innovation is that the current model generates a reasoning tree which collaborating models use to select arms. Information communication is performed through shared KV cache, reducing communication overhead. Compared to LLMCompiler, COLT achieves 53% latency reduction and 87% cost reduction while achieving equal or better performance.

---

## Method

### COLT Architecture

1. **Reasoning Tree Generation**:
   - Current model (Master) generates reasoning tree
   - Each node represents an optimization decision
   - Leaf nodes represent final decisions

2. **Arm Selection (Collaborating Models)**:
   - Collaborating models use reasoning tree
   - Select optimal branches
   - Support Master model decisions

3. **Shared KV Cache**:
   - KV cache sharing between models
   - Significantly reduces communication overhead
   - Efficient information delivery

### MCTS-based Collaboration

MCTS components:
- **Selection**: Select promising nodes
- **Expansion**: Add new nodes
- **Simulation**: Simulate outcomes
- **Backpropagation**: Backpropagate values

In COLT:
- Master model performs MCTS reasoning
- Collaborating models select arms based on reasoning tree
- Shared KV cache for efficient communication

---

## Datasets & Experiments

### Evaluation Benchmarks
1. **SPEC CPU 2017**: Industry standard benchmark
2. **LLVM Test Suite**: Compiler test cases
3. **Custom Micro-benchmarks**: Specific optimization types

### Optimization Targets
- Execution speed: Runtime performance improvement
- Code size: Binary size reduction
- Memory usage: Memory optimization

---

## Results

### Table 1: Overall Performance

| Method | Latency Reduction | Cost Reduction | Quality |
|--------|------------------|---------------|---------|
| GCC -O3 | baseline | baseline | baseline |
| LLVM -O3 | +2.1% | baseline | +2.1% |
| LLMCompiler | -45% | -65% | +8.5% |
| **COLT** | **-53%** | **-87%** | **+9.2%** |

### Key Findings
1. **53% latency reduction** over LLMCompiler
2. **87% cost reduction** while maintaining quality
3. **Quality improvement**: +9.2% performance boost
4. **Heterogeneous configurations best**: Diverse model combinations outperform single models

---

## Key Figures

### Figure 1: COLT Overview
![Overview](figs/overview.png)
- MCTS-based collaboration mechanism

### Figure 2: GPT-5.2 Results
![GPT5](figs/colt-gpt5.2-combined.png)
- GPT-5.2 evaluation results

### Figure 3: Llama 70B Results
![Llama](figs/colt-llama70-combined.png)
- Llama 3 70B evaluation results

---

## Main Contributions

1. **MCTS-based lightweight multi-LLM collaboration**: Novel collaboration mechanism
2. **Shared KV cache**: Significantly reduces communication overhead
3. **Practical compiler optimization application**: Demonstrates practical applicability
4. **Both latency and cost improvement**: Significant improvement over existing methods

---

## Key Findings

- MCTS reasoning sharing achieves effective collaboration
- Shared KV cache reduces communication overhead
- Significant improvements in both latency and cost
