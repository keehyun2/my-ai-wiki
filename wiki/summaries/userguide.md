---
doc_type: pageindex
full_text: sources/userguide.json
---

# Preface (pages 1–9)

Summary: The partial document is the ORE User Guide dated 30 January 2026. It covers a comprehensive document history from 2016 to 2026, detailing releases and changes by Quaternion, Acadia, and LSEG. The table of contents outlines the guide's structure, including introduction, ORE data flow, building ORE, extensive examples (covering curve building, market risk, initial margin, exposure, netting sets, scripted trades, American Monte Carlo, XVA risk, credit risk, performance, ORE-Python/API), parameterisation (analytics, market data, simulation, sensitivity, stress, curves, reference data, IBOR fallback, SIMM calibration, conventions, historical returns), collateral balances, counterparty information, netting set definitions, market data types, fixing history, and dividends history. The introduction explains ORE's purpose as an open-source risk engine for pricing and risk analysis, targeting quantitative risk practitioners, and acknowledges contributions from Quaternion, Acadia, and LSEG.

# Introduction (pages 9–10)

Summary: The partial document introduces the Open Source Risk Project and its main software, Open Source Risk Engine (ORE), which provides a Monte Carlo simulation framework for risk analytics and value adjustments. It outlines the target audience, including risk management practitioners, quant developers, and academics. The document also details project sponsorship history from Quaternion Risk Management, Acadia, and LSEG, and invites community contributions. The scope section covers ORE's capabilities: portfolio pricing, cash flow generation, exposure measures (EE, ENE, Basel, PFE), derivative value adjustments (CVA, DVA, FVA, COLVA, MVA), market risk analytics (sensitivity, stress testing, VaR methods, P&L), and recent instrument extensions such as Equity/FX exotics, commodity products, and credit products.

## Scope (pages 10–12)

Summary: The partial document covers the scope and capabilities of the Open Source Risk Engine (ORE), including portfolio pricing, cash flow generation, market risk analysis, exposure measures (EE, ENE, Basel measures, PFE), and derivative value adjustments (CVA, DVA, FVA, COLVA, MVA). It details the market risk framework (sensitivity, stress testing, parametric and historical VaR, P&L explain). The document outlines ORE's product coverage expansions across quarterly releases (v7–v12), adding equity/fx exotics, commodities, credit, bonds, hybrids, scripted trades, and other instruments. Recent analytics additions include XVA Risk, regulatory capital (SA-CCR, BA-CVA, SA-CVA), and dynamic SIMM using algorithmic differentiation. Simulation models are described (cross-currency with LGM, lognormal FX/EQ, Hull-White). Finally, it covers ORE's Python/Java bindings via SWIG, with pip installation and repository structure changes.

## ORE in Python or Java (pages 12–13)

Summary: The partial document covers the following main points: a table listing various financial products (e.g., bonds, swaps, options, inflation products, credit derivatives) and their support for pricing/cashflows, sensitivity analysis, stress testing, and exposure simulation/XVA; an explanation of ORE's availability in Python and Java via SWIG bindings and pip installation; a roadmap outlining future development plans for regulatory capital analytics (SA-CCR, BA-CVA, FRTB-SA), performance enhancements using AAD and GPUs, expansion of the Python wrapper, and a proof-of-concept REST API service; and a list of further resources (project site, GitHub, FAQs, documentation, YouTube channel) along with the organization of the document.

## Roadmap (pages 13–13)

Summary: The partial document covers the roadmap for ORE, including community-driven growth, planned expansion of regulatory capital analytics (SA-CCR, BA-CVA, FRTB-SA), performance enhancements via AAD and GPU parallelization, extended Python wrapper coverage, and a proof-of-concept RESTful API service. It also lists further resources such as the Open Source Risk project site, source code repository, FAQs, Twitter, product catalogue, methodology, and YouTube academy, along with a note on the document's organization.

## Further Resources (pages 13–14)

Summary: The partial document covers the ORE roadmap, including community-driven growth, expansion of regulatory capital analytics (SA-CCR, BA-CVA, FRTB-SA), performance enhancements via AAD and GPU parallelization, development of the ORE Python wrapper, and a RESTful API proof-of-concept. It then lists further resources (project site, source code, FAQs, Twitter, product catalogue, methodology, YouTube academy). Section 2 introduces the ORE data flow, detailing three core processing steps: portfolio loading/curve building/model calibration, followed by pricing/market simulation/forward pricing, and finally aggregation/collateral modeling/exposure analytics. It describes inputs (trade data, market data, configuration XML) and outputs (NPV, cash flow, exposure, XVA reports) and notes the interactive visualization of exposure and NPV distributions.

# ORE Data Flow (pages 14–15)

Summary: The partial document covers two main sections: the ORE data flow, detailing three core processing steps (portfolio loading, curve building, model calibration; pricing, simulation, and NPV cube generation; aggregation, collateral modeling, and XVA computation), and instructions for obtaining and building ORE, including release archives and source code access.

# Getting and Building ORE (pages 15–15)

Summary: The partial document describes a processing step that generates reports (NPV, cashflows) and an NPV cube, which is written to binary and text formats. The third processing step performs risk analysis by aggregating trades, applying collateral rules, and computing XVAs (CVA, DVA, FVA, MVA) with optional trade-level allocation. Outputs include XVA reports and a net NPV cube. It then covers how to obtain and build ORE, including downloading release bundles or checking out source code from GitHub, with options for pre-built Python modules or automatic builds. Instructions for ORE releases are provided, including source code archives and additional PDF documentation.

## ORE Releases (pages 15–16)

Summary: The partial document describes a processing step that generates an NPV cube and performs sophisticated risk analysis, including aggregation over netting sets, collateral rules, and computation of XVAs (CVA, DVA, FVA, MVA). It then explains how to obtain and build the ORE (Open Source Risk Engine) source code, either by downloading release archives or cloning the Git repository, and lists the directory structure of a release.

## Access via Git (pages 16–17)

Summary: The partial document covers the directory structure of the ORE repository, notes that each release includes the dependent QuantLib version, instructions for accessing the code via Git (cloning, submodules, and checking out specific releases), and the prerequisites for building ORE from source, including required tools such as a C++ compiler, Boost, CMake, and optional tools, with platform-specific guidance for Windows, Linux, and macOS.

## Prerequisites for Building ORE (pages 17–20)

Summary: The partial document covers the following main points:

- Instructions for cloning the ORE repository using Git submodules or the `--recurse-submodules` option, including how to checkout a specific release tag.
- Prerequisites for building ORE from source: C++ compiler (Visual Studio on Windows, gcc on Linux, clang on macOS), Boost libraries (version 1.75.0 or later), CMake, optional Ninja and zlib, Eigen, Swig, and Python (latter two for the Python module).
- Detailed installation steps for Boost on Linux/macOS (using apt or homebrew) and Windows (pre-compiled binaries or compiling from source with Visual Studio tools).
- A table of supported compiler and Boost version combinations for ORE v13.
- Optional tools: Ninja (for faster builds) and zlib (for compression), with installation guidance including VCPKG on Windows.
- Requirements for Eigen, Swig, and Python for building the ORE Python module.
- The CMake build system with a table of essential parameters (options like ORE_BUILD_DOC, ORE_BUILD_TESTS, ORE_USE_ZLIB, etc.) and hints for configuring Boost and Python paths if not automatically found.

## Building ORE (pages 20–22)

Summary: The partial document covers the prerequisites and build process for ORE (Open Source Risk Engine). It explains the need for Eigen libraries for Credit Risk analytics and installation via VCPKG on Windows, as well as SWIG and Python for building the ORE Python module. It details the CMake build system with essential parameters and their defaults, followed by step-by-step build instructions for Linux/macOS and Windows (including Visual Studio 2019/2022 and command line). Finally, it addresses building ORE Python wheels for distribution and typical usage.

## Building ORE Python Wheels (pages 22–23)

Summary: The partial document covers building ORE on Windows with MSVC using CMake (generating project files and building via command line or Visual Studio), building ORE Python wheels via setup.py and GitHub workflows, the experimental ORE Python integration feature (prerequisites and usage), and an overview of over 80 ORE examples grouped by topic.

## ORE with Python Integration (pages 23–23)

Summary: The partial document covers two main topics: (1) An experimental ORE feature for Python integration, allowing calls to Python functions (e.g., regression from scikit-learn or py-earth2) to avoid C++ implementation, with prerequisites for building and configuring the environment. (2) An overview of over 80 ORE examples grouped by topic, with reference to Table 3 and the examples folder structure corresponding to the User Guide sections.

# Examples (pages 23–25)

Summary: The partial document covers two main topics: 
- **ORE with Python Integration** (section 3.6): Describes an experimental feature allowing ORE to call Python functions (e.g., regression methods from scikit-learn and py-earth2) to avoid C++ implementation. Lists prerequisites: building ORE with ORE_PYTHON_INTEGRATION, setting Python_ROOT and Python_LIBRARY in cmake, and extending PYTHONPATH. References a Jupyter notebook demonstration.
- **Examples** (section 4): Overview of over 80 ORE examples grouped by topic (e.g., Academy, Products, Curve Building, Market Risk, Initial Margin, Exposure, XVA, Credit Risk, Performance, ORE-Python, ORE-API). Describes how examples are run via Python scripts and input files (ore.xml, portfolio.xml, etc.). Lists typical output files (e.g., npv.csv, flows.csv, curves.csv, exposure reports, PDF graphs). Mentions testsuites for QuantLib, QuantExt, OREData, and OREAnalytics.

## Testsuites (pages 25–26)

Summary: The partial document describes how to run ORE examples using Python scripts, lists the required input files (e.g., ore.xml, portfolio.xml, netting.xml) and their descriptions, and details the typical output files (e.g., npv.csv, flows.csv, xva.csv, exposure reports, PDF graphs). It also covers notes on building ORE for Windows, the test suites for QuantLib/QuantExt/OREData/OREAnalytics, the need for Python 3, and three specific example sections: Academy (demo cases from YouTube), Minimal Setup (vanilla swap exposure with minimal market data), and Products (150+ sample trades across asset classes with valuation batch configuration and analytics including npv, cashflow, and portfolioDetails).

## Academy (pages 26–26)

Summary: The partial document covers the following main points: instructions for running tests with `ctest`, a requirement for Python 3, a reference to ORE Academy videos, a minimal setup example for vanilla swap exposure simulation, a products example with over 150 sample trades across asset classes and configuration for valuation, and details on selected analytics (NPV, cashflow, portfolioDetails) with XML configuration.

## Minimal Setup (pages 26–26)

Summary: The partial document describes how to run tests using the `ctest` command, highlights the need for Python 3, and outlines several example setups: the Academy section referencing tutorial videos, a Minimal Setup for swap exposure simulation using minimal market data, and a Products section containing 150+ sample trades across asset classes with configuration and market data. It also details the analytics configuration in `ore.xml`, including NPV, cashflow, and portfolioDetails analytics.

## Products (pages 26–27)

Summary: The partial document covers sections 4.2 to 4.5.1 of an ORE (Open Source Risk Engine) guide. It begins with a command for running tests (`ctest -C Release -j4 –timeout 3600`), a note on Python 3 requirement, and an Academy section linking to YouTube videos. Section 4.3 (Minimal Setup) demonstrates a minimal market data setup for a vanilla swap exposure simulation. Section 4.4 (Products) describes 150+ sample trades across asset classes, a valuation batch configuration, and analytics (NPV, cashflow, portfolioDetails) that produce output files like counterparties.csv and riskFactors.csv. Section 4.5 (Curve Building) lists multiple curve building examples (bootstrap consistency, discount ratio, fixed-vs-float cross currency, USD-Prime, bond yield shifted, central bank dates, SABR volatilities). Subsection 4.5.1 (Bootstrap Consistency) explains verifying bootstrapped curves with three discounting setups (EUR collateral, USD collateral, in-currency OIS) and generating portfolio files via `TradeGenerator.py`.

## Curve Building (pages 27–27)

Summary: The partial document covers:
- The reporting of portfolio composition in a series of extra files (counterparties.csv, marketObjects.csv, netting_sets.csv, riskFactors.csv, swap_indices.csv, trade_types.csv, underlying_indices.csv) stored in the Products/Output folder.
- An overview of curve building cases (Bootstrap Consistency, Discount Ratio Curves, Fixed vs Float Cross Currency Helpers, USD-Prime Curve Building, Bond Yield Shifted Curves, Central Bank Meeting Dates, SABR Swaption and Cap/Floor Volatilities) with commands to run them.
- A detailed section on Bootstrap Consistency, which validates bootstrapped curves repricing bootstrap instruments (FRAs, Interest Rate Swaps, FX Forwards, Cross Currency Basis Swaps) under three pricing setups (EUR collateral discounting, USD collateral discounting, in-currency OIS discounting), requiring generation of portfolio files from market data and trade templates via a TradeGenerator.py script.

### Bootstrap Consistency (pages 27–28)

Summary: The partial document describes several curve building cases in a financial software system, including output files in a Products/Output folder (such as counterparties.csv, marketObjects.csv, etc.) and detailed examples: Bootstrap Consistency (verifying that bootstrapped curves correctly reprice instruments with three discounting setups), Discount Ratio Curves (building a GBP collateralized in EUR curve using discount ratios), Fixed vs Float Cross Currency Helpers (building a TRY collateralized in USD curve using fixed vs float cross currency swaps), and USD-Prime Curve Building (building a USD-Prime yield curve from basis swap quotes). Each section provides instructions for running the corresponding Python scripts and expected results (e.g., zero NPVs).

### Discount Ratio Curves (pages 28–28)

Summary: The document covers curve building examples, including a consistency check at the Examples/CurveBuilding level (yielding zero NPVs), discount ratio curves for constructing a GBP-in-EUR curve using three reference curves, fixed vs. float cross currency swap helpers for building a TRY-in-USD curve, and USD-Prime curve building from basis swap quotes, each with associated run commands and portfolio verification.

### Fixed vs Float Cross Currency Helpers (pages 28–28)

Summary: The partial document covers several curve building examples in ORE. Key points include: a consistency check that produces zero NPVs for benchmark instruments; an example building a GBP collateralized in EUR discount curve using discount ratios from three other curves; an example using fixed vs. float cross currency swap helpers to build a TRY collateralized in USD curve; and an example building a USD-Prime yield curve from basis swaps with two fair basis swaps.

### USD-Prime Curve Building (pages 28–29)

Summary: The partial document describes several curve building examples in the ORE framework, each with specific use cases and execution instructions. It covers: (1) Discount Ratio Curves – building a GBP collateralized in EUR discount curve using a discount ratio segment and referencing three other curves; (2) Fixed vs Float Cross Currency Helpers – using fixed vs. float cross currency swap helpers to build a TRY collateralized in USD curve; (3) USD-Prime Curve Building – constructing the USD-Prime yield curve from basis swap quotes and verifying the 3% rule relative to Fed Funds; (4) Bond Yield Shifted Curves – shifting a yield curve based on bond prices and cross-checking zero bond NPVs; (5) Central Bank Meeting Dates – building a GBP OIS curve using MPC Swaps with specific forward start/end dates; (6) SABR Volatility Surfaces – pricing swaptions and caps on volatility surfaces interpolated with SABR model flavors. Each example includes commands to run and expected outputs (e.g., zero NPVs, curves.csv files).

### Bond Yield Shifted Curves (pages 29–29)

Summary: The partial document covers several curve building and volatility surface examples: the bootstrapping of USD-FedFunds and USD-Prime curves following the 3% rule, a bond yield shifted curve example using three specific bonds, a central bank meeting dates example for a GBP OIS curve with MPC swaps, and a SABR volatility surfaces example for pricing swaptions and caps with various SABR interpolation types.

### Central Bank Meeting Dates (pages 29–29)

Summary: The partial document covers the following main points:

- Confirmation that bootstrapped USD-FedFunds and USD-Prime curves follow the market's "3% rule" (U.S. Prime Rate = Fed Funds Target Rate + 3%), with a reference to a market source.
- A demonstration of building a Bond Yield Shifted Curve (USD.BMK.GVN.CURVE_SHIFTED) using three specific liquid bonds, with output in curves.csv and cross-checking ZeroBond prices against the curve.
- An example of building a GBP OIS curve using MPC Swaps at the short end, incorporating concrete forward start and end dates (Central Bank Meeting Dates).
- An example demonstrating pricing of a Swaption and a Cap using SABR volatility surfaces, with supported SABR interpolation types (Hagan2002Lognormal, Hagan2002Normal, Hagan2002NormalZeroBeta, Antonov2015FreeBoundaryNormal).

### SABR Volatility Surfaces (pages 29–30)

Summary: The partial document covers several curve building examples, including the USD-Prime curve following the Fed Funds rate plus 3% rule, bond yield shifted curves using specific bonds, a GBP OIS curve using MPC Swaps, and SABR volatility surfaces for swaptions and caps. It also introduces the Market Risk section, detailing sensitivity analysis, parametric VaR, stress testing, historical simulation VaR, P&L explanation, and various utility scripts.

## Market Risk (pages 30–30)

Summary: The partial document covers the calibration or external provision of SABR parameters for options, and then focuses on market risk analytics, listing various sensitivity, VaR, stress testing, and utility scripts. It specifically details a sensitivity analysis example for a portfolio containing swaps, cross-currency swaps, FX forwards and options, swaptions, caps, and floors.

### Sensitivity Analysis (pages 30–33)

Summary: The partial document covers market risk analytics, focusing on sensitivity analysis, stress testing, Value-at-Risk (VaR), and related utilities. It details SABR parameter calibration, a collection of Python scripts for various market risk calculations (e.g., sensitivity, parametric VaR, stress testing, historical simulation VaR, P&L explanation), and a comprehensive example of sensitivity analysis (section 4.6.1) for a diverse portfolio including swaps, FX options, swaptions, caps/floors, bonds, equities, inflation swaps, and CDS. The sensitivity analysis computes first- and second-order derivatives (raw domain) for discount curves, forward curves, FX, swaption/caplet vegas, credit curves, equity, and inflation, followed by conversion to the par domain via Jacobi transformation, with XML configuration details. Section 4.6.2 extends sensitivity analysis to pricing with smile, using two market configurations (ATM only vs. full surface) for equity, swaption, and FX options, and notes limitations on strike-specific sensitivities.

### Sensitivity Analysis and Pricing with Smile (pages 33–34)

Summary: The partial document covers the following main points:

- Configuration of discount curves, instruments, single curve flags, and conventions for GBP and EUR-USD curves.
- A note that par sensitivity analysis requires matching shift tenor grids between sensitivity data and simulation configuration.
- Sensitivity analysis and pricing with smile: example using a portfolio of equity call/put options, a receiver swaption, and an FX call option; two configurations (ATM only and full surface) for simulation and sensitivity; output files.
- Parametric VaR: calculation based on sensitivity/cross gamma output and an external covariance matrix; results broken down by portfolio, risk class, and risk type; Delta Gamma Normal VaR and Monte Carlo VaR alternatives.
- Correlation: calculation based on an external scenario matrix; output showing correlation between risk factor keys.
- Stress testing: two stress tests (parallel_rates and twist) applied to the same portfolio; output includes base NPV, NPV under shifts, and differences.
- Stress testing in the par domain: extended framework that operates in the par rate domain without requiring user manipulation of input market data.

### Parametric VaR (pages 34–34)

Summary: The partial document covers four main topics: Parametric VaR calculation using sensitivities and covariance matrix, with results broken down by portfolio, risk class, and risk type; Correlation calculation based on external scenario matrix input; Stress Testing using predefined scenarios (parallel_rates and twist) on a portfolio, outputting base NPV, shifted NPV, and differences; and Stress Testing in the Par Domain, which allows configurable stress testing in the par rate domain without manually altering market data.

### Correlation (pages 34–34)

Summary: The main points covered in this partial document are:

- **Parametric VaR (section 4.6.3)**: Demonstrates a parametric VaR calculation using sensitivity outputs (deltas, vegas, gammas, cross gammas) and an external covariance matrix. Results are broken down by portfolio, risk class, and risk type, showing Delta Gamma Normal VaRs for 95% and 99% quantiles, with an option for Monte Carlo VaR.

- **Correlation (section 4.6.4)**: Demonstrates a correlation calculation based on an external scenario matrix input, outputting correlations between risk factor keys.

- **Stress Testing (section 4.6.5)**: Uses the same portfolio as sensitivity analysis. Defines two stress tests (`parallel_rates` and `twist`) with specific shifts to rates, FX, and vols. Output includes base NPV, NPV under shifts, and differences per trade and scenario.

- **Stress Testing in the Par Domain (section 4.6.6)**: Extends stress testing to operate in the “par” rate domain (e.g., swap rates, CDS spreads, flat vols) without manually manipulating input market data, allowing configurable analysis of market rate shifts.

### Stress Testing (pages 34–34)

Summary: The partial document describes several financial risk analysis examples: 
- Parametric VaR calculation using sensitivities and covariance matrix, with results broken down by portfolio, risk class, and risk type, and an option for Monte Carlo VaR.
- Correlation calculation from an external scenario matrix, showing correlations between risk factor keys.
- Stress testing using a portfolio with defined stress scenarios (parallel_rates and twist), outputting base NPV, scenario NPV, and differences per trade.
- Stress testing in the par domain, which allows applying market rate shifts without modifying input market data, as an extension of the raw domain stress testing.

### Stress Testing in the Par Domain (pages 34–35)

