# LIFECYCLE.MD — Wine E-Commerce
*Companion file to MARKETING.MD — Customer value tiers, lifecycle stage definitions, post-purchase sequences, and lifecycle strategy*
*Loaded by: lifecycle-analysis skill, plan-campaign skill, winback agents*
*Authority: This file is the sole authority for customer value tiers, lifecycle stage definitions and transitions, post-purchase sequences, lifecycle × persona matrix, and acquisition vs. retention strategy.*

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

## 6. Lifecycle Stage Definitions & Transitions

> These stages define the operational state of each customer and drive triggered messaging. Unlike customer value tiers (Section 1), these stages are transient — a customer moves between them based on purchase behavior. Wine buyers do not move linearly: a Collector may be dormant for 8 months and then drop $800 in a single pre-order. Dormancy is not always churn.

```yaml
lifecycle_stages:

  new:
    definition: "First purchase made within the last 60 days"
    goal: "Drive second purchase before the initial excitement fades"
    primary_kpi: second_purchase_rate_30d
    success_threshold: "35%+ convert to second purchase within 30 days"
    marketing_response: first_purchase_welcome_sequence
    transition_to_active:
      condition: "second purchase made"
    transition_to_at_risk:
      condition: "no second purchase within 60 days of first"
    persona_note: "Explorers and Gifters move here fastest. Collectors and Loyalists may skip — they often arrive already knowing exactly what they want."

  active:
    definition: "2+ lifetime purchases; last purchase within 90 days"
    goal: "Increase purchase frequency and deepen category preference"
    primary_kpi: purchase_frequency_90d
    success_threshold: "3+ purchases per rolling 90-day window"
    marketing_response: standard_campaign_cadence
    transition_to_at_risk:
      condition: "no purchase in 90 days"
    loyalty_upgrade_trigger: "5+ purchases OR CLV > $500 — consider Loyalist persona reclassification"

  at_risk:
    definition: "Previously active; no purchase in 90–180 days OR churn_risk_score > 0.50"
    goal: "Re-engage before full lapse — this is a softer touch than winback"
    primary_kpi: reactivation_rate
    success_threshold: "20%+ make a purchase within 30 days of at-risk sequence"
    marketing_response: soft_reengagement_sequence
    important: "This is NOT a winback campaign. No hard offer. Show what is new."
    transition_to_active:
      condition: "purchase made"
    transition_to_lapsed:
      condition: "no purchase after soft reengagement, or 180 days elapsed since last purchase"
    persona_note: "Do not trigger at-risk for Collectors — their purchase cadence is naturally long. Only flag if churn_risk_score > 0.65."

  lapsed:
    definition: "No purchase in 180+ days AND churn_risk_score > 0.70"
    goal: "Win back with a single well-crafted send, or sunset gracefully"
    primary_kpi: winback_conversion_rate
    success_threshold: "15%+ make a purchase within 30 days of winback send"
    marketing_response: winback_campaign   # single send — see companion/CAMPAIGNS.MD: winback
    transition_to_active:
      condition: "purchase made"
    transition_to_churned:
      condition: "no response after 3 winback attempts across 180+ days"
    persona_note: "A lapsed Collector with high historical CLV should be flagged for human review before any automated winback. Manual outreach from the store owner is often more effective."

  churned:
    definition: "No response after 3 winback attempts, or 365+ days since last purchase"
    goal: "Suppress from campaign sends; retain address for annual re-permission attempt"
    primary_kpi: re_permission_rate
    marketing_response: annual_sunset_email   # one send per year — 'still want to hear from us?'
    reactivation_path: "Manual only for CLV > $300 — flag for human review"
```

---

## 7. Post-Purchase Sequences

> These sequences fire after a transaction regardless of which campaign drove it. They are relationship-building, not promotional. Never frequency-cap away a day-0 order confirmation. The welcome sequence is the highest-leverage touchpoint in the customer lifecycle.

