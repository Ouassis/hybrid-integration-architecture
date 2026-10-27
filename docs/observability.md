# Observability and support

## Correlation

Create or accept a correlation ID at the boundary and propagate it across middleware and downstream calls. Preserve separate identifiers for the business document, integration message, and individual attempt. Do not use personal information or secrets as correlation IDs.

## Structured log fields

Recommended fields, subject to platform capabilities:
- timestamp and environment
- integration name and contract version
- correlation ID and message/event ID
- source and destination system aliases
- operation and processing stage
- outcome and normalized error category
- attempt count and elapsed duration
- business reference only where approved and appropriately protected

## Metrics

Track message throughput, success/error rates, latency percentiles, retries, queue depth/age, dead-letter volume, and reconciliation backlog. Define thresholds against agreed service objectives rather than arbitrary universal numbers.

## Alerts

Alerts should be actionable: name the integration, impact, first diagnostic steps, responsible team, and relevant dashboard/runbook. Avoid paging on every isolated transient error if retries are working as designed.

## Logging safeguards

- Never log credentials, authorization headers, private keys, or unredacted sensitive payloads.
- Bound payload capture and retention.
- Restrict log access and audit privileged access.
- Ensure errors are useful without disclosing secrets or personal data.
- Verify trace/debug modes cannot be enabled broadly in production without approval.