Summary: The document covers several financial risk analysis examples: 
- **Parametric VaR** (Section 4.6.3): calculates Delta Gamma Normal VaR using sensitivities and covariance matrix, with breakdowns by portfolio, risk class, and risk type; supports Monte Carlo VaR as an alternative.
- **Correlation** (Section 4.6.4): computes correlations between risk factor keys from an external scenario matrix.
- **Stress Testing** (Section 4.6.5): applies predefined stress scenarios (parallel rates, twist) to a portfolio and outputs base NPV, stressed NPV, and differences per trade and scenario.
- **Stress Testing in the Par Domain** (Section 4.6.6): extends stress testing to operate directly in the par rate domain without manual market data manipulation.
- **Stressed Sensitivity Analysis** (Section 4.6.7): combines stress scenarios with sensitivity analysis, replacing today’s market with a simulation market; supports only zero-domain sensitivities.
- **Historical Simulation VaR** (Section 4.6.8): calculates VaR using historical market scenarios, with configurable parameters for output granularity, observation periods, MPOR settings, and simulation market structure.

### Stressed Sensitivity Analysis (pages 35–35)

Summary: The document covers two main topics:

1. **Stressed Sensitivity Analysis** (Section 4.6.7): Introduces a new analytic type `SENSITIVITY_STRESS` that combines stress testing with sensitivity analysis. It applies stress scenarios to the T0 market, replaces the `todaysMarket` with a `SimulationMarket` during calculations, and currently supports dependent sensitivity analysis only in the zero domain for all asset classes. Recommendations include using `UseSpreadedTermStructures` and simulating `SwaptionVolatilities`.

2. **Historical Simulation VaR** (Section 4.6.8): Demonstrates a historical simulation VaR calculation using externally provided market scenarios. Key parameters include output file format, trade-level vs. portfolio-level breakdown, risk factor breakdown, quantiles, portfolio filter, historical observation periods (defined by date pairs), `mporDays` for scenario spacing, calendar, overlapping vs. consecutive periods, and a simulation configuration file for market structure.

### Historical Simulation VaR (pages 35–36)

Summary: The partial document covers four main topics:

- **Stressed Sensitivity Analysis**: Demonstrates using the `SENSITIVITY_STRESS` analytic type, which applies stress scenarios to the T0 market and runs sensitivity analysis. It uses the existing stress test framework and replaces the current market with a simulation market. Dependent sensitivity analysis is supported only in zero domain for all asset classes.

- **Historical Simulation VaR**: Demonstrates a historical simulation VaR calculation using external market scenarios. Details the required parameters in `ore.xml`, including output file, trade P&L breakdown, risk factor breakdown, quantiles, portfolio filter, historical observation periods, MPOR settings, simulation configuration, and scenario file format.

- **SMRC - Basic Market Risk Capital**: Mentioned briefly, referencing the script `run_smrc.py` for calculating basic market risk capital under the Standardized Measurement Method (SMRC).

- **P&L and P&L Explain**: Demonstrates P&L and P&L explain analytics using a simple test portfolio of two single-leg swaps. Describes the output report columns (e.g., NPV at different times, theta, clean/dirty P&L) and the explainer output that attributes P&L to sensitivities and market moves, requiring a sensitivity.xml file.

### SMRC - Basic Market Risk Capital (pages 36–36)

Summary: The partial document covers three main topics: the specification of a historical scenario file (CSV) for market scenarios, including granularity and representation of yield curve tenors as discount factors; an introduction to the SMRC (Standardized Market Risk Capital) basic example run with `run_smrc.py`; and a detailed description of a P&L and P&L Explain example (`run_pnlexplain.py`) using a test portfolio of two single-leg swaps. The P&L example lists the columns in the output `pnl.csv` (TradeId, Maturity, StartDate, EndDate, NPV values, PeriodCashFlow, Theta, HypotheticalCleanPnL, CleanPnL, DirtyPnL, Currency) and mentions additional reports: four NPV reports, four related results reports, and two market scenario reports. The P&L Explain analytic produces `pnl_explain.csv`, includes the Pnl analytic as dependent, and requires a `sensitivity.xml` input.

### P&L and P&L Explain (pages 36–37)

Summary: The partial document covers three main topics: the specification of a historical scenario file for market simulations, the P&L and P&L explain analytics for a simple swap portfolio, and a stand-alone utility for converting zero sensitivities to par sensitivities using a Jacobi transformation. Key details include required CSV column formats, output reports, and configuration parameters.

### Stand-alone Par Conversion Utility (pages 37–38)

Summary: The partial document covers two main topics: the Stand-alone Par Conversion Utility (section 4.6.11) and the Base Scenario Utility (section 4.6.12). The Par Conversion Utility demonstrates converting zero sensitivities (e.g., zero rates) to par sensitivities (e.g., swap rates) using a Jacobi transformation, with detailed configuration requirements in ore.xml, including input file columns and sensitivity.xml ParConversion data blocks for various discount curves. The Base Scenario Utility exports the simulation market’s base scenario as a file, used internally in P&L analytics and for extracting historical scenarios.

### Base Scenario Utility (pages 38–39)

Summary: The partial document covers several main points: the baseNpvColumn definition and the Jacobi transformation to par sensitivities, controlled by ParConversion data blocks in sensitivity.xml, with examples for EUR, USD, and GBP discount curves showing different instrument types and conventions. It notes that par sensitivity analysis requires matching shift tenor grids with the simulation configuration. Sections 4.6.12 and 4.6.13 describe utilities for base scenario export and zero-to-par shift conversion. Section 4.7 introduces initial margin, focusing on ISDA SIMM (versions 1.0 to 2.6) and IM Schedule, including support for 1d and 10d MPoR horizons, CRIF input, and example output with breakdown by product class, risk class, and margin type.

### Zero Shift to Par Shift Conversion Utility (pages 39–39)

Summary: The partial document covers two main topics: 
- **Zero Shift to Par Shift Conversion Utility** (section 4.6.13): Demonstrates converting zero rate shifts to par rate shifts using ORE, where zero shifts are applied to zero curves to compute implied fair rate shifts for par instruments, used internally in the par-sensitivity-based P&L explainer.
- **Initial Margin** (section 4.7): Introduces two groups: ISDA SIMM and IM Schedule, and a Dynamic Initial Margin case study. Subsection 4.7.1 details ISDA SIMM calculation using an example script (`python run_simm.py`) with a CRIF sensitivity file. It lists supported SIMM versions (1.0 to 2.6), confirms testing against ISDA unit test suites, notes MPoR horizons for versions ≥2.2, and describes the output report (`simm.csv`) with breakdowns. The example runs SIMM versions 2.4 and 2.6 for 1-day and 10-day MPoR.

## Initial Margin (pages 39–39)

Summary: The partial document covers two main topics:

1. **Zero Shift to Par Shift Conversion Utility**: Demonstrates conversion of zero rate shifts to par rate shifts using `python run_zerotoparshift.py`. ORE applies zero rate shifts to zero curves and computes resulting shifts in implied fair rates of par instruments. Used internally for par-sensitivity-based P&L explainer.

2. **Initial Margin**: Includes two groups: ISDA SIMM and IM Schedule, and a Dynamic Initial Margin case study.  
   - **ISDA SIMM and IM Schedule**: Example `python run_simm.py` calculates initial margin using ISDA SIMM based on a CRIF sensitivity file. ORE supports all SIMM versions from 1.0 to 2.6, tested against ISDA unit tests. For versions ≥2.2, supports both 1-day and 10-day MPoR. The example uses a CRIF file (`Input/crif.csv`) and generates a SIMM report (`simm.csv`) with breakdown by product class, risk class, margin type, bucket, and SIMM side. SIMM calculations shown for versions 2.4 and 2.6 with 1-day and 10-day MPoR.

### ISDA SIMM and IM Schedule (pages 39–41)

Summary: The partial document covers the following main points:

- **Section 4.6.13: Zero Shift to Par Shift Conversion Utility** – Demonstrates conversion of zero rate shifts to par rate shifts using ORE, with zero shifts defined as stresstests and par instruments defined in sensitivity configuration, used internally for par-sensitivity-based P&L explainer.

- **Section 4.7: Initial Margin** – Introduces two groups: ISDA SIMM & IM Schedule, and a Dynamic Initial Margin case study.

- **Section 4.7.1: ISDA SIMM and IM Schedule** – Details calculation of initial margin using ISDA SIMM (versions 1.0 to 2.6) based on CRIF file input, with support for MPoR horizons (1d and 10d); also covers the IM Schedule method requiring CRIF lines for NPV and notional per trade, with product classes (Rates, FX, Equity, Credit, Commodity) and minimal configuration.

- **Section 4.7.2: Dynamic Initial Margin and MVA** – Presents Dynamic Initial Margin calculations for five basic products (EUR swap, European swaption, USD swap, cross-currency swap, FX option), with visualization of expected DIM evolution over time using various regression methods (simple, zero-order, first-order, second-order).

### Dynamic Initial Margin and MVA (pages 41–42)

Summary: The partial document covers Dynamic Initial Margin (DIM) and MVA calculations for several derivative products (EUR swap, European swaption, USD swap, EUR/USD cross-currency swap, EUR/USD FX option). It describes visualization of expected DIM evolution and regression plots, and explains four Initial Margin projection methods: Simple (99% quantile), Zero Order Regression (scaled standard deviation), First/Second Order Regression (conditional variance regression), and Dynamic Delta VaR. It also introduces a prototype Dynamic SIMM implementation in section 4.7.3, referencing input files and analytic configuration.

### Dynamic SIMM (pages 42–45)

Summary: The partial document covers several key topics related to Dynamic Initial Margin (DIM) calculations and exposure simulation. It presents regression snapshot figures (zero, first, and second order) for EUR swap and swaption at time step 100, and shows the evolution of expected DIM for various instruments (EUR swap, EUR swaption, EUR/USD FX option) using regression models and Dynamic Delta VaR. It introduces a prototype "Dynamic SIMM" method embedded in AMC simulation, which uses Algorithmic Differentiation to generate sensitivities along paths. Validation of the new method against a conventional SIMM calculator is shown for both zero volatility (single path) and non-zero volatility (multiple paths), with performance benchmarks indicating a significant speedup. The document also begins a section on exposure simulation and CVA for uncollateralized single trades, listing examples for swaps, FRAs, and other vanilla products.

## Netting Set Exposure and Collateral (pages 65–65)

Summary: The partial document describes exposure calculation and XVA for a small netting set of three swaps, illustrating the effect of collateral choices on exposure. It covers: the use of a biweekly Margin Period of Risk (MPoR) grid; results from ORE runs with different collateral parameters (no collateral, threshold with MTA, zero threshold); explanation of exposure spikes caused by cash flows during MPoR; and the summary of XVA components (CVA, DVA, FVA, COLVA, MVA, Collateral Floor) in an output file.

### MPoR (Biweekly) Grid (pages 65–68)

Summary: The partial document covers netting set exposure and collateral modeling for a small portfolio of three swaps in different currencies. It demonstrates exposure calculation and XVA under various collateral arrangements, including no collateral, collateral with threshold and minimum transfer amount, and zero threshold. Key topics include the Margin Period of Risk (MPoR) biweekly grid, the cause of exposure spikes due to cash flows during the MPoR, and the "Classical+" collateral model used. It details XVA outputs (CVA, DVA, FVA, COLVA, MVA, Collateral Floor) in a summary table and explains exposure reports with EPE, ENE, PFE, and Basel measures. The section also covers allocation of netting set exposure and XVA to individual trades using the marginal (Euler) allocation method, showing both uncollateralized and collateralized cases with allocated exposure graphs. Finally, it introduces a close-out grid alternative for handling MPoR using uneven time steps.

### Close-out Grid (pages 68–70)

Summary: The partial document covers exposure allocation without and with collateral for example swaps (Figures 32 and 33), describing allocated EPE profiles and XVAs. It then introduces the close-out grid methodology (Section 4.9.2) for modelling the Margin Period of Risk, including two calculation modes (sticky date and actual date), and presents results comparing uncollateralized, variation-margin-only, and VM+initial margin exposures (Figures 34-36). Finally, it mentions a first MPoR adjustment example (Section 4.9.3).

### First MPoR Adjustment (pages 70–71)

Summary: The partial document covers figures illustrating swap exposure with variation margin (VM) and initial margin (IM) under different netting sets and MPOR settings, including a comparison of expected IM from regression vs Delta VaR. It then describes the first MPoR adjustment for collateral balances in XVA calculations, using a flag to carry over differences during the first MPoR period as a conservative measure. Finally, it introduces the scripted trade module in ORE for representing exotic products (e.g., equity options, barrier options) with hybrid payoffs and path-dependence, demonstrating its use with analytical, Monte Carlo, and finite difference pricing through a series of example trades.

## Scripted Trade (pages 71–72)

Summary: The partial document covers two main topics:

1. **Scripted Trade (Section 4.10)**: A new ORE module for flexible representation of exotic products with hybrid payoffs, path-dependence, and early termination options. It supports Monte Carlo and Finite Difference pricing, with GPU parallelism and AD methods. An example folder demonstrates eight trades (vanilla European options, barrier options, equity accumulators) represented as standard XML, generic scripted trades, and compact scripted trades, using analytical, MC, and FD pricing. Notes highlight pricing deviations for barrier options with daily observations and the versatility of the scripted trade framework beyond single-asset equity cases.

2. **American Monte Carlo (Section 4.11)**: Demonstrates use of American Monte Carlo Simulation (AMC) for exposure generation in ORE. Includes several runnable examples: benchmarking AMC vs. classic exposure simulation on a small IR/FX portfolio, scripted Bermudan swaption and LPI swap, FX TaRF product with embedded C++ script, forward bond with AMC, overlapping close-out grid, and scenario statistics.

## American Monte Carlo (pages 72–73)

Summary: The partial document covers two main topics: scripted trade examples (Trades 7b, 8, 8b) for barrier options and equity accumulators, including pricing notes on Black-Scholes model usage, deviations from analytical pricing for daily observations, and the versatility of the scripted trade framework. The second part introduces American Monte Carlo (AMC) simulation for exposure generation, with benchmarking against classic simulation on a portfolio of Bermudan swaption, single/cross currency swaps, FX swap and FX option. It details configuration changes (e.g., LGM mean reversion, regression polynomial order) and shows exposure profile comparisons (EPE/ENE) for each trade, emphasizing accuracy improvements through increased training paths and basis functions. Additional AMC examples include scripted Bermudan swaption, LPI swap, FX TaRF, forward bond, overlapping close-out grid, and scenario statistics.

### Benchmarking AMC vs Classic Simulation (pages 73–79)

Summary: The partial document covers the following main points:

- Benchmarking American Monte Carlo (AMC) simulation against classic exposure simulation in ORE, using a portfolio of four trades (Bermudan swaption, single currency swap, cross currency swap, FX option) on a quarterly grid.
- Comparison of EPE/ENE profiles between classic and AMC for each trade, highlighting the need for specific settings (e.g., zero mean reversion, high-order regression polynomials) to achieve agreement.
- Configuration steps to enable AMC in the simulation analytic, including setting the `amc` parameter, specifying an AMC pricing engines file, and listing trade types.
- Detailed pricing engine configuration for AMC-enabled products (e.g., BermudanSwaption), with parameters for training and pricing phases (random sequences, basis functions, sample counts, etc.).
- Table of supported product types (Swap, CrossCurrencySwap, FxOption, BermudanSwaption, MultiLegOption) and their corresponding model and engine types.
- Additional features: plain MC pricing engines for Bermudan swaptions and the MultiLegOption trade type, including sample configurations and model parameters.
- Section 4.11.2 on Scripted Bermudan, demonstrating AMC exposure simulation for scripted trade types (Bermudan Swaption, LPI Swap) using a script library and specific settings in `ore.xml`.

### Scripted Bermudan (pages 79–80)

Summary: The partial document covers model parameters for cross-asset correlations and calibration strategies (IrCalibrationStrategy, FXCalibration, ExtrapolateFxVolatility), along with engine parameters for Monte Carlo simulation (training/pricing sequences, seeds, samples, basis functions, Brownian Bridge ordering, Sobol direction integers). It then details several use cases: Scripted Bermudan (AMC for Bermudan Swaption and LPI Swap with configuration in ore.xml), Scripted TaRF (FX Target Redemption Forward using scripted trade framework), Forward Bond (AMC exposure simulation for forward and plain vanilla bonds, with security spread implied from bond prices), and Overlapping Close-out Grids in AMC (demonstrating overlapping primary and close-out simulation grids).

### Scripted TaRF (pages 80–80)

Summary: The partial document covers several main points: ORE's ability to handle a mix of trades using both AMC and classic simulations, combining NPV cubes for exposure and XVA calculations. It then describes specific examples: scripted FX Target Redemption Forward (TaRF) using the FxTARF trade type with payoff script embedded in C++ code; a forward bond demo showing AMC simulation with security spread implied from bond prices, requiring specific curve configuration and naming convention for forward bonds; and an overlapping close-out grids demo for AMC, enabling overlapping primary and close-out grids from ORE v13 onwards.

### Forward Bond (pages 80–80)

Summary: The partial document covers ORE's ability to handle a mix of trades from AMC and classic simulations, with NPV cubes combined for exposure and XVA results. It then describes three specific examples: Scripted TaRF (FX Target Redemption Forward) showing scripted trade implementation in C++, Forward Bond demonstrating AMC exposure simulation for a forward and plain vanilla bond with security spread implied from bond prices, and Overlapping Close-out Grids in AMC where primary and close-out grids overlap on a daily simulation grid.

### Overlapping Close-out Grids in AMC (pages 80–81)

Summary: The partial document covers several key topics: the specification of aggregation scenario data files (scenariodata.csv.gz and scenariodata.csv), a note on ORE's ability to handle a mix of trades from AMC and classic simulations combining NPV cubes. It then details four examples: Scripted TaRF (FX Target Redemption Forward) which uses a built-in trade type with scripted framework internally; Forward Bond (AMC exposure simulation and XVA for forward and plain vanilla bonds, including security spread implication); Overlapping Close-out Grids in AMC (demonstrating overlapping primary and close-out grids, a feature from ORE v13); and Extract Scenario Statistics (basic statistical analysis of simulated scenario data). Finally, it introduces XVA Risk examples: XVA Stress Testing (using XVA_STRESS analytic with classical and AMC engines, stress scenarios, and recommendations for settings) and XVA P&L Explain (computing market implied XVA change between evaluation dates using par rate shifts).

### Extract Scenario Statistics (pages 81–81)

Summary: The partial document covers two main topics: extracting scenario statistics (section 4.11.6) and XVA risk examples (section 4.12). Specifically, section 4.11.6 describes a Python script that performs basic statistical analysis (min, mean, max, standard deviation, skewness, kurtosis) on simulated raw scenario data (yield curve discount factors, FX spot rates) for each factor at each simulated future date. Section 4.12 introduces XVA risk examples, including subsection 4.12.1 on XVA stress testing using classical and AMC XVA engines, with details on the XVA_STRESS analytic type, stress scenarios, and recommendations for settings; and subsection 4.12.2 on XVA P&L explain, which computes market implied XVA changes between two evaluation dates using par rate shifts.

## XVA Risk (pages 81–81)

Summary: The partial document covers two main topics: **Extract Scenario Statistics** (section 4.11.6), which describes using `run_scenariostatistics.py` to perform basic statistical analysis (min, mean, max, standard deviation, skewness, kurtosis) on simulated raw scenario data such as yield curve discount factors and FX spot rates; and **XVA Risk** (section 4.12), which introduces two examples: **XVA Stress Testing** (4.12.1) using `run_stress.py` to perform stress testing with classical and AMC XVA engines, analyzing market rate shifts and generating xva/exposure reports; and **XVA P&L Explain** (4.12.2) using `run_xvaexplain.py` to compute market implied XVA changes between evaluation dates by deriving par rate shifts and calculating CVA changes.

### XVA Stress Testing (pages 81–81)

Summary: The partial document covers Section 4.11.6 on extracting scenario statistics, which involves running a script to perform basic statistical analysis (min, mean, max, standard deviation, skewness, kurtosis) on simulated raw scenario data at each future date. Section 4.12 introduces XVA Risk examples, including subsection 4.12.1 on XVA Stress Testing, which demonstrates stress testing using classical and AMC XVA engines, with a new analytic type that supports stress tests in zero and par domains, and notes recommended settings. Subsection 4.12.2 covers XVA P&L Explain, which computes market implied XVA changes between evaluation dates by deriving par rate shifts for each risk factor and calculating the resulting CVA change.

### XVA P&L Explain (pages 81–82)

Summary: This partial document covers two main topics: **Extract Scenario Statistics** (section 4.11.6), which describes running a basic statistical analysis of simulated raw scenario data (e.g., yield curve discount factors, FX spot rates) to generate a report with min, mean, max, standard deviation, skewness, and kurtosis for each factor at each future date; and **XVA Risk** (section 4.12), which includes several examples: XVA Stress Testing (using classical and AMC engines, generating xva and exposure reports under market rate shift scenarios), XVA P&L Explain (computing market implied XVA changes between two dates using par rate shifts), XVA Sensitivities (computing XVA sensitivities via bump & revalue, supporting classic and AMC simulation, outputting SA-CVA data), and CVA Capital (SA-CVA and BA-CVA) calculation, which utilizes the XVA sensitivity output or direct input to compute capital figures.

### XVA Sensitivities (pages 82–82)

