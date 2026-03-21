# VISUAL.MD — Wine E-Commerce
*Companion file to MARKETING-wine-ecommerce.md — Visual identity for AI-generated assets*
*Loaded by: Design agents, image-generation agents, content agents producing visual assets*

---

## 1. Visual Identity Philosophy

```yaml
philosophy:
  purpose: "Visual consistency makes us recognizable and trustworthy — every AI-generated asset must feel like it came from the same knowledgeable, unpretentious source"
  
  aesthetic_direction: "Wine without wine-snobbery. Knowledgeable without intimidating. Beautiful without trying too hard."
  
  visual_personality:
    - "Considered — every element is there for a reason"
    - "Warm — the color of good wine, good food, good light"
    - "Honest — we don't over-design; the wine speaks for itself"
    - "Approachable — expertise without exclusion"
  
  what_we_are_not:
    - "Glossy and corporate — we are independent, not a chain"
    - "Rustic and folksy — we are serious about wine"
    - "Trendy and ephemeral — we outlast the trend cycle"
    - "Exclusive and cold — we welcome the curious, not just the expert"
  
  agent_rule: "When in doubt, simpler is correct. An on-brand minimal asset outperforms an off-brand elaborate one."
```

---

## 2. Color Palette

```yaml
colors:
  
  primary:
    name: "Vine Burgundy"
    hex: "#6B2D3E"
    rgb: "rgb(107, 45, 62)"
    use: "Primary brand color — headlines, CTAs, primary email headers, logo background option"
    personality: "Serious, warm, wine-native without being generic"
    do_not_use_for: "Large body text — too dark for readability at small sizes"
  
  secondary:
    name: "Dusty Slate"
    hex: "#4A5568"
    rgb: "rgb(74, 85, 104)"
    use: "Secondary headings, subheadings, supporting UI elements, footer text"
    personality: "Grounded, sophisticated, pairs with everything"
  
  accent:
    name: "Harvest Gold"
    hex: "#C9A84C"
    rgb: "rgb(201, 168, 76)"
    use: "Accent elements — CTA highlights, badges (New, Limited, Featured), price callouts"
    sparingly: true
    do_not_use: "Never as a large background — too loud; works only as an accent"
  
  background_warm:
    name: "Parchment"
    hex: "#FAF7F2"
    rgb: "rgb(250, 247, 242)"
    use: "Email backgrounds, card backgrounds, content section backgrounds"
    personality: "Warm paper — feels editorial, not clinical"
  
  background_light:
    name: "Bone"
    hex: "#F5F0EB"
    rgb: "rgb(245, 240, 235)"
    use: "Alternating content sections; PDP backgrounds"
  
  text_primary:
    name: "Cellar Dark"
    hex: "#1A1A1A"
    rgb: "rgb(26, 26, 26)"
    use: "All primary body text"
    note: "Near-black — softer than pure black; more readable at length"
  
  text_secondary:
    name: "Aged Oak"
    hex: "#5C5049"
    rgb: "rgb(92, 80, 73)"
    use: "Captions, metadata, dates, supporting copy"
  
  text_on_primary:
    hex: "#FAF7F2"
    use: "Text that appears on Vine Burgundy backgrounds"
  
  success_green:
    hex: "#2D6A4F"
    use: "In-stock badges, confirmation states, positive metrics"
  
  alert_amber:
    hex: "#D4A017"
    use: "Low stock warnings, limited availability badges"
  
  prohibited_colors:
    - "Pure black (#000000) — use Cellar Dark instead"
    - "Pure white (#FFFFFF) as a standalone background — use Parchment"
    - "Bright reds or pinks — too much visual competition with wine imagery"
    - "Any neon or saturated color — inconsistent with our measured aesthetic"
```

---

## 3. Typography

