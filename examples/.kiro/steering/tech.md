# Technology Stack

## Framework & Language

- **프레임워크**: Next.js 15 (App Router)
- **언어**: TypeScript
- **런타임**: Node.js
- **UI 라이브러리**: React 18
- **UI 컴포넌트**: Shadcn UI
- **스타일링**: Tailwind CSS

## Database & ORM

- **데이터베이스**: Aurora MySQL Serverless v2
- **ORM**: Prisma
- **마이그레이션**: Prisma Migrate
- **문자 인코딩**: UTF-8 (utf8mb4)

## Authentication

- **인증 라이브러리**: NextAuth.js
- **인증 방식**: OAuth2
- **세션 관리**: JWT 기반
- **권한 관리**: 역할 기반 접근 제어 (RBAC)

## Testing

- **Unit Testing**: Vitest
- **Property-Based Testing**: fast-check (기본 100회, 복잡한 속성 200회 반복)
- **Integration Testing**: Vitest + Supertest
- **E2E Testing**: Playwright
- **Mocking**: Vitest 내장 모킹
- **Coverage**: Vitest c8

## Additional Libraries

- **스키마 검증**: Zod
- **시간대 처리**: date-fns-tz
- **날짜 조작**: date-fns
- **HTTP 클라이언트**: fetch (내장)

## Common Commands

### Development
```bash
npm run dev              # 개발 서버 시작 (http://localhost:3000)
npm run build            # 프로덕션 빌드
npm run start            # 프로덕션 서버 시작
npm run lint             # ESLint 실행
npm run type-check       # TypeScript 타입 체크
```

### Database
```bash
npx prisma generate      # Prisma Client 생성
npx prisma migrate dev   # 개발 환경 마이그레이션 생성 및 실행
npx prisma migrate deploy # 프로덕션 마이그레이션 실행
npx prisma studio        # Prisma Studio 실행 (데이터베이스 GUI)
npx prisma db seed       # 시드 데이터 실행
npx prisma db push       # 스키마를 데이터베이스에 직접 푸시 (개발용)
```

### Testing
```bash
npm run test             # 모든 테스트 실행
npm run test:unit        # 단위 테스트만 실행
npm run test:property    # Property-based 테스트만 실행
npm run test:integration # 통합 테스트만 실행
npm run test:e2e         # E2E 테스트 실행
npm run test:watch       # Watch 모드로 테스트 실행
npm run test:coverage    # 커버리지 포함 테스트 실행
```

### Linting & Formatting
```bash
npm run lint             # ESLint 실행
npm run lint:fix         # ESLint 자동 수정
npm run format           # Prettier 실행
npm run format:check     # Prettier 체크만 실행
```

### Shadcn UI
```bash
npx shadcn-ui@latest add button      # Button 컴포넌트 추가
npx shadcn-ui@latest add input       # Input 컴포넌트 추가
npx shadcn-ui@latest add form        # Form 컴포넌트 추가
npx shadcn-ui@latest add dialog      # Dialog 컴포넌트 추가
npx shadcn-ui@latest add calendar    # Calendar 컴포넌트 추가
npx shadcn-ui@latest add toast       # Toast 컴포넌트 추가
```

## Development Guidelines

### Next.js 15 Conventions

- **App Router 사용**: `pages` 디렉토리 대신 `app` 디렉토리 사용
- **Server Components 기본**: 명시적으로 `'use client'`를 선언하지 않으면 Server Component
- **Server Actions**: `'use server'` 지시어로 서버 함수 정의
- **파일 기반 라우팅**: `app` 디렉토리 구조가 URL 구조를 결정
- **레이아웃 중첩**: 각 라우트 세그먼트에 `layout.tsx` 정의 가능
- **로딩 및 에러 처리**: `loading.tsx`, `error.tsx`로 자동 처리
- **메타데이터**: `metadata` export 또는 `generateMetadata` 함수 사용
- **캐시 관리**: `revalidatePath`, `revalidateTag`로 캐시 무효화

