# Knowledge Source Policy

The project should grow from curated sources rather than indiscriminate scraping.

## Tier 1 — authoritative

- Crestron official documentation/help portals.
- Crestron official SDK documentation.
- Crestron official GitHub repositories.
- Official example and training repositories where provenance is clear.

Use these sources to establish API names, platform support, SDK contracts, compiler/toolchain requirements, and product-specific behavior.

## Tier 2 — mature implementation references

Examples include well-established Crestron open-source projects and frameworks such as PepperDash and reputable training/sample repositories.

Use these to learn architecture and implementation patterns. Do not re-label community conventions as official Crestron requirements.

## Tier 3 — community modules

Community SIMPL+, SIMPL#, drivers, and integration examples can be valuable for legacy systems and obscure devices.

Before using them as knowledge:
- record repository URL and license;
- identify target processor/toolchain when possible;
- distinguish code that merely exists from code known to compile/run;
- prefer maintained or historically credible sources;
- avoid copying code when the license does not permit redistribution.

## RAG metadata target

Each ingested knowledge unit should eventually carry fields equivalent to:

```yaml
source_type: official-doc | official-repo | training-example | mature-community | community
source_url: ...
license: ...
platforms: [2-series, 3-series, 4-series, vc4, home]
languages: [simpl, simpl-plus, simpl-sharp, simpl-sharp-pro, drivers, ch5]
transports: [serial, tcp, udp, http, websocket, ssh, cresnet, cip, dm-nvx]
product_families: [...]
version_context: ...
confidence: authoritative | verified-example | community-proven | needs-verification
```

## Ingestion rule

Do not ingest an entire repository simply because it contains Crestron code. Index at file/module/document granularity and preserve provenance so an LLM can cite where a recommendation came from and avoid cross-generation contamination.
