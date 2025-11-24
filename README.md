# Kiro CLI 스펙 기반 개발 가이드

> 아이디어만 잘 쓰면 나머지는 복붙으로 끝!

## 🎯 핵심 요약

1. **idea.md 작성** ← 여기만 신경쓰면 됨
2. **프롬프트 5개 순서대로 복붙** ← 기계적으로 진행
3. **개발 시작** ← AI가 알아서 구현
4. **Vibe 방식으로 전환** ← 완성 후 자유롭게 수정/개선

---

## 📦 설치

```bash
curl -fsSL https://cli.kiro.dev/install | bash
cd my-project
kiro-cli
```

---

## 1단계: idea.md 작성 (중요!)

### 파일 위치
`.kiro/idea/idea.md`

### 템플릿

```markdown
## 1️⃣ 아이디어 소개

### 한 문장 요약
회의실 예약을 실시간으로 관리하는 대시보드

### 배경 (왜 이 아이디어인가?)
- 회의실 예약이 겹쳐서 혼란 발생
- 예약 현황을 한눈에 볼 수 없음
- 이메일/엑셀 기반은 실시간성이 떨어짐

### 핵심 가치
- 실시간 예약 현황 확인으로 충돌 방지
- 직관적인 UI로 빠른 예약

## 2️⃣ 구현 아이디어

### 기본 콘셉트
대시보드에서 회의실별 예약 현황을 타임라인으로 보고,
빈 시간대를 클릭해서 바로 예약. 모든 변경사항은 실시간 반영.

### 필요한 주요 기능
1. **예약 현황 대시보드**: 모든 회의실의 시간대별 예약 상태 표시
2. **예약 생성/수정/취소**: 간단한 폼으로 예약 관리
3. **실시간 동기화**: 다른 사람의 예약이 즉시 반영
4. **회의실 관리**: 관리자가 회의실 정보 관리

### 사용자와 시나리오
**사용자**:
- 일반 사용자: 예약 조회 및 관리
- 관리자: 회의실 정보 관리

**시나리오**:
1. 대시보드에서 원하는 날짜/시간의 빈 회의실 확인
2. 클릭해서 예약 폼 작성
3. 제출하면 즉시 대시보드에 반영
4. 다른 사용자 화면에도 실시간으로 표시

## 3️⃣ 기술 & 실현성

### 기술 스택 (생각하고 있는 것)
- **프레임워크**: Next.js 15, TypeScript
- **데이터베이스**: PostgreSQL
- **ORM**: Prisma
- **인증**: NextAuth.js
- **배포**: Vercel
```

### ✅ 잘 쓰는 법

| 항목 | ❌ 나쁜 예 | ✅ 좋은 예 |
|------|-----------|-----------|
| 한 문장 요약 | "좋은 시스템" | "회의실 예약을 실시간으로 관리하는 대시보드" |
| 배경 | "필요해서" | "회의실 예약이 겹쳐서 혼란 발생, 실시간 확인 불가" |
| 기능 | "편리한 기능들" | "1. 예약 대시보드 2. 예약 생성/수정 3. 실시간 동기화" |
| 기술 스택 | "웹으로" | "Next.js 15, TypeScript, PostgreSQL, Prisma" |

**핵심**: 구체적으로, 명확하게!

---

## 2단계: 프롬프트 5개 복붙

### Kiro CLI 기본 사용법

```bash
kiro-cli        # 채팅 시작
```

채팅에서:
```
You: /editor    # 에디터 열기
```

에디터가 열리면:
1. 프롬프트 템플릿 내용 복붙
2. `ESC` → `:wq` → `Enter` (저장하고 종료)

### 실행 순서

#### 프롬프트 1: Requirements 생성
```
You: /editor
[prompt-template-1-requirements.md 복붙]
[저장]
```
→ `.kiro/specs/requirements.md` 생성됨

#### 프롬프트 2: Design 생성
```
You: /editor
[prompt-template-2-design.md 복붙]
[저장]
```
→ `.kiro/specs/design.md` 생성됨

#### 프롬프트 3: Tasks 생성
```
You: /editor
[prompt-template-3-tasks.md 복붙]
[저장]
```
→ `.kiro/specs/tasks.md` 생성됨

