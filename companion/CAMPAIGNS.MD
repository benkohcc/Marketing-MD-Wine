# CAMPAIGNS.MD — Wine E-Commerce
*Companion file to MARKETING-wine-ecommerce.md — Campaign type blueprints and copy guidance*
*Loaded by: plan-campaign skill, all campaign-planning and campaign-execution agents*
*Authority: This file is the sole authority for campaign type configuration. MARKETING.md Section 4 contains a glossary of type names; this file contains full blueprints.*

---

## What This File Is

Every campaign has exactly one type. Type determines default channels, tone angle, KPI hierarchy, send cadence, discount behavior, paid media rules, and suppression behavior. Agents must not override these defaults without a campaign-brief-level instruction from the queue.

---

## Campaign Type Blueprints

### Type: new_arrival

```yaml
trigger: "Human queue request, or new SKU detected in catalog"
default_channels: [email, social]
tone_angle: "Excitement and discovery — lead with story, not sell. The wine arrives; let it speak."
primary_kpis: [pdp_view_rate, add_to_cart_rate, view_to_cart_rate]
secondary_kpis: [email_open_rate, social_engagement_rate]
budget_range: "$200–500"
send_cadence: "Single launch send on arrival_date. Optional teaser 48h prior if brief notes request it. No reminder send."
discount: false
paid_media: false  # Retargeting allowed after day 7 if view_to_cart_rate > 10%
primary_personas: [Explorer, Loyalist]
suppression_notes: "No post-purchase suppression — this is awareness. Do not suppress recent buyers of similar wines."
```

**Copy guidance:** Never include a discount code or urgency language. Lead with the winemaker story or vintage conditions. The PDP update should carry "Just arrived — here's what makes this special" framing, not promotional language.

---

### Type: promotion

```yaml
trigger: "Human queue request, or inventory overstock detected above margin threshold"
default_channels: [email, paid, social]
tone_angle: "Offer-forward, then justified by wine story. The discount leads. The story is why it's worth buying even at full price."
primary_kpis: [units_sold, revenue, email_conversion_rate, paid_roas]
secondary_kpis: [discount_redemption_rate, margin_impact]
budget_range: "8–12% of GMV target"
send_cadence: "Day 1 launch → Day 3 reminder to non-openers → Day before expiry final send"
discount: true  # discount_code required in brief
paid_media: true
primary_personas: [Deal Seeker, Loyalist]
suppression_notes: "Suppress customers who purchased at full price in last 60 days. Add to suppression list at purchase during campaign."
```

**Copy guidance:** Lead every asset with the discount code prominently. Subject line A: discount-led ("15% off today"). Subject line B: urgency-led ("Your Bordeaux window is closing"). PDP short description must include the offer alongside tasting notes.

---

### Type: limited_allocation

```yaml
trigger: "Human queue request, or high_intent + stock < 30 units detected"
default_channels: [email, social]
tone_angle: "Scarcity and exclusivity — honest about the number. State the exact allocation in the opening line."
primary_kpis: [sell_through_speed, time_to_sellout]
secondary_kpis: [email_open_rate, tier_1_vs_tier_2_conversion_split]
budget_range: "$100–200"
send_cadence: "Single send to top 20% CLV first. If allocation_units > 50% remain after 48h, second wave to broader segment. No further sends."
discount: false  # Scarcity is the mechanism, not price
paid_media: false  # Paid spend on allocation campaigns signals desperation
primary_personas: [Loyalist, Collector]
suppression_notes: "Auto-cancel all queued sends when inventory alert fires for this SKU."
```

**Copy guidance:** State the exact number of bottles or cases in the opening line. Never include a discount code. Social posts use bold, honest quantity language ("Only 24 cases. Gone when they're gone."). When the SKU sells out, publish a sold-out post immediately.

---

### Type: seasonal

```yaml
trigger: "Human queue request, or upcoming event in seasonal_calendar within lead_time_days"
default_channels: [email, paid, social]
tone_angle: "Occasion-first, gift-framing, warm. The wine is the answer to the occasion moment, not a product being pushed."
primary_kpis: [revenue, new_customer_acquisition_rate]
secondary_kpis: [email_open_rate, attribution_complexity_note]
budget_range: "Highest budget allocation of all campaign types"
send_cadence: "7 days before occasion → 2 days before → on-the-day (email). Social: 7 days before + 2 days before + on-the-day. Paid: run full window."
discount: false  # Optional — include only if margin and positioning allow
paid_media: true  # Prospecting allowed — gift buyers who don't know the store are valid targets
primary_personas: [Gifter, Explorer]
suppression_notes: "No post-purchase suppression — seasonal gifts are bought for others. Concurrent campaigns may confound attribution; note in retrospective."
```

