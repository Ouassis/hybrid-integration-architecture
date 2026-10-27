# Operations runbook template

Fill in system-specific contacts, dashboards, and commands before production use.

## 1. Triage
1. Identify integration, environment, time window, and business impact.
2. Capture correlation ID, message ID, and normalized error category.
3. Check service health, queue age/depth, retry counts, and recent deployments.
4. Determine whether the failure is business, security, contract, or transient technical.

## 2. Protect business consistency
- For a timeout or uncertain outcome, check the downstream business result before replaying.
- Confirm idempotency is active for side-effecting operations.
- Avoid resubmitting messages without understanding duplicate risk.
- Preserve evidence while minimizing sensitive data.

## 3. Recover
1. Correct the underlying cause.
2. Validate the fix in a safe test path where feasible.
3. Replay only messages approved for replay.
4. Monitor completion and verify business reconciliation.
5. Record the incident, root cause, and preventive action.

## 4. Escalation fields
- Business owner:
- SAP technical owner:
- Integration platform owner:
- External service owner:
- Security contact:
- Service objective:
- Dashboard / log search:
- Dead-letter or replay procedure:
- Reconciliation report:
- Rollback procedure:

Do not place passwords, tokens, or private keys in this runbook.
