# When Agents Fail to Act: A Diagnostic Framework for Tool Invocation Reliability in Multi-Agent LLM Systems

**Paper ID:** arXiv:2601.16280

## Authors
- Donghao Huang (Singapore Management University / Mastercard)
- Gauri Malwe (Mastercard)
- Zhaoxia Wang (Singapore Management University)

---

## Abstract

We propose a comprehensive diagnostic framework for evaluating tool invocation reliability in multi-agent LLM systems. While recent LLM-based agents have demonstrated remarkable capabilities in accomplishing complex tasks using tools, systematic evaluation of procedural reliability in such multi-agent systems remains lacking. We introduce a 12-category error taxonomy capturing failure modes across four major stages: tool initialization, parameter handling, execution, and result interpretation. Through systematic evaluation of 1,980 deterministic test instances across 15 different LLM configurations spanning both open-weight models (Qwen2.5 series from 3B to 72B parameters) and proprietary alternatives (GPT-4.1, Claude 3.5 Sonnet), we identify actionable reliability thresholds for production deployment. Our findings reveal three critical insights: first, tool initialization failures are the most dominant error type, accounting for over 60% of all failures in smaller models; second, there exists a clear reliability threshold at 14B parameters for minimum viable production deployment (96.64% success rate); third, open-weight models at 32B parameter scale can achieve closed-source reliability levels (100% success rate), suggesting that model scale is a primary determinant of procedural reliability in multi-agent tool use scenarios.

우리는 multi-agent LLM 시스템에서 도구 호출 신뢰성을 평가하기 위한 포괄적인 진단 프레임워크를 제안합니다. 최근 LLM 기반 에이전트들이 도구를 사용하여 복잡한 작업을 완료하는remarkable한 역량을 보여왔지만, 이러한 multi-agent 시스템에서 절차적 신뢰성에 대한 체계적인 평가는 여전히 부족합니다. 우리는 네 가지 주요 단계, 즉 도구 초기화, 매개변수 처리, 실행 및 결과 해석에 걸친 실패 모드를 포착하는 12개 카테고리 오류 분류법을 소개합니다. 15개 서로 다른 LLM 구성(3B에서 72B 파라미터의 Qwen2.5 시리즈와 GPT-4.1, Claude 3.5 Sonnet 등 독점 대안)을 통해 1,980개의 결정론적 테스트 인스턴스의 체계적인 평가를 통해 프로덕션 배포를 위한 실행 가능한 신뢰성 임계값을 식별합니다. 우리의 발견은 세 가지 중요한 통찰력을 보여줍니다: 첫째, 도구 초기화 실패가 가장 지배적인 오류 유형으로, 더 작은 모델에서 모든 실패의 60% 이상을 차지합니다; 둘째, 최소可行的 프로덕션 배포를 위한 명확한 신뢰성 임계값이 14B 파라미터에서 존재합니다 (96.64% 성공률); 셋째, 32B 파라미터 규모의open-weight 모델이 폐쇄소스 신뢰성 수준(100% 성공률)을 달성할 수 있어, 모델 규모가 multi-agent 도구 사용 시나리오에서 절차적 신뢰성의 주요 결정 요인임을 시사합니다.

---

## Introduction

The emergence of Large Language Models (LLMs) has fundamentally transformed the landscape of artificial intelligence, enabling systems that can understand natural language, generate human-like responses, and most importantly, interact with external tools and environments to accomplish complex tasks. Recent advances have led to the development of LLM-based agents that can autonomously plan, execute, and refine their actions based on feedback from tools such as databases, file systems, and APIs. These multi-agent systems represent a significant leap forward, as they can coordinate multiple specialized agents to handle different aspects of a complex workflow, potentially achieving capabilities beyond what a single LLM could accomplish.

However, while the capabilities of these systems have been extensively studied and demonstrated in various benchmarks, the reliability aspect remains critically underexplored. When a single LLM invokes a tool, there is already uncertainty about whether the invocation will succeed or fail. In multi-agent systems, this uncertainty compounds exponentially because multiple agents must coordinate their tool invocations, maintain shared state, and handle error propagation from one agent to another. A failure in one agent's tool call can cascade through the entire system, potentially causing subsequent agents to fail even if their own tool invocations would have been successful in isolation.

The challenge addressed in this paper is fundamentally about understanding how these systems fail, not just whether they succeed. Traditional evaluation metrics focused on task completion rates provide limited insight because they treat all failures as binary outcomes without distinguishing between different failure modes. For system designers and practitioners, knowing that a system fails 30% of the time is less actionable than understanding that 80% of those failures are due to tool initialization issues that could be addressed through better resource management or retry mechanisms.

