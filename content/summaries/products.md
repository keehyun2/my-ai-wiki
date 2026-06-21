---
doc_type: pageindex
full_text: sources/products.json
---

# Document Information (pages 1–11)

Summary: The document is the ORE Product Catalogue dated 30 January 2026. It serves as one of three parts of ORE documentation, alongside the User Guide and Methodology documents. This catalogue provides comprehensive descriptions of instrument payoffs, pricing methodology, and ORE XML input guide for all products supported by ORE. The document history spans from 2016 to 2026, detailing releases by Quaternion, Acadia, and LSEG. The table of contents outlines the structure: introduction, trade data (envelope, trade-specific data for over 100 product types), trade components, netting set definitions, scripted trades, pricing methodology by asset class, pricing models, curve building, Libor fallback, and pricing engine configuration.

# Introduction (pages 12–12)

Summary: The introduction explains that the ORE documentation consists of three parts: User Guide (overview, usage examples, parameterisation, market data reference), Methodology (risk methods overview), and Products (this document - product catalogue with instrument payoffs, pricing methodology, and XML input guide). This document focuses on detailed descriptions of payoffs and ORE XML input rules for all products, followed by pricing methodology applied per product.

# Trade Data (pages 12–12)

Summary: The Trade Data section describes how trades are specified in XML files with a hierarchy of nodes and sub-nodes. The top-level Portfolio node contains individual Trade nodes delimited by `<Trade id="...">` and `</Trade>` tags. Each trade includes a TradeType element and an Envelope node with common elements (Id, Type, Counterparty, Rating, NettingSetId) plus Additional fields, followed by trade-specific data. The section provides examples of portfolio.xml structure and lists the 14 basic trade types supported.

## Envelope (pages 13–14)

Summary: The Envelope node contains basic identifying details for all trade types: Id (used to identify trades, must match Trade id attribute), Counterparty (name of counterparty for exposure analytics), NettingSetId (optional identifier for netting set eligibility, must be defined in netting set definitions file), PortfolioIds (optional list of portfolio assignments for reports like VaR), and AdditionalFields (optional custom elements for informational purposes like Sector, Book, or Folder). All envelope elements except NettingSetId, PortfolioIds, and AdditionalFields must have non-blank entries for ORE to run.

### Netting Set Details (pages 14–14)

Summary: An alternative to the single NettingSetId node is the NettingSetDetails node, which extends netting set uniqueness beyond the ID. It contains NettingSetId as a sub-node plus four optional sub-nodes: AgreementType, CallType, InitialMarginType, and LegalEntityId. All allow alphanumeric strings with underscores and spaces. This provides more granular identification for netting set management in collateral and exposure calculations.

# Trade Specific Data (pages 15–478)

Summary: This section covers trade-specific data containers for each trade type supported by ORE. Each trade type has its own XML configuration using individual elements and trade components (reusable sub-nodes). The section systematically describes over 100 product types across interest rates, FX, equity, inflation, credit, commodity, bonds, and complex exotics, providing payoff descriptions, XML input examples, and allowable values.

## Interest Rate Products (pages 15–28)

Summary: The Interest Rate products section covers fundamental IR derivatives used in ORE. Key products include Swap (vanilla IRS, single-currency basis swap, OIS, BMA swap, CMS swap, CMB swap with configurable legs), Zero Coupon Swap (one zero-coupon leg compounded at swap tenor), Cap/Floor (series of European options on IBOR/CMS indices with collar combinations), Forward Rate Agreement (FRA for future period lending), Swaption (European/Bermudan/American options to enter swaps), and Callable Swap (combination of non-callable swap and physically settled swaption). Each product includes detailed XML input specifications and payoff formulas.

## FX Derivatives (pages 30–61)

Summary: The FX derivatives section covers foreign exchange products with extensive barrier and digital options. Products include FX Forward (simple forward contract), FX Average Forward (average rate forward), FX Swap (spot plus forward exchange), FX Option (European/American vanilla options), FX Asian Option (average price options), FX Barrier Option (single/knock-in/knock-out barriers), FX Digital Barrier Option (binary payoff with barrier), FX Digital Option (binary payoff without barrier), FX Double Barrier Option (two barriers), FX Double Touch Option (double binary barrier), FX European Barrier Option (continuous barrier monitoring), FX KIKO Barrier Option (knock-in knock-out combination), FX Touch Option (one-touch binary), and FX Variance/Volatility Swap (realized volatility contracts). Each product includes barrier levels, rebate amounts, and settlement specifications.

## Equity Derivatives (pages 63–95)

Summary: The Equity derivatives section mirrors FX products but for equity underlyings. Products include Equity Option (European/American vanilla options), Equity Futures Option (options on equity futures), Equity Forward (forward contracts on equities), Equity Swap (equity return vs floating rate), Dividend Swap (dividend payment contracts), Equity Asian Option (average price options), Equity Barrier Option (various barrier types), Equity Digital Option (binary payoff), Equity Double Barrier Option (two barriers), Equity Double Touch Option (double binary barriers), Equity European Barrier Option (continuous monitoring), Equity Touch Option (one-touch binary), Equity Variance Swap (realized volatility), Equity Cliquet Option (resettable strike options), Equity Position (spot holdings), and Equity Option Position (option holdings). Products support single stocks or indices with various payoff structures.

## Inflation Products (pages 97–99)

Summary: The Inflation derivatives section covers products linked to inflation indices. Products include CPI Swap (zero coupon inflation index swap exchanging fixed for inflation-linked payments based on Consumer Price Index), Year on Year Inflation Swap (exchanges floating rate based on year-on-year inflation index for fixed rate or floating rate), with detailed specifications for inflation index attachment, observation lag, and fixing calendars. These products are used for inflation hedging and inflation-linked trading.

