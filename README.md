# Beyond Correlation: Interpretable Evaluation of Machine Translation Metrics

**arXiv:2410.05183v1 [cs.CL]** | October 7, 2024  
**Original Authors:** Stefano Perrella<sup>*</sup>, Lorenzo Proietti<sup>*</sup>, Pere-Lluís Huguet Cabot, Edoardo Barba, Roberto Navigli  
**Affiliation:** Sapienza NLP Group, Sapienza University of Rome  

[![Paper PDF](https://img.shields.io/badge/Paper-PDF-blue)](https://arxiv.org/pdf/2410.05183) [![Code](https://img.shields.io/badge/Code-GitHub-green)](https://github.com/SapienzaNLP/interpretable-mt-metrics-eval) [![Repo](https://img.shields.io/badge/Summary-Repo-orange)](https://github.com/jeongon-eric/paper_summary)

## Disclaimer
*이 저장소는 Sapienza NLP Group의 원저자들에 의해 작성된 논문의 구조화된 영어/한국어 요약 및 분석입니다. 요약자: Eric (AI 어시스턴트, Jeongon의 개인 AI). 원 논문의 내용/저작권을 존중하며, 학술적 리뷰/세미나 자료로 활용하세요. 피드백 환영 (Issues/PR).*

## Overview
논문 섹션별 **원문 발췌 (blockquote)** → **영어 요약** → **한국어 요약** → **키 쿼트** → **인사이트** 형식.  
**Full Text**: [paper1.txt](paper_images/paper1.txt) (PDF 추출, 1,560줄).  
**Figures/Images**: [paper_images/](paper_images/) (전 페이지, cropped 테이블/그림).  
**Original Paper**: [2410.05183.pdf](2410.05183.pdf).

프레임워크: MT 메트릭의 scalar 점수 불투명성 해결, 데이터 필터링/리랭킹 프록시로 P/R/F<sub>β</sub> 평가 (correlation 너머).

---

![Figure 1: Scalar Score Example](paper_images/cropped_fig1.png)  
*Fig 1: COMET=0.86 등 scalar 점수의 해석 어려움 예시 (MetricX, GEMBA-MQM 포함).*

## Abstract

### Original Excerpt
> Machine Translation (MT) evaluation metrics assess translation quality automatically. Recently, researchers have employed MT metrics for various new use cases, such as data filtering and translation re-ranking. However, most MT metrics return assessments as scalar scores that are difficult to interpret [...] we introduce an interpretable evaluation framework for MT metrics [...] using Precision, Recall, and F-score [...] concerns regarding [...] DA+SQM [...] low agreement with [...] MQM [...]

### English Summary
MT metrics' scalar outputs hinder interpretability for new tasks (filtering/re-ranking). Introduces P/R/F<sub>β</sub> proxies; critiques DA+SQM reliability vs. MQM.

### 한국어 요약
MT 메트릭 scalar 점수 해석 어려움 → 필터링/리랭킹 새 용도 약함. **P/R/Fβ 프레임워크 제안**. DA+SQM 인간 데이터 MQM과 낮은 일치.

### Key Quote
> \"most MT metrics return assessments as scalar scores that are difficult to interpret [...] using Precision, Recall, and F-score\"

### Insights
From correlation (Spearman ρ/τ) to actionable metrics. Code for threshold tuning/reproducibility.

## 1. Introduction

### Original Excerpt
> Over the past few years, Machine Translation (MT) evaluation metrics have transitioned from heuristic-based to neural-based [...] new MT metrics use cases have emerged [filtering, re-ranking, RL]. [...] lack of a dedicated evaluation [...] challenging to determine [...] one metric suits a given task better [...]

### English Summary
Neural metrics improve correlation but lack opacity-aware eval for non-dev uses. Gap: Interpretable proxies needed.

### 한국어 요약
Neural MT 메트릭 correlation ↑ but 새 용도(필터링/리랭킹/RL) 불투명. **전용 해석 평가 부재**.

### Key Quote
> \"data filtering [...] translation re-ranking [...] we address these issues by introducing a novel and more interpretable evaluation framework\"

### Insights
WMT tasks gap; practical: threshold over grid-search.

## 2. Interpretability of MT Metrics’ Assessments

### Original Excerpt
> Interpretability [...] ability to explain [...] to a human. [...] lack of interpretability to three main factors: 1. Range consistency [...] 2. Error attribution [...] 3. Performance [correlation-only] [...]

### English Summary
**3 Issues**: (1) Score range inconsistency; (2) No error localization; (3) Correlation blind to use-cases. Interpretable metrics (MaTESe/xCOMET/GEMBA) have trade-offs.

### 한국어 요약
**3대 문제**: 1) 점수 범위 불일치, 2) 에러 귀속 불가, 3) 상관관계 한계. 기존 interpretable 메트릭 trade-off.

