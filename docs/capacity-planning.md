# Capacity planning

Design workload: 1,000,000 synthetic events/day at an assumed average 2 KB per event (decimal units). Average throughput ~11.57 events/s; raw storage ~2 GB/day, 60 GB/30 days, 730 GB/365 days. Excludes compression, indexes, backups and replication.

Test progressively at 100, 1,000, 10,000, 100,000 and 1,000,000 events; use bounded batches. Record hardware, versions, dataset seed, record counts, elapsed time, throughput, peak memory, storage and freshness. Measure burst handling and recovery separately. Do not infer sustained production capacity from a single batch run.

Risks: local memory, school access, cloud cost, complexity and data loss. Mitigate via local-first development, independent execution, versioned dependencies, durable replay and budget review. Retention and compression policies remain open. No benchmark results yet.