## Bond Products (pages 100–156)

Summary: The Bond products section is extensive, covering cash bonds and bond derivatives. Products include Bond (basic bonds with coupon schedules), Bond Position (spot bond holdings), Forward Bond (forward contracts on bonds), Bond Forward/T-Lock/J-Lock using reference data (lock-in products with reference data lookup), Bond Future (futures contracts on bond baskets), Bond Repo (repo agreements with bonds as collateral), Bond Option (options on bonds, callable/putable), Bond Option using bond reference data (options with reference data), Bond Total Return Swap (TRS on bond performance), Convertible Bond (bonds convertible to equity), Callable Bond (bonds with call options), Ascot (asset-backed credit option tranche), Collateral Bond Obligation CBO (CBO tranches), and Composite Trade (combination of multiple trades). Each product includes detailed specifications for coupon types, call schedules, conversion ratios, and credit enhancement.

## Credit Derivatives (pages 160–177)

Summary: The Credit derivatives section covers single-name and index credit products. Products include Credit Default Swap/Quanto CDS (protection against credit events with quanto feature for cross-currency), Index Credit Default Swap (CDS on indices like CDX/ITX), Index Credit Default Swap Option (options on index CDS), Synthetic CDO (portfolio credit derivatives with tranches), Risk Participation Agreement RPA (bank risk transfer), and Credit Linked Swap (combination of CDS and IRS). Products include specifications for reference entities, protection terms, tranche attachment/detachment points, and quotation conventions.

## Commodity Derivatives (pages 178–196)

Summary: The Commodity derivatives section covers energy, metals, and agricultural products. Products include Commodity Forward (forward contracts on commodities), Commodity Swap and Basis Swap (fixed for floating commodity price, basis swaps against benchmarks), Commodity Swaption (options on commodity swaps), Commodity Option (vanilla options on commodity prices), Commodity Digital Option (binary payoff), Commodity Spread Option (options on price spreads between commodities), Commodity Average Price Option (Asian-style commodity options), Commodity Option Strip (series of options), Commodity Variance/Volatility Swap (realized volatility contracts), and Commodity Position (spot holdings). Products support various commodity types with specific delivery locations and quality specifications.

## Hybrid and Complex Products (pages 197–324)

Summary: This section covers sophisticated multi-asset and exotic products. Products include Generic Total Return Swap/Contract for Difference CFD (TRS on any underlying), Equity Outperformance Option (relative performance between two assets), Double Digital Option (binary payoff on two conditions), European Option Contingent on a Barrier (barrier must be hit for option to exist), Autocallable Type 01 (auto-callable structured product with memory), Performance Option Type 01 (performance-based payoff), Window Barrier Option (barrier active during specific time window), Generic Barrier Option (flexible barrier specifications), Best Entry Option (option to enter at best price), Basket Options (options on baskets of underlyings), Worst Of Basket Swaps (payoff based on worst performing asset), Accumulators and Decumulators (forward contracts with knockout and leverage), Extended Accumulator (enhanced accumulator with additional features), Target Redemption Forward TaRF (forward that terminates when target profit reached), Knock Out Swap (swap that terminates if barrier hit), Strike Resettable Option (strike resets based on conditions), Rainbow Options (options on maximum/minimum of assets), and extensive variance derivatives including Variance Option, Variance Swap with KI/KO Barrier, Dual European Binary Option with Volatility and Spot KO Barrier, Corridor Variance Swap, Indexed Corridor Variance Swap, Corridor Variance Swap with KI/KO Barrier, Conditional Variance Swap (two types), Pairwise Variance Swap, Variance Dispersion Swap, Corridor Variance Dispersion Swap, KO Corridor Variance Dispersion Swap, Pairwise Geometric Variance Dispersion Swap, Gamma Swap, and Basket Variance Swap. These products require complex modeling and Monte Carlo or finite difference pricing methods.

## Scripted and Advanced Products (pages 358–363)

Summary: This section covers products that use ORE's scripting framework for maximum flexibility. Products include Generic Scripted Products (fully customizable payoff scripts), Flexi Swap (swap with flexible notional that can be adjusted), and Balance Guaranteed Swap BGS (swap with balance guarantee feature). These products leverage the scripted trade framework for complex path-dependent payoffs and hybrid instruments.

# Trade Components (pages 364–476)

Summary: The Trade Components section describes reusable XML sub-nodes that can be used across multiple trade types. These include Option Data (exercise dates, style, settlement, premiums), Premiums (option premium amounts and payment dates), Leg Data and Notionals (leg types, payer/receiver flags, notionals, currencies), Schedule Data (rules, dates, and derived schedules for payment streams), Fixed Leg Data and Rates (fixed rate specifications), Floating Leg Data with Spreads, Gearings, Caps and Floors (floating leg parameters), Leg Data with Amortisation Structures (notional amortization schedules), Indexings (FX and index conversions for cashflows), Cashflow Leg Data (user-defined cashflow streams), CMS Leg Data (constant maturity swap leg parameters), Constant Maturity Bond Leg Data (CMB-linked legs), Digital CMS Leg Data (digital CMS payoffs), Duration Adjusted CMS Leg Data (duration-adjusted CMS), CMS Spread Leg Data (CMS spread legs), Digital CMS Spread Leg Data (digital CMS spread payoffs), Equity Leg Data (equity-linked legs), CPI Leg Data (inflation-linked legs based on CPI), YY Leg Data (year-on-year inflation legs), ZeroCouponFixed Leg Data (zero-coupon fixed legs), Commodity Fixed Leg and Data (fixed commodity price legs), Commodity Floating Leg and Data (floating commodity price legs), Commodity Schedules (commodity delivery schedules), Equity Margin Leg and Data (equity margin lending legs), CDS Reference Information (credit default swap reference entities), Basket Data (multiple underlying specifications), Underlying (single underlying specifications), StrikeData (strike prices for options), Barrier Data (barrier levels and types), RangeBound (rangebound specifications for corridor products), Bond Basket Data for Cashflow CDO (bond baskets for CDOs), CBO Tranches (CBO tranche specifications), and Formula Based Leg Data (user-defined formula-based coupon calculations). These components enable flexible construction of complex trades from reusable building blocks.

