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

    User -->|HTTPS 443| Nginx
    Nginx -->|Proxy Pass| API

    API --> Layer1
    Layer1 --> Layer2
    Layer2 --> Layer3
    Layer3 -->|SQL Queries| DB

    style Nginx fill:#009639,stroke:#ffffff,color:#ffffff
    style API fill:#512bd4,stroke:#ffffff,color:#ffffff
    style DB fill:#336791,stroke:#ffffff,color:#ffffff

```markdown
    style Nginx fill:#009639,stroke:#ffffff,color:#ffffff
    style API fill:#512bd4,stroke:#ffffff,color:#ffffff
    style DB fill:#336791,stroke:#ffffff,color:#ffffff

3. Database Modeling

I designed a relational schema focused on referential integrity.

Challenge: Managing the relationship between complex institutional programs and their specific KPIs.

Solution: A normalized structure that supports historical tracking of goals and evidence, ensuring that all data is traceable.

4. Security & DevOps (Nginx & Docker)

Containerization: Used Docker to encapsulate the environment, ensuring the app runs identically in development and production.

Reverse Proxy (Nginx): Configured to manage SSL termination, load balancing, and to hide the application server from direct public exposure, adding a crucial layer of security.

🚀 Key Achievements

Full Cycle Ownership: I handled everything from initial requirements gathering with stakeholders to final deployment.

Process Automation: The automated reporting engine significantly reduced the time spent on administrative tasks by ensuring data was collected and formatted in real-time.

🧠 Lessons Learned

Stakeholder Communication: Learned how to translate complex government requirements into technical specifications.

Full-Stack Responsibility: Managing both the database integrity and the UI/UX consistency taught me the importance of a holistic view of software engineering.

Security-First Mindset: Implementing Nginx and Docker taught me how to protect enterprise applications in a production environment.

📈 Impact

The system is currently the primary tool for monitoring management contracts at SergipeTec, providing transparency and efficiency for the SEDETEC (Secretariat of State for Economic Development, Science, and Technology).
