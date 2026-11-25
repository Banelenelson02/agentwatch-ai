# Data contracts v1 (proposed)

All events require globally unique event_id (string, stable across retries), event_type (enum), schema_version (integer, 1), source (real or synthetic), and timestamp (ISO 8601 with timezone, normalised to UTC). Ingestion adds received_at separately. Never include credentials, customer messages or private responses.

| Type | Additional fields |
|---|---|
| agent_response | agent_id, session_id, provider, model_id, prompt_version (strings); input_tokens, output_tokens (nullable nonnegative integers); latency_ms (nonnegative number); status (success or failure); optional error_code |
| tool_execution | parent_event_id, tool_name (strings); execution_time_ms (nonnegative number); status; optional error_code |
| evaluation | parent_event_id, evaluator_name, evaluator_version, benchmark_run_id (strings); correctness_score (number 0–1 or null if not evaluated); evaluated_at (UTC timestamp) |

Example (illustrative):
```json
{"event_id":"evt_001","event_type":"agent_response","schema_version":1,"source":"real","timestamp":"2026-11-24T18:00:00Z","agent_id":"agent_001","session_id":"session_001","provider":"ollama","model_id":"qwen3:0.6b","prompt_version":"v1","input_tokens":150,"output_tokens":85,"latency_ms":2400,"status":"success"}
```

A model request succeeding does not imply correctness. Evaluate independently using known answers and a versioned benchmark. Join evaluations by parent_event_id; defer unresolved parents rather than silently discard. Distinguish missing values from zero. Unsupported versions are quarantined. Real and synthetic metrics remain separate by default. Formal machine-readable schemas and fixtures are a next implementation task.
