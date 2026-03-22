# MEASUREMENT.MD — Wine E-Commerce
*Companion file to MARKETING.MD — Attribution, tracking, and measurement governance*
*Loaded by: performance-report skill, analytics agents*

---

## 1. Measurement Philosophy

```yaml
measurement_philosophy:
  approach: "Triangulation — MTA for tactical; MMM for strategic; incrementality for causal validation"
  
  wine_specific_consideration: >
    Wine buying is a multi-session, multi-touchpoint journey. A Collector may read three
    blog posts, receive two emails, and click a paid ad over six weeks before purchasing.
    Last-touch attribution systematically undercredits email and editorial content.
    Linear or time-decay models are more appropriate for this buying behavior.
  
  model_hierarchy:
    tactical: "Linear multi-touch attribution — daily/weekly campaign decisions"
    strategic: "Marketing mix modeling — quarterly budget allocation"
    causal: "Incrementality testing — validates both; quarterly minimum"
  
  conflict_resolution: "When MTA and MMM disagree by > 20% on channel contribution, flag for human review before reallocating budget"
```

---

## 2. Attribution Models

### Primary Model

```yaml
primary_attribution:
  model: linear
  use_for: "Daily campaign optimization; weekly performance reports"
  rationale: "Wine buyers engage with email, editorial content, and paid across multiple sessions before purchasing. Linear attribution gives appropriate credit to the full touchpoint sequence."
  
  known_limitations:
    - "Undervalues high-frequency early touchpoints (email newsletter that builds awareness)"
    - "Overvalues last-touch in impulse-category campaigns (limited allocation)"
    note: "For limited allocation and flash campaigns, consider reviewing first-touch data alongside linear"
  
  agent_rules:
    - "Always use linear model for standard campaign reporting"
    - "For Collector and pre-order campaigns, report both linear and first-touch alongside each other"
    - "Flag to human if attribution data is more than 24 hours old before producing weekly report"
```

### Secondary Model

```yaml
secondary_attribution:
  model: marketing_mix_modeling
  use_for: "Quarterly budget allocation decisions"
  
  mmm_variables:
    - "Paid search spend and impressions (Google Shopping, branded, non-branded)"
    - "Paid social spend and reach (Meta, Pinterest)"
    - "Email send volume and engaged list size"
    - "Organic search traffic"
    - "Seasonality (wine calendar events — harvest, holiday, Valentine's)"
    - "Promotional calendar (discount campaigns, limited allocation events)"
  
  calibration: "MMM results calibrated against incrementality holdout tests quarterly"
  model_refresh: "Quarterly minimum; after any major channel mix change"
  minimum_data_window_months: 12
```

---

## 3. Conversion Windows

```yaml
conversion_windows:
  paid_search_click: 14 days
  paid_social_click: 7 days
  paid_social_view: 1 day      # view-through only for Collector-targeting campaigns where research cycles are longer
  email_click: 30 days         # wine consideration cycles are long — 30-day window is appropriate
  organic_search: 30 days
  direct: 30 days
  
  default_lookback_window: 90 days
  
  wine_specific_windows:
    collector_campaigns: "Consider 60-day click window — pre-order and allocation decisions take time"
    limited_allocation: "7-day click window — scarcity campaigns convert fast or not at all"
    educational_content: "30-day view-then-purchase window — content plants a seed; purchase follows later"
  
  ios_and_browser_restrictions:
    safari_itp: "7-day click cap in Safari — email attribution especially affected; supplement with post-purchase surveys"
    ios_att: "Use SKAdNetwork for iOS; supplement with server-side tracking"
    agent_rule: "Never use platform-reported attribution as the source of truth — always recalculate from MCP data using configured windows"
```

---

## 4. UTM & Tracking Standards

