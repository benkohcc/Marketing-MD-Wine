# LIFECYCLE.MD — Wine E-Commerce
*Companion file to MARKETING-wine-ecommerce.md — Customer value tiers, winback rules, and lifecycle strategy*
*Loaded by: lifecycle-analysis skill, plan-campaign skill, winback agents*

---

## 1. Customer Value Tiers

```yaml
customer_value_tiers:
  
  vip:
    definition: "CLV > $2,000 OR Collector persona with 5+ purchases OR any customer with a single order > $500"
    treatment: "Human review before any automated campaign targeting; personal outreach from store owner for allocation and pre-order"
    communication_style: "Direct, expert, exclusive — promotional tone is never appropriate"
    agent_authority: "Flag for human review; do not include in any automated promotional campaign"
    natural_dormancy: "Up to 180 days between purchases is normal cellar accumulation behavior — do not trigger winback within 180 days"
    allocation_access: "Priority access to new allocation wines; notification comes from store owner directly"
    critical_rule: "If a VIP customer unsubscribes, do not attempt re-permission for 6 months. Their relationship with the brand is valuable enough to respect their decision."
  
  loyalist:
    definition: "CLV $300–$2,000; 3+ purchases; persona: Loyalist; active within 90 days"
    treatment: "Standard Loyalist campaign cadence; first-tier access to limited releases and new arrivals before general list"
    communication_style: "Knowledgeable, insider-feeling, assumes depth"
    agent_authority: "Standard campaign automation permitted; no promotional campaigns in their primary preferred category"
    natural_dormancy: "Up to 120 days is normal — Loyalists buy with purpose, not constantly"
  
  regular:
    definition: "2–4 purchases; CLV $80–$300; active within 60 days; persona: Explorer or Gifter"
    treatment: "Standard campaign cadence; second-purchase nurture priority for newer members of this tier"
    agent_authority: "Full automation permitted within campaign type defaults"
  
  new:
    definition: "First purchase within 30 days; no persona classification yet"
    treatment: "Welcome sequence; active second-purchase nurture; begin persona classification"
    agent_authority: "Welcome sequence fully automated; second-purchase campaign automated"
    persona_classification_timing: "Classify after 2nd purchase or 60 days of behavioral signals, whichever comes first"
  
  at_risk:
    definition: "Previously active customer; churn_risk_score > 0.6; no purchase in 60–120 days"
    treatment: "Soft reengagement — not winback language; educational content preferred over promotion"
    agent_authority: "Soft reengagement content automated; any promotional offer requires brief approval"
    wine_note: "Before triggering at-risk for a Loyalist, check their natural dormancy window — some Loyalists simply buy quarterly"
  
  lapsed:
    definition: "No purchase in 120+ days; churn_risk_score > 0.7; not VIP tier"
    treatment: "Single-send winback attempt; sunset sequence if no response"
    agent_authority: "Winback automated per Section 3; VIP lapsed → human review before any send"
  
  churned:
    definition: "2+ failed winback attempts; 240+ days since last purchase"
    treatment: "Annual re-permission email only; no other promotional contact"
    agent_authority: "Annual re-permission automated; no other sends without human approval"
    suppression_note: "Customers who unsubscribed are permanently suppressed — never re-permission an unsubscribe"
```

---

## 2. Acquisition vs. Retention Strategy

```yaml
acquisition_retention_balance:
  
  current_stage: "early_growth"
  
  target_spend_split:
    acquisition: 60%
    retention: 40%
    note: "Review quarterly; shift toward 50/50 as repeat purchase rate improves; shift toward 40/60 at maturity"
  
  acquisition_rules:
    target_cac: $45
    max_cac: $80
    cac_to_ltv_minimum_ratio: "1:4"
    ltv_measurement_window: "12-month"
    
    quality_guard:
      min_first_order_value: $35
      preferred_acquisition_personas: [Explorer, Gifter]
      note: "Deal Seeker acquisition is acceptable if AOV is above floor — they can be converted to repeat buyers with the right cadence"
      avoid_acquiring: "Customers whose first order is entirely discount-driven with no organic browse signal — their retention rate is significantly lower"
  
  retention_investment_priority:
    1: "VIP / Collector — protect the relationship at any cost within reason"
    2: "At-risk Loyalist with CLV > $500 — early intervention is high ROI"
    3: "New customers — convert to second purchase within 30 days"
    4: "Lapsed Explorer with 3+ purchases — selective winback is worth the attempt"
    5: "Lapsed Deal Seeker with CLV < $100 — sunset gracefully; do not over-invest"
  
  second_purchase_urgency: "Second purchase is the most important conversion in wine e-commerce. A customer who makes a second purchase within 30 days has 4× the 12-month retention rate of a customer who waits longer."
  
  budget_within_retention:
    second_purchase_nurture: 30%
    at_risk_reengagement: 25%
    loyalty_deepening: 25%
    winback: 20%
```

