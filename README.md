<aside>
🎯

**수업 개요 및 수업 목표**

</aside>

- 본 수업은 대학에서의 데이터 분석 수업의 두 가지 딜레마를 직시하고자 한다
    - **학계에서의 양적 연구**와 **산업 현장에서 요구되는 데이터 분석** 수요를 어떻게 절충할 것인가?
    - AI 시대에 이미 **데이터 분석 과정의 상당 부분이 자동화**되고, 관련 지식 역시 AI를 통해 쉽게 배울 수 있게 된 시대에 **대학에서의 데이터 분석 수업은 어떤 의미**가 있겠는가?
- 그렇기에 본 수업은 도메인 상으로는 아래의 세 가지 영역을 다루는 동시에
    1. 설문 데이터
    2. 행정 데이터
    3. 대규모 웹 데이터
    
    방법론적으로는 이하 세 가지 기법들을 실습하고 학습하는데에 주목한다.
    
    1. (횡단면 데이터에 대한) 회귀분석
    2. (시계열·패널 데이터에 대한) 인과추론
    3. 딥러닝 및 AI를 활용한 텍스트 데이터 분석
- 전통적으로 위의 범위를 교육하기 위해서는 최소 2-3개 정도의 강의가 필요했으나, AI의 발달 덕에 우리는 훨씬 더 많은 내용들을 빠르게 학습할 수 있기 때문이다. (물론 이를 위해서는 수강생들의 적극적인 참여가 필요하다)
- 또한 본 수업의 목표는 “논문 작성”에만 한정되지 않는다. 모든 학생들이 대학원에 진학하고 학계의 연구자가 되는 것을 목표로 할 필요는 없기 때문이다. 그렇기에 AI 챗봇으로부터 이미 쉽게 설명을 들을 수 있는 내용을 그대로 다루거나, 교과서에 작성된 목차 순서를 따르기보다는 **“실무”에서 발생하는 핵심 문제들**을 위주로 강의가 진행될 예정이다.
- 그러나 이러한 자유로운 구성이 절대로 통계적인 엄밀성의 부족을 의미하지 않는다. 가령, 수강생들은 본 수업을 통해 다음의 문장들을 이해할 수 있게 될 것이다.
    
    > 우리가 어렸을 때부터 배워 온 평균(mean)은 회귀분석(regression)의 univariate special case이다.
    > 
    
    > 회귀단절(regression discontinuity)은 사실 도구변수(Instrument Variable)와 동일한 기법이다. 그러나 도구 변수는 나쁜 접근이고, 회귀단절은 그보다는 덜 나쁘다. 결국 데이터 분석에서는 estimation보다 identification이 중요하기 때문이다.
    > 
    
    > 대규모 텍스트 데이터 분석에서 분류(classification) 모델 개발은 AI를 활용하는 것이 더 저렴하고 효율적이지만, 군집화(clustering)의 경우 전통적인 방식이 불가피하다. 전자는 zero-shot capability로 해결 가능하지만, 후자는 global optimization이기에 O(n2) pairwise comparison이 필요하기 때문이다.
    > 

<aside>
📜

**선수 학습 내용 및 요구사항**

</aside>