## Option Data (pages 365–372)

Summary: The OptionData component is used within SwaptionData and FXOptionData containers. It contains LongShort (position direction), OptionType (Call/Put), Style (European/Bermudan/American), NoticePeriod/NoticeCalendar/NoticeConvention (for Bermudan exercise), Settlement (Cash/Physical), SettlementMethod (cash settlement method), MidCouponExercise (exercise on coupon dates), PayOffAtExpiry (timing of payoff), ExerciseFees (fees on exercise), ExerciseDates/ExerciseSchedule (exercise date specifications), Premiums (option premium payments), AutomaticExercise (automatic exercise feature), ExerciseData (for already-exercised options), PaymentData (payment specifications for exercise), and SettlementData (settlement specifications). This component handles all option-related parameters across different product types.

## Premiums (pages 372–373)

Summary: The Premiums component specifies option premium payments with Amount (premium amount in currency), Currency (premium currency), PayDate (premium payment date), and Type (Premium/RefundablePremium). This component is used across all option-type products to specify upfront and periodic premium payments.

## Leg Data and Notionals (pages 374–379)

Summary: The LegData component is fundamental for all multi-legged products. It includes LegType (Fixed/Floating/CMS/CMSSpread/DurationAdjustedCMS/CPI/YY/ZeroCouponFixed/Cashflow/Equity/CommodityFixed/CommodityFloating/EquityMargin), Payer (true if paying the leg), Currency (leg currency), Notionals (notional amounts as single value or schedule), DayCounter (day count convention), PaymentConvention (payment date convention), PaymentCalendar (payment calendar), PaymentLag (days for payment calculation), NotionalInitialExchange (initial notional exchange), NotionalFinalExchange (final notional exchange), NotionalAmortization (amortization schedule), NotionalAccretion (accretion schedule), FXIndex (for non-deliverable currencies), and IsNotionalReset (notional reset flag). This component handles the basic structure of each leg in a trade.

## Schedule Data (pages 379–384)

Summary: The ScheduleData component provides flexible schedule generation for payment streams. It supports three modes: Rules (generating dates from rules with StartDate, EndDate, Tenor, Calendar, Convention, Rule directive for forward/backward/zero/termination dates, and EndOfMonth flag), Dates (explicit date lists), and Derived (dates derived from another schedule with offset). The Rules mode includes advanced features like DateContainer (reference to existing date list), LastRegularFlag (handling irregular periods), and FirstDate/LastDate/PenultimateDate (specific date overrides). This component enables flexible construction of payment schedules for various products.

## Fixed Leg Data and Rates (pages 384–385)

Summary: The FixedLegData component specifies fixed rate legs with Rates (single rate or schedule of rates), and references the basic ScheduleData for payment timing. The rates can be specified as a single value for all periods or as a schedule for different periods. This component is used for the fixed legs of swaps and other products with fixed rate payments.

## Floating Leg Data, Spreads, Gearings, Caps and Floors (pages 385–392)

Summary: The FloatingLegData component specifies floating rate legs with Index (IBOR/OIS/BMA/SIFMA index name), fixingDays (days for fixing calculation), fixingCalendar (calendar for fixing dates), geometricCentres (for geometric averaging options), Spread (single spread or schedule), Gearings (gearings for leverage), Caps (cap rates), Floors (floor rates), and accrualAdjustments (accrual adjustments for certain products). This component handles various floating rate features including capped/floored floating legs and complex spread structures.

## Leg Data with Amortisation Structures (pages 392–394)

Summary: Legs with amortization schedules use the NotionalAmortization and NotionalAccretion elements within LegData. Amortization can be specified as AbsoluteAmount (amount by which notional reduces), RelativeAmount (percentage of initial notional), or RelativeAmountReduction (percentage reduction of current notional), each as a schedule. These components enable modeling of amortizing and accrediting swaps, loans, and other products with changing notionals over time.

## Indexings (pages 394–398)

Summary: The Indexings component applies FX conversions and index fixings to cashflows, particularly for non-deliverable currencies. Each Indexing includes Index (index name for conversion), FixingDays (days for fixing), FixingCalendar (calendar for fixing dates), IsInArrears (in-arrears fixing flag), and EquityDailyFixing (for equity index daily fixings). This component enables proper handling of multi-currency trades and index-based products.

## Cashflow Leg Data (pages 398–399)

Summary: The CashflowLegData component allows specification of user-defined cashflow streams instead of formula-based legs. It includes Amounts (cashflow amounts), Dates (corresponding payment dates), and PayDates (actual payment dates, possibly different from calculation dates). This component is used for loans, customized swaps, and other products with prespecified cashflows.

## CMS Leg Data (pages 399–401)

Summary: The CMSLegData component specifies Constant Maturity Swap legs with Index (CMS index name like CMS-10Y or CMS-30Y), fixingDays (days for fixing), fixingCalendar (calendar for fixing dates), and FallbackDigitalFixing (fallback fixing method). This component handles legs linked to swap rates of constant maturity, which require special fixing and averaging methods.

## Constant Maturity Bond Leg Data (pages 401–403)

