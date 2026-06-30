# GridCMDB — OT/ICS Asset Management on Google Workspace

Landing page for GridCMDB, an OT/ICS configuration management database that runs entirely on Google Workspace.

**Live site:** https://cmdb.cyberautomations.com

## What's in this repo

- `index.html` — the landing page (single-file, no framework, no build step)
- `FEATURE-GAP-ANALYSIS.md` — product feature roadmap (18 features ranked by ROI)
- `WEBSITE-REVIEW-AND-FIXES.md` — review notes and applied fixes

## Tech

- Pure HTML/CSS/JS — no build tools, no dependencies
- 48KB total
- Dark theme (#0a0e1a bg, #00d4ff accent)
- Inter + JetBrains Mono via Google Fonts
- Responsive (mobile hamburger menu, breakpoints)
- Deployed on Vercel, subdomain on CyberAutomations.com

## Deploy

The site is deployed via Vercel CLI from the `docs/` directory of the main CMDB project. This repo is the canonical source for the website.

```bash
npx vercel --prod --yes
```

## Contact

- Calendly: https://calendly.com/cyberautomations/gridcmdb-demo
- Email: teonmoore@cyberautomations.com