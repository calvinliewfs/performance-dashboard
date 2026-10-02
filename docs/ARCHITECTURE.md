# Architecture

## Stack
Next.js (App Router) + Supabase (Postgres) + Vercel. Charts via Recharts.

## Build Now vs Later
- **Now**: Property/tenant CRUD, turnover entry, rental auto-calc, dashboard with charts, category split.
- **Later**: Auth + RLS lock-down, AI anomaly flagging, automated POS ingestion, PDF export.

## Key User Action Flow
1. User opens dashboard → selects a property from sidebar/dropdown.
2. Dashboard queries turnover records for that property's tenants, grouped by month.
3. Renders trend chart (Recharts), category split, per-tenant table with rental charges.
4. User clicks "Add Turnover" → form (tenant, month, amount, category auto-filled from tenant).
5. On submit → DB insert → rental charge auto-created (turnover × GTO%) → dashboard refreshes.

## Responsive Nav Shell
Left sidebar (desktop): Properties list + selected property's tenant list. Collapses to hamburger menu on mobile. Single main panel: dashboard. "Add Turnover" is a modal/drawer.

## Layer Plan
1. **Data layer** (`lib/data/`): all Supabase reads/writes — properties, tenants, turnover, rental charges.
2. **App logic** (`lib/actions/`): server actions for CRUD + rental charge computation.
3. **UI** (`components/`, `app/`): dashboard, charts, forms.
4. **Smart features** (`lib/ai/`, later): anomaly detection, forecast suggestions.

Core runs without AI: turnover CRUD + rental calc + charts are pure DB + code.

## Repo Structure
```
app/
  dashboard/page.tsx
  layout.tsx
components/
  PropertySidebar.tsx
  TurnoverChart.tsx
  CategorySplit.tsx
  TenantTable.tsx
  TurnoverFormModal.tsx
  EmptyState.tsx
lib/data/
  properties.ts
  tenants.ts
  turnover.ts
  rentalCharges.ts
lib/actions/
  turnover.ts
  rentalCharge.ts
lib/ai/
  (later)
__tests__/
  turnover.test.ts
```

## Module Map
| Module | Responsibility | Data Owned | Build Order |
|--------|--------------|------------|-------------|
| properties | CRUD for properties | properties table | 1 |
| tenants | CRUD for tenants + GTO config | tenants table | 1 |
| turnover | Log monthly turnover per tenant | turnover_records table | 2 |
| rental-charges | Auto-compute charge from turnover | rental_charges table | 2 |
| dashboard | Aggregate + display charts/table | reads all tables | 3 |
| auth (later) | Login + owner-scoped RLS | auth integration | 5 |
