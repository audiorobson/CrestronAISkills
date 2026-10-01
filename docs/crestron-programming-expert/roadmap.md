# Crestron Programming Expert — Development Roadmap

## Milestone 1 — Domain router
- Initial skill frontmatter and behavior.
- Processor/runtime separation.
- Language/toolchain separation.
- Behavioral evals.
- Initial platform matrix.

## Milestone 2 — Curated knowledge inventory
Catalog official and community sources for:
- SIMPL Windows;
- SIMPL+;
- SIMPL#;
- SIMPL# Pro;
- Drivers/RAD;
- Crestron Home;
- CH5;
- Toolbox/diagnostics;
- 2-Series/3-Series legacy support;
- 4-Series/VC-4 current development.

Every source receives license, provenance, platform, language, and confidence metadata.

## Milestone 3 — Programming patterns
Create reviewed reference guides for:
- TCP/UDP clients and servers;
- serial framing and parsers;
- reconnect and command queues;
- REST/HTTP integrations;
- WebSocket integrations;
- EISC/CIP patterns;
- UI join contracts;
- module/driver architecture;
- logging and diagnostics.

## Milestone 4 — Validation toolchain
Add a separate tool-enabled layer capable of validating generated artifacts using available compilers/build systems.

Target flows:
- SIMPL+ source validation/compilation;
- C# project build against the appropriate Crestron SDK/runtime;
- CH5 lint/build/package;
- schema validation for drivers/configuration.

The advisory skill itself remains distinct from execution tooling.

## Milestone 5 — Retrieval/RAG
Build retrieval that filters by platform, language, SDK generation, device family, and source confidence before supplying context to the model.

## Milestone 6 — Regression corpus
Collect known-good tasks from legacy and current projects and run them as regression evaluations to detect hallucinations, platform mixing, and breaking behavior.
