# MARKETING.MD — Wine E-Commerce
*Machine-readable marketing configuration for an AI-native agentic marketing department*

---

## What This File Is

`MARKETING.MD` is the authoritative configuration document for the wine e-commerce AI marketing system. Every AI agent reads this file at session start before accessing the MCP, creating campaign briefs, generating copy, or executing any channel action. It is the single source of marketing intent — replacing per-skill brand reminders, scattered prompt context, and ad hoc tone guidance with one version-controlled declaration.

This file is consumed by AI, not humans. It is structured to answer the decisions AI agents face before they can act well: who are we selling to, how do we speak, what does success look like by campaign type, and what are we never allowed to do.

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

> Every campaign has exactly one type. Type determines default channels, tone angle, KPI hierarchy, send cadence, and suppression behavior. Agents must not override these defaults without a campaign-brief-level instruction.

---

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

### Campaign Type Quick Reference

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

---

## 5. Wine Seasonal & Vertical Calendar

> Wine has a seasonal calendar shaped by culture and harvest cycles that differs significantly from standard retail seasonality. AI agents check for upcoming events at every planning run and generate briefs with appropriate lead times. Events marked `campaign_required: true` must have an approved brief by `brief_deadline`.

```yaml
calendar:
  - event: "New Year's Eve"
    date_range: "Dec 28 – Jan 1"
    brief_deadline: "Nov 25"
    campaign_required: true
    recommended_campaign_type: seasonal
    featured_categories: [Champagne, Sparkling, Prosecco]
    messaging_angle: "The toast matters. Make it count."

  - event: "Valentine's Day"
    date_range: "Feb 7 – Feb 14"
    brief_deadline: "Jan 10"
    campaign_required: true
    recommended_campaign_type: seasonal
    featured_categories: [Rosé, Burgundy, Champagne, Red Bordeaux]
    messaging_angle: "Gift framing dominant — the Gifter persona leads. Occasion > wine story."

  - event: "Houston Rodeo Season"
    date_range: "Late Feb – Late Mar"
    brief_deadline: "Feb 1"
    campaign_required: false
    recommended_campaign_type: seasonal
    featured_categories: [Texas Red Blends, Bold Reds, Malbec, Syrah, Zinfandel]
    messaging_angle: "Local cultural pride + BBQ pairing. Rodeo-specific copy resonates in Houston market."
    notes: "City-level angle — if store serves Houston market, this is a high-signal seasonal window."

  - event: "Spring Clearance"
    date_range: "Mar 15 – Apr 15"
    brief_deadline: "Mar 1"
    campaign_required: false
    recommended_campaign_type: promotion
    featured_categories: [Overstock reds, Winter varietals]
    messaging_angle: "Move winter inventory before warm-weather rotation. Bordeaux, Syrah, Cab."

  - event: "Mother's Day"
    date_range: "May 5 – May 12"
    brief_deadline: "Apr 7"
    campaign_required: true
    recommended_campaign_type: seasonal
    featured_categories: [Rosé, Sparkling, White Burgundy, Light Reds]
    messaging_angle: "Gifter dominant. Elegant presentation signals matter as much as the wine."

  - event: "Summer Rosé Season"
    date_range: "May – Aug"
    brief_deadline: "Apr 15"
    campaign_required: false
    recommended_campaign_type: new_arrival
    featured_categories: [Provence Rosé, Dry Rosé, Sparkling Rosé]
    messaging_angle: "Discovery angle for Explorers. Lighter, outdoor, occasion-flexible."

  - event: "Father's Day"
    date_range: "Jun 8 – Jun 15"
    brief_deadline: "May 10"
    campaign_required: false
    recommended_campaign_type: seasonal
    featured_categories: [Cabernet Sauvignon, Barolo, Whisky-barrel aged reds, Bold Bordeaux]
    messaging_angle: "Bold reds, gift set positioning, Gifter persona leads."

  - event: "Harvest Season / New Vintage Releases"
    date_range: "Sep – Nov"
    brief_deadline: "Aug 15"
    campaign_required: true
    recommended_campaign_type: new_arrival
    featured_categories: [Burgundy, Barolo, Bordeaux, California Cab]
    messaging_angle: "Vintage release excitement. Loyalist and Collector personas lead. Drinking window guidance essential."

  - event: "Beaujolais Nouveau Release"
    date_range: "Third Thursday of November"
    brief_deadline: "Oct 25"
    campaign_required: false
    recommended_campaign_type: new_arrival
    featured_categories: [Beaujolais, Gamay]
    messaging_angle: "Annual ritual. Fun and accessible. Explorer persona. Quick-sell — this wine is not for the cellar."

  - event: "Thanksgiving"
    date_range: "Nov 18 – Nov 28"
    brief_deadline: "Oct 20"
    campaign_required: true
    recommended_campaign_type: seasonal
    featured_categories: [Pinot Noir, Chardonnay, Riesling, Zinfandel, Table reds]
    messaging_angle: "Pairing angle works here — Explorers respond to 'what wine for the table.' Gifter angle also valid for host gifts."

  - event: "Holiday Gifting"
    date_range: "Nov 25 – Dec 20"
    brief_deadline: "Nov 1"
    campaign_required: true
    recommended_campaign_type: seasonal
    featured_categories: [Gift sets, Champagne, Luxury reds, Mixed cases]
    messaging_angle: "Highest-budget campaign of the year. Gifter persona dominant. Gift packaging is a conversion signal."

  - event: "Pre-Harvest Futures / En Primeur"
    date_range: "Mar – Apr (varies by region)"
    brief_deadline: "Feb 15"
    campaign_required: false
    recommended_campaign_type: pre_order
    featured_categories: [Bordeaux en primeur, Barolo futures, Burgundy allocation]
    messaging_angle: "Collector and Loyalist personas only. Allocation access + vintage quality framing. Never discount."
```

