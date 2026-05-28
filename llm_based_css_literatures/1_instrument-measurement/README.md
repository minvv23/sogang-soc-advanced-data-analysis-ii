# 1. 측정 도구로서의 LLM (Instrument: 측정·분류·임베딩·인과추론·멀티모달)

LLM을 텍스트·이미지를 사회과학 변수로 변환하는 측정 도구로 사용하는 연구들. (1) LLM 주석·분류, (2) 측정값의 타당한 통계추론(DSL/SRI/debiasing) 및 text-as-treatment 인과추론, (3) 측정 위험·개념화 비평, (4) 멀티모달·응용·인프라/데이터로 나뉜다. 총 51편.

## Detecting Propaganda Techniques in Memes

- **arXiv / 제출**: 2109.08013 (ACL-IJCNLP 2021)
- **저자**: Dimitrina Zlatkova, Giovanni Da San Martino, Preslav Nakov 외 (SemEval-2021 Task 6 관련 연구진)
- **연구질문**: 멀티모달(텍스트+이미지) 밈에서 사용되는 선전(propaganda) 기법을 자동으로 탐지·분류할 수 있는가? 텍스트 단독, 이미지 단독, 그리고 두 모달리티 결합 중 무엇이 효과적인가?
- **데이터**: 950개의 밈을 22개 선전 기법(예: loaded language, name calling, smears, glittering generalities 등) 분류 체계로 다중 레이블(multi-label) 주석한 데이터셋. 텍스트(밈에 박힌 문구)와 이미지(시각적 요소)를 모두 포함.
- **LLM 기법·방법**: 텍스트 측에는 BERT 계열 트랜스포머를, 이미지 측에는 ResNet-152 같은 CNN 특징 추출기를 사용한다. 핵심은 멀티모달 융합 모델로, ViLBERT, VisualBERT, MMBT(Multimodal Bitransformer)를 비교 평가한다. 각 모델은 텍스트 토큰 임베딩과 이미지 영역(region) 특징을 공동 어텐션(co-attention) 또는 초기 융합(early fusion)으로 결합하여 다중 레이블 분류 헤드(시그모이드 출력)로 22개 기법의 존재 확률을 예측한다. fastText 기반 단순 베이스라인과도 대조한다.
- **핵심 발견**:
  - 다수의 선전 기법은 주로 텍스트 신호에서 탐지되며, 이미지 단독 모델 성능은 낮다.
  - 멀티모달 융합이 텍스트 단독 대비 일부 기법에서 향상을 주지만 모든 기법에서 일관되게 우월하지는 않다.
  - 클래스 불균형과 일부 기법의 희소성이 분류 난이도를 높인다.
- **한계·주의**: 데이터 규모가 작고(950개) 레이블 불균형이 심해 희귀 기법의 일반화가 어렵다. 이미지의 미묘한 시각적 함의를 모델이 충분히 포착하지 못한다.
- **CSS 관점 의의/흥미점**: 온라인 허위정보·정치 선전 연구에서 텍스트뿐 아니라 밈 같은 멀티모달 콘텐츠의 설득 전략을 계량화하는 측정 도구를 제공한다.

## Can Large Language Models Transform Computational Social Science?

- **arXiv / 제출**: 2305.03514 (Computational Linguistics, 2024, 50권 1호)
- **저자**: Caleb Ziems, William Held, Omar Shaikh, Jiaao Chen, Zhehao Zhang, Diyi Yang
- **연구질문**: LLM이 제로샷(zero-shot) 환경에서 인간 주석자를 대체하거나 보조하여 CSS의 다양한 텍스트 분류·생성 과제를 수행할 수 있는가? 어느 과제에서 잘 되고 어느 과제에서 한계가 있는가?
- **데이터**: 24개 대표 CSS 벤치마크 과제(감정·정서·입장·설득력·이데올로기·예의·공감·풍자·혐오·이벤트 추출 등)로 구성된 광범위한 평가 스위트. 각 과제는 기존 인간 주석 골드 레이블을 보유.
- **LLM 기법·방법**: FLAN-T5/FLAN-UL2, OpenAI davinci-001/002/003, GPT-3.5-turbo 등 13개 LLM을 제로샷 프롬프팅으로 평가한다. 각 과제별로 표준화된 지시문(instruction) 프롬프트를 설계하고, 출력 파싱을 통해 분류 레이블을 추출한다. 분류 과제는 정확도·F1로, 생성 과제는 인간 평가로 측정한다. 또한 LLM을 "주석 파이프라인의 보조자"로 쓰는 zero-shot CSS 워크플로(LLM이 후보 레이블·설명 생성 후 인간 검증)를 제안한다.
- **핵심 발견**:
  - LLM은 대다수 분류 과제에서 fine-tuned 소형 모델에는 못 미치지만, 다수 과제에서 인간 미세조정 없이도 합리적 성능(평균적으로 인간 대비 상당 부분)을 낸다.
  - 생성 과제(설명·요약)에서는 LLM이 크라우드워커보다 품질 높은 자유서술을 산출하기도 한다.
  - 추상적·맥락 의존적·주관적 구성개념일수록 LLM 성능이 떨어진다.
- **한계·주의**: 제로샷 분류 정확도가 미세조정 모델 대비 낮아 LLM을 단독 1차 코더로 쓰기엔 위험하다. 프롬프트·모델 버전에 민감하다.
- **CSS 관점 의의/흥미점**: LLM을 인간 코더의 "보조 증폭기(augmenter)"로 자리매김하는 현실적 청사진을 제시하며, CSS 측정 도구로서 LLM의 강점·약점 지형도를 그려준다.

## Design-based Supervised Learning (DSL)

- **arXiv / 제출**: 2306.04746 (NeurIPS 2023; Egami, Hinck, Stewart, Wei)
- **저자**: Naoki Egami, Musashi Hinck, Brandon Stewart, Hanying Wei
- **연구질문**: LLM/머신러닝의 불완전한(편향된) 텍스트 주석을 다운스트림 통계 분석(회귀계수 추정 등)에 사용할 때, 어떻게 점근적으로 불편(unbiased)이고 타당한 신뢰구간을 보장할 수 있는가?
- **데이터**: 사회과학 텍스트 분류 응용(소량의 인간 골드 레이블 + 대량의 LLM 예측 레이블)을 가정한 일반 프레임워크. 여러 CSS 데이터셋으로 검증.
- **LLM 기법·방법**: 핵심은 design-based supervised learning(DSL)이다. 인간이 무작위 표본에 대해 골드 레이블을 부여하고(설계 기반 표본추출, 표본 포함확률 pi가 알려짐), LLM 예측 레이블(surrogate)과 골드 레이블의 차이로 "편향 보정 의사결과(bias-corrected pseudo-outcome)"를 구성한다. 구체적으로 각 관측치의 보정 결과는 LLM 예측에 역확률 가중(IPW) 보정항 (1/pi)*(인간레이블 - 예측)을 더한 형태로, 이를 모멘트 조건/M-추정에 대입한다. 이중 강건성(doubly robust) 성질과 교차적합(cross-fitting)을 통해 surrogate 모델이 틀려도 일관성을 유지하며 sandwich 분산으로 타당한 신뢰구간을 얻는다.
- **핵심 발견**:
  - DSL은 LLM 예측 품질이 낮아도(편향이 있어도) 다운스트림 추정량의 점근적 불편성과 정확한 커버리지를 보장한다.
  - 전량 인간 주석 대비 비용을 크게 줄이면서 통계적 타당성을 유지한다.
  - 단순히 LLM 예측을 그대로 회귀에 넣는 방식(naive)은 편향된 계수를 낳음을 이론·실증으로 보인다.
- **한계·주의**: 골드 레이블 표본추출 확률이 알려져 있어야 하고 인간 레이블이 정답(error-free)이라는 가정에 의존한다. 인간 레이블 표본이 너무 작으면 분산이 커질 수 있다.
- **CSS 관점 의의/흥미점**: "측정은 LLM, 추론 타당성은 통계 설계로 보장"이라는 분업을 정식화하여, LLM 시대 CSS 측정-추론 파이프라인의 표준 도구가 되었다.

## LLVMs4Protest: 비전-언어 모델을 활용한 시위 탐지

- **arXiv / 제출**: 2311.18241
- **저자**: Yongjun Zhang 외
- **연구질문**: 대규모 비전-언어 모델(LLVM)을 활용해 이미지(뉴스 사진·소셜미디어 이미지)에서 시위(protest) 사건과 그 속성을 자동으로 탐지할 수 있는가?
- **데이터**: 시위 이미지 데이터셋(UCLA protest image dataset 계열 등)으로, 시위 여부 및 시각적 속성(폭력성, 표지판, 군중 규모 등) 레이블 포함.
- **LLM 기법·방법**: Swin-Transformer v2 같은 최신 비전 백본과 LLaVA-1.6(Mistral 7B 기반) 같은 멀티모달 LLM을 활용한다. 이미지 인코더가 시각 특징을 추출하고, 비전-언어 정렬을 통해 시위 분류 헤드 또는 지시문 기반 프롬프팅으로 시위 여부·속성을 예측한다. 파인튜닝된 비전 트랜스포머 분류기와 제로샷 멀티모달 LLM 추론을 비교한다.
- **핵심 발견**:
  - 파인튜닝된 최신 비전 트랜스포머가 시위 이미지 분류에서 높은 정확도를 달성한다.
  - 멀티모달 LLM은 추가 학습 없이도 시위 장면을 설명·분류할 수 있으나, 미세한 속성에서는 전용 분류기에 못 미친다.
- **한계·주의**: 시각적 모호성(축제 vs 시위 군중)과 문화·지역 편향이 오분류를 유발한다. 데이터 도메인 이동에 취약하다.
- **CSS 관점 의의/흥미점**: 사회운동·집합행동 연구에서 텍스트 기반 시위 이벤트 DB를 넘어 이미지 증거를 대규모로 코딩하는 멀티모달 측정 도구를 제공한다.

## Prompt Refinement or Fine-tuning? CSS에서의 선택

- **arXiv / 제출**: 2408.01346
- **저자**: (CSS 텍스트 분류 방법론 비교 연구진)
- **연구질문**: CSS 텍스트 분류 과제에서 프롬프트 개선(prompt refinement)과 파인튜닝(fine-tuning) 중 어느 전략이 더 효과적·비용효율적인가? 어떤 조건에서 무엇을 선택해야 하는가?
- **데이터**: 다수의 CSS 분류 벤치마크(감정·입장·주제 등)에서 다양한 데이터 규모·과제 복잡도 조건을 설정.
- **LLM 기법·방법**: 제로샷·퓨샷 프롬프팅, 반복적 프롬프트 개선(에러 분석 기반 지시문 수정), 그리고 QLoRA 등 파라미터 효율 파인튜닝(PEFT), 전체 파인튜닝을 비교한다. 생성형 지식 프롬프팅(generated knowledge prompting), 사고연쇄(chain-of-thought) 등 프롬프트 전략과 GPT-3.5/GPT-4, Llama 계열 모델을 교차 평가하여 성능 대비 라벨링 비용·연산 비용을 정량화한다.
- **핵심 발견**:
  - 라벨이 충분하면 파인튜닝(특히 PEFT)이 일관되게 높은 정확도를 주지만, 라벨이 적은 저자원 환경에서는 잘 설계된 프롬프트가 경쟁력을 가진다.
  - 프롬프트 개선은 빠르고 저렴하나 성능 천장이 존재하며 프롬프트 민감성이 크다.
  - 과제 복잡도가 높을수록 파인튜닝의 이점이 커진다.
- **한계·주의**: 최적 프롬프트 탐색이 비결정적이고 모델 버전 변화에 따라 재현성이 떨어진다.
- **CSS 관점 의의/흥미점**: 연구자가 예산·데이터·과제 특성에 따라 측정 도구(프롬프트 vs 파인튜닝)를 선택하도록 돕는 실무 의사결정 지침을 제공한다.

## Causal Representation Learning: Texts as Treatments (Imai-Nakamura)

- **arXiv / 제출**: 2410.00903
- **저자**: Kosuke Imai, Kentaro Nakamura
- **연구질문**: 텍스트 자체를 처치(treatment)로 보는 인과추론에서, 텍스트의 어떤 잠재적 속성이 결과에 인과적 영향을 주는지를 어떻게 식별·추정하는가? LLM 내부 표현을 활용해 텍스트 처치의 인과효과를 추정할 수 있는가?
- **데이터**: 텍스트-처치 실험·관측 데이터(예: 메시지·발화가 응답·태도에 미치는 효과). LLM 생성 텍스트와 그 내부 표현 활용.
- **LLM 기법·방법**: 잠재적 결과(potential outcomes) 틀에서 텍스트의 인과적으로 관련된 표현(causal representation)을 학습한다. LLM의 내부 임베딩/생성 메커니즘을 이용해 텍스트를 저차원 잠재 변수로 사상하고, 이 표현이 처치를 충분히 요약한다는 분리가능성(separability)·무교란(ignorability)·중복(overlap) 가정 하에 평균처치효과(ATE)를 식별한다. 이중머신러닝(DML)·교차적합으로 nuisance 함수를 추정하여 점근적으로 타당한 추정량을 구성한다.
- **핵심 발견**:
  - 텍스트의 특정 잠재 속성을 인과적으로 분리해 그 효과를 추정하는 식별 조건을 정식화한다.
  - LLM 내부 표현을 활용하면 텍스트 처치의 고차원성을 다루면서 인과효과를 일관되게 추정할 수 있다.
- **한계·주의**: 분리가능성·무교란 가정이 강하고 검증이 어렵다. LLM 표현의 통계적 성질이 불완전해 추정 오차가 발생할 수 있다.
- **CSS 관점 의의/흥미점**: "텍스트=처치" 인과추론을 LLM 표현학습과 결합하여, 메시지·프레임의 인과효과를 측정하는 엄밀한 도구를 제시한다.

## CausalDANN: 텍스트 개입(text interventions)의 인과효과 추정

