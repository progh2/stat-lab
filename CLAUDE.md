# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 프로젝트 개요

**기초 통계량 실험실** — 기초 통계(중심값·퍼짐·사분위수)를 인터랙티브하게 학습하는 단일 HTML 페이지 앱.

- 외부 빌드 도구, 번들러, 패키지 없음. 모든 코드는 `index.html` 한 파일에 집약.
- CSS: `<style>` 블록, HTML: `<body>`, JS: `<script>`
- 한국어 UI, Pretendard 웹폰트 CDN 사용 (`cdn.jsdelivr.net`).
- 라이브: https://progh2.github.io/stat-lab/

## 개발/실행 방법

빌드 없음. 브라우저에서 직접 열거나 아래 중 하나:

```bash
# 로컬 서버 (live-reload 불필요 시)
open index.html

# Python 서버
python3 -m http.server 8080
# 브라우저: http://localhost:8080
```

## 아키텍처

### JS 구조 (`index.html` `<script>`)

| 블록 | 역할 |
|------|------|
| **통계 엔진** `S` | 순수 함수: `mean`, `median`, `mode`, `range`, `variance`, `std`, `quartiles` |
| **헬퍼** | `parseList`, `modeText`, `boxPlotSVG` |
| **진행 상태** | `STEPS` 4단계 + `done` + localStorage `stat-lab-done` |
| **이해 체크** `wireQuizlet()` | 객관식 퀴즈 공통 핸들러 |
| **§1** | 평균/최빈 손계산, `drawCT()` 점 도표(평균·중앙값·최빈값선, 꼬리 버튼) |
| **§2** | 범위 비교, `drawSP()` 히스토그램, `drawBX()` 상자그림, 두 반 비교 |
| **§3** | `verifyData` 계산 + `decideData` 해석 + 붙여넣기 계산기 |
| **§4** | `EXAM_POOL` 약 100문항, 20/40/100 · 순서/랜덤 |
| **§5** | 68–95–99.7 종곡선 (평가 제외) |
| **팡파레** `celebrate()` | Canvas 컨페티 + Web Audio API |
| **연습 A–C** | 중앙값·분산·사분위수 워크시트 |

### CSS 설계 원칙

- CSS 변수(`--mean` 빨강, `--median` 청록, `--mode` 금색, `--spread` 보라)로 색상 의미 통일.
- 반응형: `@media (max-width:560px)`로 2열→1열 전환.
- 모션 감소: `@media (prefers-reduced-motion:reduce)`로 애니메이션 일괄 비활성.

### 콘텐츠 섹션 구조

- `#s1` — 중심값 (평균·중앙값·최빈값)
- `#s2` — 퍼짐 (범위·분산·SD·상자그림) + `#hook-close` 두 반 비교
- `#s3` — 데이터 파악·해석 + `#own-data` 붙여넣기
- `#s4` — 형성평가
- `#s5` — 선택 미리보기 (진행 체크 없음)

## 수정 시 주의

- **통계 엔진 `S`는 모집단 공식** 사용(표본 분산 `n-1` 아님). 변경 시 모든 워크시트·형성평가 기댓값도 함께 갱신 필요.
- **`S.mode`**: 최대 도수가 1이면 `null`(없음). 공동 1등이면 배열(쌍봉/다봉). 수업·퀴즈 문구와 규칙을 맞출 것.
- **`quartiles()`**: 중앙값 제외한 하위/상위 절반으로 Q1·Q3 (Tukey). 페이지에 방법명을 밝혀 둠.
- SVG는 JS로 문자열 템플릿 빌드(`innerHTML` 직접 할당). `viewBox="0 0 720 ..."` 좌표계 기준.
- 효과음은 Web Audio API (`AudioContext`) — 브라우저 정책상 사용자 인터랙션 후 활성화됨.
- 형성평가에 정규분포(68–95–99.7) 문항을 넣지 말 것.