**Copy guidance:** Occasion leads in every asset. The wine is the answer, not the subject. For multi-SKU seasonal briefs, use carousel format in social to show options. Paid copy includes the occasion prominently ("Perfect for Mother's Day").

---

### Type: winback

```yaml
trigger: "churn_risk_score > 0.70 detected in segment, or human queue request"
default_channels: [email]
tone_angle: "Personal, warm, non-pushy. Lead with the relationship, not the product. Acknowledge the gap. No urgency."
primary_kpis: [reactivation_rate, second_purchase_rate_90d]
secondary_kpis: [email_open_rate]
budget_range: "$0 paid spend"
send_cadence: "Single send only. No follow-up. No reminder."
discount: false  # Prefer soft offer (free shipping) over discount — discount signals desperation
paid_media: false  # Winback is a CRM play, never acquisition
primary_personas: [Loyalist, Explorer]
suppression_notes: "Suppress anyone who received a winback email in the last 60 days. Check is_suppressed() before every trigger. Add 60-day suppression after send."
```

**Copy guidance:** Subject line is relationship-led ("We've been thinking about you"). Body acknowledges the gap warmly, shows what's new since they last visited, soft offer (if any) at the very end. No urgency language anywhere.

---

### Type: educational

```yaml
trigger: "SEO content request in queue, or demand gap with search_volume > 50/month"
default_channels: [email, seo]
tone_angle: "Genuinely informative — write as an expert, not a salesperson. No selling until the very end, and even then, softly."
primary_kpis: [content_dwell_time, scroll_depth, pdp_click_rate]
secondary_kpis: [downstream_conversion_rate_14d]
budget_range: "$0 paid spend"
send_cadence: "Single send. No reminder."
discount: false
paid_media: false
primary_personas: [Explorer]
suppression_notes: "Standard fatigue guard applies. No post-purchase suppression — educational content is for everyone."
```

**Copy guidance:** Blog posts 1,200–1,500 words. H2 subheadings required for SEO. CTA at end is soft ("Explore our Barolo collection"), never a hard sell. Email subject line is knowledge-led ("The definitive guide to Barolo's eleven communes"). No discount code, no urgency language anywhere.

---

### Type: bundle

```yaml
trigger: "Human queue request, or strong get_frequently_bought_together signal"
default_channels: [email, social]
tone_angle: "Pairing concept — these were made for each other. The logic of why they belong together matters as much as the offer."
primary_kpis: [avg_order_value, basket_size]
secondary_kpis: [revenue, units_sold_per_sku]
budget_range: "$200–400"
send_cadence: "Launch send → one reminder at day 5."
discount: false  # Optional price framing — call out bundle value, not discount
paid_media: false  # Light retargeting only, no prospecting
primary_personas: [Explorer, Gifter]
suppression_notes: "Suppress customers who already purchased both bundle SKUs."
```

**Copy guidance:** Call `get_frequently_bought_together()` to validate the pairing rationale before briefing. The pairing story must be specific — why these two wines, why together, why now. Social visual: both bottles together. Do not lead with price.

---

### Type: pre_order

```yaml
trigger: "Human queue request for an upcoming arrival"
default_channels: [email, social]
tone_angle: "Insider access, anticipation, future-facing. You're being invited in before anyone else."
primary_kpis: [reservation_count, deposit_completion_rate]
secondary_kpis: [email_open_rate, social_click_through_rate]
budget_range: "$100–200"
send_cadence: "Launch send when reservation opens → reminder 3 days before close → fulfilment send on arrival_date."
discount: false  # Early access exclusivity is the value — discounts cheapen it
paid_media: false
primary_personas: [Loyalist, Collector]
suppression_notes: "No inventory constraint — set allocation_units as a cap if applicable. Track drop-off between email open → reservation page → completion."
```

**Copy guidance:** Arrival date must appear prominently in the email. Subject line is exclusivity-led ("Reserve yours before it arrives"). Build desire around what's coming — don't oversell a wine the customer hasn't tasted yet.

---

## Campaign Type Quick Reference

| Type | Channels | Discount | Paid | Primary KPI | Primary Persona |
|------|---------|---------|------|------------|----------------|
| new_arrival | email, social | No | No | pdp_view_rate | Explorer, Loyalist |
| promotion | email, paid, social | Yes | Yes | units_sold, revenue | Deal Seeker, Loyalist |
| limited_allocation | email, social | No | No | sell_through_speed | Loyalist, Collector |
| seasonal | email, paid, social | Optional | Yes | revenue | Gifter, Explorer |
| winback | email | Optional (soft) | No | reactivation_rate | Loyalist, Explorer |
| educational | email, seo | No | No | content_dwell_time | Explorer |
| bundle | email, social | Optional | No | avg_order_value | Explorer, Gifter |
| pre_order | email, social | No | No | reservation_count | Loyalist, Collector |
