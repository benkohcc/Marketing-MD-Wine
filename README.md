# MARKETING.MD — Wine E-Commerce

**A production-ready implementation of the [MARKETING.MD agentic marketing standard](https://github.com/[your-handle]/marketing-md) for direct-to-consumer wine retail.**

---

## What This Is

This repository is a fully populated vertical implementation of [MARKETING.MD](https://github.com/[your-handle]/marketing-md) — a machine-readable configuration standard for AI-native marketing systems.

Where the generic standard provides templates and placeholders, this implementation provides working configuration for a real business context: a curated direct-to-consumer wine shop, operating via DTC shipping, with an agentic marketing department built on [Claude Cowork](https://www.anthropic.com/) and [MCP](https://modelcontextprotocol.io/) tooling.

If you are new to the `MARKETING.MD` standard, start with the [generic repository](https://github.com/[your-handle]/marketing-md) to understand the concept, architecture, and design decisions. Then return here to see what a complete, production-ready implementation looks like.

---

## What's Included

```
MARKETING.MD                    # Core configuration — loaded by every agent at session start
companion/
  SAFETY.MD                     # Wine-specific crisis protocols (quality, recall, compliance)
  MESSAGING.MD                  # Positioning, pillars, and wine anti-hallucination rules
  PRICING.MD                    # Wine pricing tiers, Collector discount prohibition
  CONTENT.MD                    # Wine editorial strategy, SEO clusters, vintage content rules
  CAMPAIGNS.MD                  # Full blueprints for all 8 campaign types
  CHANNELS.MD                   # Per-channel execution config (email, paid, social, SEO)
  CALENDAR.MD                   # Seasonal wine calendar with brief deadlines and campaign flags
  SIGNALS.MD                    # Behavioral signal config — triggers, suppression, conflict rules
  BUDGET.MD                     # Channel allocation, agent spend authority, stop-loss, bid ceilings
  MEASUREMENT.MD                # Attribution config, wine-specific KPIs
  EXPERIMENTATION.MD            # A/B test library with wine-specific test designs
  COMPETITORS.MD                # DTC wine competitive landscape and response rules
  PERSONALIZATION.MD            # Recommendation engine config, anti-creepiness rules
  LIFECYCLE.MD                  # Value tiers, lifecycle stages, Collector dormancy logic, acq/ret strategy
  PARTNERS.MD                   # Producer content rules, affiliate policy
  VISUAL.MD                     # Wine visual identity system and photography style
```

---

## What Makes This Wine-Specific

Every section of the generic standard has been adapted for the realities of selling wine direct-to-consumer. Some of those realities have no analogue in other verticals.

**DTC shipping compliance.** Wine is one of the most legally complex categories in US e-commerce. Shipping eligibility varies by state, changes without warning, and violations carry regulatory consequences. Every campaign in this implementation includes a pre-send state eligibility check. The kill switch procedure includes specific guidance for shipping compliance crises. Agents are configured to suppress any send to an unverified state rather than proceed.

**Age verification.** Every paid media channel in this implementation is configured with 21+ age targeting. The personalization rules prohibit any behavioral inference from age signals. The safety file requires a visible age gate on all entry points.

**Responsible consumption.** The content and messaging standards explicitly prohibit any copy that frames wine as a vehicle for intoxication, associates consumption with unsafe activities, or makes health claims of any kind. These rules are not in a separate compliance document — they are embedded in the campaign defaults, the approved claims library, and the copy rules throughout.

**Wine hallucination risk.** AI models generate confident, plausible-sounding wine content: press scores from publications that didn't review the wine, production quantities that were never verified, winemaker quotes that were never said. This is a category-specific failure mode with category-specific consequences — a 94-point score fabricated for a 90-point wine is not a vague brand error; it is a false advertising claim. The `MESSAGING.MD` companion file contains an approved claims library and explicit prohibition rules designed specifically for this risk.

**Persona behavior that breaks generic models.** The five customer personas in this implementation — Explorer, Gifter, Loyalist, Deal Seeker, Collector — have behavioral characteristics that differ materially from generic e-commerce personas. A Collector who hasn't purchased in 180 days is not lapsing; they are cellaring. A Gifter who bought wine in February isn't a Loyalist; they were shopping for Valentine's Day. A Loyalist in their primary category should never receive a discount, even when a discount campaign is running. These distinctions are encoded throughout the configuration and would not emerge from a generic template.

**Seasonal calendar specificity.** Wine retail has a distinct seasonal rhythm — Beaujolais Nouveau in November, en primeur in spring, harvest dispatches in fall, Dry January as a suppression window rather than a promotional opportunity. The seasonal calendar in this implementation reflects that rhythm with specific content deadlines, campaign brief windows, and tone rules for each event.

---

## The Five Personas

The customer model at the center of this implementation:

| Persona | Profile | AOV | Primary Need |
|---|---|---|---|
| **Explorer** | 28–42, discovery-driven, building knowledge | $45 | Guidance and education |
| **Gifter** | Occasion-driven, less wine-focused | $80 | Confidence in the gift choice |
| **Loyalist** | Category-committed, repeat buyer | $140 | Insider access and depth |
| **Deal Seeker** | Promotion-activated, value-conscious | $38 | Clear value and urgency |
| **Collector** | Cellar-building, prestige-focused | $450 | Allocation access and vintage intelligence |

Each persona has its own tone angle, channel defaults, suppression rules, discount policy, lifecycle dormancy thresholds, and personalization configuration throughout the companion files.

---

## The Agentic System This Configures

This implementation was built to configure an agentic marketing department running on [Claude Cowork](https://www.anthropic.com/) with MCP tooling. The MCP layer provides 84 functions across seven domains: campaign management, customer data, content and assets, email operations, analytics, advertising, and inventory. The `MARKETING.MD` core and companion files provide the brand context, decision rules, and safety constraints that those functions operate within.

The agent skills the system includes:

- `plan-campaign` — reads this file to propose campaigns aligned with the seasonal calendar and persona defaults
- `generate-content` — reads `CONTENT.MD` and `MESSAGING.MD` before producing any copy
- `check-inventory` — verifies stock before any paid campaign launches or email send references a specific SKU
- `performance-report` — reads `MEASUREMENT.MD` for KPI definitions and attribution configuration before producing any report
- `update-personalization` — reads `PERSONALIZATION.MD` before modifying recommendation weights
- `review-behavior` — reads `EXPERIMENTATION.MD` before designing or evaluating any A/B test
- `lifecycle-analysis` — reads `LIFECYCLE.MD` for tier definitions and winback rules before segmenting customers
- `seo-audit` — reads `CONTENT.MD` for keyword clusters and on-page standards before auditing or optimizing content

---

## Using This as a Starting Point

This implementation is designed to be forked and adapted, not used verbatim. If you are building an agentic marketing system for a wine DTC store, you can use this configuration directly — replacing placeholder values with your brand's specifics — and have a working foundation in hours rather than days.

If you are building for a different vertical, the structure and design decisions transfer even where the content does not. The persona model, the approved claims library, the Collector dormancy logic, the autonomy tier framework — these are patterns that apply across verticals with vertical-specific values substituted in.

The generic `MARKETING.MD` template provides the blank structure. This implementation shows what it looks like when the blanks are filled in with real decisions.

---

## Related

- [MARKETING.MD Generic Standard](https://github.com/[your-handle]/marketing-md) — the template and concept documentation
- [Model Context Protocol](https://modelcontextprotocol.io/) — the tool-calling standard the agentic system uses
- [Anthropic Claude Cowork](https://www.anthropic.com/) — the agentic desktop environment where this system runs
- [Google Stitch / DESIGN.MD](https://deepmind.google/technologies/stitch/) — the design-system analogue that inspired the standard

---

*An implementation of the [MARKETING.MD](https://github.com/[your-handle]/marketing-md) agentic marketing standard.*