- **arXiv / 제출**: 2410.21474
- **저자**: (텍스트 개입 인과추론 연구진)
- **연구질문**: LLM으로 텍스트를 반사실적(counterfactual)으로 변형(text intervention)했을 때 결과의 인과효과를, 도메인 이동(domain shift)에 강건하게 추정하는 방법은 무엇인가?
- **데이터**: 원문 텍스트와 LLM이 특정 속성만 변경해 생성한 반사실 텍스트 쌍, 그리고 결과 변수(태도·반응 등).
- **LLM 기법·방법**: LLM을 사용해 텍스트의 처치 속성을 조작한 반사실 버전을 생성하고, 도메인 적대 신경망(Domain Adversarial Neural Network, DANN)의 gradient reversal layer를 결합한 CausalDANN을 제안한다. 적대적 학습으로 사실/반사실 도메인 간 표현 분포를 정렬하여 분포 이동에 의한 편향을 줄이고, 잠재적 결과 틀에서 텍스트 개입의 ATE를 추정한다.
- **핵심 발견**:
  - LLM 생성 반사실 텍스트로 처치를 정의하면 텍스트 개입 효과를 실험 없이도 추정할 수 있다.
  - 도메인 적대 정규화가 사실/반사실 간 분포 차이로 인한 추정 편향을 완화한다.
- **한계·주의**: LLM 반사실 생성이 의도한 속성만 정확히 바꾼다는 보장이 없고(부수적 변화), 생성 품질이 추정 타당성을 좌우한다.
- **CSS 관점 의의/흥미점**: 메시지 프레이밍·표현 변화의 인과효과를 LLM 반사실 생성으로 측정하는 확장 가능한 실험 대체 도구를 제시한다.

## Causal Inference on Outcomes Learned from Text

- **arXiv / 제출**: 2503.00725
- **저자**: (텍스트 학습 결과변수 인과추론 연구진)
- **연구질문**: 결과변수(outcome)가 텍스트로부터 학습/측정될 때(texts-as-outcomes), 처치의 인과효과를 편향 없이 추정하는 방법은 무엇인가? LLM이 측정한 결과의 오차가 인과추정을 어떻게 왜곡하는가?
- **데이터**: 처치-결과 데이터에서 결과가 텍스트(예: 발화·게시물)에서 LLM/분류기로 측정된 설정.
- **LLM 기법·방법**: 잠재적 결과 틀에서 텍스트 기반 결과의 측정오차를 보정하는 추정 전략을 제안한다. LLM 예측을 surrogate 결과로 두고, 소량 인간 레이블로 측정모델을 보정(영향함수 기반 doubly-robust 추정, 교차적합)하여 ATE/CATE를 일관되게 추정한다. TarNet/DragonNet 류의 표현학습 추정기 및 deconfounder 아이디어와 연결한다.
- **핵심 발견**:
  - LLM이 측정한 결과를 그대로 쓰면 측정오차가 인과효과 추정을 체계적으로 편향시킨다.
  - 영향함수 기반 보정과 소량 골드 레이블 결합으로 점근적으로 타당한 추정이 가능하다.
- **한계·주의**: 측정오차의 비차별성(non-differential) 등 가정이 필요하며, 이를 위반하면 보정이 실패한다.
- **CSS 관점 의의/흥미점**: "텍스트=결과변수" 설정에서 LLM 측정의 신뢰성을 인과추론에 안전하게 연결하는 방법론을 제공한다.

## Can LLMs Grasp Visual Concepts? 유튜브 우울증 콘텐츠 분석

- **arXiv / 제출**: 2503.05109
- **저자**: (디지털 정신건강·멀티모달 CSS 연구진)
- **연구질문**: 멀티모달 LLM이 유튜브 영상의 시각적 개념을 파악하여 우울증 관련 자기개방(self-disclosure)·정신건강 신호를 텍스트 단독 대비 더 잘 측정할 수 있는가?
- **데이터**: 정신건강·우울증 주제의 유튜브 영상(자막·메타데이터·프레임 이미지)과 자기개방·정서 레이블.
- **LLM 기법·방법**: LLaVA 계열 멀티모달 LLM과 텍스트 전용 LLM을 비교한다. 영상 프레임의 시각 정보와 자막 텍스트를 함께 입력하는 멀티모달 프롬프팅으로 우울증 신호를 분류하고, 텍스트 단독 프롬프팅과 성능을 대조한다. 부록에 구체적 분류 프롬프트 템플릿을 제시한다.
- **핵심 발견**:
  - 시각 정보를 결합하면 일부 정신건강 개념(맥락 의존적 자기개방 등)에서 텍스트 단독 대비 측정이 개선된다.
  - 그러나 LLM이 미묘한 시각적 함의를 일관되게 파악하지는 못해 개념별 편차가 크다.
- **한계·주의**: 정신건강 레이블의 주관성과 윤리적 민감성, 시각 개념 이해의 불안정성이 한계다.
- **CSS 관점 의의/흥미점**: 디지털 정신건강 연구에서 영상이라는 멀티모달 데이터를 LLM으로 측정하는 가능성과 한계를 동시에 보여준다.

## Navigating the Risks of Using LLMs for Text Annotation in Social Science

- **arXiv / 제출**: 2503.22040
- **저자**: Hao Lin, Yongjun Zhang (Stony Brook University)
- **연구질문**: 사회과학 텍스트 주석에 LLM을 사용할 때 타당성(validity)·신뢰성(reliability)·복제가능성(replicability)·투명성(transparency)의 인식론적 위험은 무엇이며 어떻게 완화·보고할 것인가?
- **데이터**: 사회운동 연구의 DoCA(Dynamics of Collective Action) 프로젝트 NYT 기사(1987-2007, LDC 코퍼스와 정렬)로, 시위 관련 개념(경찰 개입, 시위 규모, 시위 활동)을 인간 코딩한 골드 레이블.
- **LLM 기법·방법**: gpt-4-turbo, Llama-3-8B, Llama-3.3-70B를 제로샷으로 평가한다. role-play 프롬프트, zero-shot CoT, zero-shot Tree-of-Thoughts(ToT) 등 프롬프트 전략을 비교한다. 신뢰성은 동일 프롬프트를 25회 반복 실행 후 급내상관(ICC)으로, 타당성은 인간 골드 레이블 대비 정확도·F1로 측정한다. LLM을 (A) 1차 코더 또는 (B) 보조 코더로 쓰는 워크플로(개발셋으로 프롬프트 선정 -> 전량 적용 -> 평가셋으로 인간 검증)를 제안한다.
- **핵심 발견**:
  - 과제 복잡도가 올라갈수록(이진 -> 다중분류 -> 다중레이블) LLM 성능이 하락한다(예: 경찰 이진 정확도 0.84-0.85, 시위 규모 다중분류 0.46-0.50).
  - 신뢰성도 단순 과제에서 높고(경찰 ICC 0.934) 복잡 과제에서 낮다(시위 규모 ICC 0.518).
  - 중간 추론단계(CoT)를 출력시키면 코딩 의사결정의 투명성을 높일 수 있다.
- **한계·주의**: 제로샷만 실험했고 사회운동 단일 도메인에 한정된다. 모델 발전·드리프트로 결과가 변할 수 있다.
- **CSS 관점 의의/흥미점**: LLM 주석을 인식론적 위험 관점에서 체계적으로 점검·보고하는 실천 지침을 제시하며, 복잡 개념일수록 인간 검증이 필수임을 강조한다.

## Causality for Natural Language Processing (박사학위 논문)

- **arXiv / 제출**: 2504.14530 (Zhijing Jin, 2024 PhD thesis)
- **저자**: Zhijing Jin (지도: Bernhard Scholkopf, Mrinmaya Sachan)
- **연구질문**: LLM은 인과추론을 할 수 있는가? LLM의 내부 메커니즘은 어떻게 작동하는가? 학습 변수 간 인과/반인과 방향이 NLP에 어떤 함의를 갖는가? 인과추론을 텍스트 기반 CSS에 어떻게 응용하는가?
- **데이터**: Corr2Cause(20만+ 샘플의 상관-인과 추론 벤치마크), CLadder(1만 인과 그래프/질의), 수학추론·감정분석 데이터, COVID-19 정책·트위터 데이터, 논문 인용 데이터 등 다수.
- **LLM 기법·방법**: 4부 구성이다. (1) Corr2Cause로 순수 인과추론(상관에서 인과 도출)을 테스트하고 CLadder + CausalCoT(인과 사고연쇄 프롬프팅)로 인과효과 추론을 평가한다. (2) competition of mechanisms(로짓 검사·어텐션 수정)로 사실 vs 반사실 처리의 내부 메커니즘을 추적하고, 수학추론의 강건성을 인과 그래프로 정량화한다. (3) 독립인과메커니즘(ICM) 원리로 NLP 과제를 인과/반인과로 분류(130+ 연구 메타분석)하고, 감정분석의 인과 방향을 발견해 인과 프롬프트로 성능을 개선한다. (4) 텍스트 기반 CSS 응용으로 COVID-19 정책 결정의 원인을 트위터 여론에서 마이닝(교란변수 통제), CausalCite(TextMatch로 고차원 텍스트 임베딩 매칭)로 논문 인용의 인과적 영향을 추정한다.
- **핵심 발견**:
  - 17개 기존 LLM은 순수 인과추론에서 거의 무작위 수준이며, 파인튜닝해도 분포 외(OOD)에서 일반화에 실패한다.
  - 데이터 수집의 인과 방향(인과 vs 반인과)이 SSL·도메인적응 등 학습 결과에 유의미한 영향을 준다.
  - 인과 방향에 맞춘 프롬프트가 감정분석 성능을 개선한다.
- **한계·주의**: 순수 인과추론은 경험지식과 분리하기 어렵고, 모델 규모만으로 강건성이 향상되지 않는다.
- **CSS 관점 의의/흥미점**: LLM의 인과 능력 한계를 엄밀히 진단하면서, 텍스트 매칭 기반 인과추론(CausalCite)·여론-정책 인과 마이닝 등 CSS 직결 응용을 제시한다.

## Unified Multimodal Understanding and Generation Models: Advances, Challenges, and Opportunities (서베이)

- **arXiv / 제출**: 2505.02567
- **저자**: Shanshan Zhao, Xinjie Zhang, Jintao Guo 외 (Alibaba Group 등)
- **연구질문**: 멀티모달 이해(understanding)와 이미지 생성(generation)을 단일 아키텍처로 통합하려는 최근 연구들을 어떻게 분류·정리하고, 핵심 도전과 기회는 무엇인가?
- **데이터**: 서베이 논문으로, 2023-2025년 200+ 통합 멀티모달 모델·데이터셋·벤치마크를 체계적으로 정리.
- **LLM 기법·방법**: 통합 모델을 백본 아키텍처에 따라 (1) 확산(diffusion) 기반(예: Dual Diffusion, UniDisc, MMaDA), (2) 자기회귀(autoregressive) 기반, (3) 융합(AR+diffusion) 기반으로 분류한다. 자기회귀 모델은 이미지 토큰화 방식(픽셀 기반 VQGAN/VQ-VAE, 의미 기반 CLIP/SigLIP/EVA-CLIP, 학습 가능 쿼리 기반 SEED/MetaQueries, 하이브리드)으로 세분한다. 확산의 순방향/역방향 마르코프 체인 수식, 자기회귀의 다음토큰 예측 우도, VQ 토크나이저 메커니즘, any-to-any 모델(텍스트·오디오·영상·음성)을 함께 다룬다.
- **핵심 발견**:
  - GPT-4o의 통합 능력이 이 분야 급성장을 촉발했으며, 이해(자기회귀 선호)와 생성(확산 선호)의 아키텍처 간극이 핵심 난제다.
  - 효율적 토큰화, 교차모달 어텐션, 데이터 구축이 통합 모델 확장의 관건이다.
- **한계·주의**: 분야가 초기 단계로 토큰화·평가·데이터 표준이 미성숙하며, 모달리티 불균형(텍스트·이미지 편중) 문제가 있다.
- **CSS 관점 의의/흥미점**: CSS가 활용할 멀티모달 측정·생성 도구의 기술 지형을 포괄적으로 정리해, 향후 텍스트+이미지+영상 통합 분석의 기반 지식을 제공한다.

## Benchmarking Debiasing Methods for LLM-based Parameter Estimates

- **arXiv / 제출**: 2506.09627 (EMNLP 2025)
- **저자**: Nicolas Audinet de Pieuchon, Adel Daoud, Connor T. Jerzak, Moa Johansson, Richard Johansson
- **연구질문**: LLM 주석을 다운스트림 모수(회귀계수·유병률) 추정에 쓸 때 편향을 보정하는 대표 방법인 DSL과 PPI(Prediction-Powered Inference)는 유한표본에서 어떻게 성능이 차이나는가? 언제 LLM 주석 + 소량 전문가 주석이 전문가 단독보다 통계적으로 유리한가?
- **데이터**: Multi-domain Sentiment, Misinfo-general, Bias in Biographies, Germeval18의 4개 데이터셋. LLM 주석은 BERT, DeepSeek v3, Phi-4, Claude 3.7 Sonnet 4종으로 생성.
- **LLM 기법·방법**: 동일 과제에서 PPI와 DSL을 비교한다. PPI는 LLM 예측을 imputation 추정값으로 쓰고 1차(first-order) rectifier(전문가-LLM 주석 차이의 그래디언트)로 편향을 보정한다. DSL은 설계 기반 표본추출(포함확률 pi 기지)로 IPW 보정한 의사결과를 교차적합·M-추정에 넣어 이중강건 추정한다. 두 실험(전문가 주석 비율 변화 / 총 표본 크기 변화)에서 표준화 RMSE(sRMSE)로 평가한다.
- **핵심 발견**:
  - DSL이 평균적으로 PPI보다 낮은 sRMSE(더 나은 편향 감소·효율)를 보이나, 데이터셋 간 변동성이 커 일관성은 떨어진다(특히 다중공선성에 민감).
  - PPI는 안정적이지만 효율 이득이 작다. 즉 디바이어싱 방법 수준에서 편향-분산 트레이드오프가 존재한다.
  - 비용 분석상 손익분기 전문가 라벨 수가 매우 작아(Phi-4 2개, Claude 105개 등), 적은 전문가 라벨로도 LLM 예측 보강이 유리하다.
