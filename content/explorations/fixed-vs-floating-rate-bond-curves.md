---
query: "변동금리 국채를 무위험 평가할때 할인커브에 추가로 index forward 커브가 필요하죠? 고정금리 국채를 무위험 평가할때는 할인커브만 있으면 되고"
---

이 답변은 ORE의 곡선 구축 가이드, Bond 평가 방법론, Floating Leg 설정을 검토하여 작성되었습니다.

---

# 고정금리 vs 변동금리 국채 평가: 필요한 곡선

**네, 정확합니다.** 귀하의 이해가 맞습니다.

## 핵심 요약

| 채권 유형 | 무위험 평가에 필요한 곡선 |
|----------|----------------------|
| **고정금리 국채** | 할인 곡선 (Discount Curve) **만 필요** |
| **변동금리 국채** | 할인 곡선 (Discount Curve) **+ 지수 전망 곡선 (Index Forward Curve) 필요** |

## 상세 설명

### 고정금리 국채 (Fixed-Rate Bond)

**필요한 곡선**: 할인 곡선 1개

고정금리 채권의 경우, 모든 미래 쿠폰 지급액이 **알려져 있고 고정**되어 있으므로:

$$P = \sum_{t=1}^{T} \frac{C}{(1+r_t)^t} + \frac{F}{(1+r_T)^T}$$

여기서:
- $C$: 고정 쿠폰 (알려짐)
- $F$: 액면가 (알려짐)
- $r_t$: 할인율 (할인 곡선에서 제공)

**결과**: 할인 곡선만으로 모든 현금흐름을 할인할 수 있습니다.

### 변동금리 국채 (Floating-Rate Bond)

**필요한 곡선**: 할인 곡선 + 지수 전망 곡선 (2개)

변동금리 채권의 경우, 미래 쿠폰 지급액이 **확정되지 않고** 참조 지수(Index)에 따라 변하므로:

$$P = \sum_{t=1}^{T} \frac{C_t(\text{Index}_t)}{(1+r_t)^t} + \frac{F}{(1+r_T)^T}$$

여기서:
- $C_t(\text{Index}_t)$: 쿠폰 = 지수 + 스프레드 (알려져 있지 않음)
- $\text{Index}_t$: 미래 지수 값 (전망 곡선에서 제공 필요)
- $r_t$: 할인율 (할인 곡선에서 제공)

**결과**: 미래 쿠폰을 계산하기 위해 **지수 전망(Projection/Forward) 곡선**이 추가로 필요합니다.

## ORE 설정

### curveconfig.xml에서의 구성

#### 1. 고정금리 채권용 (Discount Curve만)

```xml
<CurveConfiguration>
  <!-- 할인 곡선만 있으면 됨 -->
  <Curve id="KRW-DISC" currency="KRW" type="Discount">
    <Segments>
      <Segment type="Simple">
        <PillarChoice>Deposit</PillarChoice>
        <Quotes>
          <Quote>
            <Tenor>1Y</Tenor>
            <Rate>0.035</Rate>
          </Quote>
          <Quote>
            <Tenor>5Y</Tenor>
            <Rate>0.036</Rate>
          </Quote>
          <Quote>
            <Tenor>10Y</Tenor>
            <Rate>0.037</Rate>
          </Quote>
        </Quotes>
      </Segment>
    </Segments>
  </Curve>
</CurveConfiguration>
```

#### 2. 변동금리 채권용 (Discount Curve + Index Curve)

```xml
<CurveConfiguration>
  <!-- ① 할인 곡선 (현금흐름 할인용) -->
  <Curve id="KRW-DISC" currency="KRW" type="Discount">
    <Segments>
      <Segment type="Simple">
        <PillarChoice>Deposit</PillarChoice>
        <Quotes>
          <Quote>
            <Tenor>1Y</Tenor>
            <Rate>0.035</Rate>
          </Quote>
          <Quote>
            <Tenor>5Y</Tenor>
            <Rate>0.036</Rate>
          </Quote>
          <Quote>
            <Tenor>10Y</Tenor>
            <Rate>0.037</Rate>
          </Quote>
        </Quotes>
      </Segment>
    </Segments>
  </Curve>

  <!-- ② 지수 전망 곡선 (미래 쿠폰 계산용) -->
  <Curve id="KRW-CD91" currency="KRW" type="Index">
    <Segments>
      <Segment type="Simple">
        <PillarChoice>Deposit</PillarChoice>
        <ProjectionCurve>KRW-DISC</ProjectionCurve> <!-- 할인 곡선 참조 -->
        <Quotes>
          <Quote>
            <Tenor>3M</Tenor>
            <Rate>0.034</Rate>
          </Quote>
          <Quote>
            <Tenor>6M</Tenor>
            <Rate>0.035</Rate>
          </Quote>
          <Quote>
            <Tenor>1Y</Tenor>
            <Rate>0.036</Rate>
          </Quote>
        </Quotes>
      </Segment>
    </Segments>
  </Curve>
</CurveConfiguration>
```

