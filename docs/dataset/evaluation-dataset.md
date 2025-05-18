# Evaluation Dataset

평가 데이터셋은 언어 모델의 성능을 객관적으로 평가하기 위해 사용되는 데이터셋입니다.

## 평가 데이터셋 개요

평가 데이터셋은 다음과 같은 특징을 가집니다:

- 모델 성능을 측정하기 위한 벤치마크 역할
- 다양한 작업과 도메인을 포함
- 명확한 평가 기준과 메트릭 제공
- 모델 간 공정한 비교를 위한 표준화된 형식

## 평가 데이터셋 유형

Potential Meme는 다음과 같은 평가 데이터셋 유형을 지원합니다:

1. **일반 능력 평가**: 언어 이해, 추론, 지식 등 기본 능력 평가
2. **특수 작업 평가**: 번역, 요약, 코드 생성 등 특정 작업 성능 평가
3. **도메인 특화 평가**: 의학, 법률, 금융 등 특정 도메인 지식 평가
4. **안전성 평가**: 모델의 안전성, 편향성, 유해성 평가

## 평가 데이터셋 구조

일반적인 평가 데이터셋의 구조:

```json
{
  "id": "math-001",
  "question": "다음 방정식을 풀어주세요: 2x + 5 = 15",
  "reference_answer": "x = 5",
  "category": "mathematics",
  "difficulty": "easy",
  "evaluation_criteria": {
    "correctness": "정답 여부",
    "explanation": "풀이 과정의 명확성"
  },
  "metadata": {
    "source": "수학 교과서",
    "tags": ["algebra", "linear-equation"]
  }
}
```

## 평가 데이터셋 생성

### 수동 생성

```python
from potential_meme.dataset import EvaluationDataset

# 빈 평가 데이터셋 생성
eval_dataset = EvaluationDataset()

# 수동으로 평가 항목 추가
eval_dataset.add_item(
    question="다음 문장의 감정을 분석해주세요: '오늘은 정말 기분 좋은 날이다.'",
    reference_answer="긍정적",
    category="sentiment-analysis"
)

# 데이터셋 저장
eval_dataset.save("output/manual_evaluation.jsonl")
```

### 기존 데이터셋 변환

```python
from potential_meme.dataset import DatasetConverter

# 기존 데이터셋을 평가 형식으로 변환
converter = DatasetConverter()
eval_dataset = converter.convert_to_evaluation(
    source_dataset="data/squad.json",
    format="qa",
    add_metrics=["exact_match", "f1_score"]
)

eval_dataset.save("output/converted_evaluation.jsonl")
```

## 평가 메트릭

### 일반적인 평가 메트릭

- **정확도(Accuracy)**: 정답 비율
- **F1 점수**: 정밀도와 재현율의 조화 평균
- **BLEU/ROUGE**: 텍스트 생성 품질 평가
- **정확 일치(Exact Match)**: 참조 답변과 정확히 일치하는 비율

### 사용자 정의 메트릭

```python
from potential_meme.evaluation import CustomMetric

# 사용자 정의 메트릭 정의
def semantic_similarity(prediction, reference):
    # 의미적 유사도 계산 로직
    return similarity_score

# 메트릭 등록
custom_metric = CustomMetric(
    name="semantic_similarity",
    function=semantic_similarity,
    higher_is_better=True
)

# 평가에 메트릭 적용
from potential_meme.evaluation import Evaluator

evaluator = Evaluator()
evaluator.add_metric(custom_metric)
results = evaluator.evaluate(model="llama3-8b", dataset=eval_dataset)
```

## 평가 실행

```python
from potential_meme.evaluation import Evaluator

# 평가기 초기화
evaluator = Evaluator()

# 단일 모델 평가
results = evaluator.evaluate(
    model="llama3-8b",
    dataset=eval_dataset,
    metrics=["accuracy", "f1_score"]
)

# 여러 모델 비교 평가
comparison = evaluator.compare(
    models=["llama3-8b", "mistral-7b", "gemma-7b"],
    dataset=eval_dataset,
    metrics=["accuracy", "f1_score"]
)

# 결과 시각화
evaluator.visualize(comparison, output_file="model_comparison.png")
```

## 사용 가능한 공개 평가 데이터셋

| 데이터셋명 | 크기 | 언어 | 평가 영역 | 라이센스 |
|-----------|-----|------|---------|---------|
| MMLU | 15K | 영어 | 다양한 지식 | MIT |
| HumanEval | 164 | 영어 | 코드 생성 | MIT |
| HELM | 42 작업 | 다국어 | 종합 평가 | Apache 2.0 |
| MT-Bench | 80 | 영어 | 대화 능력 | MIT |
| KoBEST | 5K | 한국어 | 다양한 NLP 작업 | CC BY-SA 4.0 |

## 평가 결과 해석

```python
# 평가 결과 분석
analysis = evaluator.analyze_results(results)

print(f"전체 점수: {analysis['overall_score']}")
print(f"강점 카테고리: {analysis['strengths']}")
print(f"약점 카테고리: {analysis['weaknesses']}")
print(f"개선 제안: {analysis['improvement_suggestions']}")
```

## 평가 모범 사례

1. **테스트 데이터 분리**: 훈련에 사용된 데이터와 평가 데이터를 엄격히 분리
2. **다양한 메트릭 사용**: 단일 메트릭에 의존하지 않고 여러 측면 평가
3. **정기적인 평가**: 모델 개발 과정에서 정기적으로 평가 실행
4. **공정한 비교**: 모델 간 비교 시 동일한 조건과 환경 유지

## 다음 단계

평가 데이터셋을 활용하여 모델의 성능을 측정한 후, [Model Distillation](../model-distillation.md) 또는 [Finetuning](../finetuning/continual-pretraining.md) 과정을 통해 모델을 개선할 수 있습니다.
