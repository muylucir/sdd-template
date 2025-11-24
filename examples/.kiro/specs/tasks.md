# Implementation Plan

## Phase 1: 프로젝트 기반 설정

- [x] 1. Next.js 15 프로젝트 초기화 및 기본 설정
  - Next.js 15 프로젝트 생성 (App Router 사용)
  - TypeScript 설정 및 tsconfig.json 구성
  - ESLint, Prettier 설정
  - 프로젝트 폴더 구조 생성 (app, lib, components, types 등)
  - _Requirements: All_

- [x] 2. 의존성 패키지 설치
  - Shadcn UI 및 Tailwind CSS 설정
  - Prisma ORM 설치 및 초기화
  - NextAuth.js 설치
  - date-fns-tz 설치 (시간대 처리)
  - Zod 설치 (스키마 검증)
  - Vitest, fast-check, Playwright 설치 (테스팅)
  - _Requirements: All_

- [x] 3. 데이터베이스 스키마 정의 및 마이그레이션
  - Prisma 스키마 파일 작성 (User, Room, Reservation 모델)
  - 데이터베이스 연결 설정 (Aurora MySQL Serverless v2)
  - 초기 마이그레이션 실행
  - Prisma Client 생성
  - _Requirements: All_

- [x] 4. TypeScript 타입 정의 생성
  - 공통 타입 정의 (types/index.ts)
  - UserRole enum 정의
  - DTO 인터페이스 정의 (CreateRoomDto, UpdateRoomDto, CreateReservationDto 등)
  - 서비스 인터페이스 정의 (AuthService, RoomService, ReservationService 등)
  - ValidationResult, ErrorResponse 타입 정의
  - _Requirements: All_

- [x] 5. 환경 변수 및 설정 파일 구성
  - .env 파일 템플릿 생성
  - 데이터베이스 URL 설정
  - OAuth2 설정 변수
  - 시간대 설정 (UTC+9)
  - 비즈니스 규칙 상수 정의 (운영 시간, 예약 제한 등)
  - _Requirements: 16.1, 16.2, 16.3, 16.4_

- [x] 6. Checkpoint - 프로젝트 기반 검증
  - 프로젝트가 오류 없이 빌드되는지 확인
  - TypeScript 타입 체크 통과 확인
  - Prisma Client 생성 확인
  - 질문이 있으면 사용자에게 문의

## Phase 2: 유틸리티 및 검증 서비스 구현

- [x] 7. 시간 처리 유틸리티 구현
  - UTC+9 시간대 변환 함수 구현
  - 30분 단위 정렬 함수 구현
  - 시간 범위 계산 함수 구현
  - 운영 시간 검증 함수 구현
  - 예약 가능 기간 계산 함수 구현
  - _Requirements: 16.1, 16.2, 16.3, 16.4_

- [x] 7.1 시간 유틸리티 단위 테스트 작성
  - 30분 단위 정렬 테스트
  - UTC+9 변환 테스트
  - 운영 시간 범위 검증 테스트
  - 예약 가능 기간 계산 테스트
  - _Requirements: 16.1, 16.2, 16.3, 16.4_

- [x] 8. Validation Service 구현
- [x] 8.1 예약 시간 검증 로직 구현
  - validateReservationTime 함수 구현
  - 30분 단위 검증
  - 최소/최대 시간 검증 (30분~2시간)
  - 운영 시간 검증 (08:00~20:00)
  - _Requirements: 3.5, 3.6, 3.7, 3.8, 3.9, 3.10_

- [x] 8.2 예약 날짜 검증 로직 구현
  - validateReservationDate 함수 구현
  - 예약 가능 기간 검증 (0~30일)
  - _Requirements: 2.3, 2.4_

- [x] 8.3 시간대 충돌 검증 로직 구현
  - validateTimeSlotConflict 함수 구현
  - 시간대 겹침 감지 로직 (모든 경우)
  - 데이터베이스 조회 및 충돌 확인
  - _Requirements: 7.1, 7.2, 7.3, 7.4_

- [x] 8.4 사용자 예약 제한 검증 로직 구현
  - validateUserReservationLimit 함수 구현
  - 활성 예약 개수 확인 (현재 시간 이후)
  - 최대 3개 제한 검증
  - _Requirements: 6.1, 6.2, 6.3, 6.4_

- [x] 8.5 회의실 이름 검증 로직 구현
  - validateRoomName 함수 구현
  - 중복 이름 확인
  - _Requirements: 10.6, 10.7, 11.5, 11.6_

- [x] 8.6 회의실 삭제 가능 여부 검증 로직 구현
  - validateRoomDeletion 함수 구현
  - 활성 예약 존재 여부 확인
  - 예약 개수 포함한 메시지 생성
  - _Requirements: 12.2, 12.3, 12.5, 12.6_

- [x] 8.7 Property Test 작성 - 예약 시간 검증
  - **Property 3: 예약 시간 검증**
  - **Validates: Requirements 3.5, 3.6, 3.7, 3.8, 3.9, 3.10**
  - fast-check를 사용하여 무작위 시간 생성 및 검증
  - design.md에 명시된 반복 횟수로 테스트 실행

- [x] 8.8 Property Test 작성 - 날짜 선택 제약
  - **Property 2: 날짜 선택 제약**
  - **Validates: Requirements 2.3, 2.4, 16.4**
  - 무작위 날짜 오프셋 생성 및 검증
  - design.md에 명시된 반복 횟수로 테스트 실행

- [x] 8.9 Property Test 작성 - 예약 충돌 방지
  - **Property 4: 예약 충돌 방지**
  - **Validates: Requirements 7.1, 7.2, 7.3, 7.4**
  - 무작위 시간대 생성 및 충돌 감지 검증
  - design.md에 명시된 반복 횟수로 테스트 실행

