sources/userguide.json — Yield Curves (162~177페이지) 요약

해당 페이지는 curveconfig.xml 파일에서 YieldCurve(수익률 곡선) 를 어떻게 구성하는지 
상세히 설명합니다.

1. Yield Curve 최상위 XML 요소 (162~164쪽)

각 YieldCurve 노드는 다음과 같은 최상위 요소들로 구성됩니다:

| 요소                       | 설명                                                     
|
|----------------------------|----------------------------------------------------------
----------------------------------------|
| CurveId                    | 고유 식별자                                              
|
| CurveDescription           | 설명 (선택)                                              
|
| Currency                   | 통화                                                     
|
| DiscountCurve              | 부트스트래핑 시 할인에 사용할 곡선 ID. 비워두거나 자신과 
같으면 자기 자신 사용                   |
| Segments                   | 곡선을 구성하는 세그먼트들 (핵심)                        
|
| InterpolationVariable      | 보간 변수: Zero(연속복리 제로금리), Discount(할인계수), 
Forward(순간선도금리) (기본값: Discount) |
| InterpolationMethod        | 보간 방법: LogLinear, Linear, CubicSpline 등 (기본값: 
LogLinear)                                 |
| MixedInterpolationCutoff   | 혼합 보간 시 첫 번째 방법을 적용할 구간 수 (기본값: 1)   
|
| YieldCurveDayCounter       | 내부 일수계산 기준 (기본값: A365)                        
|
| Tolerance                  | 부트스트래핑 허용오차 (기본값: 1.0×10⁻¹²)                
|
| Extrapolation              | 외삽 여부 (기본값: True)                                 
|
| ExtrapolationMethod        | 외삽 방식: ContinuousForward 또는 DiscreteForward        
|
| ExcludeT0FromInterpolation | t=0 시점을 보간에서 제외할지 여부 (기본값: False)        
|
| BootstrapConfig            | 반복 부트스트래핑 설정 (선택)                            
|

2. Segments Node — 세그먼트 유형들 (164~177쪽)

YieldCurve는 여러 세그먼트로 구성되며, 각 세그먼트는 Type에 따라 구조가 다릅니다.

(1) Direct Segment (165쪽)

