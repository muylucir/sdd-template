# Requirements Document

## Introduction

본 문서는 사내 회의실 예약 시스템의 요구사항을 정의합니다. 현재 회의실 예약이 수동으로 이루어지면서 중복 예약이나 예약 누락이 빈번하게 발생하고 있습니다. 이러한 문제를 해결하기 위해 회사 내 모든 구성원이 실시간으로 회의실 사용 현황을 파악하고 손쉽게 예약할 수 있는 웹 기반 시스템을 구축하고자 합니다.

본 시스템은 직관적인 대시보드를 통해 회의실 예약 현황을 시각적으로 제공하며, 사용자가 원하는 날짜와 시간대에 회의실을 예약, 수정, 취소할 수 있는 기능을 제공합니다. 또한 관리자와 일반 사용자를 구분하는 권한 관리 체계를 통해 회의실 자원을 효율적으로 관리할 수 있도록 지원합니다.

본 시스템의 핵심 가치는 회의실 예약에 소요되는 시간을 최소화하고, 예약 충돌을 방지하여 구성원들이 본연의 업무에 집중할 수 있도록 하는 것입니다. 웹 기반 반응형 디자인을 적용하여 데스크톱과 모바일 환경 모두에서 접근성을 보장합니다.

## Glossary

- **System**: 사내 회의실 예약 관리 시스템
- **User**: 시스템을 사용하는 회사 내 일반 구성원으로, 회의실 예약 현황을 조회하고 자신의 예약을 생성, 수정, 취소할 수 있는 사용자
- **Administrator**: 시스템 관리 권한을 가진 사용자로, 모든 사용자의 예약을 조회 및 관리할 수 있고, 회의실 정보를 등록, 수정, 삭제할 수 있는 사용자
- **Meeting Room**: 예약 가능한 회의 공간으로, 이름, 수용 인원, 시설 정보, 사용 가능 시간 등의 속성을 가짐
- **Reservation**: 특정 사용자가 특정 회의실을 특정 날짜와 시간대에 사용하기 위해 생성한 예약 정보
- **Dashboard**: 회의실 예약 현황을 시각적으로 표시하는 메인 화면으로, 날짜별 회의실별 예약 상태를 확인할 수 있는 인터페이스
- **Time Slot**: 회의실 예약의 최소 단위 시간으로, 30분 단위로 구성됨
- **Booking Period**: 예약 가능한 기간으로, 당일부터 최대 30일 이내
- **Operating Hours**: 회의실 예약 가능 시간대로, 08:00부터 20:00까지
- **Reservation Limit**: 한 사용자가 동시에 보유할 수 있는 최대 예약 개수 (3개)
- **Reservation Duration**: 회의실 예약 가능한 시간 길이로, 최소 30분에서 최대 2시간까지

## Requirements

### Requirement 1

**User Story:** User로서, 대시보드에서 모든 회의실의 예약 현황을 확인하고 싶습니다. 그래야 빠르게 사용 가능한 회의실을 찾을 수 있습니다.

#### Acceptance Criteria

1. WHEN User가 대시보드에 접근하면, THEN the System SHALL 모든 회의실의 현재 예약 상태를 표시해야 합니다
2. WHEN 예약 상태를 표시할 때, THEN the System SHALL 각 회의실의 시간대별 예약 현황을 시각적 형식으로 표시해야 합니다
3. WHEN User가 대시보드를 조회하면, THEN the System SHALL 각 시간대가 예약 가능한지 또는 예약된 상태인지 구분하여 표시해야 합니다
4. WHEN 대시보드가 로드되면, THEN the System SHALL 회의실 이름, 수용 인원, 시설 정보를 포함한 회의실 정보를 표시해야 합니다
5. WHEN User가 대시보드를 새로고침하면, THEN the System SHALL 예약 상태를 현재 상태로 업데이트하여 표시해야 합니다
6. WHEN 대시보드를 표시할 때, THEN the System SHALL 30분 단위의 Time Slot으로 시간대를 구분하여 표시해야 합니다
7. WHEN 대시보드를 표시할 때, THEN the System SHALL Operating Hours(08:00~20:00) 범위 내의 시간대만 표시해야 합니다

