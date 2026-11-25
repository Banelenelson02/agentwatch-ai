# Week 01: System design
Planning dates: 24–25 November 2026.

## Work completed
Defined the project problem, scope, roadmap, initial architecture, requirements and proposed decisions. Created the GitHub repository and prepared the initial design documentation.

## Decisions
Local Ollama inference, synthetic workloads, batch before streaming, PostgreSQL analytics, Medallion architecture and cross-platform development.

## Challenges and approach
Local memory constraints and potential cloud costs motivate independent components and local-first testing. Heavier workloads may run on Linux where permitted.

## Next steps
Review design documentation, formalise event validation schemas, set up Python, implement a deterministic synthetic event generator and test Ollama telemetry. No implementation or measured benchmarks yet.
