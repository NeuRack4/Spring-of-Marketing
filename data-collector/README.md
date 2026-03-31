# Data Collector Service — 성과 데이터 수집 서비스

배포된 콘텐츠의 성과 데이터(CTR, 전환율 등)를 수집하고, 경쟁사 분석 데이터를 크롤링하는 서비스.

## Tech Stack

- **Framework**: FastAPI (Python)
- **Database**: Supabase (수집 데이터 저장)
- **Deployment**: AWS EC2

## 주요 기능

| 기능               | 설명                                      | 우선순위 |
| ------------------ | ----------------------------------------- | -------- |
| 성과 데이터 수집   | CTR, 전환율, 노출수 등 플랫폼별 성과 수집 | P1       |
| 데이터 정규화      | 플랫폼별 상이한 데이터 포맷 통일          | P1       |
| 경쟁사 데이터 수집 | 경쟁사 마케팅 콘텐츠 크롤링/분석          | P3       |
| 스케줄링           | 주기적 데이터 수집 작업 관리              | P1       |

## Setup

```bash
cd data-collector

# 가상 환경 생성
conda create -n som-data-collector python=3.11 -y
conda activate som-data-collector

# 의존성 설치
uv pip install -r requirements.txt

# 환경 변수 설정
cp .env.example .env

# 개발 서버 실행
python -m uvicorn app.main:app --reload --port 8004
```

## Environment Variables

```env
# Supabase
SUPABASE_URL=
SUPABASE_SERVICE_KEY=

# 플랫폼 API 키 (수집 대상)
NAVER_API_KEY=
GOOGLE_ADS_API_KEY=
META_API_KEY=
```

## API Endpoints (예시)

```
POST   /api/v1/collect/trigger           # 수동 수집 트리거
GET    /api/v1/collect/status            # 수집 상태 조회
GET    /api/v1/analytics/{campaign_id}   # 캠페인별 성과 데이터
POST   /api/v1/competitor/analyze        # 경쟁사 분석 요청
```

## 외부 루프 연동

수집된 성과 데이터는 `ai-persona` 서비스의 자기 개선 루프에 활용.

```
[플랫폼 배포] --> [data-collector] --> [Supabase 저장]
                                           |
                              [ai-persona 개선 루프에 반영]
```
