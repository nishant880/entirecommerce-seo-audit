<div align="center">

---

### **[Want us to run this for you? Book a call →](https://entirecommerce.ai/book-a-call)**

---

</div>

# SEO + AEO Audit Playbook

## A full SEO audit you can run on your own brand in 25 minutes inside Claude Code. Covers the traditional SEO surface (technical, on-page, content, backlinks, Core Web Vitals, schema, keyword gaps) plus a merged AEO / AI SEO layer that scores your citation presence across ChatGPT, Claude, Perplexity, and Google AI Overview. Delivered as one Word doc plus the markdown source. Built by Nishant Kapoor at EntireCommerce AI.

---

<div align="center">

### Fastest way to use this playbook

**Paste this document's URL into Claude Code and say:**

> *"Read this and take me through it step by step."*

**Claude will interview you for the business context, walk you through any missing API setup, and run the full audit end-to-end. You don't need to read the rest of this document.**

</div>

---

## Who This Playbook Is For

This playbook is for three people.

**The founder-led DTC brand owner on Shopify** whose organic traffic has plateaued or slipped and who doesn't have a clear picture of which lever will unblock it. You've tried an SEO agency, you've tried a freelancer, you've tried following advice from X threads. You want one document that tells you plainly what the single biggest organic constraint is right now, what to ship this week, and whether AI SEO (LLM citations, AI Overviews) should matter yet for your category.

**The in-house growth lead at a funded DTC brand** running on Shopify or Hydrogen. You have GSC, GA4, Ahrefs, and Clarity. You don't have a single place where traditional SEO and AEO findings get pulled together with a cross-cutting narrative. You want a deliverable you can share with your founder, your writer, and your engineer on the same week.

**The fractional CMO or SEO consultant** running multiple DTC clients. You need a repeatable audit that covers both SEO and AEO in one session, with consistent output across brands. Your problem is consistency: every client gets a slightly different audit depending on which tool you run first. This playbook is the same process every time, the same eight sections, the same synthesis pass.

If you've been piecing together an SEO + AEO audit by hand, running Screaming Frog on one tab, Ahrefs on another, pasting commercial queries into ChatGPT and Perplexity to check citations, this playbook collapses all of that into one Claude Code session.

---

## What The SEO + AEO Audit Actually Is

**The short version.** Eight area sections plus a ranked action list, in one consolidated report. Claude Code runs the SEO diagnostic end-to-end: crawls the site, scores Core Web Vitals per template, audits titles and metas, validates schema, maps content and keyword gaps against 3 to 5 named competitors, scores AEO presence across ChatGPT, Claude, Perplexity, and Google AI Overview, checks the backlink profile, and hands back the top five fixes to ship this week. A dedicated synthesis pass reads the whole draft end-to-end and surfaces three to five cross-cutting themes, the strategic narrative threading through every finding.

**Best for.** Premium DTC brands on Shopify, WooCommerce, or Hydrogen. AOV £500+ or 2x category median. Founder-led. US, UK, or English-speaking European markets. Established brands with 3+ months of GSC data, or pre-launch brands prepping for a content push.

**How it's different.** Three things most SEO audits skip.

First, **one audit covers both SEO and AEO**. Most agencies sell these as two separate products. That split leaves cross-cutting findings on the table. Keyword gaps in SEO often map to AEO citation gaps on the same query. Schema coverage is the same asset in both disciplines. One audit, one report, one action list.

Second, the **synthesis pass**. Section-by-section analysis gives you a directory of findings. The synthesis pass gives you the story. A schema gap in Section 2 that caps AEO extraction in Section 6. A content gap in Section 5 that overlaps an AEO whitespace in Section 6. None of those connections surface from a section-at-a-time read. Claude does the cross-read explicitly, then revises the Executive Summary to lead with the narrative.

Third, **honest stubbing**. GSC access unlocks the deepest query-level findings. Without it, the audit still runs on public SERPs and Ahrefs / DataForSEO, with missing sections clearly stubbed and an access-grant path at the end. No fabricated numbers. No filler paragraphs.