- [x] 8.10 Property Test 작성 - 사용자 예약 제한
  - **Property 5: 사용자 예약 제한**
  - **Validates: Requirements 6.1, 6.2, 6.3, 6.4**
  - 무작위 사용자 예약 개수 생성 및 제한 검증
  - design.md에 명시된 반복 횟수로 테스트 실행

- [x] 8.11 Property Test 작성 - 회의실 이름 유일성
  - **Property 8: 회의실 이름 유일성**
  - **Validates: Requirements 10.6, 10.7, 11.5, 11.6**
  - 무작위 회의실 이름 생성 및 중복 검증
  - design.md에 명시된 반복 횟수로 테스트 실행

- [x] 8.12 Property Test 작성 - 회의실 삭제 제약
  - **Property 9: 회의실 삭제 제약**
  - **Validates: Requirements 12.2, 12.3, 12.5, 12.6**
  - 무작위 회의실 및 예약 상태 생성 및 삭제 가능 여부 검증
  - design.md에 명시된 반복 횟수로 테스트 실행

- [x] 8.13 Validation Service 단위 테스트 작성
  - 30분 단위가 아닌 시간 검증 실패 테스트
  - 최소 시간 미만 검증 실패 테스트
  - 최대 시간 초과 검증 실패 테스트
  - 운영 시간 외 검증 실패 테스트
  - 예약 가능 기간 외 검증 실패 테스트
  - 시간대 충돌 감지 테스트
  - 예약 제한 초과 테스트
  - 회의실 이름 중복 테스트
  - 활성 예약 있는 회의실 삭제 거부 테스트
  - _Requirements: 3.5, 3.6, 3.7, 3.8, 3.9, 3.10, 2.3, 2.4, 7.1, 7.2, 7.3, 7.4, 6.1, 6.2, 6.3, 6.4, 10.6, 10.7, 11.5, 11.6, 12.2, 12.3, 12.5, 12.6_

- [x] 9. Checkpoint - Validation Service 검증
  - 모든 단위 테스트 통과 확인
  - design.md에 명시된 반복 횟수로 property test 실행 및 통과 확인
  - 질문이 있으면 사용자에게 문의

## Phase 3: 인증 및 권한 관리 구현

- [x] 10. Authentication Service 구현
- [x] 10.1 NextAuth.js 설정 및 Credentials Provider 통합
  - NextAuth.js 설정 파일 생성 (app/api/auth/[...nextauth]/route.ts)
  - Credentials Provider 설정 (이메일 기반 인증)
  - 세션 관리 설정
  - JWT 토큰 설정
  - _Requirements: 13.1, 13.2, 13.3, 13.4_

- [x] 10.2 Authentication Service 구현
  - getCurrentUser 함수 구현
  - hasRole 함수 구현
  - isAdministrator 함수 구현
  - isReservationOwner 함수 구현
  - _Requirements: 13.1, 13.2, 13.3, 13.4, 14.1, 14.2, 14.3, 14.4, 14.5_

- [x] 10.3 Property Test 작성 - 인증 필수
  - **Property 11: 인증 필수**
  - **Validates: Requirements 13.1, 13.2, 13.3**
  - 무작위 인증 상태 생성 및 접근 제어 검증
  - design.md에 명시된 반복 횟수로 테스트 실행

- [x] 10.4 Property Test 작성 - 역할 식별
  - **Property 12: 역할 식별**
  - **Validates: Requirements 13.4, 14.1**
  - 무작위 사용자 역할 생성 및 식별 검증
  - design.md에 명시된 반복 횟수로 테스트 실행

- [x] 10.5 Property Test 작성 - 관리자 권한 검증
  - **Property 10: 관리자 권한 검증**
  - **Validates: Requirements 14.2, 14.3, 14.5**
  - 무작위 사용자 역할 생성 및 관리 기능 접근 검증
  - design.md에 명시된 반복 횟수로 테스트 실행

- [x] 10.6 Property Test 작성 - 예약 소유권 검증
  - **Property 6: 예약 소유권 검증**
  - **Validates: Requirements 4.6, 5.4, 9.5, 14.4**
  - 무작위 사용자 및 예약 생성 및 소유권 검증
  - design.md에 명시된 반복 횟수로 테스트 실행

- [x] 10.7 Authentication Service 단위 테스트 작성
  - 유효한 인증 정보로 접근 허용 테스트
  - 유효하지 않은 인증 정보로 접근 거부 테스트
  - 관리자 역할 확인 테스트
  - 일반 사용자 역할 확인 테스트
  - 예약 소유권 확인 테스트
  - 타인 예약 접근 거부 테스트
  - _Requirements: 13.1, 13.2, 13.3, 13.4, 14.1, 14.2, 14.3, 14.4, 14.5, 4.6, 5.4, 9.5_

- [x] 11. Checkpoint - Authentication Service 검증
  - 모든 단위 테스트 통과 확인
  - design.md에 명시된 반복 횟수로 property test 실행 및 통과 확인
  - 인증 로그인 플로우 검증 완료
  - 질문이 있으면 사용자에게 문의

## Phase 4: 회의실 관리 서비스 구현

- [x] 12. Room Service 구현
- [x] 12.1 회의실 CRUD 작업 구현
  - getAllRooms 함수 구현
  - getRoomById 함수 구현
  - createRoom 함수 구현 (관리자 전용, 검증 포함)
  - updateRoom 함수 구현 (관리자 전용, 검증 포함)
  - deleteRoom 함수 구현 (관리자 전용, 활성 예약 확인)
  - isRoomNameExists 함수 구현
  - hasActiveReservations 함수 구현
  - _Requirements: 10.1, 10.2, 10.3, 10.4, 10.5, 10.6, 10.7, 11.1, 11.2, 11.3, 11.4, 11.5, 11.6, 12.1, 12.2, 12.3, 12.4, 12.5, 12.6_

