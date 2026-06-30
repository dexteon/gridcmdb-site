# GridCMDB Website — Review, Fixes, and Additions

**Site URL:** https://project-creation-2tyj.bolt.host
**Built with:** bolt.new
**Reviewed:** 2026-06-29

---

## REVIEW SUMMARY

The site is well-built. All 12 sections from the spec are present, the copy matches, the dark theme is correct, and the structure is clean (48KB, no framework dependencies). Here's what's good, what needs fixing, and what I'd add.

---

## WHAT'S GOOD (no changes needed)

- All 12 sections present and in the correct order
- Hero with headline, subheadline, two CTAs, and 4-item stat bar
- 5 feature cards with correct copy (Inventory, Network Import, IEC 62443, Risk, DQ+Incidents)
- Pricing: 3 tiers with correct prices ($5K+$1.5K, $12K+$2.5K, $25K+$4K)
- Comparison table: 13 rows, all correct data vs Claroty/Dragos/Spreadsheet
- FAQ: 11 questions across Technical and Business sections
- About section: origin story with correct copy
- Footer: 3 columns (Product, Company, Contact)
- Dark theme: #0a0e1a bg, #00d4ff accent, #2dd4bf teal
- Inter + JetBrains Mono fonts from Google Fonts
- Mobile hamburger menu with toggle
- 9 Calendly placeholder links on all CTAs
- Responsive design with breakpoints
- No MNOT-ICS branding anywhere — product is "GridCMDB" throughout

---

## FIXES NEEDED

### Fix 1: Verify FAQ accordion JavaScript works
The HTML has 30 FAQ-related elements but I couldn't visually verify the accordion toggle. 

**What to check:** Click each question — does it expand to show the answer? Does clicking again collapse it? Does only one stay open at a time?

**If it doesn't work, add this JS before </body>:**
```javascript
document.querySelectorAll('.faq-question').forEach(q => {
  q.addEventListener('click', () => {
    const answer = q.nextElementSibling;
    const isOpen = answer.style.display === 'block';
    document.querySelectorAll('.faq-answer').forEach(a => a.style.display = 'none');
    answer.style.display = isOpen ? 'none' : 'block';
  });
});
```

### Fix 2: Comparison table — highlight GridCMDB column
The GridCMDB column should have a subtle accent tint background to stand out from Claroty/Dragos/Spreadsheet columns.

**Add to CSS:**
```css
.compare-table th:nth-child(2),
.compare-table td:nth-child(2) {
  background: rgba(0, 212, 255, 0.05);
}
```

### Fix 3: Stat bar — verify JetBrains Mono is applied
The stat bar items (11,487 assets | $0 infrastructure | 1 hour | 1/4 Claroty) should use the mono font. The CSS variable is set but verify the stat items have `font-family: var(--mono)` or `font-family: 'JetBrains Mono', monospace;`.

### Fix 4: Calendly links — replace placeholder
All 9 CTA buttons currently link to `https://calendly.com/your-link-here`. Replace with your real Calendly URL once you create the account.

**Find and replace in the HTML:**
- Find: `https://calendly.com/your-link-here`
- Replace with: `https://calendly.com/teonmoore/gridcmdb-demo` (or your actual URL)

### Fix 5: Contact email — replace placeholder
The footer shows `contact@gridcmdb.com`. Since gridcmdb.com is taken, either:
- Buy the domain on aftermarket
- Change to a domain you own (e.g., `contact@cyberautomations.com`)
- Use a subdomain approach

**Find and replace:**
- Find: `contact@gridcmdb.com`
- Replace with: `teonmoore@gmail.com` (or your preferred contact email)

### Fix 6: Footer copyright
Currently: `© 2026 GridCMDB. Built for OT/ICS teams that can't afford Claroty.`
If you change the product name, update this too.

---

## ADDITIONS (to increase conversion)

### Addition 1: "How it works" strip (between Problem and Solution)
A 3-step visual that shows the deployment process. Reduces buyer anxiety about "how does this actually work?"

**Add after the Problem section, before the Solution section:**
```html
<section class="how-it-works">
  <div class="container">
    <div class="how-grid">
      <div class="how-step">
        <span class="step-number">01</span>
        <h3>Deploy</h3>
        <p>We push the CMDB to your Google Workspace. Set Script Properties. One hour.</p>
      </div>
      <div class="how-step">
        <span class="step-number">02</span>
        <h3>Import</h3>
        <p>Drop in your CSV or paste a network config. Assets normalize automatically.</p>
      </div>
      <div class="how-step">
        <span class="step-number">03</span>
        <h3>See</h3>
        <p>Dashboard, risk scores, IEC posture, data quality — all populated from your real data.</p>
      </div>
    </div>
  </div>
</section>
```

