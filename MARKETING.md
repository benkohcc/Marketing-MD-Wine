# MARKETING.MD — Wine E-Commerce
*Machine-readable marketing configuration for an AI-native agentic marketing department*

---

## What This File Is

`MARKETING.MD` and its companion files are the authoritative configuration document for the wine e-commerce AI marketing system — replacing per-skill brand reminders, scattered prompt context, and ad hoc tone guidance with one version-controlled system of record.

**MARKETING.MD** is loaded by every AI agent at session start, before any MCP call, campaign brief, copy generation, or channel action. It contains the information every agent needs regardless of role: brand identity, voice and tone, customer personas, campaign type vocabulary, compliance rules, approval gates, data model definitions, prohibited actions, and autonomy guardrails.

**Companion files** (listed in Section 13 — Companion File Registry) add specific detail for agents that need it. A paid media agent loads `BUDGET.MD` for bid ceilings and spend authority. A content agent loads `CAMPAIGNS.MD` for campaign blueprints. A crisis agent loads `SAFETY.MD` for escalation protocols. Agents load only the companion files relevant to their role — keeping context focused and session initialization fast.

This system is consumed by AI, not humans.

---

## 1. Business Identity

```yaml
brand:
  name: "[Store Name]"
  tagline: "[Store Tagline]"
  category: "Direct-to-consumer wine retail"
  market_position: "Curated — quality-forward, not luxury-gated"
  geographic_scope: "National (US) — shipping eligibility varies by state"
  business_model: "E-commerce with subscription and allocation tiers"
  catalog_size: "~120 active SKUs across 8 major varietals and 14 regions"
  customer_base: "400M+ addressable; ~1,000 active in seed dataset"
```

**Brand Promise**
> We find wines worth drinking and tell the truth about them — so every customer, from the curious newcomer to the serious collector, always leaves with something they'll be glad they bought.