---

## 6. Channel Strategy

### Email

```yaml
email:
  esp: "[Provider — Klaviyo / Mailchimp / Braze / etc.]"
  sender_name: "[Store Name]"
  sender_address: "hello@[domain]"
  reply_to: "hello@[domain]"
  
  frequency_caps:
    max_per_week: 3
    min_days_between_campaign_sends: 2
    exceptions: [transactional, cart_abandon, post_purchase_confirmation]
  
  list_health:
    sunset_after_days: 180        # suppress unengaged subscribers after 6 months
    reengagement_threshold_days: 90
    hard_bounce_auto_suppress: true
    spam_complaint_auto_suppress: true
    invalid_address_auto_suppress: true
  
  a_b_testing:
    default_split: "50/50"
    winner_metric: open_rate      # for awareness; override to conversion_rate for promotional
    min_sample_size: 200
    winner_after_hours: 4
  
  behavioral_triggers:
    cart_abandon_delay_minutes: 45
    suppress_if_purchased: true
    winback_delay_minutes: 0      # fire winback on schedule, not triggered
```

### Paid Media

```yaml
paid:
  platforms: [google, meta, pinterest]
  
  google:
    default_bidding: target_roas
    target_roas: 4.0              # adjust per category margin
    shopping_feed_sync: daily
    in_stock_only: true           # never show ads for OOS SKUs
  
  meta:
    default_bidding: target_roas
    prospecting_allowed: true     # for seasonal campaigns only
    retargeting_window_days: 14
    lookalike_source: "Champions segment"
  
  pinterest:
    use_for: [seasonal, bundle, new_arrival]
    avoid_for: [winback, educational, limited_allocation]
  
  global_rules:
    pause_on_out_of_stock: true    # immediate — check-inventory triggers this
    min_roas_before_pause: 2.0
    creative_refresh_days: 21
    never_run_paid_for: [winback, educational, limited_allocation, pre_order]
```

### Social

```yaml
social:
  platforms: [instagram, facebook, pinterest]
  
  post_frequency:
    instagram: "4–5 posts / week"
    facebook: "3–4 posts / week"
    pinterest: "5–7 pins / week (evergreen emphasis)"
  
  content_mix:
    campaign_posts_pct: 50
    organic_editorial_pct: 35
    ugc_or_reposts_pct: 15
  
  hashtag_strategy: "3–5 targeted hashtags on Instagram. Category terms (#burgundywine, #pinotnoir), occasion terms (#winetasting, #winepairing), and one brand tag. Never generic (#wine) alone."
  
  link_in_bio_priority: "Active seasonal or limited allocation campaign takes priority. Rotate to new arrival if no time-sensitive campaign is live."
  
  sold_out_posts: true    # when limited_allocation campaign sells out, publish sold-out post immediately
```

