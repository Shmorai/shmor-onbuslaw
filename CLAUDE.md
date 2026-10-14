# OnBusLaw (onbuslaw.shmor.ai)

A Shmor marketplace (shared rules in `../../CLAUDE.md`): its own brand, design and SEO. "Online business law, explained": free plain-English legal information for online shoppers, sellers and creators in the US, UK and EU: consumer rights, refunds and returns, chargebacks, scams and identity theft, trademarks, copyright, affiliate/influencer disclosure rules, website legal pages, marketplace selling and customer-service complaints. Repo: `Shmorai/shmor-onbuslaw` (private until launch). Status: **building**, with no referral links yet.

## Where things are
| What | Where |
|---|---|
| Card on shmor.ai, search keywords, **referral links**, offers, SEO defaults | `shmor-site.json` |
| Pages (1 JSON file = 1 Google landing page) | `content/` (`home.json` = homepage, `content/blog/x.json` → `/blog/x/`) |
| Design: top bar, header, logo, footer (with the legal-information notice) | `templates/layout.html` |
| Design: styles | `assets/site.css` (kit defaults at the top; **OnBusLaw theme** block at the bottom) |
| Generated output (don't edit by hand) | `index.html`, `*/index.html`, `sitemap.xml`, `robots.txt`, `404.html`, `search/`, `search-index.json`, `blog/feed.xml` |

## Pages (19)
Home · editorial-standards (footer + byline link; not in menu) · consumer-rights · refunds-and-returns · chargebacks · online-scams · identity-theft · complaints · trademarks · copyright-and-takedowns · affiliate-disclosure-rules · online-business-legal-checklist · website-terms-and-privacy · selling-on-marketplaces · blog (+4 posts: EU withdrawal button, cancelling subscriptions, Action Fraud → Report Fraud, spotting fake online shops).
Top menu = pages with `navOrder` (Your rights, Refunds, Scams, Trademarks, Affiliates, Business, Blog, Complaints [mobile/tablet only; desktop shows the navy "Resolve a dispute" header button instead]). The menu collapses to the hamburger below 1080px.
**Home blocks:** trust strip → What do you need help with? (9 photo tiles) → Key rules at a glance (8 white cards on a navy band, each tagged US / UK / EU) → Sorting out a problem (3 steps) → Why people use OnBusLaw (§-numbered) → latest posts → Popular questions → guide text → FAQ (visual order set with CSS `order`).

## Design
"Counsel" (created 2026-10-14): light law-library look. Ivory pages #FBFAF7, parchment bands #F4F1EA, lines #E3DED2, deep navy #0F1E3A (ink, top bar, bands, footer #0A152B), brass gold #B8892F (rules/icons) with #85601C for gold text on light and #D4B06A on navy, link blue #1E3D7B. Source Serif 4 headings + Inter body; eyebrows are small caps with a gold rule. Logo = gold balance-scales line icon in a navy rounded square + "OnBus*Law*" (Law in gold) + tagline "Online business law, explained" + "by Shmor.ai" pill. Top bar states "General information, not legal advice"; every guide ends with a gold-ruled note saying the same, and the footer has a full legal-information notice. Home hero = gavel-on-keyboard photo under a navy gradient, white search box with gold button, US/UK/EU badges. Tables have navy header rows and scroll inside their box on phones. Checked at 375px on all page types (no horizontal scroll).
**Photos:** every page has a free-licence Unsplash `"image"` with verified photographer credits. To change one, swap `src`/`credit`/`creditUrl` and rebuild.

## Content rules
General legal **information, never advice**; OnBusLaw is not a law firm. Factual and evergreen: no invented fees, case outcomes, statistics or reviews; don't quote official fees (they change). Each guide covers US (federal, state differences flagged), UK (Scotland/NI differences noted) and EU side by side, says "as of October 2026" where time-sensitive, and lists official `"sources"` (all checked live 2026-10-14). Time-sensitive facts to re-check: UK DMCC subscription regime (expected spring 2027 at the earliest), FTC negative option rulemaking after the July 2025 click-to-cancel vacatur, UK Report Fraud service, APP reimbursement cap (£85,000), UK VAT threshold (£90,000), Data (Use and Access) Act 2025 cookie exemptions.

## People, bylines and legal review
**Never invent staff, authors, reviewers or credentials** (fake lawyers are deceptive and, in the UK, an offence). Only real, consenting people with verifiable details go in `shmor-site.json` → `"people"`:
```json
"people": { "jsmith": { "name": "Jane Smith", "role": "Legal reviewer", "credentials": "Solicitor (England & Wales)",
  "bio": "…", "image": "https://…", "registry": { "label": "SRA register: 123456", "url": "https://…" }, "sameAs": ["https://www.linkedin.com/in/…"] } }
```
Then on a page: `"reviewedBy": "jsmith", "reviewed": "YYYY-MM-DD"` (and/or `"writtenBy"`). This adds "Reviewed by Jane Smith, Solicitor…, date" to the byline, `reviewedBy`/`lastReviewed` (or a Person `author`) to JSON-LD, and a profile card (anchor `#person-<id>`) on `/editorial-standards/`. The "Our writers and legal reviewers" section stays hidden while `people` is empty.
Every guide page (not home/blog/posts) shows a byline bar under the hero (`seo.bylines`): "Written by the OnBusLaw editorial team · Fact-checked against official sources (or Reviewed by …) · Updated date · How we write our guides". The editorial standards page says unreviewed guides are fact-checked by the editorial team but not lawyer-reviewed, and discloses AI-assisted drafting; keep those statements true.

## Commands (run here)
```bash
node tools/build.js           # rebuild after ANY change to content/, templates/ or shmor-site.json
node tools/build.js --check   # validate only
node tools/serve.js 4008      # preview http://localhost:4008  (preview config "onbuslaw")
```
After changing `shmor-site.json` (links, keywords, card), also run `node tools/sync-network.js` in `../../shmor-ai`.

## Adding referral links
1. Add to `shmor-site.json` → `"links"`: `"slug": { "merchant", "network": "awin|cj|impact|…", "url": "https://…" }` (or `"url": { "us", "uk", "eu" }`). Prefix slugs with the merchant name.
2. Show it on pages: add the slug to a page's `"partners": [...]`, or add an `"offers"` entry (`"pages": ["slug"]` to limit where it shows).
3. `node tools/build.js`, then sync the master, then commit both repos.
Likely programmes: online legal services (business formation, trademark filing, document templates), identity theft protection, password managers, privacy/cookie-consent tools, accounting/VAT software. Keep partner placement clearly separate from the legal information.

## Ideas / next
Referral links · more pages (GDPR subject access requests, product safety for sellers, digital content/app refunds, freelancer contracts, travel/flight compensation link to TravelDeals) · a social share image (`seo.image`) · a weekly blog task for new rules and scam alerts.
