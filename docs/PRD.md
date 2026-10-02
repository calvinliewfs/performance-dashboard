# Performance Dashboard — PRD

## Problem
CEOs and CFOs of multi-property portfolios lack a single view of tenant performance, turnover trends, and rental charge calculations. Monthly turnover is tracked in spreadsheets; rental charges (GTO % of tenant turnover) are computed manually and are error-prone.

## Target User
CEO and CFO of a property portfolio (multiple properties, multiple tenants per property). Internal tool, not a SaaS.

## Core Objects
- **Property** — a building/asset with tenants.
- **Tenant** — a leaseholder within a property; has a category (F&B or Non-F&B) and a GTO percentage.
- **Turnover Record** — one month's turnover for a tenant (amount, month, category, created timestamp).
- **Rental Charge** — computed charge for a tenant in a month: `turnover × GTO %`. Auto-generated from turnover.

## MVP (v1)
- [ ] Dashboard page: per-property summary (total monthly turnover, per-tenant breakdown, total rental charges).
- [ ] Add/edit/delete a turnover record for any tenant.
- [ ] Rental charge auto-computed and shown when turnover is entered.
- [ ] Trend chart: monthly turnover per tenant (line/bar).
- [ ] Category breakdown: F&B vs Non-F&B turnover per property.
- [ ] Property + tenant CRUD (seeded, but user can add/edit/delete).
- [ ] No login required — demoable by anonymous visitor.

## Non-goals (v1)
- Login / per-user isolation (later lock-down sprint).
- Multi-currency support.
- PDF export / email reports.
- Automated data ingestion from POS systems.
- AI-assisted data entry or anomaly detection.

## Success Criteria
A CEO opens the dashboard with no login, selects a property, sees a trend chart of each tenant's monthly turnover for the past 6 months, a category split (F&B vs Non-F&B), total property turnover, and the auto-computed rental charge per tenant. They add a new turnover record for a tenant for the current month; the chart and rental charge update instantly.
