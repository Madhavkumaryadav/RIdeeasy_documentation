# 17 - Architecture Diagrams

## Purpose

Visual representations of RideEasy system architecture, data flows, and key processes for better understanding across all team members.

Yeh diagrams architecture ke complex concepts ko simple visual format me represent karte hain.

---

## 1. System Architecture Overview

```mermaid
graph TB
    subgraph "Client Layer"
        UA["User App<br/>(Flutter)"]
        RA["Rider/Station App<br/>(Future)"]
        ADMIN["Admin Dashboard<br/>(Web)"]
        CP["Customer Portal<br/>(Web)"]
    end

    subgraph "API Gateway & Authentication"
        GW["API Gateway"]
        AUTH["Auth Service<br/>(JWT/OAuth)"]
    end

    subgraph "Core Services"
        US["User & Identity<br/>Service"]
        BS["Booking Service"]
        RS["Ride Tracking<br/>Service"]
        PS["Payment &<br/>Subscription Service"]
        WS["Wallet & Eco-Points<br/>Service"]
        ES["Energy Sharing<br/>& Battery Service"]
        REC["Recommendation<br/>Engine AI"]
        GRID["EV Grid<br/>Intelligence Service"]
    end

    subgraph "Data & State"
        DB["Primary Database"]
        CACHE["Cache Layer<br/>(Redis)"]
        QUEUE["Event Queue<br/>(for async ops)"]
    end

    subgraph "External Integrations"
        MAPS["Google Maps API"]
        PAY["Payment Gateway<br/>(Razorpay/Stripe)"]
        FIRE["Firebase<br/>(Notifications)"]
        WEATHER["Weather API"]
    end

    UA -->|Login, Ride, Booking| GW
    RA -->|Energy, Battery Ops| GW
    ADMIN -->|Governance, Analytics| GW
    CP -->|Org Management| GW
    
    GW -->|Route to Auth| AUTH
    AUTH -->|Verify Tokens| GW
    
    GW -->|Business Logic| US
    GW -->|Ride Operations| BS
    GW -->|Payment ops| PS
    GW -->|Wallet Access| WS
    GW -->|Energy Ops| ES
    GW -->|AI Advice| REC
    GW -->|Grid Data| GRID
    
    BS -->|Track Live| RS
    RS -->|Emit Events| QUEUE
    PS -->|Payment Status| QUEUE
    WS -->|Award Points| QUEUE
    ES -->|Battery Session| QUEUE
    
    QUEUE -->|Consume Events| WS
    QUEUE -->|Consume Events| REC
    QUEUE -->|Consume Events| GRID
    
    US --> DB
    BS --> DB
    PS --> DB
    WS --> DB
    ES --> DB
    RS --> CACHE
    
    BS -->|Route Planning| MAPS
    PS -->|Process| PAY
    UA -->|Push Notifications| FIRE
    REC -->|Weather Data| WEATHER
```

**Key Components:**
- All client apps route through API Gateway for centralized auth and routing.
- Backend services are independent and communicate via event queue for scalability.
- Real-time tracking uses cache layer for performance.
- Payment and wallet operations are fully audited and append-only.

---

## 2. Complete Ride Lifecycle

```mermaid
graph TD
    A["User Opens App"] --> B["Authenticates"]
    B --> C["Views Map with<br/>EV Vehicle Markers"]
    C --> D["Selects Vehicle &<br/>Destination"]
    D --> E["Booking Form<br/>Trip Type + Add-ons"]
    E --> F["AI Recommends<br/>Route & Energy Saving"]
    F --> G["Cost & Time<br/>Estimate Displayed"]
    G --> H{User Confirms?}
    H -->|No| I["Back to Map"]
    I --> C
    H -->|Yes| J["Payment Authorization"]
    J --> K{Payment Success?}
    K -->|Failed| L["Payment Error<br/>& Retry"]
    L --> J
    K -->|Success| M["Booking Confirmed<br/>Vehicle Reserved"]
    M --> N["Ride Starts<br/>Vehicle Unlocked"]
    N --> O["Live GPS Tracking<br/>Route Polyline & ETA"]
    O --> P["Real-time Updates<br/>Battery & Weather Alerts"]
    P --> Q{Ride Complete?}
    Q -->|Ongoing| O
    Q -->|Yes| R["Auto-Lock Vehicle"]
    R --> S["Calculate Final Bill"]
    S --> T["Payment Settlement"]
    T --> U["Award Eco-Points"]
    U --> V["Generate Receipt"]
    V --> W["Suggest Battery<br/>or Swap Options"]
    W --> X["Update Dashboard<br/>& History"]
```