```yaml
typography:
  
  primary_font:
    family: "Cormorant Garamond"
    alternative_if_unavailable: "EB Garamond, Georgia, serif"
    weights_available: [Light (300), Regular (400), Medium (500), SemiBold (600), Bold (700)]
    use: "Display headlines, collection titles, seasonal campaign headlines, editorial headers"
    personality: "Elegant but not precious — old-world craft without pretension"
    web_loading: "Use system font fallback while Cormorant loads — avoid FOUT"
  
  secondary_font:
    family: "Inter"
    alternative_if_unavailable: "Helvetica Neue, Arial, sans-serif"
    weights_available: [Regular (400), Medium (500), SemiBold (600), Bold (700)]
    use: "Body copy, navigation, product details, captions, UI elements, email body"
    personality: "Clean, modern, legible — the working font that keeps things readable"
  
  scale:
    display: "48–64px / Cormorant Garamond SemiBold — seasonal hero headlines only"
    h1: "36px / Cormorant Garamond SemiBold — primary page and email headlines"
    h2: "28px / Cormorant Garamond Medium — section headlines, wine names"
    h3: "20px / Inter SemiBold — subheadings, producer names, navigation items"
    body_large: "18px / Inter Regular — featured body copy, email openers"
    body: "16px / Inter Regular — standard body copy, product descriptions"
    body_small: "14px / Inter Regular — captions, metadata, label text"
    caption: "12px / Inter Regular — fine print, legal text, footnotes (minimum size)"
    cta_button: "16px / Inter SemiBold — CTA button text; never smaller"
  
  rules:
    - "Headlines are sentence case — never all-caps except for short badge labels (NEW, LIMITED)"
    - "Body copy is always Inter — Cormorant is for display only (never long paragraphs)"
    - "Never mix more than 2 typefaces in a single asset (Cormorant + Inter is the system)"
    - "Minimum body size is 14px on digital — 12px only for legal fine print"
    - "Line height: 1.5× for body, 1.2× for headlines"
    - "Letter spacing: -0.02em for headlines; 0 for body"
    - "Never stretch or condense type — use weight variations instead"
```

---

## 4. Logo Usage

```yaml
logo:
  
  primary_version: "Wordmark on Vine Burgundy horizontal lockup"
  
  variations:
    - name: "Primary horizontal — light"
      use: "Light backgrounds (Parchment, Bone, white)"
      color: "Vine Burgundy wordmark"
    - name: "Primary horizontal — dark (reversed)"
      use: "Dark backgrounds (Vine Burgundy, Cellar Dark)"
      color: "Parchment wordmark"
    - name: "Icon mark only"
      use: "Social profile images, favicon, contexts where wordmark is too small"
      minimum_size: "32px"
    - name: "Stacked lockup"
      use: "Square formats only — Instagram profile, app icon"
  
  clear_space:
    minimum: "1× the height of the logo letterforms on all sides"
    rule: "Nothing within the clear space — no other text, images, or graphic elements"
  
  minimum_size:
    digital: "120px wide for wordmark; 32px for icon mark"
    print: "25mm wide for wordmark; 8mm for icon mark"
  
  prohibited_uses:
    - "Do not stretch, rotate, or distort the logo"
    - "Do not change logo colors — use only the approved variations above"
    - "Do not add drop shadows, gradients, glows, or outlines"
    - "Do not place the logo on a busy photograph without a containing shape or background"
    - "Do not allow AI image generation to recreate or reinterpret the logo — always use the original file"
    - "Do not use a historical version of the logo — always check for the current version"
  
  co_brand_placement:
    rule: "Our logo appears on the left; partner logo on the right; separated by a thin rule or adequate space"
    size: "Our logo must be equal in visual weight to the partner logo"
    background: "Co-brand lockups always on Parchment background unless otherwise agreed with partner"
```

---

## 5. Photography Style