- **한계·주의**: DSL과 PPI 두 방법에 한정했고 단일과제 이진분류 결과변수에 국한된다. DSL의 변동성 원인이 완전히 규명되지 않았다.
- **CSS 관점 의의/흥미점**: LLM 측정 + 디바이어싱이라는 CSS 표준 파이프라인에서 방법 선택의 실무 근거(둘 다 보고 권장)와 자원 배분 지침을 처음으로 실증 비교했다.

## CognitiveSky: 탈중앙 소셜미디어를 위한 확장형 감정·내러티브 분석

- **arXiv / 제출**: 2509.11444
- **저자**: Gaurab Chhetri, Anandi Dutta, Subasish Das (Texas State University)
- **연구질문**: 탈중앙(decentralized) 소셜미디어(Bluesky)의 실시간 담론을, 무료 인프라만으로 확장 가능하게 감정·정서·내러티브 측면에서 측정·시각화할 수 있는가?
- **데이터**: Bluesky의 AT Protocol Firehose에서 실시간 수집한 공개 게시물(정신건강 키워드 필터 적용), 누적 5만+ 게시물.
- **LLM 기법·방법**: 트랜스포머 기반 라벨링 파이프라인이다. 감정은 CardiffNLP의 RoBERTa(positive/neutral/negative), 정서는 GoEmotions로 학습된 DistilRoBERTa로 분류하며, 각 게시물의 [CLS] 임베딩을 소프트맥스 분류기(y=softmax(W*CLS(x)+b))에 통과시킨다. 주제는 TF-IDF 벡터에 MiniBatch NMF(비음수 행렬분해)로 군집화한다. 수집(Node.js)-저장(Supabase->Turso SQLite)-라벨링(Python/GitHub Actions)-시각화(Next.js 대시보드) 모듈형 파이프라인을 전부 무료 티어로 구성한다.
- **핵심 발견**:
  - 무료·서버리스 인프라만으로 실시간 탈중앙 소셜미디어를 지속적으로 모니터링·요약하는 재현 가능한 시스템 구축이 가능하다.
  - 정신건강 담론 사례에서 감정·정서·해시태그·이모지의 시계열 패턴을 추출해 대시보드로 제공한다.
- **한계·주의**: 영어 모델에 한정되고 실시간 확장성이 API 레이트리밋에 제약된다. 정적 대시보드라 상호작용·사용자 정의가 제한된다. 시스템 구축 중심이라 실증적 사회과학 발견은 제한적이다.
- **CSS 관점 의의/흥미점**: 트위터 API 제한 이후 대안 플랫폼(Bluesky)에서 윤리적(DID만 참조, 개별 게시물 비노출)·저비용으로 여론을 측정하는 오픈소스 인프라 도구를 제시한다.

## Surrogate Representation Inference (SRI) for Text and Image Annotations

- **arXiv / 제출**: 2509.12416
- **저자**: Kentaro Nakamura (Harvard University)
- **연구질문**: LLM/머신러닝으로 텍스트·이미지를 주석할 때 다운스트림 통계추론의 표준오차를 줄이면서 타당성을 유지하려면? 인간 주석에 측정오차가 있어도 일관된 추정이 가능한가?
- **데이터**: 동기 사례로 Card et al.(2022)의 미국 의회연설 이민 프레이밍 데이터(1880-2021, 24.8만 연설, 그중 3,643개 인간 주석). RoBERTa 분류 정확도 약 65%.
- **LLM 기법·방법**: 핵심 가정은 비정형 데이터(텍스트)가 인간 주석과 구조화 변수 사이를 완전 매개(surrogate)한다는 것으로, 인간 코더가 텍스트만 보고 주석하면 설계상 보장된다. 고차원 텍스트를 저차원 surrogate representation W=f(Y,Z)로 학습하는데, DragonNet 유사 신경망(공유 표현층 + 결과모델 헤드 mu + surrogacy score 헤드 rho)으로 인간 주석과 처치를 동시에 예측한다. 준모수(semiparametric) 효율적 영향함수를 도출하고 K-fold 교차적합으로 점근정규 추정량을 구성한다. 다수 인간 주석이 있으면 double negative control 문헌을 활용해 비차별적(non-differential) 측정오차까지 보정한다.
- **핵심 발견**:
  - SRI는 머신러닝 분류 정확도가 중간(예: 85% 이하)일 때 표준오차를 기존 디바이어싱(PPI/DSL) 대비 50% 이상 줄인다.
  - 인간 주석에 비차별적 측정오차가 있어도 다수 코더를 활용해 타당한 추론(작은 편향·정확한 커버리지)을 제공한다.
  - 이민 프레이밍 응용에서 SRI는 naive(머신러닝 직접 사용)의 과장된 정당 간 차이를 교정하면서 기존 보정법보다 훨씬 좁은 신뢰구간(SE 0.002 vs 0.020)을 산출한다.
- **한계·주의**: surrogacy 가정은 코더가 구조화 변수를 보지 않도록 설계해야 성립한다. 독립 코딩 가정은 LLM 주석에 적용 시 학습데이터 중첩 때문에 위배될 수 있다.
- **CSS 관점 의의/흥미점**: "텍스트가 주석을 완전 매개한다"는 설계 보장 가정을 활용해 LLM 측정의 효율을 극대화하는, 측정-추론 통합의 최신 준모수 방법론이다.

## What is a protest anyway? LLM 시대에도 코드북 개념화는 1차적 관심사

- **arXiv / 제출**: 2510.03541
- **저자**: Andrew Halterman (Michigan State), Katherine A. Keith (Williams College)
- **연구질문**: LLM 기반 텍스트 분류에서 프롬프팅 전후 단계인 개념화(conceptualization, 코드북 작성)와 다운스트림 통계추론을 소홀히 하면 어떤 편향이 생기는가? 사후 디바이어싱이나 LLM 정확도 향상으로 이를 보정할 수 있는가?
- **데이터**: 시위(PROTEST) 분류를 실행 예제로 사용. ACE, ACLED, CAMEO, CCC 등 실제 코드북의 시위 정의 차이를 비교하고, 시뮬레이션 데이터(N=10,000)로 개념화 오류 효과를 검증.
- **LLM 기법·방법**: 주석 오류를 개념화 오류(불완전한 코드북에서 비롯)와 운영화 오류(정의를 잘못 적용)로 분해한다(positivist 가정). 세 가지 분석가 비넷(pessimist=전량 인간 주석, optimist=LLM 제로샷 직접, pragmatist=완전 코드북 + LLM + PPI/DSL 사후보정)을 대조한다. PPI 평균 추정 알고리즘(LLM 유병률 추정 - 인간-LLM 차이 rectifier)을 코드북·LLM에 맞게 변형해 제시하고, 시뮬레이션으로 불완전 코드북이 PPI/DSL로도 보정 불가능한 편향을 낳음을 보인다.
- **핵심 발견**:
  - 동일 배경개념("시위")도 코드북마다 다른 체계화 정의(폭력 포함 여부, 최소 인원, 온라인 포함 등)를 가져 같은 텍스트에 다른 골드 레이블이 매겨진다.
  - 제로샷 LLM은 개념화를 "조용히 건너뛰도록" 유혹하여 표면 레이블만으로 그럴듯하지만 편향된 라벨을 생성한다.
  - 불완전 코드북에서 비롯된 개념화 편향은 PPI/DSL 사후보정이나 LLM 정확도 향상으로 제거되지 않는다(시뮬레이션 확인).
- **한계·주의**: positivist(객관적 골드 레이블 존재) 분류에 한정하며 주관적·해석적 과제는 다루지 않는다. 개념적 논문이라 단일 예제(시위)에 집중.
- **CSS 관점 의의/흥미점**: LLM이 측정 비용을 낮춰도 개념화(코드북 작성)는 여전히 측정 타당성의 1차 관문임을 강조하며, 전체 파이프라인(개념화-운영화-추론)을 통합적으로 사고할 것을 권고한다.

## Computational Social Linguistics for Telugu Cultural Preservation: Chandassu 운율 패턴 인식

- **arXiv / 제출**: 2510.01233
- **저자**: Boddu Sri Pavan, Boddu Swathi Sree
- **연구질문**: 텔루구어 전통 운율시(Chandassu)의 율격 패턴을 자동으로 분석·검증하는 계산 프레임워크를 어떻게 구축하여 소멸 위기의 집단적 문화지식을 보존할 수 있는가?
- **데이터**: andhrabharati.com에서 수집·검증한 4,651개 padyam(운문)으로, 3개 운율 클래스(Vruttamu, Jaathi, Vupajaathi)와 8개 유형, laghuvu-guruvu(경음절/중음절) 주석 포함. GitHub에 공개.
- **LLM 기법·방법**: 본 연구는 LLM이 아니라 규칙 기반(rule-based) 알고리즘 프레임워크다. (1) AksharamTokenizer: 텔루구 문자를 운율 분석의 최소 지각 단위(aksharam)로 토큰화(접합자음·모음 부호 등 처리), (2) LaghuvuGuruvu Generator: 각 음절을 음운 길이 규칙에 따라 경음절(laghuvu, |)/중음절(guruvu, U)로 이진 분류, (3) PadyaBhedam Checker: 생성된 패턴을 유형별 제약(paadam 수, aksharam 수, ganam 시퀀스, yati 휴지, prasa 두운)과 대조 검증. 5개 세부 지표를 산술평균한 Chandassu Score를 평가 척도로 제안.
- **핵심 발견**:
  - 전체 Chandassu Score 91.73%로 텔루구 운율 분석의 첫 정량 벤치마크를 확립했다.
  - 구조적 지표(aksharam 수 99.43%, paadam 수 99.93%)는 거의 완벽하나 yati(휴지) 인식(78.69%)이 가장 어렵다.
  - 운율 클래스·유형별로 제약 복잡도가 달라 성능 편차가 나타난다.
- **한계·주의**: 입력 텍스트의 의미적 타당성은 가정하며 평가하지 않는다. sandhi(연성) 현상 미처리 등 음운 분석에 한계가 있다.
- **CSS 관점 의의/흥미점**: 계산사회언어학을 문화 보존에 적용한 사례로, 집단지성(collective intelligence)으로서의 전통 운율 지식을 공개 데이터셋·알고리즘으로 측정·보존하는 커뮤니티 중심 디지털 인문학 도구를 제시한다.

## Detecting Propaganda Techniques in Memes
- **arXiv / 제출**: 2109.08013 / 2021-08
- **저자**: Dimitar Dimitrov, Bishr Bin Ali, Shaden Shaar, Firoj Alam, Preslav Nakov, Giovanni Da San Martino 외
- **연구질문**: 밈(meme)에 사용된 선전(propaganda) 기법을 텍스트와 이미지를 함께 고려해 다중라벨로 탐지할 수 있는가, 그리고 두 모달리티가 모두 필요한가?
- **데이터**: Facebook 공개 그룹 등에서 3개월간 수집한 950개 밈. 22개 선전 기법(20개는 텍스트+이미지 공용, 2개는 이미지 전용: Appeal to (Strong) Emotions, Transfer)으로 다중라벨·스팬 단위 주석. 6명 주석자 5단계 절차, 코더 간 Krippendorff α 평균 0.77.
- **LLM 기법·방법**: 새 멀티모달 다중라벨 분류 과제로 정식화. 텍스트 전용(BERT, fastText), 이미지 전용(ResNet-152), 멀티모달 융합(early-fusion MMBT, mid-fusion BERT+ResNet, late-fusion, 사전학습 ViLBERT CC/VisualBERT COCO) 모델을 비교. micro/macro F1로 평가. Google Vision API OCR로 텍스트 추출 후 수작업 정제.
- **핵심 발견**:
  - 멀티모달 모델이 단일모달을 일관되게 능가, 최고 성능은 VisualBERT COCO(F1-micro 48.34)와 ViLBERT CC(46.76).
  - 이미지 전용(ResNet-152)은 텍스트 전용보다 성능이 낮아, 시각 모달리티만으로 기법 식별이 더 어려움을 시사.
  - 가장 흔한 기법은 Smears, Loaded Language, Name Calling. 밈당 평균 2.61개 기법.
- **한계·주의**: 950개로 표본이 작고 단일 출처(주로 미국 정치 밈) 편향이 있으며, 선전 기법 주석은 본질적으로 주관성을 내포.
- **CSS 관점 의의/흥미점**: 온라인 정치 선전을 텍스트-이미지 결합으로 세분 측정하는 멀티모달 CSS 도구의 초기 사례로, 이후 SemEval-2021 공유과제의 기반이 되었다.

## Can Large Language Models Transform Computational Social Science?
- **arXiv / 제출**: 2305.03514 / 2024-02 (v3)
- **저자**: Caleb Ziems, William Held, Omar Shaikh, Jiaao Chen, Zhehao Zhang, Diyi Yang (Stanford, Georgia Tech, Dartmouth)
- **연구질문**: 제로샷 LLM이 학습데이터 없이도 CSS의 분류·생성 과제를 신뢰성 있게 수행해 인간 주석 파이프라인을 보강할 수 있는가?
- **데이터**: 6개 사회과학 분야(역사·문학·언어학·정치학·심리학·사회학)를 아우르는 24개 대표 CSS 과제(발화 10, 대화 6, 문서 4 분류 + 생성 5). 각 과제 최대 500개 클래스층화 표본.
- **LLM 기법·방법**: 13개 언어모델(FLAN-T5 small~XXL/UL2, GPT-3 text-001/002/003, gpt-3.5-turbo, GPT-4)을 제로샷 프롬프팅으로 평가. 5개 프롬프트 섭동(gpt-3.5-turbo 패러프레이즈)으로 분산 축소, temperature=0, 로짓 바이어스로 유효 출력 유도. 다지선다 포맷, 맥락 뒤 지시 배치 등 프롬프트 가이드라인(Table 1) 제시. 분류는 macro F1, 생성은 전문가 1-5 Likert 인간평가.
- **핵심 발견**:
  - 분류에서 LLM은 잘 튜닝된 지도학습 모델을 능가하지 못하나 인간과 "공정한" 수준의 일치를 보임(RQ1).
  - 모델이 커질수록 이득이 누적되며(RQ3), 큰 instruction-tuned 모델이 선호됨.
  - 생성(설명)에서는 선도 모델이 데이터셋 참조 품질과 동등하거나 능가, 인간이 모델 출력을 50% 선호.