- [x] 12.2 Property Test 작성 - 트랜잭션 원자성 (회의실)
  - **Property 14: 트랜잭션 원자성**
  - **Validates: Requirements 10.3, 11.3, 12.3**
  - 무작위 회의실 작업 생성 및 트랜잭션 롤백 검증
  - design.md에 명시된 반복 횟수로 테스트 실행

- [x] 12.3 Property Test 작성 - 입력 데이터 검증 (회의실)
  - **Property 15: 입력 데이터 검증**
  - **Validates: Requirements 10.2, 11.2**
  - 무작위 회의실 입력 생성 및 서버 사이드 검증 확인
  - design.md에 명시된 반복 횟수로 테스트 실행

- [x] 12.4 Room Service 단위 테스트 작성
  - 모든 회의실 조회 테스트
  - 특정 회의실 조회 테스트
  - 회의실 생성 성공 테스트
  - 회의실 이름 중복 시 생성 실패 테스트
  - 회의실 수정 성공 테스트
  - 회의실 이름 중복 시 수정 실패 테스트
  - 활성 예약 없는 회의실 삭제 성공 테스트
  - 활성 예약 있는 회의실 삭제 실패 테스트
  - 일반 사용자의 회의실 관리 접근 거부 테스트
  - _Requirements: 10.1, 10.2, 10.3, 10.4, 10.5, 10.6, 10.7, 11.1, 11.2, 11.3, 11.4, 11.5, 11.6, 12.1, 12.2, 12.3, 12.4, 12.5, 12.6_

- [x] 13. Checkpoint - Room Service 검증
  - 모든 단위 테스트 통과 확인
  - design.md에 명시된 반복 횟수로 property test 실행 및 통과 확인
  - 질문이 있으면 사용자에게 문의
  - design.md에 명시된 반복 횟수로 property test 실행 및 통과 확인
  - 질문이 있으면 사용자에게 문의

## Phase 5: 예약 관리 서비스 구현

- [x] 14. Reservation Service 구현
- [x] 14.1 예약 조회 기능 구현
  - getReservationsByDate 함수 구현
  - getUserActiveReservations 함수 구현
  - getReservationById 함수 구현
  - getUserReservationCount 함수 구현
  - isTimeSlotAvailable 함수 구현
  - _Requirements: 1.1, 1.2, 1.3, 1.4, 1.5, 6.1, 6.4, 7.1, 8.1, 8.2, 8.3_

- [x] 14.2 예약 생성 기능 구현
  - createReservation 함수 구현
  - 모든 검증 규칙 적용 (시간, 날짜, 충돌, 제한)
  - 트랜잭션 사용하여 원자성 보장
  - 데이터베이스에 예약 저장
  - _Requirements: 3.1, 3.2, 3.3, 3.4, 3.5, 3.6, 3.7, 3.8, 3.9, 3.10, 6.1, 6.2, 6.3, 7.1, 7.2, 7.3_

- [x] 14.3 예약 수정 기능 구현
  - updateReservation 함수 구현
  - 소유권 검증 (소유자 또는 관리자)
  - 모든 검증 규칙 적용
  - 트랜잭션 사용하여 원자성 보장
  - 데이터베이스에 변경 사항 저장
  - _Requirements: 4.1, 4.2, 4.3, 4.4, 4.5, 4.6, 9.1, 9.2, 9.5_

- [x] 14.4 예약 삭제 기능 구현
  - deleteReservation 함수 구현
  - 소유권 검증 (소유자 또는 관리자)
  - 트랜잭션 사용하여 원자성 보장
  - 데이터베이스에서 예약 삭제
  - _Requirements: 5.1, 5.2, 5.3, 5.4, 9.3, 9.4, 9.5_

- [x] 14.5 Property Test 작성 - 예약 생성 후 상태 반영
  - **Property 7: 예약 생성 후 상태 반영**
  - **Validates: Requirements 3.3, 3.4, 4.3, 4.4, 5.2, 5.3**
  - 무작위 예약 데이터 생성 및 영속성 검증
  - design.md에 명시된 반복 횟수로 테스트 실행

- [x] 14.6 Property Test 작성 - 시간대 일관성
  - **Property 13: 시간대 일관성**
  - **Validates: Requirements 16.1, 16.2, 16.3, 16.4**
  - 무작위 날짜/시간 생성 및 UTC+9 일관성 검증
  - design.md에 명시된 반복 횟수로 테스트 실행

- [x] 14.7 Property Test 작성 - 트랜잭션 원자성 (예약)
  - **Property 14: 트랜잭션 원자성**
  - **Validates: Requirements 3.3, 4.3, 5.2**
  - 무작위 예약 작업 생성 및 트랜잭션 롤백 검증
  - design.md에 명시된 반복 횟수로 테스트 실행

- [x] 14.8 Property Test 작성 - 입력 데이터 검증 (예약)
  - **Property 15: 입력 데이터 검증**
  - **Validates: Requirements 3.2, 4.2**
  - 무작위 예약 입력 생성 및 서버 사이드 검증 확인
  - design.md에 명시된 반복 횟수로 테스트 실행

