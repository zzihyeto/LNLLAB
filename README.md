# RPA Auto Doc & Development AI

> CocoaSoft AX Challenge 2026 | Track 2 · RPA 고도화 에이전트 | 팀명: LNLLAB

---

## 프로젝트 목적

현업 담당자(비개발자)가 UiPath Studio 없이도 **자연어만으로 RPA 프로세스를 설계·생성**할 수 있도록 지원하는 AI 기반 개발 자동화 시스템입니다.

기존 RPA 개발은 UiPath Studio 숙련도가 필요하고, IT 개발자에게 전적으로 의존하는 구조로 병목 현상이 발생합니다. 본 프로젝트는 이 진입 장벽을 Claude AI로 허물고자 합니다.

---

## 대상 사용자

- RPA 프로세스를 기획·요청하는 **현업 담당자 (비개발자)**
- 반복적인 XAML 작성과 문서화 작업을 줄이고 싶은 **RPA 개발자**

---

## 시스템 아키텍처 (4단계 파이프라인)

```
자연어 입력  →  AI 프로세스 설계  →  XAML 생성 엔진  →  결과물 패키징
 (사용자)       (Claude API)       (JS 템플릿 빌더)    (ZIP + PPT)
```

---

## 구현 기능

### 1. 3단계 대화형 UX
| 단계 | 내용 |
|------|------|
| Step 1 | 자연어 프로세스 정의서 입력 (직접 입력 또는 예제 시나리오 4종 선택) |
| Step 2 | Claude AI와 티키타카 설계 분석 — 정보 부족 시 `[QUESTION]`으로 질문, 완성 시 `[DONE]`으로 JSON 확정 |
| Step 3 | XAML·PPT 자동 생성 및 다운로드 |

### 2. XAML 자동 생성
- UiPath Studio 2025.10.x Windows (net6) 호환
- 지원 액티비티: `Sequence`, `If`, `ForEach`, `Assign`, `LogMessage`, `NClick`, `NTypeInto`
- TryCatch 예외처리 **전체 프로세스 기본 적용**
- 변수명 camelCase · 인자명 `in_` / `out_` 접두사 자동 적용
- 검증된 네임스페이스 포함 (sap2010, uix 등)

### 3. UiPath 프로젝트 ZIP 패키징
- `Main.xaml` + `project.json` 자동 구성
- UiPath 고정 패키지 버전: System 25.10.4 / UIAutomation 25.10.4 / Excel 3.1.2 / Mail 2.7.12
- ZIP 다운로드 후 UiPath Studio에서 바로 열기 가능

### 4. 요건정의서 PPT 자동 생성
AX Challenge 브랜딩 (다크브라운 + 오렌지) 8슬라이드 구성:

| 슬라이드 | 내용 |
|----------|------|
| 01 표지 | 프로세스명, 팀, 생성일 |
| 02 프로세스 개요 | 목적, 실행 트리거, 소요 시간, 대상 시스템 |
| 03 프로세스 흐름도 | 단계별 플로우 |
| 04 액티비티 목록 | 타입, DisplayName, 비고 |
| 05 변수 및 인자 목록 | 이름, 타입, 범위, 기본값 |
| 06 예외처리 항목 | 예외 유형, 처리 방식 |
| 07 추가 확인 필요 항목 | 오픈 이슈 카드 |
| 08 비고 및 참고사항 | 주의사항, 생성 정보 |

### 5. 다운로드 목록
- `Main.xaml` 단독 파일
- `프로세스명_uipath.zip` — UiPath 프로젝트 패키지
- `프로세스명_요건정의서.pptx` — 브랜딩 PPT
- `design.json` — Claude 설계 원본

---

## 기술 스택

| 구분 | 기술 |
|------|------|
| AI | Claude API (claude-sonnet-4-6) |
| 프론트엔드 | Vanilla HTML / CSS / JavaScript (정적 단일 파일) |
| XAML 생성 | JavaScript 템플릿 빌더 (Python rpa_designer_app.py 기반 포팅) |
| PPT 생성 | PptxGenJS 3.12 |
| ZIP 패키징 | JSZip 3.10 |
| 배포 | GitHub Pages (github.io) |

---

## 로컬 실행 방법

```bash
# Python 내장 서버 사용
python -m http.server 8080
```

브라우저에서 `http://localhost:8080` 접속 후 Anthropic API Key 입력.

---

## GitHub Pages 배포

1. GitHub 레포 → Settings → Pages
2. Source: `main` branch, `/ (root)` 폴더 선택
3. 접속 URL: `https://zzihyeto.github.io/LNLLAB/`

---

## 팀원

| 이름 | 직급 | 역할 |
|------|------|------|
| 이지혜 | 책임 | 기획, AI 프롬프트 설계, XAML 엔진, 전체 총괄 |
| 이선우 | 선임 | 프론트엔드, PPT 생성, 시스템 아키텍처 |

---

**CocoaSoft AX Challenge 2026** | LNLLAB | Track 2 · RPA 고도화 에이전트
