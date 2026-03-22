# PERSONALIZATION.MD — Wine E-Commerce
*Companion file to MARKETING.MD — Recommendation engine, dynamic content, personalization governance*
*Loaded by: update-personalization skill, email agents, web experience agents*
*Authority: This file is the sole authority for personalization configuration — recommendation algorithm weights, diversity controls, anti-creepiness rules, per-page context rules, persona-specific personalization rules, and consent governance.*

---

## 1. Personalization Philosophy

```yaml
philosophy:
  goal: "Match the right wine to the right customer at the right moment — without making them feel watched"
  
  wine_specific_principle: >
    Wine personalization is uniquely high-stakes. A bad recommendation damages trust faster
    than a generic email. Recommending a heavy tannic Barolo to a Gifter buying for a casual
    dinner party is worse than recommending nothing. When we personalize, we must personalize
    correctly — or default to something we know is good.
  
  anti_creepiness_standard: >
    Wine buyers do not want to feel like we are tracking their drinking habits.
    Persona and category signals are fair game. Exact behavioral signals
    ('we noticed you looked at this wine 4 times') are not. The copy must feel
    like the recommendation of a knowledgeable friend, not a surveillance system.
```

---

## 2. Personalization Tiers

```yaml
tiers:
  
  tier_0_anonymous:
    identifier: "anonymous_id"
    signals_available:
      - "Current session browse (categories viewed, search queries, time on page)"
      - "Entry source and referrer"
      - "Device type and geo (state level for DTC shipping relevance)"
      - "Current session cart"
    
    permitted_personalization:
      - "Category-level collection sort based on session browse"
      - "State-appropriate shipping messaging (if state is shipping-eligible)"
      - "Trending wines in the category they're browsing"
      - "Session-context messaging (cart count, recently viewed in this session)"
    
    prohibited:
      - "Any reference to previous sessions — anonymous sessions have no memory"
      - "Inferring persona from a single session"
      - "Retargeting from fewer than 3 session signals"
  
  tier_1_engaged:
    identifier: "Email address captured; no purchase"
    signals_available:
      - "All anonymous signals"
      - "Email engagement: opens, clicks, category of links clicked"
      - "Browse history across sessions (if consented)"
    
    permitted_personalization:
      - "Category-based email content (clicked on Burgundy links → Burgundy-weighted recommendations)"
      - "Educational content matched to most-engaged category"
      - "New arrival notification for most-browsed category"
    
    prohibited:
      - "Naming specific wines they browsed in subject lines"
      - "Referencing specific price points they viewed"
      - "Inferring experience level from session behavior alone"
  
  tier_2_known:
    identifier: "Purchased or explicitly logged in; customer_id known"
    signals_available:
      - "Full purchase history with varietal, region, vintage, price tier"
      - "Persona classification (Explorer, Gifter, Loyalist, Deal Seeker, Collector)"
      - "RFM tier and CLV"
      - "Varietal affinity scores"
      - "Region affinity scores"
      - "Price tier affinity"
      - "Occasion purchase history (gift signals)"
      - "Lifecycle stage"
      - "Preferred drinking window profile (immediate vs. cellaring)"
    
    permitted_personalization:
      - "Full persona-appropriate tone and angle (per MESSAGING.MD by_persona)"
      - "Varietal and region affinity-based recommendations"
      - "Lifecycle-appropriate messaging and CTA strength"
      - "Price tier-appropriate recommendations (don't push Collector-tier to Explorer customers)"
      - "Occasion awareness (gift purchase history → upcoming occasion nudge)"
      - "Drinking window guidance based on previous purchase patterns"
    
    prohibited:
      - "Inferring health status or sensitive personal attributes from wine choice"
      - "Using gift purchase history to infer the buyer's personal taste"
      - "Revealing the data we hold ('we see you've purchased Barolo 4 times')"
      - "Cross-contaminating personas — a customer classified as Loyalist for Burgundy may be Explorer-level for other regions"
```

---

## 3. Recommendation Engine Configuration