- 수업 실습 사용 환경 : [Windows Subsystem for Linux](https://web-yiyeon.tistory.com/12) or macOS
- 사용언어 : Python
- 요구사항 : Python을 활용한 프로그래밍 경험 (본 수업에서는 별도의 프로그래밍 수업을 진행하지 않음)
- 권장사항
    - 회귀분석 개념에 대한 기초적 이해 (하지만 필수는 X)
    - ChatGPT, Claude, Gemini 세 개 서비스 중 2개 이상의 유료 플랜 구독

<aside>
💯

**평가 활동 및 항목별 비율**

</aside>

- 중간 발표 (30%)
- 최종 발표 및 연구보고서 제출 (60%)
- 출석 및 참여 (10%)

<aside>
🗓️

**주차별 수업 계획 (추후 조정될 수 있음)**

</aside>

- **Intro**
    - 3월 6일 : 어떤 데이터 분석이 중요할까? - AI 시대에 "딸깍"으로 대체 당하는 분석가가 되지 않는 법
    - 3월 13일 : 2020년대 데이터 분석 연구의 지형 - 학계 안팎으로 진행되고 있는 데이터 분석의 지형들을 파악하기
- **서베이 데이터 분석**
    - 3월 20일 : 서베이 문항 설계, 실험 디자인, 회귀분석의 기본 개념
    - 3월 27일 : 회귀모형을 활용한 서베이 데이터 분석에서의 DO와 DO NOT 리스트
    - 4월 3일 :  실제 십대 청소년 정치성향 설문 데이터를 활용한 회귀분석 실습
        - 보고서 원본 : [[한국일보×언더스코어] 10대 청소년들에게서도 “남녀 간 정치 성향 차이”가 강력하게 나타날까?](https://www.notion.so/10-2203236d0cb1802e8ee0c4d10345e8fc?pvs=21)
        - 기사 : https://www.hankookilbo.com/news/article/A2025082906560003629
- **행정 데이터 분석**
    - 4월 10일 : 정보공개청구의 중요성, 시계열·패널 데이터 분석, 인과추론의 DO와 DO NOT 리스트
    - 4월 17일 : 인과추론의 주요 기법들 - 왜 실험(RCT)과 이중차분(DID)을 제외한 나머지 방법들은 그리 ‘믿음직스럽지’ 못한걸까?
    - 4월 24일 : (중간고사 기간 수업 없음)
    - 5월 1일 : 실제 교통사고 및 교통체증 데이터를 활용한 패널 데이터 분석 실습
        - 기사 : https://news.sbs.co.kr/news/endPage.do?news_id=N1007167655&plink=ORI&cooper=NATE
- **5월 8일 : 중간고사 대체 발표**
- **텍스트 데이터 분석**
    - 5월 15일 : Before AI 텍스트 분석 - 임베딩(embedding), 분류(classification), 군집화(clustering)
    - 5월 22일 : After AI 텍스트 분석 - 대규모 데이터에서 AI를 활용한 "딸깍" CAN / CAN NOT 리스트
    - 5월 29일 : 뉴스 댓글 및 온라인 커뮤니티 댓글 데이터를 활용한 텍스트 분석 실습
        - 보고서 : [[시사기획 창 × 언더스코어] 2021~2025 국내 주요 웹 서비스 혐오 표현 분석 : 네이버 뉴스, 유튜브, 디시인사이드, 에펨코리아](https://www.notion.so/2021-2025-2853236d0cb1804b8af1c6ef5af0bc5c?pvs=21)
        - 방송 영상 : [**https://youtu.be/hjm7mfJd_fg**](https://youtu.be/hjm7mfJd_fg?fbclid=IwZXh0bgNhZW0CMTAAYnJpZBExZlMyaHh2YnlmOHJvU3pzT3NydGMGYXBwX2lkEDIyMjAzOTE3ODgyMDA4OTIAAR410K-OXl4Ih5adzPdTtOSAPVFdxPAkSUGJffgBbPL3g4zVIKQ0njQJqRt7Bw_aem_ptSoFTwXLfdi90CJ20OTnA)
- **Conclusion**
    - 6월 5일 : 왜 데이터 분석이 사실 그리 중요하지 않을까? - Before AI 시대의 데이터 분석의 역설과 주의사항 / After AI 시대에 데이터 분석의 필요성과 불필요성
    - **6월 12일 : 기말 발표 및 최종 보고서 제출**
    - 6월 19일 : (기말고사 기간 수업 없음)

<aside>
👨🏻‍🏫

**수업 운영 방식**

</aside>

| **강의** | **토의/토론** | **실습** |
| --- | --- | --- |
| 80% | 0% | 20% |

<aside>
📖

**읽기 자료 추천 리스트**

</aside>

[컴퓨터 시대의 통계적 추론 (연습문제 포함) | 에이콘 데이터 과학 시리즈  | 브래들리 에프론.트레버 해이스티](https://www.aladin.co.kr/shop/wproduct.aspx?ItemId=320222220)

[고수들의 계량경제학 | Joshua D. Angrist.Jorn-steffen Pischke](https://www.aladin.co.kr/shop/wproduct.aspx?ItemId=101546305)

[대체로 해롭지 않은 계량경제학 | Joshua D. Angrist & Jorn-steffen Pischke](https://www.aladin.co.kr/shop/wproduct.aspx?ItemId=46216053)

[계량경제학 강의 (한치록) | 한치록](https://www.aladin.co.kr/shop/wproduct.aspx?ItemId=335268633)

[Causal Inference: The Mixtape (Paperback) | Scott Cunningham](https://www.aladin.co.kr/shop/wproduct.aspx?ItemId=236813802)

https://github.com/CausalInferenceLab/Causal-Inference-with-Python

<aside>
🆘

**참고·지원사항**

</aside>

본 강의를 수강하는 장애 학생들에게는 장애 학생 개개인의 특성과 요구에 따라 수업 담당 교강사와의 상담을 통하여 적절한 수준의 지원 서비스(시험시간 연장 및 시험방법 조정 등)를 제공할 수 있다.