# MATA: A Trainable Hierarchical Automaton System for Multi-Agent Visual Reasoning

**Paper ID:** arXiv:2601.19204 (ICLR 2026)

## Authors
- Zhixi Cai, Fucai Ke, Kevin Leo, Sukai Huang, Maria Garcia de la Banda, Peter J. Stuckey, Hamid Rezatofighi (Monash University)

---

## Abstract

We present MATA (Multi-Agent hierarchical Trainable Automaton), a novel multi-agent system for visual reasoning. While existing methods often follow rigid execution orders or have complex inter-agent communication protocols, providing only limited reasoning capabilities, MATA is presented as a hierarchical finite-state automaton. The top-level transitions are chosen by a trainable hyper agent, while each agent runs a rule-based sub-automaton for micro-control. The key innovation is that the hyper agent's state transition policy can be trained. We build MATA-SFT-90K, a dataset of 90,854 training examples. MATA achieves state-of-the-art results on GQA, OK-VQA, and Referring Expression Comprehension benchmarks, significantly outperforming previous methods.

우리는 시각적 추론을 위한 새로운 multi-agent 시스템인 MATA (Multi-Agent hierarchical Trainable Automaton)를 제시합니다. 기존의 방법들이 종종 고정된 실행 순서를 따르거나 복잡한 에이전트 간 통신 프로토콜을 가져 제한된 추론 능력만 제공하는 반면, MATA는 계층적 유한 상태 오토마톤으로 제시됩니다. 최상위 전이는 학습 가능한 hyper agent가 선택하는 반면, 각 에이전트는 마이크로 제어를 위한 규칙 기반 하위 오토마톤을 실행합니다. 핵심 혁신은 hyper agent의 상태 전환 정책을 학습할 수 있다는 것입니다. 90,854개의 훈련 예제로 데이터셋인 MATA-SFT-90K를 구축했습니다. MATA는 GQA, OK-VQA 및 Referring Expression Comprehension 벤치마크에서 최첨단 결과를 달성하여 이전 방법을 크게 앞섭니다.

---

## Introduction

Visual reasoning remains a challenging task for AI systems, requiring understanding of complex scenes, spatial relationships, and contextual information. While LLMs have shown impressive reasoning capabilities, applying them to visual tasks introduces unique challenges.

시각적 추론은 여전히 AI 시스템에게 도전적인 작업으로, 복잡한 장면, 공간적 관계 및 맥락적 정보를 이해해야 합니다. LLM은 인상적인 추론 역량을 보여왔지만, 시각적 작업에 적용에는 고유한 도전이 있습니다.

Existing approaches include monolithic VLMs, compositional methods, and multi-agent systems. However, these approaches often suffer from rigid execution orders, complex communication protocols, and limited reasoning capabilities.

기존 접근법에는 monolithic VLMs, 구성적 방법 및 multi-agent 시스템이 포함됩니다. 그러나 이러한 접근법들은 종종 고정된 실행 순서, 복잡한 통신 프로토콜 및 제한된 추론 능력으로 고통받습니다.

MATA addresses these issues by introducing a hierarchical automaton where: a hyper agent decides which specialized agent to use, each sub-agent handles specific reasoning tasks, and the system can be trained to optimize transition decisions. This allows the system to learn when to use which type of reasoning, rather than relying on fixed rules.

MATA는这些问题를 해결합니다: hyper agent가 어떤 전문화된 에이전트를 사용할지 결정하고, 각 하위 에이전트가 특정 추론 작업을 처리하며, 시스템을 훈련하여 전환 결정을 최적화할 수 있습니다. 이를 통해 시스템은 고정된 규칙에 의존하는 대신 어떤类型的 추론을 언제 사용할지 학습할 수 있습니다.

---

## Method

### Hierarchical Automaton
1. **Hyper Automaton**: Trainable state transition policy (which agent to use)
2. **Sub Automata**: Rule-based micro-control (how each agent behaves)

계층적 오토마톤:
1. **Hyper 오토마톤**: 학습 가능한 상태 전환 정책 (어떤 에이전트 사용할지)
2. **하위 오토마톤**: 규칙 기반 마이크로 제어 (각 에이전트가 어떻게 행동하는지)

### States: INITIAL, ONESHOT, STEPWISE, SPECIALIZED, FINAL, FAILURE

상태: 초기, 원샷, 스텝와이즈, 특별, 최종, 실패

---

## Results

### Table 1: GQA Performance

| Method | Accuracy (%) |
|--------|--------------|
| ViperGPT | 37.9 |
| MATA | **64.9** |

### Table 2: OK-VQA Performance

| Method | Accuracy (%) |
|--------|--------------|
| GPT-4o | 75.7 |
| MATA | **76.5** |

---

## Key Figures

### Figure 1: MATA Overview
![Teaser](image/teaser.png)

### Figure 2: Pipeline
![Pipeline](image/pipeline.png)

---

## Main Contributions

1. Hierarchical automaton design combining neuro-symbolic and multi-agent approaches
2. Trainable transition mechanism replacing hand-written rules
3. MATA-SFT-90K dataset with 90,854 training examples
4. State-of-the-art on GQA, OK-VQA, RefCOCO

주요 기여:
1. 신호기호식과 multi-agent 접근법을 결합한 계층적 오토마톤 설계
2. 수작성 규칙을 대체하는 학습 가능한 전환 메커니즘
3. 90,854개의 훈련 예제가 있는 MATA-SFT-90K 데이터셋
4. GQA, OK-VQA, RefCOCO에서의 최첨단 성능
