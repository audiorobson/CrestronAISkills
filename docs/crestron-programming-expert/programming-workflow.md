# Programming Request Workflow

Use this workflow when the skill receives a request to create or modify a Crestron integration.

## 1. Establish the target

Capture or infer only when unambiguous:

- processor model/family;
- current firmware when version-sensitive;
- programming environment;
- existing project type;
- UI technology;
- third-party device model;
- communications protocol;
- whether the task is repair, extension, migration, or greenfield.

## 2. Decide the artifact type

Choose deliberately between:
- SIMPL signal/block plan;
- SIMPL+ module;
- SIMPL# library;
- SIMPL# Pro application/component;
- Crestron Driver/RAD driver;
- Crestron Home extension driver;
- CH5 UI/component;
- documentation/troubleshooting only.

Do not default to C# simply because it is expressive.

## 3. Validate platform fit

Before code:
- confirm the selected artifact is supported on the target;
- identify legacy constraints;
- identify external SDK/library dependencies;
- mark any version-specific uncertainty.

## 4. Define interfaces first

For modules/libraries/drivers, define:
- inputs;
- outputs;
- events;
- configuration parameters;
- transport settings;
- state ownership;
- error/online reporting.

For UI work, define joins/state contracts before visual implementation.

## 5. Build the smallest deterministic core

Prefer:
- explicit state machines;
- bounded buffers;
- explicit timers/timeouts;
- predictable initialization;
- limited side effects;
- one responsibility per component.

## 6. Add observability

Expose or log enough information to diagnose:
- connecting/connected/disconnected;
- authentication;
- TX/RX;
- parser errors;
- timeout/retry;
- device online/offline;
- initialization/synchronization stage.

## 7. Validate against failure cases

Never validate only the happy path.

At minimum consider:
- device unavailable at boot;
- device restarts;
- processor/network reconnect;
- malformed data;
- partial data;
- command timeout;
- duplicated feedback;
- rapid user input;
- configuration error.

## 8. Produce handoff material

For production-oriented answers include:
- artifact list;
- signal/join contract;
- configuration requirements;
- deployment prerequisites;
- test procedure;
- known uncertainties;
- rollback/migration notes if applicable.
