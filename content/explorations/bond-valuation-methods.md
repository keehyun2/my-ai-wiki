---
query: "Bond 상품 평가 하는방식에 대한 설명해주세요."
---

이 답변은 ORE Product Catalogue의 Bond Derivatives 및 Cash Products 섹션과 Yield Curves 설정 방법론을 검토하여 작성되었습니다.

---

# Bond 상품 평가 방식 (ORE)

ORE에서 Bond 상품을 평가하는 방식은 기본적으로 **할인 현금흐름(Discounted Cash Flow, DCF)** 분석에 기반하며, 곡선 구축(Curve Building)과 각 상품 유형에 따른 적절한 모델을 사용합니다.

## 기본 평가 원리: 할인 현금흐름 (DCF)

### 수익률 곡선 기반 가격결정
채권의 기본 가격은 미래 현금흐름(쿠폰 지급 + 원금 상환)을 할인율로 할인하여 계산합니다:

```
가격 = Σ(현금흐름 / 할인계수)
```

이때 필요한 **할인계수(Discount Factors)**는 [[explorations/sources-userguide-json-162-177-yeild-curve]]에 설명된 `curveconfig.xml`을 통해 구축된 수익률 곡선에서 도출됩니다.

## 수익률 곡선 구축 방법

### 1. Yield Curves 기본 구조 (p.162-163)

`curveconfig.xml`에서 수익률 곡선은 다음 요소들로 구성됩니다:

| 요소 | 설명 |
|------|------|
| **CurveId** | 곡선의 고유 식별자 |
| **Currency** | 곡선의 통화 |
| **DiscountCurve** | 할인에 사용할 곡선 참조 |
| **Segments** | 곡선을 구성하는 세그먼트 |
| **InterpolationVariable** | 보간 변수: `Discount`, `Zero`, `Forward` |
| **InterpolationMethod** | 보간 방법: `LogLinear` 등 |

### 2. Bond 특화 곡선 세그먼트

#### FittedBond Segment (p.170-172)
- **유동성 채권 가격에 피팅**하여 곡선 구축
- `IborIndexCurves`: 채권에 필요한 Ibor 지수와 전망곡선 매핑
- `ExtrapolateFlat`: 첫 번째/마지막 채권 만기 이전/이후 평탄 외삽
- 보간 방법: `NelsonSiegel`, `Svensson`, `ExponentialSplines`

#### Bond Yield Shifted Segment (p.172-173)
- **채권 수익률을 기준으로 조정된 곡선**
- `ReferenceCurve`: 스프레드 계산용 기준 곡선
- 채권의 듀레이션 시점에서 YTM과 기준곡선 간 스프레드 평균으로 조정
- 유동 채권이 적은 경우 유용 (하나의 유동 채권만으로도 구축 가능)

#### Yield Plus Default Segment (p.173-174)
- **기준 곡선 + 디폴트 곡선**으로 all-in 할인곡선 구축
- `ReferenceCurve`, `DefaultCurves`, `Weights` 필요
- 순간선도(instantaneous forward rate) 수준에서 합산
- 결과 할인계수: $P(0,t) = \prod_i S_i(t)^{(1-R_i)w_i}$

## Bond 상품 유형별 평가 방법

### 1. 기본 Bond 및 Bond Position (p.284, p.608-624)
- **표준 채권 평가**: 수익률 곡선과 신용 스프레드를 사용한 할인 현금흐름 분석
- 각종 쿠폰 타입(고정/변동/영구채권 등) 지원
- [[summaries/products]]의 Bond Products 섹션 참조

### 2. Forward Bond (p.284)
- **선물 채권 평가**: 선물 가격결정 방법론 사용
- 미래 시점의 인도일과 가격을 고려한 평가

### 3. Bond Option (p.284)
- **Black 모델 또는 Hull-White 모델** 사용
- 옵션 유형과 기초 자산 특성에 따라 모델 선택
- 콜러블/풀터블 채권의 옵션 가치 평가

### 4. Bond Total Return Swap (TRS) (p.284)
- **채권 가격 + 자금 조달 비용** 기반 평가
- 채권의 실적 대비 부동금리 지급 구조

### 5. Convertible Bond (p.284, p.608-624)
- **주식과 신용 특성 결합** 복잡한 모델
- 유한차분법(Finite Difference) 또는 Monte Carlo 방법 사용
- 전환권 가치 평가

### 6. Callable Bond (p.284, p.608-624)
- **Option-Adjusted Spread (OAS) 모델** 사용
- 이자율 트리(Interest Rate Tree) 기반 평가
- 발행자의 조기 상환 권리 가치 반영

## 상품별 특징 및 평가 고려사항

| 상품 유형 | 주요 평가 요소 | 참조 |
|-----------|---------------|------|
| **Bond** | 수익률 곡선, 신용 스프레드, 쿠폰 스케줄 | [[summaries/products]] p.100-156 |
| **Bond Forward** | 선물 가격, 인도일, 할인 곡선 | [[summaries/products]] p.284 |
| **Bond Option** | 변동성, 이자율 모델 (Black/Hull-White) | [[summaries/products]] p.284 |
| **Convertible Bond** | 주식 가격, 전환비율, 신용 리스크 | [[summaries/products]] p.284 |
| **Callable Bond** | 조기 상환 권리, OAS, 이자율 트리 | [[summaries/products]] p.284 |
| **Bond TRS** | 채권 실적, 자금 비용 | [[summaries/products]] p.284 |
| **Bond Repo** | 담보, Haircut, Repo 금리 | [[summaries/products]] p.284 |

## 곡선 구축의 핵심: 부트스트랩 방법론

### 부트스트랩 프로세스
1. 시장 상품(예금, FRA, 선물, 스왑)의 가격에서 제로금리 추정
2. 다양한 만기의 시장 인용문을 사용하여 곡선 형성
3. 보간법(Interpolation)으로 곡선 연결
4. 외삽법(Extrapolation)으로 곡선 연장

### 보간 변수 선택
- **Discount** (기본값): 할인계수를 직접 보간
- **Zero**: 제로금리를 보간
- **Forward**: 선물 금리를 보간

### 보간 방법
- **LogLinear** (기본값): 할인계수의 로그를 선형 보간
- **Linear**: 선형 보간
- **Cubic**: 3차 보간

## 실무적 고려사항

1. **신용 리스크 반영**: 디폴트 곡선과 회수율을 통해 신용 스프레드 반영
2. **유동성 조정**: 유동 채권 가격 피팅을 통해 시장 유동성 반영
3. **커브 스무딩**: Nelson-Siegel, Svensson 등의 매개변수화된 곡선 사용
4. **일정 계산**: 각 통화/상품별 관련 컨벤션 적용

## 참고 문서

- [[summaries/products]] — Bond Products 섹션 (p.100-156) 및 Bond Derivatives pricing (p.598-605)
- [[summaries/products]] — Cash Products pricing (p.608-624)
- [[explorations/sources-userguide-json-162-177-yeild-curve]] — 수익률 곡선 설정 상세
- [[summaries/userguide]] — ORE 전체 사용법 및 설정 참조
