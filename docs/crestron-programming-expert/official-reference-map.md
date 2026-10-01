# Official Reference Map — Crestron Programming

Last reviewed: 2026-10-01.

This document records official documentation entry points and the rules for using them. It is not a substitute for version-specific documentation.

## Crestron SIMPL# / SIMPL# Pro API Help

Primary reference:
- https://help.crestron.com/SimplSharp/

Observed current API pages expose version information for both:
- .NET 6.0
- .NET Compact Framework 3.5

This is useful evidence that the documentation spans multiple runtime generations, but **must not be interpreted as proof that every listed API/member is available on every processor or firmware**. Processor family, assembly version, firmware, and build toolchain still require verification.

### Retrieval rule

When answering a C# API question:
1. locate the exact namespace/class/member in official API Help;
2. capture assembly name and documented version;
3. capture runtime support information;
4. verify processor/toolchain compatibility separately when material;
5. only then use the member in generated code.

Do not infer a complete 3-Series/4-Series support matrix from a single member page.

### Useful namespaces to index first

- `Crestron.SimplSharp`
- `Crestron.SimplSharpPro`
- `Crestron.SimplSharpPro.DeviceSupport`
- `Crestron.SimplSharp.Net`
- `Crestron.SimplSharp.CrestronIO`
- `Crestron.SimplSharp.WebScripting`

The index should be built from official namespace/class pages, not remembered names.

## Crestron Drivers SDK

Primary reference:
- https://sdkcon78221.crestron.com/sdk/Crestron_Certified_Drivers_SDK/Content/Topics/Home.htm

The official SDK documentation states that Crestron Drivers can be used across the Crestron ecosystem including SIMPL, SIMPL#Pro, Crestron Home, and .AV Framework, with supported communications including IR, Serial, Ethernet, and CEC.

### Current SDK line

The official "What's New" page reports **Crestron Drivers SDK v29**, released September 15, 2026:
- https://sdkcon78221.crestron.com/sdk/Crestron_Certified_Drivers_SDK/Content/Topics/Whats-New/Whats-New.htm

Therefore, do not generate a new driver as if the older RAD-only model were the sole current architecture.

### Architecture generations

The official documentation distinguishes:

#### V1 — RAD Framework
Reference:
- https://sdkcon78221.crestron.com/sdk/Crestron_Certified_Drivers_SDK/Content/Topics/Driver-SDK-V1/Driver-SDK-V1.htm

Key model:
- C# interfaces define capabilities/device types;
- abstract device classes provide default implementations;
- driver/protocol classes specialize behavior;
- transport helpers are provided by the SDK.

The official required-library reference includes `RADCommon` and device-specific RAD libraries, with additional SIMPL#Pro-only libraries such as `RADProTransports`.

#### V2 — Entity Model
Reference:
- https://sdkcon78221.crestron.com/sdk/Crestron_Certified_Drivers_SDK/Content/Topics/Driver-SDK-V2/SDK-Framework/Overview-V2.htm

The official documentation states that SDK 21.x introduced the V2 Entity Model. The Entity Model describes capabilities in data as properties, commands, events, and types rather than relying on a growing set of C# capability interfaces.

Important architectural characteristics:
- interaction is funneled through a root `DriverController`;
- a driver can represent multiple entities/controllers;
- controller IDs identify the targeted entity;
- data exchanged with the host is designed around immutable structures.

### Driver selection rule

Before generating driver code, determine:
1. SDK version installed/targeted;
2. V1 RAD versus V2 Entity Model;
3. target host(s): SIMPL, SIMPL#Pro, Crestron Home, .AV Framework;
4. supported device type;
5. transport;
6. required feedback model.

The official SDK explicitly notes that some device types may be restricted to a particular SDK architecture. Never assume V1 and V2 are interchangeable for a given device type.

### Driver design checklist from official guidance

The official "Create a Driver" guidance asks developers to identify:
- required commands;
- API values from the actual device protocol;
- communication method;
- required device feedback;
- whether feedback is absent, unsolicited, or polled.

This maps directly to our communication architecture and should be enforced by the skill.

## Platform drivers

Official reference:
- https://sdkcon78221.crestron.com/sdk/Crestron_Certified_Drivers_SDK/Content/Topics/Driver-SDK-V1/Create-a-Driver/Device-Types/Platform/Platform-Overview.htm

A platform driver is appropriate when one gateway/API controls one or more paired/child devices. Examples include hubs or cloud-backed platforms.

Do not automatically model a gateway integration as many unrelated independent drivers when the official platform-driver model fits the device topology.

## Version-sensitive facts

Treat these as versioned facts, not timeless rules:
- supported device types;
- SDK architecture availability;
- SIMPL wrapper support;
- NuGet/package requirements;
- Visual Studio requirements;
- firmware minimums;
- Crestron Home compatibility;
- .AV Framework compatibility.

For these items, retrieve the latest official page at the time the code is generated.

## Knowledge-base implementation rule

Official API documentation should enter the RAG as structured summaries, for example:

```yaml
source_type: official-doc
url: https://help.crestron.com/SimplSharp/...
namespace: Crestron.SimplSharpPro
assembly: SimplSharpPro.dll
api_symbol: ...
runtime_support:
  - dotnet-6
  - compact-framework-3.5
platform_mapping: needs-separate-verification
reviewed_date: 2026-10-01
confidence: authoritative
```

Driver SDK documents should additionally record:
- sdk_version;
- architecture: v1-rad | v2-entity;
- device_type;
- host_environment;
- transport;
- package/library dependencies.

This metadata is intended to stop semantic retrieval from mixing old RAD examples with new Entity Model code.