This paper makes three key contributions to addressing this gap. First, we develop a comprehensive 12-category error taxonomy that systematically classifies failure modes in multi-agent tool invocation scenarios, enabling fine-grained analysis of where and why failures occur. Second, we conduct rigorous empirical evaluation across 15 different LLM configurations spanning the spectrum from small open-weight models to large proprietary ones, providing quantitative reliability thresholds that can guide production deployment decisions. Third, we provide practical recommendations for system design based on our findings, including hardware selection guidance and reliability optimization strategies.

LLM(Large Language Models)의 출현은 인공 지능의 지형을 근본적으로 변화시켰으며, 자연어를 이해하고 인간과 유사한 응답을 생성하며, 가장重要的是 외부 도구 및 환경과 상호작용하여 복잡한 작업을 완료할 수 있는 시스템들을 가능하게 했습니다. 최근 진전은 데이터베이스, 파일 시스템, API와 같은 도구의 피드백을 기반으로 자율적으로 계획을 세우고, 실행하며, 행동을 개선할 수 있는 LLM 기반 에이전트들의 개발로 이어졌습니다. 이러한 multi-agent 시스템은 여러 전문화된 에이전트를 조정하여 복잡한 워크플로우의 다른 측면을 처리할 수 있어 단일 LLM이 달성할 수 있는 것 이상의 역량을 달성할 수 있어 의미 있는 도약 represent합니다.

그러나 이러한 시스템들의 역량이 다양한 벤치마크에서 광범위하게 연구되고 입증된 반면, 신뢰성 측면은 여전히 결정적으로 충분히 탐구되지 않았습니다. 단일 LLM이 도구를 호출할 때 이미 호출이 성공할지 실패할지에 대한 불확실성이 있습니다. multi-agent 시스템에서 이 불확실성은 지수적으로 증가합니다. 여러 에이전트가 도구 호출을 조정하고, 공유 상태를 유지하며, 한 에이전트에서 다른 에이전트로의 오류 전파를 처리해야 하기 때문입니다. 한 에이전트의 도구 호출 실패가 전체 시스템を通じて cascading되어 후속 에이전트가 고립된 상태에서 자체 도구 호출이 성공했을지라도 실패하게 할 수 있습니다.

이 논문에서 다루는 도전은 근본적으로 이러한 시스템이 어떻게 실패하는지 이해하는 것이며, 단순히 성공하는지 여부가 아닙니다. 모든 실패를 실패 모드를 구분하지 않고 이진 결과로 처리하는 전통적인 평가 지표는 시스템 설계자와 실무자에게 제한적인 통찰력만 제공합니다. 시스템이 30% 실패한다는 것을 아는 것은 80%의 실패가 더 나은 리소스 관리나 재시도 메커니즘으로 해결할 수 있는 도구 초기화 문제로 인한 것임을 이해하는 것보다 실행 가능한 통찰력이 적습니다.

이 논문은 이 격차를 해결하기 위해 세 가지 주요 기여를 합니다. 첫째, multi-agent 도구 호출 시나리오에서 실패 모드를 체계적으로 분류하는 포괄적인 12개 카테고리 오류 분류법을 개발하여 실패가 발생하는 위치와 이유에 대한 세분화된 분석을 가능하게 합니다. 둘째, 작은open-weight 모델에서 큰 독점 모델에 이르기까지 15개 서로 다른 LLM 구성에 걸친 엄격한 경험적 평가를 수행하여 프로덕션 배포 결정에 안내할 수 있는 정량적 신뢰성 임계값을 제공합니다. 셋째, 하드웨어 선택 안내와 신뢰성 최적화 전략을 포함한 발견에 기반한 시스템 설계에 대한 실용적 권장사항을 제공합니다.

---

## Method

### 12-Category Error Taxonomy

Our diagnostic framework is built upon a systematic 12-category error taxonomy that comprehensively captures the failure modes in multi-agent LLM tool invocation systems. This taxonomy was developed through extensive analysis of failure patterns observed during our evaluation, and it categorizes errors into four major stages of the tool invocation lifecycle.

Our diagnostic framework는 multi-agent LLM 도구 호출 시스템에서 실패 모드를 포착하는 체계적인 12개 카테고리 오류 분류법에 기반합니다. 이 분류법은 평가 중에 관찰된 실패 패턴의 광범위한 분석을 통해 개발되었으며, 오류를 도구 호출 수명 주기의 네 가지 주요 단계로 분류합니다.