Summary: The main points covered in the partial document are:  
- The XVA Explain analytic replaces today's market with a simulation market, using different tenors and ATM volatilities depending on settings, with recommendations to activate UseSpreadedTermStructures and simulate SwaptionVolatilities.  
- XVA Sensitivities are computed via bump & revalue, utilizing sensitivity configurations similar to NPV calculations, supporting both "classic" and AMC simulation, and generating raw and par domain sensitivities for a small proof-of-concept uncollateralised portfolio.  
- Notes highlight performance challenges with large portfolios, the benefit of AMC simulation, and ongoing work on a computation graph framework for GPU parallelization and AAD.  
- CVA Capital calculation using SA-CVA (and BA-CVA) leverages the XVA sensitivity analytic’s CVA par sensitivity output, demonstrated in a script that picks up previously computed sensitivities.

### CVA Capital: SA-CVA and BA-CVA (pages 82–83)

Summary: The partial document covers several key analytics for XVA and credit risk. For XVA, it describes the XVA Explain analytic, which replaces today's market with a simulation market and recommends specific settings (UseSpreadedTermStructures and simulating SwaptionVolatilities). It then details the XVA Sensitivity analytic, which computes sensitivities via bump & revalue using both classic and AMC simulation, generating raw and par domain results. CVA capital calculations are presented: SA-CVA using XVA sensitivity outputs and BA-CVA based on SA-CCR exposure. Finally, the credit risk section covers SA-CCR capital calculation for derivatives and a Credit Portfolio Model that integrates credit defaults, rating migrations, and derivative PnL to produce a portfolio gain/loss distribution, with seven demo portfolios listed.

## Credit Risk (pages 83–83)

Summary: The partial document covers the following main points: XVA Sensitivity analytics with output files, CVA Capital calculation using the Basic Approach (BA-CVA) that relies on SA-CCR, the Standard Approach Counterparty Credit Risk (SA-CCR) capital calculation for derivatives, and the Credit Portfolio Model which integrates credit and market risk to generate portfolio gain/loss distributions, demonstrated with seven demo portfolios.

### SA-CCR (pages 83–83)

Summary: The document covers several key topics: the XVA sensitivity analytic (referenced as "XVA Sensitivity analytic"), CVA Capital calculation using the Basic Approach (BA-CVA) demonstrated by running `python run_bacva.py`, the Standard Approach Counterparty Credit Risk (SA-CCR) calculation via `python run_saccr.py`, and the Credit Portfolio Model (CPM) for generating integrated portfolio gain/loss distributions driven by credit defaults, rating migrations, and derivative PnL, demonstrated by `python run_cpm.py` with various test cases.

### Credit Portfolio Model (pages 83–84)

Summary: The partial document covers several main topics: XVA sensitivity analytics (CVA and BA-CVA calculations), the Standard Approach Counterparty Credit Risk (SA-CCR) for derivatives, a Credit Portfolio Model that integrates credit and market risk, and performance enhancements including multi-threading for exposure simulation and alternative sensitivity calculation methods using AAD and GPUs (with a Jupyter notebook for visualization).

## Performance (pages 84–84)

Summary: The partial document describes performance demonstrations for ORE: multi-threaded exposure simulation for Vanilla Swap copies, and NPV sensitivity calculations using classic bump, computation graph, AAD, and GPU acceleration (including a Jupyter notebook for visualization).

### Multi-threading (pages 84–84)

Summary: The document covers two main performance topics: multi-threading for parallel exposure simulation using `run_multithreading.py` and comparing sensitivity calculation methods (classic bump, computation graph, AAD, and GPU) via `run_sensi.py`. It also mentions activating a demo case by uncommenting a section in `run_cpm.py`, and references a Jupyter notebook for further analysis.

### NPV Sensitivities with AAD and GPUs (pages 84–85)

Summary: The partial document covers performance demonstrations for ORE, including multi-threaded exposure simulation, NPV sensitivity calculations using classic bump, computation graph, AAD, and GPU methods with timing comparisons, CVA sensitivity with AAD and GPU parallelisation (still in progress), and instructions for installing and using the ORE-Python module with example scripts.

### CVA Sensitivities with AAD (pages 85–85)

Summary: The partial document covers two main sections: CVA Sensitivities with AAD (section 4.14.3) and ORE-Python (section 4.15). The first part describes a prototype CVA sensitivity calculation using AAD on a single swap, with four execution batches: a base CVA calculation using AMC (9 sec), bump & revalue sensitivity (48 sec), AAD-based sensitivity (2 sec), and GPU parallelisation (still work in progress). It also mentions running a Jupyter notebook. The second part introduces the ORE-Python module (release 9, March 2023), providing steps to create a virtual environment, install the module via pip, and run example scripts (`ore.py` and `ore2.py`) to demonstrate Python-wrapped ORE applications.

## ORE-Python (pages 85–86)

Summary: The partial document covers three main topics: CVA Sensitivities with AAD, ORE-Python, and ORE-API. Under CVA Sensitivities, it describes a prototype script that compares base CVA using AMC, bump & revalue sensitivity, AAD-based sensitivity, and GPU parallelisation (still in progress). The ORE-Python section explains how to install the pre-compiled Python module via pip, set up a virtual environment, and run example scripts (ore.py, ore2.py, commodityforward.py) demonstrating exposure calculations, in-memory result access, and low-level QuantLib/QuantExt access. It also mentions Jupyter notebook examples in subfolders and required pip packages. Finally, the ORE-API section introduces a proof-of-concept web service based on Flask for ORE.

## ORE-API (pages 86–88)

Summary: The partial document covers several main topics: accessing and post-processing ORE in-memory results in Python without file I/O, lower-level access to QuantLib/QuantExt through the ORE Python module, deactivating or removing Python environments, building the Python module and installable packages from source, Jupyter notebook examples (merged into the ORE repository, with instructions for launching and required packages like matplotlib, pandas, etc.), the ORE-API proof-of-concept web service (based on Flask and the ORE Python module, with main files restapi.py, oreApi.py, simplefileserver.py and instructions for running a local example), and the parameterisation of ORE runs via a master input file (ore.xml) along with notes on using existing examples as boilerplate.

# Exposure (pages 45–46)

Summary: The partial document describes the validation of Dynamic SIMM distributions by comparing them to a benchmark at four future time points (1M, 1Y, 4Y, 8Y) using updated simulations and plots (Figure 9). It lists ongoing work on path-wise benchmarking, additional products, alternative regression methods, and comparison to a simpler DIM model. The document then introduces Section 4.8 on exposure simulation and CVA for uncollateralized trades, enumerating many single-trade examples (swaps, FRAs, swaptions, caps/floors, FX, cross-currency, equity, commodity, inflation, credit) and further features (long-term simulation, different measures, Hull-White models, wrong-way risk, flip view). It begins detailing the first example: a swap with flat yield curve.

# Swap with flat yield curve (pages 46–48)

Summary: The partial document covers a range of exposure simulation examples for various financial derivatives, including Swaptions, Caps/Floors, FX instruments, Cross Currency Swaps, Equity Forwards/Options, Commodity derivatives, Inflation swaps, Credit Default Swaps, and more complex trades like Capped/Floored CMS Spreads. It also introduces long-term simulation, different measures, two-factor Hull-White model, wrong-way risk, and flip view features, as well as parameter calibration for exposure models. Detailed subsections focus on specific cases: a vanilla Swap in a flat yield curve environment (Section 4.8.1), a Swap in a normal (non-flat) yield curve environment (Section 4.8.2), and a Forward Rate Agreement with Averaging Overnight Index Swaps (Section 4.8.3), illustrating exposure profiles and comparison with swaption prices.

# Swap with normal yield curves (pages 48–48)

Summary: The partial document covers two main topics: first, the behavior of a vanilla ATM swap in a realistic upward-sloping yield curve environment, showing how expected exposure from the payer's (EPE) and receiver's (ENE) perspectives diverge over time, and reconciling with swaption prices; second, an example using Forward Rate Agreements and Averaging Overnight Index Swaps in a minimal portfolio, with results stored in specific output files.

# Forward Rate Agreement (pages 48–49)

Summary: The partial document covers three main topics:

1. **Swap with normal yield curves (Section 4.8.2):** Describes a vanilla ATM swap's expected exposure in a realistic upward-sloping yield curve environment, showing that the receiver swap moves out of the money while the payer swap moves into the money, causing expected positive exposure (EPE) and expected negative exposure (ENE) to diverge, yet remain consistent with payer/receiver swaption prices.

2. **Forward Rate Agreement (Section 4.8.3):** Demonstrates pricing, cash flow projection, and exposure simulation for Forward Rate Agreements (FRA) and Averaging Overnight Index Swaps (OIS), using a minimal portfolio of four trades, with outputs in NPV, flows, and exposure files.

3. **Swaptions (Section 4.8.4):** Covers three cases:
   - **European Swaptions** with cash vs. physical settlement, highlighting differences in valuation (due to yield curve steepness) and exposure profiles (cash settlement truncates at exercise, physical settlement turns into swap-like exposure post-exercise); also compares to the underlying forward starting swap.
   - **Bermudan and American Swaptions**, noting the step-wise exposure decrease for Bermudan due to multiple exercise dates, identical exposures for cash and physical up to first exercise, and significant computation time (LGM grid engine).
   - **European Callable Swap**, represented as a combination of a non-callable swap and a physically delivered swaption (sold call option), with exposure evolutions shown; includes a note on modifying rates to see deviation from a short swap exposure.

# Swaptions (pages 49–52)

Summary: The partial document covers two main topics: Swaptions (section 4.8.4) and Cap/Floor (section 4.8.5). For Swaptions, it describes three cases: European swaptions with cash and physical settlement, highlighting differences in exposure due to yield curve steepness and the effect of premium settlement; Bermudan and American swaptions, noting the step-wise exposure decrease for Bermudan and increased computation time when using an LGM grid engine; and a European Callable Swap represented as a package of a non-callable swap and a physically settled swaption, with exposure comparisons when the underlying swap is deep in the money. For Cap/Floor, it presents two example portfolios: one combining a swap and a collar (portfolio 1) to reduce net exposure, and another with a short cap, long floor, and long collar that offset each other (portfolio 2). Both sections include figures illustrating exposure evolutions and mention simulation parameters (paths, time steps).

# Cap/Floor (pages 52–53)

Summary: The document covers two main topics: Cap/Floor and FX Forward/FX Option. For Cap/Floor, it describes example Python scripts generating exposure evolutions for swaps, caps, floors, and collars, with two specific portfolios: Portfolio 1 (a 20-year swap receiving 3% fixed plus a long collar with cap and floor at 4%) and Portfolio 2 (a short cap, long floor, and a long collar that offsets them). It also mentions three additional test portfolios. For FX Forward and FX Option, it discusses an example generating exposure evolution for a EUR/USD FX forward with a 10-year value date, comparing EPE and ENE to vanilla FX option prices, and also shows exposure evolution for an FX option. Simulation details (number of paths, quarterly time steps) are provided for all examples.

# FX Forward and FX Option (pages 53–54)

Summary: The partial document covers two main topics: FX Forward and FX Option exposure evolution (section 4.8.6), and Non-Resetting and Resetting Cross Currency Swaps (section 4.8.7). For FX instruments, it describes how the example `run_fx.py` generates exposure for a 10Y EUR/USD FX Forward, showing that EPE and ENE at the value date match Vanilla FX Option prices (Figure 17). It also illustrates FX Option exposure (Figure 18) and explains the expected flat exposure deviating due to the pricing approach. For cross currency swaps, `run_ccs.py` demonstrates a non-resetting CCS exposure blending interest rate swap and FX forward features (Figure 19), along with serialization of the calibrated model. It also shows the effect of FX resetting, which causes exposure collapse at each reset period start (Figure 20).

# Non-Resetting and Resetting Cross Currency Swaps (pages 54–55)

Summary: The partial document discusses the derivation of NPV(t) and expected positive exposure (EPE) using a numeraire asset, noting a deviation in ORE's simulation due to deterministic Black volatility and potential removal by extending volatility modelling. It then covers cross currency swaps, including a vanilla non-resetting swap's exposure profile (blending interest rate swap and FX forward features) and the effect of FX resetting, which causes exposure collapse at period starts. Next, it describes equity derivatives, listing a portfolio of options, forwards, and swaps, and notes that put-call parity holds, with equity call options showing smooth exposure and forwards increasing toward maturity. Finally, it introduces commodity derivatives as an example run.

# Equity Derivatives (pages 55–55)

Summary: The partial document covers a figure illustrating cross currency basis swap exposure evolution with and without mark-to-market notional reset, followed by sections on equity and commodity derivatives. The equity derivatives section details a Python example computing NPV, sensitivities, exposures, and XVA for a portfolio of OTC equity options, forwards, and swaps, noting put-call parity and expected exposure profiles. The commodity derivatives section introduces a Python script command.

# Commodity Derivatives (pages 55–56)

Summary: The partial document covers several sections on derivative pricing and exposure simulation: a cross-currency basis swap with and without mark-to-market notional reset (Figure 20), equity derivatives (Section 4.8.8) including a portfolio of EUR and USD equity options, forwards, and swaps, demonstrating put-call parity and exposure profiles, commodity derivatives (Section 4.8.9) with a portfolio of commodity forwards, swaps, options, and swaptions, inflation CPI and YOY swaps (Section 4.8.10) comparing Dodgson-Kainth and Jarrow-Yildirim models, and a mention of credit default swaps (Section 4.8.11).

# Inflation CPI and YOY Swap - TODO (pages 56–56)

Summary: The partial document covers several exposure simulation examples: Example 16 demonstrates simulated exposures for an equity ("Luft") call option and OTC forward trade, with a graph showing call EE and fwd EE over 2.5 years. It also mentions a portfolio of commodity derivatives (forward, swap, European option, average price option, swaption) with exposure reports and graphs. Section 4.8.10 is about inflation CPI and YOY swaps, with two batches using the Dodgson-Kainth (DK) and Jarrow-Yildirim (JY) inflation models for a portfolio of EU and UK CPI and YOY swaps, including EPE graphs. Section 4.8.11 refers to a credit default swap example via a Python script.

# Credit Default Swap (pages 56–58)

Summary: The partial document covers multiple financial derivative exposure simulations, including equity call options and OTC forwards (Example 16), inflation swaps (CPI and YOY) using the Dodgson-Kainth and Jarrow-Yildirim models, credit default swaps (CDS) with the LGM model including wrong-way risk analysis (shown via a correlation table of XVA results), and capped/floored (digital) CMS spreads as well as CMS spreads with formula-based payoffs. Figures and tables illustrate exposure evolution (EPE, ENE) and pricing outcomes.

# Capped/Floored (Digital) CMS Spread (pages 58–58)

Summary: The partial document covers a credit simulation example using the LGM model, demonstrating Wrong Way Risk due to credit correlation between a CDS underlying and counterparty. It includes a table of XVA results (CVA, DVA, FBA, FCA) for various correlation levels. Subsequent sections describe pricing and exposure simulation examples for capped/floored CMS spreads and formula-based payoff CMS spreads with bonds.

# Capped (Digital) CMS Spread with Formula-based Payoff . . . . (pages 58–59)

Summary: The partial document covers several topics: a credit simulation example using the LGM model demonstrating Wrong Way Risk due to correlation between CDS underlying and counterparty, with a table of XVA results at various correlation levels; examples of pricing and exposure simulation for Capped/Floored (Digital) CMS Spreads and CMS Spreads with Formula-based Payoffs; and a long-term simulation example highlighting the issue of noisy EPE profiles for long maturities (50 years) due to narrow NPV distributions, resolved by applying a shift transformation (ShiftHorizon parameter) to the Linear Gauss Markov model, which changes the measure to a T-Forward measure and improves numerical stability.

# Long-term simulation (pages 59–60)

Summary: The partial document covers two main topics: long-term simulation challenges and the choice of measure in exposure calculations. It first discusses issues with Monte Carlo simulation for long-term swaps (e.g., 50-year maturity) where the risk-neutral NPV distribution becomes too narrow, leading to noisy EPE/ENE profiles that do not match analytical swaption prices. The solution is a "shift transformation" applied to the Linear Gauss Markov model, which effectively performs a change of measure to a T-Forward measure (e.g., 30-year horizon) to improve numerical stability without affecting expected exposures. This adjustment corrects the upward drift of rate distributions caused by convexity. The second part briefly introduces a separate example (section 4.8.15) that demonstrates the effect of different risk-neutral measures on simulated expected and peak exposures using an un-collateralized vanilla swap.

# Choice of Measure (pages 60–61)

Summary: The partial document covers several key topics related to exposure simulation in financial modeling. It first presents Example 12, which demonstrates the impact of a horizon shift on long-term swap exposures, showing how the horizon shift alters the distribution's mean and convexity effect. It includes figures illustrating swap EPE/ENE with and without horizon shift, as well as zero rate distributions over time. Next, the document discusses the choice of risk-neutral measure, comparing LGM, Bank Account, and T-Forward measures, and shows that while expected exposures are measure-independent, peak exposures vary across measures, as depicted in Figure 27. Finally, it introduces simulation in the two-factor Hull-White model (Example 36), covering model calibration, scenario generation, and the specification of diffusion and reversion matrices derived from principal component analysis.

# Simulation in the two-factor Hull-White model (pages 61–63)

Summary: The partial document covers the following main points:

1. **Simulation under different measures**: It describes exposure simulation in three measures – LGM, Bank Account (BA), and T-Forward with horizon T=20 – and notes that expected exposures (EPE) are measure-independent while peak exposures (PFE) depend on the measure choice. A graph (Figure 27) illustrates the evolution of EPE and PFE across these measures.

2. **Simulation in the two-factor Hull-White model**: It details a two-batch process (calibration and exposure simulation) using a Hull-White multifactor model with two independent Brownian motions, four states, constant diffusion and reversion matrices. The matrices are calibrated to the first two principal components of absolute rate curve movements (parallel and rotation), with input eigenvectors and volatilities provided.

3. **Principal component analysis and validation**: Output from the calibration batch is analyzed to show model-implied eigenvalues and eigenvectors, which match the prescribed input values (e.g., volatilities of 0.0070 and 0.0030). A plot (Figure 28) compares input and model-implied eigenvectors.

4. **Second batch – cross-currency swap example**: This batch mirrors the example in section 4.8.7 (EPE/ENE for a cross-currency swap) but uses the multifactor HW model for EUR and USD, with correlations between factors of different currencies and FX factors.

5. **Wrong-Way-Risk**: The section ends with a brief mention of Wrong-Way-Risk (section 4.8.17), indicated by the call "Calling 63" as a transition to that topic.

# Wrong-Way-Risk (pages 63–64)

Summary: The partial document covers several main points:

- Presentation of input principal components (eigenvalues and eigenvectors) from a principal component analysis, along with a comparison of model-implied versus input eigenvectors for a Hull-White 4-factor model calibrated to two principal components (parallel and rotation). A figure (Figure 28) illustrates that the second model eigenvector is the negative of the input vector.

- An example of a multi-factor Hull-White model for EUR and USD generating scenarios, with correlations between interest rate factors and FX factors.

- Section 4.8.17 on Wrong-Way-Risk, demonstrating an extension of a single uncollateralized swap with dynamic credit and non-zero IR-CR correlation, and providing XVA results (CVA, DVA, FBA, FCA) for different correlation levels in Table 11.

- Section 4.8.18 on Flip View, showing how ORE can switch perspectives in XVA calculations with minimal XML changes.

- Section 4.8.19 on HW n-Factor Historical Calibration, describing two calibration approaches: full calibration using PCA on historical data, and mean reversion calibration only with user-provided eigenvalues/eigenvectors.

# Flip View (pages 64–64)

Summary: The partial document covers three main topics: an extension of a single uncollateralised swap example with dynamic credit and non-zero IR-CR correlation, including a table of XVA results at varying correlation levels; the "Flip View" functionality that allows switching perspectives in XVA calculations with minimal configuration changes; and the "HW n-Factor Historical Calibration" feature, which calibrates Hull-White model parameters using historical data via PCA or user-provided eigenvalues.

# HW n-Factor Historical Calibration (pages 64–65)

Summary: The partial document covers several key topics: an extension of an IR swap XVA example with dynamic credit and IR-CR correlation, showing results in a table for different correlation levels; a "Flip View" demonstration for switching XVA perspectives; calibration of the Hull-White n-factor model using historical data (full calibration via PCA or user-provided eigenvalues); and a section on netting set exposure and collateral, including a bi-weekly grid example illustrating collateral effects on exposure (with plots and explanation of spikes), and a summary of XVA outputs (CVA, DVA, FVA, COLVA, MVA, Collateral Floor) in an xva.csv file.

# Parameterisation (pages 88–89)

Summary: The partial document covers the parameterisation of ORE, starting with a command line invocation using an ore.xml master input file. It explains that this file contains general setup information and is divided into sections: Setup, Logging, Markets, and Analytics. The document then focuses on the Setup section, providing an example listing of parameters (e.g., asofDate, paths to input/output directories, market data, trade data, configuration files) and notes that parameter names are self-explanatory, with paths interpreted relative to the executable directory. It also mentions that users can base their configuration on provided examples.

## Analytics: ore.xml (pages 89–91)

Summary: The partial document introduces the structure of the ORE master input file, which contains Setup, Logging, Markets, and Analytics sections. It details the Setup section with parameters for paths, file references, log verbosity (logMask), market data loading, and various configuration files (curve, conventions, pricing engines, etc.). Key flags are explained, such as implyTodaysFixings, useAtParCouponsCurves, observationModel, lazyMarketBuilding, continueOnError, buildFailedTrades, nThreads, enrichIndexFixings, ignoreFixingLead, and ignoreFixingLag. It also begins describing the Logging section (5.1.1) for configuring logging options.

