# Tasks

## Sprint 1 — Database + Core CRUD (no login)
**Goal**: Schema, seed data, property + tenant CRUD, turnover entry + rental auto-calc working end-to-end.
- [ ] Create Supabase tables (properties, tenants, turnover_records, rental_charges) with permissive RLS.
- [ ] Seed 2 properties, 5 tenants, 6 months of turnover records, matching rental charges.
- [ ] `lib/data/` layer: queries for all four tables.
- [ ] `lib/actions/`: server actions — createProperty, updateProperty, deleteProperty, createTenant, updateTenant, deleteTenant, createTurnover (auto-creates rental_charge), updateTurnover, deleteTurnover.
- [ ] Property sidebar: list properties, select one, list its tenants.
- [ ] Tenant table: per-tenant monthly turnover + rental charge.
- [ ] "Add Turnover" modal: form with tenant (pre-selected), month, amount. On submit → insert turnover + auto-compute rental charge → refresh table.
- **DoD**: User can add a turnover record for a tenant and see the rental charge appear in the table. No login required.

## Sprint 2 — Dashboard + Charts ← **v1 functional milestone**
**Goal**: Full dashboard with charts and category split — the success scenario is usable.
- [ ] Turnover trend chart (Recharts line/bar) per tenant for last 6 months.
- [ ] Category split widget: F&B vs Non-F&B total turnover for selected property.
- [ ] Property total turnover + total rental charges summary cards.
- [ ] Empty/loading/error states for dashboard and chart.
- [ ] Responsive: sidebar collapses to hamburger on mobile.
- **DoD**: CEO opens dashboard without login, selects property, sees trend chart, category split, totals, and rental charges. Adds a turnover record → chart and charges update. This is the v1 success scenario.

## Sprint 3 — Polish + Edit/Delete
**Goal**: Full CRUD on all entities; UX polish.
- [ ] Edit/delete turnover records from the table.
- [ ] Add/edit/delete properties and tenants.
- [ ] Form validation (duplicate tenant+month, negative amounts, invalid GTO%).
- [ ] Loading skeletons, error toasts, empty states for every surface.
- [ ] Month picker + tenant filter on chart.
- **DoD**: Every entity can be created, edited, and deleted from the UI. All five states handled.

## Sprint 4 — Lock It Down (auth + RLS)
**Goal**: Secure the app before real data.
- [ ] Supabase Auth (email/password).
- [ ] Replace permissive RLS with `auth.uid() = user_id` on all tables.
- [ ] Redirect unauthenticated users to login.
- [ ] Set user_id on all inserts.
- **DoD**: Unauthenticated user cannot read or write data. Logged-in user sees only their own rows.

## Sprint 5 — Intelligence + Agentic (later)
**Goal**: AI-assisted features.
- [ ] Spreadsheet import → draft turnover records (confidence + review_status).
- [ ] Anomaly detection on turnover trends.
- [ ] Audit log table + logging on all writes.
- [ ] Named tools with risk-level approval gates.

## Text Gantt
```
S1: DB + CRUD          ████
S2: Dashboard + Charts ██████  ← v1 functional
S3: Polish + CRUD     ███
S4: Lock-down         ██
S5: Intelligence       ████
```
