# Grocery Price Pressure Tracker

A small analysis of Canadian grocery inflation and what it could mean for grocery delivery demand — built as a self-directed project alongside an application to Instacart's Strategic Finance team.

**[View the live dashboard →](#)** *(replace with your GitHub Pages URL once deployed)*

## The hypothesis

Instacart's business sits on top of grocery spend. Basket size, order frequency, and willingness to pay a delivery markup are all, to some degree, downstream of how much price pressure shoppers are feeling at checkout. If grocery prices rise faster in some categories than others, that pressure isn't evenly distributed — and the categories running hottest are worth watching as a leading indicator of where demand might soften first.

This project tracks that pressure directly from government price data, then applies published academic research on food price elasticity to estimate a plausible range of demand impact.

## What's in the dashboard

1. **Price trend (2021–present)** — CPI index values across 8 grocery categories, sourced from Statistics Canada, showing the post-pandemic inflation spike and where things stand now.
2. **Category comparison** — which categories are running hottest year-over-year, sorted to show where pressure is concentrated rather than averaged away.
3. **Interactive elasticity scenarios** — for any selected category, a low/base/high range of implied demand impact, using published price elasticity estimates for Canadian food demand.

## Data sources

- **Price data**: Statistics Canada, [Table 18-10-0004-01](https://www150.statcan.gc.ca/t1/tbl1/en/tv.action?pid=1810000401), *Consumer Price Index, monthly, not seasonally adjusted*. Covers "Food purchased from stores" and its 7 published sub-categories, January 2021 through April 2026.
- **Elasticity estimates, Meat**: Diakité (2024), *Estimating Demand for Lamb, Beef, Pork, and Poultry in Canada* — national-level own-price elasticities for beef, poultry, and lamb, derived from 2019–2022 Canadian retail (Nielsen) data.
- **Elasticity estimates, other categories**: Ni Mhurchu et al. (2013), *Food Prices and Consumer Demand: Differences across Income Levels and Ethnic Groups*, PLoS ONE — an Almost Ideal Demand System (AIDS) model using New Zealand household survey data from 2006/07 and 2009/10. Used here as the closest available published proxy for categories without a Canadian-specific estimate.

## Methodology notes — what this is and isn't

This is an illustrative model, not a validated forecast, and I want to be upfront about where the estimates are doing real work versus where they're a reasonable proxy:

- **Meat** uses real Canadian data: beef's elasticity (−0.65) as the conservative scenario, poultry's (−0.93) as the base case (the most statistically reliable of the three), and lamb's (−2.64) as an upper bound — flagged explicitly as the least stable estimate in the source study, since lamb consumption in Canada is comparatively low-volume and volatile.
- **All other categories** (dairy, vegetables, bakery, fruit, fish, etc.) use the New Zealand study's range (−0.22 to −1.78) as a proxy, since I could not find a published Canadian-specific elasticity for these categories at this level of detail. This is a real limitation, not a Canadian estimate dressed up as one — and it's stated as such directly in the dashboard.
- None of these elasticity figures are specific to **grocery delivery** demand (as opposed to in-store grocery demand). Delivery demand likely carries some additional price sensitivity on top of general food demand, since it's a discretionary layer on top of an already-rising cost, but I don't have data to quantify that gap, so I haven't tried to.
- This is a snapshot, refreshed manually from a one-time data pull (latest data: April 2026), not a live-updating feed.

## Why this approach

I wanted to build something that demonstrates the actual skill the role requires — reading a real cost-pressure signal and translating it into a demand-side hypothesis — rather than a generic technical demo. The honesty about what the model can't claim is intentional: a model that's clear about its own limits is more useful, and more credible, than one that overstates its precision.

## Stack

Static HTML, vanilla JS, [Chart.js](https://www.chartjs.org/) for visualization. No backend, no build step — data is pre-processed from the StatCan CSV export into a local JS file (`dashboard_data.js`) and loaded directly in the browser. Deployed via GitHub Pages.

## Possible next steps

- Automate the monthly data refresh via a scheduled script against StatCan's public API, rather than a manual CSV pull.
- Layer in a second proxy for delivery-specific demand sensitivity (e.g. consumer spending intent surveys) if a credible public source can be found.
- Extend the comparison to a second country or province-level breakdown, if regional grocery price divergence turns out to be meaningful.
