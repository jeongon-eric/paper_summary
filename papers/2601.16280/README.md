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

## Introduction

Recent advances in LLM-based multi-agent systems have demonstrated significant potential for solving complex tasks through tool invocation. However, while these systems show impressive capabilities in single-step tool usage, their reliability in multi-step workflows remains unclear.

The challenge lies in understanding how these systems behave when coordinating multiple agents, each potentially calling different tools at different stages of task execution. Unlike single-agent scenarios, multi-agent systems introduce additional complexity in terms of coordination, shared state management, and error propagation.

This paper addresses this gap by proposing a systematic diagnostic framework for evaluating procedural reliability. We focus on understanding not just whether tasks succeed, but HOW they fail - identifying specific failure modes that can be addressed in future system design.

Our contributions include: (1) a comprehensive error taxonomy with 12 categories, (2) systematic evaluation across 15 LLM configurations, (3) identification of reliability thresholds for production deployment, and (4) practical recommendations for system design.

---

## Method

### 12-Category Error Taxonomy

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
Involves: database queries, file processing, business logic comparison, result generation.

### Test Configurations
- **LLM Configurations**: 15 configurations including Qwen2.5 series (3B-72B), GPT-4, Claude 3.5
- **Hardware Platforms**: NVIDIA RTX A6000, RTX 4090, Apple M3 Max

---

## Results

### Table 1: Overall Performance

| Model | Success Rate (%) | Time (s) | Steps |
|-------|------------------|----------|-------|
| qwen2.5:3b | 23.64 | 14.7 | 5.4 |
| qwen2.5:7b | 85.45 | 12.3 | 4.2 |
| qwen2.5:14b | 96.64 | 7.3 | 3.1 |
| qwen2.5:32b | 100.0 | 6.8 | 2.9 |
| GPT-4.1 | 100.0 | 7.2 | 3.0 |

---

## Key Figures

### Figure 1: Error Taxonomy Overview
![Error Taxonomy](figures/figure-000.png)

---

## Main Contributions

1. Systematic diagnostic framework with 12-category error taxonomy
2. Reproducible evaluation across 15 LLM configurations
3. Reliability threshold identification
4. Deployment guidance with hardware-performance characterization