- [x] 14.9 Reservation Service 단위 테스트 작성
  - 특정 날짜의 예약 조회 테스트
  - 사용자 활성 예약 조회 테스트
  - 예약 생성 성공 테스트
  - 시간대 충돌 시 예약 생성 실패 테스트
  - 예약 제한 초과 시 생성 실패 테스트
  - 예약 수정 성공 테스트
  - 타인 예약 수정 시도 실패 테스트
  - 예약 삭제 성공 테스트
  - 타인 예약 삭제 시도 실패 테스트
  - 관리자의 모든 예약 관리 성공 테스트
  - _Requirements: 3.1, 3.2, 3.3, 3.4, 4.1, 4.2, 4.3, 4.4, 4.6, 5.1, 5.2, 5.3, 5.4, 6.1, 6.2, 6.3, 7.1, 7.2, 7.3, 8.1, 8.2, 8.3, 9.1, 9.2, 9.3, 9.4, 9.5_

- [x] 15. Checkpoint - Reservation Service 검증
  - 모든 단위 테스트 통과 확인
  - 질문이 있으면 사용자에게 문의

## Phase 6: 대시보드 서비스 구현

- [x] 16. Dashboard Service 구현
- [x] 16.1 대시보드 데이터 집계 기능 구현
  - getDashboardData 함수 구현
  - 특정 날짜의 모든 회의실 조회
  - 특정 날짜의 모든 예약 조회
  - 시간 슬롯 생성
  - 데이터 통합 및 반환
  - _Requirements: 1.1, 1.2, 1.3, 1.4, 1.5, 2.1, 2.2, 2.5_

- [x] 16.2 시간 슬롯 생성 기능 구현
  - generateTimeSlots 함수 구현
  - 운영 시간 기준 (08:00~20:00)
  - 30분 단위 슬롯 생성
  - UTC+9 시간대 적용
  - _Requirements: 1.6, 1.7_

- [x] 16.3 Property Test 작성 - 대시보드 데이터 일관성
  - **Property 1: 대시보드 데이터 일관성**
  - **Validates: Requirements 1.1, 1.2, 1.3, 1.4, 1.5, 1.6, 1.7**
  - 무작위 날짜 생성 및 대시보드 데이터 일관성 검증
  - design.md에 명시된 반복 횟수로 테스트 실행

- [x] 16.4 Dashboard Service 단위 테스트 작성
  - 대시보드 데이터 조회 테스트
  - 모든 회의실 포함 확인 테스트
  - 모든 예약 포함 확인 테스트
  - 시간 슬롯 30분 단위 확인 테스트
  - 시간 슬롯 운영 시간 범위 확인 테스트
  - _Requirements: 1.1, 1.2, 1.3, 1.4, 1.5, 1.6, 1.7, 2.1, 2.2, 2.5_

- [x] 17. Checkpoint - Dashboard Service 검증
  - 모든 단위 테스트 통과 확인
  - 질문이 있으면 사용자에게 문의

## Phase 7: API 레이어 구현

- [x] 18. 회의실 관리 API Routes 구현
- [x] 18.1 회의실 API 엔드포인트 생성
  - GET /api/rooms - 모든 회의실 조회
  - GET /api/rooms/[id] - 특정 회의실 조회
  - POST /api/rooms - 회의실 생성 (관리자 전용)
  - PATCH /api/rooms/[id] - 회의실 수정 (관리자 전용)
  - DELETE /api/rooms/[id] - 회의실 삭제 (관리자 전용)
  - 인증 미들웨어 적용
  - 권한 검증 미들웨어 적용
  - _Requirements: 10.1, 10.2, 10.3, 10.4, 10.5, 10.6, 10.7, 11.1, 11.2, 11.3, 11.4, 11.5, 11.6, 12.1, 12.2, 12.3, 12.4, 12.5, 12.6_

- [x] 18.2 회의실 API 통합 테스트 작성
  - GET /api/rooms 성공 테스트
  - POST /api/rooms 성공 테스트 (관리자)
  - POST /api/rooms 실패 테스트 (일반 사용자)
  - PATCH /api/rooms/[id] 성공 테스트 (관리자)
  - DELETE /api/rooms/[id] 성공 테스트 (활성 예약 없음)
  - DELETE /api/rooms/[id] 실패 테스트 (활성 예약 있음)
  - 인증 없이 접근 시 401 오류 테스트
  - _Requirements: 10.1, 10.2, 10.3, 10.4, 10.5, 10.6, 10.7, 11.1, 11.2, 11.3, 11.4, 11.5, 11.6, 12.1, 12.2, 12.3, 12.4, 12.5, 12.6_

- [x] 19. 예약 관리 API Routes 구현
- [x] 19.1 예약 API 엔드포인트 생성
  - GET /api/reservations - 예약 조회 (날짜 파라미터)
  - GET /api/reservations/[id] - 특정 예약 조회
  - GET /api/reservations/user/[userId] - 사용자 예약 조회
  - POST /api/reservations - 예약 생성
  - PATCH /api/reservations/[id] - 예약 수정
  - DELETE /api/reservations/[id] - 예약 삭제
  - 인증 미들웨어 적용
  - 소유권 검증 미들웨어 적용
  - _Requirements: 1.1, 1.2, 1.3, 3.1, 3.2, 3.3, 3.4, 4.1, 4.2, 4.3, 4.4, 4.6, 5.1, 5.2, 5.3, 5.4, 8.1, 8.2, 8.3, 9.1, 9.2, 9.3, 9.4, 9.5_

