# Instruction Dataset

지시 데이터셋은 언어 모델을 지시 따르기(instruction following)에 맞게 파인튜닝하는 데 사용되는 데이터셋입니다.

## 지시 데이터셋 개요

지시 데이터셋은 다음과 같은 특징을 가집니다:

- 지시(instruction)와 응답(response) 쌍으로 구성
- 다양한 작업과 도메인을 포함
- 인간의 의도와 요구를 반영
- 모델이 유용하고 안전한 응답을 생성하도록 훈련

## 지시 데이터셋 구조

일반적인 지시 데이터셋의 구조:

```json
{
  "instruction": "다음 영어 문장을 한국어로 번역해주세요: 'The weather is nice today.'",
  "response": "오늘 날씨가 좋네요.",
  "category": "translation",
  "difficulty": "easy",
  "metadata": {
    "source": "manual",
    "language": "ko"
  }
}
```

## 지시 데이터셋 유형

Potential Meme는 다음과 같은 지시 데이터셋 유형을 지원합니다:

1. **일반 지시**: 일상적인 질문, 요청, 대화
2. **특수 작업 지시**: 번역, 요약, 코드 생성 등 특정 작업에 대한 지시
3. **도메인 특화 지시**: 의학, 법률, 금융 등 특정 도메인에 관한 지시
4. **안전 지시**: 모델의 안전성과 정직성을 향상시키기 위한 지시

## 지시 데이터셋 생성

### 수동 생성

```python
from potential_meme.dataset import InstructionDataset

# 빈 데이터셋 생성
dataset = InstructionDataset()

# 수동으로 예제 추가
dataset.add_example(
    instruction="다음 수학 문제를 풀어주세요: 5 + 7 = ?",
    response="5 + 7 = 12입니다.",
    category="math"
)

# 데이터셋 저장
dataset.save("output/manual_instructions.jsonl")
```

### 자동 생성

```python
from potential_meme.dataset import InstructionGenerator

# 지시 생성기 초기화
generator = InstructionGenerator(model="gpt-4")

# 특정 주제에 대한 지시 생성
math_instructions = generator.generate(
    topic="mathematics",
    count=100,
    difficulty_range=(1, 5)
)

# 생성된 지시를 데이터셋에 추가
dataset = InstructionDataset()
dataset.add_examples(math_instructions)
dataset.save("output/generated_math_instructions.jsonl")
```

### 기존 데이터셋 변환

```python
from potential_meme.dataset import DatasetConverter

# 질의응답 데이터셋을 지시 형식으로 변환
converter = DatasetConverter()
instruction_dataset = converter.qa_to_instruction(
    qa_dataset="data/squad.json",
    instruction_template="다음 질문에 답해주세요: {question}"
)

instruction_dataset.save("output/converted_instructions.jsonl")
```

## 지시 데이터셋 품질 향상

### 데이터 필터링

```python
from potential_meme.dataset import InstructionFilter

# 필터 초기화
filter = InstructionFilter()

# 품질이 낮은 지시 필터링
filtered_dataset = filter.apply(
    dataset,
    min_instruction_length=10,
    min_response_length=20,
    remove_duplicates=True
)
```

### 데이터 증강

```python
from potential_meme.dataset import InstructionAugmenter

# 증강기 초기화
augmenter = InstructionAugmenter()

# 데이터 증강 적용
augmented_dataset = augmenter.apply(
    dataset,
    paraphrase=True,
    translate_and_back=True,
    augmentation_factor=2
)
```

## 사용 가능한 공개 지시 데이터셋

| 데이터셋명 | 크기 | 언어 | 특징 | 라이센스 |
|-----------|-----|------|------|---------|
| Alpaca | 52K | 영어 | 일반 지시 | CC BY-NC 4.0 |
| Dolly | 15K | 영어 | 다양한 작업 | CC BY-SA 3.0 |
| OpenAssistant | 161K | 다국어 | 대화형 지시 | Apache 2.0 |
| FLAN | 1.8M | 다국어 | 다양한 NLP 작업 | Apache 2.0 |

## 지시 데이터셋 평가

지시 데이터셋의 품질을 평가하는 방법:

```python
from potential_meme.dataset import InstructionEvaluator

evaluator = InstructionEvaluator()
metrics = evaluator.evaluate(dataset)

print(f"총 예제 수: {metrics['total_examples']}")
print(f"평균 지시 길이: {metrics['avg_instruction_length']}")
print(f"평균 응답 길이: {metrics['avg_response_length']}")
print(f"카테고리 분포: {metrics['category_distribution']}")
print(f"다양성 점수: {metrics['diversity_score']}")
```

## 다음 단계

지시 데이터셋을 준비한 후에는 [Preference Dataset](preference-dataset.md)을 사용하여 모델의 출력 품질을 더욱 향상시킬 수 있습니다.