**Key Steps:**
1. Authentication and map discovery.
2. Vehicle selection with AI-powered energy recommendations.
3. Payment authorization before booking confirmation.
4. Live tracking with real-time alerts during ride.
5. Automated lock, billing, and rewards settlement at end.
6. Optional battery/swap suggestions and post-ride dashboard update.

---

## 3. Data Flow: Booking to Settlement

```mermaid
graph LR
    subgraph Input
        B["Booking<br/>Creation"]
    end
    
    subgraph Processing
        P1["Pricing Engine"]
        P2["Payment Gateway<br/>Transaction"]
        P3["Billing Service"]
    end
    
    subgraph Events
        E1["BookingCreated<br/>Event"]
        E2["PaymentAuthorized<br/>Event"]
        E3["RideEnded<br/>Event"]
        E4["BillingSettled<br/>Event"]
    end
    
    subgraph Ledgers
        L1["Payment<br/>Ledger"]
        L2["Eco-Points<br/>Ledger"]
        L3["User Wallet<br/>Balance"]
    end
    
    B --> P1
    P1 --> P2
    P2 --> P3
    P3 --> E1
    P2 --> E2
    E2 --> L1
    E3 --> P3
    P3 --> E4
    E4 --> L2
    L2 --> L3
    L1 --> L3
```

**Important Principles:**
- Every financial transaction generates audit events.
- Payment and Eco-Points ledgers are append-only.
- Wallet balance is derived from ledger entries (never directly mutable).
- Event-driven architecture ensures consistency across services.

---

## 4. Innovation Streams: Ecosystem Interactions

```mermaid
graph TB
    subgraph "Battery & Energy Network"
        BR["Rider<br/>Low Battery"]
        ES["Energy Sharing<br/>Match Engine"]
        SO["Station Owner<br/>Battery Inventory"]
        RP["Rider Partner<br/>with Spare Battery"]
    end
    
    subgraph "AI Optimization"
        RIDE["Active Ride"]
        AI["AI Route &<br/>Energy Advisor"]
        ROUTE["Optimized Route<br/>Recommendation"]
    end
    
    subgraph "Green Credits Economy"
        GC["Green Credits<br/>Earned"]
        PM["Partner<br/>Marketplace"]
        USER["User Redemption"]
    end
    
    subgraph "EV Grid Intelligence"
        CROWD["Crowdsourced<br/>Data"]
        MAP["Live Station<br/>Map & Load"]
        USERS["Users & Stations<br/>Contribute"]
    end
    
    BR --> ES
    ES --> SO
    ES --> RP
    SO --> BR
    RP --> BR
    
    RIDE --> AI
    AI --> ROUTE
    ROUTE --> RIDE
    
    RIDE --> GC
    GC --> PM
    PM --> USER
    USER --> GC
    
    USERS --> CROWD
    CROWD --> MAP
    MAP --> USERS
    
    RP -.->|Battery Availability| MAP
    SO -.->|Live Load| MAP
```

**Differentiator Features:**
- Energy Sharing Network: connects desperate users with available resources.
- AI Energy Advisor: learns and improves route recommendations over time.
- Green Credits: incentivize ecosystem participation.
- Crowdsourced EV Intelligence: creates network externality effects.

---

## 5. RBAC and Multi-Tenant Architecture