**Stage 1: Tool Initialization Failures (3 categories)**

Tool initialization failures occur when agents attempt to invoke tools that have not been properly configured or initialized in the system. These are among the most critical failures because they prevent any tool-related operations from executing, effectively blocking the entire workflow. Our taxonomy identifies three specific initialization failure modes: DB_UPDATE_TOOL_NOT_INITIALIZED occurs when an agent attempts to perform database update operations without the database tool being properly initialized; DB_SELECT_TOOL_NOT_INITIALIZED happens when database query operations are attempted but the tool has not been set up; and DB_SEARCH_TOOL_NOT_INITIALIZED occurs in similar circumstances for search functionality. These failures typically indicate resource allocation issues or improper system configuration at startup.

도구 초기화 실패는 시스템에서 제대로 구성 또는 초기화되지 않은 도구를 호출하려고 할 때 발생합니다. 이러한 실패들은任何 도구 관련 작업이 실행되는 것을 방지하여 전체 워크플로우를 효과적으로 차단하기 때문에 가장 중요한 실패들입니다.我们的 분류법은 세 가지 특정 초기화 실패 모드를 식별합니다: DB_UPDATE_TOOL_NOT_INITIALIZED는 데이터베이스 도구가 제대로 초기화되지 않은 상태에서 에이전트가 데이터베이스 업데이트 작업을 수행하려고 할 때 발생합니다; DB_SELECT_TOOL_NOT_INITIALIZED는 도구가 설정되지 않은 상태에서 데이터베이스 쿼리 작업이 시도될 때 발생합니다; 그리고 DB_SEARCH_TOOL_NOT_INITIALIZED는 검색 기능에 대해 유사한 circumstances에서 발생합니다. 이러한 실패들은 일반적으로 시작 시 리소스 할당 문제나 부적절한 시스템 구성을 나타냅니다.

**Stage 2: Parameter Errors (3 categories)**

Parameter errors occur when tool invocations are syntactically correct but fail due to malformed or invalid parameters. Unlike initialization failures, these errors occur during actual tool execution, indicating that the system has progressed past the setup phase but encountered issues with the data or parameters being processed. The three parameter error categories are: DB_SELECT_QUERY_PARAMETER_ERROR for issues in SELECT query construction, DB_UPDATE_QUERY_PARAMETER_ERROR for problems with UPDATE statement parameters, and DB_SEARCH_QUERY_PARAMETER_ERROR for invalid search query parameters. These failures often result from misalignment between the agent's understanding of the data schema and the actual database structure.

매개변수 오류는 도구 호출이 구문적으로 올바르지만 형식이 잘못되거나 유효하지 않은 매개변수로 인해 실패할 때 발생합니다. 초기화 실패와 달리 이러한 오류들은 실제 도구 실행 중에 발생하여 시스템이 설정 단계를 통과했지만 처리 중인 데이터 또는 매개변수에서 문제를 만나았음을 나타냅니다. 세 가지 매개변수 오류 카테고리는 SELECT 쿼리 구성의 문제를 위한 DB_SELECT_QUERY_PARAMETER_ERROR, UPDATE 문 매개변수의 문제를 위한 DB_UPDATE_QUERY_PARAMETER_ERROR, 그리고 유효하지 않은 검색 쿼리 매개변수를 위한 DB_SEARCH_QUERY_PARAMETER_ERROR입니다. 이러한 실패들은 종종 에이전트의 데이터 스키마 이해와 실제 데이터베이스 구조 사이의 불일치로 인해 발생합니다.

**Stage 3: Execution Failures (3 categories)**

Execution failures represent errors that occur during the actual execution of tool operations, even when parameters are correctly formatted and tools are properly initialized. These failures often indicate environmental issues, permission problems, or runtime errors. Our taxonomy includes: DB_EXECUTION_FAILURE for general database operation failures, FILE_READ_TOOL_NOT_INITIALIZED for file reading attempts without proper tool setup, and FILE_WRITE_TOOL_NOT_INITIALIZED for similar issues in file writing operations. These are particularly challenging to diagnose because they can result from transient environmental factors such as network issues, resource constraints, or external system dependencies.

