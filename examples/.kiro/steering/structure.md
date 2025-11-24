# Project Structure

## Current Organization

```
room-book/
├── .kiro/
│   ├── idea/
│   │   └── idea.md
│   ├── specs/
│   │   ├── requirements.md
│   │   ├── design.md
│   │   └── tasks.md
│   └── steering/
│       ├── structure.md
│       ├── tech.md
│       └── product.md
└── [프로젝트 파일들]
```

## Expected Next.js 15 Structure

Next.js 15 App Router 기반 풀스택 애플리케이션 구조입니다. 프론트엔드와 백엔드가 통합된 모노리스 아키텍처를 사용하며, Server Components와 Server Actions를 활용합니다.

```
room-book/
├── .kiro/                          # 프로젝트 문서 및 명세
│   ├── idea/
│   ├── specs/
│   └── steering/
├── app/                            # Next.js 15 App Router
│   ├── (auth)/                     # 인증 관련 라우트 그룹
│   │   └── login/
│   │       └── page.tsx
│   ├── (dashboard)/                # 대시보드 라우트 그룹
│   │   └── dashboard/
│   │       ├── page.tsx            # 대시보드 메인 페이지
│   │       └── loading.tsx
│   ├── (admin)/                    # 관리자 라우트 그룹
│   │   └── admin/
│   │       └── rooms/
│   │           └── page.tsx        # 회의실 관리 페이지
│   ├── api/                        # API Routes
│   │   ├── auth/
│   │   │   └── [...nextauth]/
│   │   │       └── route.ts        # NextAuth.js 설정
│   │   ├── rooms/
│   │   │   ├── route.ts            # GET, POST /api/rooms
│   │   │   └── [id]/
│   │   │       └── route.ts        # GET, PATCH, DELETE /api/rooms/[id]
│   │   ├── reservations/
│   │   │   ├── route.ts            # GET, POST /api/reservations
│   │   │   └── [id]/
│   │   │       └── route.ts        # GET, PATCH, DELETE /api/reservations/[id]
│   │   ├── dashboard/
│   │   │   └── route.ts            # GET /api/dashboard
│   │   └── health/
│   │       └── route.ts            # GET /api/health
│   ├── actions/                    # Server Actions
│   │   ├── reservations.ts         # 예약 관련 Server Actions
│   │   ├── rooms.ts                # 회의실 관련 Server Actions
│   │   └── auth.ts                 # 인증 관련 Server Actions
│   ├── layout.tsx                  # 루트 레이아웃
│   ├── page.tsx                    # 홈 페이지
│   └── globals.css                 # 전역 스타일
├── components/                     # React 컴포넌트
│   ├── ui/                         # Shadcn UI 컴포넌트
│   │   ├── button.tsx
│   │   ├── input.tsx
│   │   ├── form.tsx
│   │   ├── dialog.tsx
│   │   ├── calendar.tsx
│   │   ├── toast.tsx
│   │   └── ...
│   ├── dashboard/                  # 대시보드 컴포넌트
│   │   ├── DashboardGrid.tsx
│   │   ├── DatePicker.tsx
│   │   ├── RoomCard.tsx
│   │   └── TimeSlotGrid.tsx
│   ├── reservations/               # 예약 컴포넌트
│   │   ├── ReservationForm.tsx
│   │   ├── ReservationCard.tsx
│   │   └── ReservationDialog.tsx
│   ├── rooms/                      # 회의실 컴포넌트
│   │   ├── RoomForm.tsx
│   │   ├── RoomList.tsx
│   │   └── RoomDialog.tsx
│   └── auth/                       # 인증 컴포넌트
│       ├── LoginButton.tsx
│       └── UserMenu.tsx
├── lib/                            # 라이브러리 및 유틸리티
│   ├── services/                   # 비즈니스 로직 서비스
│   │   ├── auth.service.ts
│   │   ├── room.service.ts
│   │   ├── reservation.service.ts
│   │   ├── validation.service.ts
│   │   └── dashboard.service.ts
│   ├── utils/                      # 유틸리티 함수
│   │   ├── time.ts                 # 시간 처리 유틸리티
│   │   ├── validation.ts           # 검증 유틸리티
│   │   └── error.ts                # 오류 처리 유틸리티
│   ├── db/                         # 데이터베이스 관련
│   │   └── prisma.ts               # Prisma 클라이언트 인스턴스
│   └── constants.ts                # 상수 정의
├── types/                          # TypeScript 타입 정의
│   ├── index.ts                    # 공통 타입
│   ├── auth.ts                     # 인증 관련 타입
│   ├── room.ts                     # 회의실 관련 타입
│   ├── reservation.ts              # 예약 관련 타입
│   └── api.ts                      # API 관련 타입
├── prisma/                         # Prisma ORM
│   ├── schema.prisma               # 데이터베이스 스키마
│   ├── migrations/                 # 마이그레이션 파일
│   └── seed.ts                     # 시드 데이터
├── tests/                          # 테스트 파일
│   ├── unit/                       # 단위 테스트
│   │   ├── services/
│   │   │   ├── auth.service.test.ts
│   │   │   ├── room.service.test.ts
│   │   │   ├── reservation.service.test.ts
│   │   │   ├── validation.service.test.ts
│   │   │   └── dashboard.service.test.ts
│   │   └── utils/
│   │       ├── time.test.ts
│   │       └── validation.test.ts
│   ├── property/                   # Property-based 테스트
│   │   ├── validation.property.test.ts
│   │   ├── reservation.property.test.ts
│   │   ├── room.property.test.ts
│   │   └── auth.property.test.ts
│   ├── integration/                # 통합 테스트
│   │   ├── api/
│   │   │   ├── rooms.test.ts
│   │   │   ├── reservations.test.ts
│   │   │   └── dashboard.test.ts
│   │   └── actions/
│   │       ├── reservations.test.ts
│   │       └── rooms.test.ts
│   ├── e2e/                        # E2E 테스트 (Playwright)
│   │   ├── auth.spec.ts
│   │   ├── dashboard.spec.ts
│   │   ├── reservations.spec.ts
│   │   ├── rooms.spec.ts
│   │   └── admin.spec.ts
│   └── helpers/                    # 테스트 헬퍼
│       ├── fixtures.ts
│       ├── generators.ts           # fast-check 생성기
│       └── setup.ts
├── public/                         # 정적 파일
│   ├── images/
│   └── icons/
├── .env                            # 환경 변수
├── .env.example                    # 환경 변수 예시
├── .gitignore
├── next.config.js                  # Next.js 설정
├── tailwind.config.ts              # Tailwind CSS 설정
├── tsconfig.json                   # TypeScript 설정
├── vitest.config.ts                # Vitest 설정
├── playwright.config.ts            # Playwright 설정
├── package.json
└── README.md
```

