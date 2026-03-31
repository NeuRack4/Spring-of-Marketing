# AI Content Service — 콘텐츠 생성 서비스

사용자 캠페인 정보를 받아 블로그, 인스타그램, 랜딩페이지 등 마케팅 콘텐츠를 자동 생성하는 서비스.

## Tech Stack

- **Framework**: FastAPI (Python)
- **LLM**: OpenAI API, Claude API
- **Deployment**: AWS EC2

## 주요 기능

| 기능                 | 설명                                  | 우선순위 |
| -------------------- | ------------------------------------- | -------- |
| 블로그 콘텐츠 생성   | SEO 최적화된 블로그 글 자동 작성      | P0       |
| SNS 콘텐츠 생성      | 인스타그램, 페이스북 등 SNS 광고 카피 | P0       |
| 랜딩페이지 카피      | 헤드라인, 서브 카피, CTA 문구 생성    | P0       |
| 검색 광고 카피       | 구글/네이버 검색 광고 문구 생성       | P1       |
| A/B 테스트 버전 생성 | 동일 콘텐츠의 복수 버전 생성          | P2       |

## Setup

```bash
cd ai-content

# 가상 환경 생성
conda create -n som-ai-content python=3.11 -y
conda activate som-ai-content

# 의존성 설치
uv pip install -r requirements.txt

# 환경 변수 설정
cp .env.example .env

# 개발 서버 실행
python -m uvicorn app.main:app --reload --port 8001
```

## Environment Variables

```env
OPENAI_API_KEY=
ANTHROPIC_API_KEY=
```

## API Endpoints (예시)

```
POST   /api/v1/generate/blog        # 블로그 콘텐츠 생성
POST   /api/v1/generate/sns         # SNS 콘텐츠 생성
POST   /api/v1/generate/landing     # 랜딩페이지 카피 생성
POST   /api/v1/generate/search-ad   # 검색 광고 카피 생성
```

## 내부 루프 연동

생성된 콘텐츠는 `ai-persona` 서비스로 전달되어 검증을 거친다. 검증 실패 시 피드백을 반영하여 재생성.

```
[ai-content] --생성--> [ai-persona] --검증-->
     ^                                  |
     └──────── 실패 시 재생성 ──────────┘
```
