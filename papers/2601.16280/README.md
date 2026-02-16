# When Agents Fail to Act: A Diagnostic Framework for Tool Invocation Reliability in Multi-Agent LLM Systems

**Paper ID:** arXiv:2601.16280

## Authors
- Donghao Huang (Singapore Management University / Mastercard)
- Gauri Malwe (Mastercard)
- Zhaoxia Wang (Singapore Management University)

---

## Abstract

We propose a comprehensive diagnostic framework for evaluating tool invocation reliability in multi-agent LLM systems. While recent LLM-based agents have demonstrated remarkable capabilities in accomplishing complex tasks using tools, systematic evaluation of procedural reliability in such multi-agent systems remains lacking. We introduce a 12-category error taxonomy capturing failure modes across tool initialization, parameter handling, execution, and result interpretation. Through systematic evaluation of 1,980 deterministic test instances across 15 LLM configurations, we identify actionable reliability thresholds for production deployment. Our findings reveal that tool initialization failures are the most dominant error type, and open-weight models at 32B parameter scale can achieve closed-source reliability levels.

---

## Method

### 12-Category Error Taxonomy

We propose a systematic error taxonomy for multi-agent LLM system failures:

1. **Tool Initialization Failures**:
   - DB_UPDATE_TOOL_NOT_INITIALIZED
   - DB_SELECT_TOOL_NOT_INITIALIZED
   - DB_SEARCH_TOOL_NOT_INITIALIZED

2. **Parameter Errors**:
   - DB_SELECT_QUERY_PARAMETER_ERROR
   - DB_UPDATE_QUERY_PARAMETER_ERROR
   - DB_SEARCH_QUERY_PARAMETER_ERROR

3. **Execution Failures**:
   - DB_EXECUTION_FAILURE
   - FILE_READ_TOOL_NOT_INITIALIZED
   - FILE_WRITE_TOOL_NOT_INITIALIZED

4. **Result Interpretation Errors**:
   - DB_RESULT_INTERPRETATION_ERROR
   - FILE_READ_PARAMETER_ERROR
   - FILE_WRITE_PARAMETER_ERROR

---

## Datasets & Experiments

### Invoice Reconciliation Task
The evaluation uses Invoice Reconciliation, which involves:
1. Database queries for relevant data
2. File processing for invoices and receipts
3. Business logic for comparison and reconciliation
4. Result generation

### Test Configurations
- **LLM Configurations**: 15 configurations (Open-weight + Proprietary)
  - Qwen2.5 series (3B, 7B, 14B, 32B, 72B)
  - Functionary
  - GPT-4, GPT-4.1, Claude 3.5, Claude 3.7

- **Hardware Platforms**:
  - NVIDIA RTX A6000
  - NVIDIA RTX 4090
  - Apple M3 Max

---

## Results

### Table 1: Overall Invoice Reconciliation Performance

| Model | Platform | Success Rate (%) | Time (s) | Steps |
|-------|----------|------------------|----------|-------|
| qwen2.5:3b | GPU | 23.64 | 14.7 | 5.4 |
| qwen2.5:7b | GPU | 85.45 | 12.3 | 4.2 |
| qwen2.5:14b | GPU | 96.64 | 7.3 | 3.1 |
| qwen2.5:32b | GPU | 100.0 | 6.8 | 2.9 |
| GPT-4.1 | API | 100.0 | 7.2 | 3.0 |

### Key Findings
1. **Reliability Threshold**: 14B parameters is minimum viable (96.6%), 32B achieves closed-source level (100%)
2. **Initialization Dominates**: Over 60% of errors are tool initialization failures
3. **Scale Effect**: Reliability improves significantly with model scale

---

## Key Figures

### Figure 1: Error Taxonomy Overview
![Error Taxonomy](figures/figure-000.png)
- (a) Superior procedural reliability of closed-source models
- (b) Dramatic variation in open-weight models with scale

---

## Main Contributions

1. **Systematic diagnostic framework** with 12-category error taxonomy
2. **Reproducible evaluation infrastructure** across 15 LLM configurations
3. **Reliability threshold identification**: 14B (minimum production), 32B (closed-source level)
4. **Deployment guidance** with hardware-performance characterization

---

## Key Findings

- Tool initialization failures are the primary reliability bottleneck
- Open-weight models at 32B scale achieve closed-source reliability
- 14B models offer optimal cost-performance tradeoff
