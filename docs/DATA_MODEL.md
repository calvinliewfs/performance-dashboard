# Data Model

## properties
| Field | Type | Notes |
|-------|------|-------|
| id | uuid PK | |
| name | text | e.g. "Marina Mall" |
| created_at | timestamptz | |
| user_id | uuid nullable | owner-scoping later |

## tenants
| Field | Type | Notes |
|-------|------|-------|
| id | uuid PK | |
| property_id | uuid FK→properties | |
| name | text | e.g. "Café Nero" |
| category | text | 'F&B' or 'Non-F&B' |
| gto_percentage | numeric | e.g. 8.5 (means 8.5%) |
| created_at | timestamptz | |
| user_id | uuid nullable | |

## turnover_records
| Field | Type | Notes |
|-------|------|-------|
| id | uuid PK | |
| tenant_id | uuid FK→tenants | |
| amount | numeric | monthly turnover |
| month | date | first of month, e.g. 2025-01-01 |
| category | text | denormalized from tenant for fast filtering |
| created_at | timestamptz | timestamp turnover was logged |
| user_id | uuid nullable | |

Unique constraint: (tenant_id, month) — one record per tenant per month.

## rental_charges
| Field | Type | Notes |
|-------|------|-------|
| id | uuid PK | |
| tenant_id | uuid FK→tenants | |
| turnover_record_id | uuid FK→turnover_records | |
| month | date | matches turnover month |
| turnover_amount | numeric | snapshot of turnover |
| gto_percentage | numeric | snapshot of GTO% at time of calc |
| charge_amount | numeric | turnover_amount × (gto_percentage/100) |
| created_at | timestamptz | |
| user_id | uuid nullable | |

## Relationships
```
property 1──* tenant 1──* turnover_record 1──1 rental_charge
```

## RLS (v1 — demo-first, permissive)
All tables: permissive SELECT + INSERT/UPDATE/DELETE for anonymous. Lock-down sprint replaces with `auth.uid() = user_id`.

## AI Fields (later)
No AI-generated fields in v1. Future: `anomaly_flag` on turnover_records with value+source+confidence+review_status.
