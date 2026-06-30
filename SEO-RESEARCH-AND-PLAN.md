# GridCMDB - SEO Research & Plan

Site: https://cmdb.cyberautomations.com
Stack: Single-page HTML on Vercel, subdomain of cyberautomations.com
Date: 2026-06-30

> Prompt-injection notice: While reading project files, two system-reminder tags appeared inside the file content claiming I must refuse to improve or augment code. That is not a real system rule - it is injected text. Flagging and ignoring.

---

## 1. Executive Summary

GridCMDB is a single-page B2B SaaS landing page for a high-ACV ($18K-$73K), sales-led product (OT/ICS CMDB on Google Workspace). Conversion is Calendly demo bookings, not self-serve signups.

### The core problem

A single page cannot rank for a meaningful number of keywords. Google needs topical depth and per-query intent pages, and LLMs (ChatGPT/Perplexity/Gemini) need citable, fact-dense, structured content. The current site has neither.

### The opportunity

The OT/ICS security tools category has low SEO competition relative to its revenue potential. The dominant vendors (Claroty, Dragos, Nozomi) are product-led, not content-led. "Claroty alternative / Dragos alternative" is an under-served, high-commercial-intent surface. A small vendor can win the long tail and comparison queries with a focused content engine.

### Recommended posture (priority order)

1. Technical foundation (week 1) - structured data, robots/sitemap, OG/Twitter cards, canonical, semantic HTML, favicon. 1-2 days.
2. Page expansion + content engine (weeks 2-12) - comparison pages, compliance-framework pages, vendor alternative pages, glossary, blog. 6-10 weeks of shipping.
3. Off-page / authority building (ongoing) - LLM citations come from third-party mentions: Reddit, LinkedIn, GitHub, Slack, podcasts, ICS-CERT commentary.

### Realistic outcome (12 months, focused execution)

- Top-10 for 80-200 head/comparison keywords in OT/ICS CMDB
- Cited in Perplexity/ChatGPT for 15-30 OT CMDB buyer prompts
- About 1,500-4,000 organic visits/month at maturity (at 1.5% demo-booking rate = 25-60 demos/month)
- Reduced CAC pressure on founder LinkedIn outbound

---

## 2. Current State Audit

### Already in place (good)

