# CHANNELS.MD — Wine E-Commerce
*Companion file to MARKETING.MD — Channel execution configuration*
*Loaded by: email agents, paid media agents, social agents, seo agents, any agent executing channel-specific actions*
*Authority: This file is the sole authority for per-channel configuration. Universal frequency cap rules are in MARKETING.MD Section 6 (Suppression & Compliance); this file contains full channel configuration.*

---

## Email

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

---

## Paid Media

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

---

## Social

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

---

## SEO / Content

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

## On-Site

```yaml
on_site:
  max_cpc: $[N]
  max_cpm: $[N]
  retargeting_max_cpm: $[N]   # retargeting audiences are smaller and more expensive

  alcohol_advertising_note: "Google, Meta, and Pinterest each have distinct alcohol advertising policies. All paid campaigns require platform-specific compliance review before launch."
```