Summary: The ConstantMaturityBondLegData component specifies legs linked to Constant Maturity Bond indices with Index (CMB index name like CMB-10Y), fixingDays (days for fixing), and fixingCalendar (calendar for fixing dates). This component is similar to CMS but references bond yields rather than swap rates.

## Digital CMS Leg Data (pages 403–404)

Summary: The DigitalCMSLegData component specifies digital CMS leg payoffs with Index (CMS index name), fixingDays (days for fixing), fixingCalendar (calendar for fixing dates), and FallbackDigitalFixing (fallback fixing method). Digital CMS legs pay binary amounts based on whether the CMS index is above or below specified strike levels.

## Duration Adjusted CMS Leg Data (pages 404–406)

Summary: The DurationAdjustedCMSLegData component specifies duration-adjusted CMS legs with Index (CMS index name), fixingDays (days for fixing), fixingCalendar (calendar for fixing dates), and FallbackDigitalFixing (fallback fixing method). Duration adjustment accounts for the different duration profiles of CMS instruments compared to standard swaps.

## CMS Spread Leg Data (pages 406–407)

Summary: The CMSSpreadLegData component specifies CMS spread legs with Index1 (first CMS index name), Index2 (second CMS index name), fixingDays (days for fixing), and fixingCalendar (calendar for fixing dates). CMS spread legs pay the difference between two CMS rates and are used for spread trading and volatility strategies.

## Digital CMS Spread Leg Data (pages 407–409)

Summary: The DigitalCMSSpreadLegData component specifies digital CMS spread leg payoffs with Index1 (first CMS index name), Index2 (second CMS index name), fixingDays (days for fixing), fixingCalendar (calendar for fixing dates), and FallbackDigitalFixing (fallback fixing method). Digital CMS spread legs pay binary amounts based on whether the CMS spread is above or below specified strike levels.

## Equity Leg Data (pages 409–413)

Summary: The EquityLegData component specifies equity-linked legs with EquityCreditCurve (credit curve for equity underlying), EquityName (name of equity underlying), InitialPrice (initial price for return calculation), and DividendCondition (conditions for dividend payments). This component is used for equity swaps, TRS on equities, and other products with equity-linked returns.

## CPI Leg Data (pages 413–417)

Summary: The CPILegData component specifies inflation-linked legs with Index (CPI index name like EUHICPXT or UKRPI), Interpolated (interpolation flag for fixings), Lag (observation lag in months), FinalObservationMonth (final observation month for seasonality), and Frequency (frequency for zero coupon inflation). This component handles legs linked to Consumer Price Index for inflation swaps and inflation-linked bonds.

## YY Leg Data (pages 417–419)

Summary: The YYLegData component specifies year-on-year inflation legs with Index (YY index name like EUHICPXT_YY), fixingDays (days for fixing), fixingCalendar (calendar for fixing dates), and FallbackDigitalFixing (fallback fixing method). YY legs pay based on year-on-year inflation rates rather than cumulative CPI.

## ZeroCouponFixed Leg Data (pages 419–421)

Summary: The ZeroCouponFixedLegData component specifies zero-coupon fixed legs with Rates (fixed rate for zero-coupon calculation) and Compounding (compounding method: Simple/Compounded/Continuous). This component is used for zero-coupon swaps and zero-coupon bonds where interest accumulates until maturity.

## Commodity Fixed Leg (pages 421–422)

Summary: The CommodityFixedLeg component specifies fixed price commodity legs with CommodityIndex (commodity index name for price reference), and CommodityPriceSchedule (schedule of fixed prices if varying). This component is used for commodity swaps where one leg pays a fixed commodity price.

## Commodity Fixed Leg Data (pages 421–421)

Summary: The CommodityFixedLegData component provides detailed specification for commodity fixed legs with Price (fixed commodity price), CommodityCurrency (currency for commodity pricing), and FutureMonth (delivery month for futures). This component handles the specifics of fixed-price commodity contracts.

## Commodity Floating Leg (pages 422–424)

Summary: The CommodityFloatingLeg component specifies floating price commodity legs with CommodityIndex (commodity index name for price reference), CommodityDailyPrice (daily price flag), CommodityFuturePriceMonth (future delivery month), and CommodityPriceFrequency (frequency for price observations). This component is used for commodity swaps where one leg pays a floating market price.

## Commodity Schedules (pages 422–422)

Summary: The CommoditySchedules component specifies delivery and pricing schedules for commodity products with DeliveryRoll (convention for rolling delivery dates), DeliveryRollDate (specific roll date), QuantitySchedule (schedule of quantities), and PriceSchedule (schedule of prices). These schedules handle the complex delivery and quantity specifications common in commodity markets.

## Commodity Floating Leg Data (pages 424–430)

Summary: The CommodityFloatingLegData component provides detailed specifications for commodity floating legs including CommodityPriceType (type of price: Spot/Future/FutureSettlement/PreviousFutureSettlement), CommodityFutureCalendar (calendar for future dates), CommodityFutureExpiryMinus (days before expiry), CommodityDeliveryPeriodRoll (delivery roll convention), and CommodityAveragingMethod (method for averaging prices). This component handles the complex pricing and delivery specifications of commodity derivatives.

## Equity Margin Leg (pages 430–430)

Summary: The EquityMarginLeg component specifies equity margin lending legs with EquityCreditCurve (credit curve for equity underlying), EquityName (name of equity underlying), FundingRate (funding rate for margin lending), and Spread (spread over funding rate). This component is used for equity margin lending and borrowing products.

## Equity Margin Leg Data (pages 430–431)

Summary: The EquityMarginLegData component provides detailed specifications for equity margin legs including InitialPrice (initial price for return calculation), and Multiplier (multiplier for leverage). This component handles the specific parameters of equity margin lending and short selling arrangements.

## CDS Reference Information (pages 431–431)