## 왜 두 개의 곡선이 필요한가?

### 이론적 배경

변동금리 채권 평가에는 두 가지 다른 기간구조가 필요합니다:

| 곡선 | 역할 | 제공하는 것 |
|-----|------|-----------|
| **할인 곡선 (Discount)** | 시간 가치 할인 | 각 시점의 할인계수 $P(0,t)$ |
| **지수 전망 곡선 (Projection)** | 미래 금리 전망 | 각 시점의 포워드 금리 $f(0,t_1,t_2)$ |

### 예시: KRW CD91 기반 변동금리 국채

```
만기 3년, 분기별 재설정 (Reset)
쿠폰 = CD91 + 10bp 스프레드
```

**평가 시 필요한 계산:**

1. **1년 후 CD91 재설정 예상 금리**: 지수 전망 곡선에서 $F_{CD91}(1Y, 1Y+3M)$ 조회
2. **쿠폰 계산**: $Coupon = F_{CD91} + 0.0010$
3. **현금흐름 할인**: 할인 곡선에서 $P(0, 1Y+3M)$로 할인

## 표기법 정리

| 용어 | 의미 | ORE 내에서의 용어 |
|-----|------|----------------|
| Index Forward Curve | 지수 전망 곡선 | **Projection Curve** 또는 **Index Curve** |
| Discount Curve | 할인 곡선 | **Discount Curve** |
| Yield Curve | 수익률 곡선 | **Yield Curve** (일반적으로 할인 곡선과 동일) |

## 실무 팁

### 1. 곡선 간 관계
```xml
<Segment type="Simple">
  <ProjectionCurve>KRW-DISC</ProjectionCurve>  <!-- 할인 곡선 참조 -->
</Segment>
```

지수 전망 곡선은 일반적으로 할인 곡선을 참조하여 구축됩니다.

### 2. 곡선 세그먼트 유형에 따른 ProjectionCurve 파라미터

[[concepts/curve-building]]에 설명된 대로:

| 세그먼트 | ProjectionCurve 사용 |
|---------|---------------------|
| **Simple** | ✅ 사용 (IBOR 지수 전망용) |
| **Tenor Basis** | ✅ 사용 (Receive/Pay 각각) |
| **FittedBond** | ✅ 사용 (IborIndexCurves) |
| **Direct** | ❌ 미사용 |
| **Zero Spread** | ❌ 미사용 |

### 3. todaysmarket.xml에서의 정의

```xml
<Market>
  <Curves>
    <Curve>Yield/KRW-DISC</Curve>        <!-- 할인 곡선 -->
    <IndexCurve>KRW-CD91/KRW-CD91</IndexCurve>  <!-- 지수 곡선 -->
  </Curves>
</Market>
```

## 요약

| 질문 | 답변 |
|-----|------|
| 고정금리 국채 무위험 평가 | **할인 곡선만 있으면 됨** ✅ |
| 변동금리 국채 무위험 평가 | **할인 곡선 + 지수 전망 곡선 필요** ✅ |
| 지수 전망 곡선의 역할 | 미래 변동 쿠폰 계산 (Forward Rates 제공) |
| 할인 곡선의 역할 | 모든 현금흐름의 시간 가치 할인 |

## 관련 문서

- [[concepts/curve-building]] — 곡선 구축 방법론 (Simple 세그먼트, ProjectionCurve)
- [[explorations/bond-valuation-methods]] — Bond 상품 평가 방식
- [[summaries/products]] — Floating Leg Data 섹션 (pages 385-392)