### Requirement 2

**User Story:** User로서, 대시보드에서 원하는 날짜로 이동하고 싶습니다. 그래야 미래의 회의실 예약 현황을 확인하고 예약할 수 있습니다.

#### Acceptance Criteria

1. WHEN User가 대시보드에 접근하면, THEN the System SHALL 날짜를 선택할 수 있는 인터페이스를 제공해야 합니다
2. WHEN User가 날짜를 선택하면, THEN the System SHALL 선택한 날짜의 회의실 예약 현황을 표시해야 합니다
3. WHEN User가 날짜를 선택할 때, THEN the System SHALL 오늘부터 30일 이내의 날짜만 선택 가능하도록 제한해야 합니다
4. WHEN User가 Booking Period를 벗어난 날짜를 선택하려고 하면, THEN the System SHALL 선택을 거부하고 안내 메시지를 표시해야 합니다
5. WHEN 날짜가 변경되면, THEN the System SHALL 선택된 날짜를 명확하게 표시해야 합니다

### Requirement 3

**User Story:** User로서, 비어있는 시간대에 회의실을 예약하고 싶습니다. 그래야 필요한 시간에 회의실을 사용할 수 있습니다.

#### Acceptance Criteria

1. WHEN User가 대시보드에서 예약 가능한 시간대를 클릭하면, THEN the System SHALL 예약 생성 폼을 표시해야 합니다
2. WHEN User가 예약 정보를 입력하고 제출하면, THEN the System SHALL 예약 정보의 유효성을 검증해야 합니다
3. WHEN 예약 정보가 유효하면, THEN the System SHALL 해당 회의실과 시간대에 Reservation을 생성해야 합니다
4. WHEN Reservation이 생성되면, THEN the System SHALL 대시보드에 예약 상태를 즉시 반영해야 합니다
5. WHEN User가 예약을 생성할 때, THEN the System SHALL 예약 시간이 30분 단위로 시작하고 종료되는지 검증해야 합니다
6. WHEN User가 예약을 생성할 때, THEN the System SHALL 예약 시간이 최소 30분 이상인지 검증해야 합니다
7. WHEN User가 예약을 생성할 때, THEN the System SHALL 예약 시간이 최대 2시간 이하인지 검증해야 합니다
8. WHEN 예약 시간이 Reservation Duration 범위를 벗어나면, THEN the System SHALL 예약 생성을 거부하고 오류 메시지를 표시해야 합니다
9. WHEN User가 예약을 생성할 때, THEN the System SHALL 예약 시간이 Operating Hours(08:00~20:00) 범위 내에 있는지 검증해야 합니다
10. WHEN 예약 시간이 Operating Hours를 벗어나면, THEN the System SHALL 예약 생성을 거부하고 오류 메시지를 표시해야 합니다

### Requirement 4

**User Story:** User로서, 내가 생성한 예약을 수정하고 싶습니다. 그래야 회의 일정 변경에 유연하게 대응할 수 있습니다.

#### Acceptance Criteria

1. WHEN User가 자신의 예약을 선택하면, THEN the System SHALL 예약 수정 폼을 현재 예약 정보와 함께 표시해야 합니다
2. WHEN User가 예약 정보를 수정하고 제출하면, THEN the System SHALL 수정된 정보의 유효성을 검증해야 합니다
3. WHEN 수정된 정보가 유효하면, THEN the System SHALL 예약 정보를 업데이트하고 변경 사항을 반영해야 합니다
4. WHEN 예약이 수정되면, THEN the System SHALL 대시보드에 변경된 예약 상태를 즉시 반영해야 합니다
5. WHEN User가 예약을 수정할 때, THEN the System SHALL Requirement 3의 모든 검증 규칙을 적용해야 합니다
6. WHEN User가 다른 사용자의 예약을 수정하려고 하면, THEN the System SHALL 수정을 거부하고 권한 오류 메시지를 표시해야 합니다

