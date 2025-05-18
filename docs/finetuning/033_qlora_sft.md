# QLoRA SFT 파인튜닝

## 1. 알고리즘 설명

QLoRA SFT는 QLoRA(4비트 양자화)와 SFT(Supervised Fine-Tuning)를 결합하여, 저사양 GPU 환경에서도 대형 언어모델을 효율적으로 지도학습 파인튜닝하는 방법입니다.

## 2. 파라미터 설명

| 파라미터 | 설명 | 일반적인 값 |
|-----------|------|------------|
| r | 저랭크 행렬의 랭크 | 4, 8, 16 |
| alpha | LoRA scaling factor | 16, 32 |
| quantization | 양자화 비트 | 4 |
| double_quant | 2단계 양자화 사용 여부 | True/False |
| learning_rate | 학습률 | 1e-4, 5e-5 |
| batch_size | 배치 크기 | 8, 16, 32 |

## 3. 주요 모델에 대한 GPU 사양

| 모델명 | 모델 크기 | 최소 GPU 사양 | 권장 GPU 사양 |
|--------|-----------|--------------|--------------|
| Llama-7B | 7B | VRAM 8GB (2080) | VRAM 16GB (3090) |
| MPT-7B | 7B | VRAM 8GB (2080) | VRAM 16GB (3090) |
| Vicuna-7B | 7B | VRAM 8GB (2080) | VRAM 16GB (3090) |

## 4. 핸즈온 Example

[이 섹션에는 실제 파인튜닝에 사용할 수 있는 코드 예제 또는 실습 예시를 추가합니다.]