```mermaid
graph TD
    subgraph "Authentication Layer"
        AUTH["Identity Provider<br/>(AuthService)"]
    end
    
    subgraph "User Types"
        IND["Individual User"]
        ORG["Organization<br/>Admin"]
        ORG_MEM["Organization<br/>Member"]
        RIDER["Rider Partner"]
        STATION["Station Owner"]
        ADMIN["Platform Admin"]
    end
    
    subgraph "Role-Based Access"
        R_IND["Individual Scope<br/>- Ride Booking<br/>- Wallet<br/>- History"]
        R_ORG["Org Scope<br/>- Manage Members<br/>- Billing<br/>- Usage Analytics"]
        R_MEM["Member Scope<br/>- Assigned Rides<br/>- Personal Wallet"]
        R_RIDER["Partner Scope<br/>- Energy Ops<br/>- Earnings<br/>- Tasks"]
        R_STATION["Station Scope<br/>- Inventory<br/>- Commission<br/>- Analytics"]
        R_ADMIN["System Scope<br/>- User Governance<br/>- Finance<br/>- Compliance"]
    end
    
    subgraph "Multi-Tenant Data Isolation"
        TENANT1["Tenant 1<br/>Org A Data"]
        TENANT2["Tenant 2<br/>Org B Data"]
        SHARED["Shared Data<br/>Individual Users"]
    end
    
    AUTH --> IND
    AUTH --> ORG
    AUTH --> ORG_MEM
    AUTH --> RIDER
    AUTH --> STATION
    AUTH --> ADMIN
    
    IND --> R_IND
    ORG --> R_ORG
    ORG_MEM --> R_MEM
    RIDER --> R_RIDER
    STATION --> R_STATION
    ADMIN --> R_ADMIN
    
    R_ORG --> TENANT1
    R_MEM --> TENANT1
    R_IND --> SHARED
    R_RIDER --> SHARED
    R_STATION --> SHARED
```

**Security Model:**
- Every role has distinct permission boundaries.
- Organization data is strictly isolated.
- Admins have full audit trail visibility.
- Individual user data is cross-tenant accessible for shared services.

---

## 6. Payment & Subscription Workflow

```mermaid
graph TB
    subgraph "Subscription Path"
        SP1["User Selects Plan<br/>Starter/Commuter/Pro"]
        SP2["Add Payment Method"]
        SP3["Process Payment<br/>via Gateway"]
        SP4{Success?}
        SP5["Subscription Active<br/>Set Expiry"]
        SP6["Schedule Renewal<br/>Reminder"]
    end
    
    subgraph "Pay-Per-Use Path"
        PP1["User Books Ride"]
        PP2["Calculate Per-Ride Fee"]
        PP3["Authorize Payment"]
        PP4{Success?}
        PP5["Capture at Ride End"]
        PP6["Update Balance"]
    end
    
    subgraph "Renewal & Expiry"
        REN1["Renewal Date Reached"]
        REN2["Attempt Auto-Renewal"]
        REN3{Success?}
        REN4["Grace Period"]
        REN5["Downgrade Permissions"]
        REN6["Notify User"]
    end
    
    subgraph "Payment Gateway"
        GW["Razorpay/Stripe"]
        VERIFY["Verify Signature"]
        WEBHOOK["Webhook Callback"]
    end
    
    SP1 --> SP2
    SP2 --> SP3
    SP3 --> GW
    GW --> VERIFY
    VERIFY --> SP4
    SP4 -->|Yes| SP5
    SP4 -->|No| SP2
    SP5 --> SP6
    SP6 --> REN1
    
    PP1 --> PP2
    PP2 --> PP3
    PP3 --> GW
    GW --> PP4
    PP4 -->|Yes| PP5
    PP4 -->|No| PP1
    PP5 --> PP6
    
    REN1 --> REN2
    REN2 --> GW
    GW --> WEBHOOK
    WEBHOOK --> REN3
    REN3 -->|Yes| SP5
    REN3 -->|No| REN4
    REN4 --> REN5
    REN5 --> REN6
```

**Critical Flows:**
- Subscription user gets recurring billing with grace period for failures.
- Pay-per-use user gets authorization hold and capture at ride completion.
- Renewal failures trigger grace period, then permission downgrade.
- All flows verify gateway signatures to prevent fraud.

---

## Diagram Usage Guide

- **System Architecture**: Share with new team members and stakeholders for high-level understanding.
- **Ride Lifecycle**: Reference for QA testing and edge case identification.
- **Data Flow**: Essential for backend engineers implementing payments and wallet operations.
- **Innovation Streams**: Present to product and business teams to understand differentiator complexity.
- **RBAC**: Use during permission audit and access review cycles.
- **Payment Workflow**: Critical for payment operations and finance reconciliation.

---

## Notes for Implementation

When actual code is added:
1. Add sequence diagrams for specific error recovery scenarios.
2. Map each service to actual microservice repository.
3. Add real-time event schema definitions.
4. Create deployment topology diagrams for DevOps planning.
5. Document failure mode scenarios for each critical path.
