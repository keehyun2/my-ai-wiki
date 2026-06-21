---
query: "sources 에 userguide.json 에서 162~177 페이지의 yeild curve 관련해서 정리해주세요"
---

먼저 index.md와 userguide의 summary를 확인하겠습니다.summary에서 확인한 바에 따르면, Yield Curves 섹션은 `sources/userguide.json`의 162~177페이지에 해당합니다. 이 내용을 가져오겠습니다.이제 162~177페이지의 내용을 정리하겠습니다.

---

## Yield Curves (curveconfig.xml, 162~177페이지) 정리

`curveconfig.xml`은 ORE에서 포트폴리오 가격결정에 필요한 다양한 기간구조(Term Structure)를 설정하는 단일 설정 파일입니다. 이 파일은 **수익률 곡선(Yield Curves)** 을 비롯해 디폴트 곡선, 인플레이션 곡선, 주식 선물가격 곡선, 다양한 변동성 구조 등을 정의합니다. (p.162)

### 5.7.1 Yield Curves — 최상위 XML 요소

각 `YieldCurve` 노드는 다음과 같은 최상위 요소들로 구성됩니다 (p.162):

| 요소 | 설명 |
|------|------|
| **CurveId** | 수익률 곡선의 고유 식별자 |
| **CurveDescription** | 곡선 설명 (생략 가능) |
| **Currency** | 곡선의 통화 |
| **DiscountCurve** | 부트스트랩 시 할인에 사용할 곡선의 CurveId. 비워두면 자기 자신 사용 |
| **Segments** | 곡선을 구성하는 세그먼트 (자식 요소) |
| **InterpolationVariable** (선택) | 보간 변수. `Discount`(기본값), `Zero`, `Forward` 중 선택 (p.164, Table 17) |
| **InterpolationMethod** (선택) | 보간 방법. `LogLinear`(기본값) 등 (Table 18 참조) |
| **MixedInterpolationCutoff** (선택) | 혼합 보간 시 첫 번째 방법 적용 구간 수, 기본값 1 |
| **YieldCurveDayCounter** (선택) | 내부 날짜계산 기준일. 기본값 A365 |
| **Tolerance** (선택) | 부트스트래핑 근찾기 허용오차. 기본값 1.0×10⁻¹². `BootstrapConfig.Accuracy` 사용 권장 |
| **Extrapolation** (선택) | 외삽 활성화 여부 (`True`/`False`), 기본값 `True` |
| **ExtrapolationMethod** (선택) | 외삽 방식: `ContinuousForward`(마지막 기둥일 이후 순간선도 일정), `DiscreteForward` (p.163) |
| **ExcludeT0FromInterpolation** (선택) | t₀ 시점을 보간에서 제외. `True`로 설정하면 시장 기둥일(pillar dates)에서만 보간. 기본값 `False` (p.164) |
| **BootstrapConfig** (선택) | 반복 부트스트랩 세부 설정 (섹션 5.7.20) |

### Segments 노드 — 세그먼트 유형

Segments 노드는 수익률 곡선을 구성하는 제로금리/할인계수/상품들을 정의하며, 다음과 같은 세그먼트 유형을 지원합니다:

#### 1. **Direct Segment** (p.165)
- **Type**: `Zero` 또는 `Discount`
- 제로금리나 할인계수를 직접 명시. 부트스트랩 불필요
- `Quotes`는 `market.txt`의 인용문을 참조하며, 와일드카드(`*`) 지원
- `Conventions`는 `conventions.xml`의 노드 ID 참조

#### 2. **Simple Segment** (p.165-166)
- **Type**: `Deposit`, `FRA`, `Future`, `OIS`, `Swap`, `BMA Basis Swap`
- 예금, FRA, 선물, OIS, 스왑 등의 시장 상품 인용문을 보유. 부트스트랩으로 할인곡선 도출
- **ProjectionCurve** (선택): 부동금리 전망용 곡선 ID. 생략 시 자기 자신
- **PillarChoice**: `MaturityDate`, `LastRelevantDate`(기본값), `NoPillar`, `StartDate` 등
- **DuplicatePillarPolicy**: 동일 기둥일 처리 방식 (`KeepLast`(기본값), `KeepFirst`, `KeepAll`, `ThrowError`)
- **Priority** (정수): 세그먼트 우선순위. 낮을수록 높은 우선순위, 기본값 0
- **MinDistance**: 세그먼트 간 최소 이격 일수 (기본값 1)

#### 3. **Average OIS Segment** (p.167)
- **Type**: `Average OIS`
- 평균 OIS 스왑 상품 인용문 보유
- 각 인용문은 **CompositeQuote**로, RateQuote(바닐라 IRS) + SpreadQuote(OIS-LIBOR 베이시스 스프레드)로 구성