### Addition 2: "30-day money-back guarantee" badge
Reduces buyer friction near the pricing section. Add a small badge below the 3 pricing cards, above the "honest exclusions" box:
```html
<div class="guarantee-badge">
  30-day money-back guarantee on the setup fee
</div>
```

### Addition 3: Feature gap analysis features (from the research)
Once you build the Tier 1 features from the gap analysis, add them to the website:

**Add to the Solution section as new feature cards:**
- Automated Alerting — "Your CMDB emails you when risk scores breach thresholds, assets go stale, or new devices appear on the network."
- Compliance Report Export — "One-click PDF reports mapped to NERC CIP-002, IEC 62443, and NIS2 Article 21. Hand your auditor a document, not a URL."
- BES Cyber System Categorization — "CIP-002 High/Medium/Low impact classification built into the asset record. Categorization wizard walks you through the criteria."
- Incident Reporting Timeline — "NIS2 24h/72h reporting clock. When an incident fires, countdown timers start. You get alerted before the deadline expires."
- Scheduled DQ Monitoring — "Weekly data quality report auto-emailed to your team. The CMDB checks its own health — you don't have to remember to look."

### Addition 4: "Trusted by" placeholder with industry names
Instead of gray boxes, use industry names as text:
```html
<div class="industries-bar">
  <span>Utilities</span>
  <span>Manufacturing</span>
  <span>Telecom</span>
  <span>Water Treatment</span>
  <span>Transportation</span>
</div>
```

### Addition 5: Schema.org structured data
Add JSON-LD to the <head> for SEO:
```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "SoftwareApplication",
  "name": "GridCMDB",
  "applicationCategory": "SecurityApplication",
  "operatingSystem": "Web Browser (Google Workspace)",
  "description": "OT/ICS Configuration Management Database that runs on Google Workspace. Zero infrastructure. Deploy in an hour.",
  "offers": {
    "@type": "Offer",
    "price": "1500",
    "priceCurrency": "USD",
    "description": "Starting at $1,500/month + $5,000 setup"
  }
}
</script>
```

---

## DOMAIN RECOMMENDATION

All three candidate names (leanics.com, levelzeroics.com, gridcmdb.com) are taken across every TLD. Options:

1. **Buy gridcmdb.com on aftermarket** — it has no DNS records, likely parked. Use Namecheap's domain broker service ($5 broker fee + seller price, typically $200-$1,000 for parked domains).

2. **Use CyberAutomations.com subdomain** — free, already hosted on Vercel. Options:
   - cmdb.cyberautomations.com
   - ot.cyberautomations.com
   - levelzero.cyberautomations.com
   
3. **Pick a new name** — try variations like:
   - otbase.com
   - gridot.com  
   - level0security.com
   - leancmdb.com (check if available)

4. **Check leanics.com** — registered since 2003 but has no active website. Could be purchasable.

My recommendation: use cmdb.cyberautomations.com for now (free, instant, brand-consistent). When you get your first paying client, buy the proper domain with the revenue.

---

## CALENDLY SETUP INSTRUCTIONS

1. Go to calendly.com → Sign up with teonmoore@gmail.com
2. Create event type: "GridCMDB Demo" (30 minutes)
3. Set availability: weekdays, your preferred hours
4. Meeting location: Google Meet
5. Custom question: "How many OT/ICS assets are you managing?"
6. Copy your link (format: calendly.com/teonmoore/gridcmdb-demo)
7. Replace all 9 instances of "https://calendly.com/your-link-here" in the website HTML

Once created, tell me the URL and I'll:
- Update the website HTML
- Save the Calendly credentials to Bitwarden
- Update the SALES-PLAN.md with the real link

---

## FINAL VERDICT

The bolt.new build is solid. The content is exactly what we specced. The design matches the Linear/Vercel aesthetic. The only critical fix is verifying the FAQ accordion works. Everything else is polish.

Ship it to cmdb.cyberautomations.com, get the Calendly link in, and start the LinkedIn outbound. The site doesn't need to be perfect — it needs to be good enough to book a demo. It is.