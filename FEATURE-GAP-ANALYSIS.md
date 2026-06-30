# GridCMDB — Feature Gap Analysis & Roadmap

**Date:** 2026-06-29
**Method:** Cross-referenced current codebase (63 .gs files, 130+ schema fields) against market requirements from Claroty, Dragos, Nozomi, ServiceNow OT, NERC CIP, IEC 62443, NIS2, and CMDB industry comparisons.

---

## What We Already Have (16 features)

| Feature | Status | Implementation |
|---------|--------|----------------|
| Asset inventory (10K+) | Complete | 11,487 real assets, 130+ fields, SchemaRegistry |
| Multi-vendor config import | Complete | Cisco IOS, Palo Alto PAN-OS, Cisco ASA parsers |
| Credential audit (hashed) | Complete | 7 fields, SHA-256 client-side, SENSITIVE_FIELDS |
| IEC 62443 posture | Complete | SL-T/SL-A, gap KPIs, zone/Purdue/business-service |
| Risk scoring (0-100) | Complete | Decomposable, explainable, telecom-aware weights |
| Data quality gates | Complete | 6 metrics (dup/orphan/verify/stale/drift/sync) |
| Incident & change tracking | Complete | Per-asset rollups, UID-linked, separate sheets |
| RBAC | Complete | Admin/Editor/Viewer, CLLI-scoped, fail-closed |
| Audit log | Complete | Separate spreadsheet, sensitive fields redacted |
| CI pipeline + tests | Complete | GitHub Actions, 6 test suites, 143 invariants |
| Zone/Purdue classification | Complete | 9 zones, ZoneService, Purdue level assignment |
| Fingerprinting | Complete | Exemplar tiered matching (MAC-OUI → ports → attrs) |
| Network topology view | Partial | by_zone/by_purdue/adjacency/matrix, manual layout |
| SBOM storage | Partial | Sheet exists, no ingestion automation |
| Vendor advisories | Partial | Sheet exists, no auto-pull from NVD/ICS-CERT |
| Patch deferrals | Partial | Sheet exists, no workflow |

---

## Feature Gaps — What the Market Demands That We Don't Have

### Tier 1: HIGH ROI — Compliance-Driven (Sell to Regulated Industries)

These features directly address NERC CIP, IEC 62443, NIS2, and EU CRA compliance mandates. They are the difference between "nice inventory tool" and "audit-ready compliance system."

#### 1. Automated Alerting System
**Why:** Every competitor has this. An OT security manager needs to know when a critical asset's risk score crosses a threshold, when a new asset appears on the network, or when a record hasn't been verified in 90+ days. Currently they have to manually run the DQ report.
**What to build:**
- Time-based trigger (daily/weekly) that checks:
  - Assets with risk_score > threshold (configurable, default 70)
  - Assets with last_verified_at > 90 days
  - New assets added since last check (asset_id not in previous snapshot)
  - Assets with default_credentials_changed = "No" or "Unknown"
  - Assets with communication_encryption = "None"
- Email alert via MailApp.sendEmail() to configured recipients
- Alert digest format: grouped by severity, with asset counts and direct links to the affected assets in the web app
- Alert configuration: admin UI to set thresholds, recipients, schedule
**GAS feasibility:** Yes — time-based triggers + MailApp. 1 trigger per alert type, well within the 20-trigger cap.
**Effort:** 2-3 days
**Sell impact:** "Your CMDB tells you when something needs attention — you don't have to look."

#### 2. Compliance Report Export
**Why:** Auditors want formatted evidence, not a web app URL. Currently the DQ report is screen-only. Competitors export PDF reports mapped to specific compliance frameworks.
**What to build:**
- SpreadsheetApp → formatted report sheet → PDF export via getBlob().getAs('application/pdf')
- Report types:
  - NERC CIP asset inventory (CIP-002): asset ID, BES impact level, location, owner
  - IEC 62443 posture report: SL-T vs SL-A by zone, gap analysis, compensating controls
  - NIS2 Article 21 asset register: assets, criticality, risk measures, supply chain
  - Data quality report: 6 metrics + trend (current vs last run)
  - Risk assessment report: per-asset risk decomposition with business justification
