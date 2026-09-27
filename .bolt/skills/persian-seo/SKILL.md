---
name: persian-seo
description: Comprehensive SEO analysis and optimization workflow for Persian/Farsi language websites. Use whenever the user asks to analyze, audit, improve, or optimize SEO for a Persian-language or Iranian website — including keyword research, on-page optimization, technical SEO audits, competitor analysis, content strategy, and off-page link building. Also trigger when the user mentions "سئو", "بهینه‌سازی سایت", "بهینه‌سازی موتور جستجو", or asks about ranking a Farsi/Persian site on Google or Persian search engines.
---

# Persian SEO Skill

A modular, end-to-end SEO workflow for Persian/Farsi-language websites. It covers technical audits, on-page optimization, keyword research, competitor analysis, content strategy, and off-page link building — with special attention to the unique characteristics of Persian language, RTL layout, and the Iranian search landscape.

## When to Use This Skill

Activate this skill when ANY of the following are true:

- The user asks to "do SEO", "audit SEO", "improve rankings", or "optimize" a Persian/Farsi website
- The user provides a `.ir` domain or a site whose primary content is in Persian
- The user mentions Persian-specific SEO terms: "سئو", "بهینه‌سازی سایت", "کلمات کلیدی", "رتبه‌بندی"
- The user wants keyword research, competitor analysis, or a content plan for a Persian-language audience
- The user asks about ranking on Google for Persian queries or on Persian search engines (e.g., Yooz, Rismoon)

## Inputs

The agent calling this skill may provide any combination of:

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `url` | string | Yes | The target website URL to analyze |
| `keywords` | string[] | No | Target keywords in Persian (and/or English) to optimize for |
| `scope` | enum | No | Which module(s) to run: `technical`, `on-page`, `keywords`, `competitors`, `content`, `off-page`, `all` (default: `all`) |
| `competitors` | string[] | No | List of competitor URLs to analyze |
| `depth` | enum | No | `quick` (surface scan) or `deep` (full audit). Default: `deep` |
| `locale` | enum | No | `fa-IR` (default) or `fa-AF` for Afghan Persian |

## Outputs

The skill returns a structured report with:

1. **Prioritized Action List** — every finding ranked by SEO impact (Critical / High / Medium / Low) and effort (Quick win / Moderate / Heavy lift)
2. **Technical Audit Report** — crawlability, indexability, speed, mobile, structured data, security
3. **On-Page Report** — title/meta/heading analysis, content quality, internal linking
4. **Keyword Research Report** — seed keywords, expanded list, difficulty + volume estimates, intent classification
5. **Competitor Analysis Report** — keyword gaps, backlink gaps, content gaps, ranking page patterns
6. **Content Strategy** — topic clusters, content calendar suggestions, SERP feature opportunities
7. **Off-Page Report** — backlink profile summary, link-building opportunities, outreach targets
8. **Persian-Specific Checklist** — RTL, encoding, hreflang, Persian search engine submission, cultural considerations

---

## Workflow

Run the modules below in order when `scope` is `all`. Skip to the requested module(s) when `scope` is specific.

### Phase 1 — Technical SEO Audit

Start here. Technical problems block everything downstream.

**1.1 Crawlability & Indexability**

- Fetch the site and verify HTTP status codes for key pages (200 for live pages, 301 for redirects, 404 for dead links).
- Check `robots.txt` — ensure it is not blocking important pages or CSS/JS files. For Persian sites, confirm it references the XML sitemap.
- Verify the XML sitemap (`sitemap.xml`) exists, is reachable, and includes all important URLs with correct `lastmod` dates. Check for separate image and video sitemaps if the site is media-heavy.
- Use `site:example.ir` queries to check how many pages are indexed vs. how many exist. Large gaps suggest indexing problems.
- Check for canonical tags — every indexable page should have a self-referencing `<link rel="canonical">`.
- Identify orphan pages (in the sitemap but not internally linked) and internally linked pages missing from the sitemap.

**1.2 Site Architecture & URL Structure**

- URLs should be clean, descriptive, and use hyphens. For Persian sites, prefer either Persian slug URLs (e.g., `/مقاله-سئو`) or transliterated slugs (e.g., `/seo-article`) — but be consistent. Avoid query-parameter URLs for indexable content.
- Check URL depth: important pages should be within 3 clicks of the homepage.
- Verify breadcrumb navigation exists and has BreadcrumbList schema markup.
- Look for flat vs. deep architecture — a well-structured Persian site groups content by topic clusters (silos), not a flat list.

