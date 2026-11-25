# Requirements

## Functional requirements
- FR-001: Generate synthetic AI events
- FR-002: Collect real Ollama telemetry
- FR-003: Accept operational events through REST APIs
- FR-004: Preserve original permitted raw data
- FR-005: Validate incoming event schemas
- FR-006: Deduplicate processed datasets
- FR-007: Quarantine invalid records
- FR-008: Handle late-arriving events
- FR-009: Transform raw events into structured datasets
- FR-010: Load processed data into PostgreSQL
- FR-011: Automate pipeline execution
- FR-012: Support event streaming
- FR-013: Calculate analytical metrics
- FR-014: Compare AI model performance
- FR-015: Detect performance degradation
- FR-016: Display dashboards
- FR-017: Generate threshold alerts
- FR-018: Recover from pipeline failures
- FR-019: Replay historical data
- FR-020: Monitor pipeline health

## Non-functional requirements (targets, not measured results)
| ID | Requirement | Target |
|---|---|---|
| NFR-001 | Scalability | 1 million synthetic events/day workload |
| NFR-002 | Integrity | Zero duplicate logical fact records |
| NFR-003 | Freshness | Within 5 minutes in streaming mode under defined test conditions |
| NFR-004 | Reliability | No silent loss of accepted events within tested failure scenarios |
| NFR-005 | Recovery | Retry and replay |
| NFR-006 | Security | Authenticated ingestion, TLS for remote endpoints, no committed credentials |
| NFR-007 | Privacy | No private prompts or responses by default |
| NFR-008 | Portability | macOS and Linux |
| NFR-009 | Maintainability | Modular documented components |
| NFR-010 | Cost | No paid services required locally |
| NFR-011 | Testability | All defined critical data rules tested |
| NFR-012 | Observability | Logs, metrics and failure tracking |

Acceptance: demonstrate real and synthetic data, repeatable batch/streaming processing, duplicate and invalid handling, replay, fault recovery, correct analytics and documented benchmarks. AWS remains budget-dependent.