- Report configuration: date range, site filter, zone filter, format (PDF/CSV/Sheets)
- Scheduled report delivery: auto-email weekly/monthly to distribution list
**GAS feasibility:** Yes — SpreadsheetApp native PDF export, MailApp for delivery.
**Effort:** 3-5 days
**Sell impact:** "Hand your auditor a PDF, not a URL. Reports map directly to NERC CIP, IEC 62443, and NIS2 requirements."

#### 3. BES Cyber System Categorization (NERC CIP-002)
**Why:** Every North American utility must categorize BES cyber systems by impact level (High/Medium/Low). This is the foundation of their entire NERC CIP compliance program. If we have this, we're not just a CMDB — we're a CIP compliance tool.
**What to build:**
- New schema field: `bes_impact_level` (High/Medium/Low/Not Applicable)
- Categorization wizard: walk through the CIP-002 criteria (does this asset affect generation? transmission? balancing? etc.)
- Auto-classification rules based on device_type, purdue_level, security_zone, and site_type
- CIP-002 report: categorized asset list with justification per asset
- Impact analysis: "if this asset goes down, what BES reliability tasks are affected?"
**GAS feasibility:** Yes — schema field + classification logic + report.
**Effort:** 2-3 days
**Sell impact:** "We don't just track your assets — we categorize them for NERC CIP compliance. CIP-002 done."

#### 4. Incident Reporting Timeline (NIS2 Article 23)
**Why:** NIS2 requires incident reporting within 24 hours (early warning) and 72 hours (full report). EU CRA requires similar timelines. Currently we log incidents but don't track the reporting obligation timeline.
**What to build:**
- Incident record gets two new fields: `early_warning_due_at` (incident_created_at + 24h) and `full_report_due_at` (incident_created_at + 72h)
- Incident dashboard shows countdown timers: "Early warning due in 3h 22m" / "Full report due in 2d 4h"
- When a report is submitted: `early_warning_submitted_at` and `full_report_submitted_at` timestamps
- Alert if deadline approaching (1h before early warning, 12h before full report)
- NIS2 incident report export: pre-formatted template with required fields
**GAS feasibility:** Yes — timestamp fields + time-based trigger for alerts.
**Effort:** 2 days
**Sell impact:** "When an incident happens, the clock starts. We track the NIS2 24h/72h reporting deadline and alert you before it expires."

#### 5. Scheduled Drift Detection (Automated DQ Monitoring)
**Why:** Data quality is only useful if it's checked regularly. Currently the DQ report is manual. Making it scheduled + emailed means the CMDB actively monitors its own health.
**What to build:**
- Time-based trigger (weekly, configurable)
- Runs the full DQ harness (6 metrics)
- Compares to previous snapshot (trend: improving/degrading)
- Email digest to configured recipients with:
  - Current scores vs last week
  - Any metric that crossed a threshold (e.g., duplicate rate > 2%)
  - Direct links to the DQ dashboard
- DQ trend chart (stored in cache, rendered in UI)
**GAS feasibility:** Yes — trigger + DQ harness (already built) + MailApp.
**Effort:** 1-2 days
**Sell impact:** "Your CMDB checks its own health every week and emails you the results. You don't have to remember to look."

---

### Tier 2: MEDIUM ROI — Operational Efficiency (Sell to Overworked Teams)

These features reduce manual work and make the CMDB something that runs itself, not something you have to babysit.

#### 6. Scheduled Auto-Import
**Why:** Currently every import is a manual button click. OT teams want to drop a CSV in a Google Drive folder and have it auto-imported, or pull from an API (nmap scan, Nessus, etc.) on a schedule.
**What to build:**
- Time-based trigger (daily/weekly)
- Import sources:
  - Google Drive folder: scan for new CSV files → import → archive
  - REST API: UrlFetchApp to pull scan results from Nessus/Qualys/nmap
  - Google Sheets: watch a staging sheet for new rows
- Import log: what was imported, when, how many rows, errors
- Auto-normalization on import (existing pipeline, just automated trigger)
**GAS feasibility:** Yes — triggers + DriveApp + UrlFetchApp. The import pipeline already exists.
**Effort:** 2-3 days
**Sell impact:** "Drop a scan file in a folder. The CMDB imports it, normalizes it, and updates the dashboard. Zero clicks."