Summary: The CDSReferenceInformation component specifies credit default swap reference entities with ReferenceObligation (reference obligation details), CreditCurveId (credit curve identifier), and FirstToDefault (flag for first-to-default in basket). This component is used for single-name and basket CDS products to specify the credit reference.

## Basket Data (pages 431–437)

Summary: The BasketData component specifies baskets of underlyings for multi-asset products with Underlying (list of underlying specifications), and BasketConstituentData (detailed constituent data). Each Underlying includes Type (Equity/Commodity/ConvertibleBond/etc.), Name (underlying name), Weight (weight in basket), IdentifierType (type of identifier), PriceType (type of price), and other type-specific fields. This component is used for basket options, variance swaps, and other multi-asset products.

## Underlying (pages 433–437)

Summary: The Underlying component specifies a single underlying for options and other derivatives. It includes Type (Equity/Fx/Commodity/ConvertibleBond/etc.), Name (underlying name), IdentifierType (type of identifier like RIC/ISIN/WPI), Weight (weight for baskets), PriceType (type of price: Spot/Forward/Future/Discount/Yield), DividendType (dividend type for equities), CreditCurveId (credit curve for credit underlyings), Currency (currency for FX), and CommodityDetails (commodity-specific information). This component is a fundamental building block for many derivative products.

## StrikeData (pages 437–439)

Summary: The StrikeData component specifies strike prices for options with Strike (single strike or schedule of strikes), StrikeType (type of strike: Absolute/Relative/Moneyness/Delta/Variance/Forward/ATMF), and StrikeCurrency (currency for strike if different from underlying). This component handles various strike specifications for different option types and markets.

## Barrier Data (pages 439–441)

Summary: The BarrierData component specifies barrier levels and types for barrier options with Level (single barrier level or schedule), Type (BarrierType: Down/Up/DownUp/DoubleDown/DoubleUp/DoubleBarrier/West/North/South/East/NW/NE/SW/SE), Style (BarrierStyle: American/European/Discrete), and Rebate (rebate amount if barrier not hit). This component handles the various barrier specifications for single and double barrier options.

## RangeBound (pages 441–442)

Summary: The RangeBound component specifies range boundaries for corridor products with LowerBarrier (lower barrier level or schedule), UpperBarrier (upper barrier level or schedule), LowerBarrierType (type of lower barrier), UpperBarrierType (type of upper barrier), LowerRebate (rebate if lower barrier not hit), and UpperRebate (rebate if upper barrier not hit). This component is used for corridor variance swaps and other range-based products.

## Bond Basket Data for Cashflow CDO (pages 442–442)

Summary: The BondBasketDataForCashflowCDO component specifies bond baskets for cashflow CDOs with Attachment (attachment point for losses), Deduction (deduction from losses), TrancheNotional (notional of tranche), and BondBasketName (name of bond basket). This component handles the specific credit enhancement and tranche structure of CDOs.

## CBO Tranches (pages 443–443)

Summary: The CBOTranches component specifies tranches for Collateral Bond Obligations with AttachmentPoint (attachment point for tranche), DetachmentPoint (detachment point for tranche), and Notional (notional amount of tranche). This component defines the loss allocation and subordination structure of CBOs.

## Formula Based Leg Data (pages 444–476)

Summary: The FormulaBasedLegData component enables user-defined formula-based coupon calculations with Formula (formula string for coupon calculation), Variables (list of variables used in formula), FallbackDate (fallback date if calculation fails), and FallbackValue (fallback value if calculation fails). The formula language supports operators (+, -, *, /, ^), functions (max, min, abs, exp, log, sqrt, pow, normal, floor, ceil, if-then-else, sign, etc.), and variable types (Index, FXIndex, Numeric, DayCounter, Calendar, Curve, Coupon, Fixing). This component provides maximum flexibility for customized coupon calculations and structured products.

# Allowable Values (pages 477–487)

Summary: The Allowable Values section lists all permissible values for various parameters used across ORE products. This includes DayCounter conventions (A360/A365/AA365/AA360/Business252/ACT/ACT360/ACT365A/ACT365ISDA/etc.), BusinessDayConventions (F/MF/P/MP/UN/UNE/etc.), Calendars (standard and custom calendars), Compounding methods (Simple/Compounded/Continuous/FlatThenSimple), Frequency frequencies (D/W/M/Q/S/A/Z), FMAIndex names (various FMA indices), IBOR index names (various IBOR indices), OIS index names (various OIS indices), SwapIndex names (various swap indices), Currency codes (ISO 4217), Commodity index names, Equity index names, Inflation index names (CPI and YY), and CreditCurve names. These allowable values ensure proper configuration and validation of product parameters.

# Netting Set Definitions (pages 488–490)

Summary: The Netting Set Definitions section explains how to define netting sets in a separate XML file for exposure calculation and XVA. Each netting set includes NettingSetId (identifier), AgreementType (optional agreement type), and optionally Bilateral (flag for bilateral agreement), and MarginCallDelayIndex (delay index for collateral). The file supports uncollateralized netting sets (no collateral parameters) and collateralized netting sets (with CSA terms). These definitions are used for collateral modeling, exposure calculation, and XVA computations.

## Uncollateralised Netting Set (pages 488–488)

Summary: Uncollateralized netting sets are defined with only NettingSetId and optional AgreementType. They represent trades without collateral agreements, where exposure calculations assume no collateral is posted or received. These are used for uncollateralized derivatives and simple trading relationships.

## Collateralised Netting Set (pages 488–490)

