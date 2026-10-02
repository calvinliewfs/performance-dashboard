# Intelligence Layer

## Messy Inputs (later)
- Uploaded spreadsheet rows → auto-mapped to tenant + month + amount.
- Free-text description of turnover → structured record.

## Auto-Structure Schema (later, JSON example)
```json
{
  "tenant_name": "Café Nero",
  "month": "2025-01",
  "amount": 45000,
  "category": "F&B",
  "confidence": 0.92,
  "source": "spreadsheet_upload",
  "review_status": "unreviewed"
}
```

## Events to Track
- Turnover record created/updated/deleted.
- Rental charge computed.
- Property/tenant created/updated.

## Scoring Rules (v1 — rule-based, no AI)
- **Tenant performance rank**: sort by total turnover (last 3 months) descending.
- **Category split**: sum F&B vs Non-F&B per property for selected period.
- **Trend direction**: compare latest month vs previous month; up/down/flat.

## What Gets Ranked
- Tenants within a property by turnover (high to low).
- Properties by total turnover (later, multi-property view).

## v1 vs Later
- **v1**: Rule-based ranking + trend direction + category split. No AI.
- **Later**: Anomaly detection (unusual turnover dips/spikes), forecast next month, auto-import from POS/spreadsheet with confidence + review_status.
