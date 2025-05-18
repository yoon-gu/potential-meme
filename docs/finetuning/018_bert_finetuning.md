# BERT 파인튜닝

## 1. 알고리즘 설명

BERT(Bidirectional Encoder Representations from Transformers)는 양방향 트랜스포머 인코더 기반의 사전학습 언어모델로, 분류, 질의응답, NER 등 다양한 태스크에 파인튜닝할 수 있습니다.

## 2. 파라미터 설명

| 파라미터 | 설명 | 일반적인 값 |
|-----------|------|------------|
| learning_rate | 학습률 | 2e-5, 5e-5 |
| batch_size | 배치 크기 | 8, 16, 32 |
| max_seq_length | 최대 시퀀스 길이 | 128, 256, 512 |
| epochs | 학습 에폭 | 3, 5 |

## 3. 주요 모델에 대한 GPU 사양

| 모델명 | 모델 크기 | 최소 GPU 사양 | 권장 GPU 사양 |
|--------|-----------|--------------|--------------|
| BERT-base | 110M | VRAM 4GB (2060) | VRAM 8GB (2080) |
| BERT-large | 340M | VRAM 8GB (2080) | VRAM 16GB (3090) |
| KoBERT | 110M | VRAM 4GB (2060) | VRAM 8GB (2080) |

## 4. 핸즈온 Example

[이 섹션에는 실제 파인튜닝에 사용할 수 있는 코드 예제 또는 실습 예시를 추가합니다.]
