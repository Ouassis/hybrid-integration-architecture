# Reliability patterns

## Timeouts

Set explicit connection and response timeouts at each hop. Derive them from the business latency objective and downstream service behavior. Do not let requests wait indefinitely. A caller timeout does not prove that the downstream business operation failed.

## Retries

Retry only failures classified as transient, such as selected network interruptions, throttling responses, or temporary service unavailability. Do not blindly retry validation failures, authorization failures, or other permanent business errors.

Use bounded retries with exponential backoff and jitter. Respect server-provided retry guidance where applicable. A retry policy must include a maximum attempt count and a final failure path.

The values in `examples/retry-policy.yaml` are illustrative only and must be tuned and tested for the actual system.

## Idempotency

For operations that create or change business state:

- Define a stable idempotency key based on the business operation.
- Persist the key and outcome for a documented retention period.
- Return the original result for a legitimate duplicate where appropriate.
- Reject reuse of the same key with a conflicting payload.
- Ensure concurrent duplicate requests cannot both perform the side effect.

If the downstream SAP API does not support idempotency directly, evaluate a durable integration-side ledger and reconciliation process. Do not assume a transport-level retry is safe.

## Duplicate and ordering handling

Define whether messages can be delivered more than once and whether order matters. For event-driven processes, consider event IDs, aggregate/business keys, sequence numbers, and replay controls.

## Error taxonomy

| Category | Typical response |
|---|---|
| Validation/business rejection | Return actionable error; do not retry automatically |
| Authentication/authorization | Stop and correct identity or permissions |
| Throttling/transient availability | Bounded backoff and retry if operation is safe |
| Timeout with uncertain outcome | Query/reconcile before repeating side effects |
| Mapping/schema failure | Quarantine or reject; alert contract owner |
| Persistent downstream failure | Circuit-break or pause flow if supported; alert operations |

## Recovery

Every integration should specify who can replay a failed message, what preconditions apply, how duplicates are prevented, and how the business outcome is reconciled.