### SEO / Content

```yaml
seo:
  primary_intents: [informational, transactional]
  
  content_cadence:
    blog_posts_per_month: 4
    product_description_refresh_days: 90
    region_guide_cadence: "One new region guide per quarter"
  
  target_kpis:
    content_dwell_time_seconds: 180
    pdp_click_rate_from_content: 0.12
    content_to_purchase_rate_14d: 0.03
  
  high_value_content_types:
    - varietal_explainer          # What is Barolo? What makes it different?
    - region_guide                # The Wine Regions of Burgundy
    - drinking_window_guide       # When to open your 2019 Bordeaux
    - food_pairing_guide          # Wine for Thanksgiving: a complete guide
    - vintage_assessment          # Is the 2021 Napa Cab worth buying?
  
  content_seo_rules:
    - "Always include the varietal name in the H1"
    - "Drinking window guidance must be specific (year, not 'soon')"
    - "Food pairings must be specific dishes, not categories"
    - "Internal link to 1–3 relevant PDPs per blog post"
    - "Never stuff keywords — write for the Explorer persona, not a search engine"
```

---

## 7. Customer Lifecycle Journey

> The lifecycle defines what *state* a customer is in and what the system does to move them forward. Unlike campaign types — which are broadcast logic — the lifecycle layer is per-customer and operates continuously. AI agents use lifecycle stage as a secondary targeting signal in campaign planning and as the primary driver of triggered messaging. Wine buyers do not move through lifecycles linearly — a Collector may be dormant for 8 months and then drop $800 in a single pre-order session. Dormancy is not always churn. The model must account for this.

### Stage Definitions & Transitions

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
    marketing_response: winback_campaign   # single send — see campaign type: winback
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

### Post-Purchase Sequences

> These sequences fire after a transaction regardless of which campaign drove it. They are relationship-building, not promotional. Never frequency-cap away a day-0 order confirmation. The welcome sequence is the highest-leverage touchpoint in the customer lifecycle — a customer who just bought wine is maximally engaged.

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

### Lifecycle × Persona Matrix

> Wine personas do not move through the lifecycle at the same speed or in the same pattern. This matrix tells AI agents what to expect and how to adapt when lifecycle stage and persona intersect.

| Persona | Typical Journey Shape | Normal Dormancy Period | At-Risk Signal | Winback Approach |
|---------|----------------------|----------------------|---------------|-----------------|
| Explorer | Fast to active; can stall if no new discovery stimulus | 30–60 days | No blog or PDP engagement for 60 days | New arrival in a region they've browsed; knowledge hook |
| Gifter | Bursty — occasion-driven; long gaps between purchases are *normal* | 60–120 days between occasions | Missing a historically purchased occasion window | Next occasion reminder; gift framing |
| Loyalist | Linear and consistent once established; a long gap is a genuine signal | 30–45 days | Silence during a new arrival in their preferred varietal | New arrival in their category; insider framing |
| Deal Seeker | Promotion-activated; dormancy between promotions is *expected* | 60–90 days between promotion windows | Not opening promotional emails | Strong offer; urgency; do not use story-led copy |
| Collector | Very long natural cadence; 6–8 months between purchases is normal | Up to 180 days | Missing a pre-order or allocation event they historically engaged | Allocation or vintage-specific outreach; never discount |

---

## 8. Behavioral Signals & Triggered Responses

> Signals are real-time customer actions that warrant a response independent of any scheduled campaign. They operate on a different clock — campaigns are planned and broadcast; signals are detected and triggered. AI agents must evaluate active signals before every scheduled campaign send. A signal can suppress a campaign send, accelerate it, or change its copy angle — depending on priority.

### Signal Priority Order

When multiple signals are active for the same customer simultaneously, resolve in this order:

1. **Compliance & suppression** — always wins; blocks all other responses
2. **Purchase intent** (cart abandon, wishlist, repeated PDP) — respond within hours
3. **Post-purchase** — customer just bought; sequence suppresses campaigns for 7 days
4. **Lifecycle risk** (churn threshold, RFM degradation) — adapt tone, do not suppress
5. **Engagement signals** — inform personalization; do not affect timing

---

### Category 1: Compliance & Suppression Signals

