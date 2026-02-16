# When Agents Fail to Act: A Diagnostic Framework for Tool Invocation Reliability in Multi-Agent LLM Systems

**Paper ID:** arXiv:2601.16280

## Authors
- Donghao Huang (Singapore Management University / Mastercard)
- Gauri Malwe (Mastercard)
- Zhaoxia Wang (Singapore Management University)

---

## Abstract (400+자)

Multi-Agent LLM 시스템의/tool invocation 신뢰성을 평가하기 위한 포괄적인 진단 프레임워크를 제안합니다. 이 연구의 배경에는 최근 LLM 기반 에이전트가 도구를 사용하여 복잡한 작업을 수행하는 능력을 보여주고 있지만, 이러한 다중 에이전트 시스템의 절차적 신뢰성에 대한 체계적인 평가는 아직 부족하다는 문제가 있습니다. 우리는 12개 카테고리 오류 분류법을 통해 도구 초기화, 매개변수 처리, 실행, 결과 해석의 실패 모드를 포착합니다. 1,980개의 결정론적 테스트 인스턴스로 15개 LLM 구성을 체계적으로 평가합니다. 실험 결과, 도구 초기화 실패가 가장 지배적인 오류 유형임을 발견했습니다. 또한 32B 파라미터 규모의 오픈 가중 모델이 폐쇄 소스 모델의 신뢰성 수준을 달성할 수 있음을 보여줍니다.

---

## Method (400+자)

### 12-Category Error Taxonomy

우리는 다중 에이전트 LLM 시스템의 실패 모드를 분류하기 위한 체계적인 오류 분류법을 제안합니다:

1. **도구 초기화 실패**:
   - DB_UPDATE_TOOL_NOT_INITIALIZED: 데이터베이스 업데이트 도구 초기화 실패
   - DB_SELECT_TOOL_NOT_INITIALIZED: 데이터베이스 선택 도구 초기화 실패
   - DB_SEARCH_TOOL_NOT_INITIALIZED: 데이터베이스 검색 도구 초기화 실패

2. **매개변수 오류**:
   - DB_SELECT_QUERY_PARAMETER_ERROR: SELECT 쿼리 매개변수 오류
   - DB_UPDATE_QUERY_PARAMETER_ERROR: UPDATE 쿼리 매개변수 오류
   - DB_SEARCH_QUERY_PARAMETER_ERROR: SEARCH 쿼리 매개변수 오류

3. **실행 실패**:
   - DB_EXECUTION_FAILURE: 데이터베이스 실행 실패
   - FILE_READ_TOOL_NOT_INITIALIZED: 파일 읽기 도구 초기화 실패
   - FILE_WRITE_TOOL_NOT_INITIALIZED: 파일 쓰기 도구 초기화 실패

4. **결과 해석 오류**:
   - DB_RESULT_INTERPRETATION_ERROR: 데이터베이스 결과 해석 오류
   - FILE_READ_PARAMETER_ERROR: 파일 읽기 매개변수 오류
   - FILE_WRITE_PARAMETER_ERROR: 파일 쓰기 매개변수 오류

### 평가 프로토콜

각 LLM 구성에 대해 1,980개의 결정론적 테스트 인스턴스를 실행하고, 오류 유형별 발생 횟수를 측정합니다. 이를 통해 모델별 신뢰성 프로파일을 구축합니다.

---

## Datasets & Experiments (400+자)

### Invoice Reconciliation Task

평가에는 Invoice Reconciliation 작업이 사용됩니다. 이 작업은 다중 에이전트 시스템에서 가장 복잡한 시나리오 중 하나로, 다음과 같은 단계가 포함됩니다:

1. **데이터베이스 쿼리**: 관련 데이터 검색
2. **파일 처리**: invoices와 receipts 읽기
3. **비즈니스 로직**: 데이터 비교 및 조정
4. **결과 생성**: 조정 결과 작성

### 테스트 설정

- **LLM 구성**: 15개 구성 (Open-weight + Proprietary)
  - Qwen2.5 series (3B, 7B, 14B, 32B, 72B)
  - Functionary
  - GPT-4, GPT-4.1, Claude 3.5, Claude 3.7

- **하드웨어 플랫폼**:
  - NVIDIA RTX A6000
  - NVIDIA RTX 4090
  - Apple M3 Max

- **시각/비시각 작업**: 8개 비전 작업 + 다양한 텍스트 전용 작업

---

## Results (800+자)

### Table 1: Overall Invoice Reconciliation Performance

| Model | Platform | Success Rate (%) | Time (s) | Steps |
|-------|----------|------------------|----------|-------|
| qwen2.5:3b | GPU | 23.64 | 14.7 | 5.4 |
| qwen2.5:7b | GPU | 85.45 | 12.3 | 4.2 |
| qwen2.5:14b | GPU | 96.64 | 7.3 | 3.1 |
| qwen2.5:32b | GPU | 100.0 | 6.8 | 2.9 |
| qwen2.5:72b | GPU | 100.0 | 6.5 | 2.8 |
| GPT-4.1 | API | 100.0 | 7.2 | 3.0 |

### Table 2: Error Distribution (Vision Tasks)

| Model | DB Init | Param | Exec | Interpret |
|-------|---------|-------|------|-----------|
| qwen2.5:3b | 45% | 12% | 8% | 10% |
| qwen2.5:7b | 8% | 4% | 2% | 1% |
| qwen2.5:14b | 2% | 1% | 0% | 0% |
| qwen2.5:32b | 0% | 0% | 0% | 0% |

### Table 3: Error Distribution (Non-Vision Tasks)

| Model | Init Failures | Parameter Errors | Execution Failures |
|-------|---------------|------------------|-------------------|
| qwen2.5:3b | 76.36% | 15.2% | 8.4% |
| qwen2.5:7b | 12.1% | 2.3% | 0.1% |
| qwen2.5:14b | 3.4% | 0% | 0% |
| qwen2.5:32b | 0% | 0% | 0% |

### 주요 발견

1. **신뢰성 임계값**: 14B 파라미터가 최소 생산 구성(96.6% 성공률), 32B가 폐쇄 소스 신뢰성 달성(100%)
2. **초기화 실패가 지배적**: 전체 오류의 60% 이상이 도구 초기화 실패
3. **하드웨어 영향**: 8.2배 지연시간 변동 (RTX A6000 vs M3 Max)
4. **규모 효과**: 모델 규모 증가에 따라 신뢰성 크게 향상

---

## Key Figures

### Figure 1: Error Taxonomy Overview
![Error Taxonomy](figures/figure-000.png)
- 12 카테고리 오류 분류법 시각화
- (a) 폐쇄 소스 모델의 우수한 절차 신뢰성
- (b) 오픈 가중 모델의 규모별 변동

---

## Main Contributions

1. **체계적 진단 프레임워크**: 12개 카테고리 오류 분류법을 통한 다중 에이전트 신뢰성 평가
2. **재현 가능한 평가 인프라**: 15개 LLM 구성, 다양한 하드웨어 플랫폼에서 표준화된 평가
3. **신뢰성 임계값 식별**: 14B(최소 생산 구성), 32B(폐쇄 소스 수준)
4. **배포 가이드**: 하드웨어-성능 특성과 실제 배포 권장사항

---

## Key Findings

- 도구 초기화 실패가 주요 신뢰성 병목입니다.
- 32B 규모에서 오픈 가중 모델이 폐쇄 소스 신뢰성을 달성합니다.
- 14B 모델이 비용-성능 tradeoff에 최적입니다.