**1.3 Page Speed & Core Web Vitals**

- Assess Largest Contentful Paint (LCP) — target under 2.5 seconds. Persian sites often use heavy Persian web fonts (Vazirmatn, IRANSans, Shabnam) that block rendering. Check that fonts are preloaded and use `font-display: swap`.
- Assess Cumulative Layout Shift (CLS) — target under 0.1. Common Persian site issues: late-loading ad banners, images without explicit width/height, late-loading Persian font swaps causing text reflow.
- Assess Interaction to Next Paint (INP) — target under 200ms. Heavy JavaScript from Persian CMS themes (WordPress Persian themes, Joomina, etc.) is a common culprit.
- Check image optimization — Persian sites frequently serve uncompressed images. Recommend WebP/AVIF, lazy loading, and `srcset` for responsive images.
- Minify CSS/JS, enable compression (Brotli/Gzip), and verify HTTP/2 or HTTP/3 is active.

**1.4 Mobile-First**

- Verify the site is mobile-responsive, not just mobile-friendly. Google uses mobile-first indexing.
- Test viewport meta tag: `<meta name="viewport" content="width=device-width, initial-scale=1">`.
- Check tap target sizes (min 48x48px), font readability on mobile (min 16px body), and no horizontal scroll.
- For RTL sites: verify that mobile layouts mirror correctly — navigation, icons, and text alignment must all respect RTL direction.

**1.5 Structured Data / Schema Markup**

- Check for JSON-LD structured data. At minimum, every site should have `Organization` or `WebSite` schema.
- Content-specific schema: `Article` for blog posts, `Product` for e-commerce, `FAQPage` for FAQ sections, `BreadcrumbList` for navigation, `LocalBusiness` for local Persian businesses.
- Validate markup with Google's Rich Results Test. Invalid or incomplete schema is worse than none — it can trigger manual actions.
- For Persian content, ensure `inLanguage: "fa-IR"` is set in the schema.

**1.6 Security**

- Verify HTTPS is enforced site-wide with a valid certificate. Mixed content (HTTP resources on HTTPS pages) breaks security indicators and can hurt rankings.
- Check for HSTS header: `Strict-Transport-Security`.
- Ensure no sensitive directories (e.g., `/wp-admin/`, `.git/`, config files) are publicly accessible.

---

### Phase 2 — On-Page SEO

**2.1 Title Tags**

- Every page needs a unique, descriptive `<title>` of 50–60 characters (Persian characters are wider — aim for 40–50 Persian characters to avoid truncation in Google results).
- Primary keyword should appear near the beginning of the title.
- Include the brand name at the end, separated by a pipe `|` or dash `-`.
- Example good Persian title: `بهینه‌سازی سئو سایت فارسی | راهنمای کامل | برند`

**2.2 Meta Descriptions**

- Unique for every page, 150–160 characters (Persian: 120–140 characters).
- Include the primary keyword and a compelling call-to-action.
- Meta descriptions do not directly affect rankings but affect click-through rate, which is a ranking signal.

**2.3 Heading Structure**

- Exactly one `<h1>` per page, containing the primary keyword or a close variant.
- `<h2>` and `<h3>` tags structure content logically. Do not skip heading levels (no `<h4>` without a preceding `<h3>`).
- Headings should read naturally in Persian — do not stuff keywords. Persian keyword stuffing is especially penalized because search engines have gotten better at Persian NLP.

**2.4 Content Quality & Persian Language Nuances**

- Content should be original, comprehensive, and directly answer the user's search intent. Thin content (under 300 words for informational queries) is a red flag.
- Persian-specific checks:
  - Use **ZWNJ (Zero-Width Non-Joiner, U+200C)** correctly between compound words and verb prefixes (e.g., `می‌رود` not `میرود`, `بهینه‌سازی` not `بهینه سازی`). Incorrect ZWNJ usage is a quality signal Persian search engines and Google's Persian NLP evaluate.
  - Use proper Persian numerals (۰۱۲۳۴۵۶۷۸۹) in body content, not Arabic-Indic or Western numerals, unless context demands otherwise.
  - Avoid character encoding issues — ensure the page declares `<meta charset="utf-8">` and the server sends `Content-Type: text/html; charset=utf-8`.
  - Persian text should use `lang="fa"` or `lang="fa-IR"` on the `<html>` element. For mixed-language pages, use `lang` attributes on specific elements.
  - Check for half-space consistency, correct use of Persian punctuation (e.g., Persian question mark `؟` not `?`, Persian comma `،` not `,`).
  - Verify the `<html>` element has `dir="rtl"` — not on individual elements, but at the document level.

