# CONTENT.MD — Wine E-Commerce
*Companion file to MARKETING-wine-ecommerce.md — Editorial strategy, content governance, SEO*
*Loaded by: generate-content skill, seo-audit skill, any agent producing editorial or long-form content*

---

## 1. Content Strategy Overview

```yaml
content_strategy:
  purpose: "Give wine buyers the knowledge to make confident choices — and make them trust us as the source of that knowledge"
  
  primary_goal: "Build authority and trust with Explorer and Loyalist personas through genuine wine education; drive organic acquisition"
  secondary_goal: "Retain Loyalists and Collectors through vintage intelligence and producer updates that make them feel like insiders"
  
  content_position: "We are the most trustworthy and useful voice for curious wine buyers. We give away knowledge that most retailers bury behind gated content or use to manufacture mystique."
  
  what_we_are_not:
    - "A content farm — we publish less but everything we publish is genuinely useful"
    - "A promotional channel disguised as editorial — content earns trust; it does not beg for the next sale"
    - "A wine critic — we curate and educate; we do not score wines on our own authority"
```

---

## 2. Content Pillars

```yaml
content_pillars:
  
  pillar_1:
    name: "Region & Varietal Education"
    purpose: "Give Explorers the knowledge they're actively looking for; reinforce the Loyalist's expertise and love for their preferred region"
    formats: [blog_post, region_guide, varietal_explainer, email_editorial, social_excerpt]
    target_personas: [Explorer, Loyalist]
    funnel_stage: awareness
    primary_kpi: "content_dwell_time > 180s AND pdp_click_rate > 12%"
    cadence: "2 pieces per month minimum"
    example_topics:
      - "The Eleven Communes of Barolo: What They Mean for the Wine in Your Glass"
      - "Why Burgundy Confuses Everyone (And How to Stop Being Confused)"
      - "Natural Wine: What It Actually Is and Whether You Should Care"
      - "Côtes du Rhône vs. Châteauneuf-du-Pape: The Price Gap Explained"
      - "What 'Old Vine' Actually Means on a Label"
      - "The Texas Hill Country Wine Guide"
  
  pillar_2:
    name: "Vintage Intelligence"
    purpose: "Give Collectors and Loyalists the insider information that justifies their relationship with us — vintage quality assessments, drinking window updates, producer news"
    formats: [vintage_assessment, drinking_window_guide, producer_profile, email_new_arrival, email_editorial]
    target_personas: [Loyalist, Collector]
    funnel_stage: consideration
    primary_kpi: "email_open_rate > 35% on Loyalist/Collector segments AND pdp_conversion_rate > 8%"
    cadence: "1–2 pieces per month; surge during harvest season (Sep–Nov)"
    example_topics:
      - "The 2022 Burgundy Vintage: What We Tasted and What to Buy"
      - "Is Your 2019 Barolo Ready to Open? Here's What We Think"
      - "Meet the Winemaker: [Producer Name]'s Philosophy in Their Own Words"
      - "2021 vs. 2022 Napa Cabernet: How to Choose"
      - "The Case for Cellaring These Five Wines for Another 5 Years"
  
  pillar_3:
    name: "Occasion & Gift Guidance"
    purpose: "Reduce decision anxiety for Gifters; make the right choice obvious for someone who doesn't know wine well"
    formats: [gift_guide, occasion_roundup, food_pairing_guide, email_seasonal]
    target_personas: [Gifter, Explorer]
    funnel_stage: conversion
    primary_kpi: "add_to_cart_rate_from_content > 8%; email_conversion_rate on seasonal campaigns"
    cadence: "Lead time per MARKETING-wine-ecommerce.md Section 5 seasonal calendar"
    example_topics:
      - "The Best Wine Gifts for People Who Know Wine (and People Who Don't)"
      - "What Wine Actually Goes With Thanksgiving Dinner"
      - "Valentine's Day Wine: What to Buy for the Partner Who Has Taste"
      - "The Host Gift That Will Make You Look Like You Know What You're Doing"
      - "10 Wines Under $50 That Taste Like They Should Cost More"
  
  pillar_4:
    name: "The Store's Point of View"
    purpose: "Build brand voice authority — this is where we have opinions, tell our story, and show the character behind the curation"
    formats: [long_form_editorial, harvest_dispatch, producer_visit_notes, store_news]
    target_personas: [all — especially Loyalist and Explorer]
    funnel_stage: awareness_and_retention
    primary_kpi: "social_shares and email_forward_rate (virality over conversion)"
    cadence: "Monthly minimum; seasonal dispatches during harvest"
    example_topics:
      - "Why We Passed on Five Barolos This Year (And What We Found Instead)"
      - "Harvest 2024: What We Tasted, What We're Buying"
      - "The Wine We Almost Didn't Carry (And Why We Changed Our Mind)"
      - "A Conversation with [Winemaker] About Why They Still Farm Organically"

content_mix_targets:
  educational: 40%
  editorial_voice: 25%
  promotional: 25%
  ugc_and_community: 10%
```