### Pricing, Cashflows, Curves (pages 93–95)

Summary: The partial document covers the Analytics section of a financial risk and pricing system (ORE). It lists permissible analytics types (e.g., NPV, Cashflows, Curves, Exposure Simulation, xVA, Sensitivity, VaR, ISDA SIMM, etc.) and describes their parameterization via key/value pairs within `<Analytic>` tags, including an `active` parameter to enable/disable each analysis. Detailed examples are provided for basic analytics: NPV (with base currency, output file, additional results precision), Cashflows (outputting future and optionally past cashflows with details on amount, coupon, fixing value, notional), and Curves (exporting yield curves on a specified time grid, with calibration report options). The document also introduces Simulation and Model Calibration analytics, explaining that Monte Carlo simulation generates an NPV cube for all trades over future time steps and paths, supporting both classic and American Monte Carlo methods for exposure and XVA calculations. Additionally, it mentions the `additionalResults` and `todaysMarketCalibration` analytics for pricing engine-specific outputs and market build information.

### Simulation and Model Calibration (pages 95–100)

Summary: The document describes several analytics in the ORE framework: 
- **Curves Analytic**: exports yield curves built from a configuration file, with options for time grid (monthly steps or explicit tenors), calendar, and output to CSV.
- **Calibration Report Control**: parameters to enable/disable calibration reports and set decimal precision.
- **Additional Results Analytic**: writes a report with trade-specific results (e.g., for swaptions) as shown in a sample table.
- **Today's Market Calibration Analytic**: outputs information on the build of the t0 market.
- **Simulation and Model Calibration**: details Monte Carlo simulation for NPV cube generation, including parameters for scenario data, cash flows, survival probabilities, and American Monte Carlo (AMC) for specific trade types. Also covers calibration analytics for CAM and HW models, with extensive parameters for historical calibration, PCA, and mean reversion.
- **Scenario Generation Analytic**: generates scenarios with statistics and distribution, configurable via simulation config file, bucket count, and zero rate output.
- **Value Adjustments (XVA)**: supports CVA, DVA, FVA, COLVA calculations using a pre-generated NPV cube and CSA details, enabling quick re-analysis without re-generating the cube.

### Scenario Generation (pages 100–100)

Summary: The document covers two main topics: scenario generation and value adjustments. The scenario generation section describes the `scenarioGeneration` analytic, its configuration parameters (simulationConfigFile, distributionBuckets, outputZeroRate, scenariodump), and their meanings. The value adjustments section explains the XVA analytic for calculating CVA, DVA, FVA, and COLVA, which depend on a pre-generated NPV cube referenced by cubeFile and CSA details from csaFile. It highlights the ability to rerun XVA analytics without regenerating the cube, and notes file compression formats.

### Value Adjustments (pages 100–105)

Summary: The partial document covers three main topics:

- **Scenario Generation (5.1.4)**: Describes the `scenarioGeneration` analytic, its configuration parameters (e.g., `simulationConfigFile`, `distributionBuckets`, `outputZeroRate`, `scenariodump`), and their interpretations.

- **Value Adjustments (5.1.5)**: Details the XVA analytic type, including parameters for CVA, DVA, FVA, COLVA, KVA, DIM, MVA, and PFE. It explains the dependency on a pre-generated NPV cube, CSA file, and numerous optional settings for exposure profiles, calculation types, allocation methods, dynamic initial margin, flip view, and cube output files.

- **Sensitivity and Stress Testing (5.1.6)**: Briefly introduced as providing bump and revalue sensitivities and NPV changes under user-defined stress scenarios, with a typical configuration to follow.

### Sensitivity and Stress Testing (pages 105–110)

Summary: The partial document covers several key areas:

1. **DIM Regression Snapshot Parameters**: Defines parameters for netting set identification (dimOutputNettingSet), grid points for time dimension (dimOutputGridPoints), and cube output file names for trade NPV (rawCubeOutputFile) and aggregated NPV after collateral (netCubeOutputFile). Also describes settings for full initial collateralization (fullInitialCollateralisation), flip view for XVA calculations (flipViewXVA) with associated curve postfixes, and an assumption for cash flow payments within MPoR (mporCashFlowMode).

2. **Sensitivity and Stress Testing Analytics**: Introduces the sensitivity analytic with configuration parameters (marketConfigFile, sensitivityConfigFile, pricingEnginesFile, output files for scenarios, sensitivities, cross gamma, etc.). Explains parameters such as outputSensitivityThreshold, recalibrateModels, parSensitivity, outputJacobi, and decomposeIndexSensitivities. Describes decomposition of credit, equity, and commodity index sensitivities, controlled by pricing engine settings or trade envelope fields. Details the separate zeroToParSensiConversion analytic for converting raw sensitivities to par sensitivities, including required input columns (idColumn, riskFactorColumn, deltaColumn, currencyColumn, shiftSizeColumn, baseNpvColumn). Presents stress analytic configuration similar to sensitivity, with additional parameters for stress scenario file, precision, and stressZeroScenarioDataFile. Notes the parStressConversion analytic for generating raw domain stress configuration without running tests. Describes the combined SENSITIVITY_STRESS analytic that runs sensitivity under each stress scenario.

3. **Value at Risk (VaR) Analytics**: Introduces the parametricVar analytic for computing VaR measures using sensitivity data (delta, gamma, cross gamma). Configuration includes parameters for portfolioFilter, sensitivityInputFile, covarianceInputFile, SalvagingAlgorithm, quantiles, breakdown, method (e.g., DeltaGammaNormal), mcSamples, mcSeed, and outputFile.

### Value at Risk (pages 110–111)

Summary: The partial document covers two main analytics: Stressed Sensitivity Analysis and Value at Risk (VaR). For Stressed Sensitivity Analysis, it lists configuration parameters (marketConfigFile, stressConfigFile, sensitivityConfigFile, calcBaseScenario) and their interpretations. For VaR, it provides a configuration example (Listing 20) and explains parameters such as portfolioFilter, sensitivityInputFile, covarianceInputFile, SalvagingAlgorithm, quantiles, breakdown, method, mcSamples, mcSeed, and outputFile. It also briefly introduces the Correlation analytic (Listing 21) at the end.

### Correlation (pages 111–112)

Summary: The partial document covers three main sections: 
1. Parameters for Value-at-Risk (VaR) computation, including portfolio filter, sensitivity input, covariance file, salvaging algorithm, quantiles, breakdown options, method (Delta, DeltaGammaNormal, MonteCarlo), Monte Carlo samples/seed, and output file.
2. Configuration and parameters for the Correlation analytic, such as correlation method, market configuration file, historical scenario file, sensitivity configuration, historical period, MPOR days/calendar, and output file.
3. A brief mention of P&L, P&L Explain, ZeroToParShift, and Scenario analytics, with configuration examples referenced.

### P&L, P&L Explain, ZeroToParShift, Scenario (pages 112–115)

Summary: The document covers several ORE analytics, including:

- **Correlation analytic**: Configuration for computing correlations (e.g., Pearson method), with parameters for market configuration, historical scenarios, sensitivity configuration, historical period, MPOR days/calendar, and output file.
- **P&L analytic**: Setup for single-period P&L calculation, with parameters for MPOR date/days, simulation config, curve/conventions/portfolio files for MPOR, and optional date-adjusted risk factors.
- **P&L Explain analytic**: Extends P&L with explanation using par or raw sensitivities, including sensitivity config, parSensitivity flag, and risk factor level reporting.
- **Zero to Par Shift analytic**: Utility to convert raw market moves to equivalent par moves, requiring market, stress, sensitivity, and pricing engine configs.
- **Scenario analytic**: Exports the simulation market's base scenario to a file.
- **Initial Margin (ISDA SIMM) analytic**: Computes initial margin using SIMM, with parameters for version, CRIF file, currencies, IM regulations, MPOR days, and SIMM calibration. It can also generate CRIF internally for IR/FX risks.

### Initial Margin: ISDA SIMM and IM Schedule, CRIF Generation . (pages 115–117)

Summary: The partial document covers three main topics: the scenario analytic for exporting simulation base scenarios, the initial margin analytics including ISDA SIMM computation with CRIF generation and IM Schedule, and XVA stress testing for bump-and-revalue XVA sensitivities and stress scenarios. Key configuration examples and parameter interpretations are provided for each analytic.

### XVA Stress Testing (pages 117–118)

Summary: The partial document covers three main analytics: IM Schedule, XVA Stress Testing, and XVA Sensitivity. For IM Schedule (Listing 28), it requires a CRIF file with two lines per trade (RiskClass PV and Notional), and specifies product class categories (Rates, FX, Equity, Credit, Commodity). For XVA Stress Testing (Listing 29), it details parameters (marketConfigFile, stressConfigFile, sensitivityConfigFile, writeCubes) and explains stress scenario generation, simulation market behavior, and performance recommendations (use of AMC, spreaded term structures, swaption volatility simulation). For XVA Sensitivity (Listing 30), it notes similar configuration to XVA stress, using existing exposure and XVA analytic parameterizations, and describes bump-and-revaluation sensitivity computation. The document also mentions that ORE reuses existing settings and allows deactivation of regular analytics when stress/sensitivity analytics are active.

### XVA Sensitivity (pages 118–119)

Summary: The partial document covers three XVA analytics: XVA Stress, XVA Sensitivity, and XVA Explain. Main points include:
- **XVA Stress**: Uses stress test scenarios (defined in `stressConfigFile`) to compute stressed value adjustments. The simulation market may differ from today's market (e.g., different tenor structures, only ATM swaption vols). Recommendations: activate `UseSpreadedTermStructures` and swaption volatility simulation. Reuses existing exposure/XVA parameterizations.
- **XVA Sensitivity**: Computes bump-and-revaluation sensitivities for value adjustments. Configuration similar to XVA Stress, with `sensitivityConfigFile`, `parSensitivity` flag for additional par sensitivity outputs. Also replaces `todaysMarket` with `ScenarioSimMarket`, same recommendations as stress.
- **XVA Explain**: Computes market-implied changes of value adjustments between two evaluation dates. Parameters include `stressConfigFile`, `sensitivityConfigFile`, `writeCubes` (outputs raw/net cubes), `shiftThreshold`, `mporDays`, `mporCalendar`. Reuses existing XVA/exposure settings.
- Common elements: `active` flag to enable analytics, no dedicated XVA/exposure parameterizations—they reuse regular ones. `writeCubes` controls cube output.

### XVA Explain (pages 119–120)

Summary: The partial document covers three main topics: XVA Sensitivity Analytic, XVA Explain Analytic, and SA-CCR Capital calculation. Key points include how ORE computes XVA and exposure under sensitivity scenarios, the use of a parSensitivity flag for additional outputs, and the replacement of the current market with a ScenarioSimMarket in sensitivity and explain analytics. Recommendations for minimizing simulation market effects (e.g., activating UseSpreadedTermStructures and swaption volatility simulation) are provided. The XVA Explain analytic details market-implied changes in value adjustments between two dates, along with configuration parameters (marketConfigFile, stressConfigFile, sensitivityConfigFile, writeCubes, shiftThreshold, mporDays, mporCalendar) and output (CSV with CVA explain table). Finally, the SA-CCR analytic computes capital requirements using a csaFile and collateralBalancesFile.

### CCR Capital: SA-CCR (pages 120–121)

Summary: The partial document covers CVA Explain results with a table showing CVA base, scenario, and change for various risk factors and netting sets. It details the CVA Explain analytic, including parameters like shiftThreshold, mporDays, and mporCalendar, and explains how ORE computes market implied XVA changes between evaluation dates, outputs a CSV with value adjustments, and uses a ScenarioSimMarket. Additionally, it describes the SA-CCR analytic for CCR capital calculation with required input files (csaFile, collateralBalancesFile) and the SA-CVA and BA-CVA analytics for CVA capital, including on-the-fly or external sensitivity inputs and necessary configuration.

### CVA Capital: SA-CVA and BA-CVA (pages 121–123)

Summary: The partial document covers ORE analytics for capital calculations, including SA-CCR, SA-CVA, BA-CVA, and SMRC, each with XML configuration examples. It also introduces the market configuration file (todaysmarket.xml) and its structure for defining discounting curves, index curves, yield curves, FX rates, inflation curves, equity curves, default curves, and various volatility structures.

## Market: todaysmarket.xml (pages 123–123)

Summary: The document describes the market configuration file `todaysmarket.xml`, which defines the subset of the market universe to be built by ORE. It emphasizes user responsibility to ensure the subset covers the portfolio, otherwise the application will exit. The file name is user-defined and entered into the master configuration file `ore.xml`. The file uses opening and closing `<TodaysMarket>` tags and contains multiple configuration blocks (e.g., discounting curves, index curves, FX spot rates, volatility structures, securities). Each block can have alternative versions with unique identifiers. The section then begins detailing the layout of discounting curves (subsection 5.2.1).

### Discounting Curves (pages 123–124)

Summary: The partial document describes the market configuration file `todaysmarket.xml`, which defines the subset of the market universe built by ORE for portfolio analysis. It lists the types of configuration blocks (discounting curves, index curves, yield curves, swap index curves, FX spot rates, inflation index curves, equity curves, default curves, and various volatility structures) that can be included, each with unique IDs for alternative versions. The document then details three subsections: 5.2.1 on Discounting Curves, showing how to specify curves per currency with identifiers; 5.2.2 on Index Curves, associating index names with yield curves for projecting fixings; and 5.2.3 on Yield Curves, providing an example block with named curves.

### Index Curves (pages 124–124)

Summary: The partial document covers three main sections: Discounting Curves (Section 5.2.1), Index Curves (Section 5.2.2), and Yield Curves (Section 5.2.3). It explains how ORE builds discount curves for five currencies (EUR, USD, GBP, CHF, JPY) using unique curve identifiers like "Yield/EUR/EUR1D". The Index Curves section shows how yield curves are associated with index names (e.g., EUR-EURIBOR-3M) for forwarding rate projections. The Yield Curves section defines additional curves for lending/borrowing (e.g., BANK_EUR_LEND). All curves refer to a curve configuration file (curveconfig.xml) for definitions.

### Yield Curves (pages 124–125)

Summary: The partial document describes configuration blocks for financial curves and market data in ORE. It covers discounting curves for multiple currencies (EUR, USD, GBP, CHF, JPY), index forwarding curves linking yield curves to specific indices (e.g., EUR-EURIBOR-3M), yield curves for additional purposes like XVA and bond pricing, swap index curves that associate CMS swaps with forwarding and discounting curves, and FX spot rates for currency pairs. Each block uses unique identifiers to reference curve definitions in a configuration file.

### Swap Index Curves (pages 125–125)

Summary: The partial document covers three main topics: building additional yield curves for XVA post-processor and bond pricing, defining swap index curves to create swap index objects tied to forwarding and discounting curves for swaption volatility surfaces, and specifying FX spot rates for various currency pairs.

### FX Spot (pages 125–126)

Summary: The partial document describes several configuration blocks in ORE for building financial market data. Main points include: a yield curves block for additional curves used in XVA post-processing and bond pricing; a swap index curves block that creates swap index objects linked to existing forwarding and discounting curves, particularly short-term (1Y) and long-term (30Y) indices for swaption volatility surfaces; an FX spot block providing EUR-based quotes for currency conversion; an FX volatilities block for four EUR FX pairs; a swaption volatilities block for five currencies; and a cap/floor volatilities block (section heading only, details not shown).

### FX Volatilities (pages 126–126)

Summary: The partial document covers three main sections: FX Volatilities, Swaption Volatilities, and Cap/Floor Volatilities. It explains how ORE is instructed to build volatility structures for four FX pairs with target currency EUR (EURUSD, EURGBP, EURCHF, EURJPY), five swaption volatility structures (for EUR, USD, GBP, CHF, JPY), and a cap/floor volatilities block (shown partially). Each section provides XML examples and notes that the specific volatility structure definitions are found in a separate curve configuration file.

### Swaption Volatilities (pages 126–126)

Summary: The partial document covers three volatility-related sections: FX Volatilities, Swaption Volatilities, and Cap/Floor Volatilities. It explains that the FX Volatilities block instructs ORE to build four volatility structures for currency pairs with target currency EUR. The Swaption Volatilities block builds five swaption volatility structures for different currencies. The Cap/Floor Volatilities block is introduced but not fully detailed.

### Cap/Floor Volatilities (pages 126–127)

Summary: The partial document covers several configuration blocks for ORE: FX quotes (four quotes with target currency EUR), FX volatilities (four pairs with target EUR), Swaption volatilities (five currencies), Cap/Floor volatilities (three currencies), Default curves (three curves with names), and Securities (a security name linked to spread/rate). Each block instructs ORE to build corresponding structures or curves as defined in the curve configuration file, with user-defined tokens referenced in the CurveId tag.

### Default Curves (pages 127–127)

Summary: The document describes three configuration blocks for ORE: the Cap/Floor Volatility block (Listing 43) instructs building three volatility structures for EUR, USD, and GBP currencies, referencing user-defined tokens in the curve configuration file; the Default Curves block (Listing 44) builds a set of default probability curves with named identifiers (e.g., BANK, CPTY_A) linked to curve configuration definitions; and the Securities block (Listing 45) associates a named security (e.g., SECURITY_1) with a spread and rate pair from the curve configuration, used in bond pricing.

### Securities (pages 127–128)

Summary: The partial document covers several configuration blocks used by ORE to set up market data structures. It includes Cap/Floor volatility definitions for EUR, USD, and GBP; default probability curves for names like BANK and counterparties; a security block linking a bond security name to a spread/rate pair; equity curves for SP5 and Lufthansa with spot prices and dividend yields; equity volatility structures for the same names; and a reference to zero inflation index curves. Each XML block specifies an ID and references user-defined tokens found in the curve configuration file.

### Equity Curves (pages 128–128)

Summary: The partial document covers three main sections: Equity Curves (5.2.11), which describes how ORE constructs equity curves consisting of spot prices and dividend yield term structures for assets like SP5 and Lufthansa; Equity Volatilities (5.2.12), which explains the creation of equity volatility structures for the same assets; and Inflation Index Curves (5.2.13), which introduces a block for zero inflation index curves. Each section includes an XML excerpt and instructions on how the curves and volatilities are defined and used.

### Equity Volatilities (pages 128–128)

Summary: The partial document covers three main points:  
- **Equity Curves (5.2.11):** Explains how to define equity curves for assets like SP5 and Lufthansa, each consisting of a spot price and a term structure of dividend yields to compute forward prices.  
- **Equity Volatilities (5.2.12):** Describes building equity volatility structures for the same assets, referenced from a curve configuration file.  
- **Inflation Index Curves (5.2.13):** Introduces a block for zero inflation index curves, with an excerpt from an example file.

### Inflation Index Curves (pages 128–129)

Summary: The partial document covers four main topics: Equity Curves (5.2.11), which instructs ORE to build equity curves from spot prices and dividend yield term structures; Equity Volatilities (5.2.12), which constructs equity volatility structures for given names; Inflation Index Curves (5.2.13), detailing both zero inflation index curves and year-on-year inflation index curves, each associated with an index name and defined in the curve configuration file; and Inflation Cap/Floor Volatility Surfaces (5.2.14), which is introduced but not fully detailed in the excerpt.

### Inflation Cap/Floor Volatility Surfaces (pages 129–130)

Summary: The partial document covers configuration blocks for ORE: Zero Inflation Index Curves (e.g., EUHICPXT, UKRPI) and Year-on-Year Inflation Index Curves, each mapping an index name to a curve path in the curve configuration file. It then details Inflation Cap/Floor Volatility Surfaces for both YoY and zero-coupon inflation indices, associating paths like EUHICPXT_YY_CF or UKRPI_ZC_CF. Additionally, it describes CDS Volatility Structures (e.g., CDXIG, CDXHY) and Base Correlation Structures (e.g., CDXIG), all defined via XML blocks with the ID "default".

### CDS Volatility Structures (pages 130–130)

Summary: The document covers three main configuration blocks: inflation cap/floor volatility surfaces (year-on-year and zero), CDS volatility structures, and base correlation structures. Each block has a default ID and contains named entries that reference volatility surfaces or structures defined in the curve configuration file.

### Base Correlation Structures (pages 130–131)

Summary: The partial document covers the configuration of inflation cap/floor volatility surfaces (year-on-year and zero), CDS volatility structures, base correlation structures, correlation structures, and market configurations in ORE. It explains how these are defined in XML blocks with specific IDs and how market configurations bundle various curve and volatility objects for different purposes (e.g., calibration, pricing, simulation).

### Correlation Structures (pages 131–131)

Summary: The partial document covers two main topics: correlation structures and market configurations. It first explains how correlation structures are configured with a `Correlations` block using a default ID, showing examples for EUR and USD cross-currency correlations, and notes that the composition is defined in the curve configuration. Then it describes market configurations, where various blocks (discount curves, index curves, volatility structures, etc.) are bundled into configuration IDs in the `todaysmarket.xml` file. Examples of multiple configurations (default, collateral_inccy, collateral_eur, libor) are provided, each specifying a different discounting curve ID. It explains that ORE builds all market configurations side by side, enabling different setups for model calibration, risk factor evolution, collateralized vs. uncollateralized pricing, and other purposes. The master input file `ore.xml` requires four configuration IDs for 'lgmcalibration', 'fxcalibration', 'pricing', and 'simulation'. The configuration ID concept applies to all curve and volatility objects but is currently used only to distinguish discounting.

### Market Configurations (pages 131–132)

