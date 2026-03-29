# 01 - Project Structure Guide

## Purpose

This document explains the planned Flutter project structure and responsibilities.

Yeh guide define karta hai ki kaunsa module kis kaam ke liye responsible hoga.

## Top-Level Layout

- android/ and ios/: platform-specific configuration and builds.
- lib/: main application source code.
- pubspec.yaml: dependency and asset definitions.
- README.md: project overview and docs index.

## lib/main.dart

- Application entry point.
- Initializes theme, providers, and route configuration.

## lib/core/

- app_routes.dart: centralized navigation map.
- app_theme.dart: design tokens and global theme system.
- constants.dart: static keys, limits, plan codes, and enums.
- utils.dart: shared helpers (formatting, validation, conversions).
- providers/: cross-feature state providers.

### core/providers

- auth_provider.dart: auth state, session, and role context.
- weather_provider.dart: weather warnings and location weather state.
- ride_provider.dart: active ride, booking lifecycle, and updates.

## lib/models/

Domain entities used across app layers:
- user_model.dart
- vehicle_model.dart
- booking_model.dart
- weather_alert_model.dart
- safety_event_model.dart

## lib/services/

Backend and integration boundaries:
- firebase_service.dart: backend bootstrap and SDK wrappers.
- auth_service.dart: login/register, OTP, token lifecycle.
- weather_service.dart: weather alert fetch and normalization.
- notification_service.dart: push and in-app notifications.
- map_service.dart: maps, routes, markers, ETA interactions.
- payment_service.dart: subscriptions, one-time transactions, webhooks.
- storage_service.dart: local persistence and cache abstraction.

## lib/screens/

Feature-first UI organization:
- auth/
- home/
- alerts/
- rides/
- profile/

Each feature may include:
- screen widgets
- dedicated widgets/
- controllers/
- feature-local models/ (if needed)

## lib/widgets/

Reusable global components:
- custom_button.dart
- custom_textfield.dart
- loading_indicator.dart
- error_dialog.dart

## Recommended Layer Rules

1. Screens call providers/controllers, not direct raw SDK code.
2. Providers orchestrate use-cases and call services.
3. Services isolate external integrations.
4. Models remain framework-light and serializable.
5. Shared widgets avoid business logic.

## Future Structure Extensions

Suggested additions for scale:
- lib/features/<feature>/domain
- lib/features/<feature>/data
- lib/features/<feature>/presentation
- lib/core/di for dependency injection
- lib/core/errors for typed failures

Yeh extensions large team development me maintainability improve karenge.
