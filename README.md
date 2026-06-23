# 기초 통계량 실험실

> 📊 고등학생을 위한 기초 통계량 인터랙티브 학습 페이지

🔗 **[지금 바로 열기 → https://progh2.github.io/stat-lab/](https://progh2.github.io/stat-lab/)**

---

## 소개

평균·중앙값·최빈값부터 분산·표준편차·사분위수까지, **직접 값을 바꾸고 손으로 계산하며** 통계량의 의미를 체득하는 단일 HTML 학습 앱입니다. 별도 설치 없이 브라우저로 바로 열 수 있습니다.

## 주요 기능

| 단원 | 내용 |
|------|------|
| ① 중심값 실험실 | 점 분포에 값 추가/삭제 → 평균·중앙값·최빈값 실시간 확인 |
| ② 퍼짐 | 슬라이더로 분산 조절 → 히스토그램 + 표준편차 시각화 |
| ② 상자그림 | 직접 데이터 입력 → Q1·Q2·Q3·IQR·이상치 상자수염그림 |
| ③ 단계별 계산 연습 | 정렬→중앙값 / 분산·표준편차 워크시트 / 펜스·이상치 판별 (새 문제 반복) |
| ④ 형성평가 | 선택형 + 계산형 20문항, 즉시 채점 |
| 기타 | 단원 완료 체크박스, 진행률 표시, 완료 시 컨페티 팡파레, 효과음 on/off |

## 사용법

### 방법 1 — GitHub Pages (인터넷)

[https://progh2.github.io/stat-lab/](https://progh2.github.io/stat-lab/) 접속

### 방법 2 — 로컬 실행

```bash
# 저장소 클론
git clone https://github.com/progh2/stat-lab.git
cd stat-lab

# index.html을 브라우저로 열기
open index.html          # macOS
start index.html         # Windows
xdg-open index.html      # Linux
```

## 단원 구성

```
① 자료의 중심을 나타내는 값   → 평균 / 중앙값 / 최빈값
② 자료의 퍼짐을 나타내는 값   → 편차 / 분산 / 표준편차 / 상자그림
③ 데이터 파악 연습             → 3종 계산 워크시트 (반복 연습 + 채점)
④ 형성평가                    → 20문제 혼합형 최종 확인
```

> **참고:** 분산·표준편차는 모분산(÷n) 기준으로 계산됩니다.

## 기술 스택

- 순수 HTML / CSS / Vanilla JS — 단일 파일(`index.html`)
- 외부 의존성: [Pretendard](https://github.com/orioncactus/pretendard) 웹폰트 CDN
- 빌드 도구 없음

## 라이선스

[MIT License](LICENSE) © 2025 [@progh2](https://github.com/progh2)
