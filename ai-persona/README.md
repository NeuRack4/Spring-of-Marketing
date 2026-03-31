# AI Persona Service — 페르소나 검증/시뮬레이션 서비스

LLM 페르소나 기반으로 생성된 콘텐츠의 타겟 관점 품질을 평가하고, 시뮬레이션 결과를 제공하는 서비스.

## Tech Stack

- **Framework**: FastAPI (Python)
- **LLM**: OpenAI API, Claude API
- **Vector DB**: ChromaDB (페르소나 데이터 임베딩 저장)
- **Deployment**: AWS EC2

## 주요 기능

| 기능           | 설명                                  | 우선순위 |
| -------------- | ------------------------------------- | -------- |
| 페르소나 생성  | 8개 차원 기반 타겟 고객 페르소나 생성 | P0       |
| 콘텐츠 검증    | 생성 콘텐츠의 페르소나 관점 품질 평가 | P0       |
| 세그먼트 분석  | 연령대별, 특성별 반응 시뮬레이션      | P0       |
| 저항 요인 분석 | 주요 저항 요인 식별 및 해결책 제시    | P0       |
| 자기 개선 루프 | 성과 데이터 기반 페르소나 자동 고도화 | P2       |

## 페르소나 8개 차원

인구 통계, 경제적 특성, 직업/커리어, 심리적 특성, 소비 행동, 디지털/미디어 행동, 가치관, 관심사/니즈

## Setup

```bash
cd ai-persona

# 가상 환경 생성
conda create -n som-ai-persona python=3.11 -y
conda activate som-ai-persona

# 의존성 설치
uv pip install -r requirements.txt

# 환경 변수 설정
cp .env.example .env

# 개발 서버 실행
python -m uvicorn app.main:app --reload --port 8002
```

## Environment Variables

```env
OPENAI_API_KEY=
ANTHROPIC_API_KEY=
CHROMA_HOST=localhost
CHROMA_PORT=8010
```

## API Endpoints (예시)

```
POST   /api/v1/persona/generate          # 페르소나 생성
POST   /api/v1/persona/validate          # 콘텐츠 검증 (통과/실패 + 피드백)
GET    /api/v1/persona/{id}/segments     # 세그먼트별 분석 결과
GET    /api/v1/persona/{id}/resistances  # 저항 요인 분석
POST   /api/v1/persona/{id}/improve      # 성과 데이터 기반 고도화
```

## ChromaDB 사용

페르소나 속성 데이터를 벡터화하여 ChromaDB에 저장. 유사 페르소나 검색, 과거 캠페인 성과 매칭에 활용.

```
[캠페인 타겟 정보] --> [임베딩] --> [ChromaDB 유사 검색]
                                        |
                                  유사 페르소나 + 과거 성과 데이터 활용
```
