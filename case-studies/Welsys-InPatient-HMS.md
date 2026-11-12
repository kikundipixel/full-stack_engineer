# Welsys InPatient HMS

**A Kenya DHA/SHA-compliant inpatient hospital management system**, built on the CARE engine with HAPI FHIR as the canonical FHIR repository.

## Stack

Python, Django on the vendored CARE engine · HAPI FHIR · Keycloak · PostgreSQL · Nginx · Docker Compose · n8n · FOSSBilling.

## What I built

Sole developer and architect. I forked and extended upstream CARE rather than starting from a blank page, so the work was integration and productisation, not a rewrite.

- **Keycloak authentication** and role-based access across clinical and administrative roles.
- **FOSSBilling subscription gating** and whitelabelling, so the same codebase serves more than one facility brand.
- **Kenya MoH service catalogue** and **KES pricing**, mapped into the billing surfaces.
- **FHIR-native** on HAPI FHIR as the canonical repository.
- **267 tests**, CI and Docker.

## Engineering notes

Extending an existing clinical system is mostly a boundary problem. Upstream CARE owns the clinical model; the fork owns tenancy, branding, subscription state and local pricing. Every change had to be made on the correct side of that boundary, or the next upstream merge becomes a rewrite.

The regulated part is the catalogue and the price. If sales quote a tier the app does not enforce, or finance sees a price the catalogue does not contain, the product is wrong even when the feature works. That is why the subscription gate and the pricing table were built and tested together, with 267 tests covering the tenant and catalogue surfaces.

## Code access

The repository is private because it contains client data. I can demonstrate the login, the service catalogue and pricing, and the test run on a call, or share a recording.