```yaml
compliance_signals:

  unsubscribe:
    detection: "Customer clicks unsubscribe or submits opt-out"
    response: immediate_global_suppress
    blocks: all_campaign_and_triggered_sends
    human_review: false
    wine_note: "State-level shipping suppression is also non-negotiable — check eligibility before every send."

  spam_complaint:
    detection: "ESP reports abuse complaint"
    response: immediate_global_suppress + deliverability_alert
    blocks: all_sends
    human_review: true
    note: "Spike in complaints may indicate a list quality or campaign targeting problem — flag for review."

  hard_bounce:
    detection: "ESP reports permanent delivery failure"
    response: immediate_suppress
    blocks: all_sends
    human_review: false

  state_shipping_ineligible:
    detection: "Customer billing or shipping address is in a wine-shipping-restricted state"
    response: suppress_from_all_wine_purchase_campaigns
    blocks: promotional sends; does not block educational or content sends
    human_review: false
    note: "DTC wine shipping laws change frequently — maintain a current state eligibility list and check before every campaign launch."
```

---

### Category 2: Purchase Intent Signals

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

### Category 3: Post-Purchase Signals

```yaml
post_purchase_signals:

  first_purchase_completed:
    detection: "Purchase event; order_count = 1"
    response: first_purchase_welcome_sequence (see Section 7)
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
    response: high_value_followup_email (see Section 7)
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

### Category 4: Lifecycle Risk Signals

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

### Category 5: Engagement Signals

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

### Signal Conflict Resolution

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

## 9. KPI Framework

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

## 10. Suppression & Compliance Rules

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

## 11. Human Approval Gates

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

## 12. Wine-Specific Data Model Extensions

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

## 13. Inter-Agent Communication

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

## 14. Prohibited Actions

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

---

## 15. Versioning

```yaml
marketing_md:
  version: "2.0.0"
  vertical: "wine-ecommerce"
  last_updated: "2026-03-21"
  updated_by: "[Store Marketing Lead]"
  changelog:
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
  
  mcp_server_version: "5.0.0"
  cowork_plugin_version: "1.0.0"
  
  session_start_protocol:
    required_reads: [MARKETING-wine-ecommerce.md, SAFETY.MD]
    conditional_reads: "See Section 28 — Companion File Registry"
    validation: "Agent must log which files it has read before taking any action"
```

---

*This file is read by AI marketing agents at session start, before any MCP call, campaign creation, copy generation, or channel execution. Changes take effect on the next agent session. Campaign-level overrides belong in the `notes` field of the campaign brief and are scoped to that campaign only. They do not modify this document.*

---

## 16. Brand Positioning & Messaging Framework

> Voice & Tone governs how we speak. This section governs what we say. Every piece of AI-generated copy must trace back to a messaging pillar. Claims not in the approved library must not be published without human review — this is the primary guardrail against hallucinated facts.
>
> Full messaging pillars, approved claims library, per-persona copy angles, and anti-hallucination rules are in **companion/MESSAGING.MD**, loaded by all content-generating agents.

### Positioning Statement

```yaml
positioning:
  statement: "For wine buyers who are tired of algorithm-driven shelves and inflated tasting notes, [Store] is the curated wine retailer that matches the right wine to the right person — because we know our wines and our customers well enough to make that match."

  pillars: ["Honest Curation", "Knowledge Without Pretension", "Right Wine, Right Customer"]
  # Full pillar definitions, approved phrases, and per-persona copy angles: see companion/MESSAGING.MD
```

---

## 17. Budget Governance & Spending Guardrails

### Total Budget

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

### Agent Spending Authority

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
    - action: "Any paid campaign for limited_allocation SKUs (prohibited — see Section 4)"
```

### Stop-Loss Thresholds

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

### Bid Ceilings

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

## 18. Pricing & Promotional Rules

> Full pricing governance — discount authority matrix, promotional frequency rules, price integrity rules, pricing tiers, channel-specific pricing, persona pricing rules, and bundle pricing — is in **companion/PRICING.MD**, loaded by all campaign agents.

---

## 19. Content Strategy & Governance

> Full content governance — content pillars (with example topics, cadence, and quantified KPIs), content mix targets, quality standards, SEO governance, and format specifications — is in **companion/CONTENT.MD**, loaded by all content-generating agents.

---

## 20. Personalization Strategy

