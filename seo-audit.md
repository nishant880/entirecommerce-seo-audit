# SEO + AEO Audit: Master Prompt

> Paste this entire file into Claude Code from a folder containing a `.env` (your API keys). If a `CLAUDE.md` business brief is already present and filled in, Claude loads it and proceeds. Otherwise Claude interviews you conversationally for the business specifics and writes the `CLAUDE.md` for you. Either way, Claude runs the audit end-to-end, produces a single consolidated report in markdown and Word formats, and saves supporting data alongside.
>
> Alternative fastest path: paste this document's URL into Claude Code and say "read this and take me through it step by step". Claude reads the document directly and runs Step 1 through Step 14 without any manual setup.
>
> Built by Nishant Kapoor at EntireCommerce AI. Version 1, April 2026.

---

You are executing the SEO + AEO Audit playbook for the brand in the current working directory. Follow these steps in order. Do not skip steps. Do not invent data. Honour the voice conventions in Step 13.

---

## Step 1. Load or populate the business brief

Look for `CLAUDE.md` in the current working directory.

**If `CLAUDE.md` exists and is fully filled in** (no `{placeholder}` text remaining, required fields populated), read it and proceed to Step 2.

**If `CLAUDE.md` does not exist, contains placeholder text, or is missing required fields, run the business-brief interview before proceeding.** Do not skip. Do not guess the inputs.

### The business-brief interview

Ask the user the following questions conversationally, one batch at a time. After each batch, write the answers into `CLAUDE.md` in the current working directory (create the file if missing) and confirm with the user before moving to the next batch. This is a progressive save.

**Batch 1: Brand overview.** Brand name. Primary URL. How long the domain has been live. Ecommerce platform (Shopify, WooCommerce, Hydrogen, custom, something else). Geographic focus. Stage (pre-launch, first year, established with trading history, mature).

**Batch 2: Product and conversion goal.** What you sell in one sentence. Price range or AOV. Catalog size (number of active SKUs). The primary conversion goal (checkout purchase, demo request, email signup, etc.).

**Batch 3: Target audience (ICP).** Core buyer in one sentence, in your own words. What they search for before buying (informational, comparison, commercial query patterns). Where they hang out online.

**Batch 4: #1 struggle.** The one organic pain the founder feels most right now. Is it flat traffic, ranking for the wrong intent, no AEO presence, a specific Google update, a specific competitor pulling ahead?

**Batch 5: Positioning and competitors.** Why you win in one sentence. Three to five competitor URLs the buyer also considers (load-bearing: these feed Section 3 content gap, Section 5 keyword gap, and Section 6 AEO whitespace). Pricing tier vs category median.

**Batch 6: Tool stack and geography.** Website/CMS. Search Console property verified? Analytics (GA4 or other). SEO tools (Ahrefs, Semrush, DataForSEO). Ad platforms. Shopping feed. Email/SMS. CRO tools. Primary target geography.

### Minimum required to proceed to Step 2

If after the interview you still do not have these seven fields captured, ask again before proceeding:

1. Brand name
2. Primary URL
3. What the brand sells (one sentence)
4. Core buyer (one sentence)
5. Three to five competitor URLs
6. Ecommerce platform
7. Target geography

Optional fields can be marked "unknown" or "to be confirmed" in `CLAUDE.md`. Claude will flag any gaps in the final audit report so the founder knows where the audit leaned on incomplete inputs.

Do not invent any value. Ask the user.

---

## Step 2. Inventory tool access

Read the `.env` file in the current working directory. Print a credential inventory to the user in this format:

```
External tools (public data)
- DataForSEO: configured / not configured
- Serper: configured / not configured
- Keywords Everywhere: configured / not configured
- Ahrefs: configured / not configured
- Google PageSpeed Insights (GOOGLE_AI_KEY): configured / not configured
- Screaming Frog CLI (local): configured / not configured

Internal tools (your brand's own data)
- Google Search Console: configured / not configured
- Google Analytics 4: configured / not configured
- Shopify Admin: configured / not configured
- Microsoft Clarity: configured / not configured
- Google Merchant Center: configured / not configured
```

For each internal tool flagged "not configured", the corresponding section of the report will stub out with a "grant access to populate" note. That is expected behaviour. Missing tools become access-grant items in the final report's checklist.

### Offer setup instructions for missing tools

After printing the inventory, go through each tool flagged "not configured" (External and Internal both). For each one, ask the user:

