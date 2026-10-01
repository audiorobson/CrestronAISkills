# Communication Integration Architecture

This guide defines the default reasoning model for third-party device integrations. It is intentionally platform-neutral until the target Crestron runtime is identified.

## Core layers

A robust integration should separate:

1. **Transport**
   - serial;
   - TCP client/server;
   - UDP;
   - HTTP/REST;
   - WebSocket;
   - SSH;
   - IR/CEC when applicable.

2. **Framing**
   - terminators;
   - fixed length;
   - delimiters;
   - binary headers;
   - checksums;
   - escaping.

3. **Protocol parser**
   - converts raw frames to typed state/events;
   - never assumes one receive callback equals one complete message;
   - handles partial frames and multiple frames in one receive buffer.

4. **Command scheduler**
   - command queue;
   - pacing/rate limit;
   - request/response correlation where applicable;
   - retry rules;
   - timeout rules.

5. **State model**
   - desired state;
   - reported state;
   - online/ready state;
   - stale/unknown state.

6. **Crestron-facing contract**
   - SIMPL joins/signals;
   - SIMPL# properties/events;
   - driver capabilities;
   - EISC contract;
   - CH5 join/state contract.

## TCP lifecycle

Do not generate a TCP integration as only "connect and send".

Account for:
- connection establishment;
- authentication/handshake;
- connection loss;
- reconnect backoff;
- receive re-arming when required by the target API;
- command queue behavior while offline;
- heartbeat/keepalive if the protocol defines one;
- synchronization after reconnect.

Never invent a port number. If the protocol document does not state one, mark it as required input.

## Serial lifecycle

Always identify:
- baud rate;
- data bits;
- parity;
- stop bits;
- hardware/software flow control if applicable;
- command terminator;
- response terminator.

If any serial setting is unknown, do not present a guessed value as a default.

## Parser rules

Prefer deterministic parsers.

For ASCII line-oriented protocols:
- accumulate bytes/chars in a buffer;
- search for the documented terminator;
- extract one frame at a time;
- leave incomplete remainder buffered;
- protect against unbounded buffer growth.

For binary protocols:
- locate/validate header;
- determine expected frame length;
- validate checksum/CRC where defined;
- reject malformed frames safely;
- resynchronize without discarding arbitrary valid data.

## Command queues

Use a queue when the device:
- requires pacing;
- permits only one outstanding request;
- returns ambiguous acknowledgements;
- becomes unstable under bursts.

A queue design should define:
- enqueue policy;
- maximum depth;
- deduplication/coalescing;
- timeout;
- retry count;
- cancellation on disconnect;
- post-reconnect synchronization.

## Feedback-first design

Whenever possible, UI/SIMPL state should reflect **device feedback**, not simply the last command sent.

Recommended state flow:

```text
User intent
   -> command
   -> transport
   -> device
   -> feedback
   -> parser
   -> state model
   -> Crestron signals/UI
```

For devices without feedback, explicitly label state as assumed/commanded rather than verified.

## Testing

Every protocol integration should accumulate test vectors:

- valid command;
- valid response;
- unsolicited event;
- fragmented response;
- multiple responses in one read;
- malformed response;
- timeout;
- disconnect during command;
- reconnect and resync;
- boundary values.

These test vectors are strong candidates for automated regression tests once the execution/validation layer is added.
