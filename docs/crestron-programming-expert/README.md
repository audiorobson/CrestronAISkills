# Crestron Programming Expert — Technical Index

This directory contains the development knowledge model behind the `crestron-programming-expert` skill.

## Core documents

- [Platform matrix](platform-matrix.md) — routing between processor generations, programming environments, and UI/runtime models.
- [Programming workflow](programming-workflow.md) — standard workflow for turning a request into the right Crestron artifact.
- [Communication architecture](communication-architecture.md) — transport, parser, queue, state, reconnect, and testing model.
- [Source policy](source-policy.md) — provenance and licensing rules for knowledge ingestion.
- [Source inventory](source-inventory.md) — human-readable curated source list.
- [Machine-readable source catalog](sources.json) — structured source metadata for future retrieval/RAG tooling.
- [Roadmap](roadmap.md) — phased development plan.

## Design principle

The knowledge base is organized to answer this sequence before code generation:

```text
processor/runtime
   -> programming environment
   -> toolchain/version
   -> transport/protocol
   -> artifact type
   -> authoritative references
   -> implementation
   -> validation
```

This ordering is intended to prevent the most dangerous class of domain hallucination: code that looks like valid Crestron code but combines APIs or assumptions from incompatible generations.

## Planned reference areas

The next reference documents should cover:

- 2-Series and 3-Series legacy programming;
- 4-Series / current .NET development;
- SIMPL Windows patterns;
- SIMPL+ language and parser patterns;
- SIMPL# versus SIMPL# Pro;
- Crestron Drivers / RAD;
- Crestron Home extension drivers;
- CH5 contracts and packaging;
- VC-4 deployment considerations;
- Toolbox diagnostics;
- EISC/CIP integration;
- DM / DM NVX programming boundaries.

## RAG target

Future retrieval should filter candidate knowledge by metadata before semantic similarity. At minimum:

```text
platform + language + source confidence + version context
```

then optionally:

```text
transport + product family + artifact type
```

This prevents a highly similar but incompatible example from outranking a platform-correct source.
