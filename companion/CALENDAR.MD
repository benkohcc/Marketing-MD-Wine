# CALENDAR.MD — Wine E-Commerce
*Companion file to MARKETING-wine-ecommerce.md — Seasonal & vertical calendar*
*Loaded by: plan-campaign skill, campaign-planning agents, content agents, seo agents*
*Authority: This file is the sole authority for seasonal event configuration, brief deadlines, and campaign-required flags. Agents check this file at every planning run to identify upcoming events and generate briefs with appropriate lead times.*

---

## Wine Seasonal & Vertical Calendar

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

## Versioning

```yaml
calendar_md_wine:
  version: "1.0.0"
  last_updated: "2026-03-22"
  updated_by: "Wine marketing system operator"
  review_cadence: "Annually — update dates, add new events, remove obsolete ones"

  changelog:
    - version: "1.0.0"
      date: "2026-03-22"
      changes: "Initial release — moved from MARKETING.md Section 5"
```