```yaml
utm_standards:
  format: "utm_source=[source]&utm_medium=[medium]&utm_campaign=[campaign_id]&utm_content=[asset_id]"
  
  source_values:
    google: "google"
    meta: "meta"
    pinterest: "pinterest"
    email: "email"
    organic_social: "social"
    affiliate: "affiliate"
  
  medium_values:
    google_shopping: "shopping"
    paid_search: "cpc"
    paid_social: "paid_social"
    email_campaign: "email"
    organic_social: "organic_social"
    display: "display"
  
  campaign_id_format: "[YYYY-MM]-[type_code]-[persona_code]-[sku_short]"
  content_id_format: "[campaign_id]-[channel_code]-[asset_type]-[variant]"
  
  wine_specific_rules:
    - "Include sku_short in campaign_id when a campaign features a specific wine"
    - "For educational campaigns with no featured SKU, use topic slug instead (e.g., 2025-03-edu-ex-barolo-guide)"
    - "For seasonal multi-SKU campaigns, use the occasion name (e.g., 2025-02-seas-gi-valentines)"
  
  enforcement:
    - "All agent-generated links must include UTM parameters — no exceptions"
    - "Missing UTM = unattributed revenue; flagged in daily QA"
    - "Verify UTM parameters are active and tracking correctly at campaign launch before any paid spend begins"
```

---

## 5. Wine-Specific KPI Definitions

```yaml
kpi_definitions:
  
  sell_through_speed:
    definition: "Units sold per day during campaign flight"
    formula: "total_units_sold / campaign_days_elapsed"
    use_for: "Primary KPI for limited_allocation campaigns"
  
  time_to_sellout:
    definition: "Days from campaign launch to SKU reaching zero inventory"
    use_for: "Secondary KPI for limited_allocation; primary for measuring scarcity effectiveness"
  
  reactivation_rate:
    definition: "Lapsed customers who make a purchase within 30 days of winback send"
    formula: "winback_campaign_purchasers / winback_campaign_recipients"
    measurement_window: 30 days
  
  second_purchase_rate:
    definition: "New customers who make a second purchase within 30/60/90 days of first"
    formula: "customers_with_2+_purchases_in_window / customers_with_first_purchase_in_period"
    measurement_windows: [30, 60, 90]   # report all three
  
  reservation_count:
    definition: "Number of pre-order reservations completed (deposit paid or expression of interest submitted)"
    formula: "completed_reservation_actions / pre_order_email_recipients"
    use_for: "Primary KPI for pre_order campaigns"
  
  pdp_view_rate:
    definition: "Percentage of email recipients who visit the featured wine's product page"
    formula: "unique_pdp_visits / delivered_emails"
    use_for: "Primary KPI for new_arrival campaigns (awareness measure, not conversion)"
  
  content_dwell_time:
    definition: "Average time spent on a blog post or guide by visitors who spend > 10 seconds (eliminates bounces)"
    target: "> 180 seconds"
    use_for: "Primary KPI for educational campaigns"
  
  pdp_click_rate_from_content:
    definition: "Percentage of blog/guide page visitors who click through to a featured PDP"
    formula: "pdp_clicks_from_content / content_page_visitors"
    target: "> 12%"
    use_for: "Secondary KPI for educational campaigns"
```

---

## 6. Reporting Standards

```yaml
reporting:
  
  daily:
    required_metrics: [revenue, orders, aov, paid_roas, email_sends, email_ctr, site_conversion_rate, active_campaign_performance]
    wine_additions: [sell_through_speed_for_allocation_campaigns, inventory_status_for_active_campaign_skus]
    distribution: "[Slack / Dashboard — human reviews]"
  
  weekly:
    required_metrics: [channel_attribution_linear, campaign_kpi_vs_target, clv_trend, segment_health, content_performance]
    wine_additions: [vintage_inventory_aging_report, high_intent_low_stock_skus, churn_risk_segment_update]
    distribution: "[Store owner / marketing lead]"
  
  post_campaign_retrospective:
    timing: "Immediately after campaign closes; within 48 hours"
    required_sections:
      - "Actual KPIs vs. targets (primary and secondary)"
      - "Attribution by channel (linear model)"
      - "A/B test results if any tests ran"
      - "Inventory impact (sell-through achieved, days-of-supply change)"
      - "Top 3 learnings with actionable recommendations"
      - "Retrospective stored in MCP via create_campaign_retrospective()"
    wine_additions:
      - "Persona response analysis — which segments converted vs. expected"
      - "SKU halo effect — did the campaign drive interest in related SKUs?"
      - "Drinking window implication — does strong sell-through suggest we should prioritize cellaring guidance?"
```

---

## 7. Versioning

```yaml
measurement_md_wine:
  version: "1.0.0"
  last_updated: "2026-03-21"
  updated_by: "Wine marketing system operator"
  review_cadence: "Quarterly — update after MMM refresh; review conversion windows after platform changes"
  
  changelog:
    - version: "1.0.0"
      date: "2026-03-21"
      changes: "Initial release"
```