- Type: Zero 또는 Discount
- 제로금리나 할인계수를 직접 명시 (부트스트래핑 불필요)
- 와일드카드 사용 가능 (예: ZERO/RATE/EUR/*)

(2) Simple Segment (165~166쪽)

- Type: Deposit, FRA, Future, OIS, Swap, BMA Basis Swap
- 시장 악성으로부터 곡선을 부트스트래핑
- 주요 하위 요소:
  - ProjectionCurve — 변동금리 투영용 곡선 ID (선택)
  - PillarChoice — 부트스트래핑 기둥 결정 방식
  - DuplicatePillarPolicy — 중복 기둥 처리 방식 (KeepLast, KeepFirst, KeepAll, 
ThrowError)
  - Priority — 세그먼트 우선순위 (낮을수록 높은 우선순위, 기본값 0)
  - MinDistance — 인접 세그먼트 간 최소 거리(일)

(3) Average OIS Segment (167쪽)

- Type: Average OIS
- 평균 OIS 스왑 악성 보유 (USD Overnight Index Swap 등)
- 각 악성은 복합 악성(CompositeQuote) 으로, 일반 IRS 악성 + OIS-LIBOR 베이시스 스프레드 
악성으로 구성
  - RateQuote: IRS 악성 ID
  - SpreadQuote: OIS-LIBOR 베이시스 스프레드 악성 ID

(4) Tenor Basis Segment (167~168쪽)

- Type: Tenor Basis Swap 또는 Tenor Basis Two Swaps
- Tenor Basis Swap: 서로 다른 텐더의 Ibor를 스왑
- Tenor Basis Two Swaps: 두 개의 공정 스왑 간 고정금리 차이
- 두 개의 투영 곡선 노드: ProjectionCurveReceive(짧은 텐더), ProjectionCurvePay(긴 텐더)

(5) Cross Currency Segment (168~170쪽)

- Type: FX Forward, Cross Currency Basis Swap, Cross Currency Fix Float Swap
- FX Forward:
  - DiscountCurve: 상대 통화 할인 곡선
  - SpotRate: 현물 FX 악성 ID
- Cross Currency Basis Swap:
  - DiscountCurve, SpotRate 외에
  - ProjectionCurveDomestic: 자국 통화 변동금리 투영 곡선
  - ProjectionCurveForeign: 상대 통화 변동금리 투영 곡선

(6) Zero Spread Segment (170쪽)

- Type: Zero Spread
- 기준 곡선 대비 스프레드 형태로 곡선 구축
- ReferenceCurve 노드로 기준 곡선 지정
- 악성은 ZERO/YIELD_SPREAD/... 형식

(7) Fitted Bond Segment (170~172쪽)

- Type: FittedBond
- 유동 채권 가격에 곡선을 피팅
- IborIndexCurves: 채권에 필요한 Ibor 지수와 추정 곡선 매핑
- ExtrapolateFlat: 첫 번째/마지막 만기 전후로 평탄 외삽
- 보간 방법: NelsonSiegel, Svensson, ExponentialSplines 등 사용
- BootstrapConfig에서 Accuracy, GlobalAccuracy, MaxAttempts(최대 시도 횟수) 설정

(8) Bond Yield Shifted Segment (172~173쪽)

- Type: Bond Yield Shifted
- 유동 채권 수익률로 조정된 곡선 구축
- 하나의 유동 채권만으로도 구축 가능 (NelsonSiegel 피팅이 불안정한 경우 유용)
- ReferenceCurve: 스프레드 계산의 기준이 되는 곡선
- 조정값 = 채권 만기수익률과 기준 곡선의 차이의 평균

(9) Yield Plus Default Segment (173~174쪽)

- Type: Yield Plus Default
- 기준 곡선 + 디폴트 곡선들의 가중합으로 올인 할인 곡선 구축
- ReferenceCurve, DefaultCurves, Weights 지정
- 디폴트 곡선은 기준 곡선과 다른 통화여도 허용
- 할인계수: $P(0,t) = \prod_i S_i(t)^{(1-R_i)w_i}$

(10) Weighted Average Segment (174~175쪽)

- Type: Weighted Average
- 두 기준 곡선의 순간선도금리를 가중합산하여 비표준 Ibor 곡선 구축 (예: Euribor 2M을 
1M+3M으로)
- 할인계수: $P(0,t) = P_1(0,t)^{w_1} P_2(0,t)^{w_2}$

(11) Ibor Fallback Segment (175쪽)

- Type: Ibor Fallback
- 무위험금리(RFR) + 스프레드로 Ibor 지수 투영 곡선 구축
- IborIndex, RfrCurve(RFR 곡선), RfrIndex, Spread 지정

(12) Discount Ratio Segment (176~177쪽)

- Type: Discount Ratio
- 세 개의 입력 곡선(기준/분자/분모)으로부터 할인계수 구축
- 공식: $P(0,t) = P_b(0,t) \cdot P_n(0,t) / P_d(0,t)$
- 주 사용처: "CCY1-IN-CCY2" 할인 곡선 구축 (예: GBP 담보화된 EUR 할인 곡선)
- 예시: BaseCurve=EUR1D, NumeratorCurve=GBP-IN-USD, DenominatorCurve=EUR-IN-USD

3. 주요 특징

- 모든 세그먼트 유형(DiscountRatio, AverageOIS 제외)에서 Quote 요소에 optional="true" 
속성 부여 가능
- 와일드카드를 통한 대량 악성 로딩 지원
- Priority와 MinDistance를 통한 세그먼트 간 중복/충돌 해결 메커니즘
- 부트스트래핑이 필요한 세그먼트(Simple, AverageOIS, TenorBasis, CrossCurrency)와 직접 
지정 세그먼트(Direct), 파생/조합 세그먼트(ZeroSpread, FittedBond, BondYieldShifted, 
YieldPlusDefault, WeightedAverage, IborFallback, DiscountRatio)로 분류