Summary: The partial document covers three main topics: **Correlation Structures** (Section 5.2.17) which are configured using a `<Correlations>` block with named correlations referencing external curve files; **Market Configurations** (Section 5.2.18) that bundle various curve and volatility objects into configurations identified by IDs, allowing different setups for calibration, pricing, and simulation, with examples of discount curve IDs; and the **Simulation Parameters** (Section 5.3.1) within the `simulation.xml` file, detailing the `<Parameters>` block including Grid, TimeStepsPerYear, Calendar, DayCounter, Sequence, Seed, Samples, Ordering, DirectionIntegers, and optional CloseOutLag and MporMode.

## Simulation: simulation.xml (pages 132–132)

Summary: The document describes the configuration of the risk factor simulation module via the `simulation.xml` file, which consists of three blocks: Parameters, CrossAssetModel, and Market. Section 5.3.1 provides a detailed explanation of the Parameters block, including an example XML listing and descriptions of key parameters such as Grid (simulation time grid), TimeStepsPerYear (minimum steps for stochastic process evolution), Calendar (for date adjustments), DayCounter (date-to-time conversion), Sequence (random number generator type), Seed, Samples, Ordering, DirectionIntegers, and optional nodes CloseOutLag and MporMode. Notes on defaults and usage for exposure calculation are also included.

### Parameters (pages 132–133)

Summary: The partial document describes the structure and configuration of a simulation module (`simulation.xml`), focusing on two main blocks: **Parameters** and **CrossAssetModel**. 

- **Parameters** block: Details input parameters for the Monte Carlo simulation, including time grid (`Grid`), time steps per year, calendar, day counter, random sequence generator type (e.g., SobolBrownianBridge), seed number, number of samples, ordering of variates, direction integers for Sobol generator, optional close-out lag for margin period of risk, and MPOR mode (StickyDate vs ActualDate).

- **CrossAssetModel** block: Specifies the cross-asset model composition, including:
  - LGM models for each currency,
  - FX models for exchange rates to base currency,
  - Equity, inflation, credit, and commodity models,
  - Correlation structure among components.
  - Also notes that simulated currencies must match portfolio requirements, otherwise an exception is raised.

### Model (pages 133–145)

Summary: The partial document covers simulation configuration parameters and the CrossAssetModel structure. Key points include:
- Random number generator settings: seed, number of Monte Carlo paths, sequence ordering, and direction integers for Sobol generators.
- Close-out lag and MporMode for close-out grid setup.
- CrossAssetModel configuration: currencies, LGM models for each currency with calibration options, FX models (CrossCcyLGM), equity models (CrossAssetLGM), inflation models (DodgsonKainth or JarrowYildirim) with calibration details, commodity models (CommoditySchwartz), and instantaneous correlation structure.
- Market section: translation of simulated risk factors to yield curves and volatility surfaces, including equity and commodity volatility simulation methods (ATM only or full surface).

### Market (pages 145–150)

Summary: The partial document covers two main sections: the simulation model correlation configuration and the market configuration, followed by sensitivity analysis.

- **Simulation Model Correlation Configuration** (Listing 66): Defines instantaneous correlations between risk factors (e.g., interest rates, FX) within a `<CrossAssetModel>`. Explicitly set correlations (e.g., EUR/USD, EUR/GBP) and defaults all unspecified pairs to zero correlation. Commodity correlations are allowed among themselves but must be zero with other components.

- **Market Configuration** (Section 5.3.3): Details the `<Market>` XML structure for translating simulated risk factors into yield curves and volatilities. Key points include:
  - Currency specification must include all currencies used in the cross‑asset model and portfolio.
  - Volatility simulation methods: For equity, commodity, swaption, and FX volatilities, options include simulating only ATM volatilities (with T0 smile shift) or the full surface/smile, controlled by `<SimulateATMOnly>` and `<Surface>`/`<Moneyness>` nodes.
  - Smile dynamics (StickyStrike, StickyMoneyness, StickySABR) can be specified per risk factor; StickySABR only for swaption/yield/cap‑floor volatilities with SABR calibration.
  - Day counting, interpolation (LogLinear/LinearZero), and extrapolation (FlatFwd/FlatZero) for yield curves, default curves, etc.
  - `<CurveAlgebra>` node allows linking curves (e.g., spread operations) in the simulation market.
  - The full `<Market>` XML example includes configurations for yield curves, indices, swap indices, default curves, swaption/cap‑floor/FX/equity volatilities, benchmark curves, securities, inflation curves, CDS volatilities, correlations, and aggregation scenario data.

- **Sensitivity Analysis** (Section 5.4, `sensitivity.xml`): Lists supported market components for sensitivity computation (discount curves, index curves, FX spots/vols, swaption vols, etc.) and configuration parameters: shift type (Absolute/Relative), shift size, shift scheme (Forward/Backward/Central), and specific tenor/expiry/strike buckets.

## Sensitivity Analysis: sensitivity.xml (pages 150–157)

Summary: The partial document covers two main sections: sensitivity analysis (5.4) and stress scenario analysis (5.5). 

**Sensitivity Analysis (5.4):**  
- ORE supports sensitivity to various market data: discount curves, index curves, yield curves, FX spots/volatilities, swaption/cap/floor volatilities, default probability curves, equity spots/volatilities, inflation curves, CDS volatilities, bond credit spreads, base correlation curves, and correlation term structures.  
- Configuration is specified in `sensitivity.xml` with parameters: ShiftType (absolute/relative), ShiftSize, ShiftScheme (forward/backward/central), ShiftTenors (for curves), ShiftExpiries/Strikes/Terms (for volatilities), and Index.  
- Optional `key` attribute allows different shift values per sensitivity template (e.g., larger shift for Bermudan swaptions).  
- Cross gamma filter: lists pairs of sensitivity keys to compute second-order sensitivities; keys follow a naming convention (e.g., `DiscountCurve/EUR/5/7Y`).  
- Additional flags: `ComputeGamma` (suppress second order) and `UseSpreadedTermStructures`.  
- Par sensitivity analysis: requires extra configuration for par instruments (DEP, FRA, IRS, OIS, etc.) and conventions for DiscountCurves, IndexCurves, CapFloorVolatilities, CreditCurves, and inflation curves.  
- Par conversion excludes, fixing removal (regex), and matrix regularisation (silent/warning/disable) can be controlled.  
- Shift tenors must match simulation grid; instrument list length must match shift tenors.

**Stress Scenario Analysis (5.5):**  
- Stress tests are applied to the same market segments as sensitivity, configured in `stressconfig.xml`.  
- Each scenario defines shifts for selected market components; shifts can be zero or par rate shifts.  
- Instead of a single shift size, a vector of shifts can be applied to each curve/surface point.  
- For FX volatility shifts, explicit shift values per expiry/tenor or weighting schemas (unadjusted/weighted) are supported.  
- Examples show parallel, twist, and par rate scenarios.

## Stress Scenario Analysis: stressconfig.xml (pages 157–161)

Summary: The partial document covers stress scenario configuration (stressconfig.xml), including how to define stress tests with shifts for various market components (e.g., discount curves, FX spots, volatilities). It details explicit and weighted shift methods for FX volatility, with examples of absolute shifts and weighting schemas (weighted and unadjusted). It also explains par rate shifts and the use of spreaded term structures. Additionally, it introduces calendar adjustment (calendaradjustment.xml) for adding extra holidays or business days to existing calendars and creating custom calendars (prefixed with "CUSTOM_").

## Calendar Adjustment: calendaradjustment.xml (pages 161–162)

Summary: The partial document covers two main sections: "Calendar Adjustment" (section 5.6) and "Curves" (section 5.7). 

- Section 5.6 describes the `calendaradjustment.xml` file, which lists additional holidays and business days to be added to a specified calendar in ORE. It provides an example adding dates to the "Japan" calendar and explains how to create a new calendar using a `BaseCalendar` parameter, which must be prefixed with "CUSTOM_". Adding duplicate dates does not raise errors.

- Section 5.7 introduces the `curveconfig.xml` file, which configures various term structures (yield curves, default curves, inflation curves, equity forward curves, volatility structures, etc.) and other market objects (FX spots, security spreads, rates). It then details the top-level XML elements for a `YieldCurve` node, including `CurveId`, `Currency`, `DiscountCurve`, `Segments`, `InterpolationMethod`, `BootstrapConfig`, and others.

## Curves: curveconfig.xml (pages 162–162)

Summary: The partial document describes the configuration file `curveconfig.xml`, which defines various term structures for pricing a portfolio, including yield curves, default curves, inflation curves, equity forward price curves, swaption volatility structures, cap/floor volatility structures, FX option volatility structures, CDS volatility structures, inflation cap/floor price surfaces, equity volatility structures, security spreads and recovery rates, base correlation curves, and correlation termstructures. It also includes other market objects like FX spots, security spreads, and security rates. Subsection 5.7.1 provides the top-level XML elements for a YieldCurve node, listing fields such as CurveId, CurveDescription, Currency, DiscountCurve, Segments, InterpolationVariable, InterpolationMethod, MixedInterpolationCutoff, YieldCurveDayCounter, Tolerance, Extrapolation, ExcludeT0FromInterpolation, and BootstrapConfig.

### Yield Curves (pages 162–177)

Summary: The partial document describes the configuration of various term structures required for pricing a portfolio, primarily through a single configuration file (`curveconfig.xml`). It covers the composition of yield curves, default curves, inflation curves, equity forward price curves, and several volatility structures. The main focus is on yield curve configuration, detailing top-level XML elements (e.g., CurveId, Currency, InterpolationMethod, BootstrapConfig) and various segment types (Direct, Simple, AverageOIS, TenorBasis, CrossCurrency, ZeroSpread, FittedBond, BondYieldShifted, YieldPlusDefault, WeightedAverage, IborFallback, DiscountRatio) used to build curves from market instruments. It also introduces default curves from CDS, including bootstrapping from spread or price quotes.

### Default Curves from CDS (pages 177–179)

Summary: The partial document covers the following main points:

- A **Discount Ratio segment** within a yield curve configuration, illustrated with an XML example that defines a discount curve (GBP collateralized in EUR) using a numerator curve (GBP-IN-USD) and denominator curve (EUR-IN-USD) relative to a base curve (EUR1D).

- **Default curves from CDS** (Section 5.7.2): Detailed explanation of bootstrapping default curves from credit default swap market instruments, including the meaning of configuration nodes such as CurveId, CurveDescription, Currency, Type (SpreadCDS, Price, ConvSpreadCDS), DiscountCurve, DayCounter, RecoveryRate, StartDate, RunningSpread, IndexTerm, Quotes (with optional attribute), Conventions, Extrapolation, ImplyDefaultFromMarket, BootstrapConfig, and AllowNegativeRates. An XML template (Listing 100) is provided.

- The beginning of **Benchmark Default Curve** (Section 5.7.3), which describes setting up a default curve as a difference curve between two yield curves, typically used to back out a default curve from an all-in discounting curve fitted to liquid bond prices (the “source curve”) and a benchmark.

### Benchmark Default Curve (pages 179–181)

Summary: The partial document covers three main topics related to default curve construction:

1. **Credit Event Auction Settlement Handling**: Describes a flag that, when true, assumes an entity is in default and awaiting a credit event auction if CDS spreads/upfront prices are absent but a recovery rate exists. In this case, a survival probability curve with a value slightly above zero for one day after the valuation date is built to approximate CDS pricing.

2. **BootstrapConfig and Negative Rates**: Optional nodes for configuring iterative bootstrap (defaults if omitted) and controlling negative instantaneous hazard rates. If `AllowNegativeRates` is false (default), negative rates cause an exception or a zero rate (if `DontThrow` is true), leading to inexact market matching. If true, negative rates are allowed within technical limits.

3. **Default Curve Types**:
   - **Benchmark Default Curve**: Constructed as a difference curve of two yield curves (source and benchmark). Survival probabilities are derived from the ratio of discount factors, with an optional recovery rate. Configurable via nodes like `BenchmarkCurve`, `SourceCurve`, `Pillars`, etc.
   - **Multi-Section Default Curve**: Built by stitching together instantaneous hazard rates from multiple source curves across date ranges defined by switch dates. Survival probabilities are computed using a product of source curve survival probabilities and their recovery rates.

### Multi-Section Default Curve (pages 181–182)

Summary: The partial document covers three main topics: a benchmark default curve configuration (Listing 101), the construction and configuration of multi-section default curves (including equation (12) and node descriptions, with an example in Listing 102), and the beginning of a section on swaption volatility structures, showing an example configuration with parameters like Dimension, VolatilityType, Interpolation, and ParametricSmileConfiguration.

### Swaption Volatility Structures (pages 182–185)

Summary: The partial document covers the following main points:  
- An optional extrapolation setting for curves (defaults to true).  
- A multi-section default curve example with multiple source curves and switch dates.  
- Detailed configuration elements for Swaption Volatility Structures, including CurveId, Dimension, VolatilityType, Interpolation, ParametricSmileConfiguration, Extrapolation, OutputVolatilityType, OutputShift, ModelShift, DayCounter, Calendar, BusinessDayConvention, ATM matrix specification, Smile section specification, and QuoteTag.  
- An introduction to Cap Floor Volatility Structures, describing three types of input term cap volatilities (ATM strip, absolute strike grid, combined) and three types of input optionlet volatilities (ATM strip, absolute strike grid, combined), along with the roles of the InputType and InterpolateOn nodes.

### Cap Floor Volatility Structures (pages 185–202)

Summary: The partial document covers the configuration and parameterization of cap/floor volatility structures, including:

- How market datum labels incorporate quote tags (e.g., EUR-EURIBOR-3M).
- Two types of market data input: term cap volatilities and optionlet volatilities.
- For term cap volatilities, three input structures: ATM strip, maturity-by-strike grid, and combined; and two interpolation approaches (on term volatilities or optionlet volatilities) affecting the stripping process.
- For optionlet volatilities, similar structures but no bootstrapping.
- Detailed XML configurations for six cases: ATM curve with interpolation on term or optionlet vols, surface (with or without ATM column) with interpolation on term or optionlet vols, and optionlet ATM curve/surface.
- Explanation of relevant XML nodes (e.g., CurveId, VolatilityType, InterpolationMethod, IncludeAtm, Tenors, InputType, etc.) and their allowed values.
- Proxy cap/floor volatility configuration: referencing an existing surface and adjusting for different underlying indices, optionally scaling.

### FX Volatility Structures (pages 203–207)

Summary: The partial document covers three main topics: proxy cap floor volatility configuration, FX volatility structures, and the beginning of equity curve structures. The proxy section explains fields like Index, RateComputationPeriod, ONCapSettlementDays, and ScalingFactor, along with the proxy mechanism steps, and includes an XML example for creating a USD-SOFR volatility surface from USD-LIBOR-3M with a scaling factor of 0.95. The FX volatility structures section provides multiple configuration examples (ATM, Smile types such as VannaVolga, Delta, BFRR, Absolute, and ATMTriangulated) and details the meaning and allowable values for each XML element (e.g., CurveId, Dimension, SmileType, Expiries, Deltas, FXSpotID, etc.). The equity curve structures section introduces a sample configuration for an equity forward price curve (SP500) with fields such as CurveId, Currency, ForecastingCurve, Type (e.g., DividendYield), ExerciseStyle, SpotQuote, Quotes, and dividend interpolation settings.

### Equity Curve Structures (pages 207–209)

Summary: The partial document covers configuration fields for FX volatility structures, including Calendar, Conventions, BaseVolatility surfaces, and SmileExtrapolation. It then details the configuration of equity forward price curves, listing elements such as CurveId, Currency, ForecastingCurve, Type, SpotQuote, Quotes, DayCounter, DividendInterpolation, DividendExtrapolation, and Extrapolation, along with explanations of their meanings and allowable values. Finally, it introduces equity volatility structures, describing four configuration options (constant, expiry-dependent, surface, proxy) and common fields like CurveId, EquityId, Currency, Calendar, DayCounter, OneDimSolverConfig, and PreferOutOfTheMoney.

### Equity Volatility Structures (pages 209–214)

Summary: The partial document covers the following main points:

- **Equity Curves**: Describes the composition of equity curves, including spot equity price, forward prices, or dividend yields. It explains the use of a "ForwardDividendPrice" curve type for dividend futures indices, which is excluded from SIMM calculations. It also notes the internal storage of equity spot price, forecasting curve, and dividend yield term structure for forward price projection.

- **Equity Volatility Structures**: Outlines four configuration options for equity volatility structures: constant volatility, volatility curve (expiry-dependent, no strike dimension), volatility surface (expiry and strike dimensions), and proxy surface (pointing to another surface). It details common fields for all configurations (e.g., CurveId, Currency, DayCounter) and provides specific configurations for:
  - **Constant volatility**: Uses a single quote held constant for all strikes and expiries.
  - **Volatility curve**: Allows quotes with varying expiry, interpolation (Linear, Cubic, LogLinear), and extrapolation (None or Flat).
  - **Volatility strike surface**: Defines a full surface with Strikes and Expiries, including nodes for QuoteType, ExerciseType, interpolation methods, and extrapolation settings. It explains the generation of quote strings and the use of wildcards.
  - **Moneyness surface**: Similar to strike surface but uses moneyness levels (Spot or Fwd) instead of strikes, with restrictions on QuoteType and VolatilityType.
  - **Proxy surface**: Permits using another volatility surface as a proxy, with fields for referencing a different equity volatility curve, FX volatility curve, and correlation curve if currencies differ.

- **Inflation Curves**: Details the configuration of inflation curves, listing specific elements such as CurveId, NominalTermStructure, Type (ZC), Segments with Conventions and Quotes, Extrapolation, Calendar, DayCounter, Lag, Frequency, BaseRate, Tolerance, InterpolationVariable, InterpolationMethod, UseLastFixingDate, and Seasonality (with BaseDate, Frequency, and Factors).

### Inflation Curves (pages 214–215)

Summary: The document describes the configuration of inflation curves, focusing on the structure and elements of an `InflationCurve` configuration block. Key points include:

- The main elements of an inflation curve: `CurveId`, `CurveDescription`, `NominalTermStructure`, `Type`, `Segments` (with sub-elements `Conventions` and `Quotes`), `Extrapolation`, `Calendar`, `DayCounter`, `Lag`, `Frequency`, `BaseRate`, `Tolerance`, `InterpolationVariable`, `InterpolationMethod`, `UseLastFixingDate`, and `Seasonality`.
- Explanation of each element's purpose, such as `NominalTermStructure` (interest rate curve for stripping), `Type` (ZC for zero coupon or YY for year on year), `Lag` (observation lag), `Frequency` (index fixing frequency), and `InterpolationVariable` (ZeroRate or PriceIndex).
- A legacy schema section that uses a single block for `Quotes` and `Conventions` instead of `Segments`.
- The `Segment` schema defining instruments for curve building with `Conventions` and `Quotes`.
- The optional `Seasonality` block containing `BaseDate`, `Frequency`, and `Factors` for multiplicative seasonality.

#### Legacy Schema (pages 215–215)

Summary: The partial document covers the legacy schema for inflation curves, detailing its elements such as NominalTermStructure, Type, Segments, Quotes, Conventions, Lag, Frequency, BaseRate, InterpolationVariable, and InterpolationMethod. It also introduces the segment schema, which defines instruments for curve building with Conventions and Quotes, and mentions an optional seasonality block for multiplicative seasonality.

#### Segment Schema (pages 215–216)

Summary: The partial document covers the following main points:

- **Legacy Schema (5.7.11.1)**: Describes the legacy schema for inflation curves, including elements such as `NominalTermStructure`, `Type` (ZC or YY), `Segments`, `Quotes`, `Conventions`, `Lag`, `Frequency`, `BaseRate`, `InterpolationVariable`, and `InterpolationMethod`.

- **Segment Schema (5.7.11.2)**: Defines the segment block with `Conventions` and `Quotes` for curve building, and the optional seasonality block containing `BaseDate`, `Frequency`, `Factors`, and `OverrideFactors`.

- **Notes (5.7.11.3)**: Highlights that all swaps in segments must reference the same inflation index, and that zero coupon swap quotes can be converted to year-on-year quotes without convexity adjustment if the type is YY.

- **Inflation Cap/Floor Volatility Surfaces (5.7.12)**: Provides configuration details for zero coupon inflation cap/floor volatility surfaces, including elements like `CurveId`, `Type`, `QuoteType`, `VolatilityType`, `Extrapolation`, `DayCounter`, `Calendar`, `BusinessDayConvention`, `Tenors`, `Strikes`, `CapStrikes`, `FloorStrikes`, `Index`, `IndexCurve`, `IndexInterpolated`, `ObservationLag`, `YieldTermStructure`, and `QuoteIndex`. An example listing (125) is given.

#### Notes (pages 216–216)

Summary: The partial document covers two main topics: 
1. Seasonality correction parameters for inflation indices, including BaseDate, Frequency, Factors, and OverrideFactors, with notes on their usage.
2. Inflation cap/floor volatility surface configuration, detailing a zero coupon inflation cap floor price surface example with XML elements such as CurveId, Type, QuoteType, VolatilityType, Extrapolation, DayCounter, Calendar, BusinessDayConvention, Tenors, Strikes, Index, IndexCurve, ObservationLag, and YieldTermStructure.

### Inflation Cap/Floor Volatility Surfaces (pages 216–217)

