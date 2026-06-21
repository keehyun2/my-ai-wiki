---
query: "기본 VND bond 상품 평가할때 필요한 마켓데이터는 뭔가요?"
---

이 답변은 ORE의 Bond 평가 방법론, 곡선 구축 가이드, 그리고 시장 데이터 설정을 검토하여 작성되었습니다.

---

# VND Bond 평가에 필요한 마켓 데이터

VND (Vietnamese Dong) 채권 상품을 ORE에서 평가하기 위해 필요한 마켓 데이터는 다음과 같습니다:

## 1. 수익률 곡선 (Yield Curves)

### 할인 곡선 (Discount Curve)
- **목적**: 현금흐름 할인을 위한 제로금리/할인계수 제공
- **구성 요소**:
  - VND 통화의 예금(Deposit) 금리
  - VND IBOR/FRA 금리 (예: VNIBOR)
  - VND 스왑 금리
  - VND OIS (Overnight Index Swap) 금리

### 지수 곡선 (Index Curves)
- **목적**: 부동금리 지수의 전망(Projection) 제공
- **주요 지수**: VNIBOR (Vietnam Interbank Offered Rate)

> **참고**: VNIBOR는 ORE의 기본 허용값 목록에 없으므로, [[explorations/fixing-history-vnibor-allow-values]]에 설명된 대로 **Generic Index** 형식(`GENERIC-VNIBOR`)으로 등록해야 합니다.

### 곡선 구축 방법
VND 채권 평가를 위해 다음 곡선 세그먼트 유형을 사용할 수 있습니다:

| 세그먼트 유형 | 설명 | 사용 시기 |
|-------------|------|-----------|
| **FittedBond** | 유동 채권 가격에 피팅하여 곡선 구축 | 시장에 유동 VND 채권이 충분할 때 |
| **Bond Yield Shifted** | 채권 YTM 기준 조정된 곡선 | 유동 채권이 적을 때 (하나로도 구축 가능) |
| **Yield Plus Default** | 기준 곡선 + 디폴트 곡선 | 신용 스프레드가 중요할 때 |
| **Simple** | 예금, FRA, 스왑 등 기본 상품 | 표준 금리 상품이 있을 때 |

## 2. 신용 곡선 (Credit/Default Curves)

### 디폴트 곡선 (Default Curves)
- **목적**: 발행체의 신용 리스크 반영
- **구성 요소**:
  - 위험률(Hazard Rate) 기간 구조
  - 회수율(Recovery Rate): 일반적으로 40%

### 신용 스프레드
- CDS 스프레드 또는 채권 스프레드에서 부트스트랩
- 발행체/등급별로 별도 구성

## 3. FX 곡선 (FX Curves)

### FX 현물 및 선물 곡선
- **목적**: 타 통화 표시 채권의 환율 반영
- **구성 요소**:
  - VND/USD 현물 환율
  - FX 포워드 포인트
  - 크로스커런시 베이시스 스프레드 (필요시)

### 커버드 이자율 평가(Covered Interest Rate Party) 기반
- FX 곡선은 금리 차이와 이론적 관계 유지

## 4. 변동성 구조 (Volatility Structures)

### 금리 변동성
- **목적**: 임베디드 옵션(콜러블/풀러블) 평가
- **구성 요소**:
  - Cap/Floor 변동성 (Black 또는 SABR 모델)
  - Swaption 변동성
  - 기간 구조(Term Structure) 및 스마일(Smile)

### FX 변동성 (다통화 채권의 경우)
- FX 옵션 가격 기반 변동성 표면
- Vanna-Volga 또는 SABR 모델

## 5. Fixing History (시장 데이터)

### 지수 Fixings
- **VNIBOR Fixings**: [[explorations/fixing-history-vnibor-allow-values]]에 설명된 대로 `fixings.txt`에 등록
```
20250203 GENERIC-VNIBOR 0.04500
20250204 GENERIC-VNIBOR 0.04550
```

### 기타 필요 Fixings
- OIS 지수 fixings (Overnight Index Swap 사용 시)
- CPI fixings (인플레이션 연계 채권의 경우)

## 6. 설정 파일 (Configuration Files)

### curveconfig.xml
```xml
<CurveConfiguration>
  <Curve id="VND-DISC" currency="VND" type="Discount">
    <!-- 세그먼트 정의 -->
  </Curve>
  <Curve id="VND-VNIBOR" currency="VND" type="Index">
    <!-- VNIBOR 지수 곡선 -->
  </Curve>
</CurveConfiguration>
```

### todaysmarket.xml
```xml
<Market>
  <Fixings>
    <!-- Fixing 데이터 포인트 -->
  </Fixings>
  <Curves>
    <Curve>Yield/VND-DISC</Curve>
    <Curve>Yield/VND-VNIBOR</Curve>
  </Curves>
</Market>
```

## 7. 채권별 추가 데이터

### Security Reference Data
- 채권 식별자(ISIN, CUSIP 등)
- 발행일, 만기일
- 쿠폰 타입(고정/변동/영구)
- 쿠폰 스케줄
- 발행조건(Call/Put 옵션 등)

### 시장 가격 데이터 (Curve Fitting용)
- 유동 VND 국채 및 회사채 가격
- 각 만기별 Bid-Ask 스프레드

## 요약표

| 데이터 유형 | 필요 여부 | 설명 |
|----------|----------|------|
| **할인 곡선** | 필수 | 현금흐름 할인용 |
| **지수 곡선(VNIBOR)** | 조건부 | 부동금리 채권의 경우 |
| **신용 곡선** | 권장 | 신용 리스크 반영 |
| **FX 곡선** | 조건부 | 타 통화 표시 채권의 경우 |
| **금리 변동성** | 조건부 | 옵션 내장 채권의 경우 |
| **FX 변동성** | 조건부 | 다통화 옵션 채권의 경우 |
| **Fixing 데이터** | 필수 | 지수 Fixing 역사 |
| **채권 Reference 데이터** | 필수 | 기본 발행 정보 |

## 관련 문서

- [[explorations/bond-valuation-methods]] — Bond 상품 평가 방식 상세
- [[concepts/curve-building]] — 곡선 구축 방법론
- [[summaries/products]] — Bond Products 섹션
- [[explorations/fixing-history-vnibor-allow-values]] — VNIBOR Generic Index 등록법
