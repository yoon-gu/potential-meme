# DoRA Tuning 파인튜닝

## 1. 알고리즘 설명

DoRA(Directional and Rank-One Adaptation)는 LoRA에서 발전된 기법으로, 방향성과 랭크-1 행렬을 활용해 더 적은 파라미터로 효율적으로 파인튜닝하는 방법입니다. 메모리와 연산량을 줄이면서도 성능 저하를 최소화합니다.

## 2. 파라미터 설명

| 파라미터 | 설명 | 일반적인 값 |
|-----------|------|------------|
| rank | 랭크-1 행렬의 랭크 | 1 |
| direction | 방향성 적용 여부 | True |
| learning_rate | 학습률 | 1e-4, 5e-5 |

## 3. 주요 모델에 대한 GPU 사양

| 모델명 | 모델 크기 | 최소 GPU 사양 | 권장 GPU 사양 |
|--------|-----------|--------------|--------------|
| Llama-7B | 7B | VRAM 8GB (2080) | VRAM 16GB (3090) |
| GPT-2 | 1.5B | VRAM 4GB (2060) | VRAM 8GB (2080) |
| BERT-base | 110M | VRAM 4GB (2060) | VRAM 8GB (2080) |

## 4. 핸즈온 Example

[이 섹션에는 실제 파인튜닝에 사용할 수 있는 코드 예제 또는 실습 예시를 추가합니다.]