## Directory Conventions

### `/app` - Next.js 15 App Router
- **라우트 그룹**: 괄호 `()`로 URL에 영향을 주지 않는 논리적 그룹 생성
- **페이지**: `page.tsx` 파일로 라우트 정의
- **레이아웃**: `layout.tsx`로 공통 레이아웃 정의
- **로딩**: `loading.tsx`로 로딩 상태 정의
- **에러**: `error.tsx`로 에러 처리
- **API Routes**: `app/api` 디렉토리에 `route.ts` 파일로 정의

### `/app/actions` - Server Actions
- Server Component에서 호출할 수 있는 서버 사이드 함수
- `'use server'` 지시어 사용
- 비즈니스 로직 실행 및 데이터 변경
- 파일명: 기능별로 그룹화 (예: `reservations.ts`, `rooms.ts`)

### `/components` - React 컴포넌트
- **ui/**: Shadcn UI 컴포넌트 (설치 후 자동 생성)
- **기능별 디렉토리**: 각 기능별로 관련 컴포넌트 그룹화
- Server Components와 Client Components 혼용
- Client Component는 파일 상단에 `'use client'` 지시어 필요

### `/lib` - 라이브러리 및 유틸리티
- **services/**: 비즈니스 로직을 캡슐화한 서비스 클래스/함수
- **utils/**: 재사용 가능한 유틸리티 함수
- **db/**: 데이터베이스 클라이언트 및 연결 관리
- 순수 함수 중심으로 작성하여 테스트 용이성 확보

### `/types` - TypeScript 타입 정의
- 도메인별로 타입 파일 분리
- `index.ts`에서 공통 타입 export
- Prisma 생성 타입과 애플리케이션 타입 분리
- DTO, Entity, Service 인터페이스 정의

### `/prisma` - Prisma ORM
- **schema.prisma**: 데이터베이스 스키마 정의
- **migrations/**: 자동 생성된 마이그레이션 파일
- **seed.ts**: 초기 데이터 생성 스크립트

### `/tests` - 테스트 파일
- **unit/**: 단위 테스트 (서비스, 유틸리티)
- **property/**: Property-based 테스트 (fast-check)
- **integration/**: 통합 테스트 (API, Server Actions)
- **e2e/**: E2E 테스트 (Playwright)
- **helpers/**: 테스트 헬퍼 및 픽스처

## File Naming Conventions

- **React 컴포넌트**: PascalCase (`DashboardGrid.tsx`, `ReservationForm.tsx`)
- **페이지 파일**: 소문자 (`page.tsx`, `layout.tsx`, `loading.tsx`)
- **API Routes**: 소문자 (`route.ts`)
- **Server Actions**: camelCase (`reservations.ts`, `rooms.ts`)
- **서비스 파일**: camelCase + `.service.ts` (`auth.service.ts`, `room.service.ts`)
- **유틸리티 파일**: camelCase + `.ts` (`time.ts`, `validation.ts`)
- **타입 파일**: camelCase + `.ts` (`auth.ts`, `room.ts`)
- **테스트 파일**: 원본 파일명 + `.test.ts` 또는 `.spec.ts`
  - 단위/통합: `.test.ts` (`auth.service.test.ts`)
  - E2E: `.spec.ts` (`dashboard.spec.ts`)
  - Property: `.property.test.ts` (`validation.property.test.ts`)

## Import Path Aliases

TypeScript 경로 별칭을 사용하여 import 경로를 단순화합니다.

```typescript
// tsconfig.json
{
  "compilerOptions": {
    "baseUrl": ".",
    "paths": {
      "@/*": ["./*"],
      "@/components/*": ["components/*"],
      "@/lib/*": ["lib/*"],
      "@/types/*": ["types/*"],
      "@/app/*": ["app/*"],
      "@/tests/*": ["tests/*"]
    }
  }
}
```

**사용 예시**:
```typescript
// ❌ 상대 경로 (피하기)
import { Button } from '../../../components/ui/button';
import { authService } from '../../../lib/services/auth.service';

// ✅ 절대 경로 (권장)
import { Button } from '@/components/ui/button';
import { authService } from '@/lib/services/auth.service';
```

## Module Organization

### Service Layer Pattern

서비스는 비즈니스 로직을 캡슐화하고 재사용 가능한 함수로 제공합니다.

```typescript
// lib/services/reservation.service.ts
import { prisma } from '@/lib/db/prisma';
import { CreateReservationDto, Reservation } from '@/types/reservation';
import { validationService } from './validation.service';

export const reservationService = {
  async createReservation(data: CreateReservationDto): Promise<Reservation> {
    // 검증
    const validation = await validationService.validateReservationTime(
      data.startTime,
      data.endTime
    );
    
    if (!validation.isValid) {
      throw new Error(validation.errors.join(', '));
    }

    // 트랜잭션으로 생성
    return await prisma.reservation.create({
      data,
      include: {
        user: true,
        room: true,
      },
    });
  },

  async getReservationsByDate(date: Date): Promise<Reservation[]> {
    // 구현...
  },

  // 기타 메서드...
};
```

### Server Action Pattern

Server Actions는 클라이언트에서 직접 호출할 수 있는 서버 함수입니다.

```typescript
// app/actions/reservations.ts
'use server';

import { revalidatePath } from 'next/cache';
import { reservationService } from '@/lib/services/reservation.service';
import { authService } from '@/lib/services/auth.service';

export async function createReservationAction(formData: FormData) {
  // 인증 확인
  const user = await authService.getCurrentUser();
  if (!user) {
    throw new Error('인증이 필요합니다');
  }

  // 데이터 추출
  const data = {
    userId: user.id,
    roomId: formData.get('roomId') as string,
    startTime: new Date(formData.get('startTime') as string),
    endTime: new Date(formData.get('endTime') as string),
    purpose: formData.get('purpose') as string,
  };

  // 서비스 호출
  const reservation = await reservationService.createReservation(data);

  // 캐시 무효화
  revalidatePath('/dashboard');

  return reservation;
}
```

### API Route Pattern

API Routes는 RESTful 엔드포인트를 제공합니다.

```typescript
// app/api/rooms/route.ts
import { NextRequest, NextResponse } from 'next/server';
import { roomService } from '@/lib/services/room.service';
import { authService } from '@/lib/services/auth.service';

// GET /api/rooms
export async function GET(request: NextRequest) {
  try {
    const rooms = await roomService.getAllRooms();
    return NextResponse.json(rooms);
  } catch (error) {
    return NextResponse.json(
      { error: '회의실 조회 실패' },
      { status: 500 }
    );
  }
}

// POST /api/rooms
export async function POST(request: NextRequest) {
  try {
    // 관리자 권한 확인
    const user = await authService.getCurrentUser();
    if (!user || !await authService.isAdministrator(user.id)) {
      return NextResponse.json(
        { error: '권한이 없습니다' },
        { status: 403 }
      );
    }

    const data = await request.json();
    const room = await roomService.createRoom(data);
    return NextResponse.json(room, { status: 201 });
  } catch (error) {
    return NextResponse.json(
      { error: '회의실 생성 실패' },
      { status: 500 }
    );
  }
}
```

### Component Pattern

컴포넌트는 Server Component를 기본으로 하고, 필요시 Client Component로 전환합니다.

```typescript
// components/dashboard/DashboardGrid.tsx (Server Component)
import { reservationService } from '@/lib/services/reservation.service';
import { roomService } from '@/lib/services/room.service';
import { TimeSlotGrid } from './TimeSlotGrid';

interface DashboardGridProps {
  date: Date;
}

export async function DashboardGrid({ date }: DashboardGridProps) {
  // 서버에서 데이터 페칭
  const rooms = await roomService.getAllRooms();
  const reservations = await reservationService.getReservationsByDate(date);

  return (
    <div className="grid gap-4">
      {rooms.map((room) => (
        <TimeSlotGrid
          key={room.id}
          room={room}
          reservations={reservations.filter((r) => r.roomId === room.id)}
        />
      ))}
    </div>
  );
}
```

```typescript
// components/dashboard/TimeSlotGrid.tsx (Client Component)
'use client';

import { useState } from 'react';
import { Room, Reservation } from '@/types';
import { Button } from '@/components/ui/button';

interface TimeSlotGridProps {
  room: Room;
  reservations: Reservation[];
}

export function TimeSlotGrid({ room, reservations }: TimeSlotGridProps) {
  const [selectedSlot, setSelectedSlot] = useState<string | null>(null);

  // 클라이언트 사이드 인터랙션
  const handleSlotClick = (slotId: string) => {
    setSelectedSlot(slotId);
    // 예약 폼 표시 등...
  };

  return (
    <div className="grid grid-cols-24 gap-1">
      {/* 시간 슬롯 렌더링 */}
    </div>
  );
}
```

## Best Practices

- **계층 분리**: Presentation (Components) → Application (Services/Actions) → Data (Prisma) 계층을 명확히 분리
- **Server Components 우선**: 가능한 한 Server Components를 사용하고, 인터랙션이 필요한 경우에만 Client Components 사용
- **타입 안정성**: 모든 함수와 컴포넌트에 명시적 타입 정의
- **에러 처리**: try-catch 블록과 명확한 에러 메시지 제공
- **재사용성**: 공통 로직은 서비스나 유틸리티로 추출
- **테스트 가능성**: 순수 함수 중심으로 작성하여 테스트 용이성 확보
- **일관된 네이밍**: 파일명, 함수명, 변수명에 일관된 규칙 적용
- **코드 분할**: 기능별로 파일과 디렉토리를 분리하여 유지보수성 향상
- **문서화**: 복잡한 로직에는 주석으로 설명 추가
- **보안**: 서버 사이드에서 모든 입력 검증 및 권한 확인