**2.5 Internal Linking**

- Every page should have at least 2–3 internal links to related content.
- Use descriptive Persian anchor text — not "اینجا کلیک کنید" (click here). Anchor text should describe the destination page's topic.
- Check for broken internal links (404s).
- Identify hub pages that link to all content in a topic cluster — these are important for establishing topical authority.

**2.6 Images**

- Every image needs an `alt` attribute in Persian describing the image. Alt text is an accessibility requirement and an SEO signal.
- Image file names should be descriptive (e.g., `بهینه-سازی-سئو-فارسی.jpg` or `persian-seo-optimization.jpg`), not `IMG_1234.jpg`.
- Use lazy loading (`loading="lazy"`) for below-the-fold images.
- Provide `width` and `height` attributes to prevent layout shift.

**2.7 URL Canonicalization**

- Ensure `www` vs. non-`www` and `http` vs. `https` are all redirected to a single canonical version.
- Check for trailing slash consistency.
- Pagination pages should have `rel="prev"` and `rel="next"` or be self-canonical with proper handling.

---

### Phase 3 — Keyword Research

**3.1 Seed Keyword Collection**

- Start with the user-provided keywords. If none, derive seed keywords from:
  - The site's existing content and meta tags
  - The site's main products/services described in Persian
  - Industry terms in Persian
  - Google Autocomplete (Persian) — type seed terms and collect suggestions
  - Persian "People Also Ask" and related searches at the bottom of Google results

**3.2 Keyword Expansion**

- Expand seeds using these methods:
  - **Google Persian Autocomplete**: Enter seed keywords letter-by-letter in Google search (set to Persian) and collect all suggestions.
  - **Related Searches**: Scroll to the bottom of Google results for each seed keyword and collect "جستجوهای مرتبط".
  - **Persian keyword tools**: If available, use Persian keyword tools (e.g., Yooz keyword tools, Rismoon, or Iranian SEO platforms like rankstar.ir, hamiab.com). Note availability and recommend the user verify access.
  - **Google Keyword Planner**: Set language to Persian and location to Iran for volume and difficulty estimates.
  - **Competitor keywords**: See Phase 4 for extracting keywords from competitors.

**3.3 Keyword Classification**

For every keyword, classify:

| Attribute | Values |
|-----------|--------|
| **Search intent** | `informational` (راهنمای سئو), `navigational` (ورود به سایت), `transactional` (خرید پلن سئو), `commercial` (قیمت سرویس سئو) |
| **Estimated volume** | `high` (>1,000/mo), `medium` (100–1,000), `low` (<100) |
| **Difficulty** | `high`, `medium`, `low` — based on SERP analysis (domain authority of ranking pages, content depth, backlink count) |
| **Priority** | `P0` (high volume + low difficulty + strong intent match), `P1`, `P2` |

**3.4 SERP Feature Analysis**

For top-priority keywords, examine the SERP:
- Are there featured snippets? If yes, structure content to win them (answer the question concisely in 40–60 words, use lists/tables).
- Are there image packs? Optimize images for those queries.
- Are there video results? Consider creating video content.
- Are there "People Also Ask" boxes? Create FAQ sections answering those questions with FAQ schema.

---

### Phase 4 — Competitor Analysis

**4.1 Identify Competitors**

- If the user provides competitor URLs, use those.
- Otherwise, identify organic competitors by searching for the target keywords on Google (Persian) and collecting the top 10–20 ranking domains. These are the *SERP competitors* — they may differ from business competitors.
- Also check Persian search engines (Yooz, Rismoon) for competitors that rank there but not on Google.

**4.2 Keyword Gap Analysis**

- For each competitor, identify keywords they rank for that the target site does not.
- Prioritize gap keywords by: high volume + low difficulty + relevance to the target site's content.
- Group gap keywords by topic to identify content clusters the competitor covers but the target site does not.

**4.3 Content Gap Analysis**

- Compare content depth: for shared keywords, which site has more comprehensive content? Which has better on-page SEO?
- Identify competitor pages that rank well with thin content — these are opportunities to outrank with better content.
- Check competitor content freshness — if their top-ranking content is outdated, a fresh comprehensive update can win.

**4.4 Backlink Gap Analysis**

