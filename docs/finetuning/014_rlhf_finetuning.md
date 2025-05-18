# RLHF(Reinforcement Learning from Human Feedback) 파인튜닝

## 1. 알고리즘 설명

RLHF는 인간의 피드백을 활용해 모델을 강화학습 방식으로 파인튜닝하는 방법입니다. 보상 모델을 학습한 뒤, PPO 등 강화학습 알고리즘으로 언어모델을 최적화합니다.

## 2. 파라미터 설명

| 파라미터 | 설명 | 일반적인 값 |
|-----------|------|------------|
| reward_model | 보상 모델 | BERT, RoBERTa 등 |
| ppo_epochs | PPO 에폭 | 1, 4 |
| learning_rate | 학습률 | 1e-5, 5e-6 |
| batch_size | 배치 크기 | 4, 8 |

## 3. 주요 모델에 대한 GPU 사양

| 모델명 | 모델 크기 | 최소 GPU 사양 | 권장 GPU 사양 |
|--------|-----------|--------------|--------------|
| GPT-2 | 1.5B | VRAM 8GB (2080) | VRAM 16GB (3090) |
| Llama-7B | 7B | VRAM 16GB (3090) | VRAM 24GB (4090) |
| GPT-3 | 175B | VRAM 40GB (A100) | VRAM 80GB (A100) |

## 4. 핸즈온 Example

[이 섹션에는 실제 파인튜닝에 사용할 수 있는 코드 예제 또는 실습 예시를 추가합니다.]
