# Spring of Marketer — Marketing Automation Agent

> "입력만 하면 마케팅이 완성된다"

제품 정보와 목표를 입력하면 AI가 콘텐츠를 생성 > 검증 > 배포 > 개선하는 풀사이클 마케팅 자동화 에이전트

## Team

| 이름   | 역할  |
| ------ | ----- |
| 김재현 | PM    |
| 송진우 | Data  |
| 장승우 | AI    |
| 이민혜 | BE/FE |

## Tech Stack

| 레이어      | 기술                             |
| ----------- | -------------------------------- |
| Frontend    | Next.js, Vercel                  |
| Backend     | FastAPI, Supabase                |
| AI Services | OpenAI API, Claude API, ChromaDB |
| Infra       | AWS EC2, Docker, GitHub Actions  |

## Architecture

모노레포 + 마이크로서비스 구조. 각 서비스는 독립적으로 배포 가능.

```
spring-of-marketer/
├── frontend/          # Next.js 웹 클라이언트 (Vercel 배포)
├── backend/           # FastAPI 메인 API 게이트웨이 (Supabase 연동)
├── ai-content/        # AI 콘텐츠 생성 서비스 (OpenAI, Claude API)
├── ai-persona/        # AI 페르소나 검증/시뮬레이션 서비스 (ChromaDB)
├── ai-seo/            # SEO/GEO 최적화 서비스
├── data-collector/    # 성과 데이터 수집 서비스 (CTR, 전환율, 크롤링)
├── infra/             # Docker, CI/CD, AWS 인프라 설정
└── docs/              # 프로젝트 문서 (PRD, API 명세 등)
```

## Service Communication

```
[Frontend] <--REST--> [Backend (API Gateway)]
                            |
            ┌───────────────┼───────────────┐
            v               v               v
      [ai-content]    [ai-persona]     [ai-seo]
                            |
                            v
                       [ChromaDB]

      [data-collector] --> [Backend] --> [Supabase]
```

## Quick Start

```bash
# 1. 레포 클론
git clone https://github.com/your-org/spring-of-marketer.git
cd spring-of-marketer

# 2. 각 서비스별 README 참고하여 환경 세팅
# 3. 인프라 세팅 (Docker Compose로 전체 서비스 실행)
cd infra
docker-compose up -d
```

각 서비스의 상세 사용법은 해당 폴더의 README.md를 참고하세요.

## Timeline

| 기간                 | 주요 작업                            |
| -------------------- | ------------------------------------ |
| Week 1 (04/01-04/07) | 인프라 구축, 데이터 수집             |
| Week 2 (04/08-04/14) | 대시보드 제작, AI 콘텐츠 파이프라인  |
| Week 3 (04/15-04/21) | SEO/GEO 최적화, 페르소나 정확도 향상 |
| Week 4 (04/22-04/28) | 자기 개선 루프 완성                  |
| Week 5 (04/29-05/07) | 통합 테스트, 버그 수정               |
| **발표 (05/11)**     | **최종 발표**                        |
