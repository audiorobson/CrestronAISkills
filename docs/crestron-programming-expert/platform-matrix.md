# Crestron Programming Platform Matrix

This document is the initial routing map for the `crestron-programming-expert` skill. It is intentionally conservative: when a capability depends on a specific firmware, compiler, SDK, or .NET generation, the skill must verify that dependency instead of assuming compatibility.

| Target | Primary programming paths | Key caution |
|---|---|---|
| 2-Series | SIMPL Windows, SIMPL+ | Legacy toolchain and processor constraints; do not assume modern C#/.NET APIs |
| 3-Series | SIMPL Windows, SIMPL+, SIMPL#, SIMPL# Pro where supported | Runtime/toolchain generation matters; older projects may require legacy libraries and build paths |
| 4-Series | SIMPL Windows, SIMPL+, SIMPL#, SIMPL# Pro, Drivers SDK, CH5-related integrations | Prefer current documented APIs and current supported .NET/toolchain for the specific SDK |
| VC-4 | SIMPL/SIMPL# Pro patterns supported by VC-4 deployment model | Deployment/runtime differs from appliance processors; verify device/feature support |
| Crestron Home | Certified Drivers / RAD, extension drivers, supported Home integrations | Do not treat Home as interchangeable with custom SIMPL# Pro systems |
| Touchpanel UI | VT Pro-e legacy/current paths, CH5 | UI technology and supported panel model must be identified before implementation |

## Routing dimensions

Every substantial answer should classify the request by:

- processor/runtime family;
- programming environment;
- integration transport;
- user interface layer if applicable;
- compiler/SDK/firmware constraints;
- legacy repair versus migration versus greenfield implementation.

## Language separation

### SIMPL Windows
Use for deterministic graphical control logic, signal routing, device symbols, interlocks, sequencing, joins, and module composition.

### SIMPL+
Use for custom logic, protocol parsing, state machines, string processing, transport-oriented glue, and reusable modules where appropriate.

### SIMPL#
Treat as managed-code libraries intended to integrate with supported Crestron programming workflows. Do not automatically equate SIMPL# with a standalone control program.

### SIMPL# Pro
Treat as a standalone managed-code control application model where supported. Device registration, lifecycle, eventing, communications, and application architecture should be explicit.

### Crestron Drivers / RAD
Use when the target ecosystem expects a standardized driver contract rather than an arbitrary custom module. Keep device capabilities, protocol, and transport separated.

### CH5
Use for modern HTML5 UI. Keep the contract between CH5 and control logic explicit; CH5 is not the control processor itself.

## Legacy policy

A legacy system request must always distinguish:

1. **repair in place** — preserve behavior and minimize change;
2. **controlled modernization** — improve maintainability while retaining interfaces;
3. **platform migration** — move to a newer processor/runtime and explicitly map incompatibilities.

The skill must never silently convert a repair request into a migration recommendation.

## Compatibility uncertainty

When a claim depends on version-specific behavior, answers should use one of these labels:

- **Officially documented** — confirmed by Crestron documentation or official repository.
- **Verified example** — supported by official/training sample code.
- **Community-proven** — supported by mature community implementations but not asserted as official.
- **Needs verification** — plausible but version/model-specific documentation must be checked before implementation.
