# SIGNALS.MD — Wine E-Commerce
*Companion file to MARKETING.MD — Behavioral signals and triggered response configuration*
*Loaded by: triggered-messaging agents, CRM automation agents, plan-campaign skill, campaign-planning agents*
*Authority: This file is the sole authority for triggered signal configuration — detection logic, response rules, copy angles, suppression conditions, conflict resolution, and signal priority order.*

---

## Signal Priority Order

When multiple signals are active for the same customer simultaneously, resolve in this order:

1. **Compliance & suppression** — always wins; blocks all other responses
2. **Purchase intent** (cart abandon, wishlist, repeated PDP) — respond within hours
3. **Post-purchase** — customer just bought; sequence suppresses campaigns for 7 days
4. **Lifecycle risk** (churn threshold, RFM degradation) — adapt tone, do not suppress
5. **Engagement signals** — inform personalization; do not affect timing

---

## Purchase Intent Signals

```yaml
intent_signals:

  cart_abandon:
    detection: "add_to_cart event; session ends or 30+ minutes of inactivity; no purchase"
    response: cart_abandon_email
    delay_minutes: 45
    channel: email
    copy_angle: "Retrieval, not urgency — 'your wine is still waiting.' Mention the specific SKU by name. Add one pairing note to reward the click."
    suppress_if: "customer purchases before delay elapses OR is globally suppressed OR purchased same SKU in last 30 days"
    suppression_after_send: "48 hours campaign-scoped — do not re-trigger on next session"
    persona_adaptation:
      Collector: "Add drinking window note to the cart abandon email — they are evaluating, not forgetting"
      Deal Seeker: "Mention if a promotion is active on the SKU"
    priority: high

  repeated_pdp_view:
    detection: "3+ views of the same SKU PDP within 7 days; no purchase"
    response: high_intent_email OR low_stock_onsite_nudge
    channel: email + on-site
    copy_angle: "Acknowledge the consideration without being surveillance-obvious — 'still thinking about [wine name]? here is what makes it worth it.'"
    trigger_low_stock_urgency_if: "inventory_count < 20 units — honest scarcity, not manufactured"
    suppress_if: "customer already owns this SKU (check purchase history)"
    persona_adaptation:
      Explorer: "Add a 'why this wine is worth the decision' knowledge note"
      Collector: "Add press score and drinking window if available"
      Deal Seeker: "Mention if a discount is available or coming soon"
    priority: high

  wishlist_add_no_purchase:
    detection: "wishlist_add event; no purchase of that SKU within 7 days"
    response: wishlist_reminder_email
    delay_days: 7
    channel: email
    copy_angle: "The wine they saved — still available. Add one new detail they didn't have when they saved it (new pairing, an occasion it's perfect for)."
    suppress_if: "SKU is out of stock OR customer purchased SKU OR is globally suppressed"
    priority: medium

  high_intent_browse_session:
    detection: "Session with 4+ PDP views, scroll_depth > 70% on at least one, no add-to-cart"
    response: onsite_intervention — soft cross-sell drawer or 'need help choosing?' prompt
    channel: on-site only
    copy_angle: "Helpful, not tracking-obvious — 'not sure which to choose? here are our picks this week.'"
    priority: medium

  restock_of_viewed_sku:
    detection: "SKU that customer viewed 2+ times in last 30 days transitions from out_of_stock to in_stock"
    response: restock_notification_email
    channel: email
    copy_angle: "It's back — and here's why it was worth waiting for."
    suppress_if: "customer already purchased a restock email for this SKU in last 90 days"
    priority: medium
    wine_specific: true

  new_vintage_of_purchased_varietal:
    detection: "A new vintage of a varietal the customer has purchased is added to catalog OR a new release from a producer they've bought before"
    response: new_vintage_alert_email
    channel: email
    copy_angle: "Vintage-aware, insider-feeling — 'the [YEAR] [wine] is here. Here is how it compares to the vintage you loved.'"
    target_personas: [Loyalist, Collector]
    suppress_if: "customer is globally suppressed OR already received this vintage alert"
    priority: medium
    wine_specific: true

  low_stock_on_viewed_sku:
    detection: "SKU a customer has viewed 2+ times in last 14 days drops below 20 units"
    response: low_stock_nudge_email OR onsite_urgency_banner
    channel: email + on-site
    copy_angle: "Honest scarcity — state the exact number. Do not manufacture urgency."
    suppress_if: "customer already purchased this SKU OR is globally suppressed"
    priority: medium
    wine_specific: true
```

---

## Post-Purchase Signals

```yaml
post_purchase_signals:

  first_purchase_completed:
    detection: "Purchase event; order_count = 1"
    response: first_purchase_welcome_sequence (see companion/LIFECYCLE.MD)
    channel: email
    suppress_campaigns_for_days: 7
    priority: high

  repeat_purchase_milestone:
    detection: "Purchase event; order_count crosses 5 or 10"
    response: loyalty_acknowledgment_email
    channel: email
    delay_hours: 24
    priority: medium

  high_value_order_placed:
    detection: "Order AOV > $200"
    response: high_value_followup_email (see companion/LIFECYCLE.MD)
    channel: email
    delay_hours: 48
    suppress_if: "customer has placed 3+ orders above $200"
    priority: medium

  gift_purchase_detected:
    detection: "Gift wrapping selected OR ship-to address differs from billing OR gift message submitted"
    response: "Tag customer as Gifter persona if not already; queue next-occasion reminder"
    channel: internal_tag + future_triggered_email
    timing: "Reminder email fires [N] days before next relevant occasion"
    priority: low
    wine_specific: true

  post_purchase_review_window:
    detection: "14 days after estimated delivery of a purchase"
    response: review_request_email
    channel: email
    copy_angle: "Conversational, not transactional — 'how was it?' not 'leave a review'"
    suppress_if: "customer has already left a review for this SKU OR is in winback sequence"
    priority: low
```

