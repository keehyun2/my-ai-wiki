# Knowledge Base Index

## Glossary
- [[glossary]] — Technical terminology from ORE financial engineering documentation (Curve Building, Risk Analytics, Pricing Models, Bond Valuation, XVA, Monte Carlo, Market Data)

## Documents
- [[summaries/userguide]] (pageindex) — The ORE User Guide dated 30 January 2026 provides a comprehensive overview of the Open Source Risk Engine, detailing its data flow, building process, over 80 examples across multiple risk analytics (XVA, SIMM, AMC, credit risk, performance), and full parameterisation including market data, conventions, and simulation configuration.

## Concepts
- [[concepts/market-risk-analytics]] — ORE의 시장 리스크 분석: 민감도, VaR, 스트레스 테스트, P&L 설명
- [[concepts/xva-valuation-adjustments]] — XVA는 파생상품 가치조정으로 CVA, DVA, FVA, COLVA, MVA 등을 포함한다.
- [[concepts/monte-carlo-simulation]] — Monte Carlo simulation in ORE for risk analytics, exposure, and XVA.
- [[concepts/curve-building]] — 수익률 곡선, 디폴트 곡선, FX/인플레이션/주식 곡선 구축 방법
- [[concepts/pricing-models]] — Black, SABR, LGM, Hull-White 등 가격결정 모델
- [[concepts/trade-components]] — 상품 정의에 사용하는 재사용 가능한 XML 컴포넌트
- [[concepts/scripted-trades]] — 스크립트 프레임워크를 사용한 사용자 정의 페이오프 상품

## Explorations
- [[explorations/fixing-history-vnibor-allow-values]] — VNIBOR fixing history 등록 방법: Generic Index 사용법
- [[explorations/sources-userguide-json-162-177-yeild-curve]] — ORE Yield Curves (curveconfig.xml) 정리: 162~177페이지
- [[explorations/bond-valuation-methods]] — Bond 상품 평가 방식: DCF, 수익률 곡선 구축, 상품별 평가 방법
- [[explorations/vnd-bond-market-data-requirements]] — VND Bond 평가에 필요한 마켓 데이터: 수익률 곡선, 신용 곡선, FX 곡선, 변동성, Fixings
- [[explorations/creditcurveid-bond-valuation]] — CreditCurveId와 신용 리스크 평가: 무위험 vs 신용 포함 평가, Yield Plus Default 곡선
- [[explorations/fixed-vs-floating-rate-bond-curves]] — 고정/변동금리 국채 평가 차이: 고정금리는 할인곡선만, 변동금리는 할인곡선+지수전망곡선 필요