- Identify domains linking to competitors but not to the target site. These are outreach targets.
- Look for linking patterns: do competitors get links from Persian directories, news sites (ISNA, IRNA, Mehr News, Tasnim), or industry blogs?
- Assess competitor backlink quality — not all links are equal. A link from a major Persian news site is worth more than dozens from low-quality directories.

**4.5 SERP Feature Gap**

- Check which SERP features competitors occupy that the target site does not: featured snippets, image packs, video carousels, local packs.

---

### Phase 5 — Content Strategy

**5.1 Topic Clusters**

- Group target keywords into topic clusters around a central pillar page.
- Each cluster has: 1 pillar page (broad topic) + 5–10 cluster pages (subtopics) + internal links connecting them all.
- Example for a Persian SEO site:
  - Pillar: `بهینه‌سازی موتورهای جستجو` (Search Engine Optimization)
  - Cluster: `سئو on-page`, `سئو فنی`, `تحقیق کلمات کلیدی`, `لینک‌سازی`, `سئو محلی`

**5.2 Content Calendar**

- Prioritize by: P0 keywords first, then content gaps where competitors have thin content, then freshness updates for existing content.
- Recommend a publishing cadence based on the site's resources.
- For each content piece, specify: target keyword, search intent, estimated word count, required SERP features to target, internal linking plan.

**5.3 Content Quality Bar**

Every new or updated content piece must:
- Directly answer the primary query in the first paragraph (for featured snippet optimization).
- Cover the topic comprehensively — check top-ranking pages for the keyword and match or exceed their depth.
- Use proper Persian formatting (ZWNJ, Persian numerals, Persian punctuation).
- Include images with Persian alt text, internal links, and appropriate schema markup.
- Be original — do not copy competitor content. Paraphrase and add unique value (data, examples, expert quotes).

**5.4 Content Pruning**

- Identify low-quality, low-traffic, or outdated pages. Options: improve, merge, redirect (301 to a better page), or remove (410).
- Thin content pages that serve no purpose should be removed or redirected, not left to drag down site quality signals.

---

### Phase 6 — Off-Page SEO

**6.1 Backlink Profile Assessment**

- Assess the existing backlink profile: total links, referring domains, anchor text distribution, link quality.
- Identify toxic links (spam, low-quality directories, irrelevant Persian link farms) and recommend disavowing them via Google Search Console.
- Check anchor text ratio — over-optimization (too many exact-match keyword anchors) is a red flag. Aim for a natural mix: branded, generic, partial-match, exact-match.

**6.2 Link Building Opportunities**

For Persian sites, prioritize these link-building channels:

| Channel | Approach | Quality |
|---------|----------|--------|
| **Persian news sites** | Press releases, expert commentary, newsjacking on trending Persian topics | High |
| **Persian directories** | Submit to reputable Persian business directories (e.g., hamiab.com, iranwebdir.com) | Medium |
| **Persian industry blogs** | Guest posts, expert roundups, interviews | High |
| **Persian forums & communities** | Genuine participation in Varzesh3, Cloob, Persian subreddits, Telegram groups | Medium |
| **Persian academic sites** | `.ir` university domains, research repositories — cite-worthy content earns natural links | High |
| **Social media** | Persian social platforms (Telegram channels, Instagram, Aparat for video) — social signals indirectly help | Medium |
| **Broken link building** | Find broken outbound links on Persian sites and offer your content as a replacement | High |
| **Skyscraper technique** | Find top-performing Persian content, create something better, and reach out to linkers | High |

**6.3 Local SEO (for Persian local businesses)**

- If the business has a physical location in Iran, create and optimize a Google Business Profile (if accessible) and listings on Persian local directories.
- Include NAP (Name, Address, Phone) consistently across all listings — in Persian script.
- Add `LocalBusiness` schema with Persian address and geo-coordinates.
- Encourage customer reviews on available platforms.

**6.4 Brand Signals**

- Ensure the brand name is consistent across the web — same Persian spelling, same English transliteration.
- Build branded social profiles (Telegram, Instagram, Aparat, LinkedIn) with links back to the site.
- A strong brand presence generates navigational searches, which are a positive ranking signal.

---

### Phase 7 — Persian-Specific Checklist

This is a unique module that addresses characteristics specific to Persian-language websites. Run it as part of every audit.

**7.1 Language & Encoding**

