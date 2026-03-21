# PRICING.MD — Wine E-Commerce
*Companion file to MARKETING-wine-ecommerce.md — Discount authority, promotional rules, wine pricing configuration*
*Loaded by: Campaign agents, plan-campaign skill, any agent creating or modifying offers*

---

## 1. Pricing Philosophy

```yaml
pricing_philosophy:
  approach: "Value-based — price reflects quality, curation, and the trust we've built with the customer"
  
  core_principles:
    - "We do not compete on lowest price. Our competitive advantage is curation and knowledge, not discounting."
    - "Promotional pricing is a tool for inventory management and occasion-driven gifting — not a permanent state"
    - "Every discount must have a business reason (overstock, occasion, reactivation) — not just 'it's slow'"
    - "Some customers should never see a discount. Discounting for Collectors or Loyalists in their preferred category is a relationship error."
  
  price_integrity: >
    Price integrity in wine means customers trust that our prices reflect genuine value.
    Artificial compare-at prices, manufactured scarcity, and excessive discounting train
    customers to wait for the sale rather than buy at the moment of desire.
    These patterns are prohibited regardless of short-term conversion benefit.
```

---

## 2. Wine Pricing Tiers

```yaml
product_tiers:
  
  tier_collector:
    definition: "SKUs priced above $100 OR limited allocation / pre-order wines / prestige producers"
    examples: "Grand Cru Burgundy, top Barolo, Napa Cult Cab, en primeur Bordeaux"
    discount_policy: "Never discount. The price is part of the product."
    channel_rules: "Paid ads at list price only. Email: no discount language. Social: no price mention."
    persona_fit: [Collector, Loyalist]
    rationale: "Discounting a $150 Barolo tells the Collector it wasn't worth $150. That damages the relationship permanently."
  
  tier_loyalist:
    definition: "SKUs priced $45–$100; wines with regional or producer pedigree"
    examples: "Village Burgundy, Barolo from known producers, mid-tier Napa Cab, aged Rioja Reserva"
    discount_policy: "Discounts up to 15% for promotional campaigns. Not for new arrivals or limited allocation."
    exception: "Never discount in the Loyalist's primary preferred category — only in adjacent categories"
    persona_fit: [Loyalist, Explorer_advanced]
  
  tier_explorer:
    definition: "SKUs priced $20–$45; accessible-quality wines across all regions"
    examples: "Entry Burgundy, Côtes du Rhône, Malbec from quality producers, New World Pinot Noir"
    discount_policy: "Discounts up to 20% for promotional campaigns; free shipping acceptable autonomous"
    persona_fit: [Explorer, Gifter, Deal_Seeker]
  
  tier_entry:
    definition: "SKUs priced under $20; everyday drinking wines"
    discount_policy: "Discounts up to 25% autonomous; above requires brief approval"
    persona_fit: [Deal_Seeker, Explorer_early]
    note: "Be careful with heavy discounting here — it reinforces price-seeking behavior that doesn't build a profitable customer relationship"
```

---

## 3. Discount Authority Matrix

```yaml
discount_authority:
  
  agent_autonomous:
    max_discount_pct: 10
    permitted_types: [free_shipping, percentage_off_tier_entry_and_explorer]
    excluded_tiers: [tier_collector]
    excluded_sku_conditions:
      - "New arrival within 30 days"
      - "Limited allocation or pre-order wine"
      - "Any wine with fewer than 12 bottles remaining in stock"
      - "Any wine from a prestige producer (Domaine de la Romanée-Conti, Petrus, etc.)"
    max_per_customer: "1 discount per customer per campaign"
  
  notify_then_apply:
    discount_range_pct: "10%–20%"
    prerequisites:
      - "Campaign brief approved at Gate 1"
      - "Discount code specified in campaign brief"
      - "Featured SKU not in excluded conditions above"
    notification: "Slack: campaign ID, SKUs, discount %, estimated margin impact, eligible segment size"
  
  human_approval_required:
    triggers:
      - "Any discount above 20%"
      - "Any site-wide sale"
      - "Flash sale under 48 hours without pre-approved brief"
      - "Any discount on tier_collector SKU (even 5% — escalate to owner)"
      - "Bundle pricing not specified in brief"
      - "Free shipping + percentage discount stacked"
      - "Any discount modification after campaign launch"
```

---

## 4. Promotional Frequency Rules