```yaml
photography:
  
  style_principles:
    - "Natural and ambient light always preferred — avoid studio-flash harshness"
    - "Lifestyle context over pure product isolation — the wine is part of a moment"
    - "Honest color treatment — accurate representation of the wine and setting; no heavy filtering"
    - "Depth and texture — hands, tables, natural surfaces; wine is tactile and sensory"
    - "Restraint — we would rather have one beautiful image than six mediocre ones"
  
  subject_guidelines:
    wine_bottle:
      - "Always show label clearly — brand and vintage must be readable at intended display size"
      - "Preferred: bottle in context (on a table, being poured, beside appropriate food)"
      - "Acceptable: clean studio shot with warm background, no harsh shadows"
      - "Avoid: bottle floating in darkness; heavy gloss highlights obscuring label"
    
    wine_in_glass:
      - "Show the appropriate glass for the varietal — Burgundy bowl for Pinot, Bordeaux glass for Cab"
      - "Fill level: roughly one-third — shows color and gives room for aromas"
      - "Light source: natural or warm artificial — reveal the wine's color authentically"
      - "Hands optional — adds warmth and human context when done naturally"
    
    food_pairing:
      - "Food must be prepared and styled with care — sloppy food styling reflects on the wine"
      - "Frame both the food and the wine — neither should dominate"
      - "Setting should feel like a real meal, not a commercial shoot"
    
    people:
      - "Natural and uncontrived — not posed stock-photo expressions"
      - "Diverse representation — the wine lover is not one type of person"
      - "Expertise shown through context (cellar visit, vineyard) not affected props (sommelier costume)"
    
    settings:
      - "Cellars, vineyards, dining tables, outdoor settings with natural light"
      - "Warm materials: wood, stone, linen, terracotta — not glass, steel, or clinical surfaces"
      - "Avoid: hotel rooms, generic restaurant backdrops, white seamless studio backgrounds"
  
  prohibited:
    - "Heavily filtered or desaturated color treatment (our wine has real color)"
    - "Stock photo clichés (generic couple with wine glasses; business team with champagne)"
    - "Culturally appropriative imagery"
    - "Any image depicting intoxication or excessive consumption"
    - "Real people without model release"
  
  technical:
    minimum_resolution_digital: "1200px minimum dimension; 72dpi"
    minimum_resolution_print: "300dpi at final print size"
    file_formats: [JPEG for photos, PNG for graphics with transparency, WebP for web delivery]
    color_mode: "RGB for digital; CMYK for print"
    hero_email_width: "600px (standard email width)"
    hero_email_height: "300–400px (maintain 2:1 to 3:2 ratio)"
```

---

## 6. Asset Size Specifications

```yaml
asset_sizes:
  
  email:
    header_image: "600px × 300px"
    product_image_in_email: "300px × 300px (square)"
    full_width_product_feature: "600px × 400px"
    max_file_size_per_image: "200KB"
    total_email_image_weight: "< 500KB"
  
  social:
    instagram_feed_square: "1080px × 1080px"
    instagram_feed_portrait: "1080px × 1350px (preferred — takes more screen)"
    instagram_story_reel: "1080px × 1920px"
    pinterest_standard_pin: "1000px × 1500px (2:3 ratio)"
    pinterest_long_pin: "1000px × 2100px (infographic style for guides)"
    facebook_post: "1200px × 630px"
  
  paid_media:
    google_shopping_product_image: "800px × 800px minimum (square)"
    meta_single_image: "1200px × 628px"
    meta_story: "1080px × 1920px"
    meta_carousel_card: "1080px × 1080px"
    google_display_rectangle: "300px × 250px"
    google_display_leaderboard: "728px × 90px"
    google_display_large_rectangle: "336px × 280px"
  
  on_site:
    hero_banner_desktop: "1440px × 600px"
    hero_banner_mobile: "768px × 500px"
    collection_banner: "1200px × 400px"
    product_image_primary: "800px × 800px (square)"
    product_image_thumbnail: "300px × 300px"
    blog_hero: "1200px × 630px"
```

---

## 7. Visual Tone by Campaign Type