> Full personalization tier configuration (permitted signals, allowed/prohibited actions per tier, critical rules) is in **companion/PERSONALIZATION.MD**, loaded by email agents and personalization agents.

### Recommendation Engine Rules

```yaml
recommendation_rules:
  diversity_control:
    max_same_varietal_pct: 60%      # never show only one varietal even for Loyalists
    max_same_region_pct: 70%
    exploration_ratio: 20%           # 1 in 5 recs should be outside known affinity
    out_of_stock_filter: true
    margin_floor: 30%
  
  # For per-page context rules (homepage, PDP, cart, email, post-purchase) and algorithm weights, see companion/PERSONALIZATION.MD

  anti_creepiness_rules:
    - "Never write 'you've been looking at [wine]' — frame as 'still available' instead"
    - "Never reference a specific price point the customer viewed"
    - "Never infer occasion from a single gift purchase — require 2+ gift signals"
    - "Never assume a Collector wants a discount — never recommend discounted versions of prestige SKUs"
    - "Browse history from a single session is not sufficient for persona classification"
    - "A customer who buys wine for others (Gifter) does not have personal wine preferences from those purchases — do not infer"
```

---

## 21. Competitive Intelligence Rules

### Competitive Mention Policy

```yaml
competitive_mention_policy:
  permitted_contexts:
    - "Comparison landing pages — with substantiated SKU-level claims only"
    - "Educational content distinguishing wine regions or producers (factual, not competitive)"
  
  prohibited_contexts:
    - "Email subject lines and body copy — never name a competitor"
    - "Organic social posts — brand dignity above all"
    - "Paid ad copy — never comparative in paid (platform risk + brand risk)"
    - "Any context without immediate substantiation"
  
  legal_requirements:
    - "All comparative claims must be truthful and substantiated (FTC standards)"
    - "Wine press scores used comparatively must be from the same publication and vintage"
    - "Price comparisons must reflect current verified prices — not historical"
    - "Never imply competitor endorsement of our product"
  
  wine_specific_rules:
    - "Never compare tasting notes — subjective and unsubstantiable"
    - "Comparative wine scoring claims require same critic, same vintage, same publication"
    - "Never disparage a producer — the wine community is small"
```

### Competitive Response Triggers

```yaml
competitive_triggers:
  - trigger: "Major online wine retailer announces significant discount campaign"
    response: "Alert; do not auto-match pricing — maintain price integrity"
    agent_action: "Flag in planning queue; human decides on response"
  
  - trigger: "Competitor launches a wine club or subscription competing with ours"
    response: "Review positioning; update battle cards"
    agent_action: "Human review only — do not modify live campaigns"
  
  - trigger: "Competitor faces PR crisis (contamination, fraud, legal action)"
    response: "Do not capitalize — this will be seen as opportunistic and will damage brand"
    agent_action: "Suppress any comparative content scheduled; maintain neutral tone"
  
  - trigger: "High-profile winemaker or producer we carry also launches with a competitor"
    response: "Lead with our relationship and curation story — do not mention competitor"
    agent_action: "Update new arrival campaign copy to strengthen our relationship angle"
```

---

## 22. Crisis & Brand Safety Protocols

> Full crisis protocols, kill switch procedures, brand safety categories, and tone override rules are governed by **companion/SAFETY.MD**, which is loaded at every session start alongside this file. SAFETY.MD is the authoritative and more detailed version of these protocols.

---

## 23. Attribution Model Specification

> Full attribution governance — primary and secondary models, known limitations, agent rules, conversion windows (including wine-specific scenarios and iOS/Safari restrictions), and UTM standards — is in **companion/MEASUREMENT.MD**, loaded by all analytics and reporting agents.

---

## 24. Experimentation Framework

> Full experimentation governance — statistical standards, test governance, concurrent limits, agent authority, guardrail metrics, rollout stages, and wine-specific test designs — is in **companion/EXPERIMENTATION.MD**, loaded by all experimentation agents.

---

## 25. Acquisition vs. Retention Balance

### Strategic Balance

```yaml
acquisition_retention_balance:
  current_business_stage: "scaling"    # update as business matures
  
  target_spend_split:
    acquisition: 45%
    retention: 55%
    note: "Wine retention is high-value — Loyalists and Collectors have 3–5× the CLV of one-time buyers. Retention investment compounds."
  
  rebalancing_trigger: "Review if new customer CAC exceeds 3× first-order AOV for 2 consecutive months"
```