- **한계·주의**: 최선의 LLM 성능도 인간 주석을 완전 대체하기엔 낮고, 프롬프트 설계·모델 선택에 민감.
- **CSS 관점 의의/흥미점**: LLM을 CSS 도구로 쓰기 위한 광범위 벤치마크·로드맵을 처음 제시하고, 인간-AI 협업 라벨링(LLM 합의 시 LLM, 불일치 시 인간) 구도를 제안한다.

## Using Imperfect Surrogates for Downstream Inference: Design-based Supervised Learning for Social Science Applications of Large Language Models
- **arXiv / 제출**: 2306.04746 / 2024-01 (v3, NeurIPS 2023)
- **저자**: Naoki Egami, Musashi Hinck, Brandon M. Stewart, Hanying Wei (Columbia, Princeton)
- **연구질문**: LLM이 생성한 불완전·편향된 대리(surrogate) 라벨을 하류 회귀분석에 쓰면서도 점근적 불편성과 올바른 신뢰구간을 보장하려면 어떻게 추정해야 하는가?
- **데이터**: 18개 실데이터셋. 대표적으로 Congressional Bills Project(40만 법안, Macroeconomy 이진분류, GPT-3 제로샷 대리 정확도 68%/90%) 및 Ziems et al.(2023)의 17개 CSS 과제(flan-ul2 대리).
- **LLM 기법·방법**: Design-based Supervised Learning(DSL) 추정량 제안. K-fold 교차적합으로 ML 모델 ĝ(Q,X)를 학습한 뒤, 편향보정 의사결과 Ỹ=ĝ + (R/π)(Y-ĝ)를 구성(이중강건 방식). 골드라벨 표집확률 π(Q,W,X)가 설계로 알려져 있다는 가정만 쓰며, ML 모델이 오설정돼도 일치성과 정규성을 증명. 적률추정량으로 측정·회귀·로지스틱 등으로 확장.
- **핵심 발견**:
  - 대리 정확도 80-90%여도 측정오차 무시 시 하류 회귀에 상당한 편향과 신뢰구간 과소피복(90% 정확도에서 95% CI 피복이 40%)이 발생.
  - DSL만이 SO/SL 대비 낮은 편향과 명목 피복을 동시 달성하며 GSO보다 효율적(균형조건 RMSE 14% 개선, 5-shot에서 31%).
  - 대리 품질이 좋아질수록 DSL의 효율이 향상.
- **한계·주의**: 코퍼스가 사전 확보돼 골드라벨 표집확률을 설계로 통제할 수 있는 회귀 세팅에 국한되며, 도메인 시프트·개체단위 예측에는 부적합.
- **CSS 관점 의의/흥미점**: "LLM 라벨을 그대로 종속/독립변수로 쓰면 추정이 편향된다"는 핵심 위험을 정면으로 풀어, 사회과학의 추론 타당성을 지키는 표준적 도구를 제공한다.

## LLVMs4Protest: Harnessing the Power of Large Language and Vision Models for Deciphering Protests in the News
- **arXiv / 제출**: 2311.18241 / 2023-11
- **저자**: Yongjun Zhang (Stony Brook University)
- **연구질문**: 사전학습된 대형 언어·비전 모델을 파인튜닝해 뉴스의 텍스트·이미지에서 시위(protest) 사건과 속성을 식별할 수 있는가?
- **데이터**: (텍스트) Dynamics of Collective Action(DoCA)와 NYT 기사를 매칭한 11,902개 시위 관련 양성 기사 + LDC NYT 코퍼스에서 추출한 27,000개 음성 기사. (이미지) UCLA-Protest 40,764개 이미지(폭력·경찰 등 시각 속성 주석, 시위 이미지 11,659개).
- **LLM 기법·방법**: GPT-4 의존 대신 전이학습 접근. 긴 문서용 longformer-base-4096(RoBERTa 체크포인트 기반)을 DoCA 매칭 데이터로 파인튜닝해 시위 기사 식별, swinv2-base-patch4-window8-256(Swin Transformer V2)를 UCLA-Protest로 파인튜닝해 시위 이미지·시각 속성 분류. 두 모델 정확도 모두 94% 이상.
- **핵심 발견**:
  - 상용 GPT-4 없이 오픈 파인튜닝 모델로 시위 식별에서 94%+ 정확도 달성.
  - longformer로 장문 뉴스, Swin-v2로 이미지를 처리하는 멀티모달 파이프라인 제시.
- **한계·주의**: 학습데이터가 1960-1995년에 치우쳐 최근 시위 추론에 시간적 제약이 있고, 파인튜닝에 ML·하드웨어 지식이 필요하며 교차검증이 더 필요(짧은 기술보고서).
- **CSS 관점 의의/흥미점**: 사회운동 연구자가 직접 운용 가능한 오픈소스 멀티모달 시위 탐지 모델을 공유해, 상용 API 비용·접근성 장벽을 낮춘다.

## Prompt Refinement or Fine-tuning? Best Practices for using LLMs in Computational Social Science Tasks
- **arXiv / 제출**: 2408.01346 / 2024-08
- **저자**: Anders Giovanni Møller, Luca Maria Aiello (IT University of Copenhagen, Pioneer Centre for AI)
- **연구질문**: CSS 텍스트 분류에서 프롬프트 개선·파인튜닝·사전학습량 증가 중 어떤 전략이 언제 효과적인가?
- **데이터**: SOCKET 벤치마크(58개 데이터셋 중 분류 과제 44개, 평가용 대표 23개). humor&sarcasm, offensiveness, sentiment&emotion, trustworthiness, social factors 5개 그룹.
- **LLM 기법·방법**: Llama-2-7B-chat과 Meta-Llama-3-8B-Instruct에 6개 방법 적용 - 제로샷, AI-knowledge 프롬프트(GPT-4로 라벨 설명 생성), RAG(all-MiniLM-l6-v2 임베딩+FAISS), 파인튜닝(QLoRA 4-bit + DPO 2단계), instruction tuning, reverse instruction tuning(gpt-3.5-turbo로 합성 지시 179,510개 생성). 정확도로 교차과제 평가.
- **핵심 발견**:
  - 모델 선택(충분히 사전학습된 모델)이 가장 중요(RQ3): Llama-3가 평균 0.05 향상.
  - 제로샷도 비교적 높으나 AI-knowledge 프롬프트가 일관되게 능가(파인튜닝 정확도를 평균 0.13-0.15 추가 향상). RAG는 효과가 불안정(RQ1).
  - 파인튜닝(QLoRA)은 작은 학습셋으로도 비용효율적으로 일관된 향상. 다만 instruction/reverse tuning은 모델에 따라 성능이 크게 갈리고 환각·정보누출 위험(RQ2).
- **한계·주의**: 과제 난이도 차이로 성능 변동이 크고, 추가 전략들을 우리 것과 결합했을 때의 효과는 평가하지 못함(5쪽 분량).
- **CSS 관점 의의/흥미점**: CSS 실무자에게 "리치한 맥락 프롬프트 우선, 자원 있으면 파인튜닝, 자동 instruction tuning은 신중히"라는 실용 지침을 제공한다.

## Causal Representation Learning with Generative Artificial Intelligence: Application to Texts as Treatments
- **arXiv / 제출**: 2410.00903 / 2025-09 (v4)
- **저자**: Kosuke Imai, Kentaro Nakamura (Harvard University)
- **연구질문**: 텍스트 같은 고차원 비정형 처치에서 특정 처치 특성(주제·감정)의 인과효과를, 생성형 AI의 내부표상을 활용해 교란요인을 통제하며 타당하게 추정할 수 있는가?
- **데이터**: Fong-Grimmer(2016) 후보 프로필 실험(위키 후보 약력 1,246개, 유권자 1,886명 feeling thermometer 평가; 실증분석 표본 5,291). Llama3-8B로 약력을 (재)생성.
- **LLM 기법·방법**: GenAI-Powered Inference(GPI) 제안. LLM 내부표상 R(Llama3 마지막 토큰 4096차원)에서 저차원 deconfounder f(R)를 TarNet 구조로 학습, 처치·교란 특성의 분리가능성(separability) 가정하에 ATE를 비모수 식별. 결정적 디코딩으로 노이즈 제거, double ML(DML)로 점근적 신뢰구간 확보. 데이터에서 표상을 학습하는 기존(BERT 기반 Pryzant/Gui-Veitch) 방식과 달리 LLM의 "진짜" 표상을 직접 사용해 겹침(overlap) 위반을 회피. 지각된 처치(perceived treatment)에는 IV 접근 확장.
- **핵심 발견**:
  - GPI가 BERT 기반 DML/outcome 모델보다 낮은 편향·RMSE와 명목 95% 피복을 달성, 분리가능성 충족 시 우수.
  - positivity 위반을 IOSS(독립지지 점수)로 진단 가능(실증에서 GPI 0.10 vs BERT기반 0.41).
  - 런타임이 BERT 기반 추정량의 약 1/100. 군사경력의 효과가 통계적으로 유의(평가 점수 상승).
- **한계·주의**: 분리가능성 가정이 위배되면 모든 추정량이 함께 악화되며, 결정적 디코딩·배치 미사용 등 LLM 운용 제약이 따름.
- **CSS 관점 의의/흥미점**: "텍스트가 처치"인 정치·여론 실험에서 LLM 내부표상을 인과추론의 교란통제 장치로 활용하는 새로운 방법론적 다리를 놓는다.

## Estimating Causal Effects of Text Interventions Leveraging LLMs
- **arXiv / 제출**: 2410.21474 / 2026-03 (v3)
- **저자**: Siyi Guo, Myrl G. Marmarelis, Fred Morstatter, Kristina Lerman (USC Information Sciences Institute)
- **연구질문**: 텍스트에 잠재된 속성(예: 분노)에 대한 가상의 텍스트 개입(intervention) 효과를, 개입군이 관측되지 않아도 추정할 수 있는가?
- **데이터**: 3개 반합성(semi-synthetic) 데이터셋. Amazon 리뷰(5.6K, 긍정감정→클릭 효과), Reddit r/AmITheAsshole(상위댓글 노출 효과, 분노 수준 효과). 평가 그라운드트루스는 GPT-4/Claude-3.5-Sonnet의 반사실 생성으로 구성.
- **LLM 기법·방법**: CausalDANN 프레임워크 제안. (1) LLM 프롬프팅으로 관측 텍스트를 변환(예: 분노 강화/감정 변경)해 개입군을 구성하고 개입을 텍스트 변환 g(W)로 정식화, (2) Domain Adversarial Neural Network(DANN, BERT 인코더+outcome 예측기+gradient reversal 도메인 예측기)를 결과예측기로 써서 관측↔개입 텍스트 간 도메인 시프트에 강건하게 미관측 결과를 예측, (3) ATE/CATE를 추정. IPW·DR·바닐라 BERT·TextCause와 비교(ΔATE, CATE의 MSE).
- **핵심 발견**:
  - CausalDANN이 ΔATE·CATE 모두에서 baseline(BERT, IPW, DR)을 능가, 개입군이 전혀 관측되지 않아도 효과 추정 가능.
  - 도메인적응(DANN)이 BERT 단독보다 편향을 낮춤. IPW는 성향점수 0/1 쏠림으로 수치적으로 불안정.
  - 처치가 텍스트에 잠재돼 별도 관측이 안 되는 상황을 다룬 첫 직접개입 인과추정 방법.
- **한계·주의**: 평가가 LLM 생성 반합성 데이터라 실제 인간행동이 아니며, LLM 변환이 분노 외 toxicity 등 다른 속성을 의도치 않게 바꿀 수 있고 미관측 교란 가능성이 남음.
- **CSS 관점 의의/흥미점**: "글의 분노를 줄이면 참여가 어떻게 바뀌나"처럼 실험이 불가능한 텍스트 개입 질문을, LLM 변환+도메인적응으로 반사실 추정하는 길을 연다.

## Causal Inference on Outcomes Learned from Text
- **arXiv / 제출**: 2503.00725 / 2025-03
- **저자**: Iman Modarressi, Jann Spiess, Amar Venugopal (Cambridge, Stanford)
- **연구질문**: 무작위 실험에서 결과가 텍스트로 표현될 때, 두 집단(처치/대조)의 텍스트가 체계적으로 다른지, 무엇이 다른지, 그 기술이 얼마나 완전한지를 어떻게 타당하게 추론하는가?
- **데이터**: 개념증명으로 econometrics 카테고리 arXiv 초록 200개(연구팀원이 자기 관심사 부합 여부로 주관적 그룹 A/B 라벨링), 훈련/홀드아웃 반분.
- **LLM 기법·방법**: 세 질문으로 분해. (whether) 역예측(reverse-prediction): LLM(Gemini 1.5 Pro)이 문서로 그룹을 trivial 벤치마크보다 잘 맞히는지를 표본분할+순열검정으로 p값화(알고리즘 무가정 타당). (what) LLM에 "인과 테마(causal themes)"와 척도를 제안시키고, 훈련에서 테마 학습 후 홀드아웃을 전문가가 채점해 검정(theme score bias 문제로 인간 검증 필요, PPI식 cheap+costly 점수 결합 가능). (how complete) 테마 점수의 그룹 예측력을 비모수 벤치마크 대비 완전성(completeness) 0-1로 정량화. 표본분할로 LLM 출력의 통계적 타당성 확보.
- **핵심 발견**:
  - 역예측+순열검정으로 LLM 예측을 써도 알고리즘 가정 없이 그룹 차이의 타당한 검정 가능(개념증명에서 정확도 86% vs trivial 71%, p=0.000).
  - "기계 점수만으로는 실질적(substantive) 주장에 타당한 추론을 못 한다" - 테마의 실질적 정확성 검증엔 인간 라벨이 필수.
  - 사전등록(pre-specification)·인간개입을 firewall 원칙 하에 워크플로에 통합.