Summary: Collateralized netting sets include CSA parameters for collateral modeling. Elements include BilateralCSA (flag for bilateral agreement), CSAComment (optional comment), CSACurrency (collateral currency), MinimumTransferAmount (minimum transfer amount), Threshold (threshold amount), MarginPeriodOfRisk (MPOR), MarginPeriodOfRiskCount (number of MPOR periods), MarginPeriodOfRiskMultiplier (MPOR multiplier), CalculationType (calculation type for collateral), CollateralCalculationType (collateral calculation method), Index (index for interest on collateral), PayFrequency (payment frequency), ReceiveFrequency (receive frequency), Calendar (calendar for collateral dates), and CollateralFloor (collateral floor flag). These parameters enable detailed modeling of collateral agreements for accurate exposure and XVA calculations.

# Scripted Trade (pages 491–512)

Summary: The Scripted Trade section describes ORE's scripting framework for flexible product definition. Scripted trades use a payoff script language to define custom payoffs beyond standard product types, enabling exotic and hybrid products. The framework supports event-based scripting, various data types (Event, Number, Index, Currency, Daycounter), compact XML format for efficiency, and detailed payoff scripting language with arithmetic, logical, and financial functions. Scripted trades support both Monte Carlo and finite difference pricing methods and can handle path-dependent and early-exercise features.

## General Structure (pages 492–492)

Summary: Scripted trades use ScriptedTradeData as the trade type, containing ScriptedPayoffData (with TradeType, ProductTag, and Script), NumberData (number variables), IndexData (index variables), CurrencyData (currency variables), DayCounterData (daycounter variables), andEventData (event variables). The Script element contains the payoff formula in the scripting language, while other elements define the variables used in the script. This structure allows fully customizable payoff definitions while maintaining compatibility with ORE's pricing infrastructure.

## Data Types (pages 493–500)

Summary: The scripting language supports several data types. Event includes Type (various event types like Fixing/BarrierDetection/AverageObservation/etc.), Dates (date or date range), Level (level for barriers/averages), Barrier (barrier type), Observation (observation type), and Condition (condition for events). Number includes Name (variable name), Value (numeric value), and OptionalValue (optional value). Index includes Name (index name), Type (index type: FX/IR/Equity/Inflation/Commodity/Credit), and IndexName (specific index). Currency includes Name (variable name) and CurrencyCode (ISO currency code). Daycounter includes Name (variable name) and Daycounter (daycount convention). These data types provide the building blocks for complex payoff scripts.

## Compact Trade XML (pages 498–500)

Summary: Compact XML format allows shorter scripted trade definitions by combining variables directly in the script string rather than separate variable elements. Number variables can be defined as "#N(var_name)" and "#N(var_name,value)" in the script. Index variables can be defined as "#I(index_type,index_name)" in the script. Currency variables can be defined as "#C(currency_code)" in the script. This format reduces verbosity while maintaining clarity for complex payoff definitions.

## Payment Currency in Scripted Trades (pages 500–500)

Summary: Scripted trades require careful specification of payment currency. The currency can be specified as an index (FX index), as a currency code (using a currency variable), or directly in the formula using currency conversion functions. This flexibility supports various multi-currency payoff structures and hedging scenarios.

## Payoff Scripting Language (pages 501–512)

Summary: The payoff scripting language provides comprehensive operators and functions for defining custom payoffs. Operators include arithmetic (+, -, *, /, ^), comparison (==, !=, <, >, <=, >=), logical (and, or, !, ?), and assignment (let). Functions include abs, exp, log, pow, sqrt, normal, max, min, if-then-else, sign, floor, ceil, round, time, day, month, year, weekday, daysbetween, isbusinessday, advance, fixings, npv, cashflows, performance, payoff, histfixing, histvalue, histvolatility, histpercentile, calibrate, di, du, da, dp, dc, n, u, a, p, c, opmax, opmin, opsum, sort, quantile, mean, stdev, correlation, regression, discount, forward, atmVol, capFloorPrice, swaptionPrice, fxOptionPrice, fwdFx, fwdBondYield, atmVolatility, capVolatility, swaptionVolatility, fxVolatility, equityVolatility, commodityVolatility, dividendYield, and prob (default probability). This language enables sophisticated payoff definitions including path-dependency, barrier conditions, averaging, and regression-based features.

# Pricing Methodology (pages 513–624)

Summary: The Pricing Methodology section provides detailed descriptions of the pricing models and methods applied to each product type in ORE. For interest rate derivatives, this includes discounted cash flow analysis, curve construction, volatility modeling (Black/SABR for caps/floors, swaption volatilities), and numerical methods (analytical formulas, trees, finite difference, Monte Carlo). For FX and equity derivatives, it includes Black-Scholes models, local volatility, stochastic volatility, and Monte Carlo simulation. For credit derivatives, it includes default curve construction, correlation modeling (Gaussian copula), and tranche pricing. For commodity derivatives, it includes commodity-specific models and seasonality. For exotics and structured products, it includes Monte Carlo simulation, finite difference methods, and regression-based approaches for American Monte Carlo. This section ensures users understand the theoretical foundations of ORE's pricing calculations.

## Interest Rate Derivatives (pages 514–533)

Summary: Interest rate derivative pricing in ORE uses discounted cash flow analysis with appropriate curve construction. For vanilla swaps, FRA, and basis swaps, pricing uses standard discounted cash flow methodology. For cross currency swaps, pricing uses both domestic and foreign discount curves with FX rates. For overnight index swaps, pricing uses overnight index curves with compounding methods (arithmetic or geometric). For zero coupon swaps, pricing uses compounding over the swap tenor. For CMS/CMB swaps, pricing uses CMS/CMB indices derived from the yield curve. For caps/floors, pricing uses Black/SABR models for caplet/floorlet volatilities, with support for forward-looking and backward-looking RFR term rates, backward-looking RFR caplets, and SIFMA caplets. For swaptions, European swaptions use Black/SABR models, while Bermudan/American swaptions use LGM/Hull-White models with trees or finite difference methods. For callable swaps, pricing treats them as a package of a non-callable swap and a physically settled swaption. For CMS spread options, pricing uses various models depending on complexity.