---

## 3. Content Formats & Standards

```yaml
format_standards:
  
  blog_post:
    minimum_word_count: 800
    preferred_word_count: 1200
    structure_required: [H1_with_keyword, introduction_hook, H2_subheadings, conclusion, soft_CTA]
    internal_links: "2–4 to relevant PDPs or complementary guides"
    images_required: true
    seo_optimization: required
    human_review: required_before_publish
    wine_specific_rules:
      - "H1 must include the varietal or region name"
      - "Include vintage year wherever relevant — not 'recent vintage'"
      - "Food pairings must name specific dishes, not categories"
      - "Drinking window must use specific years, not 'drink soon' or 'cellar for a while'"
      - "Producer names must be correct and complete on first reference"
  
  region_guide:
    minimum_word_count: 1200
    structure: "[Overview + geography + key producers + varietals + buying guide + recommended SKUs from catalog]"
    internal_links: "3–6 to PDPs and related guides"
    update_cadence_months: 18   # regions don't change; vintages do — update when new vintage releases dominate
    human_review: required
  
  vintage_assessment:
    minimum_word_count: 400
    structure: "[Vintage overview + regional conditions + what to buy + what to cellar + our picks from catalog]"
    required_sourcing: "Vintage assessment must be based on documented harvest data, winemaker reports, or press coverage — never generated from inference"
    expiry: "Assessments for a specific vintage are relevant for 3–5 years — archive after that"
    human_review: required
  
  product_description:
    minimum_word_count: 120
    maximum_word_count: 250
    structure: "[Opening sentence (what it is, who it's for) + tasting notes + food pairing + drinking window]"
    required_fields: [varietal, region, vintage, producer, tasting_notes, drinking_window, food_pairing]
    persona_adaptation: "Tone adapts to the primary persona for this SKU tier (Collector tone for tier_collector, Explorer tone for tier_explorer)"
    seo: "Include varietal + region + vintage in first 50 words; natural — not stuffed"
    human_review: recommended_for_new_skus
  
  email_body:
    maximum_words: 400     # respect inbox attention spans
    structure: "[Hook (first sentence must earn the read) + value + single clear CTA]"
    cta_count: "1 primary CTA; 1 secondary maximum"
    personalization: "Persona-appropriate tone — pull from MESSAGING.MD by_persona sections"
    human_review: required_at_gate_2
  
  social_caption:
    instagram_optimal_chars: 125    # above the fold threshold
    instagram_max_chars: 2200
    facebook_optimal_chars: 250
    pinterest_max_chars: 500
    hashtag_count: "3–5 targeted; never generic #wine alone"
    wine_rules:
      - "Never state a price in organic social — link to PDP"
      - "Vintage year should appear when specific to the post"
      - "Producer names must be spelled correctly — check against product catalog"
```

---

## 4. Editorial Calendar (Structure)