#### 프롬프트 4: Steering 생성
```
You: /editor
[prompt-template-4-steering.md 복붙]
[저장]
```
→ `.kiro/steering/structure.md, tech.md, product.md` 생성됨

#### 프롬프트 5: 개발 시작
```
You: /editor
[prompt-template-5-development.md 복붙]
[저장]
```
→ AI가 tasks.md 보고 순서대로 구현 시작

---

## 3단계: 개발 진행

프롬프트 5 실행 후 AI가:

1. ✅ 모든 스펙 파일 읽음
2. ✅ tasks.md 1번부터 순서대로 실행
3. ✅ 코드 작성 + 테스트 작성
4. ✅ 완료된 작업 체크박스 업데이트
5. ✅ 다음 작업으로 자동 진행

### 중간에 할 일

**진행 상황 확인**:
```
You: 현재 어디까지 했어?
```

**문제 발생 시**:
```
You: 왜 테스트가 실패했어?
You: 다시 시도해줘
```

**특정 작업부터 시작**:
```
You: tasks.md의 5번 작업부터 시작해줘
```

**끝!**

---

## 4단계: Spec 완료 후 - Vibe 방식으로 전환

### 🎨 자유로운 수정과 개선

Spec 기반 개발로 기본 구조와 핵심 기능이 완성되면, 이제는 **vibe 방식**으로 자유롭게 수정하고 개선할 수 있습니다!

#### ⚠️ 중요: Context에 스펙 파일 추가 필수!

Vibe 방식으로 전환할 때, AI가 프로젝트 구조와 규칙을 이해할 수 있도록 **스펙 파일과 스티어링 파일을 context에 추가**해야 합니다.

**방법 1: 세션 컨텍스트 (임시 - 현재 대화에만 적용)**

```bash
kiro-cli

# 스펙 파일들 추가
You: /context add .kiro/specs/*.md

# 스티어링 파일들 추가
You: /context add .kiro/steering/*.md

# 확인
You: /context show
```

**방법 2: Agent 설정 (영구 - 권장)**

`.kiro/agent.json` 파일 생성:
```json
{
  "resources": [
    "file://.kiro/specs/requirements.md",
    "file://.kiro/specs/design.md",
    "file://.kiro/specs/tasks.md",
    "file://.kiro/steering/structure.md",
    "file://.kiro/steering/tech.md",
    "file://.kiro/steering/product.md"
  ]
}
```

이렇게 하면 모든 채팅 세션에서 자동으로 스펙을 참조합니다!

#### Vibe 방식이란?

- 📝 **스펙 없이 자연어로**: "이 버튼 색상 파란색으로 바꿔줘"
- 🎯 **즉흥적인 개선**: "여기 애니메이션 추가해줘"
- 🔄 **빠른 피드백 반영**: "이 부분 UI 좀 더 예쁘게 만들어줘"
- 💡 **창의적 실험**: "이 기능 다른 방식으로 구현해볼래?"

#### 왜 Spec 먼저, Vibe 나중에?

```
Spec 기반 개발 (초기)          Vibe 방식 (이후)
├─ 체계적 구조 확립      →    ├─ 세부 개선
├─ 핵심 기능 구현       →    ├─ UX/UI 향상
├─ 테스트 기반 안정성    →    ├─ 성능 최적화
└─ 완전한 문서화        →    └─ 새로운 아이디어 실험
```

**장점**:
- ✅ Spec으로 **탄탄한 기반** 확보
- ✅ Vibe로 **빠른 개선과 실험**
- ✅ 문서화된 스펙이 있어 **큰 변경도 안전**
- ✅ 필요하면 **언제든 스펙 업데이트** 가능

#### Vibe 방식 사용 예시

**Spec 개발 완료 후**:
```bash
kiro-cli

# 1. 스펙 파일을 context에 추가 (첫 세션에만)
You: /context add .kiro/specs/*.md
You: /context add .kiro/steering/*.md

# 2. 자유로운 요청
You: 로그인 페이지 디자인 좀 더 모던하게 바꿔줘
Kiro: [structure.md의 파일 규칙을 따라 수정]

You: 대시보드에 다크모드 추가해줘
Kiro: [tech.md의 스타일 가이드를 참고하여 구현]

You: 이 API 응답 속도 개선할 방법 있어?
Kiro: [design.md의 아키텍처를 고려하여 최적화]

You: 여기 로딩 인디케이터 추가해줘
Kiro: [즉시 수정/구현]
```

