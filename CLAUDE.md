# Business brief: {Your brand}

> This file is the business brief Claude Code loads automatically on every session start. It grounds every playbook you run from this folder in your brand's specifics.
>
> **Two ways to populate it:**
>
> **Option A (fastest, recommended).** Leave the file as-is (or delete it entirely). Run the SEO + AEO Audit master prompt and Claude will interview you conversationally, ask every question below, and fill in the file for you as you go. Takes about 10 minutes. You answer in plain language. Claude writes the structured brief.
>
> **Option B (DIY).** Fill in every `{placeholder}` yourself before running the audit. Keep it tight: one to two sentences per field. Use founder voice over marketing copy.
>
> Either way the end state is the same: a populated `CLAUDE.md` that every future playbook (GTM audit, SEO audit, weekly review, etc.) reads from.

---

## Brand overview

- **Brand name**: {Your brand name}
- **Primary URL**: {https://yourbrand.com}
- **Domain age**: {How long the domain has been live, e.g. "launched March 2025" or "ten years"}
- **Ecommerce platform**: {Shopify / WooCommerce / Hydrogen / Custom / etc.}
- **Geographic focus**: {US, UK, EU, global, etc.}
- **Stage**: {Pre-launch / first year / established with trading history / mature}

## Product

- **What you sell (one sentence)**: {e.g. "Launch-monitor-backed short-game training systems for club golfers improving wedge consistency."}
- **Price range**: {e.g. "£500 to £1,200. AOV £650."}
- **Catalog size**: {Number of active SKUs or product lines}
- **Distinctive or patented elements**: {What makes this product materially different from alternatives}

## Primary conversion goal

- **The one conversion that matters most**: {e.g. "Checkout purchase on Shopify" / "Demo request form" / "Email signup for launch list"}
- **Secondary conversion** (optional): {Lead capture, newsletter signup, etc.}

## Target audience (ICP)

- **Core buyer (one sentence)**: {e.g. "Club golfers in the US aged 35 to 55 frustrated by inconsistent wedge distances inside 100 yards."}
- **Secondary buyer (if any)**: {Second audience segment if material}
- **What they search for before buying (intent patterns)**: {Informational queries, comparison queries, commercial queries}
- **Where they hang out online**: {Reddit subs, niche forums, YouTube channels, Instagram accounts, podcasts}

## Founder vision (one to two lines)

{Why the founder built this. What they believe nobody else is doing. The one-line positioning hypothesis.}

## Positioning and competitors

- **Why you win (one sentence, in your words)**: {What you do that nobody else does, or do better}
- **Three to five named competitors (with URLs)**: These feed Section 3 content gap, Section 5 keyword gap, and Section 6 AEO whitespace. Load-bearing.
  - {competitor 1 URL}
  - {competitor 2 URL}
  - {competitor 3 URL}
  - {competitor 4 URL} (optional)
  - {competitor 5 URL} (optional)
- **Pricing tier vs category median**: {e.g. "priced 3x category median" / "premium of the category" / "value tier"}

## Target keywords (hypothesis)

Optional but useful. List 3 to 10 commercial queries you *think* the brand should rank for. The audit validates your hypothesis against public data.

- {primary keyword}
- {secondary keyword 1}
- {secondary keyword 2}

## Monthly traffic and revenue (order of magnitude)

Rough numbers only. Used to calibrate impact estimates in Section 9 (Prioritised Action Items).

- **Monthly organic sessions**: {e.g. "~2,000" or "unknown / pre-launch"}
- **Monthly revenue**: {e.g. "~£50K" or "unknown / pre-launch"}
- **Current organic conversion rate**: {e.g. "~1.2%" or "unknown"}

## Tool stack

List every tool you use for marketing and operations. Claude will detect which have API credentials wired in `.env`.

- **Website / CMS**: {Shopify, WordPress, Next.js, Hydrogen, etc.}
- **Search Console**: {Google Search Console property verified? yes/no}
- **Analytics**: {GA4, Mixpanel, etc.}
- **SEO tools**: {Ahrefs, Semrush, DataForSEO, Screaming Frog, etc.}
- **Ad platforms**: {Google Ads, Meta Ads, TikTok, etc.}
- **Shopping feed**: {Google Merchant Center, Bing Merchant}
- **Email / SMS**: {Klaviyo, Brevo, Postscript, etc.}
- **CRO / session behaviour**: {Microsoft Clarity, Hotjar, FullStory}
- **Tag management**: {GTM, Shopify Pixel Manager}

## Target geography

- **Primary market**: {US / UK / EU / global}
- **Secondary markets (if any)**: {countries the brand also sells into}
- **Languages served**: {English only / English + other}

## Known pain points

- **The organic pain you feel most**: {e.g. "Traffic plateaued six months ago" / "Ranking for head terms but not for commercial queries" / "No AI Overview presence on any buying-intent query" / "Competitors outrank us despite weaker content"}
- **What has been tried and did not work**: {Previous SEO agencies, content programs, link-building campaigns}
- **Internal constraints**: {Time, team, budget, platform limitations}

## Growth goals

- **Twelve-month organic goal**: {What you want organic traffic and revenue to look like in 12 months}
- **The one SEO lever you believe unlocks it**: {If you could only pull one, what would it be? The audit will sanity-check this against the data.}

## Voice and brand guidelines (optional)

- **Spelling conventions**: {e.g. "ecommerce one word, never e-commerce"}
- **Phrases to avoid**: {Any banned clichés, industry jargon you reject}
- **Phrases the brand owns**: {Your recurring taglines, headlines, or catchphrases}
- **Tone**: {Direct / warm / technical / luxury / conversational}

## Session history (updated by Claude across sessions)

> Claude will append notes below as it learns patterns specific to your business. Leave this section blank to start; it grows over time.

---

## How Claude should use this file

On every session start, load this brief and treat it as the ground truth for your brand's specifics. When you run any EntireCommerce playbook (like `seo-audit.md`) in this folder, cross-reference the inputs here before asking the user for them. Do not invent values. If a field is blank, ask the user to fill it in before proceeding with work that depends on it.