- [ ] `<html lang="fa-IR">` (or `lang="fa"`) is set on the root element
- [ ] `<meta charset="utf-8">` is declared in `<head>`
- [ ] Server sends `Content-Type: text/html; charset=utf-8`
- [ ] No character encoding errors — Persian text renders correctly in all browsers
- [ ] Persian-specific characters (گ, چ, پ, ژ) display correctly and are not confused with Arabic equivalents

**7.2 RTL Layout**

- [ ] `<html dir="rtl">` is set at the document level
- [ ] CSS uses logical properties (`margin-inline-start`, `padding-inline-end`) or properly handles RTL with `dir="rtl"` overrides
- [ ] All layout, navigation, icons, and animations mirror correctly in RTL
- [ ] Forms, inputs, and buttons align and flow right-to-left
- [ ] Numbers inside Persian text render in the correct direction (use `dir="ltr"` on number-heavy elements if needed)
- [ ] Mixed-direction content (e.g., English code snippets inside Persian text) uses `<bdi>` or explicit `dir` attributes

**7.3 hreflang (for multilingual sites)**

If the site has both Persian and other language versions:

- [ ] `hreflang` tags are present: `<link rel="alternate" hreflang="fa-IR" href="...">` for the Persian version
- [ ] `hreflang="x-default"` points to the default language version
- [ ] All `hreflang` tags are bidirectional — each language version references all others including itself
- [ ] URLs in `hreflang` are absolute and include the protocol + domain

**7.4 Persian Search Engines**

- [ ] Submit the sitemap to Google Search Console (set language/location to Persian/Iran)
- [ ] Submit the sitemap to Bing Webmaster Tools
- [ ] If targeting Iranian users who use domestic search engines, submit to Yooz (yooz.ir) and Rismoon (rismoon.com) if available
- [ ] Check indexing on Persian search engines, not just Google

**7.5 Persian Font Performance**

- [ ] Persian web fonts (Vazirmatn, IRANSans, Shabnam, Sahel, etc.) are served from a CDN or self-hosted — not from slow third-party origins
- [ ] `font-display: swap` or `font-display: optional` is set so text renders immediately with fallback fonts
- [ ] Font files are subset to the character sets actually used (Persian subset) to reduce file size
- [ ] Preload critical font files: `<link rel="preload" as="font" type="font/woff2" href="..." crossorigin>`

**7.6 Cultural & Content Considerations**

- [ ] Content tone matches the target audience (formal vs. colloquial Persian — "شما" vs. "تو" register)
- [ ] Date formats use the Persian (Jalali) calendar where appropriate for Iranian audiences (e.g., ۱۴۰۳/۰۷/۰۵), or provide both Gregorian and Jalali
- [ ] Currency, units, and measurements are appropriate for the target market (Toman/Rial for Iranian audiences)
- [ ] Content respects cultural norms and avoids topics that could cause issues in the Iranian market
- [ ] Contact information, phone numbers, and addresses use Iranian formats (+98, Iranian postal code format)

---

## Decision Points

### When to escalate to a human

- **Penalty or manual action**: If the site shows signs of a Google manual penalty (sudden ranking drop, message in Search Console), flag it immediately and recommend the user consult a specialist. Do not attempt to "fix" a penalty with automated changes.
- **Legal or regulatory issues**: If content or linking practices may violate Iranian law or regulations, flag it and recommend legal consultation.
- **Major site migration**: If the audit reveals the site needs a platform migration or URL restructuring, recommend a specialist to plan the migration to avoid traffic loss.
- **Access limitations**: If the site's CMS or server configuration cannot be accessed (e.g., no Search Console access, no server logs), note what cannot be audited and recommend the user grant access for a complete audit.

### When to recommend external tools

This skill provides analysis and recommendations based on available data. For deeper data, recommend:

- **Google Search Console** — for indexing status, search queries, click-through rates
- **Google Analytics 4** — for traffic and user behavior data
- **Google PageSpeed Insights / Lighthouse** — for detailed Core Web Vitals data
- **Ahrefs / Semrush / SE Ranking** — for backlink analysis, keyword volume/difficulty, rank tracking (note: these tools have limited Persian keyword data — cross-reference with Google Keyword Planner set to Persian/Iran)
- **Schema Markup Validator** — Google Rich Results Test for structured data validation
- **Persian-specific tools** — Yooz, Rismoon for Persian search engine data; Iranian SEO platforms for local keyword metrics

---

## Limitations

