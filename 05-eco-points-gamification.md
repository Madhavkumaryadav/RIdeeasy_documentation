# 05 - Eco-Points and Gamification System

## Objective

Reward users for sustainable behavior and increase retention through measurable progress.

Eco-Points system ka goal hai users ko regular eco rides ke liye motivate karna aur app engagement ko long-term improve karna.

## Core Components

1. Points Calculation Engine
2. Eco-Points Wallet
3. Redemption Marketplace
4. Progress and analytics dashboard

## Points Engine Logic (Concept)

Base factors:
- distance in km
- vehicle type multiplier
- ride time efficiency
- green route selection

Bonus factors:
- larger shared EV usage
- off-peak optimized charging behavior
- station data contributions
- streak completion

Example formula:
points = basePerKm * km * vehicleMultiplier + bonusPoints

## Wallet Design

Wallet fields:
- currentBalance
- lifetimeEarned
- lifetimeRedeemed
- pendingPoints
- ledgerEntries

Ledger entry types:
- earned
- redeemed
- adjusted
- expired

## Redemption Options

- Ride discount coupons
- Priority booking perks
- Partner store rewards
- Charging fee reduction

## Gamification Features

- weekly streak bar
- monthly eco challenge
- badges by milestones
- leaderboard (optional and privacy-aware)

## Fraud and Integrity Controls

- anti-abuse checks on repeated micro-rides
- duplicate event prevention via event IDs
- manual adjustment controls for admins
- anomaly detection for unusual earning patterns

## Dashboard UX Requirements

Display:
- current points balance
- weekly earning trend
- redemption history
- progress to next reward tier

## KPI Suggestions

- average points earned per active user
- redemption conversion rate
- impact on monthly retention
- fraud-adjusted net reward cost
