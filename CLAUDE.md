# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 프로젝트 개요

**기초 통계량 실험실** — 기초 통계(중심값·퍼짐·사분위수)를 인터랙티브하게 학습하는 단일 HTML 페이지 앱.

- 외부 빌드 도구, 번들러, 패키지 없음. 모든 코드는 `index.html` 한 파일에 집약.
- CSS: `<style>` 블록 (L7–251), HTML: `<body>` (L253–529), JS: `<script>` (L530–끝)
- 한국어 UI, Pretendard 웹폰트 CDN 사용 (`cdn.jsdelivr.net`).

## 개발/실행 방법

빌드 없음. 브라우저에서 직접 열거나 아래 중 하나:

```bash
# 로컬 서버 (live-reload 불필요 시)
open index.html

# Python 서버 (CORS가 필요한 경우)
python3 -m http.server 8080
# 브라우저: http://localhost:8080
```

Firebase 배포: `/deploy` 스킬 사용.

## 아키텍처

### JS 구조 (`index.html` L530~)

| 블록 | 위치 | 역할 |
|------|------|------|
| **통계 엔진** `S` | L531–547 | 순수 함수 객체: `mean`, `median`, `mode`, `range`, `variance`, `std`, `quartiles` |
| **진행 상태** | L551–576 | `STEPS` 배열 + `done` 객체로 4단계 완료 추적, 상단 진행바 렌더링 |
| **이해 체크** `wireQuizlet()` | L578–594 | 객관식 퀴즈 공통 핸들러 |
| **§1 중심값** `drawCT()` | L596–651 | 점 도표(dot plot) SVG + 평균·중앙값·최빈값 실시간 계산 |
| **§2A 퍼짐 슬라이더** `drawSP()` | L653–698 | 히스토그램 SVG + 표준편차 시각화 |
| **§2B 상자그림** `drawBX()` | L699–745 | 상자수염그림(box plot) SVG + 이상치(outlier) 강조 |
| **§3 검증형 연습** | L747–835 | `verifyData` 배열 기반 수치 입력 → 자동 채점 |
| **§4 형성평가** | L836–940 | 20문항 혼합형(객관식+단답) 채점 |
| **팡파레** `celebrate()` | L941–1012 | Canvas 컨페티 + Web Audio API 효과음 |
| **연습 A–C 워크시트** | L1013~ | 손계산 워크시트: 중앙값·분산·사분위수 |

### CSS 설계 원칙

- CSS 변수(`--mean` 빨강, `--median` 청록, `--spread` 보라)로 색상 의미 통일.
- 반응형: `@media (max-width:560px)`로 2열→1열 전환.
- 모션 감소: `@media (prefers-reduced-motion:reduce)`로 애니메이션 일괄 비활성.

### 콘텐츠 섹션 구조

- `#s1` — 중심값 실험실 (평균·중앙값·최빈값 인터랙티브)
- `#s2` — 퍼짐 (분산·표준편차 슬라이더 + 상자그림)
- `#s3` — 데이터 파악 (검증형 자가 연습)
- `#s4` — 형성평가 20문항

## 수정 시 주의

- **통계 엔진 `S`는 모집단 공식** 사용(표본 분산 `n-1` 아님). 변경 시 모든 워크시트 기댓값도 함께 갱신 필요.
- SVG는 JS로 문자열 템플릿 빌드(`innerHTML` 직접 할당). `viewBox="0 0 720 ..."` 좌표계 기준.
- `quartiles()` 구현: 중앙값 제외한 하위/상위 절반으로 Q1·Q3 계산(Tukey 방식).
- 효과음은 Web Audio API (`AudioContext`) — 브라우저 정책상 사용자 인터랙션 후 활성화됨.