```yaml
editorial_calendar:
  planning_horizon: "6 weeks ahead — briefs due 4 weeks before publish date"
  cadence:
    blog_posts_per_month: 4
    email_newsletters_per_month: 2   # editorial newsletters, not campaign emails
    social_posts_per_week: "See MARKETING-wine-ecommerce.md Section 6"
  
  seasonal_content_windows:
    valentines:
      brief_deadline: "January 10"
      publish_window: "February 1–13"
      formats: [gift_guide, email_editorial, social_content]
      pillar: occasion_and_gift_guidance
    
    houston_rodeo:
      brief_deadline: "February 1"
      publish_window: "Late February – Late March"
      formats: [regional_pairing_guide, social_content, email_editorial]
      pillar: occasion_and_gift_guidance
      note: "City-specific — only if serving Houston market"
    
    spring_clearance:
      brief_deadline: "March 1"
      publish_window: "March 15 – April 15"
      formats: [promotional_email, social_campaign_content]
      pillar: "Promotional — not an editorial pillar"
    
    summer_rose_season:
      brief_deadline: "April 15"
      publish_window: "May – August"
      formats: [varietal_explainer, social_content, email_editorial]
      pillar: region_and_varietal_education
    
    harvest_dispatches:
      brief_deadline: "August 15"
      publish_window: "September – November"
      formats: [vintage_assessment, producer_notes, email_editorial, social_harvest]
      pillar: vintage_intelligence
      note: "Highest engagement period for Loyalist and Collector content"
    
    beaujolais_nouveau:
      brief_deadline: "October 25"
      publish_window: "Third Thursday of November"
      formats: [blog_post, email_new_arrival, social]
      pillar: region_and_varietal_education
    
    thanksgiving:
      brief_deadline: "October 20"
      publish_window: "November 18 – November 28"
      formats: [food_pairing_guide, gift_guide, email_seasonal, social]
      pillar: occasion_and_gift_guidance
    
    holiday_gifting:
      brief_deadline: "November 1"
      publish_window: "November 25 – December 20"
      formats: [gift_guide, email_seasonal, social_campaign, paid_assets]
      pillar: occasion_and_gift_guidance
      note: "Highest-volume content period — begin production in October"
```

---

## 5. SEO Configuration

```yaml
seo:
  
  keyword_strategy:
    approach: "Topic cluster model — pillar pages for major varietals/regions + supporting blog content"
    
    primary_keyword_clusters:
      barolo:
        pillar_page: "Complete Guide to Barolo Wine"
        supporting_topics:
          - "Barolo vs Barbaresco"
          - "When to drink Barolo [vintage year]"
          - "Best Barolo producers"
          - "Barolo food pairing"
          - "How to cellar Barolo"
      
      burgundy_pinot_noir:
        pillar_page: "Burgundy Wine: The Complete Guide"
        supporting_topics:
          - "Burgundy village wines vs premier cru vs grand cru"
          - "Côte de Nuits vs Côte de Beaune"
          - "Burgundy vintages ranked"
          - "Best Burgundy under $100"
      
      napa_cabernet:
        pillar_page: "Napa Valley Cabernet Sauvignon Guide"
        supporting_topics:
          - "Napa vs Sonoma Cabernet"
          - "Best Napa Cabernet vintages"
          - "Napa Cabernet food pairing"
      
      wine_gifts:
        pillar_page: "The Best Wine Gifts for Every Budget"
        supporting_topics:
          - "Best wine gift under $50"
          - "Wine gift for someone who knows wine"
          - "Wine gift sets"
          - "Valentine's Day wine gift"
          - "Wine gift for boss / colleague"
      
      food_pairing:
        pillar_page: "Wine and Food Pairing: The Honest Guide"
        supporting_topics:
          - "Wine with steak"
          - "Wine with salmon"
          - "Wine with Thanksgiving dinner"
          - "Wine with pasta"
    
    cluster_update_cadence_days: 90
    
    keyword_research_sources:
      - "get_search_query_report() — on-site searches are highest-intent demand signals"
      - "get_demand_gap_report() — zero-result searches reveal unmet demand"
      - "Google Search Console — click-through data for ranking keywords"
    
    targeting_criteria:
      min_monthly_search_volume: 100
      max_keyword_difficulty: 50
      priority_intent: [informational, transactional]
  
  on_page_standards:
    title_tag:
      format: "[Primary keyword] — [Secondary hook or producer name] | [Store Name]"
      examples:
        - "Barolo Wine: The Complete Guide | [Store]"
        - "2021 Barolo Brunate, [Producer] | [Store]"
      max_chars: 60
    
    meta_description:
      format: "Compelling description including primary keyword and a specific value hook"
      example: "Discover [wine] — tasting notes, food pairings, and drinking windows from our curated selection. Free shipping over $[N]."
      max_chars: 155
    
    h1: "Must include primary varietal or region keyword; one per page"
    
    h2_structure: "Topic-organized subheadings including secondary keywords naturally"
    
    image_alt_text: "Descriptive and specific — '[Varietal], [Region], [Vintage]' not 'wine bottle image'"
    
    internal_linking:
      blog_to_pdp: "Every educational article must link to 2–4 relevant PDPs"
      blog_to_guide: "Every article should link to 1–2 related pillar guides"
      anchor_text: "Descriptive and specific — never 'click here' or 'read more'"
    
    structured_data:
      blog_posts: "Article schema"
      product_pages: "Product schema including price, availability, and aggregate review rating"
      guides: "FAQPage schema for educational guides with Q&A structure"
    
    canonical_tags: required
  
  wine_seo_rules:
    - "Always include the vintage year in the page title for vintage-specific product pages"
    - "Producer name in the page title increases branded search capture for known producers"
    - "Drinking window guidance must use specific years — 'drink 2024–2030' not 'drink now'"
    - "Food pairings must name specific dishes for long-tail keyword value — 'duck confit' not 'poultry'"
    - "Region guides should target the official appellation name — 'Gevrey-Chambertin' not 'a Burgundy village'"
    - "Varietal pages must include the regional variations — Pinot Noir article should include Burgundy, Oregon, and California angles"
  
  prohibited_seo_tactics:
    - "Keyword stuffing varietal names (e.g., 'Barolo Barolo Barolo wine from the Barolo region')"
    - "Duplicate product descriptions across similar varietal pages without meaningful differentiation"
    - "Auto-generating product descriptions from templates — human review required"
    - "Buying backlinks from non-wine-related domains"
    - "Scraping competitor tasting notes"
    - "Creating thin pages for every producer-vintage combination without genuine content depth"
```

