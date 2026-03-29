# 12 - Data Models and State Contracts (Conceptual)

## Objective

Define conceptual entities and lifecycle states for core platform operations.

Yeh models engineering aur product dono teams ko shared data language dete hain.

## Core Entities

1. User
- id
- role
- authMethods
- profileStatus
- organizationId (optional)

2. Vehicle
- id
- type
- batteryLevel
- location
- availabilityStatus

3. Booking
- id
- userId
- vehicleId
- destination
- tripType
- bookingStatus
- pricingEstimate

4. RideSession
- id
- bookingId
- startTime
- endTime
- routeSummary
- distance
- status

5. SubscriptionPlan
- code
- name
- monthlyPrice
- benefits
- eligibilityRules

6. UserSubscription
- id
- userId or organizationId
- planCode
- status
- renewalDate
- expiryDate

7. PaymentTransaction
- id
- purpose (subscription/ride/add-on)
- amount
- status
- gatewayRef
- failureCode

8. EcoWallet
- userId
- currentBalance
- lifetimeEarned
- lifetimeRedeemed

9. EcoPointLedgerEntry
- id
- userId
- amount
- entryType
- sourceEventId
- timestamp

10. BatteryShareSession
- id
- requesterId
- providerType
- stationId or riderId
- status
- settlementStatus

11. StationNode
- id
- ownerId
- location
- loadStatus
- avgChargeSpeed
- reliabilityScore

## Key State Transitions

Booking:
requested -> confirmed -> active -> completed
requested -> expired
active -> cancelled (with policy checks)

RideSession:
initialized -> started -> in_progress -> ended -> settled

PaymentTransaction:
created -> authorized -> captured
created -> failed
authorized -> refunded (optional)

UserSubscription:
trial -> active -> grace -> expired
active -> cancelled

BatteryShareSession:
requested -> matched -> in_progress -> completed
requested -> failed

## Integrity Rules

- one active ride per vehicle at a time.
- payment settle required before benefit unlock where applicable.
- wallet ledger entries are append-only.
- all financial adjustments require audit references.

## Future Code Sync Placeholder

After actual implementation, add:
- JSON schema references
- DTO and mapper links
- API endpoint mapping
- migration/version strategy
