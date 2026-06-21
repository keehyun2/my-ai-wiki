---
sources: [summaries/products.md]
brief: ORE에서 수익률 곡선, 디폴트 곡선, FX/인플레이션/주식 곡선 등 다양한 기간구조를 구축하는 방법
---

# 곡선 구축 (Curve Building)

ORE는 포트폴리오 가격결정에 필요한 다양한 **기간구조(Term Structure)**를 `curveconfig.xml`을 통해 구축합니다. 이 문서는 곡선 구축의 개념과 ORE에서의 구현 방법을 설명합니다.

## 곡선 유형

ORE는 다음과 같은 곡선 유형을 지원합니다:

| 곡선 유형 | 설명 | 주요 용도 |
|-----------|------|-----------|
| **수익률 곡선 (Yield Curves)** | 할인율과 제로금리의 기간구조 | 채권, 스왑 등 금리 파생상품 평가 |
| **FX 곡선 (FX Curves)** | 현물 및 선물 환율의 기간구조 | FX 파생상품 평가 |
| **인플레이션 곡선 (Inflation Curves)** | CPI 및 YY 인플레이션 지수의 기간구조 | 인플레이션 파생상품 평가 |
| **주식 곡선 (Equity Curves)** | 주가 및 배당수익률의 기간구조 | 주식 파생상품 평가 |
| **디폴트 곡선 (Default Curves)** | 위험률(Hazard Rate) 및 회수율의 기간구조 | CDS 및 신용 파생상품 평가 |
| **상품 곡선 (Commodity Curves)** | 선물 가격의 기간구조 | 상품 파생상품 평가 |
| **변동성 구조 (Volatility Structures)** | 각 자산 클래스별 변동성 표면 | 옵션 평가 |

## 수익률 곡선 구축 (p.631-634)

### 부트스트랩 방법론

수익률 곡선은 시장 상품의 가격으로부터 제로금리를 부트스트랩하여 구축합니다:

1. **입력 상품**: 예금(Deposit), FRA, 선물(Future), 스왑(Swap), OIS
2. **제로금리 추정**: 각 만기의 시장 가격에서 제로금리 역산
3. **보간**: 연속적인 곡선 형성 (LogLinear, Linear, Cubic 등)
4. **외삽**: 곡선의 범위 밖 추정 (ContinuousForward, DiscreteForward)

### 곡선 세그먼트 유형

[[explorations/sources-userguide-json-162-177-yeild-curve]]에서 상세히 설명하지만, 주요 세그먼트는 다음과 같습니다:

| 세그먼트 | 설명 | 주요 파라미터 |
|---------|------|--------------|
| **Direct** | 제로금리/할인계수 직접 명시 | Quotes, Conventions |
| **Simple** | 예금, FRA, 선물, 스왑 등 기본 상품 | ProjectionCurve, PillarChoice |
| **Average OIS** | OIS 스왑 평균 | CompositeQuote (Rate + Spread) |
| **Tenor Basis** | 텐서 베이시스 스왑 | ProjectionCurveReceive/Pay |
| **Cross Currency** | FX 선물, 크로스커런시 베이시스 | DiscountCurve, SpotRate |
| **Zero Spread** | 기준 곡선 대비 스프레드 | ReferenceCurve |
| **FittedBond** | 채권 가격 피팅 | IborIndexCurves, InterpolationMethod |
| **Bond Yield Shifted** | 채권 YTM 기준 조정 | ReferenceCurve |
| **Yield Plus Default** | 기준 곡선 + 디폴트 곡선 | ReferenceCurve, DefaultCurves, Weights |
| **Weighted Average** | 두 곡선의 가중합 | 가중치 파라미터 |

### 보간 및 외삽

- **InterpolationVariable**: `Discount`(기본값), `Zero`, `Forward`
- **InterpolationMethod**: `LogLinear`(기본값), `Linear`, `Cubic`, `LogCubic`
- **Extrapolation**: `True`(기본값)로 활성화
- **ExtrapolationMethod**: `ContinuousForward`, `DiscreteForward`

## 디폴트 곡선 구축 (p.636)

디폴트 곡선은 CDS 시장 상품(par spread 또는 upfront price)과 회수율(recovery rate)으로부터 부트스트랩됩니다:

- **Type**: `SpreadCDS` (MidPointCdsEngine), `Price` 또는 `ConvSpreadCDS` (IsdaCdsEngine)
- **DiscountCurve**: 현금흐름 할인용 수익률 곡선
- **RecoveryRate**: 회수율 (일반적으로 40%)

## FX 곡선 구축 (p.634)

FX 곡선은 커버드 이자율 평가(Covered Interest Rate Parity) 이론에 기반하여 구축됩니다:

- **FX 현물 곡선**: 현물 환율 제공
- **FX 선물 곡선**: FX 스왑 및 포워드 포인트로부터 구축
- **크로스커런시 베이시스 스왑**: 두 통화 간 베이시스 반영

## 인플레이션 곡선 구축 (p.635)

인플레이션 곡선은 인플레이션 스왑 및 인플레이션 연계 채권으로부터 구축합니다:

- **CPI 곡선**: Zero Coupon Inflation용
- **YY 곡선**: Year-on-Year Inflation용
- **계절성 조정**: 인플레이션 지수의 계절적 패턴 반영

## 주식 곡선 구축 (p.635)

주식 곡선은 주가 및 배당 수익률 정보로부터 구축합니다:

- **주식 현물 곡선**: 현재 주가 및 선물 가격
- **배당수익률 곡선**: 옵션 가격, 배당 선물, 배당 스왑으로부터 도출

## 상품 곡선 구축 (p.636)

상품 곡선은 선물 가격 및 스왑 가격으로부터 구축합니다:

- **선물 가격 곡선**: 각 만기별 선물 가격
- **계절성 조정**: 에너지, 농산물 등의 계절적 패턴 반영

## 변동성 구조 (p.636-638)

변동성 표면은 각 자산 클래스별 옵션 가격으로부터 구축합니다:

| 자산 클래스 | 모델 옵션 |
|-------------|-----------|
| **금리** | Black, SABR (Caps/Floors, Swaptions) |
| **FX** | Black, Vanna-Volga, SABR |
| **인플레이션** | Black, SABR |
| **주식** | Black, Local Volatility, Stochastic Volatility |
| **상품** | Black, 기타 모델 |

## 관련 개념

- [[explorations/sources-userguide-json-162-177-yeild-curve]] — 수익률 곡선 설정 상세 가이드
- [[concepts/bond-valuation]] — 채권 평가에서의 곡선 활용
- [[summaries/products]] — 전체 상품 카탈로그
- [[summaries/userguide]] — ORE 설정 및 사용법

## 실무적 고려사항

1. **일관성**: 동일 통화 내의 모든 곡선은 일관된 컨벤션 사용
2. **안정성**: 부트스트랩 수렴 허용오차(Tolerance) 설정
3. **검증**: 구축된 곡선의 시장 가격 재현성 검증
4. **유동성**: 유동성이 좋은 상품 우선 사용
