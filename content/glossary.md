---
title: Glossary (용어사전)
description: Technical terminology from ORE financial engineering documentation
---

# Glossary (용어사전)

Technical terms used across ORE concepts and explorations, organized by category.

## Categories

- [Curve Building](#curve-building)
- [Risk Analytics](#risk-analytics)
- [Pricing Models](#pricing-models)
- [Bond Valuation](#bond-valuation)
- [XVA Adjustments](#xva-adjustments)
- [Monte Carlo](#monte-carlo)
- [Market Data](#market-data)

---

## Curve Building

### Bootstrap Methodology (부트스트랩 방법론)
**Definition:** A method to construct a zero-coupon yield curve by sequentially deriving zero rates from market instrument prices (deposits, FRAs, futures, swaps).

**ORE Context:** Used in `curveconfig.xml` to build yield curves. Each instrument's market price is used to back out the zero rate for its maturity, creating a continuous term structure.

**Related:** [[concepts/curve-building]] | [[explorations/bond-valuation-methods]]

### Discount Curve (할인 곡선)
**Definition:** A term structure of discount factors used to calculate present values of future cash flows.

**ORE Context:** Primary curve type in ORE. Provides zero rates/discount factors for NPV calculation. Built from deposits, FRAs, futures, and swaps.

**Related:** [[concepts/curve-building]] | [[explorations/vnd-bond-market-data-requirements]]

### Index Curve (지수 곡선)
**Definition:** A term structure used for projecting future index rates (e.g., IBOR rates for floating rate payments).

**ORE Context:** Required for floating rate instruments. Projects future fixings of indices like VNIBOR, EURIBOR, etc.

**Related:** [[concepts/curve-building]] | [[explorations/fixed-vs-floating-rate-bond-curves]]

### Projection Curve (전망 곡선)
**Definition:** Same as Index Curve - used for projecting future values of floating rate indices.

**ORE Context:** Referenced in floating rate leg definitions to forecast cash flows.

**Related:** [[concepts/curve-building]]

### Term Structure (기간구조)
**Definition:** The relationship between rates (yields, discount factors, forward rates) and time to maturity.

**ORE Context:** Fundamental concept underlying all curve types in ORE (yield, FX, inflation, equity, commodity, default curves).

**Related:** [[concepts/curve-building]]

### Interpolation Methods (보간 방법)
**Definition:** Mathematical methods to estimate values between known data points on a curve.

**ORE Context:** Supported methods include:
- **LogLinear** (default): Logarithmic linear interpolation of discount factors
- **Linear**: Linear interpolation
- **Cubic**: Cubic spline interpolation

**Related:** [[concepts/curve-building]]

### Extrapolation (외삽)
**Definition:** Estimating values beyond the known range of a curve.

**ORE Context:** Methods include:
- **ContinuousForward**: Continuous forward rate extrapolation
- **DiscreteForward**: Discrete forward rate extrapolation

**Related:** [[concepts/curve-building]]

### Zero Rate (제로금리)
**Definition:** Interest rate for a zero-coupon bond of a given maturity.

**ORE Context:** Fundamental output of bootstrap methodology. Used to construct discount factors.

**Related:** [[concepts/curve-building]]

### Forward Rate (선물 금리)
**Definition:** Interest rate implied by current term structure for a future time period.

**ORE Context:** Calculated from zero rates. Used in FRA and forward contract valuation.

**Related:** [[concepts/curve-building]]

### Swap Rate (스왑 금리)
**Definition:** The fixed rate that equates the present value of fixed and floating legs in a swap.

**ORE Context:** Used in par sensitivity conversions and as input for curve bootstrapping.

**Related:** [[concepts/curve-building]]

### Interpolation Variable (보간 변수)
**Definition:** The curve variable used for interpolation.

**ORE Context:** Options include:
- **Discount** (default): Interpolate discount factors
- **Zero**: Interpolate zero rates
- **Forward**: Interpolate forward rates

**Related:** [[concepts/curve-building]]

### Yield Curve (수익률 곡선)
**Definition:** A curve showing yields (interest rates) across different maturities.

**ORE Context:** Core market data for pricing. Types include discount curves, index curves, and various basis curves.

**Related:** [[concepts/curve-building]] | [[explorations/sources-userguide-json-162-177-yeild-curve]]

---

## Risk Analytics

### VaR (Value-at-Risk)
**Definition:** Maximum potential loss at a given confidence level over a specified time horizon.

**ORE Context:** Supported types:
- **Parametric VaR**: Delta-gamma normal VaR using sensitivity + covariance matrix
- **Historical Simulation VaR**: Using historical market scenarios

**Related:** [[concepts/market-risk-analytics]]

### Sensitivity Analysis (민감도 분석)
**Definition:** Calculation of first and second order derivatives of portfolio value with respect to market factors.

**ORE Context:** Calculates:
- **1st order**: Delta (interest rates, FX, etc.)
- **2nd order**: Gamma, Cross-gamma, Vega

**Related:** [[concepts/market-risk-analytics]]

### Stress Testing (스트레스 테스트)
**Definition:** Evaluating portfolio impact under predefined adverse market scenarios.

**ORE Context:** Scenarios include:
- **Parallel rates**: Parallel shift of yield curve
- **Twist**: Curve steepening/flattening
- Custom scenarios via `stressconfig.xml`

**Related:** [[concepts/market-risk-analytics]]

### P&L Explain (손익 설명)
**Definition:** Decomposition of profit/loss into contributions from market movements and sensitivities.

**ORE Context:** Uses par sensitivity for intuitive explanation of P&L changes between two dates.

**Related:** [[concepts/market-risk-analytics]]

### Par Domain Conversion (Par 도메인 변환)
**Definition:** Transformation from zero rates to par rates (swap rates) using Jacobi transformation.

**ORE Context:** Makes sensitivity analysis more intuitive by expressing in market-observable par rates.

**Related:** [[concepts/market-risk-analytics]]

### Delta (델타)
**Definition:** First-order sensitivity of portfolio value to changes in underlying market factors.

**ORE Context:** Computed for discount curves, index curves, FX spot/volatility, etc.

**Related:** [[concepts/market-risk-analytics]]

### Gamma (감마)
**Definition:** Second-order sensitivity of portfolio value to changes in underlying factors.

**ORE Context:** Convexity measure for risk management.

**Related:** [[concepts/market-risk-analytics]]

### Vega (베가)
**Definition:** Sensitivity to volatility changes.

**ORE Context:** Computed for swaption volatilities and other volatility-sensitive products.

**Related:** [[concepts/market-risk-analytics]]

---

## Pricing Models

### Black Model
**Definition:** Analytical model for European options assuming lognormal distribution.

**ORE Context:** Standard model for caps/floors, swaptions, FX options, equity options. Assumes constant volatility (no smile).

**Related:** [[concepts/pricing-models]]

### SABR Model (Stochastic Alpha Beta Rho)
**Definition:** Stochastic volatility model for capturing volatility smile effects.

**ORE Context:** Parameters:
- **Alpha**: ATM volatility
- **Beta**: Elasticity (0-1, 0.5 = CEV)
- **Rho**: Correlation between asset and volatility
- **Nu**: Vol of vol

**Related:** [[concepts/pricing-models]]

### LGM Model (Linear Gauss Markov)
**Definition:** One-factor interest rate model with linear Gaussian Markov process.

**ORE Context:** Used for Bermudan/American swaptions, callable bonds. Solvable analytically with tree implementation for early exercise.

**Related:** [[concepts/pricing-models]] | [[concepts/monte-carlo-simulation]]

### Hull-White Model
**Definition:** Extended Vasicek model with time-dependent parameters.

**ORE Context:** Mean-reverting process with time-dependent volatility. Used for Bermudan/American options via tree or finite difference.

**Related:** [[concepts/pricing-models]]

### Bachelier Model
**Definition:** Option pricing model assuming normal distribution.

**ORE Context:** Designed for negative interest rate environments. Used in EU and other markets with negative rates.

**Related:** [[concepts/pricing-models]]

### Barone-Adesi Whaley (BAW)
**Definition:** Analytical approximation for American options.

**ORE Context:** Fast approximation for American FX and equity options. More efficient than full numerical methods.

**Related:** [[concepts/pricing-models]]

### Shifted Black
**Definition:** Modified Black model for situations where lognormal assumption doesn't hold.

**ORE Context:** Used when standard Black model assumptions are violated.

**Related:** [[concepts/pricing-models]]

### Implied Volatility (내재 변동성)
**Definition:** Volatility parameter that makes model price equal market price.

**ORE Context:** Reverse-engineered from market prices. Used for model calibration.

**Related:** [[concepts/pricing-models]]

### ATM (At-The-Money)
**Definition:** Option whose strike price equals the current forward price.

**ORE Context:** Reference point for volatility quotes and smile modeling.

**Related:** [[concepts/pricing-models]]

### Volatility Smile (변동성 스마일)
**Definition:** Pattern where implied volatility varies by strike price (typically higher for OTM/ITM options).

**ORE Context:** SABR model captures this effect. Important for accurate option pricing.

**Related:** [[concepts/pricing-models]]

---

## Bond Valuation

### DCF (Discounted Cash Flow)
**Definition:** Valuation method that discounts future cash flows at appropriate rates.

**ORE Context:** Fundamental methodology for bond pricing. Price = Σ(Cash Flow × Discount Factor).

**Related:** [[explorations/bond-valuation-methods]]

### YTM (Yield to Maturity)
**Definition:** Internal rate of return equating bond price to present value of cash flows.

**ORE Context:** Used in Bond Yield Shifted curve segments. Measures yield if held to maturity.

**Related:** [[explorations/bond-valuation-methods]]

### OAS (Option-Adjusted Spread)
**Definition:** Spread measure that accounts for embedded options (callable/puttable features).

**ORE Context:** Used for callable bonds. Reflects credit and option risk beyond basic yield.

**Related:** [[explorations/bond-valuation-methods]]

### Duration (듀레이션)
**Definition:** Measure of bond price sensitivity to interest rate changes (first derivative).

**ORE Context:** Key risk metric for fixed income. Used in Bond Yield Shifted calculations.

**Related:** [[concepts/market-risk-analytics]]

### Convexity (컨벡서티)
**Definition:** Second-order measure of bond price sensitivity to rate changes.

**ORE Context:** Adjusts duration for large rate changes. Important for risk management.

**Related:** [[concepts/market-risk-analytics]]

### Hazard Rate (위험률)
**Definition:** Instantaneous probability of default intensity.

**ORE Context:** Used in default curve construction. Core input for CVA and credit risk modeling.

**Related:** [[explorations/vnd-bond-market-data-requirements]] | [[concepts/xva-valuation-adjustments]]

### Recovery Rate (회수율)
**Definition:** Expected percentage recovered in event of default.

**ORE Context:** Typically 40% for corporate defaults. Used in CVA and default curve calculations.

**Related:** [[explorations/vnd-bond-market-data-requirements]] | [[concepts/xva-valuation-adjustments]]

### Credit Spread (신용 스프레드)
**Definition:** Additional yield over risk-free rate compensating for credit risk.

**ORE Context:** Can be bootstrapped from CDS spreads or bond spreads. Used in Yield Plus Default curves.

**Related:** [[explorations/creditcurveid-bond-valuation]]

### Callable Bond (콜러블 본드)
**Definition:** Bond that issuer can redeem before maturity.

**ORE Context:** Valued using OAS model or interest rate tree. Early exercise right affects valuation.

**Related:** [[explorations/bond-valuation-methods]]

---

## XVA Adjustments

### XVA (X-Value Adjustment)
**Definition:** Collective term for valuation adjustments to OTC derivative portfolio fair value.

**ORE Context:** Calculated via Monte Carlo simulation. Reflects funding, credit, collateral, and capital costs.

**Related:** [[concepts/xva-valuation-adjustments]] | [[concepts/monte-carlo-simulation]]

### CVA (Credit Valuation Adjustment)
**Definition:** Valuation adjustment for counterparty credit risk.

**ORE Context:** Cost of potential loss if counterparty defaults. Calculated from exposure profiles and default probabilities.

**Related:** [[concepts/xva-valuation-adjustments]]

### DVA (Debit Valuation Adjustment)
**Definition:** Valuation adjustment for own credit risk.

**ORE Context:** Benefit if own default occurs. Mirrors CVA from own perspective.

**Related:** [[concepts/xva-valuation-adjustments]]

### FVA (Funding Valuation Adjustment)
**Definition:** Valuation adjustment for funding costs.

**ORE Context:** Cost of funding uncollateralized positions. Reflects funding spread in market.

**Related:** [[concepts/xva-valuation-adjustments]]

### COLVA (Collateral Valuation Adjustment)
**Definition:** Adjustment for collateral agreement (CSA) effects.

**ORE Context:** Costs/benefits from collateral posting based on thresholds, MTA, etc.

**Related:** [[concepts/xva-valuation-adjustments]]

### MVA (Margin Valuation Adjustment)
**Definition:** Adjustment for initial margin posting costs.

**ORE Context:** Cost of funding initial margin requirements. Important for SIMM and DIM calculations.

**Related:** [[concepts/xva-valuation-adjustments]]

### KVA (Capital Valuation Adjustment)
**Definition:** Adjustment for regulatory capital costs.

**ORE Context:** Economic cost of capital allocated to trades. Reflects regulatory capital requirements.

**Related:** [[concepts/xva-valuation-adjustments]]

### EPE (Expected Positive Exposure)
**Definition:** Average positive exposure over time horizon.

**ORE Context:** Core metric for CVA calculation. Expected future value when positive (credit exposure).

**Related:** [[concepts/monte-carlo-simulation]] | [[concepts/xva-valuation-adjustments]]

### PFE (Potential Future Exposure)
**Definition:** Maximum positive exposure at confidence level (e.g., 95th percentile).

**ORE Context:** Risk metric for exposure limits. Used in regulatory capital and margin calculations.

**Related:** [[concepts/monte-carlo-simulation]] | [[concepts/xva-valuation-adjustments]]

### ENE (Expected Negative Exposure)
**Definition:** Average negative exposure over time horizon.

**ORE Context:** Used for DVA calculation. Expected future value when negative (benefit from own default).

**Related:** [[concepts/monte-carlo-simulation]] | [[concepts/xva-valuation-adjustments]]

### MPoR (Margin Period of Risk)
**Definition:** Time required to replace or close positions in default scenario.

**ORE Context:** Typically 10-20 days for regulatory purposes. Affects margin calculations and SIMM.

**Related:** [[concepts/xva-valuation-adjustments]]

---

## Monte Carlo

### Monte Carlo Simulation (몬테카를로 시뮬레이션)
**Definition:** Computational method using random sampling to model probabilistic systems.

**ORE Context:** Core engine for XVA, exposure simulation, and market risk analysis. Simulates future market scenarios across multiple asset classes.

**Related:** [[concepts/monte-carlo-simulation]]

### NPV Cube (NPV 큐브)
**Definition:** Three-dimensional array of NPV values (dates × paths × trades).

**ORE Context:** Generated by Monte Carlo simulation. Reused for multiple XVA calculations without regeneration.

**Related:** [[concepts/monte-carlo-simulation]] | [[concepts/xva-valuation-adjustments]]

### CrossAssetModel (교차 자산 모델)
**Definition:** Multi-asset model framework simulating correlated risk factors.

**ORE Context:** Components:
- **LGM**: Interest rate model per currency
- **FX**: FX spot models
- **Equity**: Equity models
- **Inflation**: Inflation models
- **Correlation**: Instantaneous correlations

**Related:** [[concepts/monte-carlo-simulation]]

### Sobol Sequence
**Definition:** Low-discrepancy quasi-random number sequence.

**ORE Context:** Default RNG type in ORE. Provides better convergence than pseudo-random for Monte Carlo.

**Related:** [[concepts/monte-carlo-simulation]]

### AMC (American Monte Carlo)
**Definition:** Monte Carlo method for American/Bermudan options using regression-based conditional expectation.

**ORE Context:** Enables exposure simulation for early-exercise products. Requires LGM mean reversion = 0 for consistency.

**Related:** [[concepts/monte-carlo-simulation]]

### Scenario Generation (시나리오 생성)
**Definition:** Generation of market scenarios from simulation model.

**ORE Context:** `scenarioGeneration` analysis type exports base scenarios and computes statistics.

**Related:** [[concepts/monte-carlo-simulation]]

---

## Market Data

### VNIBOR (Vietnam Interbank Offered Rate)
**Definition:** Benchmark interest rate for Vietnamese Dong interbank market.

**ORE Context:** Not in ORE's default index list. Must register as Generic Index (`GENERIC-VNIBOR`) in allow values and fixings.

**Related:** [[explorations/fixing-history-vnibor-allow-values]] | [[explorations/vnd-bond-market-data-requirements]]

### Fixing History (결제 이력)
**Definition:** Historical values of market indices/fixings.

**ORE Context:** Required in `fixings.txt` for index curve construction. Format: `DATE INDEX VALUE`.

**Related:** [[explorations/fixing-history-vnibor-allow-values]] | [[explorations/vnd-bond-market-data-requirements]]

### Generic Index (일반 지수)
**Definition:** Custom index registration for indices not in ORE's built-in list.

**ORE Context:** Format `GENERIC-<NAME>`. Used for VNIBOR and other non-standard indices.

**Related:** [[explorations/fixing-history-vnibor-allow-values]]

### curveconfig.xml
**Definition:** Configuration file defining curve templates and segment parameters.

**ORE Context:** Central configuration for all curve types (yield, FX, inflation, equity, commodity, default, volatility).

**Related:** [[concepts/curve-building]] | [[explorations/sources-userguide-json-162-177-yeild-curve]]

### todaysmarket.xml
**Definition:** Configuration file linking curves to market data quotes.

**ORE Context:** Defines which curve configurations to use for today's market and links to market data quotes.

**Related:** [[explorations/vnd-bond-market-data-requirements]]

### FittedBond Segment
**Definition:** Curve segment type that fits to liquid bond prices.

**ORE Context:** Constructs yield curve by bootstrapping from bond prices. Includes interpolation/extrapolation settings.

**Related:** [[concepts/curve-building]] | [[explorations/sources-userguide-json-162-177-yeild-curve]]

### Bond Yield Shifted Segment
**Definition:** Curve segment adjusted from bond YTM relative to reference curve.

**ORE Context:** Useful when few liquid bonds available. Can build from single bond YTM.

**Related:** [[concepts/curve-building]] | [[explorations/sources-userguide-json-162-177-yeild-curve]]

### Yield Plus Default Segment
**Definition:** Curve combining reference curve + default curve.

**ORE Context:** All-in discount curve including credit risk. Combines at instantaneous forward rate level.

**Related:** [[concepts/curve-building]] | [[explorations/creditcurveid-bond-valuation]] | [[explorations/sources-userguide-json-162-177-yeild-curve]]

### Tenor Basis Swap (텐서 베이시스 스왑)
**Definition:** Swap exchanging floating rates of different tenors (e.g., 3M vs 6M LIBOR).

**ORE Context:** Used to construct tenor basis curves. Captures yield curve shape between tenors.

**Related:** [[concepts/curve-building]]

### Cross Currency Basis Swap (크로스커런시 베이시스 스왑)
**Definition:** Swap exchanging cash flows in different currencies.

**ORE Context:** Used to construct FX curves and cross-currency basis spreads.

**Related:** [[concepts/curve-building]]

---

## Related Pages

- [[index]] — Main knowledge base index
- [[concepts/curve-building]] — Curve building methodology
- [[concepts/market-risk-analytics]] — Market risk analysis
- [[concepts/pricing-models]] — Pricing models
- [[concepts/xva-valuation-adjustments]] — XVA adjustments
- [[concepts/monte-carlo-simulation]] — Monte Carlo simulation
