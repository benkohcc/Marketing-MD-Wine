# EXPERIMENTATION.MD — Wine E-Commerce
*Companion file to MARKETING-wine-ecommerce.md — A/B testing governance and rollout rules*
*Loaded by: review-behavior skill, update-personalization skill, experimentation agents*

---

## 1. Statistical Standards

```yaml
statistical_standards:
  confidence_level: 95%
  statistical_power: 80%
  minimum_detectable_effect: 5%
  
  minimum_test_duration_days: 7
  maximum_test_duration_days: 28
  
  novelty_effect_correction: true    # do not read results in first 48 hours
  peeking_prevention: true           # check results maximum once per day; do not stop early
  sample_ratio_mismatch_detection: true
  
  wine_specific_warnings:
    seasonal_contamination: >
      Tests running across major wine seasonal windows will be contaminated.
      Do not start a test on November 15 and try to read results on December 1 —
      the holiday demand spike will invalidate the signal. Hold tests until after
      the seasonal window clears, or exclude seasonal-window days from analysis.
    
    persona_segmentation: >
      Wine buyer behavior is highly persona-specific. A test that wins on the
      full customer base may lose on Collectors and win on Explorers.
      Segment results by persona tier in every test report.
    
    low_volume_skus: >
      Limited allocation and pre-order SKUs have inherently small audiences.
      Do not run formal A/B tests on these — the sample size will never reach
      statistical significance. Use qualitative signals and retrospective analysis instead.
```

---

## 2. Test Governance

```yaml
test_governance:
  
  concurrent_limits:
    per_page_element: 1
    per_page: 3
    sitewide: 8
    per_email_campaign: 1
  
  approval_requirements:
    agent_can_create:
      - "Email subject line A/B tests"
      - "PDP urgency banner tests (low stock messaging vs. standard)"
      - "PDP badge tests (Just Arrived, Limited Allocation, etc.)"
      - "Collection sort order tests"
      - "Social creative copy variants (2 caption alternatives)"
      - "Winback email subject line tests"
    
    requires_human_approval:
      - "Checkout flow modifications"
      - "Pricing display or discount presentation"
      - "Tests on audience > 500 customers"
      - "Any test during peak windows (Nov 15 – Jan 5; Feb 7–14; week of Thanksgiving)"
      - "Tests modifying the PDP tasting notes or drinking window display"
      - "Tests on tier_collector or limited_allocation SKU pages"
    
    never_test_without_owner_sign_off:
      - "Anything that changes how a wine's price is displayed"
      - "Any test on the allocation access flow (Loyalist and Collector trust is fragile)"
  
  winner_promotion:
    agent_authority: false    # agents surface results; humans approve
    presentation_format: |
      A/B TEST RESULT — AWAITING APPROVAL
      Test: [name]
      Winner: [variant_id] — [description]
      Primary metric lift: [N]% on [metric]
      Statistical confidence: [N]%
      Sessions per variant: [N]
      Duration: [N] days
      Guardrail metric outcomes: [all clear / any degradation noted]
      Persona breakdown: [Explorer lift: N%; Loyalist lift: N%; etc.]
      Recommendation: Promote [variant] to 100% of traffic
      Estimated annual impact if promoted: [revenue / conversion estimate]
```

---

## 3. Wine-Specific Test Designs

