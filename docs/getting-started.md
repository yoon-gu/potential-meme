# Getting Started

이 가이드는 Potential Meme 프로젝트를 시작하는 데 필요한 기본 정보를 제공합니다.

## 설치 방법

### 요구 사항

- Python 3.8 이상
- pip (최신 버전)
- Git

### 설치 단계

1. 저장소 복제:

```bash
git clone https://github.com/yoon-gu/potential-meme.git
cd potential-meme
```

2. 가상 환경 생성 및 활성화:

```bash
python -m venv .venv
# Windows
.venv\Scripts\activate
# Linux/Mac
source .venv/bin/activate
```

3. 필요한 패키지 설치:

```bash
pip install -r requirements.txt
```

## 프로젝트 구조

```
potential-meme/
├── docs/                # 문서
├── foundation-models/   # 기반 모델 관련 코드
├── dataset/             # 데이터셋 관리 코드
├── finetuning/          # 파인튜닝 관련 코드
├── benchmark/           # 벤치마크 도구
└── utils/               # 유틸리티 함수
```

## 첫 번째 단계

프로젝트를 설치한 후 다음 단계를 따라 시작할 수 있습니다:

1. 기본 모델 카탈로그 살펴보기
2. 샘플 데이터셋 준비하기
3. 간단한 파인튜닝 실행하기
4. 결과 벤치마킹하기

각 단계에 대한 자세한 내용은 해당 섹션에서 확인할 수 있습니다.

## 도움말 및 지원

문제가 발생하거나 질문이 있는 경우 다음 방법으로 도움을 받을 수 있습니다:

- GitHub 이슈 제출
- 프로젝트 문서 참조
- 커뮤니티 포럼 방문

## 다음 단계

기본 설정을 완료한 후에는 [Foundation Models](foundation-models/model-catalog.md) 섹션으로 이동하여 사용 가능한 모델에 대해 알아보세요.
