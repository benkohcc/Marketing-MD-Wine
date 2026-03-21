# PARTNERS.MD — Wine E-Commerce
*Companion file to MARKETING-wine-ecommerce.md — Partnership, producer, and affiliate configuration*
*Loaded by: Campaign agents, content agents producing co-branded content*

---

## 1. Partnership Philosophy

```yaml
philosophy:
  purpose: "Partnerships extend our reach and lend credibility — but every partner association reflects on the quality of our curation"
  
  wine_specific_principle: >
    In wine, relationships are everything. The winemakers, importers, and distributors
    we work with are also our advocates. A partnership that damages their reputation
    damages ours. We only partner with producers and organizations whose standards we'd
    stand behind in public.
  
  approval_requirement: "All co-branded content requires human approval before publication, regardless of partner tier"
  
  agent_rule: "Agents draft co-marketing and affiliate content but never publish it autonomously. Gate 2 applies to all partner-facing content, plus explicit partner confirmation from a human operator."
```

---

## 2. Partner Tiers

```yaml
partner_tiers:
  
  tier_1_producer:
    definition: "Winemakers and producers whose wines we actively carry — the core relationship"
    approval_level: "Store owner approves relationship; any co-marketing requires owner review"
    branding_rules: "Producer logo may appear in email featuring their wine; must follow their brand guidelines"
    content_rights: "Product and producer content is subject to what the winery has approved for retail partners"
    notes: "Producers are not traditional marketing partners — they are the product. Handle all producer communication with care. The wine community is small."
  
  tier_2_importer_distributor:
    definition: "Importers and distributors who supply our wines — indirect but important relationships"
    approval_level: "Store owner approves; individual touchpoints are operational, not marketing-led"
    branding_rules: "Typically not co-branded; importer name may appear in product attribution copy"
    content_rights: "Press assets, producer information, and tasting notes often originate from the importer — always credit correctly"
  
  tier_3_affiliate:
    definition: "Revenue-sharing referral partnerships — wine accessories, glassware, travel, food"
    approval_level: "Store owner approves partner onboarding; human approves all affiliate content"
    branding_rules: "Standard brand guidelines apply to all affiliate-produced content referencing us"
    disclosure_requirement: "FTC-compliant affiliate disclosure required on all content"
    scope: "Complementary categories only — never affiliate relationships with competing wine retailers"
  
  tier_4_co_marketing:
    definition: "Occasion-based co-marketing with complementary brands (restaurants, cheese shops, cooking schools)"
    approval_level: "Store owner approves each partnership and each campaign"
    branding_rules: "Standard brand guidelines apply; co-brand lockup approved per campaign"
```

---

## 3. Producer Content Rules

```yaml
producer_content_rules:
  # Rules for using producer/winemaker content in our marketing
  
  press_assets:
    rule: "All press photos, winery imagery, and winemaker portraits require explicit permission from the producer or their PR representative before use"
    attribution: "Always credit the photographer and producer when using their assets"
    agent_rule: "Agents must flag when producer imagery is needed — do not source autonomously"
  
  winemaker_quotes:
    rule: "Only use quotes that appear in approved press releases, verified interviews, or have been provided directly by the winery"
    never: "Generate, paraphrase, or approximate a winemaker quote"
    attribution: "Always include the source (publication, date) when using a quote"
    approval: "Quotes used in email or paid copy require winery PR confirmation that the quote is approved for retail use"
  
  tasting_notes:
    sources_permitted:
      - "Importer's official tasting notes (credit: 'via [Importer Name]')"
      - "Our own tasting notes written by a human with direct experience of the wine"
      - "AI-drafted notes based on catalog data — must be human-reviewed before PDP use"
    never:
      - "Copy tasting notes from another retailer's website"
      - "Generate tasting notes for a wine without catalog data to anchor them"
      - "Present AI-generated notes as if they're from the winemaker"
  
  vintage_information:
    rule: "Vintage assessments attributed to a winemaker or publication must have a verified source"
    agent_rule: "If vintage assessment isn't in the product catalog or approved claims library, omit it — do not generate"
```

---

## 4. Affiliate Configuration

```yaml
affiliates:
  
  policy:
    permitted_categories:
      - "Wine accessories (decanters, corkscrews, wine preservers)"
      - "Glassware (Riedel, Zalto, etc.)"
      - "Wine storage and cellar management"
      - "Wine travel and experiences (wine country tours, virtual tastings)"
      - "Food and cheese (complementary to wine consumption)"
      - "Wine education (courses, books, sommelier content)"
    
    prohibited_categories:
      - "Competing wine retailers or subscription services — direct conflict of interest"
      - "Spirits and beer — out of category; creates positioning confusion"
      - "Products whose quality standards we can't verify"
  
  disclosure_standards:
    short_form: "This post contains affiliate links. We may earn a commission if you purchase through our links."
    long_form: "This content includes affiliate links. If you click and make a purchase, we may receive a small commission at no extra cost to you. We only affiliate with products and brands we'd genuinely recommend."
    placement: "Before the first affiliate link — never at the bottom of the post"
    social: "#ad or #sponsored where required by platform"
  
  per_affiliate_configuration:
    # Template — add each active affiliate here
    - name: "[Affiliate Partner Name]"
      category: "[Category]"
      status: "[active | paused | expired]"
      commission_rate: "[N]%"
      tracking_parameter: "utm_source=email&utm_medium=affiliate&utm_campaign=[affiliate_id]"
      cookie_window_days: [N]
      disclosure_text: "[Specific disclosure if different from standard]"
      prohibited_tactics:
        - "Bidding on our branded keywords"
        - "Discount code stacking with our offers"
      agreement_expiry: "[YYYY-MM-DD]"
      contact: "[Name, email]"
      notes: "[Anything agents should know about this specific affiliate]"
```

---

## 5. Co-Marketing Content Rules

```yaml
co_marketing:
  
  suitable_co_marketing_partners:
    - "Artisan cheese and charcuterie producers"
    - "Independent restaurants with strong wine programs"
    - "Cooking schools and culinary education programs"
    - "Wine country travel operators"
    - "Complementary lifestyle brands with overlapping audiences"
  
  content_approval_sequence:
    1: "Store owner approves the partnership and campaign concept"
    2: "Agent drafts co-branded content"
    3: "Store owner reviews draft (Gate 2)"
    4: "Partner receives draft and confirms approval in writing"
    5: "Final content published"
    
  brand_safety_check:
    - "If co-marketing partner faces a PR crisis, suspend the co-marketing immediately"
    - "Monitor partner for brand safety issues — a partner who produces alcohol-glorifying content reflects on us"
    - "If a partner produces content that violates our responsible consumption standards, suspend the relationship pending review"
  
  wine_community_rules:
    - "Never co-market with a business that disparages a producer or region we carry"
    - "Never co-market with a direct competitor, even indirectly through a shared partner"
    - "Wine critic relationships: we may reference a critic's publicly published scores (per approved claims); we do not create co-marketing content with critics that could be construed as pay-for-play"
```

---

## 6. Versioning

```yaml
partners_md_wine:
  version: "1.0.0"
  last_updated: "2026-03-21"
  updated_by: "Wine marketing system operator"
  review_cadence: "Quarterly — verify affiliate statuses; check producer content permissions; review co-marketing pipeline"
  
  changelog:
    - version: "1.0.0"
      date: "2026-03-21"
      changes: "Initial release"
  
  critical_note: "In wine, producer relationships are the business. Any partner content that touches producer names, winemaker quotes, or producer imagery must be handled with particular care."
```
