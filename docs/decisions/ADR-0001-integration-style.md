# ADR-0001: Select an integration style

- **Status:** Proposed template
- **Date:** To be completed
- **Decision owner:** To be assigned

## Context
Describe business process, SAP release, connected systems, data sensitivity, throughput, latency, and availability requirements.

## Options
1. Synchronous API (OData, SOAP, REST, or another supported interface).
2. Asynchronous messaging/event-driven integration.
3. Batch/file or bulk transfer.
4. SAP-specific mechanism such as IDoc or another released interface where appropriate.

## Decision criteria
- Business latency and consistency needs.
- API availability and support in the target SAP release.
- Expected volume and burst behavior.
- Retry, duplicate, ordering, and reconciliation requirements.
- Security and network topology.
- Monitoring and operational ownership.
- Cost, licensing, and platform skills.

## Decision
Record the selected pattern and why it fits. Do not select technology only because it is familiar.

## Consequences
Document operational complexity, failure modes, ownership, security controls, monitoring, and migration considerations.

## Validation
List proof-of-concept tests and acceptance criteria required before the decision is final.
