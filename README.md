# Beyond Correlation: Interpretable Evaluation of Machine Translation Metrics

**arXiv:2410.05183v1 [cs.CL]** | October 7, 2024  
**Authors:** Stefano Perrella<sup>*</sup>, Lorenzo Proietti<sup>*</sup>, Pere-Lluís Huguet Cabot, Edoardo Barba, Roberto Navigli  
**Affiliation:** Sapienza NLP Group, Sapienza University of Rome  

[![Paper PDF](https://img.shields.io/badge/Paper-PDF-blue)](https://arxiv.org/pdf/2410.05183) [![Code](https://img.shields.io/badge/Code-GitHub-green)](https://github.com/SapienzaNLP/interpretable-mt-metrics-eval) [![Repo](https://img.shields.io/badge/Repo-Source-orange)](https://github.com/jeongon-eric/paper_summary)

## Overview
This repository hosts a structured, sectional summary of the paper, designed for academic review and seminar preparation. Each major section includes:

- **Original Excerpts**: Key passages from the paper.
- **Summary**: Concise distillation of core ideas.
- **Key Quotes**: Pivotal statements.
- **Insights**: Analytical takeaways and implications for MT research.

**Full Text Extraction**: [paper1.txt](paper_images/paper1.txt) (1,560 lines from PDF via pdftotext).  
**Figures**: High-resolution extracts from [paper_images/](paper_images/) (all pages, cropped tables/figs).  
**Original Paper**: [2410.05183.pdf](2410.05183.pdf).

The framework addresses limitations in MT metric interpretability, proposing Precision/Recall/F<sub>β</sub>-based proxies for data filtering and re-ranking—beyond traditional correlation-with-human metrics.

---

![Figure 1](paper_images/cropped_fig1.png)  
*Figure 1: Example of opaque scalar scores (COMET=0.86) across metrics, highlighting interpretability challenges.*

## Abstract

### Original Text
```
Machine Translation (MT) evaluation metrics assess translation quality automatically. Recently, researchers have employed MT metrics for various new use cases, such as data filtering and translation re-ranking. However, most MT metrics return assessments as scalar scores that are difficult to interpret [...] To address these issues, we introduce an interpretable evaluation framework for MT metrics [...] using Precision, Recall, and F-score [...] we raise concerns regarding the reliability of [...] DA+SQM [...] reporting a notably low agreement with Multidimensional Quality Metrics (MQM) annotations.
```

### Summary
MT metrics' scalar outputs lack interpretability for emerging tasks (filtering, re-ranking). Proposes P/R/F<sub>β</sub> framework as proxies; critiques DA+SQM vs. MQM reliability.

### Key Quote
> \"most MT metrics return assessments as scalar scores that are difficult to interpret [...] we introduce an interpretable evaluation framework [...] using Precision, Recall, and F-score\"

### Insights
Shifts evaluation from Spearman/τ correlation to actionable P/R/F<sub>β</sub> (β=√(1/2), Precision-weighted). Enables threshold selection for binary classification (GOOD/BAD). Code released for reproducibility.

## 1. Introduction

### Original Excerpt
```
Over the past few years, Machine Translation (MT) evaluation metrics have transitioned from heuristic-based to neural-based [...] new MT metrics use cases have emerged [filtering, re-ranking, RL rewards]. [...] the lack of a dedicated evaluation [...] makes it challenging to determine whether one metric suits a given task better [...]
```

### Summary
Neural MT metrics excel in correlation but falter in opacity for non-traditional uses. Gap: No interpretable proxies for filtering/re-ranking.

### Key Quote
> \"data filtering [...] translation re-ranking [...] lack of a dedicated evaluation [...] we address these issues by introducing a novel and more interpretable evaluation framework\"

### Insights
WMT Metrics tasks noted; emphasizes practical design choices (e.g., threshold optimization over grid-search).

## 2. Interpretability of MT Metrics’ Assessments

### Original Excerpt
```
Interpretability [...] refers to [...] explaining [...] to a human. [...] we attribute MT metrics assessments’ lack of interpretability to three main factors: 1. Range consistency [...] 2. Error attribution [...] 3. Performance [correlation-only] [...]
```

### Summary
**Core Issues**: (1) Inconsistent score ranges; (2) No error spans; (3) Correlation ignores use-case performance. Existing interpretable metrics (MaTESe, xCOMET, GEMBA-MQM) trade off efficacy.

### Key Quote
> \"Range consistency: unclear whether a difference in metric score has the same meaning [...] Error attribution: scalar quality assessments do not identify specific translation errors. Performance: correlation with human judgment [...]\"

### Insights
Focuses on *assessment interpretability* (not model internals). Paves way for proxy evaluations.

![P/R Trade-off](paper_images/cropped_paper1_graph.png)

## 3. Proposed Evaluation Framework

### Original Excerpt (3.1 Binary Classifiers)
```
Metrics as Binary Classifiers for Data Filtering: By selecting τ, M(t) ≥ τ → GOOD [...] P_Mτ = Pr(H(t)=GOOD | M(t) ≥ τ) [...] F_Mτ = (3PR)/(2√(1/2)P + R)
```

### Summary
**Filtering Proxy**: Binary classification with τ-optimized P/R/F<sub>β</sub> (Precision > Recall).  
**Re-ranking Proxy**: RRP = |T^M ∩ T^H| / |T^M| (top-ranked overlap).

### Key Quote
> \"F_Mτ = (3 P_Mτ R_Mτ) / (2√(1/2) P_Mτ + R_Mτ) [...] Re-Ranking Precision [...] identifies the best translation [...]\"

### Insights
β-weights Precision to penalize false positives (critical for filtering). Framework released as software.

## 4. Experimental Setup

### Original Excerpt
```
Data: WMT23MQM (MQM annotations), WMT23DA+SQM. Metrics: COMET*, BLEURT-20, MetricX-23*, xCOMET*, MaTESe*, GEMBA-MQM, etc. [...] GOOD: MQM ≥ -4 (no Major errors, ≤4 Minor); PERFECT ≥ -1.
```

### Summary
ZH→EN focus (others in Appendix). 15 MT systems. Thresholds: max F on test/dev sets.

### Insights
MQM weighting: Major(-25/-5), Minor(-1/-0.1). DA+SQM as human baseline.

## 5. Results

### Key Findings (Table 1 Excerpt)
| Metric | GOOD/BAD F<sub>β</sub> | PERFECT/OTHER F<sub>β</sub> | RRP |
|--------|-------------------------|-----------------------------|-----|
| GEMBA-MQM | 81.59 | 67.14 | 42.58% |
| xCOMET-QE-ENSEMBLE | 81.40 | 67.73 | 41.40% |
| MetricX-23-QE-XL (ref-free, open) | 79.64 | 68.10 | 36.09% |
| DA+SQM (human) | 75.18 | 56.06 | 32.99% |

![Table 1](paper_images/cropped_table1.png)  
![Threshold Variability (Fig 3)](paper_images/cropped_paper1_fig3.png)

### Summary
Ref-based ≥ ref-free overall; MetricX-23-QE-XL top open ref-free. Thresholds unstable across langs/datasets. False positives: ~3 extra Minor errors avg.

### Insights
**Recommendations**:
- **Filtering**: MetricX-23-QE-XL (ref-free).
- **Re-ranking**: Ref-based + MBR decoding.
DA+SQM underperforms autometrics, questioning guidelines.

## Discussion & Future Work
- Threshold instability: Aggregate large annotated sets.
- Extend proxies: RL rewards, QE.
- Robustness: Cross-domain, low-resource langs.

**Citation**:  
Perrella, S., et al. (2024). Beyond Correlation: Interpretable Evaluation of MT Metrics. arXiv:2410.05183.

---

*For full details, consult the paper. Contributions/feedback welcome via Issues/PRs.*