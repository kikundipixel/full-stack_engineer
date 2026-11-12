# RxPoa Pharmacy Dashboard

**Clinical-to-operational pharmacy platform for Kenyan pharmacies.** Bridges FHIR prescriptions into ERPNext inventory, billing and CRM.

## Stack

Python 3.12, FastAPI, SQLAlchemy 2.0 (async), Alembic, PostgreSQL, Redis · React 19, Vite, TypeScript · Docker Compose (local), Kubernetes (production) · Keycloak OIDC, Stripe, M-Pesa (Daraja API), SNOMED CT, Snowstorm FHIR API.

## What I built

Sole developer and architect, end to end.

- **FHIR bridge** connecting prescriptions to ERPNext inventory, billing and CRM — three systems that shared neither a data model nor an identity model.
- **Payments** with M-Pesa (Daraja API) and Stripe, reconciled against the ERPNext stock ledger. Traced the `Stock Entry` and `Sales Invoice` schemas and queried a live site, because stock is not a field you update — it is the sum of voucher movements.
- **Terminology** via the Snowstorm FHIR API. The item master is keyed on SNOMED CT codes, while the regulatory identity in Kenya is the PPB registration number, which contains slashes (`H2022/CTD7340/14438`). I wrote the mapping decision down, named a single enforcement point, and reviewed it with the ERPNext implementer before work started.
- **Security and operations:** Keycloak OIDC, FHIR partitioning chosen server-side from the JWT so the client cannot pick its own partition, Prometheus metrics, Alembic migrations, Docker Compose to Kubernetes.

## Engineering notes

The hard part was not the API call. It was making "dispense" mean the same thing in four places: the pharmacy's stock, the invoice, the payment and the regulatory record. Each had a different identifier and a different owner. The design decision that unlocked it was separating *regulatory identity* (PPB) from *integration identity* (SNOMED), then enforcing that boundary at one point in the code instead of scattering checks.

## Code access

The repository is private because it contains client data. I am happy to walk through the architecture, the schema and the reconciliation logic on a call, or share a recorded demo.
