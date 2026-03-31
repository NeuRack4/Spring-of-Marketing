# AI SEO Service — SEO/GEO 최적화 서비스

생성된 콘텐츠의 검색 엔진 최적화(SEO) 및 생성 AI 노출 최적화(GEO)를 수행하는 서비스.

## Tech Stack

- **Framework**: FastAPI (Python)
- **LLM**: OpenAI API, Claude API
- **Deployment**: AWS EC2

## 주요 기능

| 기능              | 설명                                         | 우선순위 |
| ----------------- | -------------------------------------------- | -------- |
| 키워드 분석       | 타겟 키워드 추출 및 경쟁도 분석              | P2       |
| SEO 콘텐츠 최적화 | 메타 태그, 헤딩 구조, 키워드 밀도 최적화     | P2       |
| GEO 최적화        | 생성 AI(ChatGPT, Gemini 등) 검색 노출 최적화 | P2       |
| SEO 점수 평가     | 콘텐츠 SEO 점수 산출 및 개선 제안            | P2       |

## Setup

```bash
cd ai-seo

# 가상 환경 생성
conda create -n som-ai-seo python=3.11 -y
conda activate som-ai-seo

# 의존성 설치
uv pip install -r requirements.txt

# 환경 변수 설정
cp .env.example .env

# 개발 서버 실행
python -m uvicorn app.main:app --reload --port 8003
```

## Environment Variables

```env
OPENAI_API_KEY=
ANTHROPIC_API_KEY=
```

## API Endpoints (예시)

```
POST   /api/v1/seo/analyze          # 키워드 분석
POST   /api/v1/seo/optimize         # SEO 콘텐츠 최적화
POST   /api/v1/geo/optimize         # GEO 최적화
GET    /api/v1/seo/score/{id}       # SEO 점수 조회
```

## Note

P2 우선순위. Week 3 (04/15-04/21)부터 개발 시작 예정.