실행 실패는 매개변수가 올바르게 형식화되고 도구가 제대로 초기화된 경우에도 도구 작업의 실제 실행 중에 발생하는 오류를 나타냅니다. 이러한 실패들은 종종 환경 문제, 권한 문제 또는 런타임 오류를 나타냅니다.我们的 분류법은 일반적인 데이터베이스 작업 실패를 위한 DB_EXECUTION_FAILURE, 적절한 도구 설정 없이 파일 읽기 시도를 위한 FILE_READ_TOOL_NOT_INITIALIZED, 그리고 파일 쓰기 작업에서 유사한 문제를 위한 FILE_WRITE_TOOL_NOT_INITIALIZED를 포함합니다. 이러한 실패들은 네트워크 문제, 리소스 제약 또는 외부 시스템 종속성과 같은 일시적인 환경 요인으로 인해 발생할 수 있어 진단이 특히 어렵습니다.

**Stage 4: Result Interpretation Errors (3 categories)**

Result interpretation errors occur when tools execute successfully but the agent fails to properly process or interpret the returned results. This represents a distinct failure mode where the technical execution succeeds but the semantic understanding fails. The three categories are: DB_RESULT_INTERPRETATION_ERROR for failures in processing query results, FILE_READ_PARAMETER_ERROR for issues in reading file content, and FILE_WRITE_PARAMETER_ERROR for problems in writing output. These errors often reveal limitations in the agent's reasoning capabilities or misunderstandings about data formats and structures.

결과 해석 오류는 도구가 성공적으로 실행되지만 에이전트가 반환된 결과를 적절히 처리하거나 해석하지 못할 때 발생합니다. 이것은 기술적 실행이 성공하지만 의미적 이해가 실패하는 고유한 실패 모드를 나타냅니다. 세 가지 카테고리는 쿼리 결과 처리 실패를 위한 DB_RESULT_INTERPRETATION_ERROR, 파일 내용 읽기 문제를 위한 FILE_READ_PARAMETER_ERROR, 그리고 출력 쓰기 문제를 위한 FILE_WRITE_PARAMETER_ERROR입니다. 이러한 실패들은 종종 에이전트의 추론 능력의 한계 또는 데이터 형식과 구조에 대한 오해를 드러냅니다.

---

## Datasets & Experiments

### Invoice Reconciliation Task

Our evaluation is built around the Invoice Reconciliation task, a comprehensive multi-step workflow that simulates real-world business processes requiring coordination between multiple agents. This task was selected because it encompasses all four stages of tool invocation (initialization, parameter handling, execution, result interpretation) and requires the type of complex, multi-turn interactions that stress-test agent reliability.

우리 평가는Invoice Reconciliation 작업 위에 구축되었으며, 이는 여러 에이전트 간 협업을 필요로 하는 실제 비즈니스 프로세스를 시뮬레이션하는 포괄적인 multi-step 워크플로우입니다. 이 작업은 도구 호출의 네 가지 단계(초기화, 매개변수 처리, 실행, 결과 해석)를 모두 포함하고 에이전트 신뢰성을 stress-test하는 복잡한 multi-turn 상호작용을 필요로 하기 때문에 선택되었습니다.

The workflow involves four key stages: first, database queries to retrieve relevant invoice and transaction records; second, file processing to read invoice and receipt documents from the file system; third, business logic execution to compare retrieved data and identify discrepancies; and fourth, result generation to produce reconciliation reports. Each stage involves multiple tool invocations and provides opportunities for failures at different points in the pipeline. The task terminates when either all invoices are successfully reconciled or when a predetermined step limit is reached.

워크플로우는 네 가지 주요 단계를 포함합니다: 첫째, 관련 송장 및 거래 기록을 검색하기 위한 데이터베이스 쿼리; 둘째, 파일 시스템에서 송장 및 영수증 문서를 읽기 위한 파일 처리; 셋째, 검색된 데이터를 비교하고 불일치를 식별하기 위한 비즈니스 로직 실행; 넷째, 조정 보고서를 생성하기 위한 결과 생성. 각 단계는 여러 도구 호출을 포함하며 파이프라인의 다양한 지점에서 실패 기회를 제공합니다. 작업은 모든 송장이 성공적으로 조정되거나事先 결정된 단계 제한에 도달하면 종료됩니다.

### Test Configurations

We evaluate 15 different LLM configurations representing the spectrum from small open-weight models to large proprietary systems. For open-weight models, we use the Qwen2.5 series at five different scales: 3B, 7B, 14B, 32B, and 72B parameters. These models represent the current state-of-the-art in open-weight LLM development and provide a systematic view of how model scale affects reliability. For proprietary models, we test GPT-4.1, GPT-4o-mini, Claude 3.5 Sonnet, and Claude 3.7, representing leading commercial offerings from OpenAI and Anthropic.