**왜 context 추가가 중요한가?**
- ✅ AI가 프로젝트 구조를 이해하고 올바른 위치에 파일 생성
- ✅ 기술 스택과 코딩 규칙을 준수
- ✅ 기존 아키텍처와 일관성 유지
- ✅ 더 정확하고 품질 높은 코드 생성

#### 주의사항

⚠️ **대규모 기능 추가 시**:
- Vibe 방식으로 빠르게 프로토타입
- 만족스러우면 → idea.md 업데이트 → 스펙 재생성
- 문서와 코드 동기화 유지

⚠️ **핵심 로직 변경 시**:
- requirements.md와 design.md 확인
- 정확성 속성(Property) 테스트 깨지지 않는지 확인
- 필요하면 스펙 문서 업데이트

#### 최적의 워크플로우

```
1. 새 프로젝트 시작
   └─ Spec 기반 개발 (프롬프트 1-5)

2. 핵심 기능 완성 ✅
   └─ Vibe 방식으로 전환

3. 작은 개선/수정
   └─ Vibe: "여기 고쳐줘", "저기 바꿔줘"

4. 큰 기능 추가 필요?
   └─ idea.md 업데이트 → Spec 재생성 → 개발

5. 다시 작은 개선
   └─ Vibe 방식 계속
```

**핵심**: Spec은 **구조와 안정성**을, Vibe는 **속도와 유연성**을 제공합니다!

---

## 📁 최종 디렉토리 구조

```
my-project/
├── .kiro/
│   ├── agent.json                   # Vibe 모드용 context 설정 (선택)
│   ├── idea/
│   │   └── idea.md                  # 직접 작성
│   ├── specs/
│   │   ├── requirements.md          # 프롬프트 1로 생성
│   │   ├── design.md                # 프롬프트 2로 생성
│   │   └── tasks.md                 # 프롬프트 3으로 생성
│   └── steering/
│       ├── structure.md             # 프롬프트 4로 생성
│       ├── tech.md                  # 프롬프트 4로 생성
│       └── product.md               # 프롬프트 4로 생성
└── [실제 코드]                       # 프롬프트 5로 생성
```

---

## 🎬 실전 예시: 시작부터 끝까지

```bash
# 1. Kiro CLI 시작
kiro-cli

# 2. idea.md 작성 (직접)
You: .kiro/idea/idea.md 파일을 만들어줘
[idea 내용 작성]

# 3. 프롬프트 1 실행
You: /editor
[prompt-template-1-requirements.md 복붙]
Kiro: requirements.md 생성 완료!

# 4. 프롬프트 2 실행
You: /editor
[prompt-template-2-design.md 복붙]
Kiro: design.md 생성 완료!

# 5. 프롬프트 3 실행
You: /editor
[prompt-template-3-tasks.md 복붙]
Kiro: tasks.md 생성 완료! 총 20개 작업

# 6. 프롬프트 4 실행
You: /editor
[prompt-template-4-steering.md 복붙]
Kiro: steering 문서 3개 생성 완료!

# 7. 프롬프트 5 실행 (개발 시작!)
You: /editor
[prompt-template-5-development.md 복붙]
Kiro: 작업 1 시작합니다...
      [코드 작성 중]
      작업 1 완료!
      작업 2 시작합니다...
      [계속 진행]

# 8. 나는 커피 마시면서 대기
You: [지켜보기만 하면 됨]

# 9. 개발 완료 후 - Vibe 모드로 전환
You: /context add .kiro/specs/*.md .kiro/steering/*.md
You: 로그인 페이지 좀 더 예쁘게 만들어줘
Kiro: [스펙을 참고하여 개선]
```

---

## 💡 팁

### idea.md 작성 팁