- **한계·주의**: 무작위 실험 직접 적용이 아닌 개념증명이며, 인간 검증 비용과 AI 기반 추론의 재현성 문제가 남음.
- **CSS 관점 의의/흥미점**: 실험 결과 자체가 자유서술 텍스트인 경우(웰빙·태도 등)를 위한 인과추론 틀로, LLM의 가설생성과 인간 검증을 통계적으로 결합한다.

## The Economics of Digital Intelligence Capital: Endogenous Depreciation, the Red Queen Effect, and the Structural Jevons Paradox
- **arXiv / 제출**: 2601.12339 / 2026-01
- **저자**: (이론·ABM 단독/소수 저자 논문)
- **연구질문**: AI 역량을 자본재로 볼 때, 그 자본의 가치 감가상각이 내생적으로 결정되는 메커니즘은 무엇이며 시장 구조(승자독식)와 가격 동학에 어떤 함의를 주는가?
- **데이터**: 실증 코퍼스가 아닌 이론 모델 및 행위자 기반 몬테카를로 시뮬레이션(Δt=0.1, T=20년) 산출 데이터.
- **LLM 기법·방법**: "디지털 지능 자본(Digital Intelligence Capital)" 개념을 CES 생산함수(ϱ=-0.2, γ=1.3)와 로짓 수요로 모델링. 감가상각을 선형화하여 δᵢ=δ₀+δ₁gₐ+δ₂·max{0,Gapᵢ} 형태로 내생화하고, 데이터 플라이휠이 임계값 Ω*≈1.5에서 분기(bifurcation)해 승자독식으로 귀결됨을 보임. 교차 감가상각 탄력성≈-2.4, 호 가격탄력성 |ε|≈1.42 등 시뮬레이션으로 추정.
- **핵심 발견**:
  - Red Queen 효과: 경쟁자가 발전하면 내 자본이 가만히 있어도 가치가 떨어지는 내생적 감가상각이 발생.
  - 데이터 플라이휠은 임계점을 넘으면 격차가 자기강화되어 시장이 소수 승자로 수렴.
  - 구조적 Jevons 역설과 "Wrapper Trap"(상위 모델에 종속된 응용업체의 가치 포획 실패)을 이론적으로 제시.
- **한계·주의**: 순수 이론·시뮬레이션 연구로 실데이터 검증이 없어 파라미터 값과 예측의 외적 타당성은 미확인.
- **CSS 관점 의의/흥미점**: AI를 측정·관찰 대상이 아니라 경제 동학을 만드는 자본재로 재개념화하여, AI 산업 집중과 불평등을 사회과학적으로 분석할 틀을 제공한다.

## How Do We Engage with Other Disciplines? A Framework to Study Meaningful Interdisciplinary Citation Engagement
- **arXiv / 제출**: 2601.17020 / 2026-01
- **저자**: (학제간 인용 분석 연구팀)
- **연구질문**: 학제간 인용이 단순 참조인지 실질적 지식 활용인지를 어떻게 분류하고 측정할 수 있는가?
- **데이터**: Grobid/SciPDF로 파싱한 학술논문 전문과 인용 맥락(citation context) 문장.
- **LLM 기법·방법**: 인용 참여도를 7개 범주(Substantiation+Basis, Basis, Substantiation, Use, Definition, Analysis, Related Work)로 나눈 분류 체계를 구축. RoBERTa-base를 파인튜닝해 트랙(track) 분류기를 만들고, Decision Tree와 ChatGPT 5.2 프롬프팅을 결합, SPECTER 임베딩으로 논문 표현을 생성. 코더 간 신뢰도는 Krippendorff's α로 검증.
- **핵심 발견**:
  - 인용은 표면적 빈도가 아니라 "참여 깊이"로 구분할 때 학제간 영향의 실질을 드러냄.
  - 파인튜닝 분류기와 LLM 프롬프팅을 결합한 하이브리드 파이프라인이 분류 가능성을 보여줌.
- **한계·주의**: 7범주 경계가 모호해 코더 간 일치가 완전하지 않으며, 파싱 오류가 인용 맥락 추출에 영향을 줄 수 있음.
- **CSS 관점 의의/흥미점**: 과학사회학·계량서지학에서 "어떻게 학문 분야가 서로 영향을 주는가"를 인용의 의미 수준으로 측정하는 새 도구를 제시한다.

## Causal Effect Estimation with Latent Textual Treatments
- **arXiv / 제출**: 2602.15730 / 2026-02
- **저자**: (텍스트 인과추론 방법론 연구팀)
- **연구질문**: 텍스트 안에 잠재된 처치(latent textual treatment)의 인과효과를 어떻게 식별하고 추정하며 가설을 생성할 수 있는가?
- **데이터**: 텍스트 코퍼스와 그로부터 유도한 준-반사실(quasi-counterfactual) 텍스트.
- **LLM 기법·방법**: Sparse Autoencoder(SAE)로 해석 가능한 텍스트 차원을 추출해 가설 생성 및 스티어링(steering)에 활용하고, 준-반사실 텍스트를 생성. CATE 추정은 잔차화(residualization) 기반으로 차원별(dimension-by-dimension) 또는 PC1 제거 방식을 사용하며, R-learner/double ML(EconML)로 추정. 식별 점수 IC=I*·J*, 편향 한계 |τ̃-τ|≤2Lδ를 제시하고 positivity(공통지지) 위반 문제를 다룸.
- **핵심 발견**:
  - SAE 잠재 차원이 텍스트 처치의 해석 가능한 후보를 자동 생성.
  - 잔차화 기반 추정량으로 텍스트 교란요인 통제하에 CATE 추정 가능.
  - 편향에 대한 이론적 상한을 제공.
- **한계·주의**: positivity 위반과 SAE 차원의 해석 신뢰성에 따라 추정 편향이 커질 수 있음.
- **CSS 관점 의의/흥미점**: "텍스트가 처치"인 사회과학 문제(프레이밍·수사 효과 등)에 현대적 인과추론(double ML)과 해석가능성 도구(SAE)를 결합한다.

## The Prediction-Measurement Gap: Toward Meaning Representations as Scientific Instruments
- **arXiv / 제출**: 2603.10130 / 2026-03
- **저자**: (의미표상·측정 이론 연구팀)
- **연구질문**: 임베딩 같은 의미표상을 "과학적 측정도구"로 쓰려면 예측 성능을 넘어 어떤 조건을 충족해야 하는가?
- **데이터**: 정적 임베딩과 맥락적(contextual) 임베딩에 대한 개념적·경험적 비교.
- **LLM 기법·방법**: 예측-측정 격차(prediction-measurement gap) 개념을 도입하고, 의미표상이 측정도구가 되기 위한 4가지 성공 기준(기하학적 가독성, 해석가능성/추적가능성, 비의미적 강건성을 동반한 의미 민감성, 인지적 타당성)을 제안. 정적 임베딩 대 맥락적 임베딩을 이 기준으로 평가하고 이방성(anisotropy) 문제를 논의.
- **핵심 발견**:
  - 예측 잘하는 표상이 좋은 측정도구인 것은 아님(격차 존재).
  - 4가지 기준으로 표상의 측정 적합성을 체계적으로 평가 가능.
  - 이방성 등 기하학적 왜곡이 측정 타당성을 저해.
- **한계·주의**: 7쪽 분량의 입장(position) 논문으로 대규모 실증 검증보다 개념틀 제시에 초점.
- **CSS 관점 의의/흥미점**: 임베딩을 도구로 무비판 사용하는 관행에 대해, 측정 타당성이라는 사회과학 방법론의 기준을 명시적으로 요구한다.

## POLAR: A Per-User Association Test in Embedding Space
- **arXiv / 제출**: 2603.15950 / 2026-03
- **저자**: (임베딩 편향·사용자 분석 연구팀)
- **연구질문**: 개별 사용자 수준에서 임베딩 공간 내 어휘 연상(편향)을 어떻게 측정하고 통계적으로 검정할 수 있는가?
- **데이터**: 사용자별 텍스트가 포함된 코퍼스(MLM 파인튜닝용).
- **LLM 기법·방법**: 사용자 토큰(usr||SHA1[:10])을 마스크드 언어모델(bert-base-uncased)에 주입해 사용자별 표상을 학습. WEAT 스타일 통계량 s(u;A,B)로 사용자 u의 개념집합 A·B에 대한 연상을 측정하고, 순열검정(permutation) p값과 Benjamini-Hochberg FDR로 다중비교를 보정.
- **핵심 발견**:
  - 집단 평균이 아닌 개인 단위로 임베딩 연상(편향)을 검정하는 POLAR 방법 제시.
  - 순열검정+FDR로 통계적으로 엄밀한 사용자별 편향 탐지 가능.
- **한계·주의**: 사용자 토큰 학습에 충분한 사용자별 텍스트가 필요하며 데이터가 적은 사용자는 추정이 불안정.
- **CSS 관점 의의/흥미점**: 편향·태도 측정을 집단 수준에서 개인 수준으로 내려, 개인차 연구와 계산사회과학을 잇는 정밀 측정도구를 제공한다.

## Multi-Perspective LLM Annotations for Subjective Tasks
- **arXiv / 제출**: 2603.21404 / 2026-03
- **저자**: (주관적 주석·능동추론 연구팀)
- **연구질문**: 인구집단마다 답이 다른 주관적 주석 과제에서 LLM 주석을 어떻게 보정해 다관점 추정량을 효율적으로 얻는가?
- **데이터**: POPQUORN 데이터셋(인구통계 정보가 부여된 주관적 라벨링 과제).
- **LLM 기법·방법**: Perspective-Driven Inference(PDI)를 제안, 인구집단별 벡터 추정량을 정의. XGBoost 오차예측기로 LLM 오차 err̂ᵢ를 학습해 적응적 표집 πᵢ∝err̂ᵢ을 수행하고, IPW 기반 정정(rectified) 추정량과 Prediction-Powered Inference(PPI++)/능동추론(active inference)을 결합. 페르소나 프롬프팅의 한계를 비판적으로 검토.
- **핵심 발견**:
  - 단순 페르소나 프롬프팅만으로는 집단별 관점을 신뢰성 있게 재현하지 못함.
  - 오차 기반 적응적 표집+PPI로 적은 인간 라벨로도 편향 없는 집단별 추정 가능.
- **한계·주의**: 오차예측기의 품질과 인구집단 표본 크기에 추정 효율이 좌우됨.
- **CSS 관점 의의/흥미점**: "정답이 하나가 아닌" 주관적 사회과학 측정에서 다양성을 통계적으로 보존하면서 LLM과 인간을 효율 결합하는 길을 제시한다.

## AI Token Futures Market: Commoditization of Compute and Derivatives Contracts
- **arXiv / 제출**: 2603.21690 / 2026-03
- **저자**: (금융공학·AI 인프라 경제 연구팀)
- **연구질문**: AI 추론 토큰을 거래 가능한 상품으로 표준화할 때 가격 동학을 어떻게 모델링하고 위험을 헤지할 수 있는가?
- **데이터**: 가격 시뮬레이션(몬테카를로 10,000 경로, 3년) 산출 데이터.
- **LLM 기법·방법**: AI 추론 토큰을 상품(commodity)으로 보고 표준추론토큰(SIT)과 토큰가격지수(TPI)를 정의. 가격을 평균회귀 점프-확산(mean-reverting jump-diffusion) SDE로 모델링하고 몬테카를로로 선물·파생상품 가격을 산출, 최소분산 헤지비율로 헤지 효율(62-78%)을 추정. 전력 선물(electricity futures)과의 유추를 활용.
- **핵심 발견**:
  - AI 추론 비용을 금융 상품화해 선물·파생으로 거래·헤지하는 시장 설계를 제안.
  - 평균회귀 점프-확산이 토큰 가격의 변동성·급등을 포착.
  - 최소분산 헤지로 62-78%의 헤지 효율 달성.
- **한계·주의**: 실제 거래 데이터가 아닌 시뮬레이션 기반이며 SIT 표준화의 시장 수용성은 미검증.
- **CSS 관점 의의/흥미점**: 컴퓨팅·AI 추론이 전력처럼 거래되는 시장의 사회경제적 함의를 선제적으로 모델링한다.

## Large Language Models Unpack Complex Political Opinions through Target-Stance Extraction
- **arXiv / 제출**: 2603.23531 / 2026-03
- **저자**: Özgür Togay, Javier Garcia Bernardo, Florian Kunneman, Anastasia Giachanou (Utrecht University)
- **연구질문**: 정치적 텍스트에서 무엇(target)에 대한 어떤 입장(stance)인지를 LLM이 동시에 추출(Target-Stance Extraction)할 수 있는가?
- **데이터**: r/NeutralPolitics(2005-2023.4, Pushshift) 게시글 1,084개 수작업 주석, 138개 타깃+"Other" 범주, 골드 테스트셋 200개(무타깃 50, 입장별 50).
- **LLM 기법·방법**: 타깃 식별과 입장 탐지를 결합한 TSE 과제 정의. 프롬프팅 전략으로 zero-shot, few-shot, 대화 맥락 증강(스레드 주변 글 최대 4개), 정보 맥락 증강(코드북 타깃 설명)을 비교. GPT-4.1/o3, Gemini-2.5 계열, Llama-3.1/4, Qwen-3, Gemma-3 등 다수 모델 평가. 타깃 탐지 Krippendorff α=0.48.
- **핵심 발견**:
  - 최고 zero-shot 타깃 F1 0.73(gpt-4.1), 입장 F1/Acc 0.84/0.85(o3).
  - o3 few-shot+정보맥락이 최고 성능(타깃 F1 0.76, 입장 F1 0.87).
  - 추론 모델은 입장 탐지는 개선하나 타깃 식별은 크게 개선하지 못하고, 8B 미만에서 성능 급락. o3를 제3 주석자로 쓸 때 20개 불일치 중 12개에서 전문가와 일치.
