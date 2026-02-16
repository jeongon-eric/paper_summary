# Learning Decentralized LLM Collaboration with Multi-Agent Actor Critic

**Paper ID:** arXiv:2601.21972

## Authors
- Shuo Liu, Tianle Chen, Ryan Amiri, Christopher Amato (Northeastern University)

---

## Abstract

Recent work has explored optimizing LLM collaboration through Multi-Agent Reinforcement Learning (MARL). However, most MARL fine-tuning approaches rely on predefined execution protocols, which often require centralized execution. Decentralized LLM collaboration is more appealing in practice, as agents can run inference in parallel with flexible deployments. Also, current approaches use Monte Carlo methods for fine-tuning, which suffer from high variance and thus require more samples to train effectively. Actor-critic methods are prevalent in MARL for dealing with these issues, so we developed Multi-Agent Actor-Critic (MAAC) methods to optimize decentralized LLM collaboration. In this paper, we analyze when and why these MAAC methods are beneficial. We propose 2 MAAC approaches: CoLLM-CC with a Centralized Critic and CoLLM-DC with Decentralized Critics. Our experiments across writing, coding, and game-playing domains show that Monte Carlo methods and CoLLM-DC can achieve performance comparable to CoLLM-CC in short-horizon and dense-reward settings. However, they both underperform CoLLM-CC on long-horizon or sparse-reward tasks, where Monte Carlo methods require substantially more samples and CoLLM-DC struggles to converge.

최근 연구들은 Multi-Agent Reinforcement Learning (MARL)을 통해 LLM 협력을 최적화하는 것을 탐구해왔습니다. 그러나 대부분의 MARL fine-tuning 접근법은 사전 정의된 실행 프로토콜에 의존하며, 종종 중앙집중식 실행이 필요합니다. 분산 LLM 협력이 실제로 더 매력적인데, 에이전트가 병렬로 추론을 실행하고 유연하게 배포될 수 있기 때문입니다. 또한 현재 접근법은 fine-tuning에 Monte Carlo 방법을 사용하는데, 이는 높은 분산으로 인해 더 많은 샘플이 필요합니다. Actor-Critic 방법은 이러한 문제를 해결하기 위해 MARL에서 널리 사용되며, 우리는 분산 LLM 협력을 최적화하기 위한 Multi-Agent Actor-Critic (MAAC) 방법을 개발했습니다. 이 논문에서 우리는 이러한 MAAC 방법이 언제 그리고 왜 유용한지 분석합니다. 중앙 집중식 Critic이 있는 CoLLM-CC와 분산 Critic이 있는 CoLLM-DC의 두 가지 MAAC 접근법을 제안합니다. 글쓰기, 코딩, 게임 영역에 걸친 우리의 실험은 단기/밀집 보상 설정에서 Monte Carlo 방법과 CoLLM-DC가 CoLLM-CC에 필적하는 성능을 달성할 수 있음을 보여줍니다. 그러나 장기/희소 보상 작업에서 둘 다 CoLLM-CC보다 성능이 낮으며, Monte Carlo 방법은 훨씬 더 많은 샘플이 필요하고 CoLLM-DC는 수렴하기 어렵습니다.

---

## Introduction

Advanced LLMs have demonstrated remarkable capabilities in natural language understanding and generation. This progress has driven growing efforts to transform them into autonomous agents that can solve tasks by proactively interacting with users and systems to obtain feedback and learn from past experience.

진보된 LLM은 자연어 이해와 생성에서remarkable한 역량을 보여왔습니다. 이 진전은 사용자와 시스템과 적극적으로 상호작용하여 피드백을 받고 과거 경험에서 학습하여 작업을 해결할 수 있는 자율 에이전트로 변환하려는 노력들을 이끌었습니다.

In this context, it is becoming popular to explore coordinating multiple LLMs to improve performance where agents are specified by roles, such as generators, planners, or verifiers. Building on the studies of Multi-Agent Systems (MAS), recent methods employ Multi-Agent Reinforcement Learning (MARL) to optimize their interactions. However, most existing approaches remain confined to predefined execution paradigms, which limits their applicability to broader settings. Moreover, these agents often rely on extensive inter-agent communication to accomplish tasks, requiring centralized execution, which results in limited scalability as well as potential privacy issues in larger-scale MAS.

이러한 맥락에서 생성기, 플래너, 검증기 등 역할을 지정된 에이전트들이 성능을 개선하기 위해 여러 LLM을 조정하는 것이 인기를 얻고 있습니다. Multi-Agent Systems (MAS) 연구를 기반으로, 최근 방법들은 MARL을 사용하여 상호작용을 최적화합니다. 그러나 대부분의 기존 접근법은 사전 정의된 실행 패러다임에 국한되어 있어 더 넓은 설정에 대한 적용 가능성이 제한됩니다. 또한 이러한 에이전트들은 종종 작업 수행을 위해 광범위한 에이전트 간 통신에 의존하며, 중앙집중식 실행이 필요하여 대규모 MAS에서 확장성 محد짐과 잠재적인 프라이버시 문제를 초래합니다.

Decentralized systems have been studied for decades, where each agent is deployed separately and executes independently based on its own observations. Leveraging decentralized LLM agents to complete tasks is beneficial, as it reduces memory and storage pressure on each node and improves efficiency. However, how to effectively optimize these decentralized LLMs to collaborate remains an open question.

