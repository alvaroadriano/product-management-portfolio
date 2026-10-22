# Technical Product Exercise: Reliable Procure-to-Pay Handoffs

> **Portfolio exercise — illustrative design, not historical implementation.** This is a self-directed technical PM exercise informed by my Coupa/LATAM business-spend work. It does not describe FARFETCH’s internal architecture, APIs, or shipped technical design. My verified professional contribution covered business requirements, workflow and control design, and stakeholder coordination; engineering teams owned technical implementation.

## Why this exercise

In my Coupa work, procurement touched requisitions, approvals, purchase orders, receiving, invoices/AP, ERP and tax processes, and Amazon PunchOut. This exercise shows how I would make the product boundary between procurement and ERP explicit: preserve approval controls, give operations a clear transaction state, and make failures recoverable without creating duplicate financial records.

## Product problem

A buyer can complete a procurement step in one system while the next system rejects, delays, or duplicates the handoff. If users cannot tell whether a purchase order or invoice was accepted, they may retry manually, contact support, or create duplicate work. Finance and Procurement also need an audit trail that connects the request, approval, ERP record, and any exception.

**Primary users:** requesters, approvers, Procurement Operations, AP/Finance, and support administrators.

**Goals**

- Show an understandable status for each handoff and the source of any failure.
- Preserve the Delegation of Authority (DOA) approval record before an approved purchase order is sent onward.
- Recover safely from timeouts and transient outages without duplicating ERP records.
- Make unresolved exceptions visible to the team that can act on them.

**Out of scope:** choosing an actual vendor architecture, claiming a specific FARFETCH API or message broker, redesigning tax policy, or changing approval authority.

## Illustrative system boundary

~~~mermaid
flowchart LR
    P["Requester / PunchOut"] --> C["Coupa: requisition and approval"]
    C --> I["Proposed integration boundary"]
    I --> E["D365: ERP record"]
    T["Tax validation process"] <--> I
    E --> C
~~~

This is a product-level boundary diagram, not a reverse-engineered architecture. The integration could use APIs, a managed connector, or another approved mechanism; that decision depends on the actual systems, supported interfaces, security review, and engineering constraints.

## Proposed product behavior

1. **Capture:** a PunchOut cart returns to a requisition with supplier, line items, quantities, currency, and available product references. The requester reviews and submits it.
2. **Approve:** Coupa applies the configured DOA rules. The approval record and the approved requisition version are immutable references for downstream processing.
3. **Validate:** before export, validate required business identifiers and data such as supplier, legal entity, currency, cost center, tax code, and line totals. Missing or invalid master data creates an actionable exception; it does not silently drop a field.
4. **Create or update:** after approval and validation, send the purchase order to the ERP boundary. Return the ERP identifier and status to the originating procurement record.
5. **Reconcile:** compare eligible procurement records with ERP acknowledgements on a scheduled basis. Surface records with no acknowledgement, mismatched totals, or an unresolved status for operations review.

The detailed field map and whether invoices or receipts follow the same interface must be confirmed during technical discovery; this exercise does not assume one shared contract for every object.

## Illustrative contract and control rules

The following fields describe a proposed canonical message, not a real API payload:

| Field | Purpose |
|---|---|
| source_record_id | Stable Coupa-side reference for support and reconciliation |
| source_version | Identifies the approved version being transmitted |
| legal_entity | Routes the transaction to the correct company context |
| supplier_id | Links the transaction to an agreed supplier master record |
| currency and lines[] | Carries item, quantity, unit price, tax reference, and line total |
| approval_reference | Links the export to the recorded DOA outcome |
| idempotency_key | Prevents a retry from creating a second ERP transaction |
| correlation_id | Connects logs and status across the integration boundary |

**Control rule:** once approved, a change to a financially material field should invalidate or restart the appropriate approval path before export. Engineering and Finance would define the material-field list and audit requirements together.

## Failure handling and observability

| Failure | Product response | Recovery owner / signal |
|---|---|---|
| ERP timeout or unavailable | Keep the transaction in Pending acknowledgement; retry with the same idempotency key and bounded backoff | Integration support; age of pending records and retry count |
| ERP rejects master data | Mark Action required, show the rejected field and safe error detail, and prevent blind resubmission | Procurement Operations or master-data owner; rejection reason and resolution time |
| Duplicate delivery | ERP-side idempotency or duplicate check returns the existing record; do not create a second PO | Engineering; duplicate-prevention and duplicate-detection events |
| Amount or currency mismatch | Quarantine from automated completion and send to Finance/Procurement review | Finance/AP; mismatch count and reconciliation status |
| Approval reference missing or stale | Stop export and return the record for review; do not bypass the DOA control | Procurement control owner; blocked export reason and audit event |

Logs should carry correlation and source identifiers, timestamps, state transitions, and normalized error categories. They should avoid unnecessary personal or payment data. Access to retries, corrections, and overrides should be role-based and audited.

## Acceptance criteria

- Given an approved and valid requisition, when the ERP accepts its purchase order, then the procurement record shows the ERP reference and accepted status.
- Given the ERP times out after receiving a request, when the same delivery is retried, then the system returns or finds the original ERP record instead of creating a duplicate.
- Given invalid supplier or tax master data, when validation fails, then the record is held with a clear next action and no silent data loss.
- Given an unacknowledged eligible record, when reconciliation runs, then it appears in an exception queue with source ID, age, last attempt, and owner.
- Given a financially material edit after approval, when export is attempted, then the configured approval control is re-applied before transmission.

## Measures to baseline before setting targets

- Percentage of eligible transactions acknowledged by the ERP without manual intervention
- Rejection and retry rates by normalized reason
- Time from approval to ERP acknowledgement, segmented by market and transaction type
- Age and volume of unresolved exceptions
- Duplicate records prevented and reconciliation mismatches found

Targets should be set only after a reliable baseline and agreement on which transaction types are in scope.

## Decisions I would validate with Engineering, Finance, and Operations

- Which system is authoritative for supplier, tax, currency, and status fields?
- Which supported interface and delivery guarantee fit the ERP and integration platform?
- Which field changes require re-approval, and who may resolve or override an exception?
- How do Brazil and Mexico differ in legal entity, tax, currency, and invoice handling?
- What retention, access, and audit requirements apply to transaction and error data?

## What this demonstrates

Technical product thinking across system boundaries, workflow states, data contracts, idempotent recovery, reconciliation, controls, exception ownership, observability, acceptance criteria, and outcome measurement—while making clear which design elements are proposed rather than historical facts.
