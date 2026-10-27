# Reference architecture

## Logical flow

```text
SAP ECC / SAP S/4HANA
  |  released API, OData, SOAP, IDoc, RFC (where appropriate)
  v
Integration boundary
  - API management / gateway
  - integration platform or middleware
  - authentication and policy enforcement
  - schema validation and mapping
  - routing, correlation, error handling
  v
External application / partner / cloud service
```

Select components based on the actual SAP release, licensed products, network topology, latency, volume, and operational ownership. This diagram is logical, not a prescription to deploy every component.

## Pattern selection

| Need | Candidate pattern | Main trade-off |
|---|---|---|
| Immediate response required | Synchronous API/OData/SOAP | Caller experiences downstream latency and availability |
| High decoupling or burst absorption | Asynchronous message/event | Eventual consistency and operational queue management |
| Bulk transfer with reconciliation | Batch/file or bulk API | Freshness delay and restart/reconciliation complexity |
| SAP business document exchange | IDoc or released business API, where supported | Coupling to SAP message semantics and configuration |

Avoid synchronous chains across many services. Every additional hop adds latency and another failure boundary.

## Contract design

- Define business purpose, owner, consumer, schema, and version policy.
- Distinguish business errors from transient technical errors.
- Define timeout, retry, duplicate, ordering, and replay behavior.
- Specify required identifiers, timestamps, and correlation metadata.
- Establish compatibility rules before changing a contract.

## Request lifecycle

1. Authenticate the caller and authorize the operation.
2. Validate schema and business preconditions.
3. Assign or propagate a correlation ID.
4. Execute the SAP or external business operation.
5. Persist or propagate the outcome safely.
6. Emit operational telemetry without sensitive payloads.
7. Provide a reconciliation path for uncertain outcomes.

## Architecture decisions to record

- System of record for each business entity.
- Synchronous versus asynchronous delivery.
- SAP API and release compatibility.
- Identity propagation and trust boundaries.
- Idempotency key and retention period.
- Error queue and replay ownership.
- Service-level objectives and alert thresholds.
- Data classification and retention.