```yaml
recommendation_engine:
  
  algorithms:
    collaborative_filtering:
      purpose: "Customers with similar purchase history also bought these wines"
      weight: 40%
      cold_start_threshold: "3 purchases minimum before collaborative filtering applies; use content-based below threshold"
      wine_note: "Collaborative filtering is strong in wine — taste preferences cluster reliably"
    
    content_based:
      purpose: "Recommend wines with similar attributes to what they've purchased"
      weight: 35%
      attributes_used:
        - varietal
        - region
        - sub_region
        - producer_tier
        - price_tier
        - body_weight    # light/medium/full
        - tannin_level
        - drinking_window_type    # immediate vs. cellarable
        - oak_influence
    
    popularity:
      purpose: "Trending and bestsellers — fallback for cold-start; adds diversity"
      weight: 15%
      window_days: 30
    
    campaign_boost:
      purpose: "Elevate active campaign SKUs"
      override_weight: "1.5× multiplier on base score (capped — never overrides relevance entirely)"
      max_boost_factor: 1.5
  
  wine_specific_diversity_controls:
    max_same_varietal_pct: 40%          # no more than 40% from the same varietal in any rec set
    max_same_region_pct: 50%            # no more than 50% from the same region
    exploration_ratio: 15%              # 15% of recs should be outside known affinity (discovery)
    out_of_stock_filter: true
    margin_floor_pct: 20%               # never recommend below this margin
    recently_purchased_window_days: 90  # suppress wines bought in the past 90 days (unless replenishment)
    allocation_wines_in_general_recs: false    # never surface allocation/pre-order wines in standard recommendation blocks
    drinking_window_filter:
      enabled: true
      rule: "For Collector customers, surface only wines within or approaching their drinking window — not wines that should be cellared further than their stated preferences"
  
  context_rules:
    homepage:
      blend: "40% affinity-based + 30% campaign boost + 30% trending"
      max_recommendations: 8
      persona_weighting: true
      wine_note: "Collector homepage should foreground their primary region; Explorer homepage should foreground discovery angle"
    
    product_detail_page:
      primary: "Same varietal, different producer or vintage"
      secondary: "Frequently bought together (verify from get_frequently_bought_together())"
      tertiary: "Same region, different varietal (cross-varietal discovery)"
      max_recommendations: 4
      must_not_show: "A lower-priced version of the wine they're viewing (implicit down-grade signal)"
    
    cart:
      primary: "Complementary varietal for the occasion (food pairing logic)"
      secondary: "Bundle opportunity (if get_bundle_candidates() returns a match)"
      max_recommendations: 2
      tone: "Soft suggestion — never disrupt checkout momentum"
      must_not_show: "A competing wine to one already in the cart"
    
    email:
      max_recommendations: 3
      inventory_check_at_send: true   # verify in-stock at send time, not at content creation
      persona_adaptation: true
      price_tier_filter: "Recommendations must stay within the customer's established price tier tolerance (± 20% of typical purchase price)"
    
    post_purchase_email:
      timing: "Day 3 after delivery confirmation"
      primary: "Complementary wine to pair with what they just received"
      secondary: "Educational content about the wine they bought (region, producer, drinking window)"
      must_not_show: "A competing alternative to what they just bought — they made their choice"
```

---

## 4. Persona-Specific Personalization Rules

```yaml
persona_personalization:
  
  Explorer:
    primary_signal: "Category browse patterns + content engagement + search queries"
    angle: "Discovery and education — show them something they haven't seen yet"
    recommendation_bias: "Emphasize exploration of new regions and varietals adjacent to what they know"
    content_personalization: "Educational blog content matched to most-browsed category"
    copy_adaptation: "Curious, enthusiastic, educational — treats them as an engaged learner"
    warning: "Don't overwhelm with too many options — Explorers respond to a clear, opinionated recommendation"
  
  Gifter:
    primary_signal: "Occasion seasonality + previous gift purchase price tier"
    angle: "Occasion framing and gift suitability — make the decision easy"
    recommendation_bias: "Gift-appropriate presentation, recognized producers, appropriate price tier"
    content_personalization: "Gift guide content, 'what to say when they open it' storytelling"
    copy_adaptation: "Confident, occasion-appropriate, social-proof-led"
    warning: "Never recommend their past gift purchases as new suggestions — they bought it for someone else"
    occasion_signals:
      - "Valentine's Day window (Feb 1–13): surface gift-appropriate reds and champagne"
      - "Mother's Day window (Apr 20 – May 11): surface Champagne, Rosé, elegant whites"
      - "Holiday window (Nov 25 – Dec 20): surface gift sets, prestige bottles, Champagne"
  
  Loyalist:
    primary_signal: "Purchase history in primary category + price tier + producer preferences"
    angle: "Insider access and depth — they know what they like; give them more of it at a higher level"
    recommendation_bias: "Within their primary category; adjacent producers they haven't tried; next-tier wines in their established region"
    content_personalization: "Vintage assessments, producer profiles, drinking window updates for their collection"
    copy_adaptation: "Expert-to-expert, respectful of their depth, no hand-holding"
    critical_rule: "Never recommend a downgrade or a discount on a wine they've purchased at full price. Never cross-sell outside their primary category with discount framing."
    suppression_rule: "Suppress any promotional language in their primary preferred category"
  
  Deal_Seeker:
    primary_signal: "Discount code usage + purchase timing (post-promotion) + price tier floor"
    angle: "Value capture — make the deal obvious and the urgency real"
    recommendation_bias: "Best value-to-quality ratio at their established price tier"
    content_personalization: "Sale notifications, flash deal alerts, bundle value messaging"
    copy_adaptation: "Direct, value-led, urgency-appropriate (with real deadlines)"
    retention_rule: "Do not suppress between promotions — they will engage again at the next offer. Maintain email cadence with non-promotional content."
  
  Collector:
    primary_signal: "Purchase history in primary region + producer tier + price tier + cellar purchase patterns"
    angle: "Allocation access and vintage intelligence — they want what most customers can't get"
    recommendation_bias: "Allocation and pre-order wines; prestige producers in their primary region; vintage intelligence"
    content_personalization: "Vintage assessments with specificity; drinking window reports for their cellar; producer news"
    copy_adaptation: "Expert, direct, information-dense — no marketing fluff; treat them as a peer"
    critical_rules:
      - "Automation restriction: do not automate outreach for Collector customers with CLV > $2,000. Human review before any major campaign targeting this segment."
      - "Never recommend a wine below their established price tier floor"
      - "Allocation invitations must come from the store owner — not from a generic campaign"
      - "Dormancy window: up to 180 days without purchase is normal cellar behavior — do not trigger winback until 180 days"
```

---

## 5. Anti-Creepiness Rules

```yaml
anti_creepiness:
  
  wine_copy_rules:
    never_write:
      - "'We noticed you've been looking at this Barolo' — surveillance language"
      - "'Based on your purchase history...' — makes the tracking explicit"
      - "'We know you love Burgundy' — presumptuous; use 'Your Burgundy collection' only if they've made 3+ Burgundy purchases"
      - "'You've purchased from us [N] times' — feels like we're keeping score, not serving them"
      - "Any reference to how long ago they last visited or bought"
    
    write_instead:
      - "'A new vintage from a producer you've explored before' (instead of 'we see you bought their last vintage')"
      - "'The kind of Barolo you'd build a cellar around' (instead of 'based on your cellar profile')"
      - "'Still available' (instead of 'you were looking at this')"
      - "'Something for the cellar' (instead of 'we noticed your recent purchases suggest you're building a collection')"
  
  inference_limits:
    - "One purchase in a category does not establish a persona — require 3+ confirming signals"
    - "A gift purchase does not reveal the buyer's taste — never use gift purchase history for personal recommendations"
    - "Price tier inference from a single order requires 2+ confirming signals before applying to recommendations"
    - "Silence (no purchase in 60 days) is not data about preferences — do not infer from absence"
  
  sensitive_prohibitions:
    - "Never infer health, age, or lifestyle from wine choices"
    - "Never use Collector status to infer income"
    - "Never reference drinking frequency — ever"
```

---

## 6. Consent & Data Governance

```yaml
consent_governance:
  consent_model: "Opt-in for behavioral tracking; opt-out for order-related communications"
  
  wine_specific_data_rules:
    age_verification: "21+ confirmed at signup — do not use for any other personalization inference"
    gift_purchase_firewall: "Gift purchase history is stored but never merged into the buyer's personal preference profile"
    drinking_window_data: "Stored per SKU for the customer's account — used only to serve them relevant vintage intelligence"
  
  right_to_erasure:
    agent_rule: "When erasure is requested, suppress from all personalization signals immediately — before next model refresh"
    timeline: "Signal suppression within 4 hours; full propagation within 48 hours"
```

---

## 7. Versioning

```yaml
personalization_md_wine:
  version: "1.0.0"
  last_updated: "2026-03-21"
  updated_by: "Wine marketing system operator"
  review_cadence: "Quarterly — review algorithm weights; update persona rules; audit anti-creepiness compliance"
  
  changelog:
    - version: "1.0.0"
      date: "2026-03-21"
      changes: "Initial release"
  
  mcp_alignment: "Aligned with wine-marketing-complete-spec v5.0.0; get_recommendations() is the runtime engine; get_frequently_bought_together() feeds PDP and cart blocks"
```