> "`{Tool}` is not configured. Want me to look up the current sign-up steps and API-key retrieval flow, so you can wire it in and we can populate more of the audit? Answer `yes`, `no`, or `skip all`."

If the user answers `yes`, use WebSearch and WebFetch to pull the current sign-up flow for that specific tool (pricing tiers, free-tier availability, where the API key lives in the account settings, and the exact `.env` variable name this playbook expects). Produce step-by-step instructions the user can follow in ~5 minutes. Include a one-line estimate of credit cost for a typical audit run where known.

If the user answers `no` for a specific tool, skip that one and ask about the next missing tool.

If the user answers `skip all` at any point, stop offering and proceed to Step 3.

After the user adds any new credentials to `.env`, reprint the updated credential inventory before continuing. Confirm the new tool is now flagged "configured".

Never hardcode sign-up URLs or pricing numbers from memory. Pull fresh from the web every time.

---

## Step 3. Detect path and mode

Based on the `.env` inventory and the brand's data maturity (inferred from `CLAUDE.md` "Stage" field and any Shopify/GSC/GA4 history available), auto-detect the path and mode:

| Mode | Path | Trigger |
|---|---|---|
| A1 (Full) | Established | GSC + GA4 + Ahrefs/DataForSEO all configured |
| A2 (Quick) | Established | Same as A1 but operator running a 30-minute scan before a sprint |
| A2-thin | Established | Only GSC configured, no other external credentials |
| B1 (New) | New / pre-launch | Any external tool set, minimal GSC history |
| B2 (Comparison) | Either | Focused three-competitor comparison |

State the detected path and mode, and ask the user to confirm or override. Record both in the report header.

---

## Step 4. Section 1. Crawlability and indexation

Produce Section 1 in drafting mode. Do not write to disk yet.

- `[E]` Site-level crawl via Screaming Frog CLI or DataForSEO OnPage API. Report crawled-URL count, crawl depth, broken links, redirect chains, orphan pages (no internal links pointing to them).
- `[E]` `robots.txt` check: presence, syntax, blocked paths, sitemap reference, AI-bot allow-list (must allow GPTBot, ChatGPT-User, PerplexityBot, ClaudeBot, anthropic-ai, Google-Extended, Bingbot). Missing any of these blocks AEO surface.
- `[E]` XML sitemap check: presence, index sitemap format, URL count, last-modified dates, sitemap referenced in `robots.txt`.
- `[E]` `noindex` / `nofollow` tag review on commercial pages.
- `[E]` Canonical tag audit: self-canonicals on unique pages, cross-canonicals on duplicates, no canonical chains.
- `[I]` GSC Index Coverage report: Valid count, Excluded breakdown.
- `[I]` GSC sitemap submission status.
- `[E]` Shopify redirect chain hygiene (Shopify only) via `shopify-admin-url-redirect-audit` skill.
- `[E]` Shopify collection hygiene (Shopify only) via `shopify-admin-collection-membership-audit` skill.

Output: a coverage scorecard, a ranked list of indexation blockers, and a short list of orphan or near-orphan pages worth reconnecting.

## Step 5. Section 2. Technical foundations

- `[E]` Core Web Vitals per template via PageSpeed Insights API. Pull mobile and desktop. Templates: homepage, top category, top product, top blog, checkout. Thresholds: LCP < 2.5s, INP < 200ms, CLS < 0.1, mobile score > 70, desktop score > 80. Flag every template failing any threshold.
- `[E]` Mobile UX audit: viewport meta, tap-target sizing, legible font sizes, no horizontal scroll.
- `[E]` Schema markup validation: Organization, Product, Breadcrumb, FAQ, Review, HowTo, Article, CollectionPage. Record which schemas are present, which are missing, which have warnings.
- `[E]` HTTPS and certificate check: HTTP to HTTPS redirect, valid certificate, no mixed-content warnings.
- `[E]` Internal linking graph: anchor-text distribution, orphan pages, deep-link pages more than 3 clicks from home. Flag commercial pages receiving fewer than 5 internal links.
- `[E]` URL structure: lowercase, hyphenated, no session IDs, consistent trailing-slash behaviour.
- `[E]` International SEO: `hreflang` tag presence and bidirectional matching, `x-default` for the global version.

Output: Core Web Vitals template table, schema coverage matrix, ranked template-level fixes.

## Step 6. Section 3. On-page SEO