우리는 작은open-weight 모델에서 큰 독점 시스템에 이르기까지 15개 서로 다른 LLM 구성을 평가합니다. open-weight 모델의 경우, Qwen2.5 시리즈를 다섯 가지 다른 규모(3B, 7B, 14B, 32B, 72B 파라미터)에서 사용합니다. 이러한 모델들은open-weight LLM 개발의 현재 최첨단을 나타내며 모델 규모가 신뢰성에 어떻게 영향을 하는지에 대한 체계적인view을 제공합니다. 독점 모델의 경우, OpenAI와 Anthropic의 주요 상업적 제품을 represented하는 GPT-4.1, GPT-4o-mini, Claude 3.5 Sonnet, Claude 3.7을 테스트합니다.

Testing is conducted across three different hardware platforms to understand the interaction between model selection and deployment infrastructure. Our platforms include NVIDIA RTX A6000 (professional datacenter GPU), NVIDIA RTX 4090 (consumer high-performance GPU), and Apple M3 Max (ARM-based laptop processor). Each platform represents different deployment scenarios: server-class GPU for cloud deployments, enthusiast-grade GPU for edge computing, and mobile processor for on-device inference.

테스트는 모델 선택과 배포 인프라 간의 상호작용을 이해하기 위해 세 가지 다른 하드웨어 플랫폼에서 수행됩니다. 우리의 플랫폼에는 NVIDIA RTX A6000(전문 데이터센터 GPU), NVIDIA RTX 4090(소비자 고성능 GPU), 그리고 Apple M3 Max(ARM 기반 노트북 프로세서)가 포함됩니다. 각 플랫폼은 서로 다른 배포 시나리오를 나타냅니다: 클라우드 배포를 위한 서버 클래스 GPU, 에지 컴퓨팅을 위한 애호가 등급 GPU, 그리고 온디바이스 추론을 위한 모바일 프로세서입니다.

---

## Results

### Table 1: Overall Performance

| Model | Success Rate (%) | Time (s) | Steps |
|-------|------------------|----------|-------|
| qwen2.5:3b | 23.64 | 14.7 | 5.4 |
| qwen2.5:7b | 85.45 | 12.3 | 4.2 |
| qwen2.5:14b | 96.64 | 7.3 | 3.1 |
| qwen2.5:32b | 100.0 | 6.8 | 2.9 |
| qwen2.5:72b | 100.0 | 6.5 | 2.8 |
| GPT-4.1 | 100.0 | 7.2 | 3.0 |
| Claude 3.5 | 100.0 | 7.0 | 2.9 |
| Claude 3.7 | 100.0 | 6.8 | 2.8 |

Our results reveal three critical findings that have direct implications for production deployment. First, there is a clear reliability threshold at 14B parameters - models below this scale show significantly lower success rates (23.64% for 3B, 85.45% for 7B), while models at or above 14B achieve near-perfect reliability (96.64% for 14B, 100% for 32B and above). Second, tool initialization failures dominate in smaller models, with the 3B model showing 76.36% of all errors being initialization-related, while 32B and larger models show zero initialization failures. Third, there is an 8.2x latency variation across hardware platforms, with RTX A6000 providing the best performance and Apple M3 Max showing the highest latency, suggesting that hardware selection should be considered alongside model selection for latency-critical applications.

우리의 결과는 프로덕션 배포에 직접적인 시사점을 가진 세 가지 중요한 발견을 보여줍니다. 첫째, 14B 파라미터에서 명확한 신뢰성 임계값이 존재합니다 - 이 규모 미만의 모델은 현저히 낮은 성공률을 보여주는 반면(3B의 경우 23.64%, 7B의 경우 85.45%), 14B 이상 모델은 거의 완벽한 신뢰성을 달성합니다(14B의 경우 96.64%, 32B 이상의 경우 100%). 둘째, 도구 초기화 실패가 더 작은 모델에서 지배적이며, 3B 모델은 모든 오류의 76.36%가 초기화 관련인 것을 보여주는 반면, 32B 이상 모델은 초기화 실패가 제로입니다. 셋째, 하드웨어 플랫폼 간에 8.2배의 지연 시간 변동이 있으며, RTX A6000이 가장 좋은 성능을 제공하고 Apple M3 Max가 가장 높은 지연 시간을 보여주어, 지연 시간 중심 애플리케이션에서는 모델 선택과 함께 하드웨어 선택을 고려해야 함을 시사합니다.