```yaml
campaign_visual_tone:
  # How the visual style adapts per campaign type while staying on brand
  
  new_arrival:
    tone: "Clean and focused — the wine is the hero"
    preferred_treatment: "Bottle + label + minimal context; let the wine speak"
    color_emphasis: "Vine Burgundy and Harvest Gold accents"
    badge: "Just Arrived — Vine Burgundy background, Parchment text"
  
  limited_allocation:
    tone: "Quieter, more exclusive — scarcity needs no shouting"
    preferred_treatment: "Bottle in cellar or dark-background setting; intimate scale"
    color_emphasis: "Dark, muted — Cellar Dark backgrounds, Parchment type"
    badge: "Limited — minimal, Cellar Dark background, Parchment text"
    do_not_use: "Urgency red, bright accents, sale-style graphics"
  
  seasonal_promotion:
    tone: "Warm and occasion-appropriate"
    holiday: "Warm candlelight; deep Vine Burgundy and Harvest Gold"
    valentines: "Intimate; warm pinks and burgundy; not garish"
    summer_rose: "Bright, light; Provence-palette inspiration; outdoor settings"
  
  educational_content:
    tone: "Editorial — could be from a quality wine magazine"
    preferred_treatment: "Maps, vineyard photography, winemaker imagery, food and wine context"
    typography_emphasis: "Cormorant headlines prominent; editorial layout"
    do_not_use: "Product shots in editorial content — undermines the educational credibility"
  
  winback:
    tone: "Warm and personal — not promotional"
    preferred_treatment: "A single, beautiful image — not a product grid"
    color_emphasis: "Parchment and warm tones; no urgency visual language"
  
  gift_guide:
    tone: "Celebratory but refined — gift-worthy, not garish"
    preferred_treatment: "Gift context — ribbon, kraft paper, warm setting; not overproduced"
    color_emphasis: "Holiday: Vine Burgundy and Harvest Gold; Valentine: warm plums and blush"
```

---

## 8. AI Image Generation Rules

```yaml
ai_image_generation:
  permitted: true
  approved_use_cases:
    - "Lifestyle and food styling reference images (not final asset — starting point for photographer brief)"
    - "Infographic illustration for blog content and guides"
    - "Background textures and abstract visual elements"
    - "Region and vineyard illustration (non-photographic, clearly illustrative)"
  
  prohibited:
    - "Real wine bottle and label recreation — always use actual product photography"
    - "Real identifiable people — no real faces, no celebrity likenesses"
    - "Winery or cellar recreation that implies a specific real winery"
    - "Any content in SAFETY.MD absolute exclusion categories"
    - "Content suggesting intoxication, irresponsible consumption, or targeting minors"
  
  style_prompt_guidance:
    include:
      - "warm ambient natural light"
      - "editorial photography style"
      - "no harsh shadows"
      - "warm color palette — burgundy, parchment, gold"
      - "authentic, uncontrived feel"
      - "food and wine context"
    avoid:
      - "commercial stock photo look"
      - "overly saturated"
      - "neon or bright artificial lighting"
      - "white seamless background"
      - "posed or artificial expressions"
  
  human_review: "Required before use in any customer-facing context — no exceptions for AI-generated imagery"
  
  disclosure:
    required: true
    method: "Machine-readable metadata tag; visible label in editorial context if AI illustration"
    note: "EU AI Act Article 50 — machine-readable AI content marking required from August 2026"
```

---

## 9. Versioning

```yaml
visual_md_wine:
  version: "1.0.0"
  last_updated: "2026-03-21"
  updated_by: "Wine marketing system operator"
  review_cadence: "Annually or on any brand refresh"
  
  asset_library_location: "[URL or path to master asset library — to be configured]"
  
  changelog:
    - version: "1.0.0"
      date: "2026-03-21"
      changes: "Initial release — wine e-commerce visual identity system"
  
  mcp_alignment: "Visual assets referenced in campaign briefs via get_asset_library(); upload_assets() for new assets"
```
