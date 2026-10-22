# Illustrative Coupa Workflow and User Stories

> **Portfolio sample — reconstructed, not an original Coupa configuration or FARFETCH specification.**
> This artifact is a high-level illustration based on verified project scope. The process details, user stories, and acceptance criteria below are examples created for this portfolio and do not disclose internal configuration or controls.

## Verified retrospective context

The Coupa implementation supported LATAM spend management in Brazil and Mexico. The work covered requirements and business rules across procurement and finance workflows, Delegation of Authority approvals, D365 ERP integration, tax, Finance and Accounts Payable, Amazon PunchOut, sourcing, purchase orders, receiving, and invoices.

The product and implementation effort connected procurement to Finance. This summary describes product and process coordination; it does not claim sole ownership of configuration, architecture, or implementation. No verified savings or cycle-time impact is claimed.

## Illustrative high-level workflow

1. **Discover and request:** an employee identifies a business need and creates a purchase request.
2. **Review and approve:** the request follows applicable business rules and approval authority.
3. **Source and order:** the request uses an appropriate sourcing or catalog path, including PunchOut where applicable, and results in a purchase order.
4. **Receive:** the business records receipt of goods or services.
5. **Invoice and pay:** invoice and tax information flow through the agreed Finance and Accounts Payable process, with ERP integration dependencies.

This is a simplified process view. Actual routing and system behavior depend on organization-specific policies, configuration, and local requirements.

## Example user stories

### Purchase request and approval

**As an employee,** I want to submit a purchase request with the information required by my organization, **so that** the request can be reviewed and approved before an order is placed.

**Illustrative acceptance criteria**

- The request captures required business, supplier or catalog, amount, and accounting information.
- Missing required information is identified before submission.
- The request is routed according to configured approval rules.
- The requester can see the request status and next action.

### PunchOut catalog purchase

**As a requester,** I want to select items from an approved supplier catalog and return them to my purchase request, **so that** the selected items can follow the organization’s review and approval process.

**Illustrative acceptance criteria**

- The requester can open an available supplier catalog from the procurement experience.
- Selected item details return to the request for review.
- The requester can correct or remove items before submission.
- Catalog or return failures provide a clear recovery path and do not silently submit an incomplete request.

### Invoice and finance handoff

**As an Accounts Payable partner,** I want approved purchase and receiving context available with invoice information, **so that** I can perform the agreed invoice review and finance processing steps.

**Illustrative acceptance criteria**

- The invoice can be associated with the relevant purchase order and receiving context where applicable.
- Exceptions such as missing or inconsistent information are visible to the responsible team.
- Required tax and finance fields are handled according to local process requirements.
- Integration errors can be identified and routed for resolution.

## Integration and delivery considerations

- Confirm the system-of-record boundary between Coupa and D365 for relevant data.
- Align Finance and Accounts Payable on invoice, tax, and exception handling needs.
- Validate local requirements for Brazil and Mexico with the appropriate specialists.
- Include sourcing, receiving, and approval dependencies in end-to-end testing.
- Define ownership and escalation paths for integration failures and data issues.

## Example outcome measures to define

These are illustrative measurement ideas only; no results are asserted:

- Request completion and return rates
- Approval turnaround time by request type
- Purchase order creation success and exception rates
- Invoice match or exception rates
- Integration error volume and resolution time
- Requester and Finance/AP feedback

Measurement definitions should account for process differences, local rules, baseline quality, and data availability before setting targets.

## Evidence boundary

The verified scope above summarizes project domains and integrations at a high level. The workflow, personas, user stories, acceptance criteria, and measurement ideas are reconstructed examples, not original requirements, Coupa settings, architecture, or proof of implemented behavior.