## Foreign Exchange Derivatives (pages 535–540)

Summary: FX derivative pricing in ORE uses Black-Scholes models for vanilla products and more sophisticated models for exotics. FX forwards use forward FX rates from FX curves. FX swaps use spot and forward FX rates. European FX options use Black/SABR models with smile handling. American FX options use Barone-Adesi Whaley approximation. FX barrier options use barrier option models with continuous or discrete monitoring. FX KIKO options use knock-in knock-out combinations. FX digital options use binary payoff models. FX Asian options use average price models. FX variance swaps use realized variance models. The section emphasizes proper handling of volatility surfaces, correlation between FX and interest rates, and settlement conventions.

## Inflation Derivatives (pages 540–542)

Summary: Inflation derivative pricing in ORE uses inflation curve construction and appropriate index fixing. CPI swaps and zero coupon inflation index swaps use CPI index curves with observation lags and interpolation methods. CPI caps/floors use option pricing on inflation index values. Year-on-year inflation swaps use YY index curves. Year-on-year caps/floors use option pricing on YY index values. Pricing accounts for index fixings, seasonality, and the specific index conventions for different regions.

## Equity Derivatives (pages 542–553)

Summary: Equity derivative pricing in ORE uses equity curve construction (spot prices and dividend yields) and volatility surfaces. Equity forwards use forward prices from equity curves. Equity swaps use equity returns vs floating rates. European equity options use Black-Scholes models with dividend yield adjustments. American equity options use Barone-Adesi Whaley or finite difference methods. Equity barrier options use barrier option models. Equity composite options handle quanto effects. Equity digital options use binary payoff models. Equity Asian options use average price models. Equity variance swaps use realized variance models. Equity positions and option positions use spot pricing or standard option pricing. Pricing accounts for dividends (continuous, discrete, or dividend yield curves), volatility surfaces, and correlation between equity and interest rates.

## FX / Equity / Commodity / Rates / Inflation Exotics (pages 554–561)

Summary: Exotic derivative pricing in ORE uses advanced numerical methods. Double digital options use binary payoff models with two conditions. Options contingent on barriers use conditional activation. Autocallables use Monte Carlo simulation with call schedule monitoring. Performance options use Monte Carlo simulation. Cliquet options use forward-starting option models with resetable strikes. Window barrier options use barriers active during specific periods. Generic barrier options use flexible barrier specifications. Best entry options use lookback features. Basket options use multi-asset models with correlation. Worst of basket swaps use minimum of basket performance. Rainbow options use maximum/minimum of multiple assets. Accumulators and decumulators use barrier monitoring with knockout and leverage features. Target redemption forwards use Monte Carlo simulation with cumulative profit tracking. Knock out swaps use barrier monitoring with termination. Strike resettable options use strike adjustment based on conditions. Variance derivatives use sophisticated variance models with corridor features and barriers. The section emphasizes Monte Carlo simulation, finite difference methods, and proper handling of correlation between underlyings.

## Credit Derivatives (pages 562–579)

Summary: Credit derivative pricing in ORE uses credit curve construction and correlation modeling. Credit default swaps use standard CDS pricing with default curves and recovery rates. Asset backed CDS use adjusted default curves. Index CDS use portfolio pricing with default curves. CDS options use option pricing on CDS spreads. Index CDS options use option pricing on index spreads. Synthetic CDOs use Gaussian copula models with correlation, base correlation, or tranche loss distribution models. Calibration of default curves for index tranches uses market tranche spreads. Risk participation agreements use CDS pricing methodology. Credit linked swaps combine CDS and IRS pricing. Pricing accounts for default probabilities, recovery rates, correlation, and the specific features of each credit product.

## Commodity Derivatives (pages 580–598)

Summary: Commodity derivative pricing in ORE uses commodity curve construction (forward curves, futures prices) and volatility surfaces. Commodity forwards use forward prices from commodity curves. Commodity options use Black or Black-Scholes models. Commodity futures options use Black model with futures prices. Commodity swaps use forward curve pricing. Commodity basis swaps use spread between commodity benchmarks. Commodity swaptions use option pricing on commodity swaps. Commodity average price options use average price models. Commodity spread options use spread option models. Commodity calendar spread options use time spread models. Commodity variance swaps use realized variance models. Pricing accounts for seasonality, delivery locations, quality specifications, and the specific features of each commodity market.

## Bond Derivatives (pages 598–605)

Summary: Bond derivative pricing in ORE uses bond curve construction (yield curves, credit spreads) and appropriate models for each product. Forward bonds use forward pricing methodology. Bond total return swaps use bond pricing plus funding costs. Bond options use Black or Hull-White models depending on option type and underlying. Pricing accounts for bond-specific features like callable/putable features, credit spreads, and the specific conventions of each bond market.

## Hybrid Trades (pages 605–608)

Summary: Hybrid trade pricing in ORE combines methodologies from multiple asset classes. Composite trades treat each sub-trade separately with appropriate pricing. Generic total return swaps and contracts for difference use return calculation methodology with funding costs. Pricing accounts for the multi-asset nature of these products and the interactions between different asset classes.

## Cash Products (pages 608–624)

Summary: Cash product pricing in ORE uses discounted cash flow analysis with appropriate curves and models. Bonds use standard bond pricing with yield curves and credit spreads. Bond repos use repo pricing with collateral and haircuts. Convertible bonds use complex models combining equity and credit features, often using finite difference or Monte Carlo methods. Callable bonds use option-adjusted spread models with interest rate trees. ASCOTs use option pricing on bond components. Collateral bond obligations use CDO pricing methodology with loss allocation. Pricing accounts for the specific features of each cash product and the relevant market data.