### TypeScript

- **엄격 모드 사용**: `tsconfig.json`에서 `strict: true` 설정
- **명시적 타입 정의**: 함수 매개변수와 반환 타입 명시
- **타입 추론 활용**: 변수 선언 시 타입 추론 가능하면 생략
- **인터페이스 우선**: 객체 타입은 `interface` 사용, 유니온/인터섹션은 `type` 사용
- **Enum 대신 Union Types**: 가능하면 `type UserRole = 'USER' | 'ADMINISTRATOR'` 형태 사용
- **Non-null Assertion 지양**: `!` 연산자 대신 명시적 null 체크
- **any 타입 금지**: `unknown` 또는 구체적 타입 사용
- **타입 가드 활용**: 런타임 타입 체크 시 타입 가드 함수 작성

### Database

- **Prisma Client 싱글톤**: 전역 Prisma Client 인스턴스 재사용
- **트랜잭션 사용**: 여러 작업을 원자적으로 실행할 때 `prisma.$transaction` 사용
- **관계 로딩**: 필요한 관계만 `include` 또는 `select`로 명시
- **인덱스 활용**: 자주 조회하는 필드에 인덱스 추가
- **마이그레이션 관리**: 스키마 변경 시 항상 마이그레이션 생성
- **시드 데이터**: 개발/테스트 환경용 시드 스크립트 작성
- **연결 풀링**: 프로덕션 환경에서 연결 풀 설정 최적화
- **쿼리 최적화**: N+1 문제 방지, 필요한 필드만 조회

### Testing

- **테스트 격리**: 각 테스트는 독립적으로 실행 가능해야 함
- **AAA 패턴**: Arrange (준비), Act (실행), Assert (검증) 순서로 작성
- **Property-Based Testing 태그**: 각 property test에 주석으로 속성 번호 명시
  ```typescript
  // Feature: Reservation, Property 3: 예약 시간 검증
  ```
- **반복 횟수 설정**: design.md에 명시된 반복 횟수 사용 (기본 100회, 복잡한 속성 200회)
- **테스트 데이터 생성**: fast-check Arbitrary 사용하여 무작위 데이터 생성
- **모킹 최소화**: 실제 구현 테스트 우선, 필요시에만 모킹
- **커버리지 목표**: 최소 80% 유지, 핵심 비즈니스 로직 100%
- **E2E 테스트 선택적 실행**: 크리티컬 패스 중심으로 작성

### Error Handling

- **표준 오류 형식**: `ErrorResponse` 인터페이스 사용
- **오류 코드 정의**: `ErrorCode` enum으로 오류 유형 분류
- **HTTP 상태 코드**: 적절한 HTTP 상태 코드 반환 (400, 401, 403, 404, 409, 500)
- **클라이언트 검증**: Zod 스키마로 폼 입력 검증
- **서버 검증**: 모든 입력에 대해 서버에서 재검증
- **트랜잭션 롤백**: 오류 발생 시 자동 롤백
- **사용자 친화적 메시지**: 한국어로 명확한 오류 메시지 제공
- **로깅**: 모든 오류를 구조화된 로그로 기록

### Security

- **서버 사이드 검증**: 모든 입력을 서버에서 검증
- **인증 필수**: 보호된 라우트와 API에 인증 미들웨어 적용
- **권한 확인**: 작업 수행 전 사용자 권한 확인
- **SQL Injection 방지**: Prisma ORM 사용으로 자동 방지
- **XSS 방지**: React의 자동 이스케이프 활용
- **CSRF 방지**: NextAuth.js의 CSRF 토큰 활용
- **환경 변수 보호**: `.env` 파일을 `.gitignore`에 추가
- **비밀번호 해싱**: OAuth2 사용으로 직접 비밀번호 관리 불필요

### Performance

