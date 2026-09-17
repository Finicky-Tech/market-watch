---
layout: default
title: Market Watch Investor White Paper · Finicky Technologies Ltd
permalink: /investors/white-paper
---

# Market Watch: Turning Nigeria’s Food Price Intelligence Into Real-Time Infrastructure

**Prepared By [Koyejo A.](https://www.linkedin.com/in/koyejo-adinlewa), for [Finicky Technologies Ltd](https://finicky-tech.github.io/company-profile/intro)**  
*Investor & Stakeholder Edition — September 2026*

---

## Table of Contents

- [Executive Summary](#executive-summary)
- [1. The Origin: How the Idea Came to Be](#1-the-origin-how-the-idea-came-to-be)
- [2. The Problem: Flying Blind in a High-Inflation Food Economy](#2-the-problem-flying-blind-in-a-high-inflation-food-economy)
- [3. The Solution: How Market Watch Works](#3-the-solution-how-market-watch-works)
- [4. Proven Precedent: The Science Behind Crowdsourced Prices](#4-proven-precedent-the-science-behind-crowdsourced-prices)
- [5. Market Opportunity & Commercial Growth Roadmap](#5-market-opportunity--commercial-growth-roadmap)
- [6. Closing Vision](#6-closing-vision)
- [References](#references)

## Executive Summary

Every month, the National Bureau of Statistics (NBS) releases Nigeria’s official inflation numbers. It is a careful, essential statistical report drawn from over 1,600 markets nationwide [^4]. But for everyday households, food vendors, and logistics operators, that official number arrives weeks after the market day has passed, and it can only offer state-wide averages rather than telling you what tomatoes or garri cost this morning at your local market.

**Market Watch** was born out of a simple observation: every single day, millions of Nigerians stand in open-air markets, negotiate prices, and pay for food. The ground-truth data already exists in real time inside the minds of everyday shoppers. What has been missing is the digital infrastructure to pool those daily transactions into a live, verified price feed.

By replacing slow, monthly survey sweeps with continuous, crowd-contributed price reporting at the point of purchase, Market Watch builds permanent, nationwide, Nigerian-owned price data infrastructure. Independent research by the European Commission has already proven that crowdsourced price data from ordinary citizens in Nigeria matches professional government surveys with **up to 99% statistical accuracy** [^9][^10].

This white paper lays out the commercial opportunity, the proven science behind crowdsourcing food prices, and our operational roadmap to secure institutional validation from the NBS while building high-value data products for Nigeria's food economy.

---

## 1. The Origin: How the Idea Came to Be

The idea for Market Watch came from the founder's own personal experiences of making shopping trips to the markets with a list of items and estimated prices.

If you have ever bought food in Nigeria, you know the feeling: you ask for the price of a  basket of tomatoes, and the price is completely different from what it was four days ago; or what it costs at a different market not too far away. You watch families adjust their budgets on the fly, traders trying to guess what their competitors are charging, and restaurant owners struggling to price their weekly menus.

When you look at the news later that month, the official report might tell you that food inflation moved by a fraction of a percent. But on the ground, prices are shifting every single morning.

That disconnect sparked a realization: **Nigeria does not actually have a data collection problem; it has a data aggregation problem.** Every shopper who pays for a bag of pepper or a paint bucket of garri holds exact, real-time market price intelligence. What if, instead of waiting for a monthly government survey crew to visit a small sample of markets, we gave ordinary shoppers a simple mobile tool to log what they paid as they buy it?

Market Watch was built to turn those millions of scattered daily purchases into a live, reliable, nationwide price feed that benefits consumers, businesses, and policymakers alike.

---

## 2. The Problem: Flying Blind in a High-Inflation Food Economy

Food is the single largest expense for the vast majority of Nigerian families, absorbing **more than 55% of household income** for lower-income quintiles [^6]. Yet, everyone in Nigeria’s food value chain operates with delayed and incomplete information.

```txt
┌─────────────────────────────────────────────────────────────────────────┐
│                       THE FOOD PRICE DATA GAP                           │
├───────────────────────────────┬─────────────────────────────────────────┤
│ OFFICIAL MONTHLY CPI          │ REALITY ON THE GROUND                   │
├───────────────────────────────┼─────────────────────────────────────────┤
│ • Published 3–4 weeks late    │ • Prices shift day-to-day & week-to-week│
│ • State & zonal averages only │ • Huge price variations between markets │
│ • High collection costs       │ • Millions of shoppers transacting daily│
└───────────────────────────────┴─────────────────────────────────────────┘
```

### a. The Timeliness Gap

The NBS rebased its Consumer Price Index (CPI) in early 2025 to a 2024 base year, expanding its tracking basket to roughly 934–960 items across 1,600+ markets [^3][^4][^5]. While this modernization reflects international standards, the survey is structurally limited to a **monthly cycle**. By the time monthly figures are published, market conditions have already moved. For instance, during late 2025, food inflation numbers experienced dramatic month-on-month swings (moving from 1.13% in November to -0.36% in December) [^1][^2][^7]. Whether driven by seasonal shifts or base-year adjustments, these delayed monthly figures leave businesses and households making decisions based on old data.

### b. The Granularity Gap

NBS reports prices as state and regional averages. However, a state-wide average cannot tell a restaurant owner in Abuja what tomatoes cost in Wuse Market versus Garki Market, nor can it tell a grain trader what maize costs today in Dawanau Market in Kano versus Bodija Market in Ibadan.

In a volatile economic environment where annual food inflation averaged **22.00% through 2025** [^1], operating without real-time, market-level price transparency creates massive inefficiency and financial risk for everyone involved.

---

## 3. The Solution: How Market Watch Works

Market Watch operates on a straightforward principle: **the shopper standing at the market stall is the best-placed person to report the price.**

Through the Market Watch platform, everyday market shoppers submit what they paid, for which commodity, at which specific market, right at the point of purchase.

```txt
[Shopper Buys Food at Market] 
       │
       ▼
[Confirms Purchase Price via App] 
       │
       ▼
[Automated Conversion & Safeguard Engine]
  ├── Local Unit Normalization (Mudu/Kongo/Paint ➔ kg)
  ├── Cross-Checking (Multi-submission verification)
  └── Trend Band-Checking (Outlier filtering)
       │
       ▼
[Live, Verified Nationwide Price Feed]
```

### Engine & Platform Architecture

The backend is engineered on NestJS with a fast, modern Angular frontend. The system is built specifically to process high-frequency, geolocated micro-data from thousands of distributed users simultaneously.

### Rigorous Data Quality Safeguards

Crowdsourced data is only as valuable as its verification system. Market Watch treats data integrity as a core architectural feature rather than an afterthought:

- **Cross-Checking:** Comparing independent price submissions for the same commodity within the same market or ward over a tight time window.
- **Band-Checking:** Automatically flagging or holding back any submission that falls outside realistic upper and lower thresholds based on rolling price trend bands.

### Solving Informal Market Measurement

Nigerian open-air markets do not sell food in standardized kilograms; they sell in local units—a *mudu*, a *kongo*, a *paint container*, a *derica*, or a *heap*. Market Watch does not need to reinvent unit conversion. We integrate established conversion handbooks—such as the International Institute of Tropical Agriculture (IITA) local weights manual [^15] and traditional market measurement studies [^16] to automatically convert local units into metric equivalents ($\text{₦/kg}$) on the fly.

---

## 4. Proven Precedent: The Science Behind Crowdsourced Prices

Market Watch is not an unproven experiment. It is the permanent, commercial evolution of a data collection methodology that has already been rigorously tested and validated in Nigeria by major international institutions.

### The Landmark FPCA Validation Study

Between 2018 and 2021, the **European Commission’s Joint Research Centre (EC-JRC)**, alongside the **International Institute of Tropical Agriculture (IITA)** and **Wageningen University**, conducted the *Food Price Crowdsourcing in Africa (FPCA)* project across Kano and Katsina States in northern Nigeria [^8][^17]. Over 700 volunteers submitted daily, geolocated staple food prices via a mobile app.

A peer-reviewed validation study published in ***PLOS ONE*** and highlighted by the **World Bank** directly compared this crowdsourced data against parallel surveys conducted by trained government-style enumerators over an 8-month period [^9][^10]:

| Commodity | Statistical Agreement ($R$) | Explaining Variance ($R^2$) |
| :--- | :---: | :---: |
| **Maize (Yellow & White)** | **0.99** | **0.98** |
| **Rice (Local & Imported)** | **0.93** | **0.87** |

*Source: World Bank Data Blog & PLOS ONE Study (Adewopo et al.) [^9][^10].*

> **Key Finding:** Ordinary citizens reporting what they paid at local markets produced price data statistically **almost indistinguishable** from professional, trained survey enumerators. Furthermore, the large volume of daily crowdsourced entries naturally smoothed out individual human errors and outliers far better than small enumerator samples.

### Global Industry Shift Toward Real-Time Data

This approach aligns with global trends. The **World Bank’s Real-Time Prices (RTP)** database uses machine-learning models to estimate high-frequency market prices across dozens of Nigerian markets specifically because traditional monthly surveys are constrained by cost, frequency, and reach [^11].

Other existing tools, such as **SBM Intelligence’s Jollof Index** [^12] (which tracks a single dish for headline advocacy), the **World Food Programme's mVAM** [^13] (focused on humanitarian crisis zones), and **FEWS NET Price Bulletins** [^14] (which aggregate third-party monthly data), highlight the growing demand for high-frequency price tracking. Market Watch complements these by operating as a primary, nationwide, item-level data infrastructure.

### Positioning in the Existing Landscape

| Initiative | What It Does | How Market Watch Differs |
| :--- | :--- | :--- |
| **NBS Official CPI** [^4] | Monthly survey, state averages | Continuous, real-time & market-local price feed |
| **SBM Jollof Index** [^12] | Cost of 1 dish, periodic metric | Broad commodity basket & permanent infrastructure |
| **WFP mVAM** [^13] | Phone surveys in conflict zones | General commercial & nationwide focus |
| **FEWS NET Bulletins** [^14] | Monthly aggregated 3rd-party data | Primary 1st-party crowdsourced data |
| **JRC FPCA Pilot** [^8][^17] | Proven 2-state research project | Permanent, nationwide, Nigerian-owned infrastructure |
| **World Bank RTP** [^11] | Machine-learning estimates | Ground-truth direct purchase feed |

Market Watch takes this scientifically validated model and turns it into permanent, enterprise-grade, Nigerian-owned software infrastructure.

---

## 5. Market Opportunity & Commercial Growth Roadmap

While gaining official institutional adoption by the NBS represents our primary regulatory and methodology validation milestone, the commercial value of real-time food price data spans the entire private sector.

### Private Sector Commercial Use Cases

1. **Food Vendors & Retail Traders:** Real-time visibility into prevailing prices at neighboring wholesale and retail markets, allowing traders to price competitively and protect margins on perishable goods.
2. **Restaurants, Hotels & Caterers:** Dynamic input-cost tracking and procurement forecasting, replacing delayed monthly estimates with daily price benchmarks for staple ingredients.
3. **FMCG & Agricultural Supply Chains:** Early warning signals for localized price shocks, enabling logistics managers and agribusinesses to optimize sourcing locations across states before regional price surges hit.
4. **Financial Services & FinTech:** Real-time localized inflation feeds for micro-lending risk models, agricultural credit scoring, and inflation-hedged savings products.

### Execution & Regulatory Validation Roadmap

```txt
  [PHASE 1: Bounded Validation Pilot]
  ─── Compare Market Watch crowdsourced feed against official benchmarks in target markets (e.g. Kano/Katsina).
        │
        ▼
  [PHASE 2: Institutional Data Partnership with NBS]
  ─── Establish data-sharing feed as a supplementary reference input for national statistics.
        │
        ▼
  [PHASE 3: Commercial B2B API & Enterprise Expansion]
  ─── Launch enterprise data subscriptions, analytics dashboards, and B2B API feeds for private sector clients.
```

1. **Phase 1: Bounded Validation Pilot**  
   Execute a focused, 6-month pilot in key commercial grain and produce hubs (mirroring the FPCA pilot in Kano and Katsina), validating Market Watch data density and accuracy against official survey benchmarks.
2. **Phase 2: Institutional Partnership with NBS**  
   Establish a formal data-sharing relationship where NBS receives Market Watch’s continuous feed as a high-frequency reference input to complement their official monthly CPI process.
3. **Phase 3: B2B Enterprise Data Monetization**  
   Commercialize enterprise API access, custom market intelligence dashboards, and predictive price analytics for agribusinesses, corporate buyers, financial institutions, and logistics firms.

---

## 6. Closing Vision

Every day in Nigeria, millions of citizens walk into open-air markets and buy food. They know down to the exact Naira what rice, garri, and tomatoes cost today at their local markets, far more accurately than any monthly survey published weeks later ever can.

Market Watch is not asking anyone to take crowdsourced data on faith. We are taking a data collection model that the European Commission and the World Bank have already proven works with 99% accuracy in Nigeria, and building the permanent, commercial technology engine to power it nationwide.

By closing Nigeria's food price data gap, Market Watch is building the primary real-time economic data layer for Africa’s largest consumer market.

---

## References

[^1]: Nigeria’s headline inflation eased to 15.15% in December 2025; 12-month average food inflation stood at 22.00%; month-on-month food inflation shifted from 1.13% in November to –0.36% in December 2025. *PUNCH Online / NBS Report*, January 2026. [Nigeria’s Headline Inflation Eased to 15.15% in December 2025 – NBS](https://punchng.com/nigerias-headline-inflation-eases-to-15-15-in-december-2025-nbs/)

[^2]: December 2025 Consumer Price Index reading of 131.2; month-on-month price reductions recorded in tomatoes, garri, and eggs. *TheCable / NBS*, January 2026. [Nigeria’s Inflation Rate Now 15%, Says NBS](https://www.thecable.ng/nigerias-inflation-rate-now-15-says-nbs/)

[^3]: CPI base year updated from 2009 to 2024, introducing specialized sub-indices including Farm Produce, Energy, and Imported Food. *Nairametrics*, February 2025. [NBS Introduces Special Inflation Indices to Monthly CPI Report](https://nairametrics.com/2025/02/19/nbs-introduces-special-inflation-indices-to-monthly-cpi-report/)

[^4]: Consumer Price Index methodology covering ~934–960 product varieties across 13 COICOP divisions in 1,600+ markets nationwide. *National Bureau of Statistics (NBS) Microdata Catalog*. [NBS Consumer Price Index and Inflation](https://microdata.nigerianstat.gov.ng/index.php/catalog/154)

[^5]: Digitization of CPI price collection and expansion of item basket from 740 to 960 items. *NISER Response Unit Brief*, April 2025. [2025 NISER Brief: Consumer Price Index Rebasing and Cost of Living Reality in Nigeria](https://niser.gov.ng/v2/wp-content/uploads/2025/04/NISER-Brief-_-CONSUMER-PRICE-INDEX-REBASING-AND-COST-OF-LIVING-REALITY-IN-NIGERIA.pdf)

[^6]: ILO-aligned survey methodology; food and non-alcoholic beverages absorb over 55% of total household spending for lower-income quintiles in Nigeria. *The Cowrie Report*, 2026. [What Is Inflation in Nigeria? How the NBS Measures the CPI and What It Means for Your Money](https://thecowriereport.com/inflation-saving-naira/what-is-inflation-nigeria-nbs-cpi)

[^7]: IMF endorsement of Nigeria’s CPI methodology modernization and base-year reference period adjustment. *BusinessDay NG / AllAfrica*, January 2026. [IMF Backs Nigeria Inflation Easing After CPI Methodology Rejig](https://allafrica.com/stories/202601170006.html)

[^8]: FPCA crowdsourcing pilot design: European Commission JRC, IITA, and Wageningen University covering 700+ volunteers in Kano and Katsina States. Adewopo et al., *Global Food Security*, 2021. [Using Crowd-Sourced Data for Real-Time Monitoring of Food Prices During the COVID-19 Pandemic](https://pubmed.ncbi.nlm.nih.gov/34178595/)

[^9]: Crowdsourced price validation study comparing volunteer data against trained enumerators: Maize $R = 0.99$ ($R^2 = 0.98$), Rice $R = 0.93$ ($R^2 = 0.87$). *World Bank Data Blog*, April 2025. [Real-Time Prices, Real Results: Comparing Crowdsourcing, AI, and Traditional Data Collection](https://blogs.worldbank.org/en/opendata/real-time-prices--real-results--comparing-crowdsourcing--ai--and)

[^10]: Peer-reviewed statistical equivalence and correlation analysis of crowdsourced, AI-imputed, and enumerator food price data in Nigeria. Adewopo et al., *PLOS ONE*, April 2025. [AI-Imputed and Crowdsourced Price Data Show Strong Agreement with Traditional Price Surveys in Data-Scarce Environments](https://journals.plos.org/plosone/article?id=10.1371%2Fjournal.pone.0320720)

[^11]: World Bank Real-Time Prices (RTP) platform: weekly updated machine-learning price imputation covering Nigerian markets since 2007. *World Bank Microdata Library*. [World Bank Microdata Library, RTP Nigeria Series](https://microdata.worldbank.org/index.php/catalog/4503)

[^12]: SBM Intelligence Jollof Index tracking representative dish ingredient costs across regional markets. *SBM Intelligence*. [Jollof Index](https://en.wikipedia.org/wiki/Jollof_index)

[^13]: WFP mVAM mobile phone surveys for humanitarian food security monitoring in vulnerable areas. *World Food Programme VAM*. [WFP VAM - mVAM Food Security Monitoring, Nigeria](https://vam.wfp.org/sites/mvam_monitoring/nigeria.html)

[^14]: FEWS NET monthly price bulletins and market fundamentals reports for staple food trade flows. *FEWS NET*. [Nigeria Price Bulletin](https://fews.net/west-africa/nigeria/price-bulletin/july-2024) and [Markets and Trade](https://fews.net/topics/markets-and-trade)

[^15]: Conversion factors and handbook for Nigerian informal market weights and measures (mudu, kongo, derica, paint container). Kormawa & Ogundapo, *IITA Monograph*, 2004. [Local Weights and Measures in Nigeria: A Handbook of Conversion Factors](https://cgspace.cgiar.org/server/api/core/bitstreams/bfc6f472-e015-4a51-98a5-4cd243e0f5b8/content)

[^16]: Traditional open-air market measurement units in Nigerian regional trading. Adebayo, *The Guardian Nigeria*, 2021. [Traditional Measurements in the Nigerian Open-Air Markets](https://guardian.ng/life/traditional-measurements-in-the-nigerian-open-air-markets/)

[^17]: Food Price Crowdsourcing in Africa (FPCA) project workshop report and implementation summary. *European Commission Joint Research Centre (JRC)*, 2020. [Evidence from the "Food Price Crowdsourcing in Africa" (FPCA) Project in Nigeria](https://publications.jrc.ec.europa.eu/repository/handle/JRC119475)