```yaml
promotional_rules:
  
  frequency_caps:
    max_promotional_campaigns_per_quarter: 3
    min_days_between_promotions: 21    # 3-week cooldown minimum between discount campaigns
    max_promotional_sends_per_customer_per_month: 2
  
  blackout_periods:
    - "First 30 days after any new arrival launch — protect full-price perception"
    - "During or within 7 days of a limited allocation campaign — protect scarcity positioning"
    - "Within 14 days of the same SKU's previous promotion"
  
  price_integrity_rules:
    - "Never advertise a 'was $X, now $Y' unless the wine was sold at $X for at least 30 consecutive days"
    - "Compare-at prices must reflect a genuine prior listed price — not an inflated reference"
    - "Never offer a higher discount on the same SKU than a previous offer without approval"
    - "Allocation wines and pre-order wines are permanently excluded from promotional pricing"
    - "'Limited time' requires a real, visible end date — never use without one"
    - "Seasonal occasion framing (Valentine's Day, harvest) does not constitute a promotional campaign unless a discount code is included"
  
  discount_stacking:
    allowed: false
    exception: "Free shipping may be stacked with a percentage discount if both are in the approved brief and the combined value is within the discount authority"
    max_stacked_discount: 20%

channel_specific_pricing:
  paid_ads:
    rule: "List price only in ad copy unless a discount code is explicitly in the campaign brief"
    note: "Google Shopping automatically pulls prices from the product feed — ensure feed reflects current price accurately"
    alcohol_advertising_note: "Price in paid ads is subject to platform alcohol advertising policies — no 'sale' framing that implies alcohol promotion"
  
  email:
    rule: "Discount permitted per campaign type defaults in MARKETING-wine-ecommerce.md Section 4"
    code_placement: "Prominent — first third of email body; never buried in footer"
    expiry: "Always include offer expiry date; never leave open-ended"
    persona_rule: "Never include a discount code in an email to a Collector or Loyalist in their primary category — even if the code exists in the brief"
  
  organic_social:
    rule: "Never state a specific price in organic social posts"
    rationale: "Wine prices change. Organic posts persist. Always link to PDP where current price is visible."
    exception: "Promotional posts with a discount code — must include the code and expiry date prominently"
  
  on_site:
    rule: "Discount price visible only when: (a) discount code is applied at checkout, or (b) an active campaign brief is running for that SKU"
    crossed_out_price: "Only show if the full price was genuinely the listed price for the past 30 days"
```

---

## 5. Persona Pricing Rules

```yaml
persona_pricing_rules:
  
  Collector:
    discount_policy: "Never — no discount, no exception"
    permitted_alternatives: "Early allocation access; free shipping on case orders; complimentary tasting notes or drinking window report"
    rationale: "A Collector who receives a discount on a prestige wine begins to question whether the wine was worth full price. The relationship is more valuable than the margin you'd recover."
  
  Loyalist:
    discount_policy: "Never in their primary preferred category. Acceptable in adjacent categories."
    example: "A Burgundy Loyalist should never see a discount on Burgundy. A cross-sell promotion on a complementary Rhône is acceptable."
    permitted_alternatives: "New arrival early access; limited allocation priority; producer updates; free shipping on their standard order volume"
  
  Explorer:
    discount_policy: "Standard tiers apply; discovery framing often converts better than discount alone"
    preferred_approach: "Free shipping on first case; bundle with educational content; 'try this region for $X' framing"
    note: "An Explorer who buys because of a discount, not because of discovery, is harder to retain at full price"
  
  Gifter:
    discount_policy: "Standard tiers apply; occasion framing converts as well as or better than discount"
    preferred_approach: "Bundle pricing on gift sets; gift wrapping included; occasion-specific framing without discount"
    note: "Gifters are less price-sensitive than Deal Seekers — the gift's perceived value matters more than the discount"
  
  Deal_Seeker:
    discount_policy: "Full standard tiers apply; urgency language appropriate"
    caution: "Do not over-suppress Deal Seekers post-purchase — they will buy again at the next offer. A repeat Deal Seeker who buys 4× per year during promotions has real LTV."
    retention_note: "Consider a non-discount loyalty mechanism (free shipping tier) to begin moving Deal Seekers toward value beyond price"
```

---

## 6. Bundle Pricing Configuration

```yaml
bundle_pricing:
  
  types:
    curated_case:
      definition: "12-bottle curated case at a combined price — discount typically 10–15% vs. individual"
      approval: "Case configuration requires human review; pricing within tier authority"
      required_validation: "get_frequently_bought_together() data must support the pairing logic"
    
    occasion_gift_set:
      definition: "2–4 bottles packaged together for a specific occasion with gift packaging"
      approval: "Seasonal brief approval covers gift set pricing"
      pricing_display: "Show individual bottle prices + 'Gift set includes wrapping valued at $X' — not a raw discount"
    
    food_pairing_bundle:
      definition: "Wine + complementary product (cheese, charcuterie — if applicable) as a suggested pairing"
      approval: "Human approval for initial bundle configuration; campaign brief for each run"
  
  bundle_rules:
    - "All SKUs in any bundle must be in stock at time of launch and at time of send"
    - "Bundle discount must not reduce individual SKU below floor margin ([N]%)"
    - "Bundle must be validated against frequently_bought_together data — not arbitrary pairings"
    - "Tier restrictions apply within bundles — no tier_collector SKU in a discounted bundle"
```

---

## 7. Versioning

```yaml
pricing_md_wine:
  version: "1.0.0"
  last_updated: "2026-03-21"
  updated_by: "Wine marketing system operator"
  review_cadence: "Monthly — verify tier definitions; update discount authority limits seasonally"
  owner: "Store owner / Marketing lead"
  
  changelog:
    - version: "1.0.0"
      date: "2026-03-21"
      changes: "Initial release"
  
  mcp_alignment: "Aligned with wine-marketing-complete-spec v5.0.0; get_campaign_type_defaults() is the runtime source"
```