- **한계·주의**: 단일 서브레딧 기반이라 일반화에 한계가 있고 타깃 주석 신뢰도(α=0.48)가 중간 수준.
- **CSS 관점 의의/흥미점**: 정치 여론을 "대상-입장" 쌍으로 분해해, 단순 찬반을 넘어 복합적 정치 의견 구조를 측정하는 도구를 제공한다.

## Navigating the Prompt Space: Improving LLM Classification of Social Science Texts Through Prompt Engineering
- **arXiv / 제출**: 2603.25422 / 2026-03
- **저자**: Erkan Gunes (Constructor University), Christoffer Florczak (Aalborg University), Tevfik Murat Yildirim (University of Stavanger)
- **연구질문**: 사회과학 텍스트 분류에서 프롬프트의 맥락 구성요소(라벨 설명, 지시적 넛지, 퓨샷 예시)와 배치 크기를 어떻게 조합해야 정확도를 극대화하는가?
- **데이터**: (연구1) Comparative Agendas Project 의회 법안 제목 데이터(21개 정책 이슈 범주), (연구2) ANES "가장 중요한 문제(MIP)" 개방형 응답의 감정/중립 이진 분류(모델 학습 컷오프 이후 라벨링).
- **LLM 기법·방법**: 프롬프트를 헤더+3개 맥락 구성요소(라벨 설명·지시적 넛지·퓨샷 예시)+입력텍스트로 구조화하고, 3요소의 모든 2^3=8가지 조합을 체계적으로 변주. 배치 크기(법안: 1/10/100/500/1000, MIP: 1/10/100/300)와 두 모델(GPT-4o, Gemini 2.0 Flash)을 교차. 가중 F1로 평가하며 temperature=0에서도 출력이 비결정적임을 검증.
- **핵심 발견**:
  - 가장 미니멀한 프롬프트는 거의 항상 차선이며, 단 하나의 맥락 요소만 추가해도 큰 정확도 향상이 나타남(이후엔 한계수익 체감, 때로는 맥락 추가가 정확도를 떨어뜨림).
  - 배치 크기 1(단일 입력)은 과반의 구성에서 최적이 아님 - 배치 분류가 비용·성능 모두 유리할 수 있음.
  - temperature=0에서도 결정성이 보장되지 않고 동일 프롬프트 간 변동이 모델·프롬프트 복잡도에 의존. 모델·과제·배치 간 이질성이 커 일반 규칙 의존보다 과제별 검증이 필요.
- **한계·주의**: 모델 2개와 제한된 변주 범위만 다뤘고 퓨샷 예시 개수·선택 전략은 충분히 탐색하지 못함.
- **CSS 관점 의의/흥미점**: LLM 주석을 쓰는 사회과학자에게 "프롬프트 공간 탐색"의 실증 지침과, 결과를 재현 가능하게 만들기 위한 과제별 검증·문서화의 필요성을 제시한다.

## Artificial Intelligence in Science: Returns, Reallocation, and Reorganization
- **arXiv / 제출**: 2603.27956 / 2026-03
- **저자**: Moh Hosseinioun, Brian Uzzi (Northwestern Kellogg/NICO), Henrik Barslund Fosse (Novo Nordisk Foundation)
- **연구질문**: AI 도입이 과학 연구의 산출(논문/인용)을 얼마나 끌어올리는가, 그리고 그보다 더 본질적으로 연구 생산과정(예산 배분, 팀 규모, 과제 구성)을 어떻게 재조직하는가?
- **데이터**: 대형 국제 보건·생의학 펀딩기관에 제출된 지난 10년치 연구계획서 전수(18,896건, funded/unfunded 모두 포함). 71,479개 키워드-문장 쌍, funded 과제는 후속 논문(OpenAlex 인용·JIF)과 연결.
- **LLM 기법·방법**: 3단계 파이프라인. (1) 약 200개 시드 렉시콘 기반 정규식·사전 매칭으로 1차 탐지 후, 키워드 없는 문장에만 Qwen2.5-32B-Instruct를 적용해 도메인 특화·패러프레이즈 표현까지 포착(신뢰도 0.70 컷). (2) Meta-Llama-3.1-70B-Instruct로 각 키워드-문장을 11개 연구워크플로 역할(ideation, data collection, analysis, experimentation, inference, validation, automation, benchmarking 등)에 분류(Qwen 대조 시 Jaccard 0.41, κ 0.31, 저신뢰 ideation/experimentation은 수작업 재검토). (3) Qwen2.5-32B-Instruct로 10개 알고리즘 클래스 분류 후 Modern AI/Statistical ML/Domain-specific/Analytics 4그룹으로 축약. 예산항목은 paraphrase-multilingual-mpnet-base-v2 임베딩 코사인 매칭으로 표준 카테고리에 배정, 과제는 JAAT(O*NET task 추출기)로 추출, Anthropic의 task-level LLM exposure 점수와 결합.
- **핵심 발견**:
  - 단기 과학적 수익은 미미: AI 과제는 더 길고 비슷한 예산을 쓰며 상위 꼬리(최대 JIF/최대 인용/논문수)에서만 약한 향상.
  - 주된 효과는 자원 재배분: 장비·운영비에서 인적자본(특히 급여)으로 예산이 이동하고 팀 규모가 커짐 - 즉시 효율보다 재조직(GPT 이론의 latency)에 부합.
  - 과제 범위 확장: AI 과제는 과제 수가 더 많고(대체 아닌 확장), ideation·experimentation 활동이 LLM 역량과 가장 잘 정렬되어 향후 생산성 향상 잠재력 시사.
- **한계·주의**: 보건·생의학 단일 펀딩기관 표본이라 일반화 한계, 미관측 교란 배제 불가, JAAT는 구인공고로 학습되어 추상적 연구활동 탐지율이 낮을 수 있음.
- **CSS 관점 의의/흥미점**: LLM을 "측정 도구"로 써서 출판물이 아닌 사전적(ex ante) 연구계획서 전수(실패 과제 포함)를 분석한다는 점이 신선하며, AI를 범용기술(GPT)로 보고 산출이 아닌 "생산조직의 변화"로 효과를 포착한 점이 핵심 통찰이다.

## Bounded by Risk, Not Capability: Quantifying AI Occupational Substitution
- **arXiv / 제출**: 2604.04464 / 2026-04
- **저자**: (직업 대체 위험 정량화 연구진)
- **연구질문**: AI의 직업 대체는 기술적 "능력"이 아니라 오류가 초래하는 "위험(risk)"에 의해 제약된다 - 이 가설을 직무 활동 단위로 정량화할 수 있는가?
- **데이터**: O*NET 직업 데이터베이스의 Detailed Work Activities(DWAs)와 task statements를 대상으로 함.
- **LLM 기법·방법**: LLM에게 각 직무 활동을 능력(capability) 차원과 위험/책임(risk) 차원으로 점수화하도록 하는 constrained JSON scoring 방식. 스키마 검증과 재시도(retry) 루프로 구조화된 출력을 강제하고, 능력만으로 본 대체 가능성과 위험을 반영한 실제 대체 가능성을 구분하여, 능력은 높지만 오류비용이 큰 활동은 대체에서 보호된다는 점을 수치화.
- **핵심 발견**:
  - AI 대체의 상한은 기술적 능력이 아니라 오류 발생 시의 위험·책임 부담에 의해 결정됨.
  - 능력 점수가 높아도 고위험 활동(의료·안전·법적 책임 등)은 대체율이 낮게 추정됨.
  - 능력 기준 추정치는 대체 위협을 체계적으로 과대평가함.
- **한계·주의**: 위험 점수가 LLM의 주관적 판단에 의존하며, O*NET 활동 분류의 추상성 때문에 실제 현장의 미세 맥락은 누락될 수 있음.
- **CSS 관점 의의/흥미점**: "AI가 할 수 있는가"가 아니라 "AI가 하도록 허용되는가"라는 사회·제도적 제약을 측정 가능한 양으로 전환한 점에서, 노동시장 충격 예측의 프레임을 바꾼다.

## Sentiment Classification of Gaza War Headlines: A Comparative Analysis
- **arXiv / 제출**: 2604.08566 / 2026-04
- **저자**: (가자 전쟁 헤드라인 감정분석 연구진)
- **연구질문**: 정치적으로 민감한 가자 전쟁 뉴스 헤드라인의 감정을 분류할 때 전통적 아랍어 BERT 계열과 최신 LLM 중 무엇이 더 정확하고 일관적인가?
- **데이터**: 가자 전쟁 관련 뉴스 헤드라인 코퍼스(아랍어/영어), 감정 라벨이 부여된 비교용 표본.
- **LLM 기법·방법**: 아랍어 BERT 계열(CAMeLBERT, MARBERT, DarijaBERT, mBERT, ConfliBERT)을 fine-tuning한 supervised 분류기와 생성형 LLM(GPT-4.1, Gemini 등) 제로/few-shot 프롬프팅을 동일 데이터에서 비교. Cohen's κ 등 일치도 지표로 모델 간·인간 라벨 간 정합을 평가하고, 정치적 편향이 헤드라인 감정 분류에 미치는 영향을 검토.
- **핵심 발견**:
  - 도메인 특화 fine-tuned BERT가 특정 과제에서 범용 LLM과 경쟁력 있거나 우월할 수 있음.
  - 정치적으로 민감한 텍스트에서 모델 간 라벨 불일치가 크게 나타남.
  - 모델 선택과 프롬프트가 측정 결과를 크게 좌우함.
- **한계·주의**: 헤드라인은 짧고 맥락이 부족해 감정 추론이 불안정하며, "정답" 감정 라벨 자체가 정치적 관점에 따라 달라질 수 있음.
- **CSS 관점 의의/흥미점**: 분쟁 보도라는 고편향 영역에서 측정 도구(분류기)의 선택 자체가 결론을 바꿀 수 있음을 경고하며, CSS 측정의 도구 의존성을 드러낸다.

## Is Bitcoin A Hedge Against Central Banking? Evidence from AI-Driven Monetary Analysis
- **arXiv / 제출**: 2604.08825 / 2026-04
- **저자**: (AI 기반 통화정책 분석 연구진)
- **연구질문**: 비트코인은 중앙은행 통화정책에 대한 헤지(hedge) 자산인가? 통화정책 커뮤니케이션 텍스트를 AI로 정량화해 인과적으로 검증할 수 있는가?
- **데이터**: 중앙은행 통화정책 문서·발표문 텍스트와 비트코인 가격 시계열을 결합한 시계열 데이터.
- **LLM 기법·방법**: LLM으로 통화정책 텍스트의 매파/비둘기파 성향(긴축/완화 시그널)을 점수화하여 측정 변수를 구성하고, 이를 LSTM, Granger causality, Variational Mode Decomposition(VMD), SHAP 등 시계열·설명가능성 기법과 결합. AI가 추출한 텍스트 기반 통화정책 지표와 비트코인 수익률 간의 선·후행 인과 구조를 분석.
- **핵심 발견**:
  - LLM 기반 통화정책 텍스트 지표가 비트코인 가격 동학과 통계적으로 유의한 관계를 보임.
  - Granger 인과·VMD 분해를 통해 통화정책 시그널과 비트코인 간 시점별 연관 구조를 식별.
  - "헤지" 여부는 시기·정책 국면에 따라 조건부로 달라짐.
- **한계·주의**: 텍스트 기반 통화 시그널의 측정 오차와 비트코인 시장의 높은 변동성·외생 충격이 인과 해석을 제약함.
- **CSS 관점 의의/흥미점**: LLM을 통해 정책 커뮤니케이션을 정량 변수로 전환하고 이를 금융 시계열 인과분석에 투입한, 텍스트-as-measure의 거시금융 응용 사례다.

## The Geoeconomics of Venture Capital: An Economic Complexity Approach
- **arXiv / 제출**: 2604.09187 / 2026-04
- **저자**: (벤처캐피털 경제복잡성 연구진)
- **연구질문**: 벤처캐피털(VC) 투자의 지리·산업 구조를 경제복잡성 이론으로 측정하면 지역·국가의 기술·투자 역량을 어떻게 설명할 수 있는가?
- **데이터**: 지역·국가 단위 VC 투자 데이터(산업별·지역별 투자 매트릭스).
- **LLM 기법·방법**: 경제복잡성 이론의 RCA/RVA(현시비교/현시벤처우위)와 고유벡터 기반 복잡성 지수(GCI/ETGCI)를 VC 데이터에 적용하여 지역의 투자 역량과 다각화 구조를 측정. 투자 분야 텍스트 분류·임베딩으로 산업 범주를 구조화하고, 정보이론 지표(Shannon entropy, Jensen-Shannon distance)로 포트폴리오 다양성·전문화를 정량화.
- **핵심 발견**:
  - VC 투자의 지리적 집중과 산업 전문화 패턴이 경제복잡성 지수로 체계적으로 포착됨.
  - 고복잡성 지역이 더 다각화되고 고부가 기술 분야에 투자하는 경향.
  - 정보이론 거리로 지역 간 투자 구조의 유사성·차별성을 정량 비교 가능.
- **한계·주의**: VC 데이터의 보고 편향·불완전성, 복잡성 지수의 해석이 데이터 범위·시점에 민감함.
- **CSS 관점 의의/흥미점**: 무역 데이터에서 발전한 경제복잡성 방법론을 VC·기술투자 지형 분석으로 이식하여, 지역 기술역량을 측정하는 새로운 정량 렌즈를 제시한다.

