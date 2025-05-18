# Quality Evaluation

모델의 품질 평가(Quality Evaluation)는 언어모델이 다양한 태스크에서 얼마나 정확하고 유용한 결과를 생성하는지 측정하는 프로세스입니다.

## 평가 항목
- 정답률(Accuracy)
- 일관성(Consistency)
- 창의성(Creativity)
- 유용성(Usefulness)
- 안전성(Safety)

## 평가 방법
- 자동화된 지표(예: BLEU, ROUGE, F1)
- 인간 평가자(Expert/Non-expert) 기반 평가
- 벤치마크 데이터셋 활용

## 예시 코드

```python
from datasets import load_metric

metric = load_metric('bleu')
results = metric.compute(predictions=["오늘 날씨가 좋다."], references=[["오늘 날씨가 좋다."]])
print(results)
```
