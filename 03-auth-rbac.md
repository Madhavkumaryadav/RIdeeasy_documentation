# 03 - Multi-Tier Authentication and RBAC

## Objective

Implement secure authentication and authorization for:
- Individuals
- Business/University customers
- Platform admins

Target: har user type ko uske use-case ke according optimized login, onboarding, aur permissions milen.

## Authentication Methods (Individual)

1. Email + Password
- Sign-up with verification.
- Password reset and session controls.

2. Google Sign-In
- OAuth-based quick onboarding.
- Account linking with existing email account.

3. Phone OTP
- OTP rate limiting.
- Device and session risk checks.

## Customer Portal Onboarding (B2B)

Flow:
1. Organization registration request.
2. KYC or institutional verification.
3. Customer admin account activation.
4. Bulk user import (CSV/API).
5. Plan assignment and usage controls.

## Admin Dashboard Access

- Separate admin identity domain.
- Mandatory MFA for platform admins.
- Access logs and sensitive action audit trail.

## RBAC Matrix (Concept)

- IndividualUser: ride booking, wallet, redemption, history.
- CustomerAdmin: org users, subscriptions, billing reports.
- CustomerMember: org-assigned rides and personal dashboard.
- RiderPartner: ride participation, energy sharing actions, earnings.
- StationOwner: station status, swap inventory, settlement reports.
- SupportAgent: limited customer support actions.
- PlatformAdmin: full governance and compliance controls.

## Authorization Principles

1. Default deny policy.
2. Least privilege by role.
3. Organization scope isolation.
4. Sensitive operations require step-up verification.
5. All role changes are audited.

## Security Controls

- OTP abuse prevention (cooldown, IP/device heuristics).
- Token rotation and session revocation.
- Account lockouts with recovery flow.
- Suspicious login alerting.

## Suggested Implementation Components

- auth_service.dart: provider integration and token lifecycle.
- auth_provider.dart: current user + role context.
- middleware/policy engine (backend): permission evaluation.
- admin audit pipeline: log retention and query.

## Success Metrics

- Login success rate.
- OTP delivery success and abuse rate.
- Unauthorized action rejection rate.
- Time-to-onboard for customer organizations.
