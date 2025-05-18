# Preference Dataset

선호도 데이터셋은 언어 모델의 출력 품질을 향상시키기 위한 인간 선호도 정보를 포함하는 데이터셋입니다.

## 선호도 데이터셋 개요

선호도 데이터셋은 다음과 같은 특징을 가집니다:

- 동일한 입력에 대한 여러 모델 응답 포함
- 인간 평가자의 선호도 정보 포함
- 모델의 출력 품질, 유용성, 안전성 향상에 사용
- RLHF(Reinforcement Learning from Human Feedback)와 DPO(Direct Preference Optimization)와 같은 기법에 활용

## 선호도 데이터셋 구조

일반적인 선호도 데이터셋의 구조:

```json
{
  "instruction": "기후 변화의 주요 원인과 해결책에 대해 설명해주세요.",
  "response_a": "기후 변화의 주요 원인은...",
  "response_b": "기후 변화는 주로 인간 활동에 의해...",
  "preference": "b",  // 응답 B가 더 선호됨
  "score_a": 3,       // 1-5 척도에서의 점수
  "score_b": 5,
  "reason": "응답 B가 더 명확하고 구체적인 정보를 제공합니다."
}
```

## 선호도 데이터 수집 방법

### 인간 평가자 활용

```python
from potential_meme.dataset import PreferenceCollector

# 선호도 수집기 초기화
collector = PreferenceCollector()

# 인간 평가자로부터 선호도 수집
preferences = collector.collect_from_humans(
    instructions=instruction_dataset,
    model_a="llama3-8b",
    model_b="mistral-7b",
    evaluators=["evaluator1@example.com", "evaluator2@example.com"],
    criteria=["helpfulness", "accuracy", "safety"]
)

# 수집된 선호도 저장
preferences.save("output/human_preferences.jsonl")
```

### 모델 기반 선호도 생성

```python
from potential_meme.dataset import ModelPreferenceGenerator

# 모델 기반 선호도 생성기 초기화
generator = ModelPreferenceGenerator(judge_model="gpt-4")

# 모델을 사용하여 선호도 생성
model_preferences = generator.generate(
    instructions=instruction_dataset,
    model_a="llama3-8b",
    model_b="mistral-7b",
    criteria=["helpfulness", "accuracy", "safety"],
    samples_count=1000
)

# 생성된 선호도 저장
model_preferences.save("output/model_preferences.jsonl")
```

## 선호도 데이터 품질 관리

### 평가자 간 일치도 확인

```python
from potential_meme.dataset import PreferenceAnalyzer

analyzer = PreferenceAnalyzer()
agreement = analyzer.calculate_agreement(preferences)

print(f"평가자 간 일치도 (Cohen's Kappa): {agreement['cohens_kappa']}")
print(f"평가자 간 일치율: {agreement['agreement_rate']}%")
```

### 편향 감지 및 완화

```python
# 선호도 데이터에서 편향 감지
bias = analyzer.detect_bias(preferences)

print(f"모델 편향 점수: {bias['model_bias']}")
print(f"평가자 편향 점수: {bias['evaluator_bias']}")
print(f"주제 편향 점수: {bias['topic_bias']}")

# 편향 완화 적용
debiased_preferences = analyzer.debias(preferences)
```

## 선호도 데이터셋 분석

```python
# 선호도 데이터셋 통계 분석
stats = analyzer.analyze(preferences)

print(f"총 비교 쌍: {stats['total_pairs']}")
print(f"모델 A 선호 비율: {stats['model_a_preferred']}%")
print(f"모델 B 선호 비율: {stats['model_b_preferred']}%")
print(f"동점 비율: {stats['ties']}%")
print(f"주제별 선호도: {stats['topic_preferences']}")
```

## 선호도 데이터셋 활용

### RLHF(Reinforcement Learning from Human Feedback)

```python
from potential_meme.training import RLHFTrainer

# RLHF 트레이너 초기화
trainer = RLHFTrainer(
    base_model="llama3-8b",
    reward_model="reward-model-v1"
)

# 선호도 데이터로 보상 모델 학습
trainer.train_reward_model(preferences)

# RLHF 학습 실행
trainer.train_policy(
    max_steps=10000,
    learning_rate=1e-5,
    kl_coef=0.1
)
```

### DPO(Direct Preference Optimization)

```python
from potential_meme.training import DPOTrainer

# DPO 트레이너 초기화
trainer = DPOTrainer(base_model="llama3-8b")

# DPO 학습 실행
trainer.train(
    preferences=preferences,
    max_steps=5000,
    learning_rate=5e-7,
    beta=0.1
)
```

## 사용 가능한 공개 선호도 데이터셋

| 데이터셋명 | 크기 | 언어 | 특징 | 라이센스 |
|-----------|-----|------|------|---------|
| Anthropic HH | 170K | 영어 | 유해성 관련 선호도 | MIT |
| OpenAI WebGPT | 20K | 영어 | 웹 검색 기반 응답 | MIT |
| Stanford SHP | 385K | 영어 | 인간 선호도 | CC BY-SA 4.0 |
| UltraFeedback | 64K | 영어 | 다양한 품질 기준 | MIT |

## 다음 단계

선호도 데이터셋을 준비한 후에는 [Evaluation Dataset](evaluation-dataset.md)을 사용하여 모델의 성능을 객관적으로 평가할 수 있습니다.