```yaml
post_purchase_sequences:

  first_purchase_welcome:
    trigger: "First purchase completed; customer lifecycle_stage transitions to 'new'"
    channel: email
    goal: "Confirm, orient, and plant the seed for the second purchase"
    sends:
      - timing: immediate
        type: order_confirmation
        tone: "Warm and practical — confirm the order, express genuine enthusiasm for the wine they chose"
        content: "Order details + one sentence about the wine they bought (pull from tasting_notes) + shipping ETA"

      - timing: day_3
        type: product_guidance
        tone: "Knowledgeable and generous — help them get the most from what they bought"
        content_angle: "Serving temperature, decanting guidance if applicable, food pairing specific to their SKU. Pull from product catalog metadata."
        persona_adaptation:
          Explorer: "Frame as 'now that you have it, here is what makes it special'"
          Gifter: "Frame as 'here is what to tell them about the wine you chose'"

      - timing: day_14
        type: discovery_nudge
        tone: "Curious, not pushy — 'based on what you loved...'"
        content: "2–3 recommendations from get_recommendations(context: 'email') seeded by their purchase"
        call_to_action: "Soft — browse, not buy"

    suppression: "Respect global frequency cap on day 14 send only. Day 0 and Day 3 are exempt — they are transactional."

  repeat_purchase_acknowledgment:
    trigger: "5th or 10th purchase milestone"
    channel: email
    delay_hours: 24   # let the order confirmation land first
    goal: "Recognize loyalty without false intimacy — one genuine line, then value"
    tone: "Brief and real — 'you know your wine. here is something you probably haven't tried.'"
    content: "One curated recommendation from their varietal affinity profile, with a producer note"

  high_value_order_followup:
    trigger: "Order AOV > $200"
    channel: email
    delay_hours: 48
    goal: "Reinforce confidence in a significant purchase — validate, add context"
    tone: "Knowledgeable and assured — they made a good call, here is why"
    content: "Drinking window guidance for their specific SKU + cellar or storage tip if applicable"
    suppress_if: "customer has placed 3+ orders above $200 — they do not need reassurance"
    persona_note: "Collector persona: include press score and vintage notes if available. Loyalist: emphasize the producer relationship."

  gift_purchase_followup:
    trigger: "Gift wrapping selected, gift message submitted, or ship-to address differs from billing"
    channel: email
    delay_days: 3_after_estimated_delivery
    goal: "Close the gifting loop and seed the next occasion"
    tone: "Warm and occasion-aware"
    content: "Hope the gift landed well + plant the next occasion ('Mother's Day is [N] weeks away')"
    internal_action: "Tag customer as Gifter persona if not already classified. Add next relevant occasion to reminder queue."
```

---

## 8. Lifecycle × Persona Matrix

> Wine personas do not move through the lifecycle at the same speed or in the same pattern. This matrix tells AI agents what to expect and how to adapt when lifecycle stage and persona intersect.

| Persona | Typical Journey Shape | Normal Dormancy Period | At-Risk Signal | Winback Approach |
|---------|----------------------|----------------------|---------------|-----------------|
| Explorer | Fast to active; can stall if no new discovery stimulus | 30–60 days | No blog or PDP engagement for 60 days | New arrival in a region they've browsed; knowledge hook |
| Gifter | Bursty — occasion-driven; long gaps between purchases are *normal* | 60–120 days between occasions | Missing a historically purchased occasion window | Next occasion reminder; gift framing |
| Loyalist | Linear and consistent once established; a long gap is a genuine signal | 30–45 days | Silence during a new arrival in their preferred varietal | New arrival in their category; insider framing |
| Deal Seeker | Promotion-activated; dormancy between promotions is *expected* | 60–90 days between promotion windows | Not opening promotional emails | Strong offer; urgency; do not use story-led copy |
| Collector | Very long natural cadence; 6–8 months between purchases is normal | Up to 180 days | Missing a pre-order or allocation event they historically engaged | Allocation or vintage-specific outreach; never discount |

---

## 9. Versioning

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