## Healthcare AI for Automation or Allocation? A Transaction Cost Economics Approach
- **arXiv / 제출**: 2604.16465 / 2026-04
- **저자**: (의료 AI·거래비용경제학 연구진)
- **연구질문**: 의료 AI는 업무를 "자동화(automation)"하는가 아니면 인력·자원을 "재배분(allocation)"하는가? 거래비용경제학(TCE)으로 이 선택을 어떻게 설명하는가?
- **데이터**: 의료 직무·업무 활동 데이터(O*NET 기반 task/DWA)와 의료 업무 텍스트.
- **LLM 기법·방법**: LLM을 활용해 의료 업무 활동을 거래비용 속성(자산 특수성, 불확실성, 빈도 등)으로 점수화하고, 자동화 가능성과 자원 재배분 가능성을 구분 측정. constrained JSON scoring으로 각 활동의 TCE 차원 점수를 산출하고, 자동화가 거래비용을 낮추는 경우와 재배분이 더 효율적인 경우를 이론적으로 매핑.
- **핵심 발견**:
  - 의료 AI의 효과는 단순 자동화가 아니라 업무·인력의 재배분 형태로 나타나는 경우가 많음.
  - 거래비용(자산 특수성·불확실성)이 높은 업무는 자동화보다 인간-AI 협업·재배분이 우세.
  - TCE 프레임이 AI 도입의 조직적 선택을 예측하는 데 유용.
- **한계·주의**: TCE 차원의 LLM 점수화가 주관적이며, 의료 현장의 규제·책임 구조 등 제도 변수가 단순화됨.
- **CSS 관점 의의/흥미점**: 노벨상급 조직경제학 이론(TCE)을 LLM 측정과 결합해 "AI가 무엇을 하느냐"보다 "조직이 AI를 어떻게 배치하느냐"를 설명, AI 도입의 조직론적 통찰을 제공한다.

## Proposing Topic Models and Evaluation Frameworks for Analyzing Associations
- **arXiv / 제출**: 2604.18919 / 2026-04
- **저자**: (토픽모델·평가프레임워크 연구진)
- **연구질문**: 텍스트에서 개념·집단 간 연상(association)을 분석하기 위한 토픽 모델과 그 평가 프레임워크를 어떻게 설계·검증할 것인가?
- **데이터**: 분석 대상 텍스트 코퍼스(연상 구조 분석용 문서 집합).
- **LLM 기법·방법**: BERTopic 등 임베딩 기반 토픽 모델링(text-embedding-3-large 등 임베딩 활용)과 LLM을 결합하여 토픽을 추출하고, 토픽 간·집단 간 연상 강도를 측정. 토픽 품질·해석가능성·연상 타당성을 평가하는 프레임워크를 제안하고, 정보이론·통계 지표로 토픽 일관성과 연상의 유의성을 검증.
- **핵심 발견**:
  - 임베딩 기반 토픽 모델이 전통적 토픽 모델보다 해석 가능하고 일관된 연상 구조를 산출.
  - 제안된 평가 프레임워크가 토픽 타당성·연상 강도를 체계적으로 비교 가능하게 함.
  - LLM 보조로 토픽 라벨링·해석의 신뢰성이 향상됨.
- **한계·주의**: 토픽 모델 결과가 임베딩·하이퍼파라미터에 민감하고, 연상의 "의미"에 대한 검증은 여전히 해석 의존적임.
- **CSS 관점 의의/흥미점**: 토픽 모델을 "연상 측정 도구"로 정식화하고 평가 프레임워크를 제안함으로써, CSS에서 흔히 임의적이던 토픽 분석에 방법론적 엄밀성을 더한다.

## AI Agents for Sustainable SMEs: A Green ESG Assessment Framework
- **arXiv / 제출**: 2605.00841 / 2026-05
- **저자**: Viet Trinh 외 (University of Economics and Law, UEL, 베트남)
- **연구질문**: AI 에이전트 파이프라인으로 중소기업(SME)의 친환경·ESG 성과를 자동 평가하고 개선 권고를 생성할 수 있는가?
- **데이터**: Flash Eurobarometer FL549 설문(27개 EU 회원국, 28,000개 이상 SME).
- **LLM 기법·방법**: n8n 자동화 플랫폼 위에 AI 에이전트 파이프라인을 구축. baseline(40%)/automated(60%) 분할에 RRSSV를 적용하고, 4개 ESG 축에 가중치(0.1, 0.5, 0.3, 0.1)를 부여. 지표 점수는 x_{c,q} = Σf·s / Σf 형태로 빈도 가중 합산하며, Gemini 2.0 Flash Lite로 ESG 개선 권고를 생성. 스키마 기반 구조화 출력으로 평가의 일관성을 확보.
- **핵심 발견**:
  - AI 에이전트가 대규모 SME 설문을 자동으로 ESG 지표로 변환·점수화하고 맞춤 권고를 생성.
  - 가중 지표 설계로 ESG 4축의 상대적 중요도를 반영한 종합 점수 산출.
  - n8n 기반 파이프라인이 확장 가능한 자동 평가 워크플로를 구현.
- **한계·주의**: 설문 자기보고 편향과 가중치 설정의 임의성, 권고의 실효성 검증 부재.
- **CSS 관점 의의/흥미점**: LLM 에이전트와 워크플로 자동화(n8n)를 결합해 정책 설문을 실용적 ESG 측정·자문 도구로 전환한, 응용 지향 CSS 파이프라인의 예시다.

## The Proxy Presumption: From Semantic Embeddings to Valid Social Measures
- **arXiv / 제출**: 2605.07409 / 2026-05
- **저자**: Baishi Li, Ta Yu, Kelvin Koa, Ke-Wei Huang (National University of Singapore)
- **연구질문**: 의미 임베딩(semantic embeddings)을 사회과학 구성개념(construct)의 대리변수(proxy)로 쓰는 관행은 타당한가? 임베딩 기반 측정의 구성타당도를 어떻게 보장할 것인가?
- **데이터**: NLP 17개 논문에 대한 포렌식 리뷰(측정 타당성 감사) 및 이론적 분석.
- **LLM 기법·방법**: 입장/종합(position/synthesis) 논문으로, Construct Validity Protocol(CVP)을 제안. 핵심으로 Proposition 1(회전 모호성, Rotational Ambiguity에 의한 비식별성 증명)을 통해 임베딩 축이 구성개념과 일대일 대응하지 않음을 보이고, Counterfactual Neutralization(Ĉ = f(e_obs) - f(e_base))로 기준 임베딩 대비 효과를 분리. Validity Cards라는 보고 체계를 도입하고, 17개 논문의 판별타당도(discriminant validity)를 감사(0 Yes / 11 Partial / 6 No).
- **핵심 발견**:
  - 임베딩 거리/유사도를 구성개념 측정으로 직접 쓰는 것은 회전 모호성 때문에 비식별 문제를 안음.
  - 검토된 NLP 논문 대부분이 판별타당도를 충분히 입증하지 못함(Yes 0건).
  - Counterfactual Neutralization과 Validity Cards로 측정 타당성을 부분적으로 회복·보고 가능.
- **한계·주의**: 제안 프로토콜의 실증적 부담이 크고, 모든 응용에 일률 적용하기 어려움.
- **CSS 관점 의의/흥미점**: "임베딩=구성개념 대리"라는 광범위한 암묵적 전제를 수학적으로 해체하고 측정타당도 점검 체계를 제시, LLM/임베딩 시대 CSS 측정의 인식론적 기준점을 세운다.

## Infini-News: Efficiently Queryable Access to 1.3 Billion Processed Common Crawl News Articles
- **arXiv / 제출**: 2605.18337 / 2026-05
- **저자**: Ruggero Marino Lazzaroni, Jana Lasser, Kirill Solovev (University of Graz)
- **연구질문**: 테라바이트급 CC-News 아카이브를 로컬 저장 없이 검색·서브셋팅 가능하게 만들어, 종단·다국가 미디어 연구의 진입장벽을 낮출 수 있는가?
- **데이터**: 2016년 8월~최신 스냅샷의 전체 CC-News(원시 WARC 180TB) 처리 결과, 약 13.5억(1.357B) 기사, 117개 월별 파티션, 222개국, 1,172개 ISO 639-3 언어.
- **LLM 기법·방법**: LLM 추론보다는 대규모 텍스트 측정 인프라 논문. trafilatura로 본문 추출, 언어식별 3종 분류기(GlotLID v3, lingua, CommonLingua의 byte-level CNN+attention) 적용, 5개 소스(ccTLD, Wikidata, 큐레이션 리스트, 구조적 HTML, corpus-language rule) 기반 지리귀속 cascade(83.4% 기사에 국가 부여, held-out precision 88.8%). Infini-gram mini(접미사배열/FM-index)로 임의 부분문자열을 sub-second(완전 코퍼스 p50 6.48ms)에 검색·온디맨드 데이터셋 구성.
- **핵심 발견**:
  - 검색 우선(retrieval-first) 설계로 전체 아카이브를 다운로드 없이 쿼리, 온디맨드 서브코퍼스 구성 가능.
  - 상용 Factiva(31개 언어) 대비 1,172개 언어로 커버리지가 압도적이며 고자원 언어에서도 분량 우위.
  - 2023년 이후 CCBot 차단(robots.txt) 물결로 기사량이 감소하는 구조적 편향을 문서화.
- **한계·주의**: 실시간성 부족(retrospective 분석용), 페이월 콘텐츠 부재, 지리귀속 41.9% 도메인 미해결·저자원 언어 식별 오류 가능.
- **CSS 관점 의의/흥미점**: LLM 기반 CSS의 "원료" 자체를 민주화하는 인프라로, 측정 이전 단계의 코퍼스 접근성이 연구 외적타당도를 좌우함을 보여주는 FAIR 자원이다.

## Engagement vs. Commitment: The Economic Trade-Offs of Polarizing News Content
- **arXiv / 제출**: 2605.18357 / 2026-05
- **저자**: Shunyao Yan (Santa Clara University), Klaus M. Miller (HEC Paris)
- **연구질문**: 양극화(polarizing) 뉴스 콘텐츠가 참여(engagement, 체류시간)와 헌신(commitment, 구독·유지)에 미치는 인과효과는 같은가, 다른가?
- **데이터**: 유럽 주요 "기록신문"의 40주 클릭스트림·구매기록(등록사용자 119,913명, 1,098,857 user-week), 17,776건 의회연설(BERT 학습용, Left 5,915/Right 5,931), 62,801건 기사 아카이브. 관측 기간에 자국 연방선거 포함.
- **LLM 기법·방법**: 기사별 양극화를 두 기준계로 측정. (1) party-referenced: 의회연설로 학습한 계층적 BERT(2단계: 양극화 탐지 후 좌/우 stance, hard-negative pair, 도메인 적응 사전학습)로 좌/우/중립 분류(in-sample F1 0.922/0.938). (2) reader-referenced: Gemini 2.5 Pro로 affective + 3개 이념 차원(경제/세계화/환경)을 1-5 척도 점수화(temperature 0, κ_w 0.63-0.78, GPT o3·Claude 3.7 Sonnet과 교차검증 97%+ 일치, 판별타당도 확보). 인과식별은 두 IV: 공급측 Bartik 도구(사용자 토픽선호 × 주간 양극화 공급 변화)와 수요측 선거 도구. asinh 변환·고차원 고정효과 LPM으로 추정.
- **핵심 발견**:
  - 양극화 콘텐츠 공급 증가는 참여(체류시간)는 높이나 구독은 높이지 못함(비대칭 trade-off).
  - 선거 등 정치 현저성이 높은 시기엔 같은 콘텐츠가 구독을 낮추고 이탈을 가속(affective 양극화가 가장 큰 괴리 유발, 추가 클릭당 주간 전환확률 약 1.6%p 하락).
  - 이념 대리변수로 본 이질성에서 확증편향(confirmation bias) 근거는 약하고, 반대편 콘텐츠 소비가 1:1 이상 증가하는 균형소비(balanced consumption)와 부합.
- **한계·주의**: 단일 유럽 신문·등록사용자 표본(참여도 높은 편향), 출판사 NDA로 일부 정보 비공개.
- **CSS 관점 의의/흥미점**: BERT(party-referenced)와 LLM(reader-referenced)을 같은 기사에 짝지어 두 기준계로 측정하고, 참여-헌신 비대칭의 affective/ideological 메커니즘을 검증 가능하게 만든 측정 프레임이 정교하다.

## Building Arabic NLP from the Ground Up: Twenty Years of Lessons, Failures, and Open Problems
- **arXiv / 제출**: 2605.20786 / 2026-05
- **저자**: Wajdi Zaghouani (Northwestern University in Qatar)
- **연구질문**: 20년간 아랍어 NLP 인프라·자원을 구축한 경험에서 저자원 언어 커뮤니티를 위한 NLP, 나아가 NLP에서 CSS로의 전환에 대해 어떤 교훈·실패가 도출되는가?
- **데이터**: 저자가 참여한 20년치 프로젝트(Arabic Treebank, QALB, AraP-Tweet, ADHAR 혐오발언, 청소년 우울 코퍼스, WANLP/CheckThat! 공동작업 등)에 대한 회고적 종합.
- **LLM 기법·방법**: 입장/회고(position/reflection) 논문으로 새 모델·실험은 없음. 대신 측정 인식론을 다룸: 데이터셋은 기술 산물이 아니라 사회 인프라(커뮤니티)이며, shared task는 평가가 아니라 연구 도구라는 주장. 특히 사회현상 측정에서 annotator 불일치를 "노이즈"가 아니라 "신호"로 보존해야 한다는 점(majority-vote gold label이 사회적으로 중요한 분포 정보를 폐기), 그리고 NLP가 CSS로 갈 때 construct validity·measurement validity 같은 사회과학 측정론을 학습해야 한다고 강조.
- **핵심 발견**:
  - 가장 어려운 문제는 언어적이 아니라 사회·제도·인식론적(임상 파트너십, 정책 연계, annotator 후생 등).
  - annotator 불일치는 데이터이며, per-annotator 라벨·소프트 라벨 공개가 측정 규범이 되어야 함.
  - MSA(표준아랍어) 자원이 방언으로 깨끗이 전이된다는 가정은 틀렸고, 위세변종 우선 구축은 다수 사용자를 소외시킴.