### Key Quote
> \"Range consistency: unclear whether a difference [...] has the same meaning [...] Error attribution: [...] do not identify specific [...] errors [...] Performance: correlation [...]\"

### Insights
Assessment (not model) interpretability focus.

![P/R Trade-off Graph](paper_images/cropped_paper1_graph.png)

## 3. Proposed Framework

### Original Excerpt (3.1)
> Metrics as Binary Classifiers [...] M(t) ≥ τ → GOOD [...] P_Mτ = Pr(H(t)=GOOD | M(t) ≥ τ) [...] F_Mτ = (3PR)/(2√(1/2)P + R) [...] Re-Ranking Precision: |T^M ∩ T^H| / |T^M|

### English Summary
**Filtering**: τ-based binary P/R/F<sub>β</sub> (Precision-weighted). **Re-ranking**: Top-overlap RRP.

### 한국어 요약
**필터링**: τ로 GOOD/BAD 분류, P/R/Fβ. **리랭킹**: 최고 번역 RRP. Fβ Precision 중시.

### Key Quote
> \"F_Mτ = (3 P R) / (2√(1/2) P + R)\"

### Insights
Penalizes false positives (filtering-critical). Open-source framework.

## 4. Experiments

### Original Excerpt
> WMT23MQM [...] Metrics: COMET*, BLEURT, MetricX-23*, xCOMET*, MaTESe*, GEMBA-MQM [...] GOOD: MQM ≥ -4 [...]

### English Summary
ZH→EN (others Appendix). 15 systems. Thresholds: max F test/dev.

### 한국어 요약
WMT23MQM 데이터, 14 메트릭. GOOD ≥ -4 (Major error 없음).

### Insights
MQM penalties: Major(-25/-5), Minor(-1). DA+SQM baseline.

## 5. Results

### Key Table (Table 1, ZH→EN)
| Metric                  | GOOD/BAD F<sub>β</sub> | PERFECT/OTHER F<sub>β</sub> | RRP   |
|-------------------------|-------------------------|-----------------------------|-------|
| GEMBA-MQM              | 81.59                  | 67.14                       | 42.58%|
| xCOMET-QE-ENSEMBLE     | 81.40                  | 67.73                       | 41.40%|
| MetricX-23-QE-XL (open)| 79.64                  | 68.10                       | 36.09%|
| DA+SQM (human)         | 75.18                  | 56.06                       | 32.99%|

![Table 1 Cropped](paper_images/cropped_table1.png)  
![Threshold Fig 3](paper_images/cropped_paper1_fig3.png)

### English Summary
Ref-based ≥ ref-free; top open ref-free: MetricX-23-QE-XL. Thresholds unstable.

### 한국어 요약
Ref-based 우위, 추천: MetricX-23-QE-XL (ref-free). FP ~3 Minor errors.

### Insights
**Recs**: Filtering → MetricX-QE-XL; Re-ranking → ref-based+MBR. DA+SQM < autometrics.

## Discussion & Future
- Thresholds: Aggregate datasets.
- Extend: RL/QE proxies, low-res langs.

**Citation**:
```
@article{perrella2024beyond,
  title={Beyond Correlation: Interpretable Evaluation of MT Metrics},
  author={Perrella, Stefano and others},
  journal={arXiv:2410.05183},
  year={2024}
}
```

*Full paper recommended. Feedback via Issues/PRs.*