### Acquisition Rules

```yaml
acquisition:
  target_cac: $[N]
  cac_to_ltv_ratio: "1:4 minimum — wine LTV is driven by repeat purchase and CLV growth"
  
  primary_acquisition_channels: [google_shopping, meta_prospecting, organic_search]
  secondary_channels: [pinterest, email_referral, content_seo]
  
  new_customer_definition: "First purchase within last 60 days"
  
  quality_guard:
    min_first_order_value: $35     # don't optimize acquisition for low-AOV first orders
    persona_fit_targeting: true    # target Explorer and Gifter for acquisition — don't acquire Deal Seekers via broad prospecting without offer
    avoid_acquiring_solely_on_deal: "If first order requires > 20% discount to convert, flag for CLV review — these customers rarely return at full price"
```

### Retention Rules

```yaml
retention:
  target_retention_rate_90d: 35%
  target_second_purchase_rate_30d: 30%
  target_annual_purchase_frequency_active_customers: 5
  
  retention_investment_priority:
    1: "Collectors and Loyalists — protect at all cost; personal touch when CLV > $500"
    2: "At-risk high-CLV customers — intervene early with new arrival in their category"
    3: "New Explorer customers — convert to active with discovery-led second-purchase nudge"
    4: "Lapsed Gifters — re-engage before next seasonal occasion"
    5: "Lapsed Deal Seekers — winback with strong offer only; don't over-invest"
  
  churn_prevention_budget: "40% of retention budget"
  winback_budget: "20% of retention budget"
  loyalty_deepening_budget: "40% of retention budget (new arrivals, allocations, exclusives)"
  
  wine_specific_note: "Collector and Loyalist churn is disproportionately costly — one churned Collector represents $2,000–5,000 in lost CLV. These customers warrant direct human outreach, not automated winback."
```

---

## 26. Campaign Taxonomy & Naming Conventions

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
  
  utm_campaign: "[campaign_id]"    # UTM campaign = campaign_id for clean attribution linkage
```

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

## 27. AI Agent Autonomy & Safety Guardrails

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

> This block covers cross-cutting hallucination risk. Domain-specific rules also exist in: **companion/MESSAGING.MD Section 5** (approved claims library, copy-level rules), **companion/CONTENT.MD Section 6** (editorial standards, AI disclosure), **companion/SAFETY.MD Section 9** (brand safety, wine fault descriptions).

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
    action: "Full system pause — see Section 22"
  
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

## 28. Companion File Registry

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
    purpose: "Per-competitor profiles, repositioning statements, objection responses, competitive response triggers"
    loaded_by: [content_agents, ad_copy_agents, campaign_agents]
    required_for: "Any agent producing comparative content or responding to competitor price/product changes"
    version: "1.0.0"
    last_updated: "2026-03-21"
  
  - file: "PARTNERS.MD"
    purpose: "Per-partner branding rules, co-marketing configuration, affiliate disclosure templates, MDF budgets"
    loaded_by: [campaign_agents, content_agents]
    required_for: "Any agent producing co-branded content or managing affiliate campaigns"
    version: "1.0.0"
    last_updated: "2026-03-21"
  
  - file: "PERSONALIZATION.MD"
    purpose: "Recommendation engine full config, dynamic content rules, consent architecture, segment definitions"
    loaded_by: [personalization_agents, update_personalization_skill, send_emails_skill]
    required_for: "Any agent personalizing content beyond what Section 20 defines"
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
    purpose: "Customer value tiers, loyalty program configuration, cross-sell/upsell rules, acquisition/retention detailed rules"
    loaded_by: [analyze_segments_skill, send_emails_skill, plan_campaign_skill]
    required_for: "Any agent managing customer lifecycle transitions or producing CLV-based targeting"
    version: "1.0.0"
    last_updated: "2026-03-21"

session_start_protocol:
  required_reads: [MARKETING-wine-ecommerce.md, SAFETY.MD]
  conditional_reads: "Load companion files based on agent skill role — see loaded_by field above"
  validation: "Agent must log which files it has read before taking any action"
  mcp_server_version: "5.0.0"
  cowork_plugin_version: "1.0.0"
```