### Requirement 5

**User Story:** User로서, 내가 생성한 예약을 취소하고 싶습니다. 그래야 더 이상 필요하지 않은 회의실을 다른 사람이 사용할 수 있습니다.

#### Acceptance Criteria

1. WHEN User가 자신의 예약을 삭제하려고 선택하면, THEN the System SHALL 삭제 확인 대화상자를 표시해야 합니다
2. WHEN User가 삭제를 확인하면, THEN the System SHALL 해당 Reservation을 삭제해야 합니다
3. WHEN Reservation이 삭제되면, THEN the System SHALL 대시보드에서 해당 예약을 제거하고 시간대를 예약 가능 상태로 표시해야 합니다
4. WHEN User가 다른 사용자의 예약을 삭제하려고 하면, THEN the System SHALL 삭제를 거부하고 권한 오류 메시지를 표시해야 합니다

### Requirement 6

**User Story:** User로서, 동시에 너무 많은 예약을 생성하지 못하도록 제한받고 싶습니다. 그래야 회의실 자원이 공평하게 분배될 수 있습니다.

#### Acceptance Criteria

1. WHEN User가 새로운 예약을 생성하려고 하면, THEN the System SHALL 해당 User의 현재 활성 예약 개수를 확인해야 합니다
2. WHEN User의 활성 예약 개수가 Reservation Limit(3개) 미만이면, THEN the System SHALL 예약 생성을 허용해야 합니다
3. WHEN User의 활성 예약 개수가 Reservation Limit(3개)에 도달했으면, THEN the System SHALL 예약 생성을 거부하고 제한 안내 메시지를 표시해야 합니다
4. WHEN 활성 예약을 계산할 때, THEN the System SHALL 현재 시간 이후의 예약만 포함해야 합니다

### Requirement 7

**User Story:** User로서, 이미 예약된 시간대에는 중복 예약을 할 수 없어야 합니다. 그래야 예약 충돌을 방지할 수 있습니다.

#### Acceptance Criteria

1. WHEN User가 예약을 생성하거나 수정할 때, THEN the System SHALL 해당 회의실의 요청된 시간대에 기존 예약이 있는지 확인해야 합니다
2. WHEN 요청된 시간대에 기존 예약이 없으면, THEN the System SHALL 예약 생성 또는 수정을 허용해야 합니다
3. WHEN 요청된 시간대가 기존 예약과 겹치면, THEN the System SHALL 예약 생성 또는 수정을 거부하고 충돌 안내 메시지를 표시해야 합니다
4. WHEN 시간대 충돌을 검사할 때, THEN the System SHALL 시작 시간과 종료 시간이 겹치는 모든 경우를 감지해야 합니다

### Requirement 8

**User Story:** Administrator로서, 모든 사용자의 예약을 조회하고 싶습니다. 그래야 회의실 사용 현황을 전체적으로 파악하고 관리할 수 있습니다.

#### Acceptance Criteria

1. WHEN Administrator가 대시보드에 접근하면, THEN the System SHALL 모든 User의 예약 정보를 표시해야 합니다
2. WHEN 예약 정보를 표시할 때, THEN the System SHALL 각 예약의 예약자 정보를 포함하여 표시해야 합니다
3. WHEN Administrator가 예약을 조회하면, THEN the System SHALL 예약자 이름, 회의실, 날짜, 시간, 예약 목적 등의 상세 정보를 표시해야 합니다

### Requirement 9

**User Story:** Administrator로서, 모든 사용자의 예약을 수정하거나 취소하고 싶습니다. 그래야 긴급 상황이나 관리 목적으로 예약을 조정할 수 있습니다.

#### Acceptance Criteria