---

## 3. Winback Rules

```yaml
winback_rules:
  
  eligibility:
    min_days_since_last_purchase: 120
    churn_risk_threshold: 0.7
    min_historical_purchases: 2
    clv_minimum: $80
    excluded: ["VIP tier — human review required", "Unsubscribers — never winback"]
  
  offer_hierarchy:
    tier_1:
      offer: "Free shipping on next order — no discount"
      applies_to: "Explorer, Gifter, Loyalist (in non-primary categories)"
      rationale: "Preserves price integrity; tests re-engagement without conditioning on discount"
      wait_before_escalating_days: 14
    
    tier_2:
      offer: "10% discount on any bottle in [their browsed or purchased category]"
      applies_to: "Explorer, Gifter, Deal Seeker — not Loyalist in primary category"
      escalation_trigger: "No open or click on tier_1 after 14 days"
      wait_before_escalating_days: 14
    
    tier_3:
      offer: "Human review only — not automated"
      applies_to: "Customers where tier_1 and tier_2 have both been attempted and failed"
      options: "Re-permission email with no offer; or sunset"
  
  winback_sequence_cadence:
    day_0: "Tier 1 send"
    day_14: "Tier 2 send if day_0 had no click"
    day_28: "Sunset email if day_14 had no click"
    day_366: "Annual re-permission if still opted in"
  
  persona_winback_rules:
    Explorer: "Lead with a discovery angle — 'Something new worth exploring' + free shipping; escalate to 10% if no response"
    Gifter: "Lead with occasion framing — time the winback send to an upcoming seasonal occasion; offer gift guide"
    Loyalist:
      rule: "Never lead with a discount in their primary category"
      approach: "Lead with a new vintage or producer arrival in a category adjacent to their primary. If no response after 21 days, single soft reach-out with free shipping. No discount on primary category."
    Deal_Seeker: "Lead directly with the offer — they respond to value, not story. Keep short and direct."
    Collector:
      rule: "Do not automate. Flag for human review. Store owner decides whether to reach out personally."
      dormancy_exception: "Up to 180 days without purchase does not trigger winback for Collectors"
  
  winback_copy_rules:
    - "Personal and warm — acknowledge the gap honestly without being apologetic"
    - "No urgency language — this is not a promotional email"
    - "Subject line must not reference how long they've been away"
    - "Never reference their last specific purchase in the subject line"
    - "Keep to 150 words or fewer — winback emails that are too long signal desperation"
    - "Soft offer in the closing paragraph — never the opening"
    
  sunset_process:
    trigger: "No open, click, or purchase after full winback sequence"
    action: "Single final 're-permission or goodbye' email"
    copy_tone: "Graceful and low-pressure — 'We'd love to stay in touch, but we'll respect your inbox if not'"
    on_no_response_to_sunset: "Move to suppressed annual re-permission list; no other contact"
```

---

## 4. Cross-Sell & Upsell Rules

