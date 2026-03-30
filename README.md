# 고급데이터분석 Ⅱ (캡스톤디자인)

**SOC4013-01** | 3.0학점 | 금 10:30AM-13:15PM | 2026년 봄학기

> 강의 노트 및 실습 자료 저장소입니다.
> 수업 계획서 전문은 [Notion](https://minvv23.notion.site/2026-2f93236d0cb180569435ebab8783c209?pvs=74)에서 확인할 수 있습니다.

---

## 수업 개요

본 수업은 대학 데이터 분석 수업이 직면한 두 가지 딜레마를 직시한다.

- 학계의 양적 연구와 산업 현장의 데이터 분석 수요를 어떻게 절충할 것인가?
- AI가 분석 과정의 상당 부분을 자동화하는 시대에, 대학에서 데이터 분석을 배우는 것은 어떤 의미가 있는가?

**도메인**: 설문 데이터 · 행정 데이터 · 대규모 웹 데이터

**방법론**: 회귀분석(횡단면) · 인과추론(시계열·패널) · 딥러닝 및 AI를 활용한 텍스트 분석

수강생들은 이 수업을 통해 다음 문장들을 이해할 수 있게 될 것이다.

> 우리가 어렸을 때부터 배워 온 평균(mean)은 회귀분석(regression)의 univariate special case이다.

> 회귀단절(regression discontinuity)은 사실 도구변수(Instrument Variable)와 동일한 기법이다. 그러나 도구변수는 나쁜 접근이고, 회귀단절은 그보다는 덜 나쁘다. 결국 데이터 분석에서는 estimation보다 identification이 중요하기 때문이다.

> 대규모 텍스트 데이터 분석에서 분류(classification)는 AI의 zero-shot capability로 해결 가능하지만, 군집화(clustering)는 global optimization이기에 O(n²) pairwise comparison이 필요하다. 전자는 "딸깍", 후자는 전통적 방법론이 불가피한 이유다.

---

## 선수 요건

| 항목 | 내용 |
|------|------|
| 실습 환경 | Windows Subsystem for Linux (WSL2) 또는 macOS |
| 사용 언어 | Python |
| 필수 | Python 프로그래밍 경험 (별도 프로그래밍 수업 없음) |
| 권장 | 회귀분석 기초 개념 / ChatGPT·Claude·Gemini 중 2개 이상 유료 플랜 |

---

## 평가

| 항목 | 비율 |
|------|------|
| 중간 발표 (5월 8일) | 30% |
| 최종 발표 + 연구보고서 (6월 12일) | 60% |
| 출석 및 참여 | 10% |

---

## 주차별 수업 계획

> 추후 조정될 수 있음

### Intro
| 날짜 | 주제 |
|------|------|
| 3월 6일 | 어떤 데이터 분석이 중요할까? - AI 시대에 "딸깍"으로 대체 당하는 분석가가 되지 않는 법 |
| 3월 13일 | 2020년대 데이터 분석 연구의 지형 - 학계 안팎으로 진행되고 있는 데이터 분석의 지형들을 파악하기 |

### 서베이 데이터 분석
| 날짜 | 주제 |
|------|------|
| 3월 20일 | 서베이 문항 설계, 실험 디자인, 회귀분석의 기본 개념 |
| 3월 27일 | 회귀모형을 활용한 서베이 데이터 분석에서의 DO와 DO NOT 리스트 |
| 4월 3일 | 부활절 휴가 - 수업 없음 |

### 행정 데이터 분석
| 날짜 | 주제 |
|------|------|
| 4월 10일 | 실습 - 십대 청소년 정치성향 설문 데이터로 회귀분석 ([보고서](https://minvv23.notion.site/10-2203236d0cb1802e8ee0c4d10345e8fc?pvs=24) / [기사](https://www.hankookilbo.com/news/article/A2025082906560003629)) + 정보공개청구의 중요성, 시계열·패널 데이터 분석, 인과추론의 DO와 DO NOT 리스트 |
| 4월 17일 | 인과추론의 주요 기법들 - 왜 RCT와 DID를 제외한 나머지 방법들은 그리 믿음직스럽지 못한걸까? |
| 4월 24일 | (중간고사 기간 - 수업 없음) |
| 5월 1일 | 노동절 - 수업 없음 |

### 중간 발표
| 날짜 | 주제 |
|------|------|
| **5월 8일** | **중간고사 대체 발표** |

### 텍스트 데이터 분석
| 날짜 | 주제 |
|------|------|
| 5월 15일 | 실습 - 교통사고·교통체증 데이터로 패널 데이터 분석 ([기사](https://news.sbs.co.kr/news/endPage.do?news_id=N1007167655&plink=ORI&cooper=NATE)) |
| 5월 22일 | Before AI 텍스트 분석 - 임베딩(embedding), 분류(classification), 군집화(clustering) + After AI 텍스트 분석 - 대규모 데이터에서 AI를 활용한 "딸깍" CAN / CAN NOT 리스트 |
| 5월 29일 | 실습 - 뉴스·커뮤니티 댓글 데이터로 텍스트 분석 ([보고서](https://minvv23.notion.site/2021-2025-2853236d0cb1804b8af1c6ef5af0bc5c?pvs=24) / [방송 영상](https://youtu.be/hjm7mfJd_fg)) |

### Conclusion
| 날짜 | 주제 |
|------|------|
| 6월 5일 | 왜 데이터 분석이 사실 그리 중요하지 않을까? - Before/After AI 시대의 역설과 시사점 |
| **6월 12일** | **기말 발표 및 최종 보고서 제출** |
| 6월 19일 | (기말고사 기간 - 수업 없음) |

---

## 수업 운영 방식

강의 80% / 실습 20%

---

## 읽기 자료

- [컴퓨터 시대의 통계적 추론 - 브래들리 에프론·트레버 해이스티](https://www.aladin.co.kr/shop/wproduct.aspx?ItemId=320222220)
- [고수들의 계량경제학 - Joshua D. Angrist·Jörn-Steffen Pischke](https://www.aladin.co.kr/shop/wproduct.aspx?ItemId=101546305)
- [대체로 해롭지 않은 계량경제학 - Joshua D. Angrist·Jörn-Steffen Pischke](https://www.aladin.co.kr/shop/wproduct.aspx?ItemId=46216053)
- [계량경제학 강의 - 한치록](https://www.aladin.co.kr/shop/wproduct.aspx?ItemId=335268633)
- [Causal Inference: The Mixtape - Scott Cunningham](https://www.aladin.co.kr/shop/wproduct.aspx?ItemId=236813802)
- [Causal Inference with Python (GitHub)](https://github.com/CausalInferenceLab/Causal-Inference-with-Python)

---

## 연락처

minvv23 [at] gmail [dot] com / minvv23 [at] kaist [dot] ac [dot] kr / minvv23 [at] underscore [dot] kr