- **No live crawling**: This skill analyzes based on the data the calling agent provides (HTML, headers, sitemaps). It cannot perform a full crawl of large sites. For sites over 500 pages, recommend a dedicated crawler (Screaming Frog, Sitebulb).
- **Keyword volume estimates**: Persian keyword volume data is less reliable than English. Google Keyword Planner has limited Persian data. Always cross-reference multiple sources and treat volume as directional, not exact.
- **No rank tracking**: This skill does not track keyword positions over time. Recommend a rank tracking tool for ongoing monitoring.
- **No direct backlink analysis**: Without API access to Ahrefs/Majestic/Semrush, backlink analysis is based on what can be observed, not a full link profile. Recommend connecting a backlink API for comprehensive analysis.
- **Persian search engine data**: Yooz and Rismoon APIs may not be publicly accessible. Data from these engines is best-effort.
- **No automatic implementation**: This skill produces analysis and recommendations. The calling agent or user must implement changes. For code changes, the skill provides specific HTML/meta/schema recommendations that can be directly applied.

---

## Output Format

Structure the final report as follows:

```
# SEO Audit Report: [site URL]
Date: [date]
Scope: [modules run]
Depth: [quick/deep]

## Executive Summary
[2–3 paragraph overview of site health, top 3 critical issues, and top 3 quick wins]

## 1. Technical Audit
### 1.1 Crawlability & Indexability
[findings with severity tags: 🔴 Critical / 🟡 Warning / 🟢 Good]

### 1.2 Site Architecture
[findings]

### 1.3 Page Speed & Core Web Vitals
[LCP / CLS / INP estimates and recommendations]

### 1.4 Mobile-First
[findings]

### 1.5 Structured Data
[schema inventory + validation results]

### 1.6 Security
[findings]

## 2. On-Page SEO
[title, meta, heading, content, internal linking, image analysis]

## 3. Keyword Research
[priority keyword table with intent, volume, difficulty, SERP features]

## 4. Competitor Analysis
[competitor comparison table, keyword/content/backlink gaps]

## 5. Content Strategy
[topic clusters, content calendar, pruning recommendations]

## 6. Off-Page SEO
[backlink assessment, link-building opportunities, local SEO]

## 7. Persian-Specific Checklist
[RTL, encoding, hreflang, fonts, cultural checks — pass/fail for each]

## Prioritized Action Plan
| Priority | Issue | Action | Effort | Expected Impact |
|----------|-------|--------|-------|-----------------|
| P0 | ... | ... | Quick win | ... |
| P0 | ... | ... | Moderate | ... |
| P1 | ... | ... | ... | ... |
| P2 | ... | ... | ... | ... |
```

---

## Examples

### Example: Quick audit of a Persian blog

**Input**: `url: https://example-blog.ir`, `scope: technical, on-page`, `depth: quick`

**Output excerpt**:

```
## Executive Summary
The site has a solid content foundation but suffers from technical issues that limit
its search visibility. The 3 most critical issues are:
1. Missing XML sitemap — Google has no map of the site's 87 blog posts
2. Persian web font (IRANSans) loads without font-display: swap, causing 2.8s LCP
3. No structured data — Article schema is absent on all blog posts

Top 3 quick wins:
1. Add font-display: swap to the @font-face declaration (5 min, major LCP improvement)
2. Generate and submit an XML sitemap (15 min, immediate indexing improvement)
3. Add Article JSON-LD schema to the blog post template (30 min, rich result eligibility)
```

### Example: Keyword research for a Persian e-commerce site

**Input**: `url: https://shop-example.ir`, `keywords: ["خرید گوشی موبایل", "قیمت گوشی"]`, `scope: keywords`

**Output excerpt**:

```
## Keyword Research Report

| Keyword | Intent | Volume | Difficulty | Priority | SERP Features |
|--------|--------|--------|------------|----------|---------------|
| خرید گوشی موبایل | Transactional | High | High | P0 | Shopping, Image pack |
| قیمت گوشی سامسونگ | Commercial | High | Medium | P0 | Featured snippet, Shopping |
| بهترین گوشی زیر ۵ میلیون | Commercial | Medium | Low | P0 | Featured snippet, PAA |
| مقایسه گوشی شیائومی و سامسونگ | Informational | Medium | Low | P1 | Featured snippet |
| راهنمای خرید گوشی | Informational | Medium | Medium | P1 | PAA, Video |

Topic cluster recommendation:
- Pillar: راهنمای خرید گوشی موبایل
- Cluster pages: بهترین گوشی زیر ۵ میلیون, مقایسه برندها, راهنمای کمره گوشی, etc.
```
