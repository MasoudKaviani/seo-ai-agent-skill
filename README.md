# Persian SEO Skill

A professional, modular AI agent skill for comprehensive SEO analysis and optimization of Persian/Farsi-language websites.

## What This Skill Does

This skill gives AI agents a complete, end-to-end workflow for auditing, analyzing, and optimizing the SEO of Persian-language websites. It covers seven major areas:

1. **Technical SEO Audit** — crawlability, indexability, site architecture, Core Web Vitals, mobile-first readiness, structured data, and security
2. **On-Page SEO** — title tags, meta descriptions, heading structure, content quality, internal linking, and image optimization
3. **Keyword Research** — seed collection, expansion via Persian autocomplete and related searches, intent classification, and SERP feature analysis
4. **Competitor Analysis** — keyword gaps, content gaps, backlink gaps, and SERP feature gaps against SERP competitors
5. **Content Strategy** — topic clusters, content calendars, quality standards, and content pruning
6. **Off-Page SEO** — backlink profile assessment, link-building channels relevant to the Persian web, local SEO, and brand signals
7. **Persian-Specific Checklist** — RTL layout, UTF-8 encoding, hreflang, Persian font performance, ZWNJ usage, Persian numerals/punctuation, and cultural considerations

## Why a Persian-Specific SEO Skill?

Persian-language websites face unique SEO challenges that generic SEO skills don't address:

- **RTL layout** — right-to-left rendering affects layout, navigation, forms, and even Core Web Vitals (font swaps cause layout shift differently in RTL)
- **Persian web fonts** — popular fonts (Vazirmatn, IRANSans, Shabnam) are large and often block rendering, severely impacting LCP
- **ZWNJ (نیم‌فاصله)** — incorrect use of the zero-width non-joiner (U+200C) in compound words is a content quality signal that Persian-aware search algorithms evaluate
- **Character encoding** — Persian-specific characters (گ, چ, پ, ژ) must not be confused with Arabic equivalents
- **Persian search engines** — Yooz and Rismoon serve the Iranian market and require separate submission and analysis
- **Cultural context** — Jalali calendar dates, Toman/Rial currency, Iranian phone formats, and content tone (formal vs. colloquial Persian) all affect user experience and engagement
- **Limited keyword data** — Persian keyword volume and difficulty data is less reliable than English, requiring cross-referencing across multiple sources

## How to Use

### For AI Agent Developers

The skill file is located at:

```
.bolt/skills/persian-seo/SKILL.md
```

Load this skill in your AI agent when the user's request involves SEO for a Persian/Farsi website. The skill triggers on:

- Requests to "audit", "analyze", "improve", or "optimize" SEO for a Persian/Farsi site
- `.ir` domains or sites with Persian primary content
- Persian SEO terms: "سئو", "بهینه‌سازی سایت", "کلمات کلیدی", "رتبه‌بندی"
- Questions about ranking on Google for Persian queries or on Persian search engines

### Inputs

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `url` | string | Yes | Target website URL |
| `keywords` | string[] | No | Target keywords in Persian and/or English |
| `scope` | enum | No | Module(s) to run: `technical`, `on-page`, `keywords`, `competitors`, `content`, `off-page`, `all` (default: `all`) |
| `competitors` | string[] | No | Competitor URLs to analyze |
| `depth` | enum | No | `quick` or `deep` (default: `deep`) |
| `locale` | enum | No | `fa-IR` (default) or `fa-AF` |

### Outputs

The skill produces a structured report with:

- **Executive summary** with top critical issues and quick wins
- **Prioritized action plan** ranked by impact and effort
- **Module-specific findings** with severity tags (Critical / Warning / Good)
- **Persian-specific checklist** with pass/fail for each item

## Skill Structure

```
.bolt/skills/persian-seo/
└── SKILL.md          # The complete skill instructions
```

The `SKILL.md` file contains:

- **Frontmatter** — name and description for skill discovery and activation
- **Inputs/Outputs** — parameter definitions and expected return structure
- **Workflow** — seven phases, each with detailed step-by-step instructions
- **Decision points** — when to escalate to a human or recommend external tools
- **Limitations** — what the skill can and cannot do
- **Output format** — template for the final report
- **Examples** — sample outputs for quick audits and keyword research

## Key Features

### Modular Design

Run the full audit (`scope: all`) or target specific modules:

- Need only a technical check? Use `scope: technical`
- Researching keywords? Use `scope: keywords`
- Analyzing competitors? Use `scope: competitors`

Each module is self-contained and can be called independently.

### Prioritized, Actionable Results

Every finding is classified by:

- **Severity**: Critical / Warning / Good
- **Priority**: P0 (do now) / P1 (do soon) / P2 (do when possible)
- **Effort**: Quick win / Moderate / Heavy lift

This lets the user start with high-impact, low-effort fixes first.

### Persian Language Expertise

The skill encodes deep knowledge of Persian-specific SEO factors:

- Correct ZWNJ usage in compound words (e.g., `می‌رود` not `میرود`)
- Persian numeral consistency (۰۱۲۳۴۵۶۷۸۹)
- Persian punctuation (؟ not ?, ، not ,)
- `lang="fa-IR"` and `dir="rtl"` at the document level
- Persian web font optimization (subsetting, preloading, `font-display: swap`)
- hreflang configuration for multilingual Persian sites
- Jalali calendar dates and Iranian market conventions

### Industry Best Practices

The skill incorporates current SEO best practices including:

- Core Web Vitals targets (LCP < 2.5s, CLS < 0.1, INP < 200ms)
- Mobile-first indexing readiness
- JSON-LD structured data with `inLanguage: "fa-IR"`
- Topic cluster content architecture
- E-E-A-T (Experience, Expertise, Authoritativeness, Trustworthiness) principles
- Schema markup for articles, products, FAQs, breadcrumbs, and local businesses

## External Tools & Resources

The skill recommends these tools for deeper analysis when needed:

| Tool | Purpose |
|------|---------|
| Google Search Console | Indexing status, search queries, CTR |
| Google Analytics 4 | Traffic and user behavior |
| PageSpeed Insights / Lighthouse | Core Web Vitals |
| Ahrefs / Semrush / SE Ranking | Backlink analysis, keyword metrics, rank tracking |
| Google Rich Results Test | Schema validation |
| Yooz (yooz.ir) | Persian search engine data |
| Rismoon (rismoon.com) | Persian search engine data |
| Screaming Frog / Sitebulb | Full-site crawling for large sites |

## License

MIT
