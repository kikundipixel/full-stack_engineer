# Tibika Referral Engine

**A referral engine that carries a patient between care organisations** without becoming the system of record for clinical notes.

## Stack

React 18, TypeScript, Vite · Express, Drizzle ORM, PostgreSQL (Neon) · Anthropic SDK · Stripe, Polar · AWS S3, Africa's Talking SMS · native Android (Kotlin) and iOS clients · Docker, CI, ADRs and API specs.

## What I built

Sole developer and architect.

- **Referral flow across organisations:** one patient, two care providers, one shared identity — and a clear rule that the referral engine never owns the clinical record.
- **FHIR-based data exchange** with the surrounding platform.
- **LLM integration** (Anthropic SDK) for the referral narrative, alongside Stripe and Polar payments, AWS S3 document storage and Africa's Talking SMS notifications.
- **Native Android (Kotlin) and iOS clients** on the same API contract as the web app.
- **29 tests**, Docker, CI, plus architecture decision records and API specs.

## Engineering notes

The scope decision was the design: a referral system that quietly accumulates clinical notes becomes a second source of truth, and then every reconciliation problem in the network lands on it. I kept it as a courier — it holds the referral, the state and the participants, and it links to the clinical record rather than copying it.

Mobile was not a separate product. The Android and iOS clients consume the same endpoints as the web app, which forced the API contract to be explicit early — and made the ADRs worth writing.

## Code access

The repository is private because it contains client data. I can walk through the referral state machine, the API spec and the mobile client contract on a call.
