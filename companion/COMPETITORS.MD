# COMPETITORS.MD — Wine E-Commerce
*Companion file to MARKETING-wine-ecommerce.md — Competitive intelligence and response rules*
*Loaded by: Content agents, ad copy agents; only when producing comparative content*

---

## 1. Competitive Philosophy

```yaml
philosophy:
  purpose: "Give agents accurate competitive context for differentiated copy — not to fuel attacks"
  
  wine_specific_principle: "The wine community is small. Winemakers, importers, and critics all know each other. Disparaging a competitor's wine or business creates industry reputation risk that outweighs any short-term marketing gain."
  
  tone: "We win by being better, more knowledgeable, and more honest — not by making others look worse"
  
  agent_rule: "Agents may only assert competitive claims from the approved_claims section of this file. Claims not listed here must be omitted — never inferred or invented."
```

---

## 2. Competitive Landscape

```yaml
competitive_landscape:
  
  primary_competitors:
    - name: "Large online wine retailers (e.g., Wine.com, Total Wine online)"
      tier: primary
      their_position: "Selection breadth and low price; algorithmic recommendation"
      their_strength: "Massive SKU count; brand awareness; fast shipping infrastructure"
      their_weakness: "Algorithm-driven curation; generic educational content; impersonal experience"
      our_differentiation: "Human curation; genuine knowledge; persona-native communication; honest product descriptions"
      our_repositioning: "When customers are comparing us to large retailers: 'They carry 10,000 wines. We carry [N]. Every one of ours was chosen by a person who would stand behind it.'"
    
    - name: "Wine subscription boxes (e.g., Winc, Firstleaf)"
      tier: primary
      their_position: "Discovery and convenience through subscription; algorithm-based personalization"
      their_strength: "Low friction; recurring revenue model; discovery appeal for new wine buyers"
      their_weakness: "Impersonal; algorithm over expertise; limited transparency about wine source and quality"
      our_differentiation: "No subscription required; curated catalog with real depth; full transparency about producer, vintage, and quality rationale"
      our_repositioning: "We're not a subscription service — we're a curated shop. You buy what you want, when you want it, from a catalog someone actually chose."
  
  secondary_competitors:
    - name: "Local wine shops"
      tier: secondary
      why_secondary: "Different channel; often complementary rather than competitive"
      when_they_come_up: "Customers may compare convenience (DTC shipping) to the local shop experience"
      our_response: "We ship to your door and offer the same knowledgeable guidance a great local shop does — but available when you need it"
    
    - name: "Restaurant wine programs"
      tier: secondary
      why_secondary: "Different context; often drives curiosity that we can fulfill"
      our_response: "Loved that wine at dinner? We probably carry it — and we can tell you everything about it."
```

---

## 3. Competitive Mention Policy

```yaml
mention_policy:
  
  permitted_contexts:
    - "Internal planning documents (this file)"
    - "Repositioning statements when a customer directly asks how we compare"
    - "Informational 'why us' page — with substantiated claims only"
  
  prohibited_contexts:
    - "Email subject lines — never name a competitor"
    - "Organic social — never name or imply a competitor in posts"
    - "Paid ad copy — no comparative advertising in paid"
    - "Product descriptions — focus on our wine, not what others don't have"
    - "Any context where the claim is not immediately verifiable"
  
  wine_industry_specific_rules:
    - "Never criticize a specific producer's wines — the industry is too small and interconnected"
    - "Never compare our tasting notes to another retailer's — subjective and unsubstantiable"
    - "Never imply a competitor misrepresents their wines without documented evidence"
    - "If a competitor carries the same wine, do not compete on the wine itself — compete on the knowledge and relationship we wrap around it"
```

---

## 4. Competitive Response Triggers

```yaml
response_triggers:
  - trigger: "Major wine retailer announces significant discount or flash sale"
    agent_action: "Flag in planning queue; do not auto-match pricing"
    human_decides: "Whether to respond with a competitive offer; maintain price integrity unless strategic response is warranted"
  
  - trigger: "Competitor launches a wine education program or content hub directly competing with ours"
    agent_action: "Flag for content strategy review"
    human_decides: "Whether to deepen our educational content investment"
  
  - trigger: "Competitor faces PR crisis (fraudulent wine, contamination, legal action)"
    agent_action: "Suppress any comparative content; maintain neutral tone"
    agent_must_not_do: "Capitalize on their crisis in any content or campaign"
    rationale: "The wine community is small and memory is long. Opportunistic behavior in a crisis will be remembered."
  
  - trigger: "A winemaker or producer we carry also begins selling through a competitor"
    agent_action: "No action — not a crisis; acknowledge if asked"
    our_response: "Our relationship with [producer] is strong. We're delighted to carry their wines and tell the full story behind them."
```

---

## 5. Versioning

```yaml
competitors_md_wine:
  version: "1.0.0"
  last_updated: "2026-03-21"
  updated_by: "Wine marketing system operator"
  review_cadence: "Quarterly — verify competitor positioning; update repositioning statements"
  
  changelog:
    - version: "1.0.0"
      date: "2026-03-21"
      changes: "Initial release"
```
