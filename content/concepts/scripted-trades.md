---
sources: [summaries/products.md]
brief: ORE의 스크립트 프레임워크를 사용한 사용자 정의 페이오프 상품 정의
---

# 스크립트 거래 (Scripted Trades)

ORE의 스크립트 거래 프레임워크는 표준 상품 유형을 넘어선 **사용자 정의 페이오프**를 구현할 수 있는 유연한 방법을 제공합니다. 스크립트 언어를 사용하여 복잡하고 맞춤화된 파생상품을 정의할 수 있습니다.

## 개요

스크립트 거래는 다음과 같은 경우에 유용합니다:
- 표준 상품 유형으로 표현할 수 없는 복잡한 페이오프
- 맞춤화된 구조화 상품 (Structured Products)
- 여러 자산 클래스를 결합한 하이브리드 상품
- 패스 의존형(Path-Dependent) 상품

## 일반 구조 (p.492-492)

스크립트 거래는 `ScriptedTradeData`를 상품 유형으로 사용합니다:

| 요소 | 설명 |
|------|------|
| **ScriptedPayoffData** | 페이오프 스크립트 (TradeType, ProductTag, Script) |
| **NumberData** | 숫자 변수 |
| **IndexData** | 인덱스 변수 |
| **CurrencyData** | 통화 변수 |
| **DayCounterData** | 일수계산 변수 |
| **EventData** | 이벤트 변수 |

### ScriptedPayoffData

```xml
<ScriptedTradeData>
  <ScriptedPayoffData>
    <TradeType>ScriptedTrade</TradeType>
    <ProductTag>MyCustomProduct</ProductTag>
    <Script>...</Script>
  </ScriptedPayoffData>
  <NumberData>...</NumberData>
  <IndexData>...</IndexData>
  <CurrencyData>...</CurrencyData>
  <DayCounterData>...</DayCounterData>
  <EventData>...</EventData>
</ScriptedTradeData>
```

## 데이터 타입 (p.493-500)

### Event

이벤트 타입과 관련 파라미터를 정의합니다.

| 요소 | 설명 |
|------|------|
| **Type** | 이벤트 유형 (Fixing/BarrierDetection/AverageObservation 등) |
| **Dates** | 날짜 또는 날짜 범위 |
| **Level** | 바리어/평균용 레벨 |
| **Barrier** | 바리어 유형 |
| **Observation** | 관측 유형 |
| **Condition** | 이벤트 조건 |

### Number

숫자 변수를 정의합니다.

| 요소 | 설명 |
|------|------|
| **Name** | 변수명 |
| **Value** | 숫자 값 |
| **OptionalValue** | 선택적 값 |

### Index

인덱스 변수를 정의합니다.

| 요소 | 설명 |
|------|------|
| **Name** | 변수명 |
| **Type** | 인덱스 타입 (FX/IR/Equity/Inflation/Commodity/Credit) |
| **IndexName** | 특정 인덱스명 |

### Currency

통화 변수를 정의합니다.

| 요소 | 설명 |
|------|------|
| **Name** | 변수명 |
| **CurrencyCode** | ISO 통화 코드 (예: USD, EUR) |

### Daycounter

일수계산 변수를 정의합니다.

| 요소 | 설명 |
|------|------|
| **Name** | 변수명 |
| **Daycounter** | 일수계산 기준 (A360/A365/ACT 등) |

## 컴팩트 XML 형식 (p.498-500)

스크립트 내에서 변수를 직접 정의하여 XML을 간소화할 수 있습니다:

| 형식 | 설명 |
|------|------|
| `#N(var_name)` | 이름만 정의 |
| `#N(var_name,value)` | 이름과 값 함께 정의 |
| `#I(index_type,index_name)` | 인덱스 정의 |
| `#C(currency_code)` | 통화 정의 |

```xml
<!-- 표준 형식 -->
<NumberData>
  <Number name="strike">
    <Value>100</Value>
  </Number>
</NumberData>

<!-- 컴팩트 형식 -->
<Script>#N(strike,100) * max(#I(Equity,Apple) - #C(USD), 0)</Script>
```

## 페이오프 스크립트 언어 (p.501-512)

### 연산자

| 연산자 | 설명 |
|--------|------|
| `+`, `-`, `*`, `/`, `^` | 산술 연산 |
| `==`, `!=`, `<`, `>`, `<=`, `>=` | 비교 연산 |
| `and`, `or`, `!`, `?` | 논리 연산 |
| `let` | 할당 |

