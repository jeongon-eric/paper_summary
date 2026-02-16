# When Agents Fail to Act: A Diagnostic Framework for Tool Invocation Reliability in Multi-Agent LLM Systems

**Paper ID:** arXiv:2601.16280

## Authors
- Donghao Huang (Singapore Management University / Mastercard)
- Gauri Malwe (Mastercard)
- Zhaoxia Wang (Singapore Management University)

## Abstract
Multi-Agent LLM 시스템에서 절차적 신뢰성을 평가하기 위한 진단 프레임워크를 제안합니다. 12개 카테고리 오류 분류법을 통해 도구 초기화, 매개변수 처리, 실행, 결과 해석의 실패 모드를 포착합니다. 1,980개의 테스트 인스턴스로 15개 LLM 구성을 평가합니다.

## Method

### 12-Category Error Taxonomy
1. DB_UPDATE_TOOL_NOT_INITIALIZED
2. DB_SELECT_TOOL_NOT_INITIALIZED
3. DB_SEARCH_TOOL_NOT_INITIALIZED
4. DB_SELECT_QUERY_PARAMETER_ERROR
5. DB_UPDATE_QUERY_PARAMETER_ERROR
6. DB_SEARCH_QUERY_PARAMETER_ERROR
7. DB_EXECUTION_FAILURE
8. DB_RESULT_INTERPRETATION_ERROR
9. FILE_READ_TOOL_NOT_INITIALIZED
10. FILE_WRITE_TOOL_NOT_INITIALIZED
11. FILE_READ_PARAMETER_ERROR
12. FILE_WRITE_PARAMETER_ERROR

## Results

### Table 1: Invoice Reconciliation Performance

| Model | Platform | Success Rate (%) | Time (s) | Steps |
|-------|----------|------------------|----------|-------|
| qwen2.5:3b | GPU | 23.64 | 14.7 | 5.4 |
| qwen2.5:7b | GPU | 85.45 | 12.3 | 4.2 |
| qwen2.5:14b | GPU | 96.64 | 7.3 | 3.1 |
| qwen2.5:32b | GPU | 100.0 | 6.8 | 2.9 |
| qwen2.5:72b | GPU | 100.0 | 6.5 | 2.8 |
| GPT-4.1 | API | 100.0 | 7.2 | 3.0 |

### Table 2: Error Distribution (Vision Tasks)
### Table 3: Error Distribution (Non-Vision Tasks)

## Key Figures

### Figure 1: Error Taxonomy Overview
![Error Taxonomy](figures/figure-000.png)
- 12 카테고리 오류 분류법 시각화
- (a) 폐쇄 소스 모델의 우수한 절차 신뢰성
- (b) 오픈权重 모델의 규모별 변동

## Main Contributions
1. 12 카테고리 오류 분류법 개발
2. 15개 LLM 구성 평가
3. 신뢰성 임계값 식별 (14B: 최소, 32B: 폐쇄 소스 수준)
4. 하드웨어별 성능 분석

## Key Findings
- 도구 초기화 실패가 주요 신뢰성 병목
- 32B 규모에서 오픈 模型可以达到 폐쇄 소스 신뢰성
