# MedRoute — Symptom Triage & Specialist Booking Assistant

**Project:** MedRoute — conversational assistant that routes patients to the right medical specialist via guided symptom triage, and manages the resulting appointment request between patient and doctor — including doctor-to-doctor referral.

**Context:** Clickatell 1-Month AI Bootcamp — Week 1 (AI Foundations & Chatbot Development)
**Author:** Freddy Thosago · September 2026
**Live prototype:** https://tshepisofrominnostation.github.io/medroute-triage/

---

## What it is (and is NOT)

MedRoute is structurally a **ride-hailing marketplace**: patients request, doctors accept / decline / redirect. It is **not a diagnostic tool**.

- ✅ Classifies symptoms into a **specialty category**
- ✅ Facilitates booking between patient and doctor (with referrals)
- ❌ Never states a diagnosis (BR-2)
- ❌ Never recommends treatment or replaces a consultation

## Use cases implemented

| Use Case | Flow | Status |
|---|---|---|
| **UC-01** Triage & Request Appointment | Category → duration → severity → specialty match → doctor shortlist → slot request → Pending booking | ✅ |
| **UC-02** Doctor Responds to Booking | Doctor dashboard: Accept → Confirmed, or Refer → new Pending booking (chained, context carried) | ✅ |
| **AF-01** Emergency Symptoms Detected | Red-flag screening on chest/heart & neurological paths halts triage, shows emergency notice, no booking offered | ✅ |
| **AF-02** Doctor Refers Booking | Referred → new Pending record with full triage context + referral chain history (BR-4) | ✅ |

## Business rules enforced

- **BR-1** Bookings only offered for doctors whose specialty matches the triage outcome
- **BR-2** The system states a specialty recommendation, never a diagnosis (persistent disclaimer strip)
- **BR-3** Every unresolved Pending booking stays visible to the patient ("My Bookings" panel)
- **BR-4** A referral always creates a new bookable record — the patient's request is never silently dropped
- **BR-5** Referral chains are not artificially limited, but an admin alert is surfaced at ≥ 3 referrals

## How to demo (2 minutes)

1. **Patient Chat tab** — enter a first name, pick a category (try `❤️ Chest / Heart` first)
2. If you answer the red-flag screening with an emergency symptom → **AF-01 emergency notice**, triage halts
3. Choose "None of these", finish triage → pick a doctor → pick a slot → booking created as **Pending**
4. **Doctor Dashboard tab** — switch to the receiving doctor, **Accept** (→ Confirmed) or **Refer** to any other registered doctor (→ Referred + new Pending, chain +1)
5. Watch the patient's "My Bookings" panel update with the full event history

## Tech

- Single-page prototype: HTML + CSS + vanilla JavaScript (no framework, no build step)
- State machine-driven chatbot with typing indicator and quick-reply buttons
- Booking engine with localStorage persistence for the demo session
- 14 mock doctors across 7 specialties (Johannesburg metro), static slots/locations
- No patient medical history captured; triage answers live only for the session

## Future extension (Week 2+)

Replace the guided button flow with free-text symptom description using an LLM classifier scoped **strictly to category mapping** (see `medroute-prompt-library.md`). The triage, booking, and referral logic described in the use case remains unchanged. A production version would integrate a live scheduling backend, authentication, and a referral-chain cap with admin alerting.

---

*MedRoute Prototype · Clickatell AI Bootcamp · Mock data only — not a medical device.*
