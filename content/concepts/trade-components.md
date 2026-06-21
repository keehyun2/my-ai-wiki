---
sources: [summaries/products.md]
brief: ORE에서 상품 정의에 사용하는 재사용 가능한 XML 컴포넌트 요소들
---

# 거래 컴포넌트 (Trade Components)

ORE의 거래 컴포넌트는 여러 상품 유형에서 재사용 가능한 **XML 하위 노드**들입니다. 이 컴포넌트들을 조합하여 복잡한 파생상품을 효율적으로 정의할 수 있습니다.

## 개요

ORE는 100개 이상의 상품 유형을 지원하며, 각 상품은 기본 컴포넌트들의 조합으로 구성됩니다. 이를 통해:
- **일관성**: 동일한 컴포넌트를 여러 상품에서 재사용
- **효율성**: 중복 코드 최소화
- **유연성**: 컴포넌트 조합으로 다양한 상품 정의

## 컴포넌트 분류

### 1. 옵션 관련

#### OptionData (p.365-372)

SwaptionData 및 FXOptionData 컨테이너 내에서 사용되는 옵션 파라미터입니다.

| 요소 | 설명 |
|------|------|
| **LongShort** | 포지션 방향 (Long/Short) |
| **OptionType** | 콜/풋 (Call/Put) |
| **Style** | 행사 스타일 (European/Bermudan/American) |
| **Settlement** | 결제 방식 (Cash/Physical) |
| **SettlementMethod** | 현금 결제 방법 |
| **NoticePeriod** | 베르무단 옵션의 사전 통지 기간 |
| **ExerciseDates** | 행사 가능일 |
| **Premiums** | 옵션 프리미엄 |
| **AutomaticExercise** | 자동 행사 여부 |
| **PayOffAtExpiry** | 만기 시 지급 여부 |

#### Premiums (p.372-373)

옵션 프리미엄 지급을 정의합니다.

| 요소 | 설명 |
|------|------|
| **Amount** | 프리미엄 금액 |
| **Currency** | 통화 |
| **PayDate** | 지급일 |
| **Type** | 프리미엄/환불 가능 프리미엄 |

### 2. 레그(Leg) 관련

#### LegData (p.374-379)

모든 다중 레그 상품의 기본 구조입니다.

| 요소 | 설명 |
|------|------|
| **LegType** | 레그 유형 (Fixed/Floating/CMS/CPI/Equity 등) |
| **Payer** | 지급자 여부 (true/false) |
| **Currency** | 레그 통화 |
| **Notionals** | 명목금액 (단일 또는 스케줄) |
| **DayCounter** | 일수 계산 기준 |
| **PaymentConvention** | 지급일 컨벤션 |
| **PaymentCalendar** | 지급일 캘린더 |
| **PaymentLag** | 지급 지연 일수 |
| **NotionalAmortization** | 명목금액 상환 스케줄 |

#### ScheduleData (p.379-384)

지급 스트림의 일정 생성을 위한 유연한 설정입니다.

**모드**:
- **Rules**: 규칙 기반 일정 생성
- **Dates**: 명시적 일정 목록
- **Derived**: 다른 스케줄에서 파생

**Rules 모드 파라미터**:
- **StartDate**: 시작일
- **EndDate**: 종료일
- **Tenor**: 기간 (예: 3M, 6M)
- **Calendar**: 캘린더
- **Convention**: 영업일 컨벤션 (F/M/MP/P/UN 등)
- **Rule**: Forward/Backward/Zero/Termination
- **EndOfMonth**: 월말 여부

#### FixedLegData (p.384-385)

고정금리 레그를 정의합니다.

| 요소 | 설명 |
|------|------|
| **Rates** | 고정금리 (단일 또는 스케줄) |

#### FloatingLegData (p.385-392)

변동금리 레그를 정의합니다.

| 요소 | 설명 |
|------|------|
| **Index** | Ibor/OIS/BMA/SIFMA 지수명 |
| **FixingDays** | Fixing 계산 일수 |
| **FixingCalendar** | Fixing 일자 캘린더 |
| **Spread** | 스프레드 (단일 또는 스케줄) |
| **Gearings** | 기어링 (레버리지) |
| **Caps** | 상한금리 |
| **Floors** | 하한금리 |

### 3. 인덱스/변환 관련

#### Indexings (p.394-398)

현금흐름에 FX 변환 및 인덱스 Fixing을 적용합니다.

| 요소 | 설명 |
|------|------|
| **Index** | 변환용 인덱스명 |
| **FixingDays** | Fixing 일수 |
| **FixingCalendar** | Fixing 캘린더 |
| **IsInArrears** | Arrears Fixing 여부 |