- [x] 19.2 예약 API 통합 테스트 작성
  - GET /api/reservations 성공 테스트
  - POST /api/reservations 성공 테스트
  - POST /api/reservations 실패 테스트 (시간대 충돌)
  - POST /api/reservations 실패 테스트 (예약 제한 초과)
  - PATCH /api/reservations/[id] 성공 테스트 (소유자)
  - PATCH /api/reservations/[id] 실패 테스트 (타인)
  - DELETE /api/reservations/[id] 성공 테스트 (소유자)
  - DELETE /api/reservations/[id] 실패 테스트 (타인)
  - 관리자의 모든 예약 관리 성공 테스트
  - _Requirements: 3.1, 3.2, 3.3, 3.4, 4.1, 4.2, 4.3, 4.4, 4.6, 5.1, 5.2, 5.3, 5.4, 6.1, 6.2, 6.3, 7.1, 7.2, 7.3, 9.1, 9.2, 9.3, 9.4, 9.5_

- [x] 20. 대시보드 API Routes 구현
- [x] 20.1 대시보드 API 엔드포인트 생성
  - GET /api/dashboard - 대시보드 데이터 조회 (날짜 파라미터)
  - 인증 미들웨어 적용
  - _Requirements: 1.1, 1.2, 1.3, 1.4, 1.5, 1.6, 1.7, 2.1, 2.2, 2.5_

- [x] 20.2 대시보드 API 통합 테스트 작성
  - GET /api/dashboard 성공 테스트
  - 날짜 파라미터 검증 테스트
  - 인증 없이 접근 시 401 오류 테스트
  - _Requirements: 1.1, 1.2, 1.3, 1.4, 1.5, 1.6, 1.7, 2.1, 2.2, 2.5_

- [x] 21. 오류 처리 미들웨어 구현
- [x] 21.1 표준 오류 응답 생성 함수 구현
  - createErrorResponse 함수 구현
  - ErrorCode enum 정의
  - 오류 코드별 HTTP 상태 코드 매핑
  - _Requirements: All_

- [x] 21.2 전역 오류 처리 미들웨어 구현
  - 예상치 못한 오류 처리
  - 로깅 추가
  - 사용자 친화적 오류 메시지 생성
  - _Requirements: All_

- [x] 22. Checkpoint - API 레이어 검증
  - 모든 API 통합 테스트 통과 확인
  - Postman 또는 curl로 수동 API 테스트
  - 오류 처리 동작 확인
  - 질문이 있으면 사용자에게 문의

## Phase 8: UI 컴포넌트 구현

- [x] 23. Shadcn UI 컴포넌트 설치
  - Button, Input, Form, Dialog, Calendar, Toast 컴포넌트 설치
  - DatePicker 컴포넌트 설치
  - Card, Table 컴포넌트 설치
  - 필요한 모든 Shadcn 컴포넌트 설치
  - _Requirements: 15.1, 15.2, 15.3, 15.4_

- [x] 24. 인증 UI 구현
- [x] 24.1 로그인 페이지 구현
  - OAuth2 로그인 버튼 구현
  - 로그인 플로우 구현
  - 로그인 후 리다이렉트 처리
  - _Requirements: 13.1, 13.2, 13.3_

- [x] 24.2 인증 상태 관리 구현
  - 세션 상태 확인
  - 보호된 페이지 접근 제어
  - 로그아웃 기능 구현
  - _Requirements: 13.1, 13.2, 13.3, 13.4_

- [x] 25. 대시보드 UI 구현
- [x] 25.1 대시보드 레이아웃 구성
  - 메인 대시보드 페이지 생성 (app/dashboard/page.tsx)
  - 헤더 컴포넌트 (사용자 정보, 로그아웃)
  - 날짜 선택 컴포넌트
  - 회의실 목록 표시 영역
  - _Requirements: 1.1, 1.4, 2.1, 2.5_

- [x] 25.2 날짜 선택 컴포넌트 구현
  - DatePicker 컴포넌트 통합
  - 예약 가능 기간 제한 (0~30일)
  - 날짜 변경 시 대시보드 업데이트
  - 선택된 날짜 명확하게 표시
  - _Requirements: 2.1, 2.2, 2.3, 2.4, 2.5_

- [x] 25.3 회의실 예약 현황 표시 컴포넌트 구현
  - 회의실별 시간 슬롯 그리드 표시
  - 30분 단위 시간 슬롯 표시
  - 운영 시간 (08:00~20:00) 표시
  - 예약 가능/불가능 상태 시각적 구분
  - 회의실 정보 (이름, 수용 인원, 시설) 표시
  - _Requirements: 1.1, 1.2, 1.3, 1.4, 1.5, 1.6, 1.7_

- [x] 25.4 대시보드 데이터 로딩 및 새로고침 구현
  - Server Component로 초기 데이터 로드
  - 클라이언트 사이드 새로고침 기능
  - 로딩 상태 표시
  - _Requirements: 1.1, 1.5_

- [x] 26. 예약 생성 UI 구현
- [x] 26.1 예약 생성 폼 컴포넌트 구현
  - 빈 시간대 클릭 시 폼 표시
  - 예약 정보 입력 필드 (목적 등)
  - 시작/종료 시간 표시
  - 제출 버튼
  - _Requirements: 3.1_

- [x] 26.2 예약 생성 폼 검증 구현
  - Zod 스키마를 사용한 클라이언트 사이드 검증
  - 실시간 검증 피드백
  - 오류 메시지 표시
  - _Requirements: 3.2, 3.5, 3.6, 3.7, 3.8, 3.9, 3.10_

- [x] 26.3 예약 생성 Server Action 구현
  - 예약 생성 Server Action 함수
  - 서버 사이드 검증
  - 성공 시 대시보드 revalidate
  - 오류 처리 및 사용자 피드백
  - _Requirements: 3.2, 3.3, 3.4_

- [x] 27. 예약 수정/삭제 UI 구현
- [x] 27.1 예약 상세 및 수정 폼 구현
  - 예약 클릭 시 상세 정보 표시
  - 수정 폼 표시 (소유자 또는 관리자)
  - 현재 예약 정보 표시
  - 수정 가능한 필드 제공
  - _Requirements: 4.1, 9.1_