분산 시스템은 수십 년간 연구되어 왔으며, 각 에이전트가 별도로 배포되어 자신의 관찰에 따라 독립적으로 실행됩니다. 작업을 완료하기 위해 분산 LLM 에이전트를 활용하는 것은 각 노드의 메모리와 스토리지 압력을 줄이고 효율성을 개선하기 때문에 유익합니다. 그러나 이러한 분산 LLM이 효과적으로 협력하도록 최적화하는 방법은仍未 해결된 문제입니다.

Although Monte Carlo methods are widely adopted in RL fine-tuning due to their simplicity and efficiency, extending them to optimize multi-LLM collaboration faces many difficulties. Agents need to wait until the end of an episode to receive return signals with high variance. This leads to poor sample efficiency and limits practicality in long-horizon or episodic tasks.

비록 Monte Carlo 방법이 단순성과 효율성으로 인해 RL fine-tuning에서 널리 채택되고 있지만, multi-LLM 협력을 최적화하기 위해 확장하는 것은 많은 어려움에 직면합니다. 에이전트들은 높은 분산의 반환 신호를 받기 위해 에피소드가 끝날 때까지 기다려야 합니다. 이는 샘플 효율성이 낮고 장기 또는 에피소드 작업에서의 실용성을 제한합니다.

In this paper, we develop Multi-Agent Actor-Critic (MAAC) methods for optimizing decentralized LLM collaboration. We analyze when and why MAAC methods are beneficial for MARL fine-tuning and introduce 2 approaches: CoLLM-CC that employs a centralized critic to estimate joint history values, and CoLLM-DC that uses decentralized critics to estimate individual history values.

이 논문에서 우리는 분산 LLM 협력을 최적화하기 위한 Multi-Agent Actor-Critic (MAAC) 방법을 개발합니다. MARL fine-tuning에서 MAAC 방법이 언제 그리고 왜 유용한지 분석하고, 중앙 집중식 Critic을 사용하여joint history 값을 추정하는 CoLLM-CC와 분산 Critic을 사용하여 개별 history 값을 추정하는 CoLLM-DC의 두 가지 접근법을 소개합니다.

---

## Method

### CoLLM-CC (Centralized Critic)
Learns a shared value function Vϕ(ht) that conditions on the joint history to update each agent's policy. The critic is a training construct that can be removed during execution, allowing agents to execute in a decentralized manner.

CoLLM-CC는joint history를 조건으로 각 에이전트의 정책을 업데이트하는 공유 값 함수 Vϕ(ht)를 학습합니다. Critic은 실행 중 제거할 수 있는 학습 구성으로, 에이전트가 분산 방식으로 실행할 수 있게 합니다.

### CoLLM-DC (Decentralized Critic)
Uses individual critics Vϕi(hi,t) that condition on each agent's local history. This may be harder to converge due to non-stationarity accumulating during training.

CoLLM-DC는 각 에이전트의 로컬 history를 조건으로 하는 개별 Critic Vϕi(hi,t)를 사용합니다. 학습 중 누적되는 비정상성으로 인해 수렴하기 더 어려울 수 있습니다.

---

## Datasets & Experiments

### Tasks
1. **TLDR Summarization**: Two agents summarize Reddit posts with different roles
2. **arXiv Expansion**: Agents expand paper abstracts into full introductions
3. **CoopHE**: Cooperative code generation dataset
4. **StrBuild**: Minecraft string building task
5. **HouseBuild**: Minecraft house building with enemy defense

작업:
1. **TLDR 요약**: 두 에이전트가 서로 다른 역할로 Reddit 게시물 요약
2. **arXiv 확장**: 에이전트가 논문 초안을 전체 서론으로 확장
3. **CoopHE**: 협력적 코드 생성 데이터셋
4. **StrBuild**: Minecraft 문자 건축 작업
5. **HouseBuild**: 적 방어가 있는 Minecraft 집 건축

---

## Results

### Table 1: Overall Performance

| Method | TLDR Score | arXiv Score | StrBuild IoU | HouseBuild IoU |
|--------|------------|-------------|--------------|----------------|
| Raw Model | 30.3 | 44.0 | 36.6 | 43.2 |
| GRPO | 91.7 | 91.0 | 46.1 | 54.6 |
| CoLLM-CC | **95.2** | **95.0** | **68.5** | **52.7** |

---

## Key Figures

### Figure 1: CoLLM-CC Framework
![Framework](figs/framework.png)

### Figure 2: CoLLM-DC Framework
![Framework-DC](figs/framework-dc.png)

### Figure 3: TLDR Results
![TLDR](figs/writing_tldr.png)

### Figure 4: arXiv Results
![arXiv](figs/writing_arxiv.png)

---

## Main Contributions

1. Developed MAAC methods for decentralized LLM collaboration
2. Proposed CoLLM-CC and CoLLM-DC approaches
3. Comprehensive evaluation across writing, coding, and gaming
4. Demonstrated CoLLM-CC's superiority in long-horizon tasks

주요 기여:
1. 분산 LLM 협력을 위한 MAAC 방법 개발
2. CoLLM-CC와 CoLLM-DC 접근법 제안
3. 글쓰기, 코딩, 게임에 걸친 포괄적 평가
4. 장기 작업에서 CoLLM-CC의 우위 입증