#### 7. EOL/EOS Lifecycle Tracking
**Why:** OT devices run for 10-20 years. Knowing that a PLC's firmware is end-of-life is critical for risk assessment and budgeting. Currently we have the sheet structure but no data.
**What to build:**
- Pre-populated vendor EOL/EOS database (Schneider, Rockwell, Siemens, Cisco, Palo Alto — the top 5 OT vendors)
- Fields: vendor, product, model, firmware_version, eos_date, eol_date, replacement_model
- Auto-match: when an asset's manufacturer + model + firmware matches the DB, auto-populate eos_date/eol_date
- EOL dashboard: assets approaching EOL (6/12/24 months), assets past EOL, replacement cost estimate
- Alert: monthly EOL report emailed to procurement + security
**GAS feasibility:** Yes — data sheet + matching logic + dashboard view + trigger.
**Effort:** 3-4 days (includes research to populate the vendor DB)
**Sell impact:** "Know which of your PLCs are running unsupported firmware — before the vendor stops patching them."

#### 8. Change Detection Alerts
**Why:** The audit log records every change, but nobody reads audit logs proactively. If someone changes a firewall rule or disables SNMP on a critical asset, the security team should know immediately.
**What to build:**
- Installable onEdit trigger on the assets sheet (or a time-based trigger that diffs)
- Watched fields (configurable): risk_score, security_zone, purdue_level, default_credentials_changed, communication_encryption, has_cyberark, remote_access
- When a watched field changes on a critical asset:
  - Email alert with: asset ID, field changed, old value, new value, who changed it (from audit log), timestamp
  - Webhook notification (if configured) to SIEM/Slack
- Daily digest option: all changes in the last 24h, grouped by asset
**GAS feasibility:** Yes — onEdit trigger (watch out for the 20-trigger cap) or time-based diff.
**Effort:** 2-3 days
**Sell impact:** "Someone changes the encryption setting on a critical PLC? You get an email in 5 minutes."

#### 9. Webhook Notifications
**Why:** Modern security teams want CMDB events in their SIEM (Splunk, Chronicle) or ticketing system (Jira, ServiceNow). A webhook is the simplest integration path.
**What to build:**
- Event types: asset_created, asset_updated, asset_deleted, risk_threshold_breach, incident_created, dq_report_generated
- Webhook configuration: URL, auth header, event filter (which events to send)
- Payload format: JSON with event_type, asset_id, timestamp, changed_fields, actor
- Retry logic: 3 attempts with exponential backoff
- Webhook log: delivery status, response code, payload
**GAS feasibility:** Yes — UrlFetchApp POST with retry.
**Effort:** 1-2 days
**Sell impact:** "Pipe CMDB events into Splunk, Jira, or Slack. Asset changes, risk alerts, incidents — all in your existing workflow."

#### 10. Patch Status Tracking
**Why:** NERC CIP-007 R2 requires patch management. We have a patch_deferrals sheet but no per-asset patch status tracking. OT teams need to know: what patches are available, what's applied, what's deferred, why, and who approved the deferral.
**What to build:**
- New schema fields: `patch_status` (Current / Behind / Deferred / Unknown), `last_patch_date`, `next_patch_due`, `patch_deferral_reason`, `patch_deferral_approver`, `patch_deferral_expires`
- Patch status dashboard: compliance rate by zone, overdue patches, expiring deferrals
- Workflow: deferred patch → approver → expiry date → re-evaluation alert
- Integration with vendor advisories (when a new CVE drops, flag affected assets)
**GAS feasibility:** Yes — schema fields + dashboard + trigger.
**Effort:** 2-3 days
**Sell impact:** "CIP-007 R2 patch management. Track what's patched, what's deferred, and when the deferral expires."

---

### Tier 3: MEDIUM ROI — Risk & Vendor Management (Sell to Risk Officers)

These features extend the CMDB from "asset tracker" to "risk management platform."