Summary: The partial document covers two main topics: seasonality correction factors for inflation indices (defining BaseDate, Frequency, Factors, OverrideFactors) and the configuration of inflation cap/floor volatility surfaces (including Type, QuoteType, VolatilityType, Extrapolation, DayCounter, Calendar, Tenors, Strikes, CapStrikes, FloorStrikes, Index, IndexCurve, ObservationLag, YieldTermStructure, QuoteIndex). It also includes notes on swap conventions and a brief introduction to CDS volatilities.

### CDS Volatilities (pages 217–222)

Summary: The partial document covers three main topics:

1. **Inflation Cap/Floor Volatility Surface Parameters**: Defines configuration fields such as Type (ZC, YY), QuoteType (Volatility, Price), VolatilityType (Normal, Lognormal, ShiftedLognormal), Extrapolation, DayCounter, Calendar, BusinessDayConvention, Tenors, Strikes, CapStrikes, FloorStrikes, Index, IndexCurve, IndexInterpolated, Observation Lag, YieldTermStructure, and QuoteIndex. It also explains how quotes are constructed for building the cap/floor volatility surface.

2. **CDS Volatility Configurations**: Describes three options for CDS and index CDS options volatility structures:
   - Constant volatility (single quote)
   - Volatility curve (dependency on expiry and term, no strike dimension)
   - Volatility surface (expiry, term, and strike dimensions)
   Each configuration is detailed with XML layout examples, supported interpolation/extrapolation methods, optional parameters (e.g., EnforceMontoneVariance, StrikeFactor, QuoteName), and rules for quote lookup in market data. Also includes a deprecated legacy curve configuration using an Expiries node.

3. **Base Correlations Configuration**: Explains how to configure base correlations either from quoted base correlations directly or by implying them from upfront quotes. Provides an XML example (Listing 130) with elements like CurveId, Terms, DetachmentPoints, SettlementDays, Calendar, BusinessDayConvention, DayCounter, and Extrapolate.

### Base Correlations (pages 222–225)

Summary: The partial document covers the following main points:

- Configuration of a CDS volatility surface (Listing 129).
- Base correlations: two approaches – using quoted base correlations directly (Listing 130) or implying them from upfront quotes (Listing 131). Detailed element explanations are provided for each, including CurveId, Terms, DetachmentPoints, SettlementDays, Calendar, BusinessDayConvention, DayCounter, Extrapolate, QuoteName, StartDate, Rule, AdjustForLosses, QuoteTypes, IndexSpread, Currency, CalibrateConstituentsToIndexSpread, UseAssumedRecovery, RecoveryGrid, and RecoveryProbabilities.
- FXSpots configuration (Listing 132): each FXSpot has a CurveId of the form "Ccy1Ccy2" and an optional description.
- Securities configuration (Listing 133): each security may include optional SpreadQuote, RecoveryRateQuote, ConversionFactor, and PriceQuote; default assumptions (zero spread and recovery) and forward bond naming convention (securityId_FWDEXP_expiryDate) are noted.

### FXSpots (pages 225–225)

Summary: The document covers two main sections: FXSpot configuration (section 5.7.15) and Securities configuration (section 5.7.16). The FXSpots section describes that each FXSpot CurveId follows the format “Ccy1Ccy2”, with examples like EURUSD, EURGBP, EURCHF, EURJPY. The Securities section outlines optional attributes for each security (SpreadQuote, RecoveryRateQuote, ConversionFactor, PriceQuote) and their default behaviors, including fallback to credit curve recovery rate, default conversion factor of 1.0, and precedence of explicit SpreadQuote over implied spreads. It also notes that if no configuration is given, zero spread and recovery are assumed and excluded from simulation and sensitivity analysis, and specifies the naming convention for forward bonds (securityId_FWDEXP_expiryDate).

### Securities (pages 225–226)

Summary: The partial document covers three main configuration sections: FXSpots, Securities, and Correlations. The FXSpots section defines how FX spot curves are configured, with each CurveId in "Ccy1Ccy2" format. The Securities section details optional parameters like SpreadQuote, RecoveryRateQuote, ConversionFactor, and PriceQuote, noting defaults and behaviors for pricing, simulation, and sensitivity analysis. The Correlations section describes configuration for correlation types (CMSSpread or Generic), support for ATM or flat correlations, and quote loading methods (RATE, PRICE, NULL), along with required fields for calibration and handling of option tenors.

### Correlations (pages 226–227)

Summary: The partial document covers three main topics: Security Configuration, Correlations, and Commodity Curves. The Security Configuration section (Listing 133) defines a security curve with elements such as CurveId, CurveDescription, and various quote identifiers (spread, recovery rate, price, conversion factor). The Correlations section (Listing 134) describes the configuration of correlation curves, supporting CMSSpread and Generic types, with options for quote types (RATE, PRICE, NULL), dimension (ATM, Constant), calibration via CMS Spread Options, and parameters like OptionTenors, Conventions, SwaptionVolatility, and DiscountCurve. The Commodity Curves section presents two examples: one for WTI Oil (Listing 135), built solely from futures prices, and one for Gold (Listing 136), using FX-style spot and forward point quotes. Both commodity curves include elements like CurveId, Currency, Quotes, DayCounter, InterpolationMethod, and Extrapolation, with the Gold example also specifying SpotQuote and Conventions.

### Commodity Curves (pages 227–232)

Summary: The partial document covers two main topics: Commodity Curves and Commodity Volatilities in ORE. For Commodity Curves, it explains that they are price curves returning a price for a given time, and describes several configuration types: curves built directly from futures prices (e.g., WTI Oil), curves using FX-style spot and forward point quotes (e.g., Gold in USD), curves set up as a commodity curve times the ratio of two yield curves (e.g., Gold in EUR), curves constructed from a base future price curve and basis quotes (with details on averaging/non-averaging combinations), and piecewise price curves involving multiple future types (Future, AveragingFuture, AveragingSpot). It defines the meaning of XML elements for these configurations, including optional fields like SpotQuote, InterpolationMethod, Conventions, and basis-specific fields such as AddBasis, MonthOffset, and PriceAsHistoricalFixing. For Commodity Volatilities, it outlines four supported types: constant volatility, one-dimensional expiry-dependent volatility, two-dimensional volatility (with absolute, delta, or moneyness strikes), and average price option (APO) volatility surface. It provides configuration examples for constant and one-dimensional expiry-dependent volatility structures, explaining elements like CurveId, Currency, Quote, DayCounter, and Calendar.

### Commodity Volatilities (pages 232–244)

Summary: The partial document describes the types of commodity volatility structures supported in ORE, including constant, one-dimensional expiry-dependent, two-dimensional (absolute strike, moneyness strike, delta strike) volatility structures, and an average price option (APO) volatility surface. It provides detailed configuration examples (Listings 141–146) and explains the meaning of each XML element for curve construction, interpolation, extrapolation, quote handling, and optional parameters. Additionally, it introduces the BootstrapConfig node (Listing 147) for altering default bootstrap algorithm behavior.

### Bootstrap Configuration (pages 244–246)

Summary: The partial document covers three main topics: 
1. **StrikeExtrapolation, PriceCurveId, and YieldCurveId** – Defines strike extrapolation options (None, UseInterpolator, Linear, Flat) and identifies commodity price and yield curves.
2. **Bootstrap Configuration (BootstrapConfig)** – Describes optional parameters for bootstrap algorithms in curve construction, including Accuracy, GlobalAccuracy, DontThrow, MaxAttempts, MaxFactor, MinFactor, DontThrowSteps, Global (global vs. iterative bootstrap), and SmoothnessLambda.
3. **One Dimensional Solver Configuration (OneDimSolverConfig)** – Outlines parameters for a one-dimensional solver used in curve construction (e.g., equity volatility stripping), including MaxEvaluations, InitialGuess, Accuracy, optional MinMax (bounds), Step, LowerBound, and UpperBound.

### One Dimensional Solver Configuration (pages 246–249)

Summary: The partial document covers three main topics: the configuration of a one-dimensional solver (OneDimSolverConfig node) used in curve construction, including its elements like MaxEvaluations, InitialGuess, Accuracy, MinMax, Step, LowerBound, and UpperBound; a table of allowable interpolation methods (e.g., Linear, LogLinear, CubicSpline, etc.); and an introduction to Reference Data (referencedata.xml) for bond static data, including bond reference data structure, valid subtypes (e.g., Corp, Sovereign, ABX), and an example XML snippet.

## Reference Data referencedata.xml (pages 249–251)

Summary: The partial document covers two main topics:

1. **Reference Data (Section 5.8, referencedata.xml)**: Describes how reference data stores common static elements (e.g., bond static information) to simplify portfolio XML representation, and is used for bond derivatives and yield curve construction. It defines allowed types: Bond static data (Leg data) and optional SubType (e.g., ABS, Corp, Loans, Muni, Sovereign, or index types) for reporting without pricing impact. An XML example shows a BondReferenceData entry with fields like SubType, IssuerId, CreditCurveId, SettlementDays, Calendar, IssueDate, and LegData.

2. **Ibor Fallback Config (Section 5.9, iborFallbackConfig.xml)**: Explains configuration for replacing Ibor reference rates with risk-free rates, with fields to enable fallbacks, use RFR curves in today's market or simulation, and specify fallback entries (IborIndex, RfrIndex, Spread, SwitchDate). An XML example illustrates global settings and fallback mappings (e.g., CHF-LIBOR to CHF-SARON with defined spreads and switch dates).

## Ibor Fallback Config: iborFallbackConfig.xml (pages 251–252)

Summary: The partial document covers two main topics: Ibor Fallback Configuration and SIMM Calibration. The Ibor Fallback Config section explains rules for replacing Ibor reference rates with risk-free rates, including global settings (enable/disable fallbacks, use of Rfr curves) and per-index fallback definitions (index names, spread, switch date). The SIMM Calibration section describes how to add or override SIMM versions by specifying risk weights, correlations, and thresholds, with a file structure of <SIMMCalibrationData> containing <SIMMCalibration> subnodes.

## SIMM Calibration: simmcalibration.xml (pages 252–253)

Summary: The partial document covers the SIMM Calibration feature, explaining its purpose (adding or overriding SIMM versions with risk weights, correlations, concentration thresholds, buckets/labels, and currency groups). It describes the XML structure consisting of a `<SIMMCalibrationData>` node containing `<SIMMCalibration>` subnodes, each defining a specific SIMM version. A listing shows example components like version names, effective date, and risk class sections (Interest Rate, Credit, Equity, Commodity, FX, RiskClassCorrelations). Subsection 5.10.1 details that a `<SIMMCalibration>` node defines a single set of parameters and includes a `<VersionNames>` component with multiple `<Name>` sub-nodes for associating version names with the calibration.

### SIMM Calibration (pages 253–254)

Summary: The partial document describes the structure and components of a SIMM Calibration, defined by a `<SIMMCalibration>` node. It includes version names (e.g., 2.6, 2.5.6) that allow overriding default calibrations, additional fields for descriptive purposes, risk-class-specific sub-nodes (InterestRate, CreditQualifying, CreditNonQualifying, Equity, Commodity, FX), and risk class correlations. An example of risk class correlations is provided in Listing 150. The document also introduces a general structure for all risk class sub-nodes, which contain three components: RiskWeights, Correlations, and ConcentrationThresholds.

### General Structure (pages 254–257)

Summary: The partial document covers the SIMM calibration XML structure, including the specification of a version parameter, the optional <AdditionalFields> node for descriptive purposes, and the six risk-class-specific sub-nodes (InterestRate, CreditQualifying, CreditNonQualifying, Equity, Commodity, FX). It details the <RiskClassCorrelations> node with example correlations. The general structure common to all risk classes is described, comprising <RiskWeights> (with Delta, Vega, and optional HistoricalVolatilityRatio), <Correlations> (IntraBucket and InterBucket), and <ConcentrationThresholds> (Delta and Vega). Finally, the <InterestRate> node is illustrated with its specific sub-elements, including Inflation, XCcyBasis, CurrencyLists, and correlations like SubCurves, Inflation, XCcyBasis, and Outer.

### Interest Rate (pages 257–259)

Summary: The partial document covers the structure and calibration of several SIMM (Standard Initial Margin Model) nodes, including <ConcentrationThresholds>, <InterestRate>, and <CreditQualifying>. It provides XML listings with examples, details on risk weights (Delta, Vega, HistoricalVolatilityRatio, Inflation, XCcyBasis, BaseCorrelation), correlations (IntraBucket, SubCurves, InterBucket, etc.), and concentration thresholds specific to each risk class. The document also specifies allowable bucket values, attributes, and references to sections of the ISDA SIMM Methodology for each parameter.

### Credit Qualifying (pages 259–260)

Summary: The partial document covers three main areas: concentration threshold currency groups with bucket attributes for volatility levels; the structure and parameters for Credit Qualifying risk (including delta, vega, base correlation risk weights, intra- and inter-bucket correlations, and concentration thresholds, each with specific attributes and allowable values referenced from ISDA SIMM Methodology); and the analogous structure and parameters for Credit Non-Qualifying risk, which includes delta and vega risk weights, correlations, and concentration thresholds with different bucket values.

### Credit Non-Qualifying (pages 260–261)

Summary: The partial document outlines the calibration structure for Credit Non-Qualifying and Equity risk within the SIMM framework. It specifies XML nodes for risk weights (Delta, Vega, and Historical Volatility Ratio for Equity), correlations (intra-bucket and inter-bucket), and concentration thresholds (Delta and Vega), along with corresponding references to ISDA SIMM Methodology sections. Key details include allowable bucket values, attribute requirements for nodes (e.g., bucket, label1, label2), and constraints such as single threshold or weight nodes where applicable.

### Equity (pages 261–262)

Summary: The partial document provides specifications for the SIMM calibration XML structures for Equity and Commodity risk. For Equity, it details the <Equity> node with subnodes for risk weights (Delta, Vega, HistoricalVolatilityRatio), correlations (IntraBucket, InterBucket), and concentration thresholds (Delta, Vega), each with allowable bucket values and references to ISDA SIMM Methodology sections. For Commodity, it similarly describes the <Commodity> node structure, including risk weights, correlations, and thresholds, with specific allowable bucket values and section references. The document also notes constraints like only one <Threshold> or <HistoricalVolatilityRatio> node and required attributes such as bucket, label1/label2, or mporDays.

### Commodity (pages 262–263)

Summary: The partial document covers the structure and allowable values for the Commodity and FX risk nodes in the SIMM Calibration. It specifies XML listings for Commodity (including Delta, Vega, HistoricalVolatilityRatio, IntraBucket and InterBucket correlations, and concentration thresholds) and FX (including similar elements plus CurrencyLists). It details the required bucket attributes, allowable bucket values (1–12 or 1–17 depending on the asset class), and cross-references to specific sections in the ISDA SIMM Methodology for risk weights, correlations, concentration thresholds, and historical volatility ratios.

### FX (pages 263–265)

Summary: The partial document covers two main sections: SIMM calibration parameters for FX risk and conventions for zero rate quotes in XML. For FX risk, it details attributes and allowable values for inter-bucket correlations (label1/label2 with values "1"/"2" for volatility groups), delta and vega concentration thresholds (with bucket attributes referencing currency risk groups), risk weights, historical volatility ratio, intra-bucket correlations, and volatility correlation. It references specific sections of the ISDA SIMM Methodology. The conventions section describes XML nodes for zero rate quotes, distinguishing between tenor-based and explicit maturity date conventions, including elements like TenorBased, DayCounter, CompoundingFrequency, and related tags.

## Conventions: conventions.xml (pages 265–265)

Summary: The partial document covers section 5.11 on conventions for associating with market quotes in term structure construction. It explains that conventions are specified in an XML file (e.g., conventions.xml), each set stored in an XML node with a unique Id. The type of conventions is determined by the node name. Subsection 5.11.1 details Zero Conventions, describing two types: direct zero rate quotes with an explicit maturity date and tenor-based zero quotes. XML listings are provided for both, and the meanings of key elements (TenorBased, DayCounter, CompoundingFrequency, Compounding, and tenor-related fields) are explained.

### Zero Conventions (pages 265–266)

Summary: The partial document covers conventions for associating market quotes with term structure construction. It specifies that conventions are stored in an XML file (conventions.xml) with unique identifiers. Two main types are detailed: Zero Conventions (section 5.11.1) for direct zero rate quotes, which can be either with explicit maturity dates or tenor-based, with elements like TenorBased, DayCounter, CompoundingFrequency, Compounding, and optional fields for tenor-based quotes. Deposit Conventions (section 5.11.2) for deposit or index fixing quotes, which can be index-based or explicitly defined, with elements such as IndexBased, Calendar, Convention, EOM, and DayCounter.

### Deposit Conventions (pages 266–267)

Summary: The partial document covers conventions for zero rates, deposits, and futures. Key points include:

- **Zero rate conventions**: Compounding type, TenorCalendar, optional SpotLag, SpotCalendar, RollConvention, and EOM.
- **Deposit conventions**: Can be index-based (using an index family like EUR-EURIBOR) or explicit (specifying Calendar, Convention, EOM, DayCounter).
- **Future conventions**: For money market or overnight index futures, with fields for Id, Index, optional DateGenerationRule (IMM, FirstDayOfMonth, SecondThursday), and optional Calendar for overnight index futures with specific date generation.

### Future Conventions (pages 267–269)

Summary: The document describes convention structures for financial quotes. For deposit quotes, it lists fields: Index, Calendar, Convention, EOM, and DayCounter. For futures, it covers money market (MM) and overnight index (OI) futures, with fields: Id, Index, DateGenerationRule (options: IMM, FirstDayOfMonth, SecondThursday, with specific rules for MM and OI), optional Calendar, and OvernightIndexFutureNettingType (Compounding or Averaging). Examples for Euribor-3M, AUD-BBSW-3M, SOFR-3M, and SOFR-1M are provided. For FRA conventions, only Index is needed. For OIS conventions, fields include SpotLag, Index, FixedDayCounter, optional FixedCalendar, PaymentLag, EOM, FixedFrequency, FixedConvention, FixedPaymentConvention, Rule, PaymentCalendar, and RateCutoff.

### FRA Conventions (pages 269–269)

Summary: The partial document covers two sections: FRA Conventions and OIS Conventions. For FRA, it describes a node that stores the underlying index name (e.g., EUR-EURIBOR-6M). For OIS, it details a node with multiple elements such as SpotLag, Index, FixedDayCounter, FixedCalendar, PaymentLag, and others, along with explanations of their meanings.

### OIS Conventions (pages 269–270)

Summary: The partial document describes conventions for three types of financial instruments: FRA (Forward Rate Agreement), OIS (Overnight Indexed Swap), and Swap (vanilla interest rate swap). For FRA conventions, the key point is that the node only requires an underlying index name. For OIS conventions, the node includes numerous elements such as SpotLag, Index, FixedDayCounter, and several optional fields with defaults (e.g., PaymentLag, EOM, FixedFrequency, etc.), along with definitions for each. For Swap conventions, the node specifies fixed leg parameters (FixedCalendar, FixedFrequency, FixedConvention, FixedDayCounter) and the floating leg's Ibor index.

### Swap Conventions (pages 270–271)

Summary: The partial document describes conventions for generating OIS schedules and for vanilla interest rate swap (IRS) and average OIS quotes. It lists parameters for OIS schedule generation, including optional fields such as EOM, FixedFrequency, FixedConvention, FixedPaymentConvention, Rule, PaymentCalendar, and RateCutoff, with their defaults. It then details the structure of a Swap node, defining elements like FixedCalendar, FixedFrequency, FixedConvention, FixedDayCounter, Index, FloatFrequency, and SubPeriodsCouponType. Finally, it covers the AverageOIS node, specifying elements such as SpotLag, FixedTenor, FixedDayCounter, FixedCalendar, FixedFrequency, FixedConvention, FixedPaymentConvention, Index, OnTenor, and RateCutoff, along with their meanings and optional defaults.

### Average OIS Conventions (pages 271–272)

Summary: The partial document covers conventions for several swap types: 
- **FloatFrequency and SubPeriodsCouponType** for floating legs where payment frequency differs from index tenor, with options for "Compounding" or "Averaging".
- **Average OIS conventions**, detailing elements like SpotLag, FixedTenor, FixedDayCounter, FixedCalendar, FixedFrequency, FixedConvention, FixedPaymentConvention, Index, OnTenor, and RateCutoff.
- **Tenor Basis Swap conventions**, including PayIndex, PayFrequency, ReceiveIndex, ReceiveFrequency, SpreadOnRec, IncludeSpread, and SubPeriodsCouponType.
- **Tenor Basis Two Swap conventions**, which define spreads between fair fixed rates on two swaps against Ibor indices of different tenors.

### Tenor Basis Swap Conventions (pages 272–272)

Summary: The partial document covers two main topics: **Tenor Basis Swap Conventions** (section 5.11.8) and **Tenor Basis Two Swap Conventions** (section 5.11.9).  
- For tenor basis swaps, it defines the `TenorBasisSwap` node structure (XML) and explains each element: `PayIndex`, `PayFrequency` (optional), `ReceiveIndex`, `ReceiveFrequency` (optional), `SpreadOnRec` (optional, defaults to true), `IncludeSpread` (optional, defaults to false), and `SubPeriodsCouponType` (optional, values Compounding or Averaging).  
- For tenor basis two swaps, it introduces the `TenorBasisTwoSwap` node, used for quotes that are the spread between the fair fixed rates on two swaps against Ibor indices of different tenors.

### Tenor Basis Two Swap Conventions (pages 272–273)

Summary: The partial document covers three types of basis swap conventions:

1. **Tenor Basis Swap Conventions** (Section 5.11.8): Defines the `TenorBasisSwap` node used to store conventions for tenor basis swap quotes. It lists elements such as `PayIndex`, `PayFrequency`, `ReceiveIndex`, `ReceiveFrequency`, `SpreadOnRec`, `IncludeSpread`, and `SubPeriodsCouponType`, along with their meanings and optional default values.

2. **Tenor Basis Two Swap Conventions** (Section 5.11.9): Introduces the `TenorBasisTwoSwap` node for tenor basis swaps where the quote is the spread between fair fixed rates on two swaps against Ibor indices of different tenors (long and short swaps). It details elements like `Calendar`, `LongFixedFrequency`, `LongFixedConvention`, `LongFixedDayCounter`, `LongIndex`, `ShortFixedFrequency`, `ShortFixedConvention`, `ShortFixedDayCounter`, `ShortIndex`, and `LongMinusShort` (optional, defaulting to True).

3. **BMA / SIFMA Basis Swap Conventions** (Section 5.11.10): Begins describing the `BMABasisSwap` node for BMA/SIFMA basis swap quotes, referencing a structure shown in Listing 171 (not fully provided in the partial text).

### BMA / SIFMA Basis Swap Conventions (pages 273–274)

Summary: The partial document covers the structure and elements of two swap convention nodes: the Tenor Basis Two Swap node, which defines conventions for a long swap and a short swap, including calendar, fixed leg frequencies and conventions, day counters, Ibor indices, and an optional LongMinusShort attribute; and the BMA/SIFMA Basis Swap node, detailing conventions for BMA/SIFMA basis swaps, including an index, BMA index, and various optional payment calendars, conventions, lags, settlement days, payment period, and overnight lockout days. It also introduces the upcoming FX Conventions node.

### FX Conventions (pages 274–275)

Summary: The partial document covers three main sections: 
1. **BMA / SIFMA Basis conventions** – Defines the `<BMABasisSwap>` node with elements such as `Index`, `BMAIndex`, and various optional fields for payment calendars, conventions, lags, settlement days, payment period, and overnight lockout days for both the BMA/SIFMA leg and the reference leg.
2. **FX Conventions** – Defines the `<FX>` node for FX spot and forward quotes, including elements like `SpotDays`, `SourceCurrency`, `TargetCurrency`, `PointsFactor`, and optional fields for advance calendar, spot relative flag, end-of-month convention, and business day convention.
3. **Cross Currency Basis Swap Conventions** – Mentions the `<CrossCurrencyBasis>` node for storing cross currency basis swap quotes, with a reference to Listing 178 for its structure (details not provided in the partial text).

### Cross Currency Basis Swap Conventions (pages 275–277)

Summary: The partial document describes two main sections: FX conventions (Listing 177) and cross currency basis swap conventions (Listing 178). For FX conventions, it lists elements such as SpotDays, SourceCurrency, TargetCurrency, PointsFactor, and optional fields (AdvanceCalendar, SpotRelative, EOM, Convention) with their meanings. For cross currency basis swap conventions, it details elements including SettlementDays, SettlementCalendar, RollConvention, FlatIndex, SpreadIndex, and numerous optional fields (e.g., EOM, IsResettable, FlatIndexIsResettable, and OIS-specific parameters) along with their meanings. The document also introduces a heading for inflation swap conventions (Listing 179) but provides no content for that section.

### Inflation Swap Conventions (pages 277–279)

Summary: The partial document covers two main topics: first, a list of optional parameters for spread and flat legs of a financial instrument, including SpreadTenor, payment lags, and OIS-specific fields like IncludeSpread, Lookback, FixingDays, RateCutoff, and IsAveraged, along with their default values. Second, it describes Inflation Swap Conventions, detailing the structure and meaning of elements in an InflationSwap node (e.g., FixCalendar, DayCounter, Index, ObservationLag, PublicationRoll, PublicationSchedule), and provides an example for AU CPI inflation swap conventions. The document also begins a section on CMS Spread Option Conventions.

### CMS Spread Option Conventions (pages 279–280)

Summary: The document covers three main topics: inflation swap conventions, CMS spread option conventions, and Ibor index conventions. It explains how the market 5Y ZCIIS start and end dates and referenced inflation index quarter depend on the `PublicationRoll` setting ("OnPublicationDate" vs "AfterPublicationDate"). It details the `PublicationSchedule` node requirements, including coverage for valuation dates. It then presents examples (Listings 180-182) for AU CPI inflation swap, CMS spread option, and Ibor index conventions, along with definitions of their respective elements.

### Ibor Index Conventions (pages 280–281)

Summary: The partial document covers three main topics: inflation swap conventions (specifically a CMS spread option), Ibor index conventions, and overnight index conventions. For each, it provides XML structure examples and explains the meaning of their elements, such as ForwardStart, SpotDays, SwapTenor, FixingDays, Calendar, DayCounter, and RollConvention for CMS spread options; Id, FixingCalendar, DayCounter, SettlementDays, BusinessDayConvention, and EndOfMonth for Ibor indices; and Id, FixingCalendar, DayCounter, SettlementDays for overnight indices. It also includes important notes: dependent conventions must appear before the ones they depend on in the input file, and customized indices cannot be used in cap/floor volatility surface configurations.

### Overnight Index Conventions (pages 281–282)

Summary: The partial document covers conventions for three types of indices: Overnight Index, Inflation Index (ZeroInflationIndex), and Swap Index. For Overnight Index, it defines elements such as Id, FixingCalendar, DayCounter, and SettlementDays, along with rules about dependency order (the convention must appear before dependent conventions) and a restriction that customised indices cannot be used in cap/floor volatility surface configurations. For Inflation Index, the ZeroInflationIndex node includes Id, RegionName, RegionCode, Revised, Frequency, AvailabilityLag, and Currency, with a note that it must be placed before its use and can override existing indices. Finally, it introduces Swap Index conventions (also known as CMS indices).

### Inflation Index Conventions (pages 282–282)

Summary: The partial document covers two main topics: Inflation Index Conventions and Swap Index Conventions. Under Inflation Index Conventions, it describes the `ZeroInflationIndex` node used to define a new inflation index without recompiling C++ code, emphasizing placement before use and precedence over existing indices. It lists and explains the node's elements (Id, RegionName, RegionCode, Revised, Frequency, AvailabilityLag, Currency). Under Swap Index Conventions, it introduces the `SwapIndex` node for storing conventions for Swap (CMS) indices.

### Swap Index Conventions (pages 282–283)

Summary: The partial document covers three main topics:

1. **Inflation Index Conventions** (section 5.11.17): Introduces the `ZeroInflationIndex` node for defining new inflation indices without modifying C++ code. It lists the XML elements (`Id`, `RegionName`, `RegionCode`, `Revised`, `Frequency`, `AvailabilityLag`, `Currency`) and explains their meanings, including the precedence rule if an existing index ID is reused.

2. **Swap Index Conventions** (section 5.11.18): Describes the `SwapIndex` node for storing conventions for swap (CMS) indices. It details the elements (`Id` with format requirements, `Conventions`, optional `FixingCalendar`) and explains the naming convention and fallback behavior.

3. **FX Option Conventions** (section 5.11.19): Covers the `FxOption` node for FX option quote conventions. It lists the elements (`FXConventionID`, `AtmType`, `DeltaType`, `SwitchTenor`, `LongTermAtmType`, `LongTermDeltaType`, `RiskReversalInFavorOf`, `ButterflyStyle`) and provides meanings, including default values and choice options for ATM and delta types.

### FX Option Time Weighting Scheme (pages 284–285)

Summary: The partial document covers two main topics: FX option time weighting conventions and commodity forward conventions. It begins with optional parameters for FX options, including SwitchTenor, LongTermAtmType, LongTermDeltaType, RiskReversalInFavorOf, and ButterflyStyle. Then, it details the structure and rules for FX option time weighting, specifying weekday weights, trading centers, events, and the priority for determining daily weights. Finally, it describes commodity forward conventions, listing elements such as SpotDays, PointsFactor, and Outright, along with their optionality and default values.

### Commodity Forward Conventions (pages 285–286)

Summary: The partial document covers two main topics: 
1. Rules for determining daily weights based on weekday weights, trading centers, and events, with priority order for weekends, events, holidays, and weekdays.
2. Conventions for commodity forward and future contracts, detailing the structure and optional elements of the CommodityForward node (Id, SpotDays, PointsFactor, AdvanceCalendar, SpotRelative, BusinessDayConvention, Outright) and the CommodityFuture node (Id, AnchorDay with sub-options DayOfMonth, CalendarDaysBefore, NthWeekday).

### Commodity Future Conventions (pages 286–292)

Summary: The partial document covers two main topics: forward conventions and commodity future conventions. For forward conventions, it defines optional parameters that control date advancement (calendar), tenor relativity (spot vs. valuation date), business day roll convention, and interpretation of forward quotes (outright or points). For commodity future conventions, it provides a comprehensive structure for defining contract expiry dates, including identifier, anchor day methods (DayOfMonth, CalendarDaysBefore, NthWeekday, LastWeekday, BusinessDaysAfter, WeeklyDayOfTheWeek), contract frequency, calendars, expiry month lag, offset days, business day convention, adjustment order, averaging flags, option expiry parameters (offset, month lag, day, business day convention, contract frequency, NthWeekday, last weekday, calendar days before, minimum business days before, underlying future convention), continuation mappings, averaging data (commodity name, conventions, period, pricing calendar, use business days, delivery roll days, future month offset, daily expiry offset), hours per day, savings time, and valid contract months. It also briefly introduces credit default swap (CDS) conventions with elements like settlement days, calendar, frequency, payment convention, rule, day counter, and accrual/pay-at-default settings.

### Credit Default Swap Conventions (pages 292–293)

Summary: The partial document covers three main topics:
- **FutureMonthOffset**: An optional node for non-negative integer values, used with daily contract frequency commodities. It acts as a business day offset from the Pricing Date to reference a specific future contract, commonly applied in base metals for cash contracts.
- **Credit Default Swap Conventions (CDS)**: Defines a node storing CDS conventions with elements including Id, SettlementDays, Calendar, Frequency, PaymentConvention, Rule, DayCounter, LastPeriodDayCounter, SettlesAccrual, and PaysAtDefaultTime, each with ISDA standard defaults and allowed values.
- **Bond Yield Conventions (BondYield)**: Defines a node for converting bond prices to yields, with elements Id (format “CMB-FAMILY-TENOR”), Compounding, Frequency, PriceType, Accuracy, MaxEvaluations, and Guess, including parameters for convergence control.

### Bond Yield Conventions (pages 293–296)

Summary: The partial document covers four main sections: Credit Default Swap (CDS) fee leg conventions, Bond Yield conventions, Commodity Future conventions, and Schedule Data (rules, dates, derived). The CDS section defines date generation rules, day counters (with optional last period day counter), and boolean flags for accrual settlement and payment timing. The Bond Yield section describes the structure of a `BondYield` node, including elements like Id, Compounding, Frequency, PriceType, and convergence parameters. The Commodity Future section outlines the extensive structure of a `CommodityFuture` node, with fields for anchor day, contract frequency, calendars, expiry rules, continuation mappings, averaging data, and option-related parameters. The Schedule Data section explains how schedule dates can be rules-based, dates-based, or derived from another schedule, providing XML examples for each type.

### Schedule Data (Rules, Dates and Derived) (pages 296–301)

Summary: The partial document covers two main topics: **Schedule Data** and **Historical Return Configuration**.  

- **Schedule Data**: Explains the `ScheduleData` node used within `LegData` to define schedules via three methods: rules-based (using `StartDate`, `EndDate`, `Tenor`, `Calendar`, `Convention`, etc.), dates-based (explicit `Date` child elements), or derived from another schedule (using `BaseSchedule`, `Shift`, `Calendar`, `Convention`). It details all sub-elements, their meanings, allowable values, and optional fields (e.g., `EndOfMonth`, `FirstDate`, `RemoveFirstDate`).  
- **Historical Return Configuration**: Describes the `ReturnConfiguration` element for specifying how historical returns are computed (log, absolute, or relative) and an optional `Displacement` for each risk factor type (e.g., `DiscountCurve`, `EquitySpot`). It allows overriding defaults for specific named risk factors and notes numerical considerations.

## Historical Return Configuration (pages 301–302)

Summary: The main points covered in this partial document are:

1. **Historical Return Configuration (Section 5.12)**: The `ReturnConfiguration` XML element allows users to specify how historical returns are computed for risk factors in historical scenario generation and backtesting. It supports three return types (Log, Absolute, Relative) and an optional displacement parameter to avoid numerical issues. Default configurations can be set per risk factor type (e.g., DiscountCurve, EquitySpot), and specific overrides can be defined for named risk factors (e.g., EquitySpot/EQUITY_1).

2. **Collateral Balances**: The `collateralbalances.xml` file contains collateral balance definitions under a Credit Support Annex (CSA). Each netting set is represented by a `CollateralBalance` node within a `CollateralBalances` root element. The node includes fields for `NettingSetId`, `Currency`, `IndependentAmountHeld` (optional), `InitialMargin` (optional), and `VariationMargin` (optional), with descriptions of their allowable values and behavior (e.g., negative numbers indicate counterparty holds the amount).

# Logging (pages 91–93)

Summary: The partial document covers configuration options for deferring or disabling notifications during market updates, and parameters such as lazyMarketBuilding, continueOnError, buildFailedTrades, nThreads, enrichIndexFixings, ignoreFixingLead, and ignoreFixingLag. It then describes the Logging section with parameters like logFile, logMask, progressLogFile, structuredLogFile, rotation sizes, and console output. The Markets section specifies market configurations (lgmcalibration, fxcalibration, eqcalibration, pricing, simulation). Finally, the Analytics section lists permissible analytics types (NPV, Cashflows, Curves, Exposure Simulation, xVA, Sensitivity, etc.) and notes the parametrization of basic analytics like Pricing, Cashflows, and Curves.

# Proxy Cap Floor Volatility Configuration (pages 202–203)

Summary: The partial document describes parameter initialization (nu=0.30, rho=0.0) and calibration settings (max attempts 10, exit early error threshold 0.005, max acceptable error 0.05). It then explains the proxy cap floor volatility configuration, which allows creating a cap floor volatility surface by referencing an existing one and adjusting it for different indices, optionally applying a scaling factor. Key elements include CurveId, CurveDescription, ProxyConfig with Source (CurveId, Index, optional RateComputationPeriod) and Target (Index, optional RateComputationPeriod and ONCapSettlementDays), and an optional ScalingFactor. The proxy mechanism adjusts volatilities for forward rate differences and can scale the surface. An example configuration for USD-SOFR using USD-LIBOR-3M as source with a scaling factor of 0.95 is provided. Finally, FX volatility structures are mentioned with references to multiple listings.

# FX Option Conventions (pages 283–284)

Summary: The partial document covers three main topics: Swap index conventions (Listing 185) defining the structure for a swap index with elements Id, Conventions, and optional FixingCalendar; FX Option Conventions (Listing 186) detailing the structure for FX option quotes, including elements like AtmType, DeltaType, SwitchTenor, and related long-term conventions; and FX Option Time Weighting Scheme (Listing 187) specifying a time weighting scheme with weekday weights, trading centers, and events for FX option quotes.

# Collateral Balances (pages 302–304)

Summary: The partial document covers two main sections: **Collateral Balances** and **Counterparty Information**. 

- **Collateral Balances**: Describes the `collateralbalances.xml` file, which lists collateral balances (margin amounts and independent amounts) under a Credit Support Annex. Each netting set is defined within a `CollateralBalance` node containing `NettingSetId`, `Currency`, optional `IndependentAmountHeld`, `InitialMargin`, and `VariationMargin`. The meaning and allowable values (including defaults) for each element are specified.

- **Counterparty Information**: Describes the `counterparty.xml` file, containing counterparty-level details. It outlines the `CounterpartyInformation` node with `Counterparties` and `Correlations` children. The `Counterparties` node defines each counterparty via a `Counterparty` node with fields like `CounterpartyId`, optional `ClearingCounterparty`, `CreditQuality`, `BaCvaRiskWeight`, `SaCcrRiskWeight`, and `SaCvaRiskBucket`. Default values and allowable values for each field are provided.

# Counterparty Information (pages 304–304)

Summary: The partial document describes the counterparty information file (counterparty.xml), its XML structure with top-level CounterpartyInformation node containing Counterparties and Correlations children, and provides details on the Counterparties node. It includes a template for defining each counterparty with elements such as CounterpartyId, CreditQuality, BaCvaRiskWeight, SaCcrRiskWeight, and optional fields like ClearingCounterparty, along with their allowable values and default inputs.

## Counterparties (pages 304–305)

Summary: The partial document describes the structure and content of the counterparty information file (counterparty.xml). It covers two main sections: **Counterparties**, which defines individual counterparty inputs including fields such as CounterpartyId, CreditQuality, BaCvaRiskWeight, SaCcrRiskWeight, and SaCvaRiskBucket with their allowable values and defaults; and **Correlations**, which defines pairwise correlations between counterparties for credit risk factor calculations.

## Correlations (pages 305–306)

Summary: The partial document covers the optional SaCvaRiskBucket for SA-CVA delta risk buckets (values 1-8), the Correlations node for defining counterparty correlations with an XML template, and allowable values for date fields (multiple formats including serial numbers) and roll convention fields (e.g., Following, ModifiedFollowing, etc.).

## Allowable Values (pages 306–317)

Summary: The partial document defines allowable values for various financial trade parameters, including date formats (e.g., yyyymmdd, dd-mm-yy) and serial numbers; roll conventions (e.g., Following, ModifiedFollowing); currencies (fiat, minor, precious metals, cryptocurrencies); schedule rules (e.g., Backward, ThirdWednesday, CDS); calendars (country-specific, exchange, and special calendars); day count conventions (e.g., Actual/360, 30/360); index structures (CCY-INDEX-TENOR) with default fixing days; FX index format; inflation CPI index; credit curve IDs; equity names; commodity curve names; tier values; doc clauses; exchange codes; and boolean node values. It also introduces netting set definitions, covering both uncollateralised and collateralised ISDA agreements with XML templates.

# Netting Set Definitions (pages 317–317)

Summary: The partial document explains netting set definitions in an XML file called netting.xml, which defines ISDA netting agreements. It distinguishes between two cases: uncollateralised (no Credit Support Annex) and collateralised (with a Credit Support Annex). For uncollateralised netting sets, the XML template includes a NettingSetId, an optional ActiveCSAFlag (defaulting to True but should be False), and an optional CSADetails node that is not needed. For collateralised netting sets, a similar structure is used but with relevant CSA details. The document provides meanings and allowable values for each XML element.

## Uncollateralised Netting Set (pages 317–317)

Summary: The partial document describes the structure of a netting set definitions XML file (netting.xml) for ISDA netting agreements. It defines two types: uncollateralised netting sets (without a Credit Support Annex) and collateralised netting sets (with a CSA). For uncollateralised sets, it provides an XML template and explains the elements (NettingSetId, ActiveCSAFlag, CSADetails), including allowable values and optional fields. The collateralised section begins with a template but is incomplete.

## Collateralised Netting Set (pages 317–321)

Summary: The partial document describes netting set definitions for ISDA agreements, detailing two types: uncollateralised and collateralised. It provides XML templates for each, explaining required and optional elements. For collateralised netting sets, it elaborates on the CSADetails node, covering fields such as Bilateral, CSACurrency, Index, Thresholds, Minimum Transfer Amounts, Independent Amount, Margining Frequency, Margin Period of Risk, Collateral Compounding Spreads, Eligible Collaterals, Initial Margin settings, and calculation flags. The document then introduces a market data section, specifying the format of the market.txt file with three columns: Date, Quote, and Quote Value, along with allowable values.

# Market Data (pages 321–323)

Summary: The partial document covers the market data section used for calibrating ORE's risk factor evolution models. It explains the structure of the market.txt file, which contains three columns: Date, Quote, and Quote Value. The Quote column follows a format of Instrument Type/Quote Type followed by instrument-specific information. A table lists allowable values for Instrument Types (e.g., ZERO, MM, IR_SWAP, etc.) and Quote Types (e.g., RATE, PRICE, etc.). An excerpt from a market data file is provided. The document then introduces the Zero Rate subsection (9.1), detailing the properties for zero rate quotes, including Instrument Type (ZERO), Quote Type (RATE or YIELD_SPREAD), Currency, CurveId, DayCounter, and either a Tenor or ZeroDate.

## Zero Rate (pages 323–324)

Summary: The partial document presents an excerpt of a market data file containing money market rates, forward rate agreements (FRA), and interest rate swaps for EUR on 2011-01-31. It then defines three instrument types: **Zero Rate** (ZERO), **Discount Factor** (DISCOUNT), and **FX Spot Rate** (FX). For each, it specifies required properties such as instrument type, quote type, currency, curve identifier, and maturity specification (tenor or explicit date), along with examples of how these quotes are formatted.

## Discount Factor (pages 324–324)

Summary: The partial document covers two main sections: Discount Factor quotes (Section 9.2) and FX Spot Rate quotes (Section 9.3). For Discount Factors, it specifies the required properties (Instrument Type: DISCOUNT, Quote Type: RATE, Currency, CurveId, and Term or Discount-Date) and provides examples using either a term (e.g., 3Y) or a explicit date (e.g., 12-05-2018). It notes that only zero conventions are used for discount factors. For FX Spot Rate, it defines properties: Instrument Type: FX, Quote Type: RATE, Unit currency, and Target currency, with an example (FX/RATE/EUR/USD). Tables (38 and 39) summarize allowable values and descriptions for each.