### 함수

**수학 함수**:
- `abs`, `exp`, `log`, `pow`, `sqrt`, `normal`
- `max`, `min`, `sign`, `floor`, `ceil`, `round`

**날짜/시간 함수**:
- `time`, `day`, `month`, `year`, `weekday`
- `daysbetween`, `isbusinessday`, `advance`

**금융 함수**:
- `npv` - 순현재가치
- `cashflows` - 현금흐름
- `performance` - 수익률
- `payoff` - 페이오프
- `discount` - 할인
- `forward` - 선물 가격
- `fwdBondYield` - 채권 선물 수익률

**변동성 함수**:
- `atmVolatility`, `capVolatility`, `swaptionVolatility`
- `fxVolatility`, `equityVolatility`, `commodityVolatility`
- `histvolatility`, `histpercentile`

**옵션 가격 함수**:
- `capFloorPrice`, `swaptionPrice`
- `fxOptionPrice`

**기타**:
- `fixings` - Fixing 데이터
- `histfixing`, `histvalue` - 과거 데이터
- `prob` - 디폴트 확률
- `calibrate` - 보정
- `di`, `du`, `da`, `dp`, `dc` - Greek 계산

## 예시

### 간단한 콜 옵션

```xml
<ScriptedTradeData>
  <ScriptedPayoffData>
    <Script>#N(notional,1000000) * max(#I(Equity,SPX) - #N(strike,4000), 0)</Script>
  </ScriptedPayoffData>
</ScriptedTradeData>
```

### 바리어 옵션

```xml
<ScriptedTradeData>
  <ScriptedPayoffData>
    <Script>
      if(#I(Equity,SPX) > #N(barrier,4500),
         #N(payoff,100),
         0)
    </Script>
  </ScriptedPayoffData>
  <EventData>
    <Event name="barrierCheck">
      <Type>BarrierDetection</Type>
      <Dates>
        <StartDate>2024-01-01</StartDate>
        <EndDate>2024-12-31</EndDate>
      </Dates>
      <Level>#N(barrier,4500)</Level>
      <Barrier>DownIn</Barrier>
    </Event>
  </EventData>
</ScriptedTradeData>
```

### 아시안 옵션

```xml
<ScriptedTradeData>
  <ScriptedPayoffData>
    <Script>
      #N(notional,1000000) * max(average(#I(Equity,SPX)) - #N(strike,4000), 0)
    </Script>
  </ScriptedPayoffData>
  <EventData>
    <Event name="averageObservation">
      <Type>AverageObservation</Type>
      <Dates>
        <StartDate>2024-01-01</StartDate>
      <EndDate>2024-12-31</EndDate>
      </Dates>
      <Frequency>Daily</Frequency>
    </Event>
  </EventData>
</ScriptedTradeData>
```

## 가격결정 방법

스크립트 거래는 다음 가격결정 방법을 지원합니다:
- **Monte Carlo**: 복잡한 패스 의존형 상품
- **Finite Difference**: PDE 기반 방법
- **Analytical**: 단순 페이오프의 경우 해석적 해

## 결제 통화

스크립트 거래에서는 결제 통화를 명시해야 합니다 (p.500-500):

1. **FX 인덱스로 통화 지정**: FX 인덱스를 통해 통화 변환
2. **통화 변수 사용**: `#C(currency_code)` 형식
3. **수식 내 직접 지정**: 통화 변환 함수 사용

## 스크립트 거래 지원 상품

ORE는 스크립트 기반 상품으로 다음을 지원합니다 (p.358-363):

| 상품 | 설명 |
|------|------|
| **Generic Scripted Products** | 완전히 맞춤화된 페이오프 |
| **Flexi Swap** | 유동적 명목금액 스왑 |
| **Balance Guaranteed Swap** | 잔액 보증 스왑 |

## 관련 개념

- [[summaries/products]] — 전체 상품 카탈로그 및 스크립트 상품 섹션
- [[concepts/pricing-models]] — 가격결정 모델 및 수치 방법
- [[concepts/trade-components]] — 기본 거래 컴포넌트

## 모범 사례

1. **단순성**: 복잡한 로직은 여러 변수로 분해
2. **테스트**: 간단한 경우로 검증 후 확장
3. **문서화**: 복잡한 스크립트는 주석 추가
4. **성능**: 불필요한 계산 최소화
5. **검증**: 시나리오 분석으로 결과 검증
