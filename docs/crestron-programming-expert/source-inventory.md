# Curated Source Inventory — Crestron Programming Expert

This inventory records candidate knowledge sources for the Crestron programming skill. Inclusion here does **not** mean wholesale ingestion is permitted. Licensing, provenance, target platform, and confidence must be evaluated before copying or indexing content.

## Classification

- **A — Authoritative:** official Crestron documentation or official Crestron repositories.
- **B — Training / high-confidence implementation:** material from identifiable Crestron training personnel or mature specialist frameworks.
- **C — Community implementation:** useful examples that require stronger verification before influencing generated code.
- **D — Tooling:** editors, compilers, wrappers, and developer utilities useful for validation workflows.

## Initial sources

| Source | Class | Main value | Platform/language | License / reuse status | Ingestion policy |
|---|---|---|---|---|---|
| Crestron/CrestronAISkills | A | Official skill schema, governance, validation model | AI skills | MIT | May reuse under MIT terms; keep upstream provenance |
| Crestron/CH5ComponentLibrary | A | Official CH5 component implementation and API patterns | CH5 / TypeScript | Repository reports non-standard license; inspect exact terms before copying | Prefer reference/index metadata until license is reviewed |
| Crestron/CH5ExampleProjects | A | Official CH5 starter/complete projects | CH5 / TypeScript, React, Angular | No repository license detected in initial check | Reference facts and structure; do not mirror code without license confirmation |
| CTI-Tim/CrestronCSharpExamples | B | C# examples from Crestron C# video/training material | SIMPL#, SIMPL# Pro, C# | No LICENSE file detected in initial check | Use as high-confidence reference; do not redistribute source wholesale |
| PepperDash/Essentials | B | Mature Crestron application framework architecture | SIMPL# Pro / C# | GitHub repository metadata reports MIT | Good candidate for selective pattern indexing with attribution |
| PepperDash/PepperDashCore | B | Communications, abstractions, utilities, device patterns | SIMPL# / SIMPL# Pro / C# | GitHub repository metadata reports MIT | Good candidate for selective pattern indexing with attribution |
| Norgate-AV/crestron-simpl-plus | D | VS Code SIMPL+ editing and compiler invocation patterns | SIMPL+ / tooling | MIT | May reuse tooling concepts/code under MIT terms |
| Crestron official Help / SDK documentation | A | API names, support matrices, SDK contracts, firmware/toolchain behavior | All current documented platforms | Documentation terms apply | Index summaries/metadata and cite source; avoid bulk copying |
| Crestron Drivers SDK documentation | A | RAD/Certified Drivers contracts and architecture | Drivers / C# | Documentation terms apply | Use as authoritative reference; store structured summaries, not bulk text |

## Source-specific notes

### Crestron/CH5ComponentLibrary
Official Crestron repository. The repository metadata identifies the license as non-standard/NOASSERTION. Before copying source into this repository or a local corpus, inspect the actual licensing terms in the repository/package artifacts. Until then, treat it as an authoritative external reference.

### Crestron/CH5ExampleProjects
Official example repository containing React and Angular starter/complete projects. Initial repository inspection found no declared repository license. Use it to verify architecture, file layout, APIs, and build patterns, but avoid redistributing its source until terms are confirmed.

### CTI-Tim/CrestronCSharpExamples
Maintained by an identifiable Crestron technical trainer and contains examples from the Crestron C# video series. This makes it a valuable high-confidence training source, but absence of an explicit license means the project should not copy the repository into our corpus. Extract facts, patterns, and provenance references instead.

### PepperDash
Essentials and PepperDashCore are mature Crestron-focused C# projects. GitHub metadata reports MIT licensing. They are especially useful for:
- communications abstractions;
- plugin/device architecture;
- configuration-driven systems;
- EISC/CIP bridges;
- logging and diagnostics;
- large-system organization.

Community architecture should still remain labeled as community/mature implementation rather than official Crestron behavior.

### Norgate-AV/crestron-simpl-plus
MIT-licensed developer tooling that exposes a practical path to invoking the installed Crestron SIMPL+ compiler from VS Code. It distinguishes Series 3 compilation from combined Series 2/3 compilation. This is a strong candidate for the future validation toolchain.

## Ingestion decisions

Use four modes:

1. **Reference-only**
   - Store URL, title, platform tags, confidence, and a short original summary.
   - Use when licensing is absent/unclear or the source is proprietary documentation.

2. **Pattern extraction**
   - Record architecture/patterns in our own words with provenance.
   - Appropriate for training repositories and community code.

3. **Selective code ingestion**
   - Only for clearly licensed material.
   - Preserve license and source attribution.
   - Prefer small, self-contained examples over repository mirrors.

4. **Validation dependency**
   - Use an external tool/repository as part of compiler/build/test infrastructure without copying its corpus unnecessarily.

## Next inventory targets

- Crestron official SIMPL#/SIMPL# Pro API documentation.
- Crestron Drivers SDK and Home Extension Driver documentation.
- Official VC-4 programming/deployment documentation.
- Official SIMPL+/SIMPL Windows references.
- Current 4-Series .NET/toolchain documentation.
- Historical 2-Series/3-Series help material with redistribution status identified.
- Known-good protocol modules with explicit licenses.
