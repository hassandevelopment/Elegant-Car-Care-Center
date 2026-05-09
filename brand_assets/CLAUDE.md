# CLAUDE.md — Elegant Car Care Center

> Project context for Claude Code. Read this first before doing anything in this repo.

---

## 1. What this project is

A marketing + lead-capture website for **Elegant Car Care Center** (ELEGANT | CAR POLISH & WASH BAHRAIN), an auto detailing studio located in **East Riffa, Bahrain**.

- **Instagram:** [@elegant.car.center](https://www.instagram.com/elegant.car.center/) (~3.9k followers, 82 posts as of project start)
- **Linktree:** linktr.ee/elegant.bhr
- **WhatsApp / Phone:** +973 3335 2996
- **Hours:** 09:00–12:00 and 15:00–21:00 (split shift, Gulf-style). **Friday closed.**

The site is **not** meant to replace Instagram — Instagram is where the audience already lives. The site exists to:
1. Rank in Google for high-intent local searches ("car polish Riffa", "nano ceramic Bahrain", "تلميع سيارات الرفاع").
2. Show transparent pricing so leads pre-qualify themselves.
3. Push qualified leads into WhatsApp (the actual booking channel).
4. Build credibility for higher-ticket services (Nano Ceramic, Crystal Shine, full PPF tint).

> ⚠️ **Open strategic question for the owner — answer before scoping features:**
> Is the primary job of this site (a) SEO + lead capture into WhatsApp, (b) an actual online booking system with calendar + deposits, or (c) a B2B/fleet credibility play? These three goals lead to very different builds. Default assumption below is (a) until told otherwise.

---

## 2. Reference project — IMPORTANT

**There is a sibling project on this Mac called `Excellent Car Wash`.**

Before starting work on this project, Claude Code should:

1. Locate the `Excellent Car Wash` project directory on the local machine.
2. Read its `CLAUDE.md` (or equivalent context file).
3. Inventory the **skills, subagents, custom commands, and tooling patterns** used there (e.g., any `.claude/agents/`, `.claude/commands/`, MCP server configs, design-system conventions, deployment scripts).
4. **Adopt what fits Elegant; don't blindly copy.** Excellent Car Wash is a different brand with different positioning. Reuse infrastructure (build pipeline, deployment, agent patterns, content workflows). Do **not** reuse brand voice, color tokens, copy, or visual identity.

Things specifically worth lifting if they exist in Excellent Car Wash:
- Bilingual (AR/EN) i18n setup
- RTL CSS strategy
- WhatsApp deep-link helper
- Image optimization pipeline (these car photos are heavy)
- Any SEO/schema.org `LocalBusiness` patterns
- Form-to-WhatsApp lead handoff

If `Excellent Car Wash` doesn't have a pattern for something Elegant needs, build it fresh — don't force-fit.

---

## 3. Brand & visual identity

- **Logo:** Silver sports-car silhouette inside a circular silver crest, on **pure black** background. Wordmark "ELEGANT" in serif caps, "CAR CARE CENTER" arched below with three small stars.
- **Primary palette:**
  - Black `#000000` — dominant background
  - Silver / light gray `#C0C0C0` to `#E5E5E5` — logo, accents, dividers
  - White `#FFFFFF` — body text on dark
  - Accent red `#E63946`-ish — used sparingly for prices and CTAs in their existing creatives
- **Mood:** Premium, masculine, automotive luxury. Think dealership showroom lighting — black with chrome highlights. **Avoid** the generic "car wash" aesthetic (cartoon bubbles, bright blues, sunshine). Their existing ad creatives lean cinematic.
- **Typography direction:** Serif for the wordmark area (matching the logo's "ELEGANT" treatment); a clean modern sans-serif for body. **Must include an Arabic-capable typeface** with proper kashida/diacritic support (e.g., IBM Plex Sans Arabic, Noto Naskh Arabic, or Cairo). Don't pick an English font and hope Arabic looks fine — it won't.

---

## 4. Services & pricing

Pricing is in **BHD (Bahraini Dinar)**. Prices are taken from the brand's existing IG creatives at project start — **confirm with the owner before publishing**, prices change.

### 4.1 Polish packages

| Package | Tier | Price | Includes |
|---|---|---|---|
| 1-Step Polish | All sizes | 10 BD | Wash, polish, wax, interior clean. 2-car deal: 18 BD. |
| Professional Polish (تلميع احترافي) | Small | 30 BD | 3-step polish, scratch removal, plastic polish, 2× wax, engine clean, detailed interior. Lasts ~6 months. |
| Professional Polish | Medium | 35 BD | (same) |
| Professional Polish | SUV | 40 BD | (same) |
| Crystal Shine (لمعة كريستال) | Medium/Small | 50 BD | 5-step polish, scratch removal, plastic polish, **crystal layer**, 2× wax, engine clean, detailed interior. Lasts ~6 months. **Free renewal after 6 months.** |
| Crystal Shine | SUV | 60 BD | (same) |

### 4.2 Nano Ceramic coating

- Small/Medium: **70 BD**
- SUV: **80 BD**
- **3-year warranty**
- Marketed as "New Year offer" — confirm whether this is permanent pricing or a promo.

### 4.3 Window tint — "American Heat Insulation" (Nano-Ceramic film)

- 3 layers, **98% heat rejection** claimed
- Sedan: **40 BD**
- SUV: **46 BD**
- Front window add-on: **14 BD** (excluded from base price)
- **10-year warranty**

### 4.4 Other services visible in content

- Headlight restoration (yellowed → clear)
- Interior deep clean (carpets, console, full vacuum)
- Engine bay cleaning
- Scratch removal
- Plastic trim restoration

### 4.5 Certified products used (worth featuring as a trust signal)

- **Menzerna** (🇩🇪 Germany) — polishing compounds
- **Sonax** (🇩🇪 Germany) — care products
- **Adams** (🇺🇸 USA) — detailing chemicals

These are legitimately premium brand names in the detailing world. Surface them on the site — most local competitors don't disclose what they use.

---

## 5. Technical requirements

### 5.1 Non-negotiables

- **Bilingual: English + Arabic.** Full content parity, not just a translated nav. Locale switcher should be obvious and persist.
- **RTL layout** for Arabic locale. Test every component in both directions. Mirrored icons where appropriate (arrows, chevrons), not text.
- **Mobile-first.** Bahrain mobile traffic dominates. Desktop is secondary.
- **Fast.** Hero/before-after photography is heavy. Use modern formats (AVIF/WebP), responsive `srcset`, lazy loading, CDN. Lighthouse mobile performance ≥ 90.
- **WhatsApp as primary CTA.** Every service card and the sticky footer should deep-link into WhatsApp with a pre-filled message in the user's current locale, e.g. `https://wa.me/97333352996?text=...`.

### 5.2 Should have

- `LocalBusiness` schema.org JSON-LD with proper `geo`, `openingHoursSpecification` (note the split shift and Friday closure), `priceRange`, `areaServed`.
- `Service` schema for each package.
- Open Graph + Twitter cards for each page.
- Google Business Profile link.
- Map embed (their pin is on Road 3912/3914, East Riffa — confirm exact coordinates with owner).
- Before/after gallery component (the brand has strong before/after content; lean into it).
- Reviews/testimonials section — even if starting empty, build the slot.

### 5.3 Nice to have (Phase 2, don't build now)

- Online booking with calendar slots.
- Loyalty/membership tier (their "free renewal after 6 months" hints at this).
- Fleet/B2B inquiry form.
- Blog (only if owner will actually maintain it — dead blogs hurt SEO).

### 5.4 Tech stack

**To be decided.** Default recommendation unless the Excellent Car Wash project dictates otherwise:
- Next.js (App Router) for SSG/SSR + good i18n/RTL story
- Tailwind CSS with logical properties (`ps-*`, `pe-*`) for RTL safety
- `next-intl` or equivalent for AR/EN
- Deploy to Vercel or Cloudflare Pages
- Form submissions → email + WhatsApp deep-link fallback (no DB needed for v1)

If Excellent Car Wash is on a different stack, default to matching it for operational simplicity unless there's a concrete reason not to.

---

## 6. Content & copy guidance

- **Voice:** Confident, premium, factual. Not salesy. Let the photography and product names (Menzerna, Sonax, 3-year warranty) do the bragging.
- **Arabic copy must be written/reviewed by a native speaker.** Machine translation of marketing copy reads as cheap and will undercut the premium positioning. The owner already writes Arabic captions on IG — pull voice from there.
- **Don't invent claims.** "98% heat rejection" and "10-year warranty" come from the brand's own creatives; if the owner can't substantiate a claim, cut it.

---

## 7. What to ask the owner before building

These are blockers, not nice-to-haves. Get answers before scoping:

1. What is the **one** primary goal of the site? (SEO leads → WhatsApp / online booking / B2B credibility)
2. Are the prices listed in §4 current and publishable?
3. Exact business address and Google Maps pin coordinates.
4. Domain name — is one already registered?
5. Do they want a customer review collection mechanism, or are they fine pulling testimonials manually from IG/WhatsApp?
6. Who writes/approves Arabic copy?
7. Is the "free renewal after 6 months" on Crystal Shine an actual standing offer or a one-time campaign?
8. Any partnerships (Menzerna/Sonax/Adams official ties) that should be disclosed/branded with permission?

---

## 8. Things to deliberately NOT do

- Don't build a generic "car wash template" site. The brand is positioned as detailing/luxury, not a $5 wash bay.
- Don't use stock photos when their own photography is strong. Use stock only as filler in early dev, replace before launch.
- Don't auto-translate Arabic with an LLM and ship it. Get human review.
- Don't add a chatbot. WhatsApp is the chatbot here.
- Don't gate pricing. Their competitive edge is transparency.
- Don't forget Friday closure in any date/booking logic. (Friday is the weekend in Bahrain; getting this wrong will look amateur.)

---

## 9. Project status

- **Stage:** Pre-development. CLAUDE.md drafted from brand assets only. No code written. No domain confirmed. No stack chosen.
- **Owner:** [Fill in]
- **Last updated:** 2026-05-09