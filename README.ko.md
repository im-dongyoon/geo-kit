# geo-kit

**AI 코딩 어시스턴트를 위한 GEO(Generative Engine Optimization) 스킬.**

[English](./README.md)

AI 검색 엔진(ChatGPT, Perplexity, Google AI Overviews, Claude 등)이 여러분의 웹 콘텐츠를 발견하고 인용할 수 있도록 최적화하세요.

## GEO란?

GEO(Generative Engine Optimization)는 AI 검색 엔진이 웹 콘텐츠를 **추출**, **이해**, **인용**할 수 있도록 최적화하는 기술입니다. SEO가 Google 검색 순위를 목표로 한다면, GEO는 **AI가 생성하는 답변에서 인용되는 것**을 목표로 합니다.

- AI 검색 트래픽 전년 대비 **527%** 급증 (Previsible, 2025)
- 사용자 **58%**가 기존 검색보다 AI 도구를 선호 (Capgemini, 2025)
- 적절한 스키마가 적용된 페이지는 AI 답변에 등장할 확률이 **~2.5배** 높음 (Stackmatix, 2026)

## 설치

### 방법 1: skills.sh (모든 AI 코딩 도구)

```bash
npx skills add im-dongyoon/geo-kit --skill geo-kit
```

**15개 이상의 AI 코딩 도구** 지원: Claude Code, Cursor, Cline, GitHub Copilot, Gemini 등 — [skills.sh](https://skills.sh) 경유.

### 방법 2: Claude Code 플러그인 마켓플레이스

```
/plugin marketplace add im-dongyoon/geo-kit
/plugin install geo-kit@geo-kit
```

## 사용법

### `/geo-kit:build` — GEO 최적화된 웹 페이지 생성

```
/geo-kit:build
```

웹 페이지를 만들거나 수정할 때 GEO 모범 사례를 자동 적용합니다. "랜딩 페이지 만들어줘"나 "블로그 포스트 추가해줘" 같은 요청도 자동 감지하여 활성화됩니다:

- JSON-LD 스키마 마크업
- 인용 친화적 시맨틱 HTML 구조
- AI 크롤러 접근 설정
- AI 인용을 유도하는 콘텐츠 패턴

### `/geo-kit:audit` — 기존 페이지 점검

```
/geo-kit:audit                          # 전체 프로젝트 감사
/geo-kit:audit src/pages/landing.tsx    # 단일 페이지 감사
/geo-kit:audit src/pages/              # 디렉토리 감사
```

코드베이스를 스캔하고 **100점 만점의 GEO 감사 리포트**를 생성합니다:

1. 구조화된 데이터 스캔 (JSON-LD, microdata, RDFa)
2. 헤딩 구조 및 시맨틱 HTML 점검
3. 콘텐츠 인용 가능성 및 팩트 밀도 평가
4. 메타 태그 및 OpenGraph 평가
5. AI 크롤러 접근 확인 (robots.txt)
6. 콘텐츠 구조 및 포맷팅 점검
7. 31항목 인용 준비도 체크리스트
8. 우선순위별 개선 항목 리포트

## 포함 내용

| 영역 | 가이드 |
|------|--------|
| **핵심 원칙** | AI가 콘텐츠를 인용하기 위한 7가지 조건 |
| **페이지 템플릿** | 5가지 페이지 유형별 구조 템플릿 및 체크리스트 |
| **스키마 마크업** | JSON-LD 구현 가이드 (Tier 1/2/3) |
| **AI 크롤러 접근** | AI 검색 봇을 위한 robots.txt 설정 |
| **플랫폼 전략** | ChatGPT, Perplexity, Google AI, Claude별 최적화 |
| **인용 체크리스트** | 31항목 사전 게시 체크리스트 |

## 기여

기여를 환영합니다! GEO는 빠르게 발전하는 분야입니다. 새로운 데이터, 기법, 플랫폼별 인사이트가 있다면 PR을 보내주세요.

## 라이선스

MIT