**Skip this playbook if** you're a pure-service business with no local presence, a B2B SaaS brand selling to enterprise, or a mass-market consumer brand where organic can't move the needle. The audit is tuned for premium DTC commerce and the ecommerce-specific sections will be directionally off elsewhere.

---

## Setup (15 Minutes)

### Prerequisites

Before you start, make sure you have:

- **Claude Code** installed. Download from [claude.com/claude-code](https://claude.com/claude-code). Verify with `claude --version`.
- **pandoc** installed for the Word-doc export. On macOS: `brew install pandoc`. On Windows: [pandoc.org/installing.html](https://pandoc.org/installing.html). Verify with `pandoc --version`.
- **A project folder** on your machine. One per brand you audit. Name it after the brand.

### Cost overview

The playbook itself is free. You pay for API credits consumed by tools the audit uses. Most are free or near-free. The one with a meaningful per-run cost is DataForSEO.

| Tool | Subscription model | Typical per-run cost | Role |
|---|---|---|---|
| DataForSEO | Pay-as-you-go, no monthly fee | **$1 to $8** | Recommended. Powers competitor keyword footprints, content gap, backlinks snapshot. |
| Serper | Free tier gives 2,500 credits | Under $0.50 | Recommended. Live SERP snapshots, brand-mention scan, Google AI Overview scan. |
| Keywords Everywhere | ~$10 one-time for 100K credits | Under $0.50 | Recommended. Keyword volume lookups. |
| Ahrefs | $129+ per month | Optional | Skip unless you already have an account. DataForSEO covers most of the same ground. |
| Google PageSpeed Insights | Free | $0 | Uses a Google Cloud API key (`GOOGLE_AI_KEY`). |
| Screaming Frog CLI | Free up to 500 URLs | $0 | Optional. DataForSEO OnPage API covers larger catalogs. |
| Google Search Console | Free (your own account) | $0 | Internal tool. Share access via service account. |
| Google Analytics 4 | Free | $0 | Internal tool. |
| Shopify Admin | Included in your Shopify plan | $0 | Internal tool. Custom-app token, read scopes. |
| Microsoft Clarity | Free | $0 | Internal tool. Free project token. |
| Google Merchant Center | Free to read | $0 | Internal tool. |

**Typical total cost per full audit run: $2 to $10** across the paid external tools.

Numbers above are approximate as of April 2026. Pricing changes. When you run the master prompt, Claude will print the credential inventory and offer to look up current sign-up steps and pricing for any tool you're missing, straight from the web.

### Step 1: Create the project folder

```bash
mkdir my-brand-seo-audit && cd my-brand-seo-audit
```

Drop the three files from this bundle (CLAUDE.md, seo-audit.md, README.md) into the folder.

**Gotcha I hit:** if you're running this on a brand you already have a folder for (from a prior GTM audit run, for example), don't create a new folder. Drop the bundle files into the existing folder so the populated `CLAUDE.md` is reused.

### Step 2: Set up your .env (optional: let Claude walk you through)

Create a `.env` file in the project folder. Add the API keys you have. If you're missing any, that's fine: when you run the master prompt in Step 5, Claude will print which tools are configured and which are missing, and offer to look up the current sign-up steps for each missing one.

Minimum recommended `.env`:

```
DATAFORSEO_LOGIN=your_login
DATAFORSEO_PASSWORD=your_password
DATAFORSEO_AUTH_BASE64=your_base64_auth
SERPER_API_KEY=your_key
KEYWORDS_EVERYWHERE_API_KEY=your_key
GOOGLE_AI_KEY=your_google_cloud_api_key_for_pagespeed
AHREFS_API_KEY=your_key_if_you_have_one
```

**Gotcha I hit:** Google AI Overview scanning requires Serper (its `search` endpoint returns the AI Overview block when one exists for the query). Without Serper, the Section 6 AEO presence audit falls back to manual ChatGPT / Claude / Perplexity prompts, which still works but takes longer.

**Gotcha #2:** Never commit your `.env` to a public repo. Add `.env` to your `.gitignore` before your first commit.

### Step 3: Populate CLAUDE.md (or let Claude interview you)

You have two options:

**Option A (recommended, fastest):** Leave `CLAUDE.md` as-is. When you run the master prompt in Step 5, Claude will interview you conversationally: brand, product, audience, positioning, competitors, tool stack, constraints. Claude writes the file for you progressively as you answer. Takes about 10 minutes.

**Option B (DIY):** Open `CLAUDE.md` and replace every `{placeholder}` with your brand's specifics yourself before running the audit.

Either option produces the same end state: a populated `CLAUDE.md` that grounds every playbook you run from this folder.

**Gotcha #3:** The three-to-five competitor URLs are load-bearing for Sections 3.3 content gap, Section 5 keyword gap, and Section 6 AEO whitespace. Without hand-picked competitors, Claude will auto-discover them from the SERPs. That usually works, but your hand-picked list is always sharper.

### Step 4: Open Claude Code in the folder

```bash
claude
```

Claude Code loads `CLAUDE.md` automatically on session start. Confirm you see "Loaded CLAUDE.md" in the session log.

---

## The Three Files in This Bundle

### File 1: CLAUDE.md (business-briefing template)

**Path:** `{your-project-folder}/CLAUDE.md`
**What it does:** Claude Code loads this on every session start. Your brand's specifics live here. Every playbook you run from this folder reads from here first.
**How to use it:** Option A: let Claude interview you. Option B: replace every `{placeholder}` yourself before running the audit.

### File 2: seo-audit.md (the master prompt Claude runs)

**Path:** `{your-project-folder}/seo-audit.md`
**What it does:** The prompt Claude executes end-to-end to produce the audit. Covers all eight area sections plus the synthesis pass plus the voice-enforcement gate plus the pandoc Word-doc export.
**How to use it:** Paste its entire contents into Claude Code and hit enter. Or paste the Google Doc URL and say "read this and take me through it step by step". Don't edit the prompt unless you know what you're doing. The structure is load-bearing.

### File 3: README.md

**Path:** `{your-project-folder}/README.md`
**What it does:** You're reading it. Setup, run, and troubleshooting reference. Safe to ignore once you've run the audit once.

---

## Your First Run

Five steps. Roughly 25 minutes.

1. **Open Claude Code in your project folder.** `cd my-brand-seo-audit && claude`
2. **Paste the full contents of `seo-audit.md` into the terminal.** Hit enter. Or paste the Google Doc URL and say "read this and take me through it step by step".
3. **Claude prints a credential inventory.** You'll see which External tools are wired and which Internal tools are missing. Internal tools can stay missing. The affected sections stub honestly with an access-grant CTA.
4. **Claude auto-detects the mode** (A1, A2, A2-thin, B1, B2) based on data maturity and access level. Confirm or override.
5. **Claude runs the audit.** Crawls the site, pulls keyword data via DataForSEO, tears down 3 to 5 competitors, checks AEO presence across the four engines, runs the synthesis pass, runs the voice gate, writes the report.

Output lands at:

```
{your-project-folder}/docs/seo-audit/YYYY-MM-DD/seo-audit-report.md
{your-project-folder}/docs/seo-audit/YYYY-MM-DD/seo-audit-report.docx
```

Plus supporting evidence (competitor keyword pulls, AEO citation snapshots, Core Web Vitals JSON, schema validation results) in `{your-project-folder}/data/seo-audit/YYYY-MM-DD/`.

---

## What You'll Get

Ten high-value deliverables in one consolidated report.

1. **Executive summary with cross-cutting themes.** A 3-4 sentence narrative plus 3-5 strategic insights spanning multiple sections. Produced by a dedicated synthesis pass that reads the whole draft end-to-end. This is where the story of your organic opportunity emerges as a strategic narrative threading through every finding.
2. **Audience-language keyword inventory.** Top 100 ranking keywords with 90-day trend, plus the full content-gap and keyword-gap list against your 3 to 5 named competitors. Every query mapped to intent (informational, commercial, transactional) and an action type (new page, expand existing, rewrite title and meta, reclaim lost rank).
3. **Site-crawl findings.** Crawlability and indexation report: broken links, redirect chains, orphan pages, `robots.txt` integrity (including AI-bot allow-list), XML sitemap coverage, canonical tag audit, GSC Index Coverage summary where access exists.
4. **On-page fixes list.** Title and meta audit across the site, H1 and heading hierarchy review, cannibalisation check, duplicate-content flags, image alt coverage. Ranked by impressions at risk.
5. **Content-gap map.** Topical authority heat map (mature / shallow / missing clusters), merge-or-expand list for shallow content, and a set-difference keyword gap against named competitors computed correctly in Python (the standard DataForSEO intersection call returns the wrong set).
6. **AEO presence baseline.** 10 to 20 commercial queries scored across ChatGPT, Claude, Perplexity, and Google AI Overview. Citation matrix, whitespace map (where competitors are cited and you are not), and a Princeton GEO visibility-boost priority list for content edits that improve extraction.
7. **Schema coverage report.** Every schema type (Organization, Product, Breadcrumb, FAQ, Review, HowTo, Article, CollectionPage) scored per template, with the specific fixes that unlock AI extraction and Google rich results.
8. **Technical health score.** Core Web Vitals per template (homepage, top category, top product, top blog, checkout), mobile UX flags, HTTPS hygiene, internal linking graph, `hreflang` setup if you target multiple markets.
9. **Cross-cutting themes from synthesis pass.** 3 to 5 strategic insights each spanning two or more sections, with section numbers called out in brackets. This is the defensible differentiator versus any section-by-section audit.
10. **Ranked P0/P1/P2 action list plus 30-60-90 plan.** Every finding scored on Impact × Confidence × Effort and ranked into "This week", "Next 30 days", and "Backlog" buckets. Followed by a conclusion with next steps and an optional paid-engagement path.

**Format.** One consolidated Word doc (shareable with your team) plus the markdown source (version-controlled in your GitHub repo). Typically 3,500 to 7,000 words. Reading time around 20 minutes cover to cover, 60 seconds to skim via the Key Findings block at the top.

---

## Modes

The audit auto-detects which mode applies and adapts depth accordingly.

| Mode | When it applies | What changes |
|---|---|---|
| A1 (Full) | Established brand, GSC + GA4 + Ahrefs / DataForSEO configured | Complete diagnostic. Every section populates. |
| A2 (Quick) | Established brand, operator running a 30-minute pass before a sprint | Sections 1 through 3 depth, Sections 4 through 6 as a scorecard, Section 9 action list. Caps at 30 minutes. |
| A2-thin | Established brand, GSC-only access | GSC-driven indexation + queries + CTR opportunities. External competitor layer runs on public SERPs. AEO runs in full. |
| B1 (New) | New or pre-launch brand, any external tools | Foundations + keyword strategy + AEO readiness. Competitor positioning carries weight. |
| B2 (Comparison) | Any brand, focused three-competitor comparison | Benchmarks the brand against 3 named competitors across every section. |

---

## Honest Caveats

**AEO citation checks are time-limited snapshots.** ChatGPT, Claude, Perplexity, and Google AI Overview answers shift week to week. A query where your brand is cited today may drop out next month. Re-run Section 6 at least quarterly. Weekly is better for hot categories.

**The synthesis pass depends on Claude holding the whole draft in context.** On very large reports (above 7,000 words), the cross-cutting read can lose depth. If the Cross-cutting Themes block feels thin, rerun with three competitors to shrink the total report size.

**GSC access is the single biggest lever for audit depth.** Sections 1, 3, and 5 lose meaningful precision without GSC. Without it, the audit still runs on Ahrefs / DataForSEO and public SERPs. Grant the shared service account Restricted access on your GSC property before the first run if you can.

**DataForSEO's `labs_keyword_intersection` mode returns the intersection, meaning keywords both sites rank for.** For a genuine content gap you need `labs_ranked_keywords` on both domains separately, then a Python set difference. The playbook handles this correctly. Most tutorials on the internet get it backwards.

**Meta Ad Library is not in this audit.** Competitor creative intelligence lives in the GTM Audit or the Competitor Creative Audit playbook. This audit is SEO + AEO only.

**Voice rules are strictly enforced.** Claude runs a mechanical grep-pass for em-dashes, negative parallelisms ("X, not Y"), banned spelling ("e-commerce"), and AI clichés before writing the report to disk. This catches most style drift but isn't foolproof. If you spot a banned pattern, flag it and rerun the voice gate.

**API costs are real but small.** A typical full run costs $2 to $10 across the paid external tools. Full breakdown in the Cost overview table.

**The playbook is tuned for premium DTC commerce.** Service businesses and B2B SaaS brands can still run it for the technical SEO, AEO, and on-page sections. The ecommerce-specific layers (product schema, Merchant Center, collection hygiene) will be marked N/A.

---

## Quick-Start Checklist

Work top-to-bottom. Items to run first are ordered first.

- [ ] Claude Code installed (`claude --version` works)
- [ ] pandoc installed (`pandoc --version` works)
- [ ] Project folder created for the first brand you want to audit
- [ ] CLAUDE.md from this bundle copied into the project folder
- [ ] seo-audit.md from this bundle copied into the project folder
- [ ] DataForSEO account created and credentials added to `.env`
- [ ] Serper API key added to `.env`
- [ ] Keywords Everywhere API key added to `.env` (free tier is fine)
- [ ] Google Cloud API key created and added to `.env` as `GOOGLE_AI_KEY` (for PageSpeed Insights)
- [ ] (Optional) GSC service account invited as Restricted on your GSC property for the deepest audit
- [ ] CLAUDE.md fully filled in, every placeholder replaced (or let Claude interview you)
- [ ] First run executed and Word doc produced at `docs/seo-audit/{date}/`
- [ ] Report reviewed, top 5 "This week" action items identified
- [ ] Re-run quarterly to track whether the biggest organic lever has moved
- [ ] Book a call if you'd rather we run this for you on a live engagement: [entirecommerce.ai/book-a-call](https://entirecommerce.ai/book-a-call)

---

## Troubleshooting

| Symptom | Likely cause | Fix |
|---|---|---|
| "pandoc not found" at Word-doc export | pandoc not installed | `brew install pandoc` (macOS) or [pandoc.org/installing.html](https://pandoc.org/installing.html) |
| Section 5 content-gap table returns zero rows | DataForSEO `labs_keyword_intersection` misuse | Known. Playbook computes `competitor_keywords - client_keywords` in Python. A clean run handles this automatically. |
| Section 6 AEO citation check shows "no data" for ChatGPT / Claude / Perplexity | WebSearch returns public results only; native LLM prompts run via manual pass | Expected on runs without a custom MCP. Claude will ask you to paste 10 to 20 query outputs from each LLM manually. Or skip and rely on Google AI Overview via Serper. |
| Core Web Vitals pull fails with "API not enabled" | PageSpeed Insights API not enabled on your GCP project | Enable "PageSpeed Insights API" in [console.cloud.google.com](https://console.cloud.google.com/apis/library). Use your existing `GOOGLE_AI_KEY`. |
| Report splits across per-section files when one consolidated file is expected | Sub-agent split issue | Rerun. The spec bans per-section files. A clean run consolidates. |
| Voice gate flags em-dashes or "X, not Y" patterns | Style drift in sub-agent output | Paste the banned-patterns list back into Claude and ask it to scan-and-fix the full file. |
| GSC query pull returns empty | Service account missing on property | Add the shared service account email as Restricted on your GSC property (Settings → Users and permissions → Add user). |
| Sitemap count in Section 1 is zero | `robots.txt` sitemap reference missing | Add `Sitemap: https://{yourdomain}/sitemap.xml` to `robots.txt` and resubmit in GSC. |

---

## Credit

Built by Nishant Kapoor at EntireCommerce AI.

- **LinkedIn**: [linkedin.com/in/nishantkapoor1](https://www.linkedin.com/in/nishantkapoor1)
- **Email**: nishant@entirecommerce.co
- **Book a call**: [entirecommerce.ai/book-a-call](https://entirecommerce.ai/book-a-call)
- **Full playbook library** (GTM audit, weekly review, CRO review, competitor creative audit, and thirty-plus more): [entirecommerce.ai/playbooks](https://entirecommerce.ai/playbooks)

Use this playbook freely. Share it with other DTC founders. If you ship a case study running it on your brand, tag us. We'll link to it from the site.
