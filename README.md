# AgentWatch AI

A local-first data engineering platform for AI observability. AgentWatch collects operational events from AI applications, validates and transforms them, and produces reliable analytical datasets for model performance, reliability and resource usage.

**Status:** v0.1 design baseline; implementation and benchmarks are pending.

## Target architecture
Ollama and synthetic generators → FastAPI → Kafka → Bronze JSONL → Python validation → Silver Parquet → PostgreSQL/dbt → Gold metrics → Streamlit and alerts. Airflow orchestrates batch jobs. AWS is an optional extension.

The MVP uses local JSONL, Python/Pandas and PostgreSQL without Kafka or paid APIs.

## Documentation
- [Project overview](docs/project-overview.md)
- [Requirements](docs/requirements.md)
- [Roadmap](docs/roadmap.md)
- [High-level design](docs/high-level-design.md)
- [Low-level design](docs/low-level-design.md)
- [Data contracts](docs/data-contracts.md)
- [Database design](docs/database-design.md)
- [Data quality](docs/data-quality.md)
- [Failure recovery](docs/failure-recovery.md)
- [Capacity planning](docs/capacity-planning.md)
- [Architecture decisions](docs/adr/README.md)
- [Development journal](docs/development-journal/week-01.md)

## Development
macOS and Linux are intended targets. The first implementation milestone is a deterministic synthetic event generator and a local Ollama adapter. Setup instructions will be added with runnable code. Never commit credentials, private conversations or generated datasets.

## Inspiration
The AI evaluation and monitoring concept was inspired by [Net-Africa-2026](https://github.com/adeline-pepela/Net-Africa-2026). AgentWatch is a separate data engineering design, not a copy of that implementation.
