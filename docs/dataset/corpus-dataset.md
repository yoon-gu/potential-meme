# Corpus Dataset

코퍼스 데이터셋은 대규모 텍스트 모음으로, 언어 모델의 사전 학습 및 지속적 사전 학습에 사용됩니다.

## 코퍼스 데이터셋 개요

코퍼스 데이터셋은 다음과 같은 특징을 가집니다:

- 대규모 텍스트 데이터 (일반적으로 수십 GB 이상)
- 다양한 도메인과 주제 포함
- 최소한의 전처리 및 필터링 적용
- 언어 모델의 기본 지식 형성에 중요

## 지원되는 코퍼스 유형

Potential Meme는 다음과 같은 코퍼스 유형을 지원합니다:

1. **일반 텍스트 코퍼스**: 웹 크롤링, 위키피디아, 뉴스 등에서 수집된 일반 텍스트
2. **도메인 특화 코퍼스**: 의학, 법률, 금융 등 특정 도메인에 특화된 텍스트
3. **코드 코퍼스**: 프로그래밍 언어 코드 모음
4. **다국어 코퍼스**: 여러 언어로 된 텍스트 모음

## 코퍼스 데이터 형식

코퍼스 데이터는 일반적으로 다음 형식 중 하나로 저장됩니다:

- 일반 텍스트 파일 (`.txt`)
- JSON Lines 형식 (`.jsonl`)
- Parquet 파일 (`.parquet`)
- HDF5 파일 (`.h5`)

## 코퍼스 데이터 준비

### 데이터 수집

```python
from potential_meme.dataset import CorpusCollector

# 웹에서 데이터 수집
collector = CorpusCollector()
corpus = collector.collect_from_web(urls=["https://example.com"])

# 로컬 파일에서 데이터 수집
corpus = collector.collect_from_files(paths=["data/texts/"])
```

### 데이터 전처리

```python
from potential_meme.dataset import CorpusProcessor

processor = CorpusProcessor()

# 기본 전처리 적용
processed_corpus = processor.process(corpus)

# 사용자 정의 전처리 적용
def custom_filter(text):
    return len(text.split()) > 50  # 50단어 이상인 텍스트만 유지

processed_corpus = processor.process(corpus, filters=[custom_filter])
```

### 데이터 저장

```python
from potential_meme.dataset import CorpusExporter

exporter = CorpusExporter()

# 다양한 형식으로 저장
exporter.export_to_text(processed_corpus, "output/corpus.txt")
exporter.export_to_jsonl(processed_corpus, "output/corpus.jsonl")
exporter.export_to_parquet(processed_corpus, "output/corpus.parquet")
```

## 코퍼스 품질 평가

코퍼스 데이터의 품질을 평가하는 방법:

```python
from potential_meme.dataset import CorpusEvaluator

evaluator = CorpusEvaluator()
metrics = evaluator.evaluate(processed_corpus)

print(f"총 텍스트 수: {metrics['total_texts']}")
print(f"총 단어 수: {metrics['total_words']}")
print(f"평균 텍스트 길이: {metrics['avg_text_length']}")
print(f"언어 분포: {metrics['language_distribution']}")
```

## 대규모 코퍼스 처리 팁

대규모 코퍼스를 효율적으로 처리하기 위한 팁:

1. **스트리밍 처리**: 전체 데이터를 메모리에 로드하지 않고 스트리밍 방식으로 처리
2. **분산 처리**: 여러 머신에서 병렬로 데이터 처리
3. **증분 처리**: 데이터를 작은 배치로 나누어 순차적으로 처리
4. **효율적인 저장 형식 사용**: Parquet과 같은 컬럼 기반 형식 사용

## 사용 가능한 공개 코퍼스

| 코퍼스명 | 크기 | 언어 | 도메인 | 라이센스 |
|---------|-----|------|-------|---------|
| C4 | 800GB | 영어 | 일반 | 오픈 소스 |
| OSCAR | 1.5TB | 다국어 | 일반 | CC0 |
| The Pile | 825GB | 영어 | 다양 | 혼합 |
| RedPajama | 1.2TB | 다국어 | 다양 | 오픈 소스 |

## 다음 단계

코퍼스 데이터셋을 준비한 후에는 [Instruction Dataset](instruction-dataset.md)을 사용하여 모델을 지시 튜닝할 수 있습니다.
