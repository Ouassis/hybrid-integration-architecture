# Integration security baseline

## Identity and access

- Prefer supported OAuth 2.0, mutual TLS, or other approved mechanisms appropriate to the participating systems.
- Use technical users only where required and assign least-privilege roles.
- Separate authentication from authorization; a valid identity does not imply permission for every operation.
- Define certificate rotation, token expiry, and credential ownership.
- Validate identity propagation across middleware boundaries.

## Secrets and configuration

- Never commit passwords, private keys, access tokens, client secrets, or real connection strings.
- Use approved secret-management facilities and environment-specific secure configuration.
- Keep development, test, and production credentials separate.
- Avoid secrets in URLs, exception text, trace payloads, or CI logs.

## Data protection

- Classify payloads before logging or forwarding them.
- Minimize personal, financial, and confidential fields.
- Redact sensitive values from diagnostics.
- Define retention and deletion for messages, dead-letter queues, and logs.
- Use synthetic data in examples and automated tests.

## Network and API boundaries

- Document allowed source/destination paths and trust boundaries.
- Validate schemas, content types, size limits, and allowed operations.
- Apply rate limits and abuse protection where appropriate.
- Verify TLS and certificate validation; do not disable verification to work around certificate issues.

## Security review checklist

- [ ] Caller and service identities are documented.
- [ ] Least privilege is applied on both SAP and external systems.
- [ ] Secrets are stored outside source control.
- [ ] TLS and certificate rotation are tested.
- [ ] Sensitive payloads are redacted from logs.
- [ ] Replay and duplicate-message threats are considered.
- [ ] Access revocation and incident response are documented.