- **한계·주의**: 단일 연구자 관점의 부분적 서술이며, 다운스트림 실제 영향에 대한 체계적 실증평가는 부재.
- **CSS 관점 의의/흥미점**: "측정 타당도"와 "불일치=신호"라는 사회과학 측정론을 NLP/CSS 실무에 정면으로 요구하며, 도구 제작 이면의 사회적 조건을 성찰하게 한다.

## JobArabi: An Arabic Corpus and Analysis of Job Announcements from Social Media
- **arXiv / 제출**: 2605.20960 / 2026-05
- **저자**: Wajdi Zaghouani, Shimaa Amer Ibrahim, Mabrouka Bessghaier (Northwestern Qatar), Houda Bouamor (CMU Qatar)
- **연구질문**: 아랍어 소셜미디어(X/Twitter)의 채용공고 담론을 대규모로 수집·분석하여 노동시장 커뮤니케이션과 사회언어적 패턴(성별 언어, 지역 변이, 감정)을 어떻게 측정할 것인가?
- **데이터**: 2024.01-2025.10 X/Twitter 공개 게시물 20,528건(2024 8,316 + 2025 12,212), Meltwater 미디어모니터링으로 수집, 타임스탬프·engagement·geolocation 메타데이터 포함.
- **LLM 기법·방법**: 핵심 기여는 언어학적으로 설계된 21개 키워드 패밀리 쿼리(형식/구어 register, 동의어·연어, 복수형, 성별 굴절형, 즉시성 마커)로, 단순 영어 직역 키워드의 낮은 recall 문제를 해결. 수집 후 감정/세분 감정 분석과 BERTopic류 토픽 분석, 도메인 특화 NER 설계(JOB_TITLE, COMPANY, SKILL, DEGREE 등)를 제안. fastText 언어식별·아랍어 전처리 파이프라인 사용.
- **핵심 발견**:
  - 2025년 채용 언급이 전년 대비 46.8% 급증, 97.8%가 직접 구인공고, 71.21%가 사우디아라비아에서 발생(걸프 집중).
  - 성별 언어가 지속되나 포용적 표현("for both genders")이 긍정 감정과 연관되며 변화 중(사회언어적 전환).
  - 2024 감정의 89.28%가 중립(채용공고의 제도적 격식)이고, 분노/슬픔은 비포용·불투명 채용 관행에 대한 커뮤니티 비판으로 해석.
- **한계·주의**: 키워드 기반 recall/precision 한계(암묵적 채용표현 누락, "리플라이"의 메타담론 혼입), 플랫폼·지역(걸프) 편향, 이미지 텍스트 미처리(OCR 부재).
- **CSS 관점 의의/흥미점**: 언어학적으로 정교한 쿼리 설계로 저자원 언어 노동시장을 실시간 센서처럼 측정하고, 채용 언어의 사회언어적 변동(성별·포용)을 감정과 연결한 점이 흥미롭다.

## Audience Engagement with Arabic Women's Social Empowerment and Wellbeing: A Decadal Corpus
- **arXiv / 제출**: 2605.22204 / 2026-05
- **저자**: Wajdi Zaghouani, Mabrouka Bessghaier, Shimaa Amer Ibrahim (Northwestern Qatar), MD. Rafiul Biswas (Hamad bin Khalifa University)
- **연구질문**: 아랍어 페이스북에서 여성 권익·웰빙 담론이 어떻게 프레이밍되고, 청중이 감정 반응(reaction)으로 어떻게 집합적으로 응답하는가를 10년 규모로 측정할 수 있는가?
- **데이터**: 2013.11-2024.07 공개 페이스북 게시물 252,487건, 77개국 51,660개 페이지, 2.67억 user interaction, 41개 변수(6종 감정 reaction 포함). CrowdTangle API로 수집(API 종료로 대체 불가한 역사적 아카이브).
- **LLM 기법·방법**: 아랍어 최적화 BERTopic 파이프라인(컨텍스트 임베딩이 방언에서 약하므로 의도적으로 어휘빈도 TF-IDF 사용, 상위 4,000 uni/bigram → SVD 100차원 → UMAP 5차원 → HDBSCAN 클러스터링, 최대 20개 토픽). 게시물별 6종 페이스북 reaction(Love, Haha, Wow, Sad, Angry, Care)을 토픽별로 집계해 감정-토픽 정렬을 정량화. fastText 언어식별로 비아랍어 격리.
- **핵심 발견**:
  - 해석가능한 최대 20개 토픽 도출, Love+Haha가 전체 reaction의 80%+로 권익 담론이 주로 긍정·유머로 처리됨.
  - 폭력·차별 토픽은 Sad·Angry 비중이 높아 집합적 공감·도덕적 우려를 반영(감정-토픽 정렬).
  - reaction은 모호한 신호(같은 Love도 공감/풍자일 수 있음)이므로 개별 stance가 아닌 집합적 affective salience 지표로 해석해야 함.
- **한계·주의**: 페이스북 단일 플랫폼·공개 콘텐츠 편향, CrowdTangle 커버리지 한계, 방언 분포 불균형, reaction의 본질적 다의성.
- **CSS 관점 의의/흥미점**: 어휘기반 BERTopic으로 해석가능성을 확보하면서 reaction을 "측정된 집합 감정"으로 다룬 점, 그리고 reaction의 다의성을 명시적으로 경계한 측정 신중함이 돋보인다.

## Cohesion-6K: An Arabic Dataset for Analyzing Social Cohesion and Conflict in Online Discourse
- **arXiv / 제출**: 2605.22447 / 2026-05
- **저자**: Aisha Ali Al-Athba, Wajdi Zaghouani (Hamad Bin Khalifa University, Northwestern Qatar)
- **연구질문**: 온라인 담론에서 분열(conflict)과 통합(cohesion)의 미묘한 상호작용을 다섯 범주의 연속선으로 라벨링하고, 분열 담론이 불균형적 가시성(engagement)을 끄는지 측정할 수 있는가?
- **데이터**: 이스라엘의 팔레스타인 점령 관련 아랍어 공개 페이스북 게시물 6,000건(수작업+ChatGPT 보조 라벨링). 5개 source type(정치조직 1,440, 뉴스 2,070, 인권단체 950, 공인 860, 풀뿌리 680), engagement 2,640만. 비라벨 약 20만 건도 공개 예정.
- **LLM 기법·방법**: 5개 담론 범주(Conflict, Resolution, Community Engagement, Supportive Interactions, Shared Values)를 cohesion 연속선으로 설계. 이중단계(dual-stage) 라벨링: 앞 3,000건은 native 아랍어 annotator 3인 수작업, 뒤 3,000건은 ChatGPT(GPT-4)로 사전라벨 후 동일 annotator가 검증. 신뢰도는 Cohen's κ=0.85(우수), gold set 300건 기준 수작업 정확도 평균 92%, AI 검증 후 88-91%. 독립표본 t-test로 conflict vs resolution engagement 차이 검정(p<0.01).
- **핵심 발견**:
  - Conflict 게시물이 resolution 대비 2-4배 많은 사용자 상호작용을 받음(분열 담론의 불균형 가시성, p<0.01).
  - 강한 이념(친팔/친이스라엘) 페이지가 전체 engagement의 77%를 점유, 평화·대화 이니셔티브는 8%에 그침.
  - 하이브리드 인간-AI 라벨링(88-91%)이 순수 수작업(90-94%)에 근접하면서 시간·비용을 크게 절감.
- **한계·주의**: 단일 플랫폼·특정 역사 시점, single-label 설계로 동시다발 담론 기능 포착 한계, annotator 주관·아랍어 반어/종교표현의 해석 난점.
- **CSS 관점 의의/흥미점**: "갈등 탐지"를 넘어 "사회적 통합"을 다섯 범주로 측정하는 건설적 담론 분류를 도입하고, 인간-AI 협업 라벨링의 비용-품질 trade-off를 정량 검증한 점이 실용적이다.

## Generative AI and the Reorganization of Labor Demand
- **arXiv / 제출**: 2605.23159 / 2026-05
- **저자**: Fangyan Wang, Zaiyan Wei, Yang Wang (Purdue University, Mitch Daniels School of Business)
- **연구질문**: 생성형 AI 확산에 대응해 기업은 어디서 채용하는지(hiring reallocation), 무엇을 채용하는지(within-job redesign)를 어떻게 바꾸며, 이 조정은 직급 사다리(job ladder)에 따라 어떻게 다른가?
- **데이터**: Lightcast의 미국 전국 온라인 구인공고(2021.01-2025.06 원시 1.88억 건). occupation×seniority×industry 셀별 5% 반복 무작위 표집으로 최종 9,373,092건.
- **LLM 기법·방법**: 동적·게시물 단위 생성형 AI 노출 지수를 2단계 LLM 파이프라인으로 구성. 1단계 Llama-3.1-8b-instant로 공고당 3-10개 과제 추출 및 skill group(specialized=가중 2, common=가중 1) 매칭. 2단계 GPT-5-nano로 각 과제를 E0(무노출)/E1(직접노출)/E2(간접노출)로 분류(Eloundou et al. 기준 "동일 품질에 시간 50%+ 절감"). 공고 단위 지수 β = E1 + 0.5×E2(주측정), 정규화 가중합. 조정 마진은 Kitagawa 분해(3중 확장: 구성효과=reallocation, within-cell 효과=redesign, 상호작용)와 Oaxaca-Blinder 분해로 분리.
- **핵심 발견**:
  - 생성형 AI 노출은 고정이 아니라 동적: 2022 초까지 상승, 2023 하락, 이후 부분 회복(직업 고정 속성 아님).
  - 2023 3분기 이후 총노출 하락의 52%가 hiring reallocation, 39.46%가 within-job redesign, 8.54%가 상호작용. Oaxaca-Blinder로 직업구성 변화가 관측가능 특성 기인분의 ~90% 설명.
  - 조정은 직급별로 상이: 시니어는 더 일찍·주로 reallocation으로, 주니어는 reallocation·redesign·상호작용이 고루 기여.
- **한계·주의**: 구인공고는 실현된 고용이 아닌 수요 측면이며, LLM 노출 분류의 측정 오차·표집 의존성 존재.
- **CSS 관점 의의/흥미점**: 직업 단위 고정 노출 측정을 게시물 단위 동적 측정으로 전환하고, Kitagawa/Oaxaca 분해로 "직무 재설계 vs 채용 재배분"을 분리한 점이 노동경제 측정론에 기여한다.

## Generative AI impacts on intra-urban inequality and skill premium in Beijing
- **arXiv / 제출**: 2605.25505 / 2026-05
- **저자**: Xiliu He, Haoxiang Zhao, Yuan Lai 외 (Tsinghua University School of Architecture; ZODA LAB)
- **연구질문**: 생성형 AI(GenAI)는 도시 내 불평등을 평준화하는가, 심화하는가? 베이징을 사례로 GenAI 노출의 공간 집중, 숙련 프리미엄 변화, 인과 메커니즘을 측정할 수 있는가?
- **데이터**: 베이징 온라인 구인공고 4,995,615건(2018-2024, RESSET Big Data Platform: 51job, Zhaopin, BOSS Zhipin, Liepin), 동네(neighborhood) 단위로 POI·야간조도·NDVI·인구 등 다출처 지리데이터와 매칭. 1,605개 표준직업.
- **LLM 기법·방법**: 동네 단위 GenAI Exposure Index를 RAG 기반 직업매칭 + 5개 SOTA LLM 앙상블로 구성. (1) Qwen3-Embedding-4B로 중국 2022 직업분류사전을 벡터화한 지식베이스를 만들고, 공고를 의미유사도 검색으로 표준직업에 매칭(정확도 93%). (2) ChatGPT-4o, Gemini-2.5-pro, Claude-3.5-Sonnet, GLM-4, Deepseek-R1 5개 모델이 각 직업을 E0/E1/E2/E3로 독립 분류, 5회 반복(총 25회) 평균으로 모델 편향 완화(쌍별 상관 0.66-0.86, 전문가 검토 89% 일치). 인과식별은 사전결정(2018) 노출을 처치로 한 DID(event study로 평행추세 검증, randomization inference p=0.004, Bartik shift-share IV로 보강) 및 triple-DID로 de-skilling·crowding 메커니즘 검정.
- **핵심 발견**:
  - GenAI 노출이 도심 핵심(중관춘·금융가·CBD "골든 트라이앵글")에 공간적으로 고착(lock-in)되어 도시 내 AI 격차 심화.
  - 2023년 이후 고노출 동네는 고숙련 노동 공급은 늘되 임금은 정체·하락하는 "high-skill trap"(SBTC 이론과 배치). DID 추정 처치효과 임금 약 13.1% 하락.
  - 임금 패널티는 task de-skilling(GenAI×교육 상호작용 -1.286)과 노동시장 crowding(GenAI×job-market heat -1.619)의 두 채널로 구동.
- **한계·주의**: 베이징 단일 도시 표본, 구인공고는 고용 스톡이 아닌 흐름이라 변동성 과대표집 가능, 단기 관측으로 장기 생산성·신직업 출현 미포착.
- **CSS 관점 의의/흥미점**: 5개 LLM 앙상블로 모델 편향을 줄인 노출 측정과 사전결정 DID·randomization inference·Bartik IV를 결합한 엄밀한 인과설계로, GenAI가 숙련 프리미엄을 "역전"시키는 high-skill trap을 미시 공간 단위로 측정한 야심작이다.
