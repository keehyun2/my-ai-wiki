---
sources: [summaries/userguide.md]
brief: XVA는 파생상품 가치조정으로 CVA, DVA, FVA, COLVA, MVA 등을 포함한다.
---

# XVA 가치조정 (Valuation Adjustments)

**XVA** (X-Value Adjustment)는 장외파생상품 포트폴리오의 공정가치를 조정하는 일련의 가치조정 항목들을 총칭한다. ORE는 몬테카를로 시뮬레이션을 통해 이러한 조정을 계산하며, 주요 구성요소로는 신용평가조정(CVA), 차변평가조정(DVA), 자금조달평가조정(FVA), 담보평가조정(COLVA), 초기증거금평가조정(MVA) 등이 있다.

## 주요 XVA 구성요소

- **CVA (Credit Valuation Adjustment)**: 상대방 신용위험을 반영한 가치조정. 거래상대방이 채무불이행할 경우 손실 가능성을 반영한다.
- **DVA (Debit Valuation Adjustment)**: 자신의 신용위험을 반영한 가치조정. 자신의 채무불이행 시 이익을 반영한다.
- **FVA (Funding Valuation Adjustment)**: 자금조달 비용을 반영한 조정.
- **COLVA (Collateral Valuation Adjustment)**: 담보 약정(Credit Support Annex, CSA)으로 인한 비용/편익 조정.
- **MVA (Margin Valuation Adjustment)**: 초기증거금 포스팅 비용을 반영한 조정.
- **KVA (Capital Valuation Adjustment)**: 규제자본 비용 조정.

## ORE의 XVA 계산 흐름

ORE는 XVA 계산을 위해 세 가지 주요 단계를 수행한다:
1. **NPV 큐브 생성**: 몬테카를로 시뮬레이션으로 모든 거래에 대한 미래 시점별 NPV를 계산한다.
2. **넷팅 세트 집계 및 담보 모델링**: CSA 조건(임계값, 최소이전금액, MPoR 등)에 따라 담보를 모델링하고 순익스포저를 산출한다.
3. **XVA 산출**: 집계된 익스포저와 신용곡선, 자금조달곡선 등을 이용해 각 가치조정 항목을 계산한다.

ORE는 사전 생성된 NPV 큐브를 재사용하여 큐브 재생성 없이 다양한 XVA 시나리오를 분석할 수 있다.

## XVA 리스크 분석

ORE는 XVA 자체의 리스크 측정도 지원한다:
- **XVA 스트레스 테스트**: 시장 변동 시나리오 하에서 XVA 변화를 측정한다.
- **XVA P&L 설명**: 두 평가일 사이의 시장 변동에 따른 XVA 변화를 분해한다.
- **XVA 민감도**: Bump & Revalue 방식으로 XVA의 시장요인별 민감도를 계산한다.
- **CVA 자본**: SA-CVA 및 BA-CVA 규제자본을 산출한다.

## 관련 개념

- [[concepts/exposure-simulation]] - XVA 계산의 기반이 되는 익스포저 시뮬레이션
- [[concepts/initial-margin]] - MVA 계산과 관련된 초기증거금
- [[concepts/netting-set-collateral]] - 담보 모델링과 CSA 조건
- [[concepts/american-monte-carlo]] - AMC를 활용한 XVA 계산
- [[summaries/userguide]] - ORE 사용자 가이드 상세 요약

## 성능 최적화

ORE는 XVA 민감도 계산을 위해 AAD(Algorithmic Differentiation)와 GPU 병렬화를 지원한다. 단일 스왑의 CVA 민감도 예시에서는 Bump & Revalue 방식이 48초 소요되던 것을 AAD로 2초로 단축했다.