# Pricing Models (pages 625–630)

Summary: The Pricing Models section provides details on the specific pricing models implemented in ORE. Models include Bachelier (normal model for options on rates), Black and Shifted Black (lognormal models for options), Linear Terminal Swap Rate model LTSR (swaption pricing), Bivariate swap rate model BrigoMercurio (CMS spread options), One-Factor Linear Gauss Markov model LGM (Bermudan/American swaptions, callable bonds), and Barone-Adesi and Whaley (American options approximation). Each model includes specification of volatility surfaces, mean reversion, and other parameters. The section emphasizes proper model selection for each product type and calibration procedures.

# Curve Building (pages 631–638)

Summary: The Curve Building section describes how ORE constructs various curves and surfaces for pricing. For interest rates, this includes discount curves, index curves, and yield curves using various instruments (deposits, FRAs, futures, swaps, OIS, basis swaps). For foreign exchange, this includes FX spot curves and forward curves. For inflation, this includes CPI curves and YY curves using inflation swaps and bonds. For equity, this includes equity spot curves and dividend yield curves. For credit, this includes default probability curves using CDS spreads. For commodity, this includes forward curves using futures and swaps. For volatility structures, this includes cap/floor volatilities (interest rates and inflation), swaption volatilities, FX volatilities, equity volatilities, and commodity volatilities using various models (flat, smile, SABR). The section emphasizes bootstrap methods, interpolation, and consistency across curves.

## Interest Rates (pages 631–634)

Summary: Interest rate curve building in ORE uses bootstrap methodology with various instruments. Discount curves are built from deposits, FRAs, futures, swaps, and OIS. Index curves are built from IBOR and OIS fixings. Yield curves are built from swap rates and government bonds. The section covers single-currency and cross-currency curve construction, basis swap curves, and the handling of different tenors and currencies. Curve construction includes interpolation methods, calendar conventions, and consistency checks.

## Foreign Exchange (pages 634–634)

Summary: FX curve building in ORE includes FX spot curves (for spot rates) and FX forward curves (for forward rates). FX curves are built from FX swaps and forward points. The section covers cross-currency basis swap curves and the relationship between FX curves and interest rate curves (covered interest rate parity).

## Inflation (pages 635–635)

Summary: Inflation curve building in ORE includes CPI curves (for zero coupon inflation) and YY curves (for year-on-year inflation). Curves are built from inflation swaps, inflation-linked bonds, and CPI fixings. The section covers seasonality adjustments, index lags, interpolation methods, and the handling of different inflation indices for various regions.

## Equity (pages 635–635)

Summary: Equity curve building in ORE includes equity spot curves (for spot prices) and dividend yield curves (for forward prices). Spot curves are built from equity prices and futures. Dividend yield curves are built from option prices, dividend futures, and dividend swaps. The section covers the handling of continuous and discrete dividends, as well as dividend projections.

## Credit (pages 636–636)

Summary: Credit curve building in ORE includes default probability curves (hazard rates) and recovery rate curves. Curves are built from CDS spreads, bond spreads, and bond prices. The section covers the bootstrapping of default probabilities, the handling of different seniority levels, and the construction of term structures of default probabilities.

## Commodity (pages 636–636)

Summary: Commodity curve building in ORE includes forward curves (for forward prices) and volatility surfaces. Curves are built from futures prices, swap prices, and options. The section covers seasonality adjustments, delivery location differences, quality specifications, and the handling of various commodity types (energy, metals, agricultural).

## Volatility Structures (pages 636–638)

Summary: Volatility structure building in ORE includes cap/floor volatilities for interest rates (using Black or SABR models), swaption volatilities (using Black or SABR models), FX volatilities (using Black, Vanna-Volga, or SABR models), inflation cap/floor volatilities (for CPI and YY), equity volatilities (using Black, local volatility, or stochastic volatility models), and commodity volatilities (using Black or other models). The section covers volatility surface construction, interpolation methods, smile handling, and the calibration of various volatility models.

# Libor Fallback (pages 639–640)

Summary: The Libor Fallback section describes ORE's handling of the transition from IBOR rates to risk-free rates (RFR). The baseline approach uses fallback spreads defined in conventions. Standard Libor coupon pricing applies fallback adjustments to legacy IBOR positions. Non-standard instrument pricing uses appropriate fallback methodology for various products. Sensitivity analysis includes fallback spread sensitivities. The section ensures ORE properly handles the IBOR transition and related fallback calculations.

# Pricing Engine Configuration (pages 640–741)

Summary: The Pricing Engine Configuration section provides detailed XML configuration specifications for each product type's pricing engine. Each product type has its own pricing engine parameters including model parameters (volatility type, mean reversion, etc.), engine parameters (time steps, grid settings, etc.), and instrument-specific parameters. The section covers over 90 product types including Ascot, Bond, BondOption, CallableBond, ConvertibleBond, CreditLinkedSwap, various swaption types (European/Bermudan/American with various features), various cap/floor types, commodity products, credit products, equity products, FX products, variance swaps, and scripted trades. Global parameters apply across all engine types and include numerical parameters, convergence criteria, and optimization settings. This comprehensive configuration ensures proper pricing for all supported products with appropriate models and numerical methods.

## Global Parameters (pages 735–741)

Summary: Global parameters apply across all pricing engines and include numerical parameters (grid density, time steps, optimization settings), convergence criteria (tolerance, maximum iterations), and optimization settings. These parameters ensure consistent and accurate pricing across different product types and models. The section provides guidance on appropriate parameter values for various scenarios and products.
