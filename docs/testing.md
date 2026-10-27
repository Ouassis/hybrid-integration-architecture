# Integration test strategy

## Contract tests
- Validate required fields, types, enum values, and schema version.
- Verify backward compatibility for supported consumers.
- Test invalid payloads, unsupported media types, and oversized messages.
- Verify mapping rules using synthetic fixtures.

## Reliability tests
- Simulate transient and permanent failures.
- Confirm retries are bounded and use backoff.
- Simulate a timeout after the downstream operation may have succeeded.
- Deliver the same message multiple times and verify one business effect.
- Test concurrent duplicates and conflicting reuse of an idempotency key.
- Test throttling, delayed responses, malformed responses, and connection resets.

## Security tests
- Reject missing, expired, invalid, and insufficiently privileged credentials.
- Verify TLS/certificate validation and rotation procedures.
- Confirm logs redact sensitive fields.
- Verify rate limits and payload size limits.
- Test replay protection where relevant.

## Operational tests
- Verify correlation IDs across all hops.
- Exercise alerts and dashboards.
- Replay a quarantined/dead-letter message using the approved process.
- Reconcile an uncertain result without duplicate business changes.
- Test rollback and recovery procedures.

Record environment, component versions, synthetic test data, expected/actual results, and defects. Do not place secrets or production payloads in test evidence.
