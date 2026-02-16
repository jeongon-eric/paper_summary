# COLT: Lightweight Multi-LLM Collaboration through Shared MCTS Reasoning

**Paper ID:** arXiv:2602.01935

## Authors
- Albert Shyuan Tang, Carey Priebe, Qin (Luna) Lu, Hadi Esmaeilzadeh (Johns Hopkins University)

## Abstract
COLT (Collaborative Optimization via Lightweight Threads)를 제안합니다. MCTS 추론을 공유하여 다중 LLM 협력을 가볍게 구현합니다. LLMCompiler 대비 대기 시간 53% 단축, 비용 87% 절감합니다.

## Method

### MCTS 기반 협력
1. 현재 모델이 추론 트리 생성
2. 협력 모델이Arm 선택
3. 공유 KV 캐시를 통한 정보 통신

## Results

### Table 1: Performance Comparison

| Method | Latency (s) | Cost Reduction | Quality |
|--------|-------------|----------------|---------|
| LLMCompiler | baseline | baseline | baseline |
| **COLT** | **-53%** | **-87%** | **동일 이상** |

## Key Figures

### Figure 1: COLT Overview
![Overview](figs/overview.png)
- MCTS 기반 협력 메커니즘

### Figure 2: GPT-5.2 Results
![GPT5](figs/colt-gpt5.2-combined.png)
- GPT-5.2 평가 결과

### Figure 3: Llama 3 70B Results
![Llama](figs/colt-llama70-combined.png)
- Llama 3 70B 평가 결과

## Main Contributions
1. MCTS 기반 가벼운 다중 LLM 협력
2. 공유 KV 캐시를 통한 효율적 통신
3. 실제 컴파일러 최적화 적용