```yaml
cross_sell_upsell:
  
  cross_sell:
    timing: "Day 3 post-purchase email (after delivery confirmation); cart cross-sell block; PDP frequently-bought-together"
    agent_authority: "Fully automated via get_frequently_bought_together() and get_recommendations()"
    
    wine_cross_sell_rules:
      - "Cross-sell wine must complement the purchased wine — same region + different varietal, or a food pairing suggestion"
      - "Never cross-sell a directly competing wine (different producer of the same varietal and vintage)"
      - "Cross-sell in cart must not disrupt checkout — one suggestion maximum, below the cart summary"
      - "For Collectors: cross-sell must be within their primary region or a prestige adjacent — not a casual everyday bottle"
      - "For Gifters: cross-sell post-purchase should be 'add a card' or 'add these for a complete gift' — not another bottle"
    
    post_purchase_cross_sell_timing:
      do_not_send_before: "Delivery confirmation received"
      send_on: "Day 3 after delivery confirmation"
      why: "Sending cross-sell before they've opened the bottle they just bought feels premature — let them enjoy the purchase first"
  
  upsell:
    timing: "PDP only — before add-to-cart; never in cart"
    agent_authority: "Automated within configuration below"
    
    wine_upsell_rules:
      - "Upsell must be the same varietal from a higher-prestige producer or better vintage"
      - "Price delta must be within 50% of the viewed wine's price — never push a 3× upgrade without context"
      - "Must include a clear reason: 'This is the premier cru version of the wine you're viewing — [specific difference]'"
      - "Never upsell in winback emails — relationship restoration before revenue"
      - "Never upsell a Collector on their primary category — they already know the pecking order"
  
  drinking_window_cross_sell:
    rule: "If a customer's purchase history shows they're accumulating cellaring wines, cross-sell a 'drink now' wine for everyday pleasure"
    rationale: "Collectors who only buy cellar wines are satisfied with us for futures but not for their weekly table — we can serve both needs"
    applies_to: [Collector, Loyalist_cellar_focused]
    copy_angle: "'For while you wait' — something to drink tonight while your cellar develops"
```

---

## 5. Customer Lifecycle Journey Milestones

```yaml
lifecycle_milestones:
  # Triggered automations at key moments — all within agent authority unless noted
  
  first_purchase:
    trigger: "Order confirmed"
    send: "Welcome sequence — Day 0 order confirmation + Day 3 delivery follow-up with tasting guide + Day 7 second-purchase nudge"
    goal: "Make the first purchase feel great; plant the seed for the second"
  
  second_purchase:
    trigger: "Second order confirmed"
    send: "Milestone acknowledgment — warm, not promotional; begin persona classification"
    note: "No discount with the second purchase acknowledgment — they came back without one"
  
  fifth_purchase:
    trigger: "Fifth order confirmed"
    send: "Loyalist upgrade notification — 'You've built a real relationship with us. Here's what that unlocks.' (early access, allocation priority)"
    goal: "Make them feel recognized; shift from transactional to relational"
  
  first_case_purchase:
    trigger: "Order of 12+ bottles"
    send: "Personal note from the store — humanize the relationship"
    note: "Human writes or reviews; not fully automated"
    follow_up: "Set a drinking window reminder sequence based on the wines in the case"
  
  first_allocation_purchase:
    trigger: "Pre-order or allocation reservation completed"
    send: "Allocation confirmation with full producer story + expected arrival window"
    follow_up: "Reminder when allocation ships; tasting note when delivered"
    goal: "Make allocation feel exclusive and well-served — this is how you convert Loyalists into Collectors"
  
  drinking_window_alert:
    trigger: "A wine in the customer's purchase history enters its optimal drinking window"
    send: "Friendly reminder — 'The [wine] you bought in [month] is entering its drinking window'"
    copy_tone: "Service-oriented — not promotional; this email is about their wine, not our next sale"
    agent_authority: "Automated if drinking window data exists in product catalog for the purchased SKU"
```

---

## 6. Versioning

```yaml
lifecycle_md_wine:
  version: "1.0.0"
  last_updated: "2026-03-21"
  updated_by: "Wine marketing system operator"
  review_cadence: "Quarterly — review tier CLV thresholds against actual CLV distribution; update winback offer hierarchy based on response rates"
  
  changelog:
    - version: "1.0.0"
      date: "2026-03-21"
      changes: "Initial release"
  
  mcp_alignment: "Aligned with wine-marketing-complete-spec v5.0.0; get_customer_segments(), get_churn_risk_scores(), and get_clv_predictions() are runtime sources for tier classification"
```