### 4. 특수 레그 유형

#### CMSLegData (p.399-401)

Constant Maturity Swap 레그를 정의합니다.

| 요소 | 설명 |
|------|------|
| **Index** | CMS 인덱스 (예: CMS-10Y, CMS-30Y) |
| **FixingDays** | Fixing 일수 |
| **FixingCalendar** | Fixing 캘린더 |

#### CPILegData (p.413-417)

인플레이션 연계 레그를 정의합니다.

| 요소 | 설명 |
|------|------|
| **Index** | CPI 인덱스 (예: EUHICPXT, UKRPI) |
| **Interpolated** | 보간 여부 |
| **Lag** | 관측 지연 (개월) |
| **Frequency** | 빈도 (Zero Coupon용) |

#### EquityLegData (p.409-413)

주식 연계 레그를 정의합니다.

| 요소 | 설명 |
|------|------|
| **EquityName** | 주식 기초자산명 |
| **InitialPrice** | 수익률 계산용 초기가 |
| **EquityCreditCurve** | 주식 기초자산 신용곡선 |

### 5. 옵션/바리어 관련

#### StrikeData (p.437-439)

옵션 행사가를 정의합니다.

| 요소 | 설명 |
|------|------|
| **Strike** | 행사가 (단일 또는 스케줄) |
| **StrikeType** | 행사가 유형 (Absolute/Relative/Moneyness/Delta/Variance) |
| **StrikeCurrency** | 행사가 통화 (다를 경우) |

#### BarrierData (p.439-441)

바리어 옵션의 바리어 레벨과 유형을 정의합니다.

| 요소 | 설명 |
|------|------|
| **Level** | 바리어 레벨 (단일 또는 스케줄) |
| **Type** | 바리어 유형 (Down/Up/DownUp/DoubleBarrier 등) |
| **Style** | 바리어 스타일 (American/European/Discrete) |
| **Rebate** | 리베이트 금액 |

### 6. 상품 특화 컴포넌트

#### BasketData (p.431-437)

다중 기초자산 바스킷을 정의합니다.

| 요소 | 설명 |
|------|------|
| **Underlying** | 기초자산 목록 |
| **BasketConstituentData** | 구성요소 상세 데이터 |

#### Underlying (p.433-437)

단일 기초자산을 정의합니다.

| 요소 | 설명 |
|------|------|
| **Type** | 자산 유형 (Equity/FX/Commodity 등) |
| **Name** | 기초자산명 |
| **IdentifierType** | 식별자 유형 (RIC/ISIN/WPI 등) |
| **Weight** | 바스킷 내 가중치 |
| **PriceType** | 가격 유형 (Spot/Forward/Future 등) |

## 컴포넌트 사용 예시

### Swap 레그 정의

```xml
<LegData>
  <LegType>Floating</LegType>
  <Payer>false</Payer>
  <Currency>USD</Currency>
  <Notionals>
    <Notional>10000000</Notional>
  </Notionals>
  <DayCounter>A360</DayCounter>
  <FloatingLegData>
    <Index>USD-LIBOR-3M</Index>
    <Spread>0.0010</Spread>
  </FloatingLegData>
  <ScheduleData>
    <Rules>
      <StartDate>2024-01-01</StartDate>
      <EndDate>2034-01-01</EndDate>
      <Tenor>3M</Tenor>
      <Calendar>USD</Calendar>
      <Convention>MF</Convention>
      <Rule>Forward</Rule>
    </Rules>
  </ScheduleData>
</LegData>
```

## 컴포넌트 조합 방법

ORE에서는 이러한 컴포넌트들을 조합하여 복잡한 상품을 정의합니다:

1. **기본 구조**: Envelope + TradeType + TradeSpecificData
2. **다중 레그 상품**: LegData (Fixed/Floating/CMS/Etc.)
3. **옵션 상품**: OptionData + StrikeData + (BarrierData)
4. **바스킷 상품**: BasketData + Underlying 목록
5. **스크립트 상품**: ScriptedTradeData (사용자 정의)

## 관련 개념

- [[summaries/products]] — 전체 상품 카탈로그 및 컴포넌트 상세
- [[concepts/scripted-trades]] — 사용자 정의 페이오프 스크립트
- [[summaries/userguide]] — ORE XML 설정 가이드

## 컴포넌트 재사용 팁

1. **모듈화**: 자주 사용하는 컴포넌트를 템플릿으로 저장
2. **일관성**: 동일 컴포넌트는 동일 파라미터 사용
3. **검증**: 컴포넌트 단위별로 설정 검증
4. **문서화**: 커스텀 컴포넌트는 문서화
