# Frontend — Next.js Web Client

캠페인 입력 폼, AI 콘텐츠 미리보기, 대시보드를 제공하는 웹 클라이언트.

## Tech Stack

- **Framework**: Next.js (App Router)
- **Deployment**: Vercel
- **Styling**: 추후 결정 (Tailwind CSS 권장)
- **State Management**: 추후 결정

## 주요 화면

| 화면               | 설명                                        | 우선순위 |
| ------------------ | ------------------------------------------- | -------- |
| 캠페인 입력 폼     | 기본 정보, 제품, 타깃, 채널, 예산 입력      | P0       |
| AI 콘텐츠 화면     | 채널별 탭 UI, 콘텐츠 미리보기, 캠페인 정보  | P0       |
| 페르소나 평가 화면 | 시뮬레이션 규모, 세그먼트별 분석, 저항 요인 | P0       |
| 대시보드           | 성과 통계 카드, 채널별 데이터 시각화        | P0       |

## Setup

```bash
cd frontend

# 의존성 설치
npm install

# 환경 변수 설정
cp .env.example .env.local
# .env.local 파일에 API URL 등 설정

# 개발 서버 실행
npm run dev
# http://localhost:3000
```

## Environment Variables

```env
NEXT_PUBLIC_API_URL=http://localhost:8000   # Backend API 주소
NEXT_PUBLIC_SUPABASE_URL=                   # Supabase 프로젝트 URL
NEXT_PUBLIC_SUPABASE_ANON_KEY=              # Supabase 공개 키
```

## Scripts

```bash
npm run dev       # 개발 서버 (localhost:3000)
npm run build     # 프로덕션 빌드
npm run start     # 프로덕션 서버
npm run lint      # ESLint 검사
```

## Deployment

Vercel에 자동 배포. `main` 브랜치 push 시 자동 트리거.
