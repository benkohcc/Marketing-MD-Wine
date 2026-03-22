# BUDGET.MD — Wine E-Commerce
*Companion file to MARKETING.MD — Budget governance and spending configuration*
*Loaded by: campaign-planning agents, paid-media agents, plan-campaign skill*
*Authority: This file is the sole authority for budget allocation, agent spending authority limits, stop-loss thresholds, and bid ceilings. Universal spend constraints (any spend above $500 requires approval) are in MARKETING.MD Section 7 (Human Approval Gates) and Section 12 (AI Autonomy).*

---

## Total Budget

```yaml
budget:
  period: monthly
  total: $[N]

  channel_allocation:
    email: 5%           # ESP costs — low absolute spend
    paid_search: 35%    # Google Shopping drives highest-intent wine buyers
    paid_social: 30%    # Meta retargeting + prospecting for seasonal
    content_seo: 20%    # blog production and SEO tooling
    affiliate: 5%
    reserved: 5%        # opportunistic — emerging wine events, competitor disruption

  portfolio_split:
    proven_channels: 70%    # email, Google Shopping, Meta retargeting — proven ROAS
    emerging_channels: 20%  # Pinterest, TikTok, new paid formats
    experimental: 10%       # influencer tests, podcast, niche wine media

  seasonal_rebalancing:
    # Shift allocation during high-season windows
    holiday_gifting_nov_dec:
      paid_social: 40%     # Gifter persona is most reachable via paid social
      paid_search: 30%     # Gift-intent searches spike
    harvest_season_sep_oct:
      email: 10%           # Loyalist and Collector heavy — email over-indexes
      paid_search: 30%
```

---

## Agent Spending Authority

```yaml
spending_authority:
  auto_approve:
    - action: "Adjust Google Shopping bids within active campaign"
      limit: "±15% per day"
    - action: "Pause Meta ad set"
      condition: "ROAS below 2.0× for 3 consecutive days"
    - action: "Reallocate budget between ad sets within same paid campaign"
      limit: "Up to 20% of campaign budget"

  notify_then_proceed:
    - action: "Launch a new paid campaign"
      condition: "Campaign brief approved at Gate 1; budget within channel allocation"
      notification: "Slack alert with campaign ID, SKU, budget, and targeting summary"
    - action: "Increase daily budget on overperforming campaign"
      limit: "Up to 20% increase; not to exceed channel monthly cap"

  require_approval:
    - action: "Any single-day spend above $500"
    - action: "Channel reallocation exceeding 10% of monthly budget"
    - action: "Spend on a channel not in the current allocation plan"
    - action: "Any paid campaign for limited_allocation SKUs (prohibited)"
```

---

## Stop-Loss Thresholds

```yaml
stop_loss:
  paid_roas_below: 2.0        # pause if ROAS drops below 2× for 3 consecutive days
  cpa_above: $[N]             # pause if CPA exceeds this for 3 consecutive days
  daily_spend_above: $[N]     # alert if daily spend is more than 2× planned daily rate

  auto_pause_conditions:
    - "ROAS < 2.0× for 3+ consecutive days → pause campaign, alert human"
    - "Daily spend > 2× planned daily budget → pause immediately (bid runaway protection)"
    - "Conversion rate drops > 40% vs. 7-day baseline → pause and flag"
    - "SKU sells out while paid campaign is active → pause immediately (inventory sync)"

  resume_conditions:
    - "Human explicitly approves resume"
    - "Inventory confirmed back in stock (for OOS pauses)"
```

---

## Bid Ceilings

```yaml
bid_ceilings:
  google_shopping:
    max_cpc: $[N]             # set per margin tier — high-margin SKUs warrant higher bids
  google_search:
    max_cpc: $[N]
    high_value_keywords:      # vintage-specific and producer-specific searches
      max_cpc: $[N]
  meta:
    max_cpm: $[N]
    retargeting_max_cpm: $[N]   # retargeting audiences are smaller and more expensive

  alcohol_advertising_note: "Google, Meta, and Pinterest each have distinct alcohol advertising policies. All paid campaigns require platform-specific compliance review before launch."
```

---

## Versioning

```yaml
budget_md_wine:
  version: "1.0.0"
  last_updated: "2026-03-22"
  updated_by: "Wine marketing system operator"
  review_cadence: "Quarterly — update total budget, channel allocation percentages, and bid ceilings"

  changelog:
    - version: "1.0.0"
      date: "2026-03-22"
      changes: "Initial release — moved from MARKETING.md Section 17"
```