---

## Lifecycle Risk Signals

```yaml
lifecycle_risk_signals:

  churn_risk_threshold_crossed:
    detection: "churn_risk_score rises above 0.70 on weekly model refresh"
    response: "Move to lapsed lifecycle stage; trigger winback_campaign if not in 60-day cooldown"
    channel: email
    suppress_if: "customer received winback email in last 60 days"
    persona_note: "Collector churn threshold is 0.75 — their long natural cadence means 0.70 produces false positives."
    priority: high

  rfm_tier_degradation:
    detection: "RFM tier drops 2+ levels on weekly refresh (e.g., Champions → At Risk)"
    response: "Flag for human review if CLV > $300; else move to at_risk sequence"
    channel: human_alert + email sequence
    priority: high

  at_risk_no_engagement:
    detection: "Customer in at_risk stage; 0 email opens in last 30 days AND no site visits"
    response: "Escalate to lapsed; single winback send authorized"
    channel: email
    suppress_if: "already in lapsed or churned state"
    priority: medium

  occasion_window_missed:
    detection: "A Gifter persona customer did not purchase during an occasion window they have historically purchased in (e.g., bought Valentine's Day wine last year, no purchase this year)"
    response: "Soft post-occasion reengagement — 'hope the holiday was wonderful. here is what we have for next time.'"
    channel: email
    timing: "7 days after the occasion end date"
    priority: medium
    wine_specific: true

  allocation_customer_inactive:
    detection: "Customer who has historically purchased limited allocation or pre-order SKUs has not engaged with last 2 allocation campaigns"
    response: "Human review flag — do not automate; Collector/Loyalist relationship requires personal touch"
    channel: human_alert only
    priority: medium
    wine_specific: true
```

---

## Engagement Signals

```yaml
engagement_signals:

  email_click_no_purchase:
    detection: "Email link click; no purchase within 48 hours; linked to a specific SKU"
    response: browse_abandon_nudge (lighter than cart abandon — no item was added)
    channel: email
    delay_hours: 24
    copy_angle: "Gentle retrieval — 'you looked at [wine]. still curious?' Add one new detail."
    suppress_if: "customer purchased linked SKU OR is in cart_abandon window for same SKU"
    priority: medium

  educational_content_high_engagement:
    detection: "blog_view or region_guide_view with scroll_depth > 80% AND dwell > 180 seconds"
    response: "Tag interest in content topic (varietal/region); seed next recommendation batch with related SKUs"
    channel: internal_tag + future_email_personalization
    delay: "Include in next scheduled campaign personalization — not an immediate trigger"
    priority: low

  content_to_pdp_drop_off:
    detection: "blog_view → pdp_view within same session; no add-to-cart"
    response: "Add to high-intent segment for that SKU — eligible for repeated_pdp_view trigger on next visit"
    channel: internal_segment_update
    priority: low

  consistent_non_opener:
    detection: "0 email opens in last 12 sends (minimum 8 sends in window)"
    response: "Reduce to monthly digest cadence; schedule re-permission email at 90 days of silence"
    channel: frequency_reduction + future_sunset_flow
    priority: low

  blog_varietal_interest_signal:
    detection: "Customer reads 2+ blog posts about the same varietal or region within 30 days"
    response: "Elevate that varietal/region in next recommendation email; flag for potential new arrival campaign targeting"
    channel: internal_personalization_update
    priority: low
    wine_specific: true
```

---

## Signal Conflict Resolution

```yaml
signal_conflict_resolution:

  simultaneous_trigger_rules:
    - "Compliance signals block everything — no exceptions"
    - "Cart abandon takes priority over any same-day campaign send — fire cart abandon first, delay campaign by 24 hours"
    - "Post-purchase sequence (days 0–7) suppresses all promotional campaign sends — transactional sequences still fire"
    - "Winback and any promotional campaign must be separated by 7 days minimum"
    - "Low-stock nudge and cart abandon for the same SKU should not fire on the same day — cart abandon takes priority"
    - "Never fire a restock notification and a promotional campaign for the same SKU on the same day — choose the stronger message"

  max_triggered_messages:
    per_day: 1         # maximum one triggered message per customer per day
    per_week: 3        # counts against global email frequency cap
    exceptions: [order_confirmation, shipping_notification]   # transactional always fires

  signal_expiry:
    cart_abandon: "Expires 48 hours after trigger — if customer hasn't purchased, let standard campaigns take over"
    repeated_pdp: "Expires when customer purchases SKU or 14 days after last PDP view"
    wishlist_add: "Expires when customer purchases SKU or SKU goes out of stock"
    low_stock_nudge: "Expires when inventory restocks above 20 units or SKU sells out"
    churn_risk: "Refreshed weekly — does not expire until stage transitions"
```

---

## Versioning

```yaml
signals_md_wine:
  version: "1.0.0"
  last_updated: "2026-03-22"
  updated_by: "Wine marketing system operator"
  review_cadence: "Quarterly — verify trigger thresholds; update copy angles as needed"

  changelog:
    - version: "1.0.0"
      date: "2026-03-22"
      changes: "Initial release — moved from MARKETING.md Section 8 (Categories 2–5 and conflict resolution)"
```
