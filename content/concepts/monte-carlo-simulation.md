---
sources: [summaries/userguide.md]
brief: Monte Carlo simulation in ORE for risk analytics, exposure, and XVA.
---

# Monte Carlo Simulation in ORE

ORE는 몬테카를로 시뮬레이션을 핵심 엔진으로 사용하여 포트폴리오 가격 평가, 익스포저 예측, XVA 계산, 시장 리스크 분석을 수행합니다. 시뮬레이션은 [[summaries/userguide]] 문서에 상세히 기술되어 있습니다.

## 시뮬레이션 구성 요소

몬테카를로 시뮬레이션은 `simulation.xml` 파일로 설정되며, 세 가지 주요 블록으로 구성됩니다:

### Parameters (파라미터)
- **Grid**: 시뮬레이션 시간 그리드 (예: 1M, 3M, 6M, 1Y, …)
- **TimeStepsPerYear**: 확률 과정 이산화를 위한 연간 최소 시간 단계 수
- **Calendar**: 날짜 조정용 달력
- **DayCounter**: 날짜-시간 변환
- **Sequence**: 난수 생성기 유형 (SobolBrownianBridge, Sobol, PseudoRandom 등)
- **Seed**: 난수 시드
- **Samples**: 몬테카를로 경로 수 (기본 1,000)
- **Ordering**: 변량 순서 (Steps, Paths, Sobol 등)
- **DirectionIntegers**: Sobol 생성기용 방향 정수
- **CloseOutLag / MporMode**: 증거금 기간(MPoR) 설정 (StickyDate 또는 ActualDate)

### CrossAssetModel (교차 자산 모델)
모델 구성:
- **LGM (Linear Gauss Markov)**: 각 통화의 금리 모델
- **FX**: 기준 통화 대비 환율 모델 (CrossCcyLGM)
- **Equity**: 주식 모델 (CrossAssetLGM)
- **Inflation**: 인플레이션 모델 (DodgsonKainth 또는 JarrowYildirim)
- **Commodity**: 원자재 모델 (CommoditySchwartz)
- **Correlation**: 위험 요소 간 순간 상관관계

### Market (시장)
시뮬레이션된 위험 요소를 수익률 곡선과 변동성 표면으로 변환합니다. 주요 설정:
- **통화**: 모델과 포트폴리오에 포함된 모든 통화 명시
- **변동성 시뮬레이션**: ATM 전용(전체 스마일 유지) 또는 전체 표면/스마일 시뮬레이션
- **스마일 동적 모델**: StickyStrike, StickyMoneyness, StickySABR
- **곡선 대수(CurveAlgebra)**: 스프레드 연산 등 연결 곡선 정의
- **일수 계산, 보간, 외삽 방식**

## 시뮬레이션 유형 및 활용

### 고전적 시뮬레이션 vs 아메리칸 몬테카를로(AMC)
- **고전적 시뮬레이션**: 미래 모든 시점에서 모든 거래의 NPV를 계산하여 NPV 큐브 생성
- **AMC**: 조기 행사 가능 상품(버뮤다 스왑션, 멀티레그 옵션 등)의 익스포저 생성을 위해 사용. 회귀 기반 조건부 기대값 추정

AMC 사용 시 LGM 평균회귀를 0으로 설정하고 고차 회귀 다항식을 사용하여 고전적 결과와 일치시켜야 합니다. 관련 개념: [[concepts/american-monte-carlo]]

### 측도 선택
시뮬레이션 측도(LGM, Bank Account, T-Forward)에 따라 최대 익스포저(PFE)가 달라지지만 기대 익스포저(EPE)는 측도 독립적입니다. 장기 시뮬레이션(예: 50년 만기 스왑)에서는 Shift 변환(T-Forward 측도)을 통해 수치적 안정성을 확보합니다.

### 시나리오 생성
`scenarioGeneration` 분석 유형은 시뮬레이션 시장의 기본 시나리오를 내보내고, 통계(분포)를 계산합니다. 관련 개념: [[concepts/scenario-analysis]]

## 성능 최적화

ORE는 성능 향상을 위해 다음 기술을 지원합니다:
- **멀티스레딩**: 병렬 익스포저 시뮬레이션 (`nThreads` 파라미터)
- **AAD (Algorithmic Differentiation)**: 민감도 계산 가속 (CVA 민감도: bump & revalue 48초 → AAD 2초)
- **GPU 병렬화**: 아직 개발 중이지만 AAD와 함께 GPU를 활용한 추가 가속 예정

관련 개념: [[concepts/sensitivity-analysis]], [[concepts/xva]]

## 주요 응용

몬테카를로 시뮬레이션은 다음 분석의 기반이 됩니다:
- **익스포저 계산**: EPE, ENE, PFE, Basel 측정
- **가치 조정(XVA)**: CVA, DVA, FVA, COLVA, MVA, KVA
- **동적 초기 증거금(DIM) 및 동적 SIMM**: AMC 시뮬레이션 내 센서티비티 생성
- **신용 포트폴리오 모델**: 신용부도, 등급 이행, 파생상품 PnL 통합

## 결론

ORE의 몬테카를로 시뮬레이션 프레임워크는 유연성과 성능을 모두 갖춘 종합적인 리스크 분석 도구입니다. 다양한 자산 클래스, 모델, 시장 설정을 지원하며, AMC, AAD, GPU 등의 기술을 통해 확장성과 정확성을 제공합니다.