**Brand Story**
> [Fill in — founding story, origin philosophy, what makes this store different from a supermarket shelf or a generic online retailer. Should answer: why do we exist, who do we exist for, what do we believe about wine that others don't?]

**Competitive Differentiation**
- Curation depth: every SKU in the catalog is here because someone chose it, not because it hit a volume threshold
- Persona-native marketing: the way we talk to a Collector is fundamentally different from the way we talk to a Gifter — we don't send the same email to everyone
- Inventory integrity: we never run ads for wines that aren't in stock, and we never promote a wine we can't stand behind
- Educational generosity: we give knowledge away freely — region guides, drinking windows, pairing notes — because an informed customer is a loyal one

---

## 2. Voice & Tone

### Core Voice Attributes

| Attribute | What It Means in Practice |
|-----------|--------------------------|
| Knowledgeable | We know wine deeply and write from that knowledge — never hedging with "some people say" or "experts believe." We are the expert. |
| Approachable | Knowledge without pretension. We never make a customer feel ignorant for not knowing something. |
| Honest | We describe wines accurately — if a bottle is a great value, we say so. If it's an investment for a cellar, we say that too. We don't oversell. |
| Direct | We respect the reader's time. We say what we mean. Subject lines that bury the point are a failure, not a style. |

### Tone Modulation by Channel

Voice is constant. Tone adjusts to context.

| Channel | Tone Guidance |
|---------|--------------|
| Email — transactional | Clear, clean, no flair. Get the information to the customer fast. |
| Email — editorial / new arrival | Warm and story-led. Lead with the wine's origin before the price. |
| Email — promotional | Offer-forward, then justified with story. Never apologetic about the discount. |
| Email — winback | Personal and warm. Acknowledge the gap. Don't pitch hard. |
| Social — Instagram | Lifestyle-first. Short, human, visual. Earn the scroll. |
| Social — Facebook | Community-oriented. Slightly longer is acceptable. Recipe tie-ins work well. |
| Social — Pinterest | Product-focused and evergreen. Pairing imagery, region maps, label close-ups. |
| Paid — search | Functional. Benefit-forward. Keyword-aligned. One clear CTA. |
| Paid — social | Thumb-stopping hook in the first line. Lead with emotion or specificity, not product name. |
| On-site / PDP | Informative and trust-building. Tasting note, then context, then the pairing. Never padding. |
| Blog / Content | Expert and generous. Write to inform, not to sell. A strong CTA at the end is fine; a sales pitch throughout is not. |

### Language Rules

**Always use:**
- Varietal names precisely (Cabernet Sauvignon, not "cab"; Pinot Grigio when it's Italian, Pinot Gris when it's Alsatian)
- Producer names correctly and completely on first reference
- Specific vintage year whenever relevant (not "a recent vintage")
- Food pairing language that is specific ("duck confit with cherry reduction," not "pairs with meat")

**Never use:**
- "Complex" without saying what makes it complex
- "Smooth" as a primary descriptor — it's meaningless without context
- "Perfect for any occasion" — this is the opposite of curation
- "Luxury" for wines under $80 — it trains the customer to distrust the word
- "Amazing," "incredible," "unbelievable" — we sell wine, not supplements
- Discounts framed as generosity ("we're passing the savings on to you")
- Urgency manufactured from nothing ("Act now!" on a campaign with no actual deadline)

**Punctuation & Style:**
- Oxford comma: Yes, always
- Em dashes: Use freely in body copy; avoid in subject lines
- Sentence case for headlines: Yes (exception: proper nouns and varietal names)
- Numbers: Numerals always for prices, quantities, and vintages; spell out under ten in editorial prose
- Emoji: Never in email subject lines; sparingly in social captions (1–2 max, only where they add meaning)
- Wine scores: Include when >90 and from a credible publication; never lead with a score for educational campaigns

---

## 3. Customer Personas

> Personas are the primary targeting unit for all campaign planning, copy generation, and channel selection. Every campaign brief must name a target persona. AI agents call `get_personas()` at session start and resolve segment IDs to persona archetypes before writing any copy.

---

### Persona: The Explorer

**Who they are:** Adults 28–42, urban or suburban, mid-to-high income ($75k–$150k). Buys wine for personal discovery, dinner parties, and the quiet pleasure of knowing more than they did last week. Considers themselves wine-curious, not wine-literate — and is actively trying to close that gap.

**Purchase behavior:** 1–3 bottles per order, 6–10 orders per year. AOV $35–75. Drawn to new regions, unfamiliar varietals, and producer stories. Will try something they've never heard of if the story is credible.

**What they respond to:** Region storytelling. Winemaker profiles. Food pairing specificity. "What to try next" framing. Subject lines that promise knowledge ("The definitive guide to Burgundy's hidden appellations") outperform offer-led lines for this persona.

**What they ignore:** Hard sells. Luxury positioning. Wine scores without explanation. Anything that implies expertise they don't have.

**Acquisition channels:** Instagram, Pinterest, organic search (recipe + pairing queries), email sign-up after consuming content.

**Campaign type fit:** New arrival (discovery angle), educational (direct fit), seasonal (when occasion-framed with a learning element), bundle (pairing concept).

**Segment signals in data:** High `pdp_view` count relative to purchase count; frequent `blog_view` events; search queries using varietal and region terms; `filter_applied` events scoped to region or grape; low discount code usage history.

---

### Persona: The Gifter

**Who they are:** Broad age range (30–65). Buys wine as a gift, not for personal consumption. Does not identify as a wine enthusiast. Always operating under some time pressure (an occasion is coming). Values looking thoughtful without having to become an expert.

**Purchase behavior:** 3–6 orders per year, heavily clustered around occasions (Valentine's Day, Mother's Day, Thanksgiving, Christmas, host gifts). AOV $50–120 — willing to spend more because it's a gift. Frequently buys single bottles or gift sets.

**What they respond to:** Occasion framing above everything else. Gift-readiness signals (gift wrapping, presentation, ribbon). Reassurance that this is a safe and impressive choice ("What sommeliers actually give as gifts"). Price-to-impressiveness framing. Clear, simple copy — they do not want a wine education.

**What they ignore:** Tasting notes in isolation. Producer history. Drinking window guidance. Any copy that assumes wine knowledge they don't have.

**Acquisition channels:** Paid search (high intent around occasions: "wine gift for her," "best wine gift under $75"), social (gift guides, occasion roundups), email around key dates.

**Campaign type fit:** Seasonal (primary audience for all occasion campaigns), promotion (when offer includes gift packaging), bundle (gift set framing).

**Segment signals in data:** Purchase history clustering around holidays; low session count between purchases; `search_query` events with gift-related terms; high add-to-cart rate on sessions arriving from paid search.

---

### Persona: The Loyalist

**Who they are:** Adults 35–60, household income $120k+. Has a settled wine preference — a specific varietal, region, or producer style they return to reliably. Has purchased multiple times and treats this store as their trusted source. Not interested in being educated; interested in getting more of what they love, and being the first to know when something exceptional is available.

**Purchase behavior:** 4–8 orders per year, often multiples (3–6 bottles per order). AOV $80–200+. Low price sensitivity within their preferred category. High CLV. Retains well when treated as an insider rather than a prospect.

**What they respond to:** New arrival announcements in their preferred category. Limited allocation early access. Producer updates ("the 2022 vintage is exceptional — here's why"). Direct, knowledgeable copy that respects their expertise. First-to-know framing.

**What they ignore:** Introductory offers. Generic promotional messaging. Anything that implies they need convincing. Discounts on wines in their preferred category — these cheapen the relationship.

**Acquisition channels:** Already a customer. Primarily email. Social only peripherally.

**Campaign type fit:** New arrival (primary audience), limited allocation (gets first access), pre-order (primary audience for futures and reserves).

**Segment signals in data:** High purchase frequency in a specific varietal or region; high CLV; high email open rate; `pdp_view` events concentrated in their preference category; zero or near-zero discount code usage.

---

### Persona: The Deal Seeker

**Who they are:** Price-conscious buyer across all age ranges. Buys wine when there's a reason to — a promotion, a flash sale, a good deal surfaced by a search. Wine quality matters, but value is the deciding factor.

**Purchase behavior:** Primarily during promotions, 2–5 orders per year. AOV $25–55. High cart abandon rate without a discount. Responds quickly to urgency and time-bounded offers. Does not engage with educational or long-form content.

**What they respond to:** Discount percentage prominent in subject line. Urgency ("48 hours only," "ends Sunday"). Free shipping thresholds. Countdown copy. Offer clarity before wine story — do not bury the deal in tasting notes.

**What they ignore:** Editorial content. Producer history. Anything without a visible price advantage.

**Acquisition channels:** Paid search (deal-seeking queries), email (high open rate on promotional sends, near-zero on editorial sends).

**Campaign type fit:** Promotion (primary audience), seasonal (when offer is included), bundle (when price-framed as saving).

**Segment signals in data:** Purchase history correlates strongly with discount code usage; high `search_query` count for price-related terms; low blog engagement; high email open rate on promotional subject lines; low open rate on editorial sends.

> **Note for agents:** Do not suppress Deal Seekers aggressively post-purchase. A repeat Deal Seeker who buys 5× per year during promotions has meaningful LTV. They will buy again at the next good offer — keep them warm.

---

### Persona: The Collector

**Who they are:** Serious wine enthusiast, typically 40–65, high income ($200k+). Buys wine as an investment in future enjoyment — bottles go to a cellar, not tonight's table. Deep knowledge of producers, vintages, and regions. Follows wine press and scores. Treats the relationship with this store as a source for allocation access and futures, not a place to browse.

**Purchase behavior:** 2–4 orders per year, but very high AOV ($200–1,000+ per order; often a case at a time). Pre-orders and futures are the highest-value transaction type. Long customer lifetime — does not churn easily if treated with appropriate expertise and exclusivity.

**What they respond to:** Vintage quality assessments. Producer backgrounds. Drinking window precision. Allocation access framed as exclusive. Subject lines signaling insider access ("Your allocation of the 2022 Barolo is ready"). Scores and press mentions. Early access before the general list.

**What they ignore:** Introductory offers. Generic promotions. Any discount on a wine in their category — this signals the wine isn't worth full price.

**Acquisition channels:** Email (primary), organic search (producer and vintage-specific queries), limited paid (only for high-value, highly specific keywords).

**Campaign type fit:** Pre-order (primary audience), limited allocation (gets earliest access), new arrival (for significant producer releases only).

**Segment signals in data:** High AOV; low purchase frequency; `pdp_view` events concentrated on high-price SKUs; long session dwell time on tasting notes; `search_query` events using producer and vintage-specific terms; high email open rate; zero discount code history.

---

### Persona Quick Reference

| Persona | Avg AOV | Primary Hook | Primary Channels | Never Do |
|---------|---------|-------------|-----------------|---------|
| Explorer | $45 | Discovery story, knowledge | Email, organic, Instagram | Hard sell, luxury framing |
| Gifter | $80 | Occasion + reassurance | Paid search, email, social | Deep wine copy, tasting notes alone |
| Loyalist | $140 | Insider access, new arrivals | Email | Discounts in their category |
| Deal Seeker | $38 | Offer-forward, urgency | Paid search, email | Burying the discount |
| Collector | $450 | Allocation access, vintage intel | Email, organic search | Any discount, generic copy |

---

## 4. Campaign Types

> Every campaign has exactly one type. Full blueprints (triggers, tone angles, KPIs, send cadence, suppression rules, and copy guidance) are in **companion/CAMPAIGNS.MD**, loaded by all campaign-planning agents.

### Campaign Type Glossary

| Type | What it is | Discount | Paid | Primary Persona |
|------|-----------|---------|------|----------------|
| `new_arrival` | Single-send launch when a new SKU arrives | No | No | Explorer, Loyalist |
| `promotion` | Discount campaign; offer leads | Yes | Yes | Deal Seeker, Loyalist |
| `limited_allocation` | Scarcity-driven sell; quantity stated upfront | No | No | Loyalist, Collector |
| `seasonal` | Occasion-anchored campaign (Mother's Day, holiday, etc.) | Optional | Yes | Gifter, Explorer |
| `winback` | Single-send relationship re-open for lapsed customers | Optional (soft) | No | Loyalist, Explorer |
| `educational` | SEO blog or knowledge email; no selling | No | No | Explorer |
| `bundle` | Pairing-concept campaign for frequently bought together SKUs | Optional | No | Explorer, Gifter |
| `pre_order` | Reservation campaign for upcoming arrivals | No | No | Loyalist, Collector |

---


## 5. KPI Framework

### Sitewide Baselines

| Metric | Baseline | Warning | Critical |
|--------|---------|---------|---------|
| Email open rate | 28% | < 20% | < 12% |
| Email CTR | 3.5% | < 2.0% | < 1.0% |
| Paid ROAS | 4.0× | < 2.5× | < 2.0× |
| Site conversion rate | 2.8% | < 1.8% | < 1.2% |
| AOV | $72 | < $55 | < $40 |
| Cart abandon rate | 68% | > 75% | > 82% |
| Email deliverability | 97% | < 94% | < 90% |

### Campaign-Type KPI Hierarchy

| Campaign Type | Primary KPI | Target | Secondary KPIs |
|--------------|-------------|--------|----------------|
| new_arrival | view_to_cart_rate | > 8% | email_open_rate, social_engagement_rate |
| promotion | revenue | Brief-specific | units_sold, email_conversion_rate, paid_roas |
| limited_allocation | time_to_sellout | < 14 days | sell_through_speed, tier_1_conversion |
| seasonal | revenue | Brief-specific | new_customer_acquisition_rate |
| winback | reactivation_rate | > 15% | second_purchase_rate_90d |
| educational | content_dwell_time | > 180s | scroll_depth, pdp_click_rate |
| bundle | avg_order_value | > 1.3× baseline | basket_size, units_per_order |
| pre_order | reservation_count | Brief-specific | deposit_completion_rate |

### Anomaly Detection Rules

```yaml
anomaly_detection:
  lookback_window_days: 30
  sensitivity: medium
  alert_on: [slack, dashboard]
  
  critical_thresholds:
    paid_roas_below: 2.0
    email_deliverability_below: 90
    site_conversion_below: 1.2
    cart_abandon_above: 82
  
  auto_pause_on_critical:
    paid_roas_below_2: true       # pause paid campaigns immediately
    email_deliverability_below_90: true  # pause all campaign sends, alert human
    oos_sku_in_active_campaign: true     # pause all channels for that SKU
```

---

## 6. Suppression & Compliance Rules

> Suppression is policy. Agents check `is_suppressed()` before every individual send and verify segment-level suppression rules before every campaign send.

### Global Rules — Non-Overridable

```yaml
global_suppression:
  unsubscribes: immediate_permanent
  hard_bounces: immediate_permanent
  spam_complaints: immediate_permanent
  invalid_addresses: immediate_permanent
  customers_in_shipping_ineligible_states: campaign_suppression  # wine shipping compliance
```

### Wine-Specific Compliance

```yaml
wine_compliance:
  shipping_eligibility: required_check_before_every_send
  shipping_ineligible_states: "[Check current DTC wine shipping law — changes frequently]"
  age_verification: "All marketing assumes recipient is 21+. Never market in contexts targeting under-21."
  alcohol_advertising_rules:
    - "No claims of health benefits"
    - "No targeting based on intoxication signals"
    - "No messaging that promotes irresponsible consumption"
    - "All paid ads must comply with platform alcohol advertising policies (Meta, Google, Pinterest each have distinct rules)"
  
  disclaimer_requirement: "Email footer must include responsible drinking reminder and unsubscribe link."
```

### Email Fatigue Guard

```yaml
fatigue_guard:
  max_emails_per_week: 3
  min_days_between_campaign_sends_same_customer: 2
  cooldown_after_purchase_days: 7      # for campaign sends; transactional still fires
  exceptions:
    - transactional                    # order confirmation, shipping, etc.
    - cart_abandon                     # behavioral trigger, not campaign
    - post_purchase_sequence           # first 48h post-purchase only
```

### Post-Purchase Suppression

```yaml
post_purchase:
  suppress_campaign_sends_for_days: 30
  scope: campaign_scoped             # suppressed from the specific campaign, not all email
  applies_to: [promotion, limited_allocation, bundle]
  exceptions: [seasonal, educational, new_arrival]
  implementation: "Call add_to_suppression_list(customer_id, reason: 'purchased', campaign_id, expires_at: 30_days)"
```

### Winback Cooldown

```yaml
winback_cooldown:
  days_between_winback_sends: 60
  max_winback_attempts_before_suppress: 3
  implementation: "Check is_suppressed() before triggering. Add 60-day suppression after send."
```

---

## 7. Human Approval Gates

> These gates cannot be automated. Agents stop, surface the decision, and wait. Approval must come through the operator interface in the current session.

| Gate | Trigger | Presented | Requires Confirmation |
|------|---------|-----------|----------------------|
| 1 — Campaign Brief | `/plan-campaign` creates brief | Campaign type, audience, channels, SKUs, budget, KPIs, dates | `update_campaign_status("active", approved_by)` |
| 2 — Content Assets | `/generate-content` completes | Full copy package by channel | `approve_content_asset()` per channel + `create_approval_record()` |
| 3 — Creative Assets | Creative uploaded | Image URLs, platform fit, alt text | `approve_creative_asset()` |
| 4 — A/B Test Winner | Test reaches significance | Variant ID, lift %, p-value, sessions per variant | `update_merchandising_rules()` to promote winner |
| 5 — Campaign Cancel | Cancellation instructed | Channels active, sends to cancel, ads to pause, posts to unschedule | `update_campaign_status("cancelled", reason)` |

**Additional wine-specific gate triggers:**
- Any send to a segment > 1,000 contacts (verify targeting before firing)
- Any paid campaign with daily budget > $500
- Any campaign brief featuring a SKU with `days_of_supply < 7` (verify stock before commitment)

---

## 8. Wine-Specific Data Model Extensions

> The base customer and product data models are extended with wine-specific fields. Agents consuming `get_customer_profile()` or `get_product_catalog()` should treat these as first-class signals.

### Customer Extensions

| Field | Type | Description | Use in Marketing |
|-------|------|-------------|-----------------|
| persona | enum | Explorer / Gifter / Loyalist / DealSeeker / Collector | Primary targeting signal; drives copy angle and channel selection |
| varietal_affinities | map(varietal → score) | Affinity scores 0–1 per varietal from purchase + browse history | Used by `/generate-content` for personalized copy; by `/update-personalization` for recommendations |
| preferred_varietal | string | Single highest-affinity varietal | Shorthand for Loyalist and Collector targeting |
| preferred_region | string | Single highest-affinity wine region | Used for new arrival and limited allocation targeting |
| clv_12m | number | 12-month forward CLV projection | Tier segmentation for limited allocation access |
| churn_risk_score | float 0–1 | Model-derived churn probability | Winback trigger threshold: > 0.70 |
| upsell_propensity | float 0–1 | Probability of trading up in AOV | Used by `/analyze-segments` for upsell campaign identification |
| occasion_purchase_history | list(string) | Occasions for which customer has purchased gifts | Seasonal campaign targeting signal |

### Product Extensions

| Field | Type | Description | Use in Marketing |
|-------|------|-------------|-----------------|
| varietal | string | Wine grape variety | Persona targeting, SEO, copy tone |
| varietal_family | string | Broader category (e.g., "Burgundy" for Pinot Noir) | Collection-level targeting |
| region | string | Wine region (e.g., "Burgundy," "Napa Valley") | Persona targeting, SEO |
| sub_region | string | More specific appellation | Collector and Loyalist copy |
| vintage | integer | Harvest year | Required in all copy; critical for Collector persona |
| winemaker | string | Producer / winemaker name | Lead in new arrival and limited allocation copy |
| tasting_notes | string | Structured tasting notes | Source for `/generate-content` copy generation |
| drinking_window | string | Optimal drinking window (e.g., "2024–2030") | Required in Collector and Loyalist copy |
| days_of_supply | integer | Units on hand ÷ sell-through velocity | Inventory alert trigger for `/check-inventory` |
| velocity_units_per_day | float | 30-day average sell-through rate | Stock depletion forecasting |
| pdp_views_7d | integer | PDP views in last 7 days | High-intent signal for limited allocation detection |
| press_score | number | Wine press score (e.g., 94 WS) | Include in Collector and Loyalist copy when > 90 |
| press_publication | string | Source of press score | Required when score is cited |

---

## 9. Inter-Agent Communication

```yaml
inter_agent:
  queue_mechanism: MCP
  direct_agent_calls: false
  
  campaign_request_types:
    - campaign_request          # from check-inventory (overstock), seo-audit, or human
    - content_request           # from plan-campaign or seo-audit to generate-content
    - seo_content_request       # from seo-audit — includes target_keywords
    - inventory_alert           # from check-inventory — triggers channel pauses
    - segment_alert             # from analyze-segments — emerging pattern
  
  queue_priority_order: [urgent, high, medium, low]
  
  retrospective_loop: true      # plan-campaign MUST call get_campaign_retrospective() before new briefs
  
  channel_pause_scope: "Only pause channels present in the campaign's channels array — never pause channels a campaign isn't using"
```

---

## 10. Prohibited Actions

> These rules apply regardless of campaign context, operator urgency, or brief-level instruction.

- **Never send to a globally suppressed address** — no exception
- **Never send to a customer in a wine-shipping-ineligible state** — compliance, not preference
- **Never execute `update_campaign_status("active")` without human `approved_by`**
- **Never run paid campaigns for `winback`, `educational`, `limited_allocation`, or `pre_order` types**
- **Never include a discount code in `new_arrival`, `limited_allocation`, `educational`, or `pre_order` copy**
- **Never send more than 3 campaign emails to any customer in a 7-day window**
- **Never advertise an out-of-stock SKU** — check inventory before every paid campaign launch
- **Never claim health benefits for wine in any marketing copy**
- **Never target audiences based on intoxication signals**
- **Never apply urgency language (countdown, "ends tonight") to winback or educational campaigns**
- **Never suppress a Deal Seeker from promotional campaigns based on purchase history alone** — they will buy again
- **Never name a competitor in any customer-facing copy** — email, social, paid, or on-site

---

## 11. Campaign Taxonomy & Naming Conventions

### Campaign ID Format

```yaml
naming_conventions:
  campaign_id:
    format: "[YYYY-MM]-[type_code]-[persona_code]-[sku_short]"
    examples:
      - "2025-03-promo-ds-borg25     (March 2025 promotion, Deal Seeker, Bordeaux 2025)"
      - "2025-02-seas-gi-rose-val    (February 2025 seasonal, Gifter, Rosé for Valentine's)"
      - "2025-11-na-lo-bar22         (November 2025 new arrival, Loyalist, Barolo 2022)"
  
  content_asset_id:
    format: "[campaign_id]-[channel_code]-[asset_type]-[variant]"
    example: "2025-03-promo-ds-borg25-em-subject-A"
    
    channel_codes: {email: em, paid_search: ps, paid_social: ps2, instagram: ig, facebook: fb, pinterest: pt, seo: seo}
    asset_types: {subject_line: subject, email_body: body, ad_headline: hdl, social_caption: cap, blog_post: blog, product_description: pdp}
  
```

> UTM standards and attribution linkage rules are in **companion/MEASUREMENT.MD**.

### Content Tagging Taxonomy

```yaml
content_tags:
  required_tags:
    - content_pillar: "[Region & Varietal Education | Vintage Intelligence | Occasion & Gift Guidance | Store Point of View]"
    - funnel_stage: "[awareness | consideration | conversion | retention]"
    - persona: "[Explorer | Gifter | Loyalist | Deal Seeker | Collector | all]"
    - campaign_type: "[new_arrival | promotion | limited_allocation | seasonal | winback | educational | bundle | pre_order]"
    - channel: "[email | paid | social | seo | on-site]"
    - publish_date: "[YYYY-MM-DD]"
    - expiry_date: "[YYYY-MM-DD or evergreen]"
  
  optional_tags:
    - varietal: "[varietal name]"
    - region: "[wine region]"
    - vintage: "[YYYY]"
    - seasonal_event: "[calendar event name]"
    - ab_test_id: "[test ID if variant]"
    - press_score: "[N pts — Publication]"
```

---

## 12. AI Agent Autonomy & Safety Guardrails

### Autonomy Levels

```yaml
autonomy_levels:
  full_autonomy:
    - "Read-only MCP operations (data retrieval, reporting, analysis)"
    - "Behavioral signal detection and internal tagging"
    - "Content drafting (before any human approval gate)"
    - "A/B test creation (not promotion of winner)"
    - "Suppression list checks"
    - "Inventory status checks"
  
  notify_and_proceed:
    - "Sending a triggered email within approved parameters (cart abandon, restock nudge)"
    - "Pausing an underperforming ad set when ROAS < stop-loss"
    - "Applying a campaign recommendation boost (set_campaign_boost)"
    - "Publishing approved social content per approved schedule"
    - "Pausing a paid campaign for an OOS SKU (inventory sync)"
  
  notify_and_wait:
    - "Activating a campaign brief (Gate 1)"
    - "Approving content assets (Gate 2)"
    - "Launching a new paid campaign"
    - "Any spend action above $500 in a single day"
    - "Promoting an A/B test winner (Gate 4)"
    - "Campaign cancellation (Gate 5)"
    - "Any wine from a shipping-ineligible state flagged in a target segment"
  
  human_only:
    - "Overriding any suppression list entry"
    - "Sending to an unsubscribed address"
    - "Modifying wine prices in the product catalog"
    - "Issuing or responding to a product recall"
    - "Resuming operations after kill switch activation"
    - "Publishing any content making a wine quality claim not in approved claims library"
```

### Fail-Safe Defaults

```yaml
fail_safe_defaults:
  default_action: "Most conservative available option"
  
  specific_defaults:
    - "Unknown persona → use all-persona copy; do not infer from single session"
    - "Suppression status unknown → treat as suppressed; do not send"
    - "Inventory status unknown → do not launch or continue paid campaign"
    - "Shipping eligibility unknown → exclude customer from campaign send"
    - "Crisis level unclear → treat as Level 2; pause promotional content"
    - "Press score not in approved library → omit the score; describe the wine without it"
    - "Vintage unknown → do not generate tasting notes; flag for catalog update"
    - "Discount exceeds authority → apply maximum permitted discount, not requested amount"
    - "Budget status unknown → pause all spend; alert human"
```

### Anti-Hallucination System

> This block covers cross-cutting hallucination risk. Domain-specific rules also exist in: **companion/MESSAGING.MD** (approved claims library, copy-level rules), **companion/CONTENT.MD** (editorial standards, AI disclosure), **companion/SAFETY.MD** (brand safety, wine fault descriptions).

```yaml
anti_hallucination:
  facts_required_to_be_sourced:
    - "Wine press scores (critic, publication, date, vintage — all four required)"
    - "Awards and certifications"
    - "Vintage year (must come from product catalog, never generated)"
    - "Producer or winemaker quotes"
    - "Comparative claims vs. other wines or retailers"
    - "Drinking window guidance (pull from catalog; do not generate)"
    - "Production quantities (never generate — pull from brief or catalog)"
  
  prohibited_generation:
    - "Invented press scores or critic endorsements"
    - "Fabricated production quantities ('only 200 cases made')"
    - "Made-up winemaker quotes or biographies"
    - "Invented awards or accolades"
    - "Tasting notes claiming sensory attributes not in the product catalog (e.g., 'tastes of black truffle' if not in catalog tasting notes)"
    - "Before/after cellaring claims without documented source"
  
  wine_hallucination_risk_note: "Wine copy is high-risk for hallucination. Specific producers, vintages, scores, and production details are the exact type of verifiable facts where LLMs confidently generate plausible-sounding but false content. Every factual claim must be traced to: the product catalog, the approved claims library, or a human-reviewed source."
```

### Circuit Breakers

```yaml
circuit_breakers:
  - condition: "Email unsubscribe rate exceeds 0.5% in any 24-hour period"
    action: "Pause all promotional email sends; alert human"
  
  - condition: "Paid ROAS drops below 2.0× for 3 consecutive days"
    action: "Pause all paid campaigns; alert human; do not resume without approval"
  
  - condition: "Any customer receives > 3 emails in a 7-day period"
    action: "Suppress that customer from all sends for 7 days; log breach"
  
  - condition: "Kill switch activated or product recall issued"
    action: "Full system pause — see companion/SAFETY.MD"
  
  - condition: "Budget spend reaches 80% of monthly budget before month midpoint"
    action: "Pause all non-essential paid spend; alert human for reallocation"
  
  - condition: "Agent attempts to send to a shipping-ineligible state customer"
    action: "Block the send; log; alert human if pattern indicates a segment data issue"
  
  - condition: "Agent attempts to send to a globally suppressed address"
    action: "Block; log; alert if this happens more than once (may indicate a data pipeline issue)"
  
  - condition: "Inventory status shows OOS for a SKU in an active paid campaign"
    action: "Pause paid immediately via pause_ads_for_sku(); alert human"
```

### Data Freshness Requirements

```yaml
data_freshness:
  real_time_required:
    - "Suppression list checks (must be current at send time)"
    - "Inventory status before any paid campaign launch or continuation"
    - "State shipping eligibility before any campaign send"
  
  hourly_acceptable:
    - "Campaign ROAS and CPA (for bid adjustment decisions)"
    - "Behavioral trigger evaluation (cart abandon, high-intent browse)"
  
  daily_acceptable:
    - "Budget pacing"
    - "Email send scheduling"
    - "Recommendation score updates"
    - "Inventory for email campaign suppression"
  
  weekly_acceptable:
    - "RFM score updates"
    - "CLV recalculation"
    - "Churn risk scores"
    - "Segment membership refresh"
    - "Strategic budget reallocation"
  
  stale_data_rule: "If data is older than the maximum acceptable age, do not proceed — fetch fresh data or pause and flag. Wine inventory data is especially time-sensitive: a SKU that was in stock when the campaign launched may sell out mid-flight."
```

---

## 13. Companion File Registry

```yaml
companion_files:
  
  - file: "PRICING.MD"
    purpose: "Discount authority detail, promotional calendar, dynamic pricing by SKU tier, bundle pricing configuration"
    loaded_by: [campaign_agents, plan_campaign_skill, generate_content_skill]
    required_for: "Any agent creating or modifying a promotional offer or discount code"
    version: "1.0.0"
    last_updated: "2026-03-21"
  
  - file: "CONTENT.MD"
    purpose: "Full editorial calendar, SEO keyword clusters, content governance workflows, vintage assessment templates"
    loaded_by: [content_agents, seo_agents, generate_content_skill, seo_audit_skill]
    required_for: "Any agent generating blog posts, region guides, or vintage assessments"
    version: "1.0.0"
    last_updated: "2026-03-21"
  
  - file: "MEASUREMENT.MD"
    purpose: "Full attribution model config, MMM setup, incrementality test protocols, cross-device rules"
    loaded_by: [analytics_agents, performance_report_skill]
    required_for: "Any agent producing attribution reports or budget recommendations"
    version: "1.0.0"
    last_updated: "2026-03-21"
  
  - file: "EXPERIMENTATION.MD"
    purpose: "A/B testing governance, test prioritization framework, rollout rules, collision management"
    loaded_by: [experimentation_agents, review_behavior_skill, update_personalization_skill]
    required_for: "Any agent creating or evaluating A/B tests"
    version: "1.0.0"
    last_updated: "2026-03-21"
  
  - file: "COMPETITORS.MD"
    purpose: "Per-competitor profiles, repositioning statements, objection responses, competitive response triggers, and competitive mention implementation detail"
    loaded_by: [content_agents, ad_copy_agents, campaign_agents]
    required_for: "Any agent producing comparative content or responding to competitor price/product changes"
    version: "1.1.0"
    last_updated: "2026-03-22"
  
  - file: "PARTNERS.MD"
    purpose: "Per-partner branding rules, co-marketing configuration, affiliate disclosure templates, MDF budgets"
    loaded_by: [campaign_agents, content_agents]
    required_for: "Any agent producing co-branded content or managing affiliate campaigns"
    version: "1.0.0"
    last_updated: "2026-03-21"
  
  - file: "PERSONALIZATION.MD"
    purpose: "Recommendation engine full config, dynamic content rules, consent architecture, segment definitions"
    loaded_by: [personalization_agents, update_personalization_skill, send_emails_skill]
    required_for: "Any agent personalizing content beyond basic persona targeting"
    version: "1.0.0"
    last_updated: "2026-03-21"
  
  - file: "SAFETY.MD"
    purpose: "Full crisis playbooks, holding statement templates, keyword blocklists, escalation matrices with contacts"
    loaded_by: [all_agents]
    required_for: "All agents — this file loads alongside core MARKETING.MD at every session start"
    version: "1.0.0"
    last_updated: "2026-03-21"
  
  - file: "VISUAL.MD"
    purpose: "Color palette, typography, photography style, label imagery guidelines for AI-generated assets"
    loaded_by: [design_agents, content_agents_with_image_generation]
    required_for: "Any agent generating visual assets for campaigns"
    version: "1.0.0"
    last_updated: "2026-03-21"
  
  - file: "LIFECYCLE.MD"
    purpose: "Customer value tiers, loyalty program configuration, lifecycle stage definitions and transitions, post-purchase sequences, lifecycle × persona matrix, cross-sell/upsell rules"
    loaded_by: [lifecycle_agents, analyze_segments_skill, send_emails_skill, plan_campaign_skill, winback_agents]
    required_for: "Any agent managing customer lifecycle transitions, producing CLV-based targeting, or planning winback campaigns"
    version: "1.1.0"
    last_updated: "2026-03-22"

  - file: "CAMPAIGNS.MD"
    purpose: "Full campaign type blueprints — triggers, tone angles, KPI hierarchy, send cadence, discount rules, paid media rules, suppression notes, and copy guidance for all 8 campaign types"
    loaded_by: [plan_campaign_skill, all_campaign_planning_agents, campaign_execution_agents]
    required_for: "Any agent planning or executing a campaign — required to read before creating a campaign brief"
    version: "1.0.0"
    last_updated: "2026-03-22"

  - file: "CHANNELS.MD"
    purpose: "Per-channel execution configuration — email ESP settings, list health rules, A/B testing defaults, paid media platform rules, social post frequency and content mix, SEO content cadence, on-site ad configuration"
    loaded_by: [email_agents, paid_media_agents, social_agents, seo_agents]
    required_for: "Any agent executing channel-specific actions — email sends, paid campaigns, social publishing, SEO content"
    version: "1.0.0"
    last_updated: "2026-03-22"

  - file: "CALENDAR.MD"
    purpose: "Seasonal and vertical wine calendar — 12 annual events with date ranges, brief deadlines, campaign_required flags, featured categories, and messaging angles"
    loaded_by: [plan_campaign_skill, campaign_planning_agents, content_agents, seo_agents]
    required_for: "Any agent checking for upcoming events, generating campaign briefs, or planning content cadence"
    version: "1.0.0"
    last_updated: "2026-03-22"

  - file: "SIGNALS.MD"
    purpose: "Behavioral signal configuration — purchase intent triggers, post-purchase triggers, lifecycle risk triggers, engagement signals, and conflict resolution rules"
    loaded_by: [triggered_messaging_agents, crm_automation_agents, plan_campaign_skill]
    required_for: "Any agent detecting or responding to behavioral signals, or checking whether a signal should suppress or modify a campaign send"
    version: "1.0.0"
    last_updated: "2026-03-22"

  - file: "BUDGET.MD"
    purpose: "Channel budget allocation, agent spending authority limits, stop-loss thresholds, and bid ceilings"
    loaded_by: [campaign_planning_agents, paid_media_agents, plan_campaign_skill]
    required_for: "Any agent planning paid campaigns, adjusting bids, or making spend decisions"
    version: "1.0.0"
    last_updated: "2026-03-22"

session_start_protocol:
  required_reads: [MARKETING.MD, SAFETY.MD]
  conditional_reads: "Load companion files based on agent skill role — see loaded_by field above. See Section 13 — Companion File Registry."
  validation: "Agent must log which files it has read before taking any action"
  mcp_server_version: "5.0.0"
  cowork_plugin_version: "1.0.0"
```

---

## 14. Versioning

```yaml
marketing_md:
  version: "2.1.0"
  vertical: "wine-ecommerce"
  last_updated: "2026-03-22"
  updated_by: "[Store Marketing Lead]"
  changelog:
    - version: "2.1.0"
      date: "2026-03-22"
      changes: "Final cleanup pass — removed sections not universally needed by all agents (Seasonal Calendar, Channel Strategy, Lifecycle Journey, Behavioral Signals, Brand Positioning, Budget Governance, Personalization, Competitive Intelligence, Acquisition/Retention Balance). Moved content to respective companion files. Added BUDGET.MD companion. Renumbered sections. Replaced MARKETING-wine-ecommerce.md references with MARKETING.MD throughout."
    - version: "2.0.0"
      date: "2026-03-21"
      changes: "Added: Brand Positioning & Messaging Framework, Budget Governance, Pricing Rules, Content Governance, Personalization Strategy, Competitive Intelligence Rules, Crisis & Brand Safety Protocols, Attribution Model Specification, Experimentation Framework, Acquisition vs. Retention Balance, Campaign Taxonomy & Naming Conventions, AI Agent Autonomy & Safety Guardrails, Companion File Registry"
    - version: "1.1.0"
      date: "2026-03-21"
      changes: "Added Customer Lifecycle Journey and Behavioral Signals sections"
    - version: "1.0.0"
      date: "2026-03-21"
      changes: "Initial release — aligned with wine-marketing-complete-spec v5.0.0"

  review_cadence: "Quarterly, or on major brand positioning change"
  owner: "Director of Marketing / AI Marketing System Operator"
```

*This file is read by AI marketing agents at session start, before any MCP call, campaign creation, copy generation, or channel execution. Changes take effect on the next agent session. Campaign-level overrides belong in the `notes` field of the campaign brief and are scoped to that campaign only. They do not modify this document.*