- [x] 27.2 예약 수정 Server Action 구현
  - 예약 수정 Server Action 함수
  - 소유권 검증
  - 서버 사이드 검증
  - 성공 시 대시보드 revalidate
  - 오류 처리 및 사용자 피드백
  - _Requirements: 4.2, 4.3, 4.4, 4.5, 4.6, 9.2, 9.5_

- [x] 27.3 예약 삭제 기능 구현
  - 삭제 버튼 (소유자 또는 관리자)
  - 삭제 확인 Dialog 표시
  - 예약 삭제 Server Action 함수
  - 성공 시 대시보드 revalidate
  - 오류 처리 및 사용자 피드백
  - _Requirements: 5.1, 5.2, 5.3, 5.4, 9.3, 9.4, 9.5_

- [x] 28. 관리자 회의실 관리 UI 구현
- [x] 28.1 회의실 관리 페이지 생성
  - 관리자 전용 페이지 (app/admin/rooms/page.tsx)
  - 회의실 목록 표시
  - 회의실 추가 버튼
  - 회의실 수정/삭제 버튼
  - _Requirements: 10.1, 11.1, 12.1_

- [x] 28.2 회의실 생성 폼 구현
  - 회의실 정보 입력 폼
  - Zod 스키마를 사용한 클라이언트 사이드 검증
  - 회의실 생성 Server Action 함수
  - 성공 시 목록 revalidate
  - 오류 처리 및 사용자 피드백
  - _Requirements: 10.1, 10.2, 10.3, 10.4, 10.5, 10.6, 10.7_

- [x] 28.3 회의실 수정 폼 구현
  - 회의실 정보 수정 폼
  - 현재 정보 표시
  - 회의실 수정 Server Action 함수
  - 성공 시 목록 revalidate
  - 오류 처리 및 사용자 피드백
  - _Requirements: 11.1, 11.2, 11.3, 11.4, 11.5, 11.6_

- [x] 28.4 회의실 삭제 기능 구현
  - 삭제 확인 Dialog 표시
  - 회의실 삭제 Server Action 함수
  - 활성 예약 확인 및 경고 메시지
  - 성공 시 목록 revalidate
  - 오류 처리 및 사용자 피드백
  - _Requirements: 12.1, 12.2, 12.3, 12.4, 12.5, 12.6_

- [x] 29. 반응형 디자인 구현
- [x] 29.1 모바일 레이아웃 최적화
  - Tailwind CSS 반응형 클래스 적용
  - 모바일 뷰포트에서 레이아웃 조정
  - 터치 인터랙션 최적화
  - _Requirements: 15.1, 15.3, 15.4_

- [x] 29.2 데스크톱 레이아웃 최적화
  - 데스크톱 뷰포트에서 레이아웃 조정
  - 넓은 화면 활용
  - _Requirements: 15.2, 15.3_

- [x] 30. Toast 알림 시스템 구현
  - Shadcn Toast 컴포넌트 통합
  - 성공/오류 메시지 표시
  - 자동 닫힘 기능
  - _Requirements: All_

- [ ] 31. Checkpoint - UI 컴포넌트 검증
  - 모든 페이지가 오류 없이 렌더링되는지 확인
  - 반응형 디자인 동작 확인 (모바일/데스크톱)
  - 사용자 플로우 수동 테스트
  - 질문이 있으면 사용자에게 문의

## Phase 9: E2E 통합 테스트

- [ ] 32. Playwright 설정 및 테스트 데이터 준비
- [ ] 32.1 Playwright 설정
  - playwright.config.ts 구성
  - 테스트 브라우저 설정 (Chromium, Firefox, WebKit)
  - 테스트 데이터베이스 설정
  - _Requirements: All_

- [ ] 32.2 테스트 데이터 생성 유틸리티 구현
  - 테스트용 사용자 생성 함수
  - 테스트용 회의실 생성 함수
  - 테스트용 예약 생성 함수
  - 테스트 데이터 정리 함수
  - _Requirements: All_

- [ ] 33. 인증 플로우 E2E 테스트
- [ ] 33.1 로그인 플로우 테스트
  - OAuth2 로그인 프로세스 테스트
  - 로그인 후 대시보드 리다이렉트 확인
  - 세션 유지 확인
  - _Requirements: 13.1, 13.2, 13.3, 13.4_

- [ ] 33.2 로그아웃 및 접근 제어 테스트
  - 로그아웃 기능 테스트
  - 로그아웃 후 보호된 페이지 접근 차단 확인
  - 인증 없이 API 접근 시 401 오류 확인
  - _Requirements: 13.1, 13.2, 13.3_

- [ ] 34. 대시보드 조회 플로우 E2E 테스트
- [ ] 34.1 대시보드 로드 테스트
  - 대시보드 페이지 로드 확인
  - 모든 회의실 표시 확인
  - 시간 슬롯 표시 확인 (30분 단위, 08:00~20:00)
  - 예약 현황 표시 확인
  - _Requirements: 1.1, 1.2, 1.3, 1.4, 1.5, 1.6, 1.7_

- [ ] 34.2 날짜 선택 테스트
  - 날짜 선택 인터페이스 동작 확인
  - 날짜 변경 시 예약 현황 업데이트 확인
  - 예약 가능 기간 제한 확인 (0~30일)
  - 범위 외 날짜 선택 시 오류 메시지 확인
  - _Requirements: 2.1, 2.2, 2.3, 2.4, 2.5_

