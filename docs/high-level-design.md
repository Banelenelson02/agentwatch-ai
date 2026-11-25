# High-level design

## MVP
```mermaid
flowchart LR
 A[Ollama adapter] --> C[Local Bronze JSONL]
 B[Synthetic generator] --> C
 C --> D[Python validation and ETL]
 D --> E[PostgreSQL]
 D --> Q[Quarantine]
 E --> F[SQL analytics]
```

## Target
```mermaid
flowchart TD
 A[Ollama] --> I[FastAPI ingestion]
 B[Synthetic producer] --> I
 X[Future providers] --> I
 I --> K[Kafka]
 K --> C[Raw storage consumer]
 C --> R[Bronze JSONL local or S3]
 R --> T[Python and Pandas validation]
 T --> Q[Quarantine]
 T --> S[Silver Parquet]
 S --> W[PostgreSQL facts and dimensions]
 W --> G[dbt Gold models]
 G --> D[Streamlit dashboard]
 G --> L[Alerts]
 O[Airflow] -. schedules .-> T
 O -. schedules .-> W
 O -. schedules .-> G
 M[OpenTelemetry and logs] -. monitors .-> I
 M -. monitors .-> T
```

Push ingestion and historical imports share a versioned contract. Ingestion acknowledges only after durable storage or broker acknowledgement. Consumer offsets are committed after durable writes. Batch and streaming paths share validation and idempotent load logic. Raw metadata excludes private content. AWS S3/RDS/ECS/CloudWatch are optional later integrations; no paid dependencies for MVP.
