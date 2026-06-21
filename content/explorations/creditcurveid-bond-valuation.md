---
query: "CreditCurveId 에 대해서 설명해주세요. 고정금리 bond 를 평가할때 CreditCurveId 를 공란으로 평가했는데 이건 무위험 으로 평가하는 의미 같은데 신용도를 같이 포함해서 평가하는 방법은?"
---

이 답변은 ORE의 Bond 평가 방법론, 곡선 구축 가이드, CreditCurve 설정을 검토하여 작성되었습니다.

---

# CreditCurveId와 Bond 신용 리스크 평가

## CreditCurveId란 무엇인가?

**CreditCurveId**는 ORE에서 채권 상품의 신용 리스크를 평가하기 위해 사용하는 **신용 곡선(Credit/Default Curve)의 식별자**입니다.

### 기본 개념

| 개념 | 설명 |
|-----|------|
| **CreditCurveId** | 신용 곡선의 고유 ID (curveconfig.xml에 정의) |
| **신용 곡선** | 발행체의 디폴트 확률(위험률)과 회수율의 기간구조 |
| **신용 스프레드** | 신용 리스크로 인한 추가 수익률 요구 |

## CreditCurveId 공란 = 무위험 평가

**네, 맞습니다.** `CreditCurveId`를 공란으로 두면 **무위험 할인 곡선**으로만 평가하며, 신용 리스크가 반영되지 않습니다.

### 평가 비교

| CreditCurveId | 평가 방식 | 결과 |
|--------------|----------|------|
| **공란 (비워둠)** | 무위험 할인 곡선만 사용 | 신용 리스크 미반영 가격 |
| **지정됨** | 무위험 곡선 + 신용 곡선 | 신용 리스크 포함 가격 |

## 신용도 포함 평가 방법

고정금리 채권에 신용 리스크를 포함하여 평가하는 방법은 크게 두 가지가 있습니다:

### 방법 1: Bond Product의 CreditCurveId 지정

Bond XML 정의에서 `CreditCurveId`를 직접 지정합니다:

```xml
<Trade id="BOND_001">
  <TradeType>Bond</TradeType>
  <Envelope>
    <Counterparty>CPTY_A</Counterparty>
    <NettingSetId>NS_1</NettingSetId>
  </Envelope>
  <BondData>
    <IssuerId>ISSUER_CORP_A</IssuerId>
    <CreditCurveId>Corp_A_Curve</CreditCurveId>  <!-- 신용 곡선 지정 -->
    <Settlement>Physical</Settlement>
    <Currency>USD</Currency>
    <Notional>1000000</Notional>
    <MaturityDate>2030-12-31</MaturityDate>
    <Coupons>
      <Coupon>
        <Rate>0.05</Rate>
        <Tenor>1Y</Tenor>
      </Coupon>
    </Coupons>
  </BondData>
</Trade>
```

### 방법 2: Yield Plus Default 곡선 세그먼트 사용

[[concepts/curve-building]]에 설명된 **Yield Plus Default** 세그먼트를 사용하여 신용 리스크를 곡선 자체에 포함시킵니다.

#### curveconfig.xml 설정

```xml
<CurveConfiguration>
  <Curve id="USD-CORP-DISC" currency="USD" type="Discount">
    <Segments>
      <!-- 기준 곡선 + 디폴트 곡선 -->
      <Segment type="YieldPlusDefault">
        <ReferenceCurve>USD-RFR-DISC</ReferenceCurve>  <!-- 무위험 기준 곡선 -->
        <DefaultCurves>
          <DefaultCurve>
            <CurveId>Corp_A_Default</CurveId>         <!-- 디폴트 곡선 -->
            <Weight>1.0</Weight>
            <RecoveryRate>0.40</RecoveryRate>          <!-- 회수율 40% -->
          </DefaultCurve>
        </DefaultCurves>
      </Segment>
    </Segments>
  </Curve>
</CurveConfiguration>
```

#### 수식

할인계수는 다음과 같이 계산됩니다:

$$P(0,t) = \prod_i S_i(t)^{(1-R_i)w_i}$$

여기서:
- $S_i(t)$: 디폴트 곡선 $i$의 생존 확률
- $R_i$: 회수율 (Recovery Rate)
- $w_i$: 가중치