- `[E]` Title tag audit: length (30 to 60 chars), primary keyword position, uniqueness, brand suffix consistency.
- `[E]` Meta description audit: length (120 to 160 chars), uniqueness, click-earning phrasing.
- `[E]` H1 audit: one H1 per page, primary-keyword match, no stuffing.
- `[E]` Heading hierarchy: logical H1 → H2 → H3 nesting.
- `[E]` Keyword cannibalisation via Ahrefs or DataForSEO.
- `[E+I]` Cannibalisation confirmation via GSC query-to-page mapping when available.
- `[E]` Duplicate content and faceted-navigation crawl traps.
- `[E]` Image alt text on priority templates.

Output: a prioritised on-page fixes list.

## Step 7. Section 4. Content quality and topical authority

- `[E]` E-E-A-T signals: author byline with bio, author credentials, About page completeness, contact info, terms and privacy, original research, external citations.
- `[E]` Content depth per priority page: word count, embedded media, original analysis, first-hand experience markers.
- `[E]` Content freshness: last-updated timestamp visible, annual refresh pattern for evergreen content.
- `[E]` Topical authority map: cluster existing content, flag mature / shallow / missing topics.
- `[E]` Duplicate-topic audit: merge candidates.
- `[E]` Thin content: pages under 300 words on commercial intents.

Output: topical-authority heat map, merge-or-expand list.

## Step 8. Section 5. Keyword footprint and content gaps

- `[E]` Ahrefs or DataForSEO top-100 ranking keywords for the brand domain (position, URL, volume, difficulty, traffic share).
- `[E]` 90-day position-trend analysis. Flag keywords gaining or losing 10+ positions.
- `[E+I]` GSC query-level data (when available): top 100 queries by impressions, top 50 by clicks, top 50 by CTR.
- `[E]` Competitor keyword gap vs the 3 to 5 competitors from the positioning brief. **Do not use DataForSEO's `labs_keyword_intersection` for gap analysis** (known bug: it returns the intersection, the keywords both domains rank for). Pull `labs_ranked_keywords` on the brand and each competitor separately, then compute `competitor_keywords - brand_keywords` in Python.
- `[E+I]` Striking-distance queries (position 4 to 15, impressions 50+).
- `[E+I]` High-impression low-CTR queries (position 1 to 10, CTR under 1%).
- `[E]` Branded vs non-branded split: Ahrefs estimate, GSC confirmation when available.

Output: ranked opportunity list. Content-scoring rubric: Customer Impact 40%, Content-Market Fit 30%, Search Potential 20%, Resources 10%.

## Step 9. Section 6. AEO and AI-SEO

- `[E]` Run 10 to 20 commercial queries from the brand's category across ChatGPT, Claude, Perplexity, and Google AI Overview. Use `seo_toolkit.py aeo-serp` for the Google AI Overview scan. For the three LLMs, run manual prompts. For each query record: brand citation (yes/no), competitor citations, AI Overview existence, source URLs cited.
- `[E]` Cross-engine presence matrix: query × engine grid.
- `[E]` Extractability checklist per priority page: clear definition in first paragraph, self-contained answer blocks, statistics with named sources, comparison tables, FAQ with natural-language questions, schema markup (FAQ, HowTo, Article, Product), expert attribution, updated within 6 months, heading structure matches query patterns, AI bots allowed in robots.txt.
- `[E]` Princeton GEO visibility-boost plays: cite sources (+40%), add statistics (+37%), add quotations (+30%), authoritative tone (+25%), improve clarity (+20%), technical terms (+18%).
- `[E]` AEO whitespace map: queries where the brand has zero presence but 2+ competitors are cited.
- `[E]` Entity and topic clarity: homepage declares what the brand is in first 100 words, `Organization` schema with `sameAs` links, author pages with `Person` schema.
- `[E]` Conversational-query and passage-ranking targeting: 10 most commercially valuable conversational queries, self-contained-answer check, direct-answer-snippet check.

Output: AEO presence scorecard, whitespace map, ranked AEO content edit list.

## Step 10. Section 7. Backlinks and domain authority

- `[E]` DataForSEO Backlinks or Ahrefs snapshot: referring-domains count, DR/DA, new and lost links over 90 days, spam score (flag above 5).
- `[E]` Link velocity trend over 12 months.
- `[E]` Competitor backlink comparison. Surface domains linking to competitors but not the client.
- `[E]` Unlinked brand-mention scan via Serper.
- `[E]` Toxic-link flags: spam-score thresholds, anchor-text distribution anomalies.
- `[E]` 10-tier backlink target list for the first 90 days.
- `[I]` GSC Top linking sites report.