```yaml
wine_test_library:
  # Proven test designs for wine e-commerce — use as starting templates
  
  pdp_scarcity_messaging:
    hypothesis: "Showing exact remaining bottle count drives higher add-to-cart than generic 'limited availability'"
    variant_control: "Limited availability — order soon"
    variant_a: "Only [N] bottles remaining"
    primary_metric: add_to_cart_rate
    applicable_campaign_types: [limited_allocation, new_arrival_low_stock]
    wine_note: "Exact quantity must be real — never fabricated. Pulls from live inventory."
  
  new_arrival_subject_lines:
    hypothesis: "Winemaker story subject lines outperform wine name subject lines for Explorer persona"
    variant_control: "Now available: [Wine Name] [Vintage]"
    variant_a: "The winemaker who [specific compelling fact about them]"
    variant_b: "Why we waited [N] years to add this [varietal] to the catalog"
    primary_metric: email_open_rate
    applicable_personas: [Explorer, Loyalist]
  
  collection_page_sort:
    hypothesis: "Persona-affinity sort drives higher add-to-cart than price-ascending or popularity sort"
    variant_control: "Popularity (best-seller rank)"
    variant_a: "Persona affinity weighted (calls get_recommendations per visitor)"
    variant_b: "Campaign boost weighted (current active campaign SKUs surfaced first)"
    primary_metric: add_to_cart_rate
    guardrail: revenue_per_visitor
    wine_note: "Test must run for full 7 days to capture weekend-vs-weekday behavior differences"
  
  educational_content_cta:
    hypothesis: "Inline CTA within blog body converts better than footer CTA only"
    variant_control: "CTA button at end of post only"
    variant_a: "CTA button after second section + end of post"
    variant_b: "Floating sticky CTA bar (show after 50% scroll)"
    primary_metric: pdp_click_rate_from_content
    guardrail: content_dwell_time    # ensure CTA placement doesn't reduce reading depth
  
  winback_subject_line:
    hypothesis: "Relationship-led subject lines outperform curiosity-led subject lines for lapsed customers"
    variant_control: "We've been thinking about you"
    variant_a: "Your [preferred varietal] cellar is missing something"
    variant_b: "What's new since you last visited us"
    primary_metric: email_open_rate
    secondary: reactivation_rate_30d
    applicable_personas: [Loyalist, Explorer]
    wine_note: "Variant A requires varietal affinity data — only eligible for customers with a known preferred varietal"
  
  gift_guide_layout:
    hypothesis: "Price-tier filtering drives higher conversion than occasion filtering for gift guide pages"
    variant_control: "Filter by occasion (Valentine's, Mother's Day, etc.)"
    variant_a: "Filter by budget tier (Under $50 / $50–$100 / $100+)"
    variant_b: "Filter by recipient type (Wine lover / Occasional drinker / Collector)"
    primary_metric: add_to_cart_rate
    applicable_personas: [Gifter]
    applicable_campaign_types: [seasonal]
```

---

## 4. Guardrail Metrics

```yaml
guardrail_metrics:
  - metric: checkout_completion_rate
    max_allowed_degradation_pct: 5
    auto_rollback: true
  
  - metric: email_unsubscribe_rate
    max_allowed_degradation_pct: 20
    auto_rollback: true
  
  - metric: spam_complaint_rate
    max_allowed_degradation_pct: 30
    auto_rollback: true
  
  - metric: revenue_per_visitor
    max_allowed_degradation_pct: 10
    auto_rollback: true
  
  - metric: content_dwell_time
    max_allowed_degradation_pct: 20
    auto_rollback: false    # flag and review; some CTA tests legitimately reduce dwell
    note: "For educational content tests, a dwell time drop may indicate the variant is converting faster (good) not worse"
```

---

## 5. Rollout Stages

```yaml
rollout_stages:
  stages:
    - stage: 1; traffic_pct: 5; audience: "Internal accounts"; hold_days: 2
    - stage: 2; traffic_pct: 10; hold_days: 3
    - stage: 3; traffic_pct: 25; hold_days: 3
    - stage: 4; traffic_pct: 50; hold_days: 5; human_sign_off: required
    - stage: 5; traffic_pct: 100; observation_days: 7
  
  auto_rollback_trigger: "Any guardrail metric degrades beyond threshold at any stage"
  
  wine_exceptions:
    - "Do not advance rollout stages within 72 hours of Valentine's Day, Thanksgiving, or holiday peak — behavior is not representative of steady state"
    - "Rollout for limited allocation page changes must complete within 5 days of campaign launch — no multi-week rollouts for time-sensitive campaigns"
    - "New arrival page changes should complete rollout within 14 days of arrival date — relevance window is short"
```

---

## 6. Versioning

```yaml
experimentation_md_wine:
  version: "1.0.0"
  last_updated: "2026-03-21"
  updated_by: "Wine marketing system operator"
  review_cadence: "Quarterly — add test results to learning library; update seasonal warnings"
  
  changelog:
    - version: "1.0.0"
      date: "2026-03-21"
      changes: "Initial release"
  
  mcp_alignment: "Test creation and results stored in MCP via create_ab_test(), get_ab_test_results(), list_ab_tests()"
```