### 방법 3: Bond Yield Shifted 곡선 사용

유동 채권의 YTM(Yield to Maturity)에 스프레드를 반영하여 곡선을 구축합니다:

```xml
<Segment type="BondYieldShifted">
  <ReferenceCurve>USD-RFR-DISC</ReferenceCurve>
  <Bonds>
    <Bond>
      <Name>US_CORP_A_2030</Name>
      <Price>98.5</Price>           <!-- 시장 가격 -->
      <YTM>0.0525</YTM>             <!-- YTM (신용 스프레드 포함) -->
    </Bond>
  </Bonds>
</Segment>
```

## 신용 곡선 구축 (Default Curves)

신용 곡선은 [[concepts/curve-building]]에 따라 CDS 시장 데이터로부터 부트스트랩됩니다:

### 신용 곡선 설정

| 파라미터 | 설명 | 일반적 값 |
|---------|------|----------|
| **Type** | `SpreadCDS`, `Price`, `ConvSpreadCDS` | `SpreadCDS` |
| **DiscountCurve** | 할인용 수익률 곡선 | 통화별 무위험 곡선 |
| **RecoveryRate** | 회수율 | 40% (일반적) |

```xml
<Curve id="Corp_A_Default" currency="USD" type="Credit">
  <Segments>
    <Segment type="SpreadCDS">
      <DiscountCurve>USD-RFR-DISC</DiscountCurve>
      <RecoveryRate>0.40</RecoveryRate>
      <Quotes>
        <Quote>
          <Tenor>1Y</Tenor>
          <ParSpread>0.0050</ParSpread>  <!-- 50bp CDS spread -->
        </Quote>
        <Quote>
          <Tenor>5Y</Tenor>
          <ParSpread>0.0080</ParSpread>  <!-- 80bp -->
        </Quote>
        <Quote>
          <Tenor>10Y</Tenor>
          <ParSpread>0.0120</ParSpread> <!-- 120bp -->
        </Quote>
      </Quotes>
    </Segment>
  </Segments>
</Curve>
```

## 방법별 비교

| 방법 | 장점 | 단점 | 사용 시기 |
|-----|------|------|----------|
| **CreditCurveId 직접 지정** | 채권별로 신용 리스크 개별 적용 가능 | 각 채권마다 ID 지정 필요 | 특정 발행체 채권 |
| **Yield Plus Default** | 할인 곡선 자체에 신용 리스크 포함 | 곡선 구성이 복잡 | 발행체군 전체 |
| **Bond Yield Shifted** | 시장 가격 기반 반영 | 유동 채권 필요 | 시장 데이터 충분 시 |

## 실무적 고려사항

### 1. 데이터 요구사항
- **CDS 데이터**: CDS par spreads (각 만기별)
- **회수율**: 일반적으로 40%, 시장 상황에 따라 조정
- **발행체 정보**: 신용 등급, 산업 분류

### 2. 설정 파일 요약

```
파일 구조:
├── portfolio.xml          (Trade의 CreditCurveId 지정)
├── curveconfig.xml        (신용 곡선 정의)
└── todaysmarket.xml       (시장 데이터 포인트)
```

### 3. 검증 방법
신용 리스크가 제대로 반영되었는지 확인하려면:

1. **무위험 가격 vs 신용 포함 가격 비교**
2. **스프레드 민감도 분석**: `sensitivity.xml`에서 CreditCurve sensitivity 확인
3. **시장 가격 재현성**: 구축된 곡선으로 시장 채권 가격 재현

## 요약

| 질문 | 답변 |
|-----|------|
| CreditCurveId 공란 = 무위험? | **네**, 신용 리스크 미반영 |
| 신용도 포함 방법 | ① CreditCurveId 지정, ② Yield Plus Default 곡선, ③ Bond Yield Shifted |
| 추천 방법 | 데이터 상황에 따라 다름: CDS 데이터 있으면 ①, 유동 채권 있으면 ③ |

## 관련 문서

- [[concepts/curve-building]] — 곡선 구축 방법론 (Yield Plus Default 섹션)
- [[explorations/bond-valuation-methods]] — Bond 상품 평가 방식
- [[summaries/products]] — Bond Products 섹션 (CreditCurveId 설명)
