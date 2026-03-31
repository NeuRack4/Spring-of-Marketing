# Infra — 인프라 및 배포 설정

Docker, Docker Compose, CI/CD, AWS EC2 배포 관련 설정 파일 모음.

## Tech Stack

- **Container**: Docker, Docker Compose
- **CI/CD**: GitHub Actions
- **Cloud**: AWS EC2 (백엔드 + AI 서비스), Vercel (프론트엔드)
- **Database**: Supabase (managed), ChromaDB (self-hosted on EC2)

## 배포 구조

```
[Vercel]                    [AWS EC2]
   |                            |
frontend (Next.js)         Docker Compose
                                |
                    ┌───────────┼───────────────┐
                    |           |               |
                 backend    ai-content     ai-persona
                    |       ai-seo     data-collector
                    |
                [ChromaDB Container]

[Supabase Cloud] <-- 모든 서비스에서 접근
```

## 파일 구조 (예정)

```
infra/
├── docker/
│   ├── backend.Dockerfile
│   ├── ai-content.Dockerfile
│   ├── ai-persona.Dockerfile
│   ├── ai-seo.Dockerfile
│   └── data-collector.Dockerfile
├── docker-compose.yml          # 로컬 전체 서비스 실행
├── docker-compose.prod.yml     # 프로덕션 설정
├── .github/
│   └── workflows/
│       ├── ci.yml              # 테스트/린트 자동화
│       └── deploy.yml          # EC2 배포 자동화
├── nginx/
│   └── nginx.conf              # 리버스 프록시 설정
└── scripts/
    ├── setup.sh                # 초기 환경 세팅 스크립트
    └── deploy.sh               # 배포 스크립트
```

## Local Development (Docker Compose)

```bash
cd infra

# 전체 서비스 실행
docker-compose up -d

# 특정 서비스만 실행
docker-compose up -d backend ai-content

# 로그 확인
docker-compose logs -f backend

# 전체 중지
docker-compose down
```

## Port Mapping

| 서비스         | 포트 |
| -------------- | ---- |
| frontend       | 3000 |
| backend        | 8000 |
| ai-content     | 8001 |
| ai-persona     | 8002 |
| ai-seo         | 8003 |
| data-collector | 8004 |
| ChromaDB       | 8010 |

## CI/CD Pipeline

```
Push to main → GitHub Actions → Build & Test → Docker Image → Deploy to EC2
                                                    |
                                              Vercel (frontend 자동 배포)
```

## AWS EC2 Setup

```bash
# EC2 인스턴스 접속 후
# Docker, Docker Compose 설치 필요
# 상세 세팅은 scripts/setup.sh 참고
```