#### 4. **Tenor Basis Segment** (p.167-168)
- **Type**: `Tenor Basis Swap` 또는 `Tenor Basis Two Swaps`
- 텐더 베이시스 스왑 상품 인용문
- **ProjectionCurveReceive** (수취측 단기텐더 지수 전망) + **ProjectionCurvePay** (지급측 전망), 둘 중 하나는 필수

#### 5. **Cross Currency Segment** (p.168-170)
- **Type**: `FX Forward`, `Cross Currency Basis Swap`, `Cross Currency Fix Float Swap`
- FX 선물 또는 크로스커런시 베이시스 스왑 인용문
- **DiscountCurve**: 상대통화 할인용 곡선 ID
- **SpotRate**: FX 현물환율 인용문 ID
- 크로스커런시 베이시스 스왑의 경우 **ProjectionCurveDomestic** 및 **ProjectionCurveForeign** 선택적 추가

#### 6. **Zero Spread Segment** (p.170)
- **Type**: `Zero Spread`
- 기준 수익률 곡선 대비 **스프레드** 형태로 표현된 곡선
- **ReferenceCurve**: 기준 곡선 ID
- 인용문 형식: `ZERO/YIELD_SPREAD/EUR/BANK_EUR_LEND/A365/2Y` 등

#### 7. **Fitted Bond Segment** (p.170-172)
- **Type**: `FittedBond`
- **유동성 채권 가격**에 피팅(Fitting)하여 곡선 구축
- **IborIndexCurves**: 채권에 필요한 Ibor 지수와 전망곡선 매핑
- **ExtrapolateFlat**: 첫 번째/마지막 채권 만기 이전/이후 평탄 외삽
- **InterpolationMethod**로 `NelsonSiegel`, `Svensson`, `ExponentialSplines` 지원
- `BootstrapConfig`에서 Accuracy, GlobalAccuracy, DontThrow, MaxAttempts 설정 가능 (p.171)

#### 8. **Bond Yield Shifted Segment** (p.172-173)
- **Type**: `Bond Yield Shifted`
- **채권 수익률을 기준으로 조정된 곡선**
- **ReferenceCurve**: 스프레드 계산용 기준 곡선
- 채권의 듀레이션 시점에서 YTM과 기준곡선 간 스프레드 평균으로 조정. 유동 채권이 적은 경우 유용
- 하나의 유동 채권만으로도 구축 가능 (Nelson-Siegel 피팅보다 안정적)

#### 9. **Yield Plus Default Segment** (p.173-174)
- **Type**: `Yield Plus Default`
- **기준 곡선 + (가중합) 디폴트 곡선**으로 all-in 할인곡선 구축
- **ReferenceCurve**, **DefaultCurves** 목록, **Weights**(가중치) 필요
- 순간선도(instantaneous forward rate) 수준에서 합산
- 결과 할인계수: $P(0,t) = \prod_i S_i(t)^{(1-R_i)w_i}$ (p.174)

#### 10. **Weighted Average Segment** (p.174-175)
- **Type**: `Weighted Average`
- 두 기준 곡선의 **순간선도의 가중합**으로 새 곡선 구축
- 비표준 Ibor 전망곡선 구축에 활용 (예: 1M와 3M 곡선으로 2M 전망)
- 할인계수: $P(0,t) = P_1(0,t)^{w_1} \cdot P_2(0,t)^{w_2}$

#### 11. **Ibor Fallback Segment** (p.175)
- **Type**: `Ibor Fallback`
- **무위험금리(RFR) + 스프레드**로 Ibor 지수 전망곡선 구축
- **RfrCurve**, **RfrIndex**, **Spread** 지정. Spread 생략 시 ibor fallback 설정에서 읽어옴

#### 12. **Discount Ratio Segment** (p.176-177)
- **Type**: `Discount Ratio`
- 세 개의 입력 곡선(기준/분자/분모)으로 할인계수 산출:
  $P(0,t) = P_b(0,t) \cdot P_n(0,t) / P_d(0,t)$
- 주요 활용: **"CCY1-IN-CCY2" 할인 곡선** 구축 (통화 CCY1로 표시되고 CCY2로 담보화된 현금흐름 할인)
- **BaseCurve** = `CCY2-IN-CCY2`, **NumeratorCurve** = `CCY1-IN-BASE`, **DenominatorCurve** = `CCY2-IN-BASE`로 설정 (p.176-177)

### 5.7.2 Default Curves from CDS (p.177)

디폴트 곡선은 CDS 시장 상품(par spread 또는 upfront price)과 회수율(recovery rate) 인용문으로부터 부트스트랩됩니다. 주요 요소:
- **Type**: `SpreadCDS` (MidPointCdsEngine 사용), `Price` 또는 `ConvSpreadCDS` (IsdaCdsEngine 사용)
- **DiscountCurve**: 부트스트랩 시 현금흐름 할인에 사용할 수익률 곡선 참조 (`Yield/Currency/curve_name` 형식)