Output: referring-domain scorecard, ranked reclaim list, 10-tier target list.

## Step 11. Section 8. Local and ecommerce-specific

Runs for ecommerce brands (Shopify, WooCommerce, Hydrogen). Service / B2B brands substitute Local SEO or skip.

### Ecommerce

- `[E]` Product schema coverage and quality on every PDP.
- `[E]` Collection / category-page structure: `CollectionPage` schema, unique H1, category description, faceted-navigation crawl control.
- `[E]` Breadcrumb schema on every PDP and collection.
- `[I]` Google Merchant Center feed health (if access granted).
- `[I]` Shopify: sales-channel activation, metafield consistency.

### Local (alternative)

- `[E]` Google Business Profile completeness.
- `[E]` NAP consistency across major directories.
- `[E]` Local citation audit against top 20 niche and geographic directories.

Output: product-schema scorecard, feed-health scorecard, top 5 catalog-structure fixes.

## Step 12. Section 9. Prioritised Action Items

Convert every finding from Sections 1 through 8 into a candidate initiative. Score each on ICE:

- Impact (1 to 10): expected organic revenue or traffic lift
- Confidence (1 to 10): how sure the initiative works
- Effort (1 to 10, inverse): lower effort = higher score

Multiply for ICE score. Rank descending. Group into three buckets:

- **This week** (top 5 items). Work starts immediately.
- **Next 30 days** (next 10 items).
- **Backlog** (everything else).

**Do not label as P0/P1/P2 in the output.** Use the bucket names only.

Open Section 9 with "The biggest organic lever":

- One sentence naming the single biggest lever holding organic revenue back.
- Three to five bullets of evidence pulling the strongest data points from Sections 1 through 8. Tag each as `[E]` or `[I]`.
- One or two sentences on the counter-move.
- Expected organic impact, quantified with assumptions stated.
- Confidence: high / medium / low with a reason.

On Path B (new brand), replace "The biggest organic lever" with "The critical path hypothesis" framed as a testable experiment with a kill criterion.

Close Section 9 with an optional 30-60-90 summary:

- **30 days.** Quick wins from "This week" and "Next 30 days".
- **60 days.** Content-cluster builds and AEO-extraction rewrites.
- **90 days.** Backlink campaign results, authority-signal compounding.

---

## Step 13. Synthesis pass (mandatory before writing to disk)

Do not write the report yet. Assemble the complete draft of Sections 1 through 9 as a single document in your working context and read it end-to-end in one pass. Ask:

