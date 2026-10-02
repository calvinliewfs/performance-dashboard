# Test Plan

## v1 Success Scenario (manual)
1. Open app in browser (no login) → dashboard loads with seeded data.
2. Select "Marina Mall" property in sidebar → tenant list appears.
3. Verify trend chart shows 6 months of turnover for at least 2 tenants.
4. Verify category split widget shows F&B vs Non-F&B totals.
5. Verify summary cards show total property turnover and total rental charges.
6. Click "Add Turnover" → select tenant "Café Nero", month "2025-06", amount "50000".
7. Submit → modal closes, table shows new row with rental charge = 50000 × 8.5% = 4250.
8. Chart updates to include the new month.

## Empty State
1. Create a new property with no tenants → dashboard shows "No tenants yet — add one to start tracking."
2. Select a tenant with no turnover records → chart shows "No turnover data yet."

## Error State
1. Submit turnover form with empty amount → validation error, no DB write.
2. Submit duplicate tenant + month → unique constraint error shown as toast.
3. Disconnect network, reload → error message on dashboard, no blank screen.

## Loading State
1. Throttle network to Slow 3G → verify loading skeleton on chart + table before data renders.

## CRUD Round-Trip
1. Add a property → appears in sidebar.
2. Add a tenant to it → appears in tenant list.
3. Edit the tenant's GTO% → updated in table.
4. Delete a turnover record → removed from table and chart.
5. Delete a tenant → removed from list; its turnover records gone.
6. Delete a property → removed from sidebar.