#### 11. Vendor Risk Register
**Why:** NIS2 Article 21(2)(d) requires supply chain risk management. Companies need to assess their OT vendors (Schneider, Rockwell, Siemens, etc.) for security posture. Currently we have no vendor-level tracking — only asset-level.
**What to build:**
- New sheet: `vendor_risk_register` with fields: vendor_name, assessment_date, risk_score, assessment_status, last_audit, cert_compliance (ISO27001/SOC2/IEC62443), supply_chain_risk, notes
- Vendor assessment questionnaire (pre-built, 25 questions based on NIST/ISO frameworks)
- Vendor risk scoring (0-100, same scale as asset risk)
- Linkage: assets → vendor → vendor risk score (aggregate vendor risk across all assets)
- Dashboard: vendors ranked by risk, vendor exposure (how many of your assets depend on each vendor)
**GAS feasibility:** Yes — new sheet + questionnaire form + dashboard.
**Effort:** 3-4 days
**Sell impact:** "NIS2 supply chain risk — done. Assess every OT vendor, score their risk, see which vendors pose the biggest exposure to your estate."

#### 12. Supply Chain Risk Mapping
**Why:** Extends vendor risk register — maps which vendors supply which assets, which sites, which critical services. Shows the blast radius if a vendor is compromised.
**What to build:**
- Vendor → asset → site → service dependency chain
- Visualization: "if Schneider is compromised, here are the 847 assets affected across 3 sites"
- Vendor concentration risk: "78% of your PLCs are from one vendor — single point of failure"
- Critical vendor alerting: if a vendor's risk score changes, flag all dependent assets
**GAS feasibility:** Yes — query + aggregation + visualization (D3.js or vis.js).
**Effort:** 2-3 days (depends on #11)
**Sell impact:** "Know your blast radius. If a vendor gets breached, how many of your assets are exposed?"

#### 13. NIS2 Asset Criticality Classification
**Why:** NIS2 requires classification of assets as "essential" or "important" to the essential service. Currently we have process_criticality but no NIS2-specific mapping.
**What to build:**
- New schema field: `nis2_service_classification` (Essential / Important / Supporting / Not Applicable)
- Classification wizard: "Does this asset support an essential service? Which one?"
- Essential services registry: list of the organization's essential services + which assets support each
- NIS2 Article 21 compliance report: asset register with criticality, risk measures, gaps
**GAS feasibility:** Yes — schema field + classification logic + report.
**Effort:** 1-2 days
**Sell impact:** "NIS2 Article 21 asset register — formatted, classified, exportable."

#### 14. Network Segmentation Validation
**Why:** IEC 62443 zone-and-conduit model requires that zones are properly segmented. Currently we classify assets into zones but don't validate that the segmentation is actually enforced.
**What to build:**
- Zone policy definition: which zones are allowed to communicate with which (e.g., Z-DMZ ↔ Z-CTRL is OK, Z-FIELD ↔ Z-DMZ is NOT)
- Validation engine: check observed communications (from network import data) against the policy
- Violation report: "Asset A in Z-FIELD has a route to Asset B in Z-DMZ — this violates your segmentation policy"
- Conduit validation: verify that conduits between zones have the required security controls (firewall, gateway, etc.)
**GAS feasibility:** Yes — policy sheet + validation logic + report.
**Effort:** 3-4 days
**Sell impact:** "Don't just classify assets into zones — verify that your zones are actually segmented. IEC 62443 zone-and-conduit validation."

---

### Tier 4: LOWER ROI — Differentiators

These are nice-to-have features that differentiate from competitors but aren't deal-breakers.

#### 15. Relationship/Dependency Graph Visualization
**What:** Interactive D3.js or vis.js network graph showing asset relationships, dependencies, and blast radius. Click a node, see its dependencies and dependents.
**GAS feasibility:** Yes — HTML view with D3.js (CDN-loaded in the GAS HTML sandbox).
**Effort:** 3-5 days

#### 16. API Documentation (OpenAPI)
**What:** Formal OpenAPI 3.0 spec for the REST API, hosted in-repo, with interactive docs (Swagger UI or similar).
**GAS feasibility:** Yes — static spec file + HTML page.
**Effort:** 1 day

#### 17. Firmware Version Tracking Dashboard
**What:** Matrix view of vendor × model × firmware_version, with EOL/EOS status, asset count per version, and "upgrade available" flag.
**GAS feasibility:** Yes — aggregation + dashboard.
**Effort:** 1-2 days

#### 18. Protocol Analysis Enhancements
**What:** Deeper parsing of Modbus register maps, DNP3 data point lists, BACnet object lists. Currently the parser extracts basic info — this would extract full protocol-level detail.
**GAS feasibility:** Yes — client-side JS parser enhancement.
**Effort:** 3-5 days

---

## Features NOT Feasible on Google Apps Script

These are features competitors have that we cannot build within GAS constraints. They are not gaps to fix — they are positioning boundaries.

| Feature | Why Not | Competitive Response |
|---------|---------|---------------------|
| Real-time network discovery | Requires packet capture / sensor hardware | "We're the management layer. Use your existing discovery tool." |
| Passive traffic analysis | Requires network tap / SPAN port | Same as above |
| SSO/SAML | GAS doesn't support SAML natively | "Google Workspace auth is SOC2/ISO27001/FedRAMP certified." |
| Custom drag-drop dashboard builder | Too complex for GAS HTML constraints | "Our dashboards are purpose-built for OT, not a blank canvas." |
| Multi-tenant isolation | Would need separate script projects per tenant | "Each deployment is isolated on your Google Workspace." |

---

## Implementation Priority Matrix

| # | Feature | Effort | ROI | Tier | Compliance Link |
|---|---------|--------|-----|------|-----------------|
| 1 | Automated Alerting | 2-3d | Very High | 1 | All frameworks |
| 2 | Compliance Report Export | 3-5d | Very High | 1 | NERC CIP, IEC 62443, NIS2 |
| 5 | Scheduled DQ Monitoring | 1-2d | Very High | 1 | All frameworks |
| 3 | BES Categorization (CIP-002) | 2-3d | High | 1 | NERC CIP |
| 4 | Incident Reporting Timeline | 2d | High | 1 | NIS2, EU CRA |
| 6 | Scheduled Auto-Import | 2-3d | High | 2 | Operational |
| 9 | Webhook Notifications | 1-2d | High | 2 | Integration |
| 8 | Change Detection Alerts | 2-3d | Medium | 2 | NERC CIP-007 |
| 7 | EOL/EOS Lifecycle Tracking | 3-4d | Medium | 2 | IEC 62443, NIS2 |
| 10 | Patch Status Tracking | 2-3d | Medium | 2 | NERC CIP-007 |
| 11 | Vendor Risk Register | 3-4d | Medium | 3 | NIS2, EU CRA |
| 13 | NIS2 Asset Criticality | 1-2d | Medium | 3 | NIS2 |
| 12 | Supply Chain Risk Mapping | 2-3d | Medium | 3 | NIS2 |
| 14 | Segmentation Validation | 3-4d | Medium | 3 | IEC 62443 |
| 16 | API Documentation | 1d | Low | 4 | Integration |
| 17 | Firmware Dashboard | 1-2d | Low | 4 | Operational |
| 15 | Dependency Graph Viz | 3-5d | Low | 4 | Operational |
| 18 | Protocol Analysis | 3-5d | Low | 4 | Operational |

**Total effort for Tier 1 (features 1-5):** 10-15 days
**Total effort for Tier 1+2 (features 1-10):** 20-30 days
**Total effort for all 18 features:** 35-55 days

---

## Recommendation

Build Tier 1 first (10-15 days). These 5 features transform the product from "inventory tool" to "compliance system":

1. **Automated Alerting** — the CMDB proactively tells you when something needs attention
2. **Compliance Report Export** — hand your auditor a PDF, not a URL
3. **BES Categorization** — NERC CIP-002 done in the system, not a spreadsheet
4. **Incident Reporting Timeline** — NIS2 24h/72h clock tracking
5. **Scheduled DQ Monitoring** — the CMDB checks its own health weekly

These 5 features add 5 new selling points to the website, each mapped to a specific compliance framework. They convert "nice to have" into "need to have for our next audit."

---

*Analysis date: 2026-06-29*
*Sources: Claroty, Dragos, Nozomi product comparisons; NERC CIP-002/005/007/008/009 requirements; IEC 62443-2-1/3-3; NIS2 Directive Article 21/23; EU CRA; CMDB industry feature comparisons (ServiceNow OT, OTbase, CloudQuery, InvGate, Motadata)*