# Failure recovery

Use at-least-once delivery with idempotent processing, not an exactly-once claim.

| Failure | Response |
|---|---|
| PostgreSQL unavailable | Keep durable raw data; retry transactional load |
| Kafka unavailable | Return retryable failure; producer retains event in durable local spool |
| Consumer crash | Resume from committed offset; commit only after durable raw write |
| Duplicate delivery | Unique event ID and idempotent load |
| AI model failure | Record failed inference attempt |
| Airflow task failure | Retry boundedly; surface permanent failure |
| Invalid event | Quarantine and track reason |
| Late arrival | Recompute affected partitions |
| Dashboard unavailable | Collection continues independently |

Test outage recovery, crash between write and acknowledgement, replay twice, malformed data and late events. Kafka retention, storage backups and recovery objectives must be defined before deployment. Single-machine tests do not establish high availability.
