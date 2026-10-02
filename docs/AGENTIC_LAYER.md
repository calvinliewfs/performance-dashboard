# Agentic Layer

## Draftable Actions (low risk — auto, later)
- Draft turnover record from spreadsheet upload (AI-generated, review_status='unreviewed').
- Tag a turnover record with anomaly flag.

## Executable After Approval (medium risk — later)
- Update tenant GTO percentage (affects future charges).
- Bulk-import turnover records from a file.

## Human-Only (high/critical risk — always)
- Delete a turnover record.
- Delete a tenant or property.
- Override a rental charge amount.

## Named Tools (later)
- `import_turnover_from_file` — parse file, draft records (low risk, auto).
- `flag_anomaly` — tag unusual turnover (low risk, auto).
- `update_gto_percentage` — change tenant GTO% (medium, approval).
- `delete_turnover_record` — remove record (high, human-only).

## Audit Log Fields (later)
| Field | Type |
|-------|------|
| id | uuid PK |
| action | text |
| entity_type | text |
| entity_id | uuid |
| performed_by | uuid |
| risk_level | text |
| approved_by | uuid nullable |
| metadata | jsonb |
| created_at | timestamptz |

## v1 vs Later
- **v1**: No agentic actions. All CRUD is manual via UI forms.
- **Later**: File import drafting, anomaly flagging, approval workflow for GTO changes, full audit logging.
