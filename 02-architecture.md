# 02 - System Architecture

## Architecture Summary

RideEasy uses a layered architecture with client apps, backend services, and external integrations.

RideEasy ka architecture modular hoga jisme user-facing apps aur backend intelligence components clearly separated honge.

## Primary Components

1. User App (Flutter)
- Ride booking
- Tracking
- Wallet and rewards
- Profile and settings

Implementation reference:
- docs/18-user-app-implementation.md

2. Rider/Station App (Future or parallel app)
- Charging and battery swap operations
- Partner earnings and task management
- Station availability updates

3. Admin Dashboard (Web)
- User/customer operations
- Subscription governance
- Incident and fraud monitoring
- Ecosystem analytics

4. Customer Portal (Web)
- Bulk user onboarding
- Plan management
- Organization billing and usage tracking

5. Backend Services
- Authentication and identity
- Booking and ride orchestration
- Payment and subscription management
- Wallet and eco-points ledger
- Recommendation and AI optimization engine
- EV station and battery network service

6. External Systems
- Google Maps APIs
- Payment gateway (Razorpay or Stripe)
- Firebase services
- Notification channels
- Weather and traffic providers

## High-Level Flow

1. User authenticates via email/Google/phone OTP.
2. User requests ride and receives vehicle options from nearby pool.
3. Booking is created and pricing/energy estimates are generated.
4. During ride, GPS and telemetry update route and ETA.
5. End ride triggers billing, payment settlement, and eco-point award.
6. Wallet and rewards are updated.
7. Optional energy recommendation or battery swap suggestion is delivered.

## RBAC and Tenancy Model

Roles:
- IndividualUser
- CustomerAdmin
- CustomerMember
- RiderPartner
- StationOwner
- PlatformAdmin
- SupportAgent

Tenancy:
- Individual users are standalone accounts.
- Customer users are organization-scoped.
- Admin and support have elevated system-level permissions with audit trail.

## Core Non-Functional Requirements

- Security: strong auth, OTP controls, payment integrity.
- Reliability: graceful failure handling for payment/maps/network.
- Scalability: modular services with queue/event support.
- Observability: audit logs, metrics, and anomaly alerts.
- Compliance: data protection and retention policies.

## Suggested Backend Services (Conceptual)

- Identity Service
- User Profile Service
- Organization/Bulk Subscription Service
- Booking Service
- Ride Tracking Service
- Billing & Payment Service
- Eco-Points Wallet Service
- Station & Battery Exchange Service
- AI Recommendation Service
- Notification Service

## Integration Contracts (Conceptual)

- BookingCreated
- RideStarted
- RideEnded
- PaymentAuthorized
- PaymentFailed
- SubscriptionActivated
- SubscriptionExpired
- EcoPointsAwarded
- BatterySwapRequested
- StationLoadUpdated

Yeh event contracts future microservice expansion me help karenge.

## User App Implementation Entry

User App implementation tasks, layered app architecture, and end-to-end workflows are documented in:
- docs/18-user-app-implementation.md
