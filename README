# Project Documentation: Elite Financial Monitoring Dashboard

## 1. Executive Summary
The **Elite Financial Monitoring Dashboard** is a state-of-the-art, real-time analytics platform designed to monitor complex financial workflows (FTO processing, Bill generation, and Treasury approvals). Built for high-concurrency environments, it ensures data integrity for millions of users through a reactive, event-driven architecture.

---

## 2. Technical Ecosystem

### Core Technologies
- **Backend**: .NET 9+ (C#) Web API utilizing a Clean Architecture pattern.
- **Frontend**: Angular 19+ (Standalone, Signals-based state management).
- **Real-Time Engine**: SignalR with **MessagePack binary protocol** for high-efficiency broadcasting.
- **Database**: PostgreSQL with optimized batch query patterns.
- **Monitoring**: Real-time system resource tracking (CPU, RAM, DB Pressure).

### Architecture Diagram (High Level)
```mermaid
graph TD
    DB[(PostgreSQL)] --> DAL[Data Access Layer]
    DAL --> BLL[Business Logic Layer]
    BLL --> AggWorker[Dashboard Aggregation Worker]
    AggWorker --> Hub[SignalR Hub]
    Hub -- Binary Pulse --> UI[Angular Frontend]
    UI -- REST Request --> API[Controllers]
    API --> BLL
```

---

## 3. Key Technical Innovations

### 🔹 Split-Snapshot State Management
To prevent the common "dashboard flickering" or "reset to zero" issues during API/Socket race conditions, the system uses a **Dual-Signal State**:
1.  **Historical Base (Signal)**: The static total retrieved from the database via REST.
2.  **Live Overwrites (Signal)**: The high-frequency deltas/totals received via SignalR.
3.  **Computed Merge**: A derived signal that intelligently merges these two, ensuring the UI is always up-to-date without losing historical context.

### 🔹 Intelligent Scoped Broadcasting
The SignalR implementation is **Group-Scoped** to ensure data privacy and performance:
- **`Admin`**: Global view of all system metrics.
- **`DDO:{Code}`**: Metrics filtered for specific Drawing and Disbursing Offices.
- **`Operator:{Id}`**: Personal performance and task metrics.

### 🔹 Adaptive Context Engine
The system dynamically shifts its logic based on the user's selected time range:
- **Financial Year (FY)**: Aggregated long-term trends.
- **Quarterly/Monthly**: Drill-down performance.
- **Daily (Live)**: Activates the "Real-Time Pulse" mode with micro-animations.

---

## 4. Directory Structure Overview

### 📂 `/api` (Backend)
- **`PL` (Presentation Layer)**: Controllers, SignalR Hubs, and Background Workers.
- **`BLL` (Business Logic)**: Services for fiscal utilities, simulations, and core workflow logic.
- **`DAL` (Data Access)**: Repositories and Entity Framework Core configurations.

### 📂 `/ui` (Frontend)
- **`src/app/core/`**: Shared infrastructure (SignalR client, Interceptors, Auth).
- **`src/app/features/dashboard/`**:
    - `main/`: The primary KPI grid and charting logic.
    - `system-pressure/`: Real-time health monitoring visualizers.

---

## 5. System Features
- **Real-Time KPIs**: FTOs Received/Processed, Bills Generated, Treasury Forwarded, Rejections.
- **Micro-Animations**: KPI cards "flash" when a SignalR update is applied to provide visual feedback.
- **System Health**: Monitoring of server load to ensure the monitoring system itself isn't under stress.
- **Secure Auth**: JWT-based authentication with SignalR handshake integration.

---

## 6. Development Workflow
1.  **Backend Development**: Focus on optimized SQL and efficient broadcasting.
2.  **Frontend Development**: Prioritize "Signals" for reactive UI performance and PrimeNG for premium aesthetics.
3.  **Testing**: Validation of data consistency during high-frequency simulation cycles.
