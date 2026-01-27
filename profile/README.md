<p align="center">
    <img src="../assets/logo.png" alt="The Beyond Logo" />
</p>

Distributed proxy service with centralized management and scalable edge nodes.

[![Docker](https://img.shields.io/badge/Docker-%231D63ED.svg?style=for-the-badge&logo=docker&logoColor=white)](https://docker.com)
[![Go](https://img.shields.io/badge/Go-%2300ADD8.svg?style=for-the-badge&logo=go&logoColor=white)](https://go.dev)
[![Postgresql](https://img.shields.io/badge/PostgreSQL-%23326791.svg?style=for-the-badge&logo=postgresql&logoColor=white)](https://postgresql.org)
[![gRPC](https://img.shields.io/badge/gRPC-%232DA6B0.svg?style=for-the-badge)](https://grpc.io)

---

## 🏗️ High-Level Architecture

The system architecture is based on the **Separation of Control and Data Plane** principle. This decoupling allows for a highly resilient central management system and horizontally scalable edge nodes.

```mermaid
graph TD
    User((User))
    Admin((Admin))

    subgraph Interfaces [Client Interfaces]
        Bot[Telegram Bot]
        App[Application]
        AdminPanel[Admin Panel]
    end

    subgraph ControlPlane [Control Plane]
        API[Open API]
        DB[(PostgreSQL)]
    end

    subgraph DataPlane [Data Plane]
        Agent[Node Agent]
        Xray[Xray-core]
    end

    User --> Bot
    User --> App
    Admin --> AdminPanel

    Interfaces <--> API
    API <--> DB

    API -- "gRPC (Commands & Telemetry)" --> Agent
    Agent -- "Manage / Stats" --> Xray

    User -.->|VPN Traffic| Xray
```

# 🧩 System Components

| Layer             | Module           | Description                                                                                                                      | Status                                                                              |
|:------------------|------------------|:---------------------------------------------------------------------------------------------------------------------------------|:------------------------------------------------------------------------------------|
| **Control Plane** | **Open API**     | API for user management and node orchestration.                                                                      | ![in_progress](https://img.shields.io/badge/in_progress-%23FF0?style=for-the-badge) |
| **Control Plane** | **Telegram Bot** | Interface for subscriptions and account management.                                                                            | ![planned](https://img.shields.io/badge/planned-%23EEE?style=for-the-badge)         |
| **Data Plane**    | **Node Agent**   | Manages local Xray instances and reports stats.                                                                                  | ![planned](https://img.shields.io/badge/planned-%23EEE?style=for-the-badge)         |
| **Data Plane**    | **Xray-core**    | Proxy engine for traffic routing and obfuscation.                                                               | ![ready](https://img.shields.io/badge/ready-%2300FFFF?style=for-the-badge)          |
| **Management**    | **Admin Panel**             | Dashboard for admin tasks and system status.                                                                                     | ![planned](https://img.shields.io/badge/planned-%23EEE?style=for-the-badge)         |

---
### Credits
Badges by [shields.io](https://shields.io).