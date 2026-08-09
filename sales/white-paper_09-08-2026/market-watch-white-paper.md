---
layout: default
title: Market Watch White Paper · Finicky Technologies Ltd
permalink: /white-paper
---

# Market Watch: Closing Nigeria's Food Price Data Gap

*Prepared By [Koyejo A.](https://www.linkedin.com/in/koyejo-adinlewa), for Finicky Technologies Ltd — 9 August 2026.*

---

## Table of Contents

- [Executive Summary](#executive-summary)
- [1. The Problem: What the Official Number Doesn't Tell You](#1-the-problem-what-the-official-number-doesnt-tell-you)
- [2. The Solution: Market Watch](#2-the-solution-market-watch)
- [3. Why We Believe This Will Work](#3-why-we-believe-this-will-work)
- [4. Wider Value: Beyond NBS](#4-wider-value-beyond-nbs)
- [5. A Path Forward: Working Toward Partnership with NBS](#5-a-path-forward-working-toward-partnership-with-nbs)
- [6. Closing](#6-closing)
- [References](#references)

## Executive Summary

Every month, the National Bureau of Statistics (NBS) tells Nigeria how much
food prices moved. It is a careful, professional number, drawn from a
survey covering thousands of markets nationwide. But by the time it is
published, it is already weeks old, and it can only tell you what happened
on average across a state, not what tomatoes cost this morning in your own
market.

Market Watch proposes to close that gap. Instead of a monthly survey run by
enumerators, everyday shoppers report what they actually paid, at the
market they actually stood in, as they buy it. This is not a new idea,
a European Commission-backed pilot already tried exactly this model in two
Nigerian states and found that ordinary volunteers produced price data
almost indistinguishable from trained government-style surveys. Market
Watch's contribution is to turn that proven idea into permanent, nationwide,
Nigerian-owned infrastructure.

The ask of this paper is simple and sequenced: validate the approach
alongside NBS's own data, build a working relationship, and over time,
become a recognized input into how NBS collects its food price data. NBS
would keep full ownership of the Consumer Price Index and how it is
calculated and published. Market Watch is offering a faster, more granular
way to gather the raw prices that feed into that work — not a replacement
for the institution that turns them into a trusted national number.

---

## 1. The Problem: What the Official Number Doesn't Tell You

NBS rebased its Consumer Price Index (CPI) in early 2025, moving the base
year from 2009 to 2024 and expanding the food and non-food basket to
roughly 934–960 items — up from around 740 in the prior methodology —
collected from over 1,600 markets across all 36 states and the FCT, in
line with international (ILO) statistical standards.[^3], [^4], [^5]

Food carries the single heaviest weight in that index, because food
consistently absorbs more than 55% of household spending for Nigeria's
lower-income households.[^6] And yet the CPI, including the food index,
is published only once a month, several weeks after the reference period
it describes has already ended.[^6]

December 2025's inflation report is a useful, recent illustration of the
tension this creates. Food inflation swung from 1.13% month-on-month in
November to –0.36% in December — a large enough move that NBS had to
publicly explain it as an "artificial spike" tied to base-year effects,
leaving many ordinary readers unsure whether prices had genuinely eased or
whether the number itself had simply shifted under a new methodology —
even as NBS pointed to real, item-level relief in staples like tomatoes,
garri, and eggs as part of the story.[^1], [^2], [^7]

None of this means NBS is doing its job badly — the rebasing itself is
evidence of an institution actively modernizing its methodology. The point
is structural: even a well-run monthly survey has a ceiling on how fast and
how local it can be. Only continuous, distributed data collection — many
people reporting many prices, all the time — can lift that ceiling. NBS
reports state and zonal averages; it does not, and at monthly survey
frequency cannot, show what tomatoes cost this morning in one ward market
versus the market ten kilometres down the road.

### Why this matters in Nigerian terms

For a household, the monthly figure is already six weeks stale by the time
it reaches the news. For a trader or a small logistics operator, what
matters is today's price in Kano versus today's price in Onitsha, not last
month's national average. And when the official number and what people are
actually experiencing at the market diverge sharply, as happened around
the December 2025 rebasing, public trust in the number itself takes a hit.

This is happening against a genuinely difficult backdrop: food inflation
averaged 22.00% for the twelve months ending December 2025.[^1] That is
exactly the kind of environment where fast, local price information has
the most value — and where a month's delay costs the most.

---

## 2. The Solution: Market Watch

Market Watch works on a simple principle: the person who bought the tomato
is the best-placed person to report what it cost. Everyday shoppers —
not traders, not paid enumerators — log what they paid, for what, and at
which market, at the point of purchase or at a later time, through the
Market Watch platform.

We want to be precise here about what exists today versus what is planned.
The backend (built on NestJS) and the consumer-facing app (built on
Angular) are in active development. There is no live public dataset yet,
and this paper does not claim results it does not have. What it can claim
is a sound, deliberately-designed architecture, built on a model that has
already been proven to work in Nigeria (see Section 3).

**How submissions will be kept trustworthy.** Crowdsourced data is only
useful if it can be trusted, and we are treating quality control as a
first-class design problem, not an afterthought. Two safeguards are under
active design, though neither is finalized yet:

- **Cross-checking** — comparing multiple independent submissions for the
  same item, within the same market or ward, within the same time window.
- **Band-checking** — flagging or holding back a submitted price if it
  falls far outside the current upper and lower band of that item's known
  price trend.

We are stating this plainly rather than implying it is solved, because a
credible data-quality design matters more to a statistics-literate reader
than an unearned claim of certainty.

**A note on informal market units.** Nigerian markets often price in local
units — a paint, a mudu, a kongo, a derica, a heap — rather than the
standardized kilogram or litre. This is a real engineering task, but it is
not a problem Market Watch has to solve from first principles. Documented
conversion-factor references for exactly these units already exist,
including a dedicated handbook of local weights and measures compiled for
Nigerian agricultural markets, and NBS's own field methodology already
performs this same local-unit-to-standard conversion routinely.[^15], [^16]
The task ahead is mapping submissions onto an already-recognized standard,
not inventing a new one.

---

## 3. Why We Believe This Will Work

Market Watch has no results of its own yet, so this section leans on
something stronger than a young platform's own claims: independent,
peer-reviewed precedent, gathered in Nigeria, on Nigerian food staples.

### It's been tried before, and it worked

Between 2018 and 2021 (reactivated through the COVID-19 period), the
European Commission's Joint Research Centre (JRC), working with IITA
Nigeria and Wageningen University, ran the Food Price Crowdsourcing in
Africa (FPCA) project across Kano and Katsina States. Over 700 volunteers
were recruited to submit daily, geolocated prices for staple foods —
maize and rice — through a mobile app, with automated quality-control
filtering built in.[^8]

The critical finding came from a follow-up study. Researchers directly
compared FPCA's crowdsourced prices against prices collected by trained
enumerators running a conventional survey over the same period
(2021–2023). At monthly frequency, crowdsourced maize prices correlated
with enumerator data at R = 0.99 (R² = 0.98), and rice at R = 0.93
(R² = 0.87).[^9], [^10]

In plain terms: ordinary people reporting what they paid, at scale,
produced numbers that were statistically almost indistinguishable from a
professional government-style survey. This directly answers the question
of whether we can we trust prices reported by the public. The answer isn't
Market Watch's own claim. It's an independent finding, from Nigeria,
about Nigerian food staples.

A second, related effort reinforces the same point from a different angle.
The World Bank's Real-Time Prices (RTP) initiative has built a live,
weekly-updated dataset blending direct price collection with machine-
learning imputation, covering food price series across dozens of Nigerian
markets since 2007 — built specifically because traditional surveys are
constrained by cost, frequency, and reach.[^11] Major institutions are
already investing in alternatives to monthly, enumerator-only surveys,
because the frequency gap is a known, serious limitation — not a fringe
complaint.

### Where Market Watch fits among what already exists

| Initiative | What it does | How Market Watch differs |
| --- | --- | --- |
| NBS CPI (Food Index)[^4], [^6] | Official monthly survey, ~1,600 markets, state/zonal averages | Continuous, food item & market-specific, not monthly and averaged |
| SBM Intelligence's Jollof Index[^12] | Tracks the cost of one representative dish across select markets, published periodically | Narrow by design (one dish, headline metric); Market Watch aims for broad, continuous, item-level coverage as infrastructure |
| WFP mVAM[^13] | Phone-based surveys focused on food security and humanitarian response in vulnerable areas | Humanitarian-need focus, not general infrastructure; Market Watch targets the general population and general commerce nationwide |
| FEWS NET Price Bulletins[^14] | Monthly bulletins compiling prices from partner data for early warning | Aggregates existing third-party data; Market Watch collects first-party data directly from the public |
| JRC / FPCA[^8], [^9], [^17] | Proven crowdsourcing pilot, two states, small commodity set, project-based | Market Watch is the natural successor — same validated method, built as permanent, nationwide, Nigerian-owned infrastructure rather than a time-limited research project |
| World Bank RTP[^11] | ML-imputed prices filling gaps between sparse survey data points | Estimates prices where data is missing; Market Watch generates first-party ground-truth data, reducing the need for estimation |

Every major precedent validates the *method*. None of them is permanent,
national, and Nigerian-run. That is the gap Market Watch fills.

---

## 4. Wider Value: Beyond NBS

While NBS is the central audience for this paper, the same underlying data
has real, everyday value to Nigeria's food economy. This is offered as a
brief, secondary case — not the core argument — and kept deliberately
modest, since there is no live data yet to point to.

- **Vendors and traders** could see, in near real time, what neighbouring
  markets are charging for the same goods — useful for day-to-day pricing
  decisions, especially for fast-moving perishables.
- **Restaurants and food-service businesses** could plan input costs with
  something more current than a national monthly average, particularly
  where they source from specific regional markets based on their o.
- **Agric supply chains and logistics operators** could catch an early
  signal of a localized price shock — a sudden spike in one state — and
  adjust sourcing or distribution before it ever shows up in a national
  monthly figure.

These are plausible, grounded use cases, not proven outcomes. We raise them
to show that the same infrastructure serving NBS's needs also serves
Nigeria's food economy more broadly.

---

## 5. A Path Forward: Working Toward Partnership with NBS

We are not asking NBS to take crowdsourced data on faith. We are asking NBS
to test something a peer institution — the European Commission's JRC —
already tested successfully, in Nigeria, on Nigerian food staples. The
proposal is deliberately sequenced, starting with the lowest-commitment
step first.

1. **Validate.** A bounded pilot, in the spirit of FPCA's original
   two-state design, comparing Market Watch's crowdsourced feed against
   NBS's own survey data for a defined set of items and markets over a
   defined period. We propose Kano and Katsina States as the pilot
   locations, mirroring FPCA's own choice — this keeps the comparison as
   close as possible to the conditions under which the original validation
   findings (Section 3) were established, making any result easier to
   interpret against known precedent.
2. **Partner.** Based on pilot results, a formal data-sharing relationship
   in which NBS receives Market Watch's feed as a supplementary reference
   input, alongside — not replacing — its own survey.
3. **Integrate.** Over the longer term, Market Watch's feed becomes a
   recognized input into how NBS *collects* its food price data. NBS
   continues to own the CPI methodology and its publication; Market Watch
   simply feeds it faster, more granular prices than the current survey
   cadence alone can provide.

---

## 6. Closing

Nigeria does not lack for people who know exactly what food costs — every
shopper who walks into a market and pays for tomatoes, rice, or garri
knows it, in real time, more precisely than any monthly survey ever will.
What has been missing is a way to gather what all of them already know and
turn it into something an institution like NBS can use.

That is what Market Watch is built to do: not to replace the work NBS
does, but to give it a faster, finer-grained supply of the raw material it
already collects every month. The FPCA project showed, years ago and in
Nigeria itself, that this works. Market Watch's task now is to build the
permanent, nationwide, Nigerian-owned version of that idea — and we would
welcome the chance to prove it alongside NBS, starting small, starting
where the evidence already points.

---

## References

[^1]: Nigeria's headline inflation eased to 15.15% in December 2025; food
    inflation averaged 22.00% for the twelve months ending December 2025;
    month-on-month food inflation swung from 1.13% (November) to –0.36%
    (December). [Nigeria's Headline Inflation Eased to 15.15% in December 2025 - NBS](https://punchng.com/nigerias-headline-inflation-eases-to-15-15-in-december-2025-nbs/),
    PUNCH Online, January 2026.

[^2]: December 2025 CPI reading of 131.2, up from 130.5; food inflation
    decline attributed to falling prices of tomatoes, garri, eggs, and
    other staples. [Nigeria's Inflation Rate Now 15%, Says NBS](https://www.thecable.ng/nigerias-inflation-rate-now-15-says-nbs/),
    TheCable, January 2026.

[^3]: CPI base year moved from 2009 to 2024; special indices introduced
    (Farm Produce, Energy, Services, Goods, Imported Food).
    [NBS Introduces Special Inflation Indices to Monthly CPI Report](https://nairametrics.com/2025/02/19/nbs-introduces-special-inflation-indices-to-monthly-cpi-report/),
    Nairametrics, February 2025.

[^4]: CPI covers 934 product varieties across 13 divisions under the
    COICOP 2018 framework; weight reference period 2023, price/base year
    2024. [Nigeria - Consumer Price Index and Inflation](https://microdata.nigerianstat.gov.ng/index.php/catalog/154),
    NBS Microdata Catalog.

[^5]: CPI basket expanded to 960 items from 740 as part of rebasing;
    digitized price data collection. [2025 NISER Brief: Consumer Price Index Rebasing and Cost of Living Reality in Nigeria](https://niser.gov.ng/v2/wp-content/uploads/2025/04/NISER-Brief-_-CONSUMER-PRICE-INDEX-REBASING-AND-COST-OF-LIVING-REALITY-IN-NIGERIA.pdf),
    Nigerian Institute of Social and Economic Research.

[^6]: NBS derives the CPI from a survey covering 700+ commodities across 13
    divisions from 1,600+ markets in 36 states and the FCT, following the
    ILO framework; food absorbs 55%+ of household spending for lower
    income quintiles. [What Is Inflation in Nigeria? How the NBS Measures the CPI and What It Means for Your Money](https://thecowriereport.com/inflation-saving-naira/what-is-inflation-nigeria-nbs-cpi),
    The Cowrie, 2026.

[^7]: IMF statement on the December 2025 CPI methodology change and its
    base-year rebasing context. [IMF Backs Nigeria Inflation Easing After CPI Methodology Rejig](https://allafrica.com/stories/202601170006.html),
    Businessday NG / AllAfrica, January 2026.

[^8]: FPCA project design: JRC with IITA Nigeria and Wageningen University,
    700+ volunteers across Kano and Katsina States, daily geolocated
    maize/rice price submissions via mobile app with automated quality
    control, 2018–2019 (reactivated during COVID-19).
    [Using Crowd-Sourced Data for Real-Time Monitoring of Food Prices During the COVID-19 Pandemic](https://pubmed.ncbi.nlm.nih.gov/34178595/),
    Adewopo, Solano Hermosilla, Colen, Micale, Global Food Security, 2021.

[^9]: Validation study comparing FPCA crowdsourced prices to trained
    enumerator survey data (2021–2023): maize R = 0.99 (R² = 0.98), rice
    R = 0.93 (R² = 0.87) at monthly frequency.
    [Real-Time Prices, Real Results: Comparing Crowdsourcing, AI, and Traditional Data Collection](https://blogs.worldbank.org/en/opendata/real-time-prices--real-results--comparing-crowdsourcing--ai--and),
    World Bank Data Blog, 2025.

[^10]: Independent peer-reviewed comparison of AI-imputed, crowdsourced,
    and enumerator-led price data in northern Nigeria.
    [AI-Imputed and Crowdsourced Price Data Show Strong Agreement with Traditional Price Surveys in Data-Scarce Environments](https://journals.plos.org/plosone/article?id=10.1371%2Fjournal.pone.0320720),
    PLOS ONE / PMC, 2025.

[^11]: World Bank Real-Time Prices (RTP): live, weekly-updated dataset
    combining direct price measurement with ML imputation, covering
    Nigerian markets since 2007, built because traditional surveys are
    "constrained by challenges related to cost, frequency, and reach."
    [World Bank Microdata Library, RTP Nigeria Series](https://microdata.worldbank.org/index.php/catalog/4503).

[^12]: SBM Intelligence's Jollof Index tracks the cost of jollof rice
    ingredients across Nigerian and Ghanaian markets monthly, launched
    2015. [Jollof Index](https://en.wikipedia.org/wiki/Jollof_index), Wikipedia.

[^13]: WFP's mVAM conducts phone-based household and trader surveys on
    food security and prices, concentrated in vulnerable and
    conflict-affected areas of Nigeria since 2016.
    [WFP VAM - mVAM Food Security Monitoring, Nigeria](https://vam.wfp.org/sites/mvam_monitoring/nigeria.html).

[^14]: FEWS NET produces monthly Price Bulletins compiling staple food
    prices from partner data sources (government, FAO, WFP) for
    food-security early warning.
    [Nigeria Price Bulletin](https://fews.net/west-africa/nigeria/price-bulletin/july-2024)
    and [Markets and Trade](https://fews.net/topics/markets-and-trade), FEWS NET.

[^15]: Documented conversion factors exist for Nigerian informal market
    units (mudu, kongo, rubb, paint, derica) as used across regions,
    compiled to support agricultural price-data standardization.
    [Local Weights and Measures in Nigeria: A Handbook of Conversion Factors](https://cgspace.cgiar.org/server/api/core/bitstreams/bfc6f472-e015-4a51-98a5-4cd243e0f5b8/content).

[^16]: Regional variation in informal unit definitions and their
    approximate metric equivalents (derica, mudu, paint/rubber, milk-tin
    measures). [Traditional Measurements in the Nigerian Open-Air Markets](https://guardian.ng/life/traditional-measurements-in-the-nigerian-open-air-markets/),
    The Guardian Nigeria, 2021.

[^17]: FPCA project background and initial 2018–2019 implementation in
    northern Nigeria, EU Delegation Abuja workshop summary.
    [Evidence from the "Food Price Crowdsourcing in Africa" (FPCA) Project in Nigeria](https://publications.jrc.ec.europa.eu/repository/handle/JRC119475),
    JRC Publications Repository.
