# 환경 변수(Environment Variables)

이 문서는 프로젝트에서 사용하는 서비스의 API KEY 및 기타 중요한 환경 변수들을 안전하게 관리하는 방법에 대해 안내합니다.

## 환경 변수란?
환경 변수는 서비스의 인증 정보(API KEY, SECRET 등)나 환경에 따라 달라지는 설정 값들을 코드와 분리하여 관리하는 방법입니다. 이를 통해 보안을 강화하고, 코드의 이식성을 높일 수 있습니다.

## 환경 변수 파일 예시

보통 프로젝트 루트 디렉토리에 `.env` 파일을 생성하여 환경 변수를 관리합니다. 예시:

```
OPENAI_API_KEY=your-openai-api-key
GOOGLE_API_KEY=your-google-api-key
AWS_ACCESS_KEY_ID=your-aws-access-key-id
AWS_SECRET_ACCESS_KEY=your-aws-secret-access-key
SLACK_BOT_TOKEN=your-slack-bot-token
```

> **주의:** `.env` 파일은 절대 git 등 버전 관리 시스템에 커밋하지 마세요. `.gitignore`에 반드시 추가해야 합니다.

## 주요 환경 변수 목록

| 변수명                  | 설명                                   |
|------------------------|----------------------------------------|
| `OPENAI_API_KEY`       | OpenAI API를 사용하기 위한 키           |
| `GOOGLE_API_KEY`       | Google 서비스(API) 사용을 위한 키       |
| `AWS_ACCESS_KEY_ID`    | AWS 서비스 접근을 위한 Access Key ID    |
| `AWS_SECRET_ACCESS_KEY`| AWS 서비스 접근을 위한 Secret Access Key|
| `SLACK_BOT_TOKEN`      | Slack 봇 연동을 위한 토큰               |

필요에 따라 추가적인 환경 변수를 정의하여 사용하실 수 있습니다.

## 환경 변수 사용 방법

1. `.env` 파일에 각종 API KEY 및 환경 변수를 추가합니다.
2. 코드에서는 보통 `os.environ`(Python) 또는 `process.env`(Node.js) 등을 통해 환경 변수를 불러옵니다.
3. 환경 변수 값이 노출되지 않도록 주의합니다.

## 참고 사항
- 환경 변수는 각자의 환경에 맞게 직접 입력해야 하며, 공유하거나 공개 저장소에 올리지 않도록 주의하세요.
- 팀원들과 환경 변수 샘플 파일(`.env.example`)을 공유하면 도움이 됩니다.

---

이 문서는 프로젝트에서 사용하는 API KEY 및 환경 변수 관리에 대한 가이드입니다. 추가적으로 필요한 환경 변수가 있다면 이 문서에 업데이트 해주세요.