- What pattern emerges across three or more sections that no single section captures?
- What does a finding in Section X imply for recommendations in Section Y? (A content gap in Section 5 that overlaps an AEO citation gap in Section 6. A schema-coverage weakness in Section 2 that caps AEO extraction in Section 6. An on-page issue in Section 3 that compounds a crawl-depth issue in Section 1. A backlink gap in Section 7 that limits Section 5's rankability.)
- Is there a strategic narrative connecting the data that the Executive Summary placeholder misses?
- Does any Section 9 action address multiple section findings at once? Promote it.
- Does any high-ranked Section 9 action solve only one problem? Consider demoting it in favour of multi-leverage plays.

Produce 3 to 5 cross-cutting insight bullets. Each bullet:

- States the insight in one sentence.
- Names the sections it spans in brackets at the end.
- Is a synthesis of cross-section implications.

Then revise:

- **Executive Summary** to lead with the narrative these insights reveal (3-4 sentences total).
- **Section 9** to re-rank actions that hit multiple leverage points.
- Write the bullets into the **Cross-cutting themes** block immediately after the Executive Summary.
- Generate the **Key findings** block (5 to 7 one-sentence bullets, one per section).
- Generate the **Key action items** block (top 5 from Section 9 pulled to the front with a one-line "why this first" tied back to cross-cutting themes).
- Draft the **Conclusion** block at the end (2 to 3 short paragraphs: what to do this week, what a paid engagement looks like if the founder wants this run for them, booking CTA at https://entirecommerce.ai/book-a-call).

---

## Step 14. Voice enforcement gate (mandatory before writing to disk)

Grep the full draft for each banned pattern and rewrite every match:

| Banned | Grep for | Fix |
|---|---|---|
| Em-dash | `—` (U+2014) or `--` used as em-dash | Replace with period, comma, or colon |
| Negative parallelism | `, not `, ` rather than `, ` instead of `, `opposite of `, `not only ` | Rewrite to state the positive claim alone |
| Banned spelling | `e-commerce`, `E-commerce`, `E-Commerce` | Replace with `ecommerce` |
| AI clichés | `Here's the`, `Here's what`, `Here's why`, `Most people`, `The uncomfortable truth`, `The brutal truth`, `The breakthrough` | Rewrite without the cliché frame |
| Sub-four-word sentence | Sentences of 1 to 3 words standing alone | Merge into neighbour or expand |

`not` is permitted only when the negation is genuinely load-bearing. Default to rewriting.

Shipping a report with more than zero banned-pattern matches is a spec violation. Sub-agents must run the same voice-scan on their returned output before you merge.

---

## Step 15. Write outputs

Report structure (fixed order):

```
# SEO + AEO Audit: {Brand Name} ({YYYY-MM-DD})

Mode: {A1 / A2 / A2-thin / B1 / B2}
Path: {A Established / B New}
Access level: {External only / External + Internal}

## Executive summary
(3-4 sentences leading with the narrative)

## Cross-cutting themes
(3-5 synthesis bullets from Step 13)

## Key findings
(5-7 one-line bullets across sections)

## Key action items (top 5 this week)
(top 5 from Section 9 pulled to the front with "why this first")

## 1. Crawlability and indexation
## 2. Technical foundations
## 3. On-page SEO
## 4. Content quality and topical authority
## 5. Keyword footprint and content gaps
## 6. AEO and AI-SEO
## 7. Backlinks and domain authority
## 8. Local and ecommerce-specific
## 9. Prioritised Action Items

## Access-grant checklist
(Only appears if any Internal-layer section is stubbed)

## Conclusion
(2-3 paragraphs)
```

Write the file to:

```
{cwd}/docs/seo-audit/{YYYY-MM-DD}/seo-audit-report.md
```

Then convert to Word doc:

```bash
pandoc {cwd}/docs/seo-audit/{YYYY-MM-DD}/seo-audit-report.md \
  -o {cwd}/docs/seo-audit/{YYYY-MM-DD}/seo-audit-report.docx \
  --toc --number-sections
```

If pandoc is not installed, tell the user: `brew install pandoc` (Mac) or equivalent. Do not skip the Word doc silently.

Save supporting data (DataForSEO JSON pulls, GSC CSV exports, per-competitor crawl files, AEO citation snapshots, Core Web Vitals results, schema validation output) to:

```
{cwd}/data/seo-audit/{YYYY-MM-DD}/
```

**Exactly one consolidated report file at the primary output path.** Do not produce per-section files. If sub-agents returned per-section drafts, merge them into the single file before writing.

---

## Step 16. Merge into actions.md

If the current working directory has an `actions.md` file, merge the five items from "Key action items (this week)" into the Next Actions section. Respect the existing priority caps (P0 max 5, P1 max 10, P2 max 15). If a tier is over cap, rescore by ICE and demote the weakest before adding.

---

## Step 17. Commit (optional)

If the folder is a git repo, commit the report, Word doc, data files, and updated actions.md. Commit message format:

```
SEO + AEO audit: {Brand Name} ({YYYY-MM-DD}): {biggest lever in 6 words}
```

---

## Voice conventions (strict, applied throughout)

- No em-dashes. Use period, comma, or colon.
- No negative parallelisms. Never "X, not Y". State the positive.
- Four-word sentence floor. No one- or two-word sentences.
- Spelling: "ecommerce" one word.
- No AI clichés.
- Every finding traces to real data. No fabricated numbers. No invented sources.
- If a section is stubbed for missing access, state it plainly with the access path.

---

## Acceptance criteria

- End-to-end from this one prompt. No manual copy-paste between steps.
- Correct mode detection with user confirmation.
- Single consolidated report at the output path. Cross-cutting themes, Key findings, Key action items, Conclusion blocks populated by the synthesis pass.
- Word doc produced alongside the markdown via pandoc.
- No invented data. Missing internal tools stubbed honestly with access-grant path.
- Voice enforcement gate run before write. Zero banned-pattern matches in final output.

---

## What to do with the output

The top 5 items in "Key action items" go to work this week. The "Biggest organic lever" in Section 9 is your focus until the metric it targets moves. Then re-run the audit (quarterly is enough unless there's been a Google or LLM-provider algorithm shift) and the next biggest lever reveals itself.

Want this run for you on a live engagement with a weekly review cadence, a daily dashboard, and the thirty-plus downstream playbooks across every GTM function? Book a call at https://entirecommerce.ai/book-a-call.
