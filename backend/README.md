# Backend — FastAPI API Gateway

메인 API 게이트웨이. 프론트엔드 요청을 처리하고, 각 AI 마이크로서비스를 오케스트레이션하며, Supabase DB를 관리한다.

## Tech Stack

- **Framework**: FastAPI (Python)
- **Database**: Supabase (PostgreSQL)
- **Deployment**: AWS EC2
- **Auth**: Supabase Auth

## 주요 역할

| 역할                  | 설명                                            |
| --------------------- | ----------------------------------------------- |
| API Gateway           | 프론트엔드 요청 라우팅 및 응답 조합             |
| 캠페인 CRUD           | 캠페인 생성, 조회, 수정, 삭제                   |
| 서비스 오케스트레이션 | ai-content, ai-persona, ai-seo 서비스 호출 조율 |
| 데이터 저장           | 캠페인, 콘텐츠, 성과 데이터를 Supabase에 저장   |
| 인증/인가             | Supabase Auth 기반 사용자 관리                  |

## Setup

```bash
cd backend

# 가상 환경 생성
conda create -n som-backend python=3.11 -y
conda activate som-backend

# 의존성 설치
uv pip install -r requirements.txt

# 환경 변수 설정
cp .env.example .env
# .env 파일에 Supabase 키, 서비스 URL 등 설정

# 개발 서버 실행
python -m uvicorn app.main:app --reload --port 8000
```

## Environment Variables

```env
# Supabase
SUPABASE_URL=
SUPABASE_SERVICE_KEY=

# 마이크로서비스 URL
AI_CONTENT_SERVICE_URL=http://localhost:8001
AI_PERSONA_SERVICE_URL=http://localhost:8002
AI_SEO_SERVICE_URL=http://localhost:8003
DATA_COLLECTOR_SERVICE_URL=http://localhost:8004
```

## API Endpoints (예시)

```
POST   /api/v1/campaigns           # 캠페인 생성
GET    /api/v1/campaigns/{id}      # 캠페인 조회
POST   /api/v1/campaigns/{id}/generate   # 콘텐츠 생성 요청
GET    /api/v1/campaigns/{id}/contents   # 생성된 콘텐츠 조회
GET    /api/v1/campaigns/{id}/persona    # 페르소나 평가 결과 조회
GET    /api/v1/campaigns/{id}/analytics  # 성과 데이터 조회
```

## Deployment

AWS EC2에 Docker 컨테이너로 배포. `infra/` 폴더의 docker-compose 참고.
