# Case Study: Enterprise Management Contract System 📊

## 📌 Overview
This project was developed for **SergipeTec** (Sergipe Technological Park) to solve a critical institutional challenge: the centralized management and monitoring of performance goals and government contracts. 

As the **Lead Developer**, I was responsible for the entire lifecycle of the application, ensuring a robust, scalable, and secure environment for multiple stakeholders, including government secretaries and internal planning departments.

---

## 🏗️ The Engineering Challenge
The institution relied on fragmented data across different sectors. The goal was to build a system that:
* **Ensured Data Integrity:** Performance goals and evidence files needed to be audit-ready.
* **Automated Reporting:** Reduction of human error in quarterly reporting for stakeholders.
* **High Availability & Security:** A system capable of handling sensitive institutional data with secure access.

---

## 🛠️ Architectural Decisions

### 1. N-Tier Layered Architecture
I implemented a **Clean/Layered Architecture** to decouple business logic from the infrastructure.
* **Why?** This ensures that the system is maintainable and testable. If the database or an external service changes, the core business rules remain untouched.

### 2. Infrastructure & System Design (Diagram)
The system was designed to run in a containerized environment with a focus on security and abstraction.

```mermaid
graph TD
    %% Define styles
    subgraph Internet
        User((User / Stakeholders))
    end

    subgraph "Server Infrastructure (Docker)"
        Nginx[Nginx Reverse Proxy]
        
        subgraph "Backend Container"
            API[.NET 8 API]
            Layer1[Controllers]
            Layer2[Services / Domain]
            Layer3[Repository Layer]
        end
        
        subgraph "Database Container"
            DB[(PostgreSQL)]
        end
    end

    %% Communication Flow
    User -- "HTTPS (Port 443)" --> Nginx
    Nginx -- "Proxy Pass (Internal Network)" --> API
    
    %% Internal Layers
    API --> Layer1
    Layer1 --> Layer2
    Layer2 --> Layer3
    Layer3 -- "SQL / Integrity Constraints" --> DB

    %% Styling
    style Nginx fill:#009639,stroke:#fff,color:#fff
    style API fill:#512bd4,stroke:#fff,color:#fff
    style DB fill:#336791,stroke:#fff,color:#fff
