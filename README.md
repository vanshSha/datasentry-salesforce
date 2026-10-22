# DataSentry Enterprise

**DataSentry Enterprise** is a Salesforce-centered data quality, governance, and reliability platform.

Its purpose is to identify incomplete, invalid, outdated, and potentially duplicated CRM data, manage findings, govern corrective actions, and track data quality over time.

## Project Architecture

The product will use two separate repositories:

| Repository              | Responsibility                                                                                        |
| ----------------------- | ----------------------------------------------------------------------------------------------------- |
| `datasentry-salesforce` | Salesforce DX, Lightning Web Components, Apex, Salesforce metadata, permissions, and Salesforce tests |
| `datasentry-service`    | Java, Spring Boot, Apache Kafka, PostgreSQL, external event processing, and analytics                 |

The repositories will be integrated through authenticated APIs and Salesforce change events when the relevant phases are implemented.

## Development Roadmap

### MVP — Salesforce Core

- Requirements and project planning
- Development environment and project foundation
- Salesforce data model and security
- Rule Studio and data-quality rule engine
- Scan orchestration and background processing
- Findings Workbench
- Governed remediation and audit
- Salesforce dashboards and reporting
- Core testing and verification

### V2 — Event-Driven Integration

- Spring Boot integration foundation
- Salesforce Change Data Capture and Pub/Sub API
- Apache Kafka event processing and recovery

### V3 — Analytics and Production Readiness

- PostgreSQL analytics
- Quality trends and anomaly detection
- OpenTelemetry and monitoring
- Security and performance hardening
- CI/CD and deployment documentation

## Salesforce Development Prerequisites

- Salesforce CLI
- VS Code with Salesforce extensions
- Node.js and npm
- An authenticated Salesforce development org

## Setup

Install the project dependencies from the repository root:

```bash
npm ci
```

Verify the Salesforce CLI and authenticated orgs:

```bash
sf --version
sf org list
```

## Validation Commands

Run the available project checks:

```bash
npm test
npm run lint
npm run prettier:verify
```

The generated LWC Jest test is currently a placeholder. Passing it confirms the test runner works, but meaningful component behavior tests still need to be implemented.

## Salesforce Deployment

Deploy the starter component to the development org:

```bash
sf project deploy start \
  --source-dir force-app/main/default/lwc/dataSentryHome \
  --target-org DEV \
  --wait 10
```

Confirm that `DEV` is the intended target before deploying.

## Current Implementation Status

- Salesforce DX project initialized.
- Git repository initialized on `main`.
- Starter LWC `dataSentryHome` generated and deployed to `DEV`.
- npm dependencies installed.
- Jest, ESLint, and Prettier checks executed successfully.
- Salesforce data-quality functionality has not yet been implemented.

## Development Principles

- Salesforce remains the source of truth for CRM records.
- Remediation must respect Salesforce authorization and validation.
- External processing must handle retries and duplicate event delivery safely.
- Sensitive credentials must not be committed to Git.
- Each phase must be verified before proceeding to the next.

## Audit Retention Policy

- **Scope:** DataSentry audit records stored in `DQAudit__c`.
- **Retention target:** 12 months from the audit timestamp for the MVP.
- **Deletion:** No automatic deletion is implemented in the MVP.
- **Access:** Audit records should be readable by authorized users and protected from unauthorized modification or deletion.
- **Audit fields:** Record the action, related object, related record ID, acting user, timestamp, and relevant details.
- **Data minimization:** Avoid storing passwords, credentials, or unnecessary sensitive data in audit details.
- **Review:** Confirm the retention period against applicable legal, regulatory, contractual, and business requirements before production deployment.

**Status:** Proposed MVP policy; production approval pending.