- **Server Components 활용**: 서버에서 데이터 페칭하여 초기 로딩 속도 향상
- **이미지 최적화**: Next.js `Image` 컴포넌트 사용
- **코드 분할**: 동적 import로 필요한 코드만 로드
- **캐싱 전략**: Next.js 캐싱 활용, 필요시 `revalidate` 설정
- **데이터베이스 쿼리 최적화**: 인덱스 활용, N+1 문제 방지
- **번들 크기 최소화**: 불필요한 의존성 제거
- **Lazy Loading**: 화면에 보이지 않는 컴포넌트는 지연 로딩
- **메모이제이션**: `useMemo`, `useCallback` 적절히 사용

### Code Style

- **일관된 네이밍**: camelCase (변수, 함수), PascalCase (컴포넌트, 타입), UPPER_CASE (상수)
- **함수 길이 제한**: 한 함수는 한 가지 일만 수행, 20줄 이내 권장
- **주석 작성**: 복잡한 로직에만 주석 추가, 코드 자체가 설명이 되도록 작성
- **Early Return**: 조건문에서 early return 패턴 사용
- **매직 넘버 금지**: 상수로 정의하여 의미 부여
- **DRY 원칙**: 중복 코드 제거, 재사용 가능한 함수/컴포넌트 작성
- **SOLID 원칙**: 특히 단일 책임 원칙 준수
- **Prettier 사용**: 코드 포맷팅 자동화

## Deployment

- **플랫폼**: AWS Amplify
- **빌드 명령**: `npm run build`
- **출력 디렉토리**: `.next`
- **환경 변수**: Amplify 콘솔에서 설정
- **데이터베이스**: Aurora MySQL Serverless v2 (별도 설정)
- **도메인**: Amplify에서 자동 제공 또는 커스텀 도메인 연결
- **CI/CD**: Git 푸시 시 자동 빌드 및 배포
- **롤백**: Amplify 콘솔에서 이전 버전으로 롤백 가능
- **모니터링**: CloudWatch 로그 및 메트릭 활용
- **헬스 체크**: `/api/health` 엔드포인트 구현

## Environment Variables

프로젝트에 필요한 환경 변수:

```bash
# Database
DATABASE_URL="mysql://user:password@host:3306/database"

# NextAuth.js
NEXTAUTH_URL="http://localhost:3000"
NEXTAUTH_SECRET="your-secret-key"

# OAuth2 Provider
OAUTH_CLIENT_ID="your-client-id"
OAUTH_CLIENT_SECRET="your-client-secret"
OAUTH_ISSUER="https://your-oauth-provider.com"

# Timezone
TZ="Asia/Seoul"  # UTC+9

# Node Environment
NODE_ENV="development"  # development | production | test
```

## Package.json Scripts

```json
{
  "scripts": {
    "dev": "next dev",
    "build": "next build",
    "start": "next start",
    "lint": "next lint",
    "lint:fix": "next lint --fix",
    "format": "prettier --write .",
    "format:check": "prettier --check .",
    "type-check": "tsc --noEmit",
    "test": "vitest run",
    "test:unit": "vitest run tests/unit",
    "test:property": "vitest run tests/property",
    "test:integration": "vitest run tests/integration",
    "test:e2e": "playwright test",
    "test:watch": "vitest watch",
    "test:coverage": "vitest run --coverage",
    "prisma:generate": "prisma generate",
    "prisma:migrate": "prisma migrate dev",
    "prisma:studio": "prisma studio",
    "prisma:seed": "tsx prisma/seed.ts"
  }
}
```

## Recommended VS Code Extensions

- **ESLint**: 코드 린팅
- **Prettier**: 코드 포맷팅
- **Tailwind CSS IntelliSense**: Tailwind 클래스 자동완성
- **Prisma**: Prisma 스키마 하이라이팅 및 자동완성
- **TypeScript**: TypeScript 지원
- **Error Lens**: 인라인 오류 표시
- **GitLens**: Git 히스토리 및 블레임
- **Auto Rename Tag**: HTML/JSX 태그 자동 리네임
