# Product Requirements Document (PRD)
# Web Mobile Scientific Calculator

![Reference Design](file:///C:/Users/WIN/.gemini/antigravity/brain/b7712733-7749-4482-a62b-5871558e9a29/screen.png)

## 1. Product Overview

### 1.1 Product Vision
모바일 웹 환경에 최적화된 현대적이고 직관적인 공학용 계산기를 개발합니다. 사용자가 일반 계산과 과학 계산을 원활하게 수행할 수 있도록 하며, 다크 모드를 지원하여 다양한 환경에서 편안한 사용 경험을 제공합니다.

### 1.2 Target Users
- 학생 (중고등학생, 대학생)
- 엔지니어 및 과학자
- 일반 사용자 (기본 계산 필요)
- 모바일 기기를 주로 사용하는 사용자

### 1.3 Key Value Propositions
- **모바일 최적화**: 터치 인터페이스에 최적화된 반응형 디자인
- **현대적 UI/UX**: 깔끔하고 직관적인 인터페이스, 다크 모드 지원
- **과학 계산 기능**: 삼각함수, 로그, 지수 등 다양한 과학 계산 지원
- **계산 이력**: 이전 계산 내용 확인 가능
- **빠른 접근성**: 웹 기반으로 설치 없이 즉시 사용 가능

---

## 2. Core Features

### 2.1 Display System

#### 2.1.1 Dual Display
- **수식 표시 영역** (Expression Display)
  - 현재 입력 중인 수식 또는 이전 계산식 표시
  - 예: `(12 + 5) × log(10)`
  - 스크롤 가능한 가로 영역
  - 텍스트 색상: 회색 (보조 정보 강조)
  
- **결과 표시 영역** (Result Display)
  - 계산 결과를 큰 폰트로 표시
  - 텍스트 크기: 6xl ~ 7xl (반응형)
  - 가로 스크롤 지원 (긴 숫자 처리)
  - 텍스트 색상: 기본 텍스트 색상 (강조)

#### 2.1.2 Display Specifications
- 우측 정렬 (Right-aligned)
- 자동 폰트 크기 조정 (선택적)
- 오버플로우 처리: 가로 스크롤
- 최소 높이 보장으로 레이아웃 안정성 확보

---

### 2.2 Input System - Button Layout

#### 2.2.1 Mode Toggle (각도 단위 선택)
- **위치**: 상단 좌측
- **옵션**: 
  - RAD (라디안)
  - DEG (도) - 기본값
- **UI 타입**: Segmented Control
- **스타일**: 
  - 배경: 밝은 표면 색상
  - 선택된 항목: 강조 배경 + 그림자
  - 전환 애니메이션

#### 2.2.2 Scientific Helper Buttons (상단 우측)
빠른 접근을 위한 주요 과학 함수:
- **√** (제곱근)
- **π** (파이)
- **^** (거듭제곱)
- **!** (팩토리얼)

**스타일**: 
- 작은 크기 (h-10)
- 둥근 모서리
- 표면 색상 배경
- 호버 효과

#### 2.2.3 Main Keypad Grid (4×6 레이아웃)

**Row 1: 삼각함수 및 로그**
| sin | cos | tan | ln |

**Row 2: 괄호 및 연산자**
| ( | ) | log | ÷ |

**Row 3: 숫자 7-9 및 곱셈**
| 7 | 8 | 9 | × |

**Row 4: 숫자 4-6 및 뺄셈**
| 4 | 5 | 6 | - |

**Row 5: 숫자 1-3 및 덧셈**
| 1 | 2 | 3 | + |

**Row 6: 제어 버튼**
| AC | 0 | . | = |

#### 2.2.4 Button Styling Categories

**1. 숫자 버튼 (0-9, .)**
- 크기: h-16 ~ h-20 (반응형)
- 배경: 밝은 표면 (라이트 모드) / 어두운 표면 (다크 모드)
- 텍스트: 2xl, 중간 굵기
- 둥근 모서리: 2xl
- 그림자: 미세
- 호버: 밝기 변화

**2. 연산자 버튼 (+, -, ×, ÷)**
- 크기: h-16 ~ h-20
- 배경: 기본 색상의 10% 투명도
- 텍스트: 기본 색상 (파란색), 2xl, 굵게
- 호버: 20% 투명도로 증가

**3. 과학 함수 버튼 (sin, cos, tan, ln, log, (, ))**
- 크기: h-14 ~ h-16
- 배경: 표면 강조 색상
- 텍스트: 보조 텍스트 색상, sm ~ base
- 둥근 모서리: xl
- 테두리: 라이트 모드에서만 표시

**4. AC 버튼 (All Clear)**
- 크기: h-16 ~ h-20
- 배경: 밝은 표면
- 텍스트: 빨간색, xl, 굵게
- 호버: 빨간색 배경 (투명도)

**5. = 버튼 (Equals)**
- 크기: h-16 ~ h-20
- 배경: 기본 색상 (파란색)
- 텍스트: 흰색, 2xl, 굵게
- 그림자: 기본 색상 그림자
- 호버: 더 진한 파란색

#### 2.2.5 Backspace Button
- **위치**: 디스플레이 영역 우측 상단에 오버레이
- **아이콘**: Material Symbols - backspace
- **색상**: 기본 색상 (파란색)
- **크기**: w-12, h-10
- **호버**: 밝은 파란색

---

### 2.3 Calculation Engine

#### 2.3.1 Basic Operations
- 덧셈 (+)
- 뺄셈 (-)
- 곱셈 (×)
- 나눗셈 (÷)

#### 2.3.2 Scientific Functions
- **삼각함수**: sin, cos, tan
- **역삼각함수**: sin⁻¹, cos⁻¹, tan⁻¹ (2nd 기능)
- **로그**: log (밑 10), ln (자연로그)
- **지수**: e^x, 10^x
- **거듭제곱**: x^y
- **제곱근**: √x
- **팩토리얼**: x!
- **상수**: π (파이), e (자연상수)

#### 2.3.3 Advanced Features
- **괄호 처리**: 중첩 괄호 지원
- **연산 우선순위**: 수학적 연산 순서 준수
- **각도 단위**: RAD/DEG 전환
- **오류 처리**: 
  - 0으로 나누기
  - 도메인 오류 (예: 음수의 제곱근)
  - 구문 오류

---

### 2.4 History Feature

#### 2.4.1 History Access
- **위치**: 헤더 우측 상단
- **아이콘**: Material Symbols - history
- **동작**: 클릭 시 계산 이력 패널 표시

#### 2.4.2 History Display
- 최근 계산 내역 목록
- 각 항목: 수식 + 결과
- 항목 클릭 시 재사용 가능
- 이력 삭제 기능

---

### 2.5 Theme System

#### 2.5.1 Light Mode
- **배경**: #f6f7f8 (밝은 회색)
- **표면**: 흰색
- **텍스트**: 어두운 회색 (#0f172a)
- **테두리**: 밝은 회색 테두리

#### 2.5.2 Dark Mode
- **배경**: #101922 (매우 어두운 파란 회색)
- **표면**: #1E2630 (어두운 표면)
- **표면 강조**: #283039 (약간 밝은 표면)
- **텍스트**: 흰색
- **테두리**: 없음 (그림자로 대체)

#### 2.5.3 Theme Toggle
- 시스템 설정 자동 감지 (prefers-color-scheme)
- 수동 전환 옵션 (선택적 구현)

---

## 3. Technical Specifications

### 3.1 Technology Stack

#### 3.1.1 Frontend
- **HTML5**: 시맨틱 마크업
- **CSS**: Tailwind CSS (CDN)
- **JavaScript**: Vanilla JS (계산 로직)
- **폰트**: 
  - Inter (UI 텍스트)
  - Material Symbols Outlined (아이콘)

#### 3.1.2 Responsive Design
- **모바일 우선**: 320px ~ 768px
- **태블릿**: 768px ~ 1024px
- **데스크톱**: 1024px+
- **뷰포트 단위**: dvh (동적 뷰포트 높이)

### 3.2 Design System

#### 3.2.1 Color Palette
```css
primary: #137fec (파란색)
background-light: #f6f7f8
background-dark: #101922
surface-dark: #1E2630
surface-accent: #283039
```

#### 3.2.2 Typography
- **폰트 패밀리**: Inter, sans-serif
- **크기**:
  - 헤더: xl (20px)
  - 수식: lg (18px)
  - 결과: 6xl ~ 7xl (60px ~ 72px)
  - 버튼: sm ~ 2xl

#### 3.2.3 Spacing & Layout
- **패딩**: 4 (1rem), 6 (1.5rem)
- **간격**: 2 ~ 4 (0.5rem ~ 1rem)
- **둥근 모서리**: 
  - 기본: 0.25rem
  - lg: 0.5rem
  - xl: 0.75rem
  - 2xl: 1rem

### 3.3 Interaction Design

#### 3.3.1 Touch Optimization
- **최소 터치 영역**: 44px × 44px
- **버튼 크기**: 56px ~ 80px (h-14 ~ h-20)
- **간격**: 12px ~ 16px

#### 3.3.2 Animations & Transitions
- **버튼 호버**: 배경색 전환 (0.2s)
- **버튼 활성**: scale(0.96) + 빠른 전환 (0.05s)
- **모드 전환**: 부드러운 배경 전환
- **테마 전환**: 색상 전환 애니메이션

#### 3.3.3 Feedback
- **시각적**: 호버 상태, 활성 상태
- **색상 변화**: 연산자 강조
- **그림자**: 깊이 표현

---

## 4. User Experience Flow

### 4.1 Basic Calculation Flow
1. 사용자가 숫자 버튼 클릭
2. 디스플레이에 숫자 표시
3. 연산자 버튼 클릭
4. 다음 숫자 입력
5. = 버튼 클릭
6. 결과 표시

### 4.2 Scientific Calculation Flow
1. 과학 함수 버튼 클릭 (예: sin)
2. 괄호 자동 추가 또는 숫자 입력 대기
3. 숫자 입력
4. 필요시 괄호 닫기
5. = 버튼 클릭
6. 결과 표시

### 4.3 Error Handling Flow
1. 잘못된 입력 감지
2. 오류 메시지 표시 ("Error", "Math Error" 등)
3. AC 버튼으로 초기화

### 4.4 History Flow
1. History 아이콘 클릭
2. 이력 패널 슬라이드 인
3. 항목 선택 시 수식 재사용
4. 패널 닫기

---

## 5. Functional Requirements

### 5.1 Must Have (P0)
- [x] 기본 사칙연산 (+, -, ×, ÷)
- [x] 숫자 입력 (0-9, 소수점)
- [x] AC (전체 삭제) 기능
- [x] = (계산 실행) 기능
- [x] 디스플레이 (수식 + 결과)
- [x] 반응형 레이아웃 (모바일 우선)
- [x] 다크 모드 지원
- [x] 삼각함수 (sin, cos, tan)
- [x] 로그 함수 (log, ln)
- [x] 괄호 처리
- [x] RAD/DEG 모드 전환

### 5.2 Should Have (P1)
- [ ] Backspace (한 글자 삭제) 기능
- [ ] 계산 이력 기능
- [ ] 거듭제곱 (^) 기능
- [ ] 제곱근 (√) 기능
- [ ] 팩토리얼 (!) 기능
- [ ] π, e 상수
- [ ] 키보드 입력 지원

### 5.3 Could Have (P2)
- [ ] 2nd 기능 (역삼각함수 등)
- [ ] 메모리 기능 (M+, M-, MR, MC)
- [ ] 계산 이력 저장 (로컬 스토리지)
- [ ] 테마 수동 전환 토글
- [ ] 햅틱 피드백 (모바일)
- [ ] 음성 입력 (선택적)

### 5.4 Won't Have (현재 버전)
- 그래프 기능
- 프로그래밍 모드 (진법 변환)
- 통계 계산
- 단위 변환

---

## 6. Non-Functional Requirements

### 6.1 Performance
- **초기 로딩 시간**: < 2초
- **계산 응답 시간**: < 100ms
- **애니메이션 프레임레이트**: 60fps
- **번들 크기**: < 500KB (Tailwind CDN 제외)

### 6.2 Compatibility
- **브라우저**: 
  - Chrome/Edge (최신 2개 버전)
  - Safari (최신 2개 버전)
  - Firefox (최신 2개 버전)
- **모바일 OS**:
  - iOS 14+
  - Android 10+
- **화면 크기**: 320px ~ 2560px

### 6.3 Accessibility
- **키보드 네비게이션**: 전체 기능 접근 가능
- **스크린 리더**: ARIA 레이블 지원
- **색상 대비**: WCAG AA 준수
- **터치 영역**: 최소 44px × 44px

### 6.4 Usability
- **학습 곡선**: 5분 이내 기본 사용 가능
- **직관성**: 표준 계산기 레이아웃 준수
- **오류 복구**: 명확한 오류 메시지 + AC 버튼

---

## 7. Design Specifications

### 7.1 Layout Structure
```
┌─────────────────────────────────┐
│ Header (Standard | History)     │
├─────────────────────────────────┤
│                                 │
│  Display Area                   │
│  - Expression (작게)            │
│  - Result (크게)                │
│                                 │
├─────────────────────────────────┤
│ [RAD|DEG]  [√][π][^][!]        │
├─────────────────────────────────┤
│ [sin][cos][tan][ln]             │
│ [ ( ][ ) ][log][÷]              │
│ [ 7 ][ 8 ][ 9 ][×]              │
│ [ 4 ][ 5 ][ 6 ][-]              │
│ [ 1 ][ 2 ][ 3 ][+]              │
│ [AC ][ 0 ][ . ][=]              │
└─────────────────────────────────┘
```

### 7.2 Component Hierarchy
```
App
├── Header
│   ├── Title ("Standard")
│   └── HistoryButton
├── Display
│   ├── ExpressionDisplay
│   ├── ResultDisplay
│   └── BackspaceButton (overlay)
├── Controls
│   ├── ModeToggle (RAD/DEG)
│   ├── ScientificHelpers (√, π, ^, !)
│   └── Keypad (4×6 grid)
└── HistoryPanel (conditional)
```

### 7.3 Visual Hierarchy
1. **결과 (가장 강조)**: 큰 폰트, 진한 색상
2. **수식 (보조 정보)**: 작은 폰트, 회색
3. **= 버튼 (주요 액션)**: 파란색 배경, 그림자
4. **연산자 (강조)**: 파란색 텍스트
5. **숫자 (기본)**: 중립 색상
6. **과학 함수 (보조)**: 작은 크기, 회색 텍스트

---

## 8. Implementation Phases

### Phase 1: Core Foundation (Week 1)
- [ ] 프로젝트 구조 설정
- [ ] HTML 마크업 (레이아웃)
- [ ] Tailwind CSS 설정 및 디자인 시스템
- [ ] 기본 UI 구현 (버튼, 디스플레이)
- [ ] 다크 모드 구현

### Phase 2: Basic Calculator (Week 2)
- [ ] 숫자 입력 로직
- [ ] 기본 사칙연산 엔진
- [ ] AC, = 버튼 기능
- [ ] 디스플레이 업데이트 로직
- [ ] 소수점 처리

### Phase 3: Scientific Functions (Week 3)
- [ ] 삼각함수 구현 (sin, cos, tan)
- [ ] 로그 함수 구현 (log, ln)
- [ ] RAD/DEG 모드 전환
- [ ] 괄호 처리
- [ ] 거듭제곱, 제곱근, 팩토리얼
- [ ] π, e 상수

### Phase 4: Advanced Features (Week 4)
- [ ] Backspace 기능
- [ ] 계산 이력 시스템
- [ ] 키보드 입력 지원
- [ ] 오류 처리 개선
- [ ] 애니메이션 최적화

### Phase 5: Testing & Optimization (Week 5)
- [ ] 크로스 브라우저 테스트
- [ ] 모바일 기기 테스트
- [ ] 성능 최적화
- [ ] 접근성 검증
- [ ] 버그 수정

---

## 9. Success Metrics

### 9.1 User Engagement
- **일일 활성 사용자 (DAU)**: 목표 설정 후 측정
- **평균 세션 시간**: > 2분
- **재방문율**: > 30%

### 9.2 Performance Metrics
- **로딩 시간**: < 2초 (95th percentile)
- **계산 정확도**: 100% (표준 테스트 케이스)
- **오류율**: < 1%

### 9.3 Usability Metrics
- **작업 완료율**: > 95%
- **사용자 만족도**: > 4.0/5.0
- **오류 복구 시간**: < 5초

---

## 10. Risks & Mitigation

### 10.1 Technical Risks
| Risk | Impact | Probability | Mitigation |
|------|--------|-------------|------------|
| 부동소수점 정확도 문제 | High | Medium | 정밀 계산 라이브러리 사용 고려 |
| 브라우저 호환성 문제 | Medium | Low | Polyfill 및 철저한 테스트 |
| 성능 저하 (복잡한 계산) | Medium | Low | 계산 최적화 및 웹 워커 사용 고려 |

### 10.2 UX Risks
| Risk | Impact | Probability | Mitigation |
|------|--------|-------------|------------|
| 터치 오입력 | Medium | Medium | 충분한 버튼 크기 및 간격 확보 |
| 복잡한 수식 입력 어려움 | Medium | Medium | 명확한 수식 표시 및 괄호 하이라이트 |
| 다크 모드 가독성 | Low | Low | 충분한 대비율 확보 |

---

## 11. Future Enhancements

### 11.1 Short-term (3-6 months)
- 2nd 기능 (역삼각함수, 쌍곡선 함수)
- 메모리 기능
- 계산 이력 로컬 저장
- PWA (Progressive Web App) 지원

### 11.2 Long-term (6-12 months)
- 그래프 기능 (함수 플로팅)
- 프로그래밍 모드 (진법 변환)
- 통계 계산 모드
- 단위 변환기 통합
- 다국어 지원

---

## 12. Appendix

### 12.1 Reference Design
참조 디자인은 stitch_.zip 파일에 포함된 `code.html` 및 `screen.png`를 기반으로 합니다.

**주요 디자인 특징**:
- 모던하고 미니멀한 UI
- 다크 모드 우선 디자인
- 터치 친화적인 큰 버튼
- 명확한 시각적 계층 구조
- 부드러운 애니메이션 및 전환

### 12.2 Color Reference
```css
/* Light Mode */
--bg-light: #f6f7f8;
--surface-light: #ffffff;
--text-light: #0f172a;
--text-secondary-light: #64748b;

/* Dark Mode */
--bg-dark: #101922;
--surface-dark: #1E2630;
--surface-accent-dark: #283039;
--text-dark: #ffffff;
--text-secondary-dark: #94a3b8;

/* Accent */
--primary: #137fec;
--primary-hover: #0d6efd;
--error: #ef4444;
```

### 12.3 Button Size Reference
```css
/* Scientific Functions */
height: 3.5rem (56px) - 4rem (64px)

/* Number Buttons */
height: 4rem (64px) - 5rem (80px)

/* Helper Buttons */
height: 2.5rem (40px)
```

---

## 13. Approval & Sign-off

### 13.1 Stakeholders
- **Product Owner**: [Name]
- **Lead Developer**: [Name]
- **UX Designer**: [Name]
- **QA Lead**: [Name]

### 13.2 Review Status
- [ ] Product Owner Approval
- [ ] Technical Review
- [ ] Design Review
- [ ] Final Sign-off

---

**Document Version**: 1.0  
**Last Updated**: 2025-12-23  
**Author**: Antigravity AI  
**Status**: Draft - Pending Review
