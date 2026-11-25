# Low-level design (initial)

| Component | Interface / responsibility |
|---|---|
| Synthetic generator | Seeded fixtures to JSONL; configurable count and bad-record injection |
| Ollama adapter | Normalise model response metadata into agent_response events; record failures |
| Raw writer | Append or atomically publish immutable JSONL batches |
| Validator | Parse records, validate schema and return accepted/quarantined records with reasons |
| Transformer | Standardise UTC timestamps, numeric fields and source labels; deduplicate |
| Warehouse loader | Transactional upsert or conflict handling by event ID |
| Evaluator | Known-answer tests with dataset and evaluator versions; emit separate evaluation events |
| Ingestion API | POST /api/v1/events, /events/batch, /evaluations; GET /health |
| Kafka | Durable producer retries, consumer checkpoint after raw persistence |
| Airflow | Batch DAG: extract → validate → transform → load → aggregate → checks |
| Analytics | SQL/dbt models and read-only dashboard |
| Monitoring | Pipeline run IDs, counts, durations, errors and freshness |

API responses: 202 only after durable acceptance, 400 for invalid envelopes, 401 for unauthenticated requests, 503 for retryable unavailable storage. Detailed payload validation may quarantine accepted records asynchronously. Reuse event IDs when retrying.

MVP CLI and module signatures, dependency versions and exact batch sizes remain to be implemented and tested. Prefer bounded chunks, native PostgreSQL and one local model at a time on memory-constrained hardware. Docker and heavier services are introduced separately.
