# 04 - Subscriptions and Payments

## Objective

Build a flexible monetization engine with:
- Monthly subscriptions (INR 1500 to 5000)
- Auto-renewal and expiration handling
- Pay-per-use alternative
- Secure transaction lifecycle

## Payment Gateway Integration

Supported gateway strategy:
- Primary: Razorpay or Stripe
- Optional fallback provider for resilience

Integration requirements:
- Tokenized payment methods
- Webhook verification
- Idempotent transaction processing
- Refund and dispute workflow

## Subscription Model

Plan examples:
- Starter
- Commuter
- Pro
- Enterprise

Plan controls:
- Feature limits
- Ride quotas or discounts
- Recharge benefits
- Wallet multipliers

## Billing Lifecycle

1. Plan selected.
2. Payment authorization.
3. Subscription activated.
4. Renewal reminder.
5. Renewal attempt.
6. Grace period handling.
7. Expiration and permission downgrade.

## Pay-Per-Use Model

Use case:
- users who do not commit to monthly plans.

Logic:
- per ride base fee
- dynamic add-ons
- convenience and service charge
- optional premium support fee

## Failure Handling

Payment failure scenarios:
- authorization failed
- insufficient balance
- network timeout
- webhook delay

Response actions:
- mark payment pending or failed
- temporary permission hold logic
- retry orchestration
- user notification and clear recovery CTA

## Data Records (Concept)

- SubscriptionPlan
- UserSubscription
- PaymentMethod
- PaymentTransaction
- Invoice
- RefundRecord

## Security and Compliance

- Never store raw card data.
- Verify gateway signatures.
- Encrypt sensitive payment metadata.
- Full transaction audit for finance and support.

## KPI Suggestions

- MRR and ARR growth.
- Renewal success rate.
- Payment failure recovery rate.
- Churn by plan.
- Share of pay-per-use revenue.
