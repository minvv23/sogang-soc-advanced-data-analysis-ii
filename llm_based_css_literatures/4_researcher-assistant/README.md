# 4. 연구자 보조로서의 LLM (Researcher/Collaborator: 가설생성·자동화 사회과학)

이 폴더는 LLM을 단순한 분석 도구가 아니라 "연구자/협력자"로 활용하는 흐름의 문헌을 모은다. 핵심 주제는 (1) 방대한 문헌·데이터로부터 새롭고 검증가능한 가설을 자동으로 생성하는 작업, (2) 가설 생성에서 실험 설계, 시뮬레이션 실행, 계량분석, 논문 초고 작성, 동료심사까지 사회과학 연구 파이프라인 전체를 자동화하는 멀티에이전트 시스템, 그리고 (3) LLM 자체를 "연구 대상이자 실험 도구(scientist-and-subject)"로 보거나 인간 행동·문화의 통계적 압축물(condensate)로 재해석하는 인식론적 논의이다. 인과그래프(causal graph)·구조적 인과모형(SCM)·강화학습형 보상함수·휴먼인더루프(human-in-the-loop) 설계 등 방법론적 장치가 어떻게 가설의 신규성과 타당성을 동시에 확보하려 하는지가 공통 관심사이다.

## Automating psychological hypothesis generation with AI: when large language models meet causal graph
- **arXiv / 제출**: doi:10.1057/s41599-024-03407-5 (Humanities and Social Sciences Communications) / arXiv 2402.14424, 2024-02
- **저자**: Song Tong, Kai Mao, Zhen Huang, Yukun Zhao, Kaiping Peng (Tsinghua University)
- **연구질문**: LLM의 의미·개념 추출 능력과 인과그래프의 체계적 사고를 결합하면, 심리학 가설을 자동 생성할 때 LLM 단독보다 더 신규하고 유용한 가설을 만들 수 있는가?
- **데이터·대상**: PMC Open Access Subset에서 추린 심리학·신경과학 논문 43,312편(약 14만 편 후보에서 선별). 대상 개념은 "웰빙(well-being)".
- **LLM 기법·방법**: LLMCG(LLM-based Causal Graph) 3단계 파이프라인. (1) 문헌 수집, (2) GPT-4로 각 논문(4000토큰 단위 청크)에서 인과/상관 개념쌍을 JSON 형식으로 추출하고 인과방향성·부호까지 표준화하여 Neo4j 그래프 DB(개념 197k, 연결 235k)에 저장, (3) node2vec 임베딩 + Jaccard 유사도 기반 링크예측(link prediction)으로 아직 문헌에 없는 고확률 인과쌍을 발굴하고 이를 다시 GPT-4에 넣어 130개 가설을 생성. 평가는 박사생(human), Claude-2(LLM-only), LLMCG(랜덤선택/전문가선별) 4집단을 전문가 블라인드 평가(신규성·유용성, 5점)와 BERT 임베딩 + t-SNE 의미분석으로 비교.
- **핵심 발견**:
  - LLMCG가 생성한 가설의 신규성은 LLM-only(Claude-2)를 유의하게 능가했고(t=3.34, p=0.007), 박사생 수준에 근접.
  - GPT-4 단독 vs LLMCG 절제실험에서도 LLMCG가 신규성에서 큰 우위(Cohen's d~1.2, p<0.0001), 유용성은 차이 없음.
  - GPT-4의 인과/상관 관계 추출은 전문가 검증 시 약 87.5% 일치, 인과쌍의 약 13%는 전문가 추정과 불일치.
- **한계·주의**: 인과그래프 구축에 약 13%의 부정확한 관계쌍이 섞여 있고, 검증은 130개 가설로 한정됨. GPT의 블랙박스 특성상 특정 인과쌍 생성 근거가 불투명.
- **CSS 관점 의의/흥미점**: "LLM의 비구조적 창발성 + 인과그래프의 구조적 제약"이라는 결합이 신규성을 끌어올린다는 점을 정량적으로 보였고, 인간 전문가 의존을 가설 생성에서 평가 단계로 이동시켰다는 인식론적 함의가 흥미롭다.

## Large Language Models for Automated Open-domain Scientific Hypotheses Discovery
- **arXiv / 제출**: 2309.02726 (ACL 2024) / 2023-09 (v3 2024-06)
- **저자**: Zonglin Yang, Xinya Du, Junxian Li, Jie Zheng, Soujanya Poria, Erik Cambria (NTU, UT Dallas 등)
- **연구질문**: 사람이 미리 선별·주석한 관측이 아니라 가공되지 않은 원시 웹 코퍼스만 주어졌을 때, LLM이 인간에게도 새로운(novel) 동시에 타당한(valid) 사회과학 연구가설을 자동으로 귀추(hypothetical induction)할 수 있는가?
- **데이터·대상**: 2023년 1월 이후 출판된 상위 사회과학 저널 논문 50편으로 TOMATO 데이터셋 구축(심리학·커뮤니케이션·HRM·마케팅 등 7개 분야). 각 논문의 main hypothesis, background, inspiration을 전문가가 식별하고, 데이터 오염을 피하려 웹에서 의미상 유사한 텍스트를 원시 코퍼스로 수집.
- **LLM 기법·방법**: MOOSE(Multi-mOdule framewOrk with paSt present future fEedback) 프레임워크. GPT-3.5-turbo 기반 모듈들(Background Finder, Inspiration Title/Finder, Hypothesis Suggestor/Proposer, Clarity/Reality/Novelty Checker)이 순차 작동. 세 가지 피드백 기제 도입: present-feedback(즉시 평가·수정), past-feedback(미래 모듈 결과로 과거 모듈 보정), future-feedback(현재 모듈이 미래 모듈을 위한 근거 제공). 평가는 GPT-4 자동평가 + 박사생 전문가 평가(validness/novelty/helpfulness, 5점).
- **핵심 발견**:
  - MOOSE-base가 단순 LLM 베이스라인을 신규성·유용성에서 크게 능가하고, 세 피드백 기제가 점진적으로 품질을 개선.
  - present-feedback 반복 횟수를 늘릴수록 validness·novelty가 안정적으로 상승(최적 반복 존재).
  - Claude3-Opus를 백본으로 쓰면 절대 점수가 전반적으로 향상되어 더 강한 LLM일수록 잠재력이 큼.
- **한계·주의**: 데이터셋이 50편으로 작고 전부 전문가의 수작업 주석에 의존. 자동 setting이 통제 setting과 충돌하지 않으며, validness 평가에서 GPT-4가 "세계에 대한 이해"가 아니라 "본 적 있는 텍스트 빈도"로 점수를 매길 위험.
- **CSS 관점 의의/흥미점**: NLP 최초로 사회과학 가설 발견을 "원시 웹 코퍼스 → 인간에게 새로운 가설"이라는 개방형(open-domain) 과제로 정식화했고, LLM이 과학자의 "copilot" 역할을 할 수 있음을 실증한 선구적 작업.

## Hypothesis Generation with Large Language Models
- **arXiv / 제출**: 2404.04326 / 2024-04 (v3 2024-12)
- **저자**: Yangqiaoyu Zhou, Haokun Liu, Tejes Srivastava, Hongyuan Mei, Chenhao Tan (University of Chicago, TTIC)
- **연구질문**: 문헌이 아니라 라벨링된 데이터(예시)에 기반해, LLM이 다운스트림 분류 성능을 높이면서도 해석가능한 고품질 가설을 어떻게 생성할 수 있는가?
- **데이터·대상**: 합성 과제 SHOE SALES(단일 정답 가설) + 실세계 사회과학 과제 3개: DECEPTIVE REVIEWS(허위 리뷰 탐지), HEADLINE POPULARITY, TWEET POPULARITY(메시지 확산 예측).
- **LLM 기법·방법**: HypoGeniC(Hypothesis Generation in Context). 멀티암드 밴딧의 UCB 알고리즘에서 영감. 소수 예시로 초기 가설은행을 만들고, 각 학습예시에서 상위 k개 가설로 추론한 뒤 정확도로 보상을 갱신(보상 = 정확도항 + 탐색항 α√(log t / |Sᵢ|)). 일정 횟수 이상 틀린 예시는 "wrong example bank"에 모아 지식격차를 메우는 새 가설을 생성. 추론 전략은 best-accuracy, filter+weighted vote, single/two-step adaptive 등 다양. GPT-3.5-turbo, Mixtral, Claude-2.1로 생성·교차추론.
- **핵심 발견**:
  - HypoGeniC가 zero/few-shot은 물론 200~1000개로 미세조정한 RoBERTa·Llama-2-7B(오라클)까지 다수 과제에서 능가.
  - 한 LLM이 생성한 가설로 다른 LLM이 추론해도 성능 유지(가설의 모델간 일반화), OOD 허위리뷰 데이터에서도 일반화.
  - 기존 문헌을 확증할 뿐 아니라 새 통찰을 발견(예: 특별한 날을 언급하는 리뷰가 진실일 가능성, feature engineering 결과와 상충하는 "future" 토큰 해석).
- **한계·주의**: 다중 프롬프트 추론으로 지연·비용이 큼. 데이터에 내재한 편향·고정관념을 가설이 확증할 위험이 있어 휴먼인더루프 권장. 자연어로 표현 가능한 사회과학 과제에 한정(수학·물리는 미해결).
- **CSS 관점 의의/흥미점**: 가설 생성을 "지도학습 유사 setting + RL식 탐색-활용 보상"으로 공식화해, 해석가능한 가설이 곧 분류기로 작동하면서 새로운 사회과학적 통찰까지 산출함을 보인 점이 매력적.

## Automated Social Science: Language Models as Scientist and Subjects
- **arXiv / 제출**: 2404.11794 (NBER working paper) / 2024-04
- **저자**: Benjamin S. Manning (MIT), Kehang Zhu (Harvard), John J. Horton (MIT & NBER)
- **연구질문**: LLM을 가설 생성자(scientist)이자 실험 피험자(subjects)로 동시에 사용하여, 인간 개입 없이 in silico 사회과학 가설을 자동 생성·검증하는 시스템을 만들 수 있는가? 그리고 시뮬레이션이 LLM 직접 질의로는 얻지 못하는 정보를 주는가?
- **데이터·대상**: 시뮬레이션 시나리오 4개 - (1) 머그컵 흥정, (2) 탈세 보석심리, (3) 변호사 취업 면접, (4) 미술품 경매. 인간 데이터가 아니라 GPT-4 기반 에이전트들의 상호작용으로 데이터 생성.
- **LLM 기법·방법**: 핵심은 구조적 인과모형(SCM)을 가설의 언어이자 에이전트·실험 설계의 청사진으로 사용. GPT-4로 (1) 시나리오에서 결과변수와 잠재 원인을 추출해 SCM(DAG) 구성, (2) 외생변수를 변주한 에이전트 인스턴스화, (3) 발화 순서 프로토콜 선택, (4) 조건별 병렬 시뮬레이션 실행(예: 흥정 9×9×5=405회), (5) 에이전트에게 설문해 결과 측정, (6) 선형 SCM의 경로계수(path estimate) 추정. SCM이 사전분석계획(pre-analysis plan) 역할을 해 자동화 가능. 별도로 LLM에게 실험 없이 결과를 직접 예측(predict-yᵢ, predict-β̂)시켜 시뮬레이션 필요성을 검증.
- **핵심 발견**:
  - 시스템이 위조가능한(falsifiable) 가설을 자동 정식화·검증: 판매자 애착↑→거래확률↓, 구매자 예산·판매자 최저가가 유의, 전과기록이 보석금을 높이고 변호사시험 합격만이 채용을 좌우 등.
  - 경매 시뮬레이션 결과가 경매이론(청산가=2위 입찰가)과 매우 근접해 in silico 결과의 타당성을 시사.
  - LLM 직접 예측은 부정확(경로계수를 평균 13.2배 과대추정, predict-yᵢ MSE는 이론의 10배 이상). 그러나 적합된 SCM을 조건으로 주면 예측 MSE가 6배 개선 - "LLM은 즉시 말할 수 있는 것보다 더 많이 안다".
- **한계·주의**: 단순 선형 SCM 가정, 시뮬레이션 결과가 실제 인간으로 외삽되는지는 별도 검증 필요. 대화 종료 규칙(정지문제)이 임의적이고, 신규성 최적화는 아직 이루어지지 않음.
- **CSS 관점 의의/흥미점**: SCM을 "가설-설계-추정"을 하나로 묶는 자동화의 척추로 삼은 설계가 독창적이며, 같은 모델이 과학자이자 피험자가 되는 자기참조적 구도와 "시뮬레이션이 직접 질의를 능가한다"는 발견이 인식론적으로 흥미롭다.

## A Survey on Hypothesis Generation for Scientific Discovery in the Era of Large Language Models
- **arXiv / 제출**: 2504.05496 / 2025-04
- **저자**: Atilla Kaan Alkan, Shashwat Sourav, Maja Jablonska, Michael J. Smith, Kevin Schawinski, Ioana Ciucă 외 (UniverseTBD 컨소시엄)
- **연구질문**: LLM 시대의 과학적 가설 생성 방법을 체계적으로 분류·정리하고, 품질 향상 기법과 평가 전략, 미해결 과제를 종합하면 어떤 지형이 그려지는가?
- **데이터·대상**: arXiv API로 cs.CL 범주에서 2005~2025년 논문을 키워드 검색·수작업 큐레이션. 사전 LLM 시기(LBD, 초기 NLP)부터 최신 LLM 기법까지 포괄.
- **LLM 기법·방법**: 가설 생성(SHG) 방법을 분류체계로 정리 - Human-Centric, Literature-based Discovery(Swanson의 ARROWSMITH, MOLIERE, KnIT 등), Text-Mining, Supervised Learning, Graph-Based, 그리고 LLM-Driven(직접·적대적 프롬프팅, 파인튜닝, RAG, 지식그래프 통합 KG-CoI, 멀티에이전트 시스템). 평가는 인간 전문가 평가(블라인드·페어와이즈·다평정자 신뢰도), 자동평가(BLEU/ROUGE의 한계, 모델기반 메트릭, 신규성=의미거리, 도메인특화 평가)로 정리.
- **핵심 발견**:
  - 가설 생성 연구가 LBD→텍스트마이닝→그래프→LLM으로 진화하며, 멀티에이전트 협업과 지식그래프 결합이 부상.
  - 평가가 핵심 난제: 신규성·관련성·실현가능성·명료성을 동시에 잡아야 하고 표면적 메트릭은 부적합.
  - 핵심 도전과제로 환각(hallucination), 해석가능성, 학습데이터 편향, 계산비용, 저자권·책임 등 윤리 문제 제시.
- **한계·주의**: arXiv cs.CL 범주에 한정해 검색하여 타 분야·미출판 연구를 충분히 포괄하지 못할 수 있고, 정량적 벤치마크 비교라기보다 개념적 정리에 가까움.
- **CSS 관점 의의/흥미점**: 이 폴더의 개별 연구들(Tong 2024 인과그래프, Yang 2024 MOOSE 등)이 큰 분류체계 어디에 위치하는지 지도를 제공하는 참조 문헌으로 유용하다.

## The Third Ambition: Artificial Intelligence and the Science of Human Behavior
- **arXiv / 제출**: 2603.07329 / 2026-03
- **저자**: W. Russell Neuman, Chad Coleman (New York University)
- **연구질문**: AI 연구의 두 지배적 야망(생산성·정렬) 외에, LLM을 인간 행동·문화·도덕추론을 연구하는 "과학적 도구"로 쓰는 제3의 야망을 어떻게 정식화하고, 그 인식론적 한계는 무엇인가?
- **데이터·대상**: 경험적 데이터셋이 아닌 이론·방법론 논고. 계산사회과학, 내용분석, 서베이, 비교역사연구 전통을 배경으로 LLM 기반 행동연구를 위치시킨다.
- **LLM 기법·방법**: LLM을 인간 상징행동의 "condensate(압축물)" - 직접 관찰 불가한 학습된 분포 - 로 개념화하고, 그 표본 출력을 Generative Output으로 구분. 방법론적 혁신으로 (1) 프롬프트 기반 계산실험(프레이밍·권위단서·도덕딜레마 변주 = 실험적 조작의 계산적 유추), (2) 합성 페르소나 표본추출(서베이 전통의 확장), (3) 역사언어모형·LoRA 어댑터를 통한 비교역사 분석, (4) 데이터/정렬/표상 ablation(계산적 반사실 문화분석)을 제시. 핵심 방법론 쟁점으로 fine-tuning 문제(정렬·RLHF가 사전학습된 문화적 규칙성을 왜곡) 제기, instruct-only 튜닝을 실용적 타협으로 추천.
- **핵심 발견**:
  - LLM을 게놈DB·천체관측처럼 새로운 "관측 인프라"로 보되, 인간 피험자·인과설명의 대체물이 아니라 보완재로 삼아야 함(LHC 비유).
  - 정렬은 이진 속성이 아니라 스펙트럼이며, 사회과학에는 강한 정렬이 오히려 장애물(다툼·모호함·규범위반 정보를 가림).
  - base model vs fine-tuned model 구분이 행동연구에 근본적이며, 학습 코퍼스의 서구·영어·온라인 편향을 명시해야 함.
- **한계·주의**: 경험적 실증보다 개념·방법론 제언 중심. 모델 출력을 개인 인지·인구 유병률·인과기제의 증거로 해석하면 안 되고, 삼각검증(triangulation)으로만 타당화해야 한다고 경고.
- **CSS 관점 의의/흥미점**: "LLM = 인간 담론의 통계적 압축물"이라는 프레임이 프롬프트 변주를 곧 실험으로, ablation을 곧 반사실 문화분석으로 재해석하게 해주며, 사회과학 도구로서 LLM의 약속과 함정을 균형 있게 정리한 메타적 통찰이 돋보인다.

## HLER: Human-in-the-Loop Economic Research via Multi-Agent Pipelines for Empirical Discovery
- **arXiv / 제출**: 2603.07444 / 2026-03
- **저자**: Chen Zhu, Xiaolu Wang (China Agricultural University)
- **연구질문**: 데이터 기반 경험경제학 연구 워크플로(가설 생성→식별전략→계량분석→논문→심사)를 멀티에이전트로 자동화하되, 핵심 과학적 판단에는 인간 감독을 유지하는 파이프라인을 만들 수 있는가?
- **데이터·대상**: 경제연구에 흔히 쓰이는 3개 데이터셋 - 중국건강영양조사(CHNS, 285변수·57,203관측), 중국 다세대 패널(CMGPD-Liaoning), UK Biobank. 14회 파이프라인 실행.
- **LLM 기법·방법**: Claude Sonnet 4.6 기반 7개 전문 에이전트(DataAudit, DataProfiling, Question, Data, Econometrics, Paper, Reviewer)를 중앙 orchestrator가 RunState 공유객체로 순차 조율. 핵심 설계는 (1) dataset-aware hypothesis generation - 데이터 구조·변수 가용성·결측·분포진단으로 가설을 제약해 실현불가/환각 가설을 억제, (2) 2중 루프 - question quality loop(생성→실현가능성 스크리닝→인간 선택)와 research revision loop(자동심사→재분석→논문 수정). 계량분석은 LLM 분석계획 + statsmodels/linearmodels로 OLS·고정효과·DID·event-study 실행. 인간 결정 게이트는 연구질문 선택과 출판 승인 두 지점.
- **핵심 발견**:
  - dataset-aware 생성이 실현가능 연구질문 비율을 비제약 LLM 발상의 41%에서 87%로 끌어올림.
  - 14회 중 12회(86%)가 데이터감사~논문생성~심사 전 과정을 수동개입 없이 완주, 평균 API 비용 $0.8~1.5/run(AI Scientist의 $6~15보다 저렴).
  - revision loop가 심사점수를 평균 4.8→6.3으로 개선, 특히 명료성(+2.1)·식별신뢰성(+1.4) 향상(신규성은 +0.3로 변화 작음).
- **한계·주의**: 지원 계량설계가 제한적(IV·RDD·구조모형 미지원). ReviewerAgent가 논문 생성과 같은 LLM이라 평가에 순환성 존재. 다수 가설을 생성·검정하므로 다중검정·p-hacking 위험과 프리프린트 범람 우려.
- **CSS 관점 의의/흥미점**: 완전자동(AI Scientist류) 대신 명시적 인간 결정 게이트를 끼운 "휴먼인더루프 경제연구" 철학과, 데이터 구조로 가설을 묶어 환각을 줄이는 dataset-aware 발상이 실용적 모범을 보인다.

## LLM Agents as Social Scientists: A Human-AI Collaborative Platform for Social Science Automation
- **arXiv / 제출**: 2604.01520 / 2026-04
- **저자**: Lei Wang, Yuanzi Li, Jinchao Wu, Heyang Gao, Xiaohe Bo, Xu Chen, Ji-Rong Wen (Renmin University of China)
- **연구질문**: 실험 설계·인간행동 시뮬레이션·결과분석·보고서 작성을 아우르는 사회과학 연구 전 과정을, 연구자가 매 단계 개입·감독할 수 있는 휴먼-AI 협업 플랫폼으로 자동화(siliconize)할 수 있는가?
- **데이터·대상**: 자체 시뮬레이션 엔진 YuLan-OneSim(8개 사회과학 도메인 50개 시나리오). 사례연구 3건 - 문화전파(귀납), 교사 주의배분(연역, CEPS 221학급·5,525학생으로 검증), 공공재게임 협력기제(귀추, 인간실험 N=120으로 검증).
- **LLM 기법·방법**: S-Researcher 플랫폼이 YuLan-OneSim 위에서 작동. 엔진의 3대 능력: (1) generality - 자연어 시나리오를 ODD 프로토콜→behavior graph→실행코드로 자동변환(auto-programming), (2) scalability - 이벤트구동 비동기 Master-Worker 분산구조로 최대 10만 에이전트, (3) reliability - VR²T(Verifier-Reasoner-Refiner-Tuner) 피드백으로 백본 LLM을 SFT/DPO로 미세조정("social-science gym"). S-Researcher는 Peirce의 3대 추론(귀납·연역·귀추)으로 연구를 조직: paradigm selection agent가 모드를 고르고, detailer/experiment-config/intervention 에이전트가 실험설계, planner/execution/review 에이전트가 결과분석, outline/writing/review 에이전트가 보고서 작성. 각 모듈에 인간 개입 가능.
- **핵심 발견**:
  - 귀납: 호모필리 규칙 없이 LLM 추론만으로 Axelrod의 문화전파(국지수렴+전역양극화, ~65개 군집)를 재현.
  - 연역: 교사 주의배분에서 Expression 가설이 Merit·Elite를 능가(Spearman ρ=0.152), 실데이터 CEPS 회귀(β=0.349, R²=12.1%)와 방향 일치.
  - 귀추: 공공재게임에서 리더 기여수준이 협력의 주동인이며 "강제>자발" 효과를 발견, 인간실험과 상관 r=0.915. 단 LLM 에이전트는 인간보다 행동 이질성이 20~300배 작고 의도단서 민감도가 낮음.
- **한계·주의**: 인간 검증표본이 작고(N=120), 사례가 인지추론 중심이라 감정·문화 내재 행동은 추가 고려 필요. 전문가 심사가 문헌 통합 부족·이론적 깊이 얕음·핵심 구성개념 조작화 미흡을 지적. ReviewerAgent 자기평가의 순환성 위험.
- **CSS 관점 의의/흥미점**: 가설생성을 넘어 시뮬레이션 엔진·추론 패러다임 3종·휴먼인더루프를 통합한 가장 포괄적인 "AI 사회과학자" 플랫폼이며, LLM 에이전트가 중심경향·1차 효과는 잘 재현하나 행동 이질성·의도 민감도는 떨어진다는 능력-한계 경계를 정량적으로 짚은 점이 시사적이다.
