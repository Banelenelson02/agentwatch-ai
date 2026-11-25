# Data quality

Bronze preserves permitted raw records; Silver validates and deduplicates; Gold aggregates business metrics.

- Missing required fields, unsupported versions, malformed JSON, invalid timestamps, negative token counts and out-of-range scores: quarantine with reason and raw reference.
- Identical repeated event IDs: deduplicate; conflicting payloads with the same ID: flag and quarantine the conflict.
- Timezone-aware timestamps: normalise to UTC; late events trigger affected partition recomputation.
- Missing evaluation: mark unevaluated, not zero.
- Private prompts, credentials and customer content: exclude before persistence.
- Parent event not yet available: defer and retry; track unresolved references.

Track input, accepted, duplicate, invalid and deferred counts. Reconcile counts and test with deterministic valid/invalid fixtures. Never mix synthetic and real benchmark results without explicit labelling.