1. **구체적으로**: "편리한"보다 "실시간 동기화로 충돌 방지"
2. **기능 나열**: 최소 3-5개 주요 기능 명시
3. **시나리오 작성**: 실제 사용 흐름 1-2개
4. **기술 스택 명확히**: 프레임워크, DB, 배포 플랫폼 명시

### 프롬프트 실행 팁

1. **순서 지키기**: 1→2→3→4→5 순서 필수
2. **생성 확인**: 각 프롬프트 후 파일 생성 확인
3. **에러 시**: 프롬프트 다시 실행하면 됨

### 개발 진행 팁

1. **체크포인트 주의**: "모든 테스트 통과 확인" 나오면 확인 필요
2. **에러 발생 시**: AI에게 물어보고 수정 요청
3. **중간 저장**: 각 작업 완료마다 git commit 하는 게 좋음

---

## ❓ FAQ

**Q: idea.md만 수정하고 싶으면?**
A: 수정 후 프롬프트 1부터 다시 실행

**Q: 중간에 기능 추가하려면?**
A: idea.md 수정 → requirements.md 재생성 → design.md 재생성 → tasks.md 재생성

**Q: Spec 기반 개발 완료 후에는?**
A: Vibe 방식으로 전환! 단, `/context add .kiro/specs/*.md .kiro/steering/*.md` 로 스펙 파일 추가 필수

**Q: Vibe 모드에서 context 추가 안 하면?**
A: AI가 프로젝트 규칙을 모르니까 이상한 위치에 파일 만들거나 다른 스타일로 코드 작성할 수 있음. 반드시 추가 권장!

**Q: agent.json vs /context add 차이는?**
A: `/context add`는 임시(현재 세션만), `agent.json`은 영구(모든 세션). Vibe 자주 쓸거면 agent.json 권장

**Q: Spec 없이 Vibe만 사용하면 안 돼?**
A: 가능하지만, 프로젝트가 커질수록 구조가 흐트러짐. 초기엔 Spec으로 기반 다지고, 이후엔 Vibe로 개선하는 게 베스트

**Q: 프롬프트를 커스터마이징해도 되나?**
A: 가능하지만 구조는 유지 권장

**Q: Kiro CLI 말고 ChatGPT로도 가능?**
A: 가능! 파일 생성/관리만 직접 하면 됨

---

## 📌 치트시트

```bash
# Kiro CLI 기본
kiro-cli              # 시작
/editor              # 에디터 열기
Ctrl+C               # 종료

# Context 관리 (Vibe 모드 필수)
/context add .kiro/specs/*.md .kiro/steering/*.md   # 스펙 파일 추가
/context show                                       # 현재 context 확인
/context rm 파일명                                   # 파일 제거
/context clear                                      # 전체 초기화

# vi 에디터 (프롬프트 입력 시)
i                    # 입력 모드
ESC                  # 명령 모드
:wq                  # 저장하고 종료
:q!                  # 저장 안 하고 종료

# 워크플로우
1. idea.md 작성
2. /editor → 프롬프트 1 복붙
3. /editor → 프롬프트 2 복붙
4. /editor → 프롬프트 3 복붙
5. /editor → 프롬프트 4 복붙
6. /editor → 프롬프트 5 복붙
7. AI가 자동 구현
8. Spec 완료 후 → Vibe 방식으로 자유롭게 수정/개선
```

---

## 🚀 시작하기

```bash
# 1. 설치
curl -fsSL https://cli.kiro.dev/install | bash

# 2. 프로젝트 폴더 생성
mkdir my-awesome-project
cd my-awesome-project

# 3. Kiro CLI 시작
kiro-cli

# 4. idea.md 작성하고 프롬프트 5개 복붙
# 5. 완성! 이후엔 Vibe 방식으로 자유롭게 개선
```

**끝! 이게 전부입니다.** 🎉

---

## 참고 링크

- [Kiro CLI 공식 문서](https://kiro.dev/docs/cli/)
- [Context 관리 가이드](https://kiro.dev/docs/cli/chat/context/)
- 프롬프트 템플릿: `prompt-template-{1-5}.md`

---

**버전**: 2.2.0 (Simple Edition + Vibe 통합 + Context 관리)
**업데이트**: 2024-11-24
