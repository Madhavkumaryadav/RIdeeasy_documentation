# 16 - Open Questions and Assumptions

## Current Assumptions

1. Provided Flutter folder blueprint is the intended architecture baseline.
2. Payment stack will use Razorpay or Stripe based on business decision.
3. Rider/Station app may be separate app or role-enabled mode in one app.
4. AI recommendation engine will start with rule + model hybrid approach.
5. Eco-Points and Green Credits may remain separate but linked systems.

## Open Product Questions

1. Should Eco-Points and Green Credits be merged into one currency?
2. What is the exact plan catalog and per-plan entitlement matrix?
3. Which features are subscription-only vs pay-per-use accessible?
4. What is the first pilot city and station partner strategy?

## Open Technical Questions

1. Monolith backend first or microservice-first rollout?
2. Preferred event bus and queue strategy?
3. Real-time stack choice for live ride and station updates?
4. Offline-first behavior requirements for low network zones?

## Open Governance Questions

1. Data retention policy duration by data class?
2. Fraud operations team ownership and escalation workflow?
3. Audit log retention and access policy?

## Code Sync Tasks (When Source Code Is Added)

1. map each doc section to actual file references.
2. add API endpoint contracts and request/response examples.
3. include sequence diagrams from implemented workflows.
4. attach test strategy and coverage checkpoints.
5. validate assumptions against real implementation constraints.

## Decision Log Starter

Use this section as a living ADR (architecture decision record) seed.

Suggested fields:
- Decision ID
- Date
- Owner
- Context
- Chosen Option
- Alternatives
- Consequences
