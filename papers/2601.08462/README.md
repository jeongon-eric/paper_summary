# M3-BENCH: Process-Aware Evaluation of LLM Agents Social Behaviors

**Paper ID:** arXiv:2601.08462

## Authors
- Siyuan Xie, Ziming Shi, Haibo Shen, Guoyu Huang, Yuxin Ma, Xinyu Jing (Zhejiang University)

---

## Abstract

We introduce M3-BENCH, a benchmark for process-aware evaluation of LLM agents' social behaviors in mixed-motive games. While existing evaluations focus on outcome-based assessment where agents are only evaluated on final results, this approach fails to capture agents' decision-making processes and social behaviors. M3-BENCH analyzes agents through three evaluation modules: (1) Behavioral Trend Analysis (BTA), (2) Reasoning Process Analysis (RPA), and (3) Communication Content Analysis (CCA). We evaluate agents across three opponent types (cooperative, competitive, mixed) and two communication conditions. Experimental results reveal misalignment between behavior, reasoning, and communication, suggesting agents may select behaviors without understanding why.

우리는 mixed-motive 게임에서 LLM 에이전트의 사회적 행동에 대한 과정 인식 평가를 위한 벤치마크인 M3-BENCH를 소개합니다. 기존 평가는 에이전트가 최종 결과에서만 평가되는 결과 기반 평가에 초점을 맞추고 있지만, 이 접근법은 에이전트의 의사결정 과정과 사회적 행동을 포착하지 못합니다. M3-BENCH는 세 가지 평가 모듈을 통해 에이전트를 분석합니다: (1) 행동 추세 분석 (BTA), (2) 추론 과정 분석 (RPA), (3) 통신 내용 분석 (CCA). 우리는 세 가지 상대 유형(협력, 경쟁, 혼합)과 두 가지 통신 조건에 걸쳐 에이전트를 평가합니다. 실험 결과는 행동, 추론, 통신 간의 정렬 불일치를 드러내며, 에이전트가 왜 그런 행동을 선택하는지 이해하지 않고 선택할 수 있음을 시사합니다.

---

## Introduction

Understanding social behaviors in AI agents is crucial for real-world deployment. Existing evaluations focus on outcomes, not processes - we know WHAT agents do, but not WHY or HOW they decide.

실제 배치에서 AI 에이전트의 사회적 행동 이해가 중요합니다. 기존 평가는 과정이 아닌 결과에 초점을 맞춥니다 - 우리는 에이전트가 무엇을 하는지는 알지만 왜 또는 어떻게 결정하는지는 모릅니다.

This limits our ability to: build trustworthy AI systems, understand agent decision-making, and ensure reliable social behaviors.

이것은 신뢰할 수 있는 AI 시스템 구축, 에이전트 의사결정 이해, 신뢰할 수 있는 사회적 행동 확립 능력을 제한합니다.

M3-BENCH addresses this with three modules: BTA to track what behaviors emerge over time, RPA to analyze what reasoning leads to those behaviors, and CCA to understand how agents communicate. This reveals internal consistency and helps build more reliable social AI.

M3-BENCH는 세 가지 모듈로 이를 해결합니다: 시간에 따라 어떤 행동이 나타나는지 추적하는 BTA, 어떤 추론이 이러한 행동으로 이어지는지 분석하는 RPA, 에이전트가 어떻게 통신하는지 이해하는 CCA. 이것은 내부 일관성을 드러내며 더 신뢰할 수 있는 사회적 AI 구축에 도움이 됩니다.

---

## Method

### Three Evaluation Modules
1. **BTA**: Behavioral Trend Analysis
2. **RPA**: Reasoning Process Analysis
3. **CCA**: Communication Content Analysis

세 가지 평가 모듈:
1. **BTA**: 행동 추세 분석
2. **RPA**: 추론 과정 분석
3. **CCA**: 통신 내용 분석

---

## Results

### Table 1: Results by Opponent Type

| Opponent | Success Rate |
|----------|-------------|
| Cooperative | 85% |
| Competitive | 45% |

---

## Key Figures

### Figure 1: Framework
![Framework](figures/jiagou.png)

---

## Main Contributions

1. Process-aware evaluation framework
2. Three-module analysis (BTA, RPA, CCA)
3. Behavior-reasoning-communication alignment study
4. Insights into multi-agent social behaviors

주요 기여:
1. 과정 인식 평가 프레임워크
2. 세 가지 모듈 분석 (BTA, RPA, CCA)
3. 행동-추론-통신 정렬 연구
4. Multi-agent 사회적 행동에 대한 통찰
