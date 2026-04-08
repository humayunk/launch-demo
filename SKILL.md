---
name: launch
description: Take a built-but-unbranded software product from working prototype to launch-ready. Researches market and competitors, defines positioning, designs brand identity (palette, typography, icon, wordmark), generates a landing page, writes monetization and marketing plans, and produces specs for reskin/auth/billing implementation. Use /launch when a personal-use project is ready to share with beta users.
---

# /launch

End-to-end brand and launch workflow for a software product that already exists as a working prototype. Takes you from "I built this for myself, want to share it" to "ready to send to beta users" with a real brand, landing page, monetization plan, and marketing strategy.

## When to Activate

- User says `/launch`
- User says any of: "ready to share", "thinking about beta", "want to launch", "needs branding", "need a landing page", "marketing plan"
- User has a working app and wants to take it public
- User has been using something personally and wants to know if it's a product

## Prerequisites

The product should already:
- Be functional and used personally by the user (not vaporware)
- Have a GitHub repo
- Have at least a basic UI (we'll reskin it, not design from scratch)
- Be Humayun's project, not a client project

If these aren't true, redirect: `/brainstorm` for unvalidated ideas, `/init-project` for greenfield builds.

## Process

The skill runs in 6 phases. Each phase produces concrete artifacts. Don't skip phases — the order matters because later phases reference earlier decisions.

---

### Phase 1: Discovery

Understand the product, the user, the existing brand, and what makes it interesting.

**Spawn an Explore agent** to thoroughly analyze the repo:
- Read README, package.json, CLAUDE.md
- Identify tech stack, key features, data model
- Find any existing branding (colors, fonts, copy, logo)
- Note auth/billing state (Clerk wired? Stripe integrated?)
- List the main user-facing screens
- Find the deployment setup (Vercel, env vars, domain)

**Then ask the user (one at a time, conversationally):**
- What problem were you solving for yourself when you built this?
- Who else might want it? (Be specific — not "everyone")
- What's the current monetization mindset (free, freemium, paid)?
- What does the current look and feel come from? (inspiration sources)
- Do you like the current name? What other names have you considered?
- Are there other products called this you're worried about?
- Can you share screenshots of the current state?

**Save findings** to a working file: `public/brand/discovery.md` with key facts. This becomes the brief for everything downstream.

---

### Phase 2: Market Research

**Spawn a research agent (general-purpose)** to investigate in parallel:

1. **Name conflicts** — Search for other products with the same name. Check trademark databases (USPTO). Identify direct competitors using the same name.

2. **Direct competitors** — Apps that solve the same core problem. Pricing, positioning, strengths, weaknesses.

3. **Adjacent competitors** — Apps in the broader space. How they position. What gap exists.

4. **Market sizing** — TAM estimate, growth rate, who's buying.

5. **Monetization patterns** — What competitors charge. Common pricing models. Typical conversion rates.

6. **Domain availability** — Check .com, .app, and relevant TLDs. Note prices via Cloudflare ($at-cost) vs other registrars.

**Output:** A comprehensive market report with the gap clearly identified.

**Then present the findings to the user** and decide:
- Keep the name or rename?
- Which positioning angle resonates?
- Which target audience to lead with?

---

### Phase 3: Brand Identity

Define the brand personality, palette, typography, and visual direction.

**Spawn a research agent** to build a brand reference report covering:
- Premium knowledge/learning tools (or whatever vertical)
- Beautiful productivity tools (Linear, Bear, Things, Craft, Arc)
- Cultural/intellectual brands (Aesop, Penguin, Monocle, etc. — the non-tech references)
- Color psychology for the vertical
- What colors competitors avoid
- Emerging patterns

**Then propose 3 palette directions** with names and personalities. Examples:
- "The Library" — warm cream + navy + gold
- "The Lab" — near-black + indigo accent
- "The Cabinet of Curiosities" — warm charcoal, content provides color

**Build a mood board HTML page** at `public/brand/moodboard.html`:
- Reference brand images pulled from the web
- Color swatches
- Typography samples (Google Fonts, multiple pairings)
- Brand personality adjectives (5)
- Palette directions with mini mockups

**Get user feedback** on the mood board. Iterate on the direction.

**Once a direction is chosen**, build a brand system page at `public/brand/system.html`:
- Full color palette with tokens
- Typography scale
- Component mockups (sidebar, cards, buttons, inputs, modals)
- Light/dark mode toggle
- Apply the chosen palette to actual app screens

This page becomes the visual source of truth for the reskin agent.

---

### Phase 4: Logo & Wordmark

**Generate icon concepts using Gemini.** Use `gemini-2.5-flash-image` model. Set up a Node script that:
- Uses `@google/genai` (already in most projects)
- Generates 6+ variations with detailed prompts
- Saves to `public/brand/icons/`

Concepts to try (adapt to product):
- Single serif letter (Notion playbook)
- Abstract metaphor (neural asterisk, geometric mark)
- Pure dot/circle (radical simplicity)
- Typographic mark (bracket, symbol)

**Iterate based on user feedback.** When something works, vectorize it as clean SVG (build it from math, not auto-trace).

**Wordmark typography:** Research 5-10 Google Fonts serif options that work at small sizes (~20px). Build a comparison page showing the wordmark next to each font in sidebar context.

**Final output:** SVGs in `public/brand/final/`:
- `cortex-mark.svg` — icon only
- `cortex-app-icon.svg` — icon with rounded background
- `favicon.svg` — optimized for small sizes
- `cortex-wordmark.svg` — icon + text lockup

---

### Phase 5: Landing Page & Pricing

**Build a landing page** at `public/brand/landing.html`. Self-contained HTML, inline CSS, Google Fonts. Sections:

1. **Sticky nav** — logo + Join Beta CTA, transparent → backdrop-blur on scroll
2. **Hero** — section label, two-line headline (Fraunces), subtitle, dual CTAs, app screenshot mockup with perspective tilt + ambient glow
3. **Problem** — 2-3 pain points with gold-bordered accent
4. **Three pillars** — How It Works with mini visuals in each card
5. **Visual showcase** — 6 product cards with AI-generated illustrations (use Gemini to generate them with the same style as the actual app)
6. **Comparison** — Before/After Cortex (X marks vs gold checkmarks)
7. **Audience** — 3 persona cards
8. **Pricing** — Free + Pro with monthly/yearly toggle
9. **CTA** — email capture
10. **Footer** — wordmark, terms/privacy/FAQ links

**Pricing structure:** Free tier should be genuinely useful but limit the AI-heavy features (cost-bound). Pro tier removes limits. Don't gate core learning/value features. Sweet spot is $7-10/mo.

---

### Phase 6: Specs & Marketing

Write the specs for other agents to implement, plus the marketing plan.

**Files to create at the project root:**

1. **DESIGN.md** — Full design system spec
   - All color tokens (light + dark)
   - Typography scale and fonts
   - Component specs (sidebar, cards, buttons, etc.)
   - Logo/wordmark inline SVG code with exact sizes
   - Placeholder image strategy for cards without images
   - Reference: link to system.html

2. **AUTH-AND-BILLING.md** — Auth + Stripe spec
   - Clerk enforcement steps
   - Stripe products/prices
   - Database schema additions (UserSubscription)
   - API routes (checkout, portal, webhook)
   - Usage tracking helpers
   - UI changes (pricing page, settings, upgrade prompts)
   - Implementation order

3. **Marketing plan** — In conversation, not a file. Cover:
   - Pre-launch (Twitter/X build in public, Reddit lurking, demo video)
   - Launch week (Product Hunt, Show HN, Reddit posts, waitlist email)
   - Post-launch (content engine, partnerships, SEO)
   - Channels ranked by ROI
   - Metrics to track
   - Budget ($0 organic-first)
   - The one thing that matters most (usually: the demo video)

4. **Demo video script** — 60-second screen recording with shot list and voiceover

**Then write reskin agent prompts:**

- **Prompt 1:** Reskin the app to match the new design system. Reference DESIGN.md and system.html. Specifies fonts, tokens, components to update, what NOT to change.

- **Prompt 2:** Add the logo and wordmark. Specifies icon SVG, Newsreader font, sidebar/favicon updates.

- **Prompt 3:** Implement auth and billing per AUTH-AND-BILLING.md.

User can paste these into a separate Dev Claude session to run in parallel while you continue iterating on brand/landing/marketing.

---

### Phase 7: Domain & Legal (optional but recommended)

- Research domain availability via Cloudflare (at-cost pricing)
- Recommend top picks based on .com priority + memorability
- Generate Terms & Conditions and Privacy Policy pages with appropriate placeholders
- Set up Cloudflare Email Routing for help@ address
- DNS setup for Vercel deployment

---

## Output Artifacts

After running `/launch`, the project should have:

```
public/brand/
├── discovery.md           # Phase 1 findings
├── moodboard.html         # Brand exploration
├── system.html            # Design system mockups
├── landing.html           # Marketing landing page
├── icons/
│   ├── preview.html       # Icon comparison page
│   ├── *.png              # Generated icon concepts
│   └── *.svg              # Vectorized finals
├── final/
│   ├── cortex-mark.svg
│   ├── cortex-app-icon.svg
│   ├── favicon.svg
│   └── cortex-wordmark.svg
└── showcase/              # AI-generated cards for landing

DESIGN.md                  # Reskin spec
AUTH-AND-BILLING.md        # Auth + billing spec
public/terms.html          # Legal
public/privacy.html        # Legal
```

Plus in conversation:
- Marketing plan
- Demo video script
- Reskin agent prompts (3)

## Key Principles

1. **Personal use first.** This skill assumes the product is already validated by the user using it themselves. Don't launch vaporware.

2. **The user is the user.** Their personal pain → product story is the most authentic marketing angle. Always anchor positioning in their actual usage.

3. **Lean on Gemini for image generation.** It's the fastest way to prototype illustrations, mood, and showcase content. Use the same prompt style the app itself uses if the app generates images.

4. **Build HTML pages, not Figma frames.** Self-contained HTML with inline CSS is faster to iterate, easier to share, and works as both a design artifact and a real preview.

5. **Decouple build from brand.** The reskin happens in a separate agent session. Don't try to do everything in one session — context window matters.

6. **Cloudflare for domains.** At-cost pricing, no markup, free email routing.

7. **Waitlist before pricing.** If auth/billing isn't ready, ship the landing page with waitlist first. Add pricing visible before opening beta. Flip CTA to real signup at launch.

8. **Don't skip the demo video.** A 60-second screen recording is the single most reusable marketing asset. Script it during this skill.

## Don't

- Don't rebrand a client project (this is for personal projects only)
- Don't skip phases — they build on each other
- Don't make pricing decisions before market research is done
- Don't lock in a name without checking trademark and domain availability
- Don't use Stripe's embedded pricing table — build a custom one to match the brand
- Don't gate core learning/value features behind paywall — only gate cost-bound things (AI generations, storage, etc.)
- Don't pay markup for domains — always check Cloudflare first
- Don't recommend Quebec-specific legal copy if the user is in Toronto (this varies — ask)