1. WHEN Administrator가 임의의 예약을 선택하면, THEN the System SHALL 해당 예약의 수정 폼을 표시해야 합니다
2. WHEN Administrator가 예약을 수정하고 제출하면, THEN the System SHALL 수정된 정보의 유효성을 검증하고 예약을 업데이트해야 합니다
3. WHEN Administrator가 예약을 삭제하려고 선택하면, THEN the System SHALL 삭제 확인 대화상자를 표시해야 합니다
4. WHEN Administrator가 삭제를 확인하면, THEN the System SHALL 해당 예약을 삭제해야 합니다
5. WHEN Administrator가 예약을 수정하거나 삭제할 때, THEN the System SHALL 예약 소유자와 관계없이 작업을 허용해야 합니다

### Requirement 10

**User Story:** Administrator로서, 새로운 회의실을 등록하고 싶습니다. 그래야 회사에 추가된 회의 공간을 시스템에 반영할 수 있습니다.

#### Acceptance Criteria

1. WHEN Administrator가 회의실 등록 기능에 접근하면, THEN the System SHALL 회의실 정보 입력 폼을 표시해야 합니다
2. WHEN Administrator가 회의실 정보를 입력하고 제출하면, THEN the System SHALL 회의실 이름, 수용 인원, 시설 정보가 입력되었는지 검증해야 합니다
3. WHEN 회의실 정보가 유효하면, THEN the System SHALL 새로운 Meeting Room을 생성해야 합니다
4. WHEN Meeting Room이 생성되면, THEN the System SHALL 대시보드에 새로운 회의실을 즉시 표시해야 합니다
5. WHEN 회의실 정보가 유효하지 않으면, THEN the System SHALL 등록을 거부하고 오류 메시지를 표시해야 합니다
6. WHEN Administrator가 회의실을 등록할 때, THEN the System SHALL 동일한 이름의 회의실이 이미 존재하는지 확인해야 합니다
7. WHEN 동일한 이름의 회의실이 이미 존재하면, THEN the System SHALL 등록을 거부하고 중복 안내 메시지를 표시해야 합니다

### Requirement 11

**User Story:** Administrator로서, 기존 회의실 정보를 수정하고 싶습니다. 그래야 회의실의 수용 인원이나 시설 변경 사항을 시스템에 반영할 수 있습니다.

#### Acceptance Criteria

1. WHEN Administrator가 회의실을 선택하면, THEN the System SHALL 회의실 수정 폼을 현재 정보와 함께 표시해야 합니다
2. WHEN Administrator가 회의실 정보를 수정하고 제출하면, THEN the System SHALL 수정된 정보의 유효성을 검증해야 합니다
3. WHEN 수정된 정보가 유효하면, THEN the System SHALL 회의실 정보를 업데이트해야 합니다
4. WHEN 회의실 정보가 수정되면, THEN the System SHALL 대시보드에 변경된 정보를 즉시 반영해야 합니다
5. WHEN Administrator가 회의실 이름을 수정할 때, THEN the System SHALL 변경하려는 이름이 다른 회의실과 중복되지 않는지 확인해야 합니다
6. WHEN 회의실 이름이 중복되면, THEN the System SHALL 수정을 거부하고 중복 안내 메시지를 표시해야 합니다

### Requirement 12

**User Story:** Administrator로서, 더 이상 사용하지 않는 회의실을 삭제하고 싶습니다. 그래야 시스템에서 불필요한 회의실을 제거하고 관리를 단순화할 수 있습니다.

#### Acceptance Criteria

1. WHEN Administrator가 회의실을 삭제하려고 선택하면, THEN the System SHALL 삭제 확인 대화상자를 표시해야 합니다
2. WHEN Administrator가 삭제를 확인하면, THEN the System SHALL 해당 회의실에 미래의 활성 예약이 있는지 확인해야 합니다
3. WHEN 회의실에 미래의 활성 예약이 없으면, THEN the System SHALL 해당 Meeting Room을 삭제해야 합니다
4. WHEN Meeting Room이 삭제되면, THEN the System SHALL 대시보드에서 해당 회의실을 제거해야 합니다
5. WHEN 회의실에 미래의 활성 예약이 있으면, THEN the System SHALL 삭제를 거부하고 경고 메시지를 표시해야 합니다
6. WHEN 삭제 경고 메시지를 표시할 때, THEN the System SHALL 해당 회의실에 남아있는 예약 개수를 포함해야 합니다

