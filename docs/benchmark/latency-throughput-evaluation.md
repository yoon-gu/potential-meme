# Latency/Throughput Evaluation

지연 시간(Latency)과 처리량(Throughput) 평가는 모델의 실제 응답 속도와 초당 처리 가능한 요청 수를 측정하는 과정입니다.

## 주요 지표
- Latency(평균/최대 응답 시간)
- Throughput(초당 처리 요청 수)
- 메모리 사용량

## 평가 방법
- 다양한 입력 길이/배치 크기에서 측정
- 실제 서비스 환경에서 벤치마크

## 예시 코드

```python
import time
from transformers import AutoModelForCausalLM, AutoTokenizer

model = AutoModelForCausalLM.from_pretrained('gpt2')
tokenizer = AutoTokenizer.from_pretrained('gpt2')

prompt = "오늘 날씨 어때?"
inputs = tokenizer(prompt, return_tensors="pt")

start = time.time()
_ = model.generate(**inputs, max_length=50)
end = time.time()

print(f"Latency: {end - start:.3f} seconds")
```