- [ ] 35. 예약 생성 플로우 E2E 테스트
- [ ] 35.1 예약 생성 성공 시나리오
  - 빈 시간대 클릭
  - 예약 폼 표시 확인
  - 예약 정보 입력
  - 제출 버튼 클릭
  - 성공 메시지 확인
  - 대시보드에 예약 즉시 반영 확인
  - _Requirements: 3.1, 3.2, 3.3, 3.4_

- [ ] 35.2 예약 생성 실패 시나리오
  - 시간대 충돌 시 오류 메시지 확인
  - 예약 제한 초과 시 오류 메시지 확인
  - 유효하지 않은 시간 입력 시 오류 메시지 확인
  - _Requirements: 3.8, 3.10, 6.3, 7.3_

- [ ] 36. 예약 수정 플로우 E2E 테스트
- [ ] 36.1 예약 수정 성공 시나리오
  - 자신의 예약 클릭
  - 수정 폼 표시 확인
  - 예약 정보 수정
  - 제출 버튼 클릭
  - 성공 메시지 확인
  - 대시보드에 변경 사항 즉시 반영 확인
  - _Requirements: 4.1, 4.2, 4.3, 4.4_

- [ ] 36.2 예약 수정 실패 시나리오
  - 타인 예약 수정 시도 시 권한 오류 확인
  - 시간대 충돌 시 오류 메시지 확인
  - _Requirements: 4.6, 7.3_

- [ ] 37. 예약 삭제 플로우 E2E 테스트
- [ ] 37.1 예약 삭제 성공 시나리오
  - 자신의 예약 선택
  - 삭제 버튼 클릭
  - 삭제 확인 Dialog 표시 확인
  - 확인 버튼 클릭
  - 성공 메시지 확인
  - 대시보드에서 예약 제거 확인
  - 시간대가 예약 가능 상태로 변경 확인
  - _Requirements: 5.1, 5.2, 5.3_

- [ ] 37.2 예약 삭제 실패 시나리오
  - 타인 예약 삭제 시도 시 권한 오류 확인
  - _Requirements: 5.4_

- [ ] 38. 관리자 회의실 관리 플로우 E2E 테스트
- [ ] 38.1 회의실 생성 시나리오
  - 관리자로 로그인
  - 회의실 관리 페이지 접근
  - 회의실 추가 버튼 클릭
  - 회의실 정보 입력
  - 제출 버튼 클릭
  - 성공 메시지 확인
  - 대시보드에 새 회의실 즉시 표시 확인
  - _Requirements: 10.1, 10.2, 10.3, 10.4_

- [ ] 38.2 회의실 수정 시나리오
  - 회의실 선택
  - 수정 폼 표시 확인
  - 회의실 정보 수정
  - 제출 버튼 클릭
  - 성공 메시지 확인
  - 변경 사항 반영 확인
  - _Requirements: 11.1, 11.2, 11.3, 11.4_

- [ ] 38.3 회의실 삭제 시나리오
  - 활성 예약 없는 회의실 선택
  - 삭제 버튼 클릭
  - 삭제 확인 Dialog 표시 확인
  - 확인 버튼 클릭
  - 성공 메시지 확인
  - 대시보드에서 회의실 제거 확인
  - _Requirements: 12.1, 12.2, 12.3, 12.4_

- [ ] 38.4 회의실 삭제 실패 시나리오
  - 활성 예약 있는 회의실 선택
  - 삭제 시도
  - 경고 메시지 확인 (예약 개수 포함)
  - 삭제 거부 확인
  - _Requirements: 12.5, 12.6_

- [ ] 39. 관리자 예약 관리 플로우 E2E 테스트
- [ ] 39.1 모든 사용자 예약 조회 시나리오
  - 관리자로 로그인
  - 대시보드에서 모든 예약 표시 확인
  - 예약자 정보 표시 확인
  - 예약 상세 정보 확인
  - _Requirements: 8.1, 8.2, 8.3_

- [ ] 39.2 타 사용자 예약 관리 시나리오
  - 타 사용자 예약 선택
  - 수정 가능 확인
  - 예약 수정 성공 확인
  - 삭제 가능 확인
  - 예약 삭제 성공 확인
  - _Requirements: 9.1, 9.2, 9.3, 9.4, 9.5_

- [ ] 40. 권한 검증 플로우 E2E 테스트
- [ ] 40.1 일반 사용자 권한 제한 테스트
  - 일반 사용자로 로그인
  - 회의실 관리 페이지 접근 차단 확인
  - 타인 예약 수정 시도 차단 확인
  - 타인 예약 삭제 시도 차단 확인
  - _Requirements: 14.2, 14.3, 14.4_

- [ ] 40.2 관리자 권한 허용 테스트
  - 관리자로 로그인
  - 모든 관리 기능 접근 가능 확인
  - 모든 예약 관리 가능 확인
  - _Requirements: 14.5_

- [ ] 41. 동시성 테스트
- [ ] 41.1 동시 예약 시도 테스트
  - 두 개의 브라우저 세션 생성
  - 동일한 시간대에 동시 예약 시도
  - 한 명만 성공 확인
  - 다른 한 명은 충돌 오류 수신 확인
  - _Requirements: 7.1, 7.2, 7.3, 7.4_

- [ ] 42. 반응형 디자인 E2E 테스트
- [ ] 42.1 모바일 뷰포트 테스트
  - 모바일 뷰포트 설정
  - 모든 페이지 렌더링 확인
  - 모든 핵심 기능 접근 가능 확인
  - 터치 인터랙션 동작 확인
  - _Requirements: 15.1, 15.3, 15.4_

- [ ] 42.2 데스크톱 뷰포트 테스트
  - 데스크톱 뷰포트 설정
  - 최적화된 레이아웃 확인
  - 모든 기능 동작 확인
  - _Requirements: 15.2, 15.3_

