graph TD
    %% Define nodes
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
    User -->|HTTPS 443| Nginx
    Nginx -->|Proxy Pass| API

    %% Internal Layers
    API --> Layer1
    Layer1 --> Layer2
    Layer2 --> Layer3
    Layer3 -->|SQL Queries| DB

    %% Styling
    style Nginx fill:#009639,stroke:#ffffff,color:#ffffff
    style API fill:#512bd4,stroke:#ffffff,color:#ffffff
    style DB fill:#336791,stroke:#ffffff,color:#ffffff
