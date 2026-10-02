# Security

## Secret Handling
- Supabase service key in server-side env only (never exposed to client).
- Client uses anon key with RLS policies.
- No secrets in frontend code or client bundles.

## Permission Model
- **v1 (demo-first)**: Permissive RLS — all tables readable/writable without login. App renders for anonymous visitors.
- **Lock-down sprint**: Replace permissive policies with `auth.uid() = user_id` on all tables. Each row scoped to its owner.
- Agent (later) inherits the logged-in user's permissions; cannot exceed user scope.

## Approved-Tools Rule
- AI actions (later) use named tools only (`import_turnover_from_file`, `flag_anomaly`, etc.).
- Never expose raw `run_any` or `send_any` endpoints.
- Each tool has a declared risk level and approval gate.

## Audit Principle
- Every meaningful write (create/update/delete turnover, property, tenant, rental charge) is logged.
- Audit trail survives refresh and is server-stored.
- In v1, rely on Supabase row created_at + user_id (nullable). Full audit_logs table added in lock-down sprint.