- [ ] 42.3 뷰포트 크기 변경 테스트
  - 뷰포트 크기 동적 변경
  - 레이아웃 자동 조정 확인
  - _Requirements: 15.3_

- [ ] 43. Checkpoint - E2E 테스트 검증
  - 모든 E2E 테스트 통과 확인
  - 크로스 브라우저 테스트 확인 (Chromium, Firefox, WebKit)
  - 질문이 있으면 사용자에게 문의

## Phase 10: 배포 및 최종 검증

- [ ] 44. AWS Amplify 배포 설정
- [ ] 44.1 Amplify 프로젝트 생성
  - AWS Amplify 콘솔에서 프로젝트 생성
  - Git 저장소 연결
  - 빌드 설정 구성
  - _Requirements: All_

- [ ] 44.2 환경 변수 설정
  - Amplify 환경 변수 설정
  - 데이터베이스 연결 정보
  - OAuth2 설정
  - 기타 필요한 환경 변수
  - _Requirements: All_

- [ ] 44.3 빌드 및 배포 파이프라인 구성
  - 빌드 명령 설정
  - 테스트 실행 설정
  - 배포 트리거 설정 (main 브랜치 푸시 시)
  - _Requirements: All_

- [ ] 45. 데이터베이스 마이그레이션 및 시드 데이터
- [ ] 45.1 프로덕션 데이터베이스 마이그레이션
  - Aurora MySQL Serverless v2 인스턴스 생성
  - Prisma 마이그레이션 실행
  - 데이터베이스 연결 확인
  - _Requirements: All_

- [ ] 45.2 초기 시드 데이터 생성
  - 관리자 계정 생성
  - 샘플 회의실 생성 (선택 사항)
  - _Requirements: All_

- [ ] 46. CI/CD 파이프라인 구성
- [ ] 46.1 GitHub Actions 워크플로우 생성
  - 린트 및 타입 체크 단계
  - 단위 테스트 실행 단계
  - Property-based 테스트 실행 단계 (design.md에 명시된 반복 횟수 사용)
  - 통합 테스트 실행 단계
  - 코드 커버리지 확인 단계 (80% 이상)
  - _Requirements: All_

- [ ] 46.2 Pre-commit 훅 설정
  - Husky 설치 및 설정
  - 커밋 전 린트 실행
  - 커밋 전 타입 체크 실행
  - _Requirements: All_

- [ ] 47. 프로덕션 배포 및 스모크 테스트
- [ ] 47.1 프로덕션 배포
  - Amplify를 통한 프로덕션 배포
  - 배포 성공 확인
  - 애플리케이션 접근 확인
  - _Requirements: All_

- [ ] 47.2 스모크 테스트 실행
  - 로그인 기능 동작 확인
  - 대시보드 로드 확인
  - 예약 생성 기능 동작 확인
  - API 엔드포인트 응답 확인
  - _Requirements: All_

- [ ] 47.3 헬스 체크 엔드포인트 구현 및 확인
  - GET /api/health 엔드포인트 생성
  - 데이터베이스 연결 확인
  - 서비스 상태 반환
  - _Requirements: All_

- [ ] 48. 모니터링 및 로깅 설정
- [ ] 48.1 로깅 설정
  - 구조화된 로그 형식 설정
  - 오류 로그 수집
  - 성능 메트릭 로깅
  - _Requirements: All_

- [ ] 48.2 모니터링 대시보드 설정 (선택 사항)
  - AWS CloudWatch 설정
  - 주요 메트릭 모니터링
  - 알림 설정
  - _Requirements: All_

- [ ] 49. 문서화
- [ ] 49.1 README 작성
  - 프로젝트 개요
  - 설치 및 실행 방법
  - 환경 변수 설정 가이드
  - 테스트 실행 방법
  - _Requirements: All_

- [ ] 49.2 API 문서 작성
  - API 엔드포인트 목록
  - 요청/응답 형식
  - 오류 코드 설명
  - 인증 방법
  - _Requirements: All_

- [ ] 49.3 사용자 가이드 작성 (선택 사항)
  - 로그인 방법
  - 예약 생성/수정/삭제 방법
  - 관리자 기능 사용 방법
  - _Requirements: All_

- [ ] 50. 최종 Checkpoint - 전체 시스템 검증
  - 모든 단위 테스트 통과 확인
  - design.md에 명시된 반복 횟수로 모든 property test 실행 및 통과 확인
  - 모든 통합 테스트 통과 확인
  - 모든 E2E 테스트 통과 확인
  - 코드 커버리지 80% 이상 확인
  - 프로덕션 환경에서 모든 기능 동작 확인
  - 모든 요구사항 구현 완료 확인
  - 질문이 있으면 사용자에게 문의

## 완료!

모든 작업이 완료되면 사내 회의실 예약 시스템이 프로덕션 환경에서 정상적으로 동작합니다.

### 주요 성과물
- ✅ Next.js 15 기반 풀스택 애플리케이션
- ✅ Prisma + Aurora MySQL Serverless v2 데이터베이스
- ✅ OAuth2 인증 및 역할 기반 접근 제어
- ✅ 반응형 UI (Shadcn + Tailwind CSS)
- ✅ 포괄적인 테스트 커버리지 (Unit, Property-Based, Integration, E2E)
- ✅ AWS Amplify를 통한 자동 배포
- ✅ CI/CD 파이프라인

### 검증된 요구사항
- ✅ 16개 요구사항 모두 구현 및 테스트 완료
- ✅ 15개 Correctness Properties 모두 property-based test로 검증
- ✅ 모든 사용자 시나리오 E2E 테스트 완료