---

## 6. Wine Content Quality Standards

```yaml
quality_standards:
  
  wine_specific_minimum_standards:
    tasting_notes:
      - "Must include primary flavors with specific references (black cherry — not 'dark fruit')"
      - "Must include structural notes (tannin level, acidity, body)"
      - "Must include a finishing note (length, texture, aftertaste)"
      - "Prohibited: 'smooth,' 'complex,' 'balanced' as standalone descriptors — always elaborate"
      - "Length: 3–5 sentences for email; 5–8 sentences for PDP; 8–15 for long-form review"
    
    drinking_windows:
      - "Required format: 'Best from [year] to [year]'"
      - "Must be based on product catalog data — not generated from inference"
      - "If catalog has no drinking window: flag to human; write copy without it; do not estimate"
    
    food_pairings:
      - "Required: minimum 2 specific dish recommendations"
      - "Specific: 'grilled lamb chops with rosemary and garlic' not 'lamb'"
      - "Optional but valued: wine + cheese pairings for Collectors; wine + recipe suggestion for Explorers"
    
    vintage_information:
      - "Vintage year is required on every product page and new arrival email"
      - "Vintage context (good year, great year, challenging year) requires a sourced assessment — see vintage_assessment format"
  
  ai_content_rules:
    disclosure_required: true
    disclosure_method: "Machine-readable metadata tag on all AI-generated content (EU AI Act Article 50 compliance)"
    
    human_review_required_for:
      - "Any vintage assessment or quality claim"
      - "Any content featuring a specific winemaker's name, biography, or quotes"
      - "Any content citing a press score"
      - "Any product description for a tier_collector SKU"
      - "Any content published to channels with > 10,000 followers"
      - "Any content that will be indexed as a primary product page"
    
    human_review_turnaround_hours: 24
  
  content_lifecycle:
    refresh_cadence_days:
      blog_post: 365    # annual check — update vintage info, add new producer details
      region_guide: 548  # 18 months — regions are stable; update for major vintage releases
      vintage_assessment: "Archive when vintage is 5+ years old unless still cellar-relevant"
      product_description: 90   # quarterly — update for new vintage and inventory changes
    
    archive_rules:
      - "Vintage assessments for wines we no longer carry: archive after 12 months"
      - "Gift guides: refresh annually — same structure, updated SKU recommendations"
      - "Food pairing guides: evergreen — refresh every 18 months or when SKU list changes significantly"
    
    evergreen_designation:
      criteria: "Varietal and region guides; food pairing fundamentals; serving temperature and storage guides"
      refresh_trigger: "New major vintage releases, significant producer changes, or appellation regulation updates"
```

---

## 7. Versioning

```yaml
content_md_wine:
  version: "1.0.0"
  last_updated: "2026-03-21"
  updated_by: "Wine marketing system operator"
  review_cadence: "Quarterly — update keyword clusters after each harvest season; add new pillar topics; audit SEO standards"
  owner: "Store owner / Marketing lead"
  
  changelog:
    - version: "1.0.0"
      date: "2026-03-21"
      changes: "Initial release — wine e-commerce specific version"
  
  mcp_alignment: "Aligned with wine-marketing-complete-spec v5.0.0; seo-audit skill reads this file"
```