## FX Spot Rate (pages 324–325)

Summary: The partial document describes the structure and properties for three types of financial quotes: Discount Factors, FX Spot Rates, and FX Forward Rates. For Discount Factors, it specifies instrument type DISCOUNT, quote type RATE, currency, CurveId, and either a Term or Discount-Date. For FX Spot Rates, it defines instrument type FX, quote type RATE, unit currency, and target currency. For FX Forward Rates, it covers two quotation methods: forward points (quote type RATE) and outright (quote type PRICE), both with instrument type FX_FWD, unit currency, target currency, and a Term. Examples are provided for each type.

## FX Forward Rate (pages 325–326)

Summary: The partial document covers three main topics: FX Forward Rate, Deposit Rate, and FRA Rate. For FX Forward Rate, it explains two quotation conventions: forward points (defined as FX Forward minus FX Spot, with conversion factor 1) and forward outright (FX Spot plus forward points), each with a table of properties (Instrument Type, Quote Type, Unit/Target currencies, Term). Examples show ticker formats like FXFWD/RATE/EUR/USD/1M. For Deposit Rate (Instrument Type MM, Quote Type RATE), it lists properties (Currency, IndexName, Forward start, Term) and describes common tenors (ON, TN, SN, etc.) with forward start conventions. For FRA Rate (Instrument Type FRA, Quote Type RATE), it outlines properties (Currency, Forward start, Term) and notes typical quotation like "6x9" and IMM FRA representation.

## Deposit Rate (pages 326–326)

Summary: The partial document covers two main sections: Deposit Rate (9.5) and FRA Rate (9.6). For Deposit Rate, it defines the instrument type (MM), quote type (RATE), currency, optional index name, forward start (e.g., 0D for ON), and term (e.g., 3M), with examples like ON, TN, SN, and the quote format MM/RATE/EUR/2D/3M. For FRA Rate, it specifies instrument type (FRA), quote type (RATE), currency, forward start and term (e.g., 6x9 meaning 6M forward start, 9M maturity), and mentions IMM FRA quotes. Both sections include tables of allowable values and descriptions.

## FRA Rate (pages 326–327)

Summary: The partial document covers three main sections: Deposit Rate (9.5), FRA Rate (9.6), and Money Market Futures Price (9.7). For each, it defines the instrument type, quote type, currency, and key properties such as forward start, term, and allowable values (e.g., integers followed by D, W, M, Y). It includes examples and explains conventions like ON, TN, SN for deposits, standard FRA quotes (e.g., 6x9), IMM FRA quotes, and futures expiry formatting (YYYY-MM). Tables summarize the property definitions for each instrument type.

## Money Market Futures Price (pages 327–328)

Summary: The partial document defines several financial instrument types, including IMM FRA Rate, Money Market Futures Price, Overnight Index Futures Price, and Swap Rate. For each, it lists properties such as Instrument Type, Quote Type, Currency, and specific fields like Start/End, Expiry, Contract, Term, Tenor, or Forward start, along with their allowable values and descriptions. Examples are provided for each instrument type.

## Overnight Index Futures Price (pages 328–328)

Summary: The partial document covers two main sections: "Overnight Index Futures Price" (section 9.8) and "Swap Rate" (section 9.9). For Overnight Index Futures Price, it defines allowable values and descriptions for properties such as Instrument Type, Quote Type, Currency, Expiry (formatted as YYYY-MM), Contract, and Term, with an example of Three Months SOFR Futures. For Swap Rate, it lists properties including Instrument Type, Quote Type, Currency, optional IndexName, Forward start, Tenor, and Term, along with a reference to the currency table.

## Swap Rate (pages 328–329)

Summary: The partial document covers three main financial instrument types: Overnight Index Futures Price, Swap Rate, and Basis Swap Spread. For each, it details their properties, allowable values, and descriptions, including instrument type, quote type, currency, expiry, term, and optional identifiers. Examples are provided for each instrument to illustrate usage. Additionally, the document includes a variant of Swap Rate with start and end dates.

## Basis Swap Spread (pages 329–330)

Summary: The partial document covers four types of financial instruments: Swap Rate with Start and End Date (IR_SWAP), Basis Swap Spread (BASIS_SWAP), Cross Currency Basis Swap Spread (CC_BASIS_SWAP), and CDS Spread (CDS). For each, the document defines properties, allowable values, and descriptions, along with examples. Key properties include instrument type, quote type, currency, tenors, terms, and optional identifiers. It also notes that forward start for non-dated swap rates is usually not quoted and that conventional CDS spreads are not currently supported.

## Cross Currency Basis Swap Spread (pages 330–330)

Summary: The partial document covers two main sections: Cross Currency Basis Swap Spread (9.11) and CDS Spread (9.12). For the Cross Currency Basis Swap Spread, it defines properties such as Instrument Type (CC_BASIS_SWAP), Quote Type (BASIS_SPREAD), flat currency, flat tenor, currency, tenor, and term, with an example quote format. For the CDS Spread, it details properties like Instrument Type (CDS), Quote Types (CREDIT_SPREAD or CONV_CREDIT_SPREAD), entity, tier, doc clause, currency, term, and running spread, along with notes that only par CDS spreads are currently supported and that conventional CDS spreads are not. It also provides example CDS spread quotes.

## CDS Spread (pages 330–331)

Summary: The partial document covers three main sections: Cross Currency Basis Swap Spread (9.11), CDS Spread (9.12), and CDS Upfront Price (9.13). Section 9.11 defines properties for cross currency basis swap spread quotes, including instrument type, quote type, flat currency and tenor, non-zero spread leg currency and tenor, and swap term, with an example. Section 9.12 defines properties for CDS spread quotes, listing instrument type, quote type (CREDIT_SPREAD or CONV_CREDIT_SPREAD), entity, tier, optional doc clause, currency, term, and optional running spread, with multiple examples and a note that only par CDS spreads are currently supported. Section 9.13 defines properties for CDS upfront price quotes, including instrument type, quote type (PRICE), entity, tier, currency, optional doc clause, term, and optional running spread, with examples and notes on how the running spread is handled when omitted or provided in both quote and configuration.

## CDS Upfront Price (pages 331–332)

Summary: The partial document covers three main topics: CDS upfront price quotes, CDS recovery rate quotes, and CDS option implied volatility quotes. For CDS upfront price, it defines the quote structure (Instrument Type, Quote Type, Entity, Tier, Currency, optional DocClause, Term, optional RunningSpread), notes that the running spread can be omitted and must then be provided in the default curve configuration, and lists examples. For CDS recovery rate, it defines the quote structure (Instrument Type, Quote Type, Entity, Tier, Currency, optional DocClause), notes the optional doc clause, and lists examples. For CDS option implied volatility, it outlines four possible forms of the quote string, explains the interpretation of terms (NAME, EXPIRY, STRIKE, TERM), and provides an introductory description.

## CDS Recovery Rate (pages 332–332)

Summary: The partial document covers three main topics: CDS price quotes with examples showing varying parameters such as entity, tier, currency, doc clause, and tenor; CDS recovery rate quotes, including a property table (Instrument Type, Quote Type, Entity, Tier, Currency, DocClause) and valid examples; and CDS option implied volatility quotes, detailing four possible forms with placeholders for name, expiry, term, and strike. It also notes that the CDS documentation clause is optional.

## CDS Option Implied Volatility (pages 332–333)

Summary: The partial document covers several types of CDS and recovery rate quotes. It lists examples of CDS price quotes with varying combinations of entity, tier, currency, doc clause, and tenor. It then defines the CDS Recovery Rate quote format, including optional doc clause, with examples. Next, it explains CDS Option Implied Volatility quotes, which can take four forms involving name, expiry, optional term, and optional strike. It also describes Security Recovery Rate quotes, which only require a security ID and support par recovery rates. Finally, it covers Hazard Rate quotes, specifying issuer, seniority, currency, and term, with examples.

## Security Recovery Rate (pages 333–333)

Summary: The partial document covers three main topics: parameters for CDS options (expiry, term, and strike), specifying bond recovery rates per security (using RECOVERY_RATE or ASSUMED_RECOVERY_RATE quote types), and defining hazard rates as instantaneous probabilities of default (with issuer, seniority, currency, and term).

## Hazard Rate (Instantaneous Probability of Default) (pages 333–334)

Summary: The partial document covers four main topics: CDS option parameters (expiry, term, strike), security recovery rates (using instrument types RECOVERY_RATE and ASSUMED_RECOVERY_RATE with security ID), hazard rates (instantaneous probability of default with issuer, seniority, currency, term), and FX option implied volatility (using instrument type FX_OPTION with unit/target currency, expiry, and strike strategies like ATM, RR, BF).

## FX Option Implied Volatility (pages 334–335)

Summary: The partial document covers two main sections: FX Option Implied Volatility (Table 56) and Cap Floor Implied Volatility (Table 57). For FX options, it defines properties such as instrument type (FX_OPTION), quote type (RATE_LNVOL), currencies, expiry periods, and strike types (ATM, RR, BF) with an example. For cap floor options, it describes properties including instrument type (CAPFLOOR), various quote types (lognormal, normal, shifted lognormal, shift, premium), currency, index name, term, index tenor, ATM flag, relative flag, strike, and optional option style. It also explains the use of index names for currencies with multiple indices and provides examples of cap floor implied volatility, shift, and premium quotes.

## Cap Floor Implied Volatility (pages 335–336)

Summary: The document describes two financial instruments: Cap Floor Implied Volatility (section 9.19) and Swaption Implied Volatility (section 9.20). For cap floors, it defines the properties for a volatility quote, including instrument type CAPFLOOR, quote types (lognormal, normal, shifted lognormal volatility, shift, and premium), currency, optional index name, term, index tenor, ATM indicator, relative flag, strike, and option style. Examples illustrate how to format various cap floor quotes (e.g., ATM lognormal volatility, strike lognormal volatility, shifted lognormal volatility, shift, and premium quotes). For swaptions, it covers instrument type SWAPTION, similar quote types, currency, optional quote tag, expiry, underlying swap term, dimension (smile or ATM), strike, and option style. Examples and notes explain the usage of quote tags and absolute volatility quoting convention, along with how to format shift quotes.

## Swaption Implied Volatility (pages 336–337)

Summary: The partial document covers the following main points: cap/floor volatility quotes with shift and premium examples; swaption implied volatility data, including instrument type, allowable quote types (lognormal, normal, shifted lognormal, shift, premium), and properties such as currency, expiry, term, dimension, strike, and option style; and equity spot and forward price quotes, detailing instrument type, quote type, name, currency, and maturity for forwards.

## Equity Spot Price (pages 337–337)

Summary: The partial document covers two main areas: swaption volatility quotes for EUR (specifically for 5Y/10Y maturity and tenor, with ATM and smile quotes), and definitions of equity spot price and equity forward price, including their properties (instrument type, quote type, name, currency, and maturity for forwards) with examples.

## Equity Forward Price (pages 337–338)

Summary: The partial document covers several financial instrument quote types: swaption volatility quotes (absolute ATM and smile for EUR 5Y10Y), followed by definitions and allowable values for equity spot price, equity forward price, equity dividend yield, and equity option implied volatility, including their properties, examples, and quotation conventions.

## Equity Dividend Yield (pages 338–338)

Summary: The document defines two equity-related quote types: **Equity Dividend Yield Rate** (Section 9.23) and **Equity Option Implied Volatility** (Section 9.24). Each includes tables specifying property names, allowable values, and descriptions. For the dividend yield, key fields are Instrument Type (EQUITY_DIVIDEND), Quote Type (RATE), Name (string), Currency, and Maturity (date or duration). For option implied volatility, fields include Instrument Type (EQUITY_OPTION), Quote Type (RATE_LNVOL), Name, Currency, Expiry, Strike (supports ATM, ATMF, moneyness level, or absolute strike), and optional CallPut flag. Examples are provided for each, and the text explains how strike price is expressed relative to spot or forward for moneyness levels.

## Equity Option Implied Volatility (pages 338–339)

Summary: The document covers several financial instrument quote types: Equity Dividend Yield (RATE), Equity Option Implied Volatility (RATE_LNVOL), Equity Option Premium (PRICE), and Commodity Spot Price (PRICE). For each, it specifies properties such as Instrument Type, Quote Type, Name, Currency, Maturity/Expiry, Strike (with options for ATM, ATMF, moneyness, or absolute strike), and Call/Put flag. It provides allowable values, descriptions, and examples for each quote type.

## Equity Option Premium (pages 339–339)

Summary: The partial document covers two main topics: Equity Option Premium and Commodity Spot Price. For Equity Option Premium, it defines allowable properties such as Instrument Type (EQUITY_OPTION), Quote Type (PRICE), Name, Currency, Expiry (date or relative terms), Strike (ATM, ATMF, or absolute real number), and Call/Put flag. It provides examples of quote strings. For Commodity Spot Price, it specifies properties including Instrument Type (COMMODITY), Quote Type (PRICE), Name, and Currency, also with examples.

## Commodity Spot Price (pages 339–340)

Summary: The partial document defines several financial instrument quote types and their properties, including Equity Option Premium (quoted as a function of strike price, with parameters like currency, expiry, strike type, and call/put flag), Commodity Spot Price, Commodity Forward Price (with maturity), and Commodity Option Implied Volatility (with expiry and volatility quote types such as DEL, ATM, MNY, or absolute strike). Each section includes a table of allowable values and examples.

## Commodity Forward Price (pages 340–340)

Summary: The partial document describes two commodity-related quote types: Commodity Forward Price (Table 65) and Commodity Option Implied Volatility (Table 66). For forward prices, it details properties such as Instrument Type (COMMODITY_FWD), Quote Type (PRICE), Name, Currency, and Maturity. For option implied volatility, it lists Instrument Type (COMMODITY_OPTION), Quote Type (RATE_LNVOL), Name, Currency, Expiry (including continuation notation), and Vol Quote Type or Absolute Strike (delta, ATM, MNY, or absolute strike levels). Examples are provided for each table.

## Commodity Option Implied Volatility (pages 340–342)

Summary: The partial document covers three main sections: Commodity Forward Price (Section 9.27), Commodity Option Implied Volatility (Section 9.28), and Zero Coupon Inflation Swap Rate (Section 9.29). 

- Commodity Forward Price defines the instrument type COMMODITY_FWD, quote type PRICE, and properties such as Name, Currency, and Maturity, with an example.
- Commodity Option Implied Volatility introduces the instrument type COMMODITY_OPTION, quote type RATE_LNVOL, and explains volatility quoting methods: delta quotes (DEL) with forward/spot conventions and call/put option types, ATM quotes (ATM) with conventions like AtmFwd, AtmSpot, AtmDeltaNeutral, and moneyness quotes (MNY) with relative moneyness levels. It also supports absolute strike values. Multiple examples are provided for delta forward, delta spot, forward strike with relative moneyness, and absolute moneyness quotes. Only log-normal implied volatilities are supported.
- Zero Coupon Inflation Swap Rate defines the instrument type ZC_INFLATIONSWAP, quote type RATE, and properties Index and Maturity, with an example.

## Year on Year Inflation Swap Rate (pages 343–343)

Summary: The partial document describes two types of inflation derivatives: Year on Year Inflation Swap Rates and Zero Coupon Inflation Cap Floor Prices. It details their properties including instrument type, quote type, inflation index, maturity, and for caps/floors additionally cap/floor tag and strike. Examples are provided for each, along with a list of common inflation index names such as EUHICP, EUHICPXT, and others.

## Zero Coupon Inflation Cap Floor Price (pages 343–344)

Summary: The partial document covers several financial instrument quote types including Zero Coupon Inflation Swap Rates (examples for EUHICPXT 1Y and 2Y), Year on Year Inflation Swap Rates (table with properties like Instrument Type, Quote Type, Index, Maturity), Zero Coupon Inflation Cap Floor Prices (table with added Cap/Floor and Strike properties), Inflation Seasonality Correction Factors (table with Type, Index, Month), Bond Yield Spreads, and Bond Prices. It provides allowable values, descriptions, and examples for each, along with a list of common inflation index names (e.g., EUHICP, EUHICPXT, FRHICP).

## Inflation Seasonality Correction Factors (pages 344–344)

Summary: The partial document covers three main topics: Inflation Seasonality Correction Factors (section 9.32), which defines properties such as Instrument Type (SEASONALITY), Quote Type (RATE), Type (MULT), Index (string for inflation index), and Month (JAN-DEC), along with examples; Bond Yield Spreads (section 9.33), which defines properties for bond yield spreads over benchmark rates (Instrument Type BOND, Quote Type YIELD_SPREAD, Name); and Bond Prices (section 9.34), which defines properties for bond prices (Instrument Type BOND, Quote Type PRICE, Name). Each section includes a corresponding table and examples.

## Bond Yield Spreads (pages 344–344)

Summary: The partial document covers three sections: Inflation Seasonality Correction Factors (9.32), Bond Yield Spreads (9.33), and Bond Prices (9.34). For inflation seasonality, it defines properties such as instrument type (SEASONALITY), quote type (RATE), type of correction factor (MULT), index name (string), and month (JAN–DEC), with examples. Bond Yield Spreads specify instrument type (BOND), quote type (YIELD_SPREAD), and a bond name, providing spread over benchmark rate. Bond Prices similarly define instrument type (BOND), quote type (PRICE), and bond name. Each section includes a table and example entries.

## Bond Prices (pages 344–345)

Summary: The partial document covers five main topics: Inflation Seasonality Correction Factors (defining properties like instrument type SEASONALITY, quote type RATE, type MULT, index, month), Bond Yield Spreads (instrument type BOND, quote type YIELD_SPREAD, name), Bond Prices (instrument type BOND, quote type PRICE, name), Bond Future Price (instrument type BOND_FUTURE, quote type PRICE, name), and Bond Future Conversion Factor (instrument type BOND_FUTURE, quote type CONVERSION_FACTOR, name, future contract). Each section provides allowable values, descriptions, and examples of quote identifiers.

## Bond Future Price (pages 345–345)

Summary: The partial document covers three main types of quotes: bond price quotes, bond future price quotes, and bond future conversion factor quotes. It explains that bond price quotes include characteristics such as clean/dirty type and quote method (percentage of par or currency per unit), and provides an example. It then describes bond future price quotes with a table and example, followed by bond future conversion factor quotes, also with a table and example.

## Bond Future Conversion Factor (pages 345–346)

Summary: The partial document describes various types of financial quotes, including bond prices (with details on clean/dirty price and quote method), bond future prices, bond future conversion factors, base correlations for CDS index equity tranches, and correlations between indices. Each quote type is defined by its instrument type, quote type, and specific properties such as name, term, detachment point, or index identifiers, with examples provided for each.

## Base Correlations (pages 346–346)

Summary: The partial document covers two main topics: Base Correlations (section 9.37) and Correlations (section 9.38). For Base Correlations, it defines a quote type for CDS index equity tranches, specifying properties such as index name, term, and detachment point, with an example and note that multiple detachment points are typical. For Correlations, it describes quotes that provide either the correlation between two indices (RATE) or a premium to bootstrap correlations (PRICE), currently supporting CMS Spread correlations, with examples.

## Correlations (pages 346–347)

Summary: The document covers three main types of quotes: Base Correlations for CDS index equity tranches, specifying detachment points and terms; Correlations between two indices, with quote types RATE or PRICE (e.g., CMS Spread correlations); and Conditional Prepayment Rates (CPR) for bonds, providing spread over benchmark rates. Each section includes property tables, descriptions, and examples.

## Conditional Prepayment Rates (pages 347–348)

Summary: The document covers two main topics: (1) the definition and structure of Conditional Prepayment Rates (CPR) as a quote type with fields like property, allowable values, description, instrument type, quote type, and name, including an example of a CPR quote; (2) the format and usage of historical fixings data, which is stored in a fixings.txt file with three columns (Index Name, Fixing Date, Index Value), along with allowable values for each column and an excerpt showing sample data from various indices.

# Zero Coupon Inflation Swap Rate (pages 342–343)

Summary: The partial document covers commodity option volatility quotes, specifically log-normal implied volatilities (RATE_LNVOL), with explanations and examples of delta forward, delta spot, forward strike with relative moneyness, and absolute moneyness quotes. It then details three inflation swap instruments: Zero Coupon Inflation Swap Rate, Year on Year Inflation Swap Rate, and Zero Coupon Inflation Cap Floor Price, each specifying allowable property values, descriptions, and examples.

# Fixing History (pages 348–351)

Summary: The partial document describes two main sections: "Fixing History" and "Dividends History". The fixing history section details the format of the fixings.txt file, which contains three columns (Index Name, Fixing Date, Index Value) separated by semicolons or blanks. It specifies allowable values for each column, provides an excerpt, and defines various index types (IR indices, IR swap indices, FX fixings, zero inflation indices, and generic indices) with their allowable components and formats. The dividends history section describes the dividends.txt file format with three columns (Equity Name, Ex-Dividend Date, Dividend Amount) and defines allowable values for each, including an excerpt.

# Dividends History (pages 351–353)

Summary: The partial document describes the structure and format of a dividends history file (dividends.txt), which contains historical dividend payments with three columns: Equity Name, Ex-Dividend Date, and Dividend Amount. It specifies allowable values for each column, explains that dividends are used in path-dependent trades, and provides an excerpt of sample data for equities DAI:GR and HSBA:LN. The document also includes a list of references.


## Related Concepts
- [[concepts/monte-carlo-simulation]]
- [[concepts/xva-valuation-adjustments]]
- [[concepts/market-risk-analytics]]