---

## Key Figures

### Figure 1: Error Taxonomy Overview
![Error Taxonomy](figures/figure-000.png)

This figure provides a comprehensive visualization of our 12-category error taxonomy. Panel (a) demonstrates that closed-source models (GPT-4.1, Claude 3.5, Claude 3.7) achieve near-zero errors across all categories, indicating that these systems have mature tool invocation implementations. Panel (b) reveals the dramatic variation in open-weight models, where tool initialization failures (shown in red) dominate in smaller models and progressively decrease as model scale increases. This visualization clearly shows the relationship between model scale and reliability, with 32B and 72B models achieving closed-source-equivalent reliability levels.

이 그림은 12개 카테고리 오류 분류법의 포괄적인 시각화를 제공합니다. 패널 (a)는 폐쇄 소스 모델(GPT-4.1, Claude 3.5, Claude 3.7)이 모든 카테고리에서 거의 제로 오류를 달성하여 이러한 시스템이 성숙한 도구 호출 구현을 가지고 있음을 보여줍니다. 패널 (b)는open-weight 모델에서의劇烈한 변동을 보여주며, 여기서 도구 초기화 실패(빨간색으로 표시)가 더 작은 모델에서 지배적이고 모델 규모가 증가함에 따라 점진적으로 감소합니다. 이 시각화는 모델 규모와 신뢰성 사이의 관계를 명확히 보여주며, 32B 및 72B 모델이 폐쇄 소스-equivalent 신뢰성 수준을 달성합니다.

---

## Main Contributions

We make four key contributions to the field of multi-agent LLM system reliability. First, we develop a comprehensive 12-category error taxonomy that provides a systematic framework for understanding failure modes in tool invocation scenarios. This taxonomy enables fine-grained analysis that goes beyond simple success/failure metrics to identify specific areas for improvement. Second, we conduct rigorous empirical evaluation across 15 LLM configurations and 3 hardware platforms, providing the most comprehensive reliability study of multi-agent systems to date. Our dataset of 1,980 deterministic test instances provides statistical robustness and enables identification of reliable thresholds for production deployment. Third, we identify actionable reliability thresholds: 14B parameters as the minimum viable scale for production use, and 32B parameters for closed-source-equivalent reliability. These thresholds provide concrete guidance for system designers. Fourth, we provide practical deployment recommendations including hardware selection guidance and the observation that model scale is a primary determinant of procedural reliability in multi-agent tool use scenarios.

우리는 multi-agent LLM 시스템 신뢰성 분야에 네 가지 주요 기여를 합니다. 첫째, 도구 호출 시나리오에서 실패 모드를 이해하기 위한 체계적인 프레임워크를 제공하는 포괄적인 12개 카테고리 오류 분류법을 개발합니다. 이 분류법은 단순한 성공/실패 지표를 넘어 개선이 필요한 특정 영역을 식별할 수 있는 세분화된 분석을 가능하게 합니다. 둘째, 15개 LLM 구성과 3개 하드웨어 플랫폼에 걸친 엄격한 경험적 평가를 수행하여 현재까지 가장 포괄적인 multi-agent 시스템 신뢰성 연구를 제공합니다. 1,980개의 결정론적 테스트 인스턴스의 우리 데이터셋은 통계적 강건성을 제공하고 프로덕션 배포를 위한 신뢰할 수 있는 임계값 식별을 가능하게 합니다. 셋째, 실행 가능한 신뢰성 임계값을 식별합니다: 프로덕션 사용을 위한 최소可行的 규모로 14B 파라미터, 폐쇄 소스-equivalent 신뢰성을 위한 32B 파라미터. 이러한 임계값은 시스템 설계자에게 구체적인 안내를 제공합니다. 넷째, 하드웨어 선택 안내와 모델 규모가 multi-agent 도구 사용 시나리오에서 절차적 신뢰성의 주요 결정 요인이라는 관찰을 포함한 실용적인 배포 권장사항을 제공합니다.

주요 기여:
1. 12개 카테고리 오류 분류법을 통한 체계적 진단 프레임워크
2. 15개 LLM 구성과 3개 하드웨어 플랫폼에 걸친 재현 가능한 평가
3. 신뢰성 임계값 식별 (14B: 최소 프로덕션, 32B: 폐쇄 소스 수준)
4. 하드웨어-성능 특성을 통한 배포 안내