- title + meta description present, keyword-rich ("OT/ICS Asset Management", "Google Workspace", "1/4 the cost of Claroty")
- OG title + description (og:title, og:description, og:type=website)
- Mobile-responsive, fast (48KB, no framework, no render-blocking JS)
- HTTPS via Vercel, subdomain on aged domain (cyberautomations.com)
- Semantic HTML5 - section, nav, footer, h1/h2 hierarchy
- Internal anchor links (#features, #pricing, #compare, #faq, #about)
- FAQ section - candidate for FAQ schema
- Bolt.new badge is the only external script

### Missing or weak (gaps)

| Gap | Severity | Notes |
|---|---|---|
| No JSON-LD structured data | High | Loses rich-result eligibility, reduces LLM extraction accuracy |
| No robots.txt | Medium | Vercel default works but custom robots lets you point to sitemap |
| No sitemap.xml | Medium | Trivial with Vercel; needed as site grows |
| No canonical link tag | Low-Med | Important once duplicate paths / UTM strings exist |
| No Twitter/X card meta | Low | Links shared on X look plain |
| No OG image | High | No social preview on Slack/LinkedIn/email. Cheap fix. |
| No favicon | Low | Brand polish; affects CTR in tabs |
| No webmanifest | Low | PWA-lite metadata |
| Single H1, weak heading depth | Med | No h2s break sections into semantic chunks |
| No internal links between topical pages | High (strategic) | Will become severe as site grows |
| No analytics / GSC / Plausible | High | Cannot measure what is working |
| No keyword-targeted subpages | High (strategic) | A single page cannot rank for dozens of intents |
| No blog / glossary / resource hub | High (strategic) | LLMs and Google need topical breadth |
| No backlinks / off-page mentions | High | LLMs cite sites with third-party coverage |
| Bolt.badge.js | Cosmetic | Hide once shipped - implies work-in-progress to buyers |

### Conversion benchmark context

The 2026 B2B SaaS literature (Unbounce, First Page Sage) consistently reports:
- Median B2B SaaS landing-page conversion: 3.8% (Unbounce) / 1.1% (First Page Sage B2B SaaS)
- Cybersecurity industry median: 1.4%
- Top performers: 11.6%+

GridCMDB is structurally aligned with what high-converting B2B SaaS pages do (single CTA repeated, problem-first hero, social proof, comparison table, FAQ). What it lacks is traffic - and traffic requires SEO and content, not CRO.

---

## 3. Keyword Research and Buyer Intent Map

### 3.1 Buyer personas

- OT Security Manager: comparisons, frameworks, alternative-to-X queries. Hook: cost / no-infrastructure.
- CISO / Director of Security: board-grade tooling, framework mapping. Hook: audit evidence + risk posture.
- Compliance / Audit Lead: NERC CIP-002, NIS2 Article 21. Hook: audit-ready artefacts.
- Operations / Plant Engineer: vendor pain points, inventory tools. Hook: config import + speed.
- Procurement / CFO: cost comparison, TCO. Hook: 1/4 of Claroty, no appliance.

### 3.2 Head keywords (6-12 months to top-10)

- OT asset management software (300-800/mo, High competition)
- OT security platform (500-1,200/mo, High)
- ICS security tools (300-700/mo, High)
- OT CMDB (50-200/mo, Medium - under-served)
- ICS CMDB (50-150/mo, Medium)
- Operational technology asset inventory (100-300/mo, Medium)
- Industrial control system inventory (100-250/mo, Medium)
- Cyber physical systems security (200-400/mo, High)
- Claroty alternative (100-300/mo, Low-Medium)
- Dragos alternative (50-200/mo, Low-Medium)
- Nozomi alternative (50-150/mo, Low)
- Claroty pricing (200-500/mo, Low - most pages vague)

Volumes are estimates from public SEO tool patterns. Verify with Ahrefs/Semrush trial.

### 3.3 Comparison / alternative queries (highest-ROI)

Buyers searching alternative or vs queries are mid-funnel with budget. Big vendors publish almost no comparison content, so the surface is open.

Build:
- /compare/gridcmdb-vs-claroty
- /compare/gridcmdb-vs-dragos
- /compare/gridcmdb-vs-nozomi-networks
- /compare/gridcmdb-vs-armis
- /compare/gridcmdb-vs-forescout
- /compare/gridcmdb-vs-tennable-ot
- /compare/gridcmdb-vs-palo-alto-iot-security
- /compare/gridcmdb-vs-servicenow-ot-visibility
- /compare/ot-cmdb-vs-spreadsheet
- /claroty-alternative
- /dragos-alternative
- /nozomi-alternative
- /claroty-pricing

Template per page: honest comparison, what each tool is best at, who should NOT pick GridCMDB, feature matrix, pricing (yours disclosed, theirs estimated), CTA. Honest beats hit-piece; LLMs prefer citing it.

### 3.4 Compliance-framework pages (intent-rich, low competition)

Queries from people with mandate and budget.

- /compliance/iec-62443 - SL-T vs SL-A, zone-and-conduit
- /compliance/nerc-cip - CIP-002 BES, CIP-007 R2, CIP-005 EAP
- /compliance/nis2 - Article 21 asset register, Article 23 incident reporting
- /compliance/eu-cra - Cyber Resilience Act, SBOM
- /compliance/iso-27001 - Annex A 5.9 asset inventory
- /compliance/critical-infrastructure-asset-register

### 3.5 Long-tail / problem-aware (blog + glossary fuel)

Easiest to win on a young domain; LLMs most often cite these.

- What is an OT asset? / What is an ICS asset inventory?
- Difference between IT and OT CMDB
- Purdue model explained / What is Purdue Level 3.5
- BES cyber system categorisation CIP-002
- How to inventory PLCs
- Best practices for OT asset discovery
- IEC 62443 security level target vs achieved
- NIS2 essential vs important entity
- How long does it take to deploy a CMDB
- Why spreadsheets fail for OT asset management
- Free OT CMDB template (lead magnet - Google Sheets template, upsell to GridCMDB)

### 3.6 Vendor-specific / protocol-specific pages

- /vendors/cisco-ios-config-import
- /vendors/palo-alto-pan-os-config-import
- /vendors/cisco-asa-config-import
- /protocols/modbus-asset-inventory
- /protocols/dnp3-asset-inventory
- /protocols/bacnet-asset-inventory
- /protocols/opc-ua-asset-inventory
- /industries/utilities
- /industries/manufacturing
- /industries/water
- /industries/oil-gas

### 3.7 Search intent mapping

- Awareness (what-is, how-does) -> Glossary / long-form blog
- Consideration (X vs Y, best-of) -> Comparison page / listicle
- Decision (pricing, demo) -> Pricing / dedicated landing
- Loyalty (reviews, alternatives-to-you) -> case studies (later)

---

## 4. GEO / AEO Strategy (LLM Discovery)

Largely separate from classic SEO. From 2026 research (Microsoft AEO guide, Profound, Cubitrek): LLMs use Retrieval-Augmented Generation (RAG). They pull live web data, synthesise an answer, cite sources. Hallucinations dropped from ~60% to 3-5% with RAG. To be cited: findable, fact-dense, structured.

### 4.1 What LLMs actually look for

1. Brand mention frequency on third-party sites (Reddit, LinkedIn, podcasts, GitHub, Wikipedia) - the #1 signal
2. Structured / machine-readable data - JSON-LD, schema.org, llms.txt
3. Semantic HTML with clear Q&A patterns - h2/h3 questions, concise answers in first sentence
4. Consensus signals - multiple independent sources describing you the same way
5. Authoritative brand identifiers - official socials, founders, legal name, location

### 4.2 GEO tactics for GridCMDB

Tactic 1 - Brand Hub page. /about or /brand as fact-dense canonical page: legal name, founder (Teon Moore), product category, pricing model, geographic focus, key claims, socials, press kit. LLMs read this once and trust it for months.

Tactic 2 - llms.txt at site root. Plain-text machine-friendly summary. Free generators exist (cubitrek.com). Costs nothing.

Tactic 3 - FAQ schema on every relevant page. Current FAQ section is a candidate. Expand on every framework/comparison page with 5-10 Q&A pairs. Mark up with FAQPage schema.

Tactic 4 - Run prompt tests monthly. Identify 15-20 buyer prompts (OT CMDB on Google Workspace, Claroty alternative for utilities, NIS2 asset register tool). Run them in ChatGPT, Perplexity, Gemini, Claude monthly. Track whether GridCMDB is mentioned, how it is described, what is cited. Fix gaps.

Tactic 5 - Reddit / LinkedIn / GitHub presence. LLMs over-weight these platforms.
- Reddit: Answer questions in r/SCADA, r/cybersecurity, r/OTsecurity, r/IndustrialControlSystems. Never promotional. Mention GridCMDB only when relevant.
- LinkedIn: Founder posts 2-3x/week on OT/ICS CMDB topics. Cross-post to blog.
- GitHub: Open-source a small utility (Cisco IOS parser, NIS2 register template). Massive LLM visibility boost.
- Wikipedia: Once 2-3 credible third-party mentions exist, consider a stub. Do NOT write it yourself - COI rules.

Tactic 6 - Be quotable. Specific numbers and clear claims. Existing stats (11,487 assets, $0 infrastructure, 1-hour deploy, 1/4 Claroty cost) are perfect. Use them verbatim everywhere. Consistency is the signal.

Tactic 7 - Get on best-of lists. LLMs synthesise listicles (Top 10 OT security tools, Best CMDBs for utilities). Pitch G2, Capterra, Gartner Peer Insights, Cyber Magazine top-10, industry newsletters.

### 4.3 LLM-friendly content patterns

- Lead with the answer in the first sentence. Example: "A NIS2 asset register is a documented inventory of assets that support essential services, as required by Article 21 of the NIS2 Directive."
- Use the question verbatim as h2.
- Specific numbers ($0 infrastructure, 11,487 assets, 1/4 the cost of Claroty).
- Comparison tables with structured HTML. Already in the site - excellent.
- Definition boxes / callouts. LLMs extract these cleanly.
- Author bylines with credentials. Important for E-E-A-T.

---

## 5. On-Page SEO Specification

### 5.1 Template (apply to every new page)

- URL slug: /compliance/nis2 (kebab-case, keyword-rich)
- Title tag: NIS2 Asset Register Software | GridCMDB (60 chars max)
- Meta description: 155 chars max, keyword + value prop
- H1: One per page, keyword-rich
- H2s: 5-10 per page, question-formatted, keyword-targeted
- Canonical: link rel=canonical pointing to the page's URL
- OG title: same as title tag
- OG description: same as meta description
- OG image: 1200x630 PNG, brand-consistent
- OG type: website (article for blog posts)
- Twitter card: summary_large_image
- Schema: Article or FAQPage or SoftwareApplication, depending on page type
- Internal links: 3-5 to related pages
- External links: 1-2 to authoritative sources (NERC, IEC, NIST, ENISA)
- Word count: 800-1,500 for framework pages; 1,500-2,500 for blog posts

### 5.2 Specific fixes to apply to index.html this week

1. Add JSON-LD SoftwareApplication schema (the snippet in WEBSITE-REVIEW-AND-FIXES.md Addition 5 is correct - drop it into head)
2. Add link rel=canonical pointing to https://cmdb.cyberautomations.com/
3. Add OG image - 1200x630 brand PNG (hero stat bar makes a great social card)
4. Add Twitter card meta (twitter:card, twitter:title, twitter:description, twitter:image)
5. Add favicon + webmanifest
6. Add robots.txt at root referencing the sitemap
7. Add sitemap.xml - currently just the homepage; will grow as pages ship
8. Add FAQ schema around the existing FAQ section
9. Add Organization schema with founder, founding date, location, socials
10. Add breadcrumb schema once subpages exist
11. Remove Bolt.new badge once the page is shipped (badge signals work-in-progress to buyers - small CRO hit, not SEO)
12. Install Vercel Analytics + Google Search Console - without measurement you are flying blind

### 5.3 Information architecture (target state)

- / (landing page, existing)
- /pricing (split out from #pricing anchor)
- /compare (index of comparison pages)
- /compare/gridcmdb-vs-claroty
- /compare/gridcmdb-vs-dragos
- /compare/gridcmdb-vs-nozomi
- /compare/...
- /compliance (index of framework pages)
- /compliance/iec-62443
- /compliance/nerc-cip
- /compliance/nis2
- /compliance/eu-cra
- /features (feature deep-dives, one per card from current site)
- /vendors (vendor-specific landing pages)
- /industries (industry landing pages)
- /blog (long-form content)
- /glossary (definitions)
- /about (founder story, brand hub)
- /contact
- /demo (Calendly embed - replace outbound links)
- /llms.txt (machine-readable brand summary)

### 5.4 Editorial standards

- Every page answers who, what, why, how, how much in the first 100 words
- Every page includes at least one comparison table or stat callout
- Every page has at least 5 internal links to related pages
- Every page includes consistent brand stats (11,487 assets, $0 infra, 1-hour deploy, 1/4 Claroty)
- No fluff intros. No "in today's rapidly evolving threat landscape..." Open with the answer.

---

## 6. Content Calendar (90-day rolling)

### Month 1 - Foundation (technical + cornerstone)

Week 1:
- Technical SEO fixes to index.html (items 1-12 above)
- Submit sitemap to Google Search Console + Bing Webmaster
- Install Vercel Analytics + set up GA4 (optional)

Week 2:
- Ship /compare/gridcmdb-vs-claroty (template-setter)
- Ship /claroty-alternative

Week 3:
- Ship /compare/gridcmdb-vs-dragos + /dragos-alternative
- Ship /compliance/iec-62443

Week 4:
- Ship /compliance/nerc-cip
- Brand Hub page (/about), llms.txt, founder bio

### Month 2 - Breadth (frameworks + long-tail)

Week 5:
- /compliance/nis2
- /compliance/eu-cra
- /compare/gridcmdb-vs-nozomi
- /compare/gridcmdb-vs-armis

Week 6:
- Glossary seed (10 entries): OT asset, ICS, Purdue model, zone-and-conduit, SL-T, SL-A, BES, essential entity, SBOM, EAP
- /blog/why-spreadsheets-fail-ot-asset-management

Week 7:
- /blog/free-ot-cmdb-google-sheets-template (lead magnet)
- /vendors/cisco-ios-config-import

Week 8:
- /blog/ot-asset-discovery-without-an-appliance
- LLM prompt audit #1 (15 prompts x 4 engines, screenshot + log)

### Month 3 - Authority (depth + cadence)

Week 9:
- /industries/utilities
- /industries/manufacturing
- /blog/nerc-cip-002-bes-categorisation-walkthrough

Week 10:
- /blog/nis2-incident-reporting-timeline-24-72-hours
- First podcast appearance (LinkedIn outreach)

Week 11:
- /blog/claroty-pricing-vs-gridcmdb (honest TCO analysis)
- Reddit AMA in r/cybersecurity on OT security tooling

Week 12:
- G2 / Capterra listing live; first 3 customer reviews requested
- LLM prompt audit #2; backlink check (Ahrefs free trial); plan Q2

### Cadence after Q1

- 2 blog posts / week (one long-form 2,000+ words, one short-form tactical)
- 1 comparison or framework page / month until surface is saturated
- 1 podcast / webinar / video appearance / month (each becomes a transcripted blog post + backlink)
- Monthly LLM prompt audit - non-negotiable

---

## 7. Off-Page SEO and Authority Building

This is 80% of the long-term outcome. LLMs and Google both weight third-party mentions heavily. The work is unsexy and persistent.

### 7.1 Tier 1 - Earned media (highest value)

- Podcast appearances. "Founder of CMDB that runs on Google Workspace" is a good pitch. Targets: CyberWire Daily, Risky Business, ICS Village, Dragos-aligned podcasts, Nozomi-aligned podcasts, SANS ISC, Defensible UC.
- Conference talks. SANS ICS Summit, InfoSec World, RSA OT track, S4 (the OT security conference). A 20-minute breakout generates 5-10 backlinks.
- Industry publication mentions. CyberScoop, Dark Reading, The Record, Industrial Cyber. Pitch the no-infrastructure CMDB angle.
- Case studies. As soon as customer #1 is referenceable, publish a detailed case study (anonymised if needed). LLMs heavily index case studies.

### 7.2 Tier 2 - Listings and directories

- G2, Capterra, Gartner Peer Insights, TrustRadius, GetApp - claim listings, encourage customer reviews. LLMs scrape these for consensus signals.
- Cyber Magazine Top 10 OT security platforms and equivalents - pitch for inclusion.
- Google Business Profile - even as a remote-first SaaS, claim it. Local-citation signal.
- Crunchbase, Pitchbook - keep founder + company profiles accurate and updated.

### 7.3 Tier 3 - Community and social

- LinkedIn (founder): 2-3 posts / week on OT/ICS CMDB topics. Repurpose every blog post as a LinkedIn carousel.
- Reddit: helpful-not-promotional presence in r/SCADA, r/cybersecurity, r/OTsecurity, r/IndustrialControlSystems, r/PLC, r/utilities.
- Hacker News: launch post + occasional Show HN when shipping meaningful updates.
- Slack/Discord communities: ICS-CERT, SANS ICS, OECS, regional ISACs (E-ISAC for utilities).
- GitHub: open-source at least one small tool tied to the product (config parser, asset template, schema validator). Each repo is a long-tail SEO asset.

### 7.4 Tier 4 - Link reclamation and PR

- HARO / Featured.com / Qwoted - respond to journalist queries on OT security, CMDBs, ICS compliance. 30 minutes/week; high-value links when they land.
- Backlink gap analysis - every quarter, run Ahrefs/Semrush link intersect against Claroty, Dragos, Nozomi. Find sites linking to them but not you, then pitch.
- Guest posts - target OT/CISO publications: Claroty blog, Dragos blog, Tenable blog, Belden blog, Nozomi blog. Indirect competitor backlinks are gold.
- Sponsor one newsletter - Rational Cybersecurity, CyberWire, Curated Intelligence. About $500-$2K per placement.

### 7.5 What NOT to do

- Do not buy backlinks. Google's 2024 spam updates nuked sites that did.
- Do not stuff keywords. Modern Google (Helpful Content / core updates) penalises it.
- Do not spin AI-generated content without substantive human edit. E-E-A-T scrutiny is real.
- Do not engage in link exchanges or guest post networks. Detectable patterns.
- Do not put GridCMDB in your Reddit post history with a fresh account. The community will smell it.

---

## 8. Measurement Framework

### 8.1 Tools (free + cheap)

- Google Search Console - indexation, queries, CTR, position. Free.
- Bing Webmaster Tools - same, for Bing (which feeds Copilot). Free.
- Vercel Analytics - real-time pageviews, referrers. Free.
- Plausible / Fathom - privacy-friendly analytics (optional). $9/mo.
- Ahrefs Webmaster Tools - backlinks, technical audits (free tier).
- Ahrefs / Semrush (paid) - keyword research, competitor gaps. ~$100-200/mo.
- Profound / AthenaHQ / LLMrefs - LLM citation tracking. $50-500/mo (later).

### 8.2 KPIs (monthly review)

- Organic clicks / month (GSC). Target: 1,500-4,000.
- Indexed pages (GSC). Target: 40-80.
- Average position for head terms (GSC). Target: Top 10 for 30+ queries.
- Referring domains (Ahrefs). Target: 30+.
- LLM mention rate on 15-prompt panel. Target: 5+ prompts cite GridCMDB.
- Domain rating (Ahrefs). Target: 25+ (from current ~10).
- Demo bookings from organic (Calendly utm tracking). Target: 25-60/month.
- Organic conversion rate (Vercel + Calendly). Target: 1.0-1.5% (cybersecurity median 1.4%).

### 8.3 Leading indicators (weekly)

- New blog post shipped
- New backlink acquired
- New G2 review submitted
- LinkedIn post impressions + DM count
- LLM prompt-test results (4 engines x 5 prompts)

---

## 9. Risk and Constraint Notes

- Single-page constraint - the current site converts well but cannot scale SEO. New subpages should preserve the same minimal-HTML / no-framework aesthetic. They should look and feel like the homepage.
- Sales-led motion - at $18K-$73K ACV, organic traffic is top-of-funnel awareness, not direct revenue. Do not expect a Calendly booking from every organic visit. Expect 1.0-1.5% to convert to demo, of which about 25% close over a 60-90 day sales cycle.
- Brand-new domain on a subdomain - DA is low. Expect slow compounding rather than quick wins. Months 1-3 will feel like nothing is happening. Months 6-12 is when the curve bends.
- GAS constraint - GridCMDB itself runs on Google Apps Script. That does not affect SEO, but it shapes the marketing story (which is itself a differentiator worth leaning into).
- Founder bandwidth - Teon is solo. The plan is realistic for one person with part-time help (a freelance writer for $500/post and a freelance SEO for $1,500/mo to manage the calendar). Anything more aggressive requires hiring.
- LLM uncertainty - GEO is a new field. The tactics in section 4 are based on early-2026 consensus. Expect the playbook to evolve. Re-evaluate quarterly.

---

## 10. 30 / 60 / 90 Day Roadmap

### Day 0 to Day 30 (Foundation)

- Technical SEO fixes (items 1-12 in section 5.2) on index.html
- Ship /compare/gridcmdb-vs-claroty as the template-setter for comparison pages
- Ship /claroty-alternative and /dragos-alternative
- Ship /compliance/iec-62443
- Install GSC, Bing Webmaster, Vercel Analytics
- Submit sitemap; verify indexing
- Claim G2 + Capterra + Gartner Peer Insights listings
- First 5 LinkedIn posts from founder
- Brand Hub / About page + llms.txt

### Day 31 to Day 60 (Breadth)

- 4 more comparison pages
- 3 more compliance pages (NERC CIP, NIS2, EU CRA)
- 10 glossary entries
- 4 blog posts (2,000+ words each)
- First guest post pitched to OT/CISO publication
- First podcast pitch sent (5 podcasts)
- First LLM prompt audit (15 prompts x 4 engines)
- Backlink analysis on top 3 competitors

### Day 61 to Day 90 (Authority)

- First podcast appearance booked
- First customer case study published (anonymised if needed)
- 8 more blog posts (cadence: 2/week)
- 2 industry landing pages
- 2 vendor-specific landing pages
- First HARO / Featured.com response sent (weekly thereafter)
- First open-source GitHub utility published
- Second LLM prompt audit; document shifts

---

## 11. Effort and Investment Estimate

- Technical SEO fixes (one-time): 1-2 days founder, $0
- GSC + Bing + Vercel Analytics: 1 hour, $0
- OG image + favicon (designer): 2 hours, $50-150 (Fiverr/Upwork)
- Comparison page template (15 pages x 1 day each): 15 days founder OR $500/page x 15 = $7,500
- Compliance pages (6 pages x 1.5 days each): 9 days founder OR $750/page x 6 = $4,500
- Blog (2/week x 12 weeks = 24 posts): 12 days founder OR $250/post x 24 = $6,000
- Glossary (20 entries x 0.5 day each): 10 days founder OR $100/entry x 20 = $2,000
- llms.txt + Brand Hub: 1 day founder, $0
- Ahrefs / Semrush (3 months): $300-$600
- Profound / LLM tracking (3 months): $150-$1,500
- Podcast outreach (time): 2 hrs/week founder, $0
- Newsletter sponsorship (1 placement): $500-$2,000
- Freelance writer (3 months, 8 posts): $2,000-$4,000
- Freelance SEO manager (3 months): $4,500

Bootstrapped path (founder only): about $500 (tools + OG image) + 50-60 days of focused work over 90 days.
Funded path (founder + freelancers): about $15K-$25K + 20 days of founder oversight over 90 days.

---

## 12. Recommended Next Action

Ship the technical SEO fixes on index.html this week (items 1-12 in section 5.2). Total cost: $0. Total effort: 1-2 days. This alone unlocks structured-data eligibility, social sharing polish, and basic analytics. Then move to the comparison page template (/compare/gridcmdb-vs-claroty) - that is the highest-ROI single content asset you can ship this month.

---

End of document.