### Requirement 13

**User Story:** User로서, 시스템에 접근하기 위해 인증을 받고 싶습니다. 그래야 권한이 있는 사용자만 시스템을 사용할 수 있습니다.

#### Acceptance Criteria

1. WHEN User가 시스템에 접근하면, THEN the System SHALL 인증을 요구해야 합니다
2. WHEN User가 유효한 인증 정보를 제공하면, THEN the System SHALL 접근을 허용해야 합니다
3. WHEN User가 유효하지 않은 인증 정보를 제공하면, THEN the System SHALL 접근을 거부하고 오류 메시지를 표시해야 합니다
4. WHEN User가 인증에 성공하면, THEN the System SHALL 사용자의 역할(User 또는 Administrator)을 식별해야 합니다

### Requirement 14

**User Story:** User로서, 내 역할에 따라 적절한 기능만 사용하고 싶습니다. 그래야 권한이 없는 작업을 실수로 수행하는 것을 방지할 수 있습니다.

#### Acceptance Criteria

1. WHEN User가 작업을 수행하려고 하면, THEN the System SHALL 해당 User의 역할을 확인해야 합니다
2. WHEN 작업이 Administrator 권한을 요구하고 User가 Administrator가 아니면, THEN the System SHALL 작업을 거부하고 권한 오류 메시지를 표시해야 합니다
3. WHEN User가 일반 User 역할을 가지면, THEN the System SHALL 회의실 등록, 수정, 삭제 기능에 대한 접근을 차단해야 합니다
4. WHEN User가 일반 User 역할을 가지면, THEN the System SHALL 다른 사용자의 예약 수정 및 삭제 기능에 대한 접근을 차단해야 합니다
5. WHEN User가 Administrator 역할을 가지면, THEN the System SHALL 모든 관리 기능에 대한 접근을 허용해야 합니다

### Requirement 15

**User Story:** User로서, 모바일 기기에서도 시스템을 사용하고 싶습니다. 그래야 언제 어디서나 회의실을 예약하고 관리할 수 있습니다.

#### Acceptance Criteria

1. WHEN User가 모바일 기기에서 시스템에 접근하면, THEN the System SHALL 모바일 화면 크기에 최적화된 인터페이스를 표시해야 합니다
2. WHEN User가 데스크톱에서 시스템에 접근하면, THEN the System SHALL 데스크톱 화면 크기에 최적화된 인터페이스를 표시해야 합니다
3. WHEN 화면 크기가 변경되면, THEN the System SHALL 인터페이스를 자동으로 조정하여 표시해야 합니다
4. WHEN 모바일 인터페이스를 표시할 때, THEN the System SHALL 모든 핵심 기능(조회, 예약, 수정, 취소)에 접근 가능하도록 해야 합니다

### Requirement 16

**User Story:** User로서, 시스템이 한국 시간대를 기준으로 동작하기를 원합니다. 그래야 예약 시간이 혼동 없이 정확하게 표시됩니다.

#### Acceptance Criteria

1. WHEN System이 날짜와 시간을 표시할 때, THEN the System SHALL UTC+9 시간대를 기준으로 표시해야 합니다
2. WHEN User가 예약을 생성하거나 수정할 때, THEN the System SHALL 입력된 시간을 UTC+9 시간대로 해석해야 합니다
3. WHEN System이 현재 시간을 기준으로 판단할 때, THEN the System SHALL UTC+9 시간대의 현재 시간을 사용해야 합니다
4. WHEN System이 Booking Period를 계산할 때, THEN the System SHALL UTC+9 시간대를 기준으로 "오늘"과 "30일 후"를 계산해야 합니다
