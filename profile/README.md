<p align="center">
  <img src="https://raw.githubusercontent.com/datagram-messenger/.github/main/profile/assets/datagram-hero.svg" width="960" alt="Datagram Messenger — Engineering the conversation. Original DGP1 packet-network artwork." />
</p>

<h1 align="center">A messenger begins with its foundations.</h1>

<p align="center">An open engineering ecosystem building Datagram Messenger:<br />a protocol, application toolkit, client libraries and the tools to inspect them.</p>

<p align="center">
  <a href="#start-here">Start here</a> ·
  <a href="#the-ecosystem">Repositories</a> ·
  <a href="https://github.com/datagram-messenger/dgproto-go/blob/main/docs/protocol/dgproto-v1.md">Protocol draft</a> ·
  <a href="https://github.com/datagram-messenger/.github/blob/main/CONTRIBUTING.md">Contribute</a>
</p>

## The mission

**Make privacy a design constraint, not an afterthought.** We are building toward a privacy-first messenger by making the layers underneath it explicit: framing, encrypted sessions, application dispatch and observable behavior.

Today, DGProto protects the **client–server transport**. That is not a claim of user-to-user end-to-end encryption. The ecosystem is in active development and **DGProto v1 is a draft**; treat it as an engineering foundation to explore and improve, not an audited, production-ready consumer messenger.

## The ecosystem

Four complementary projects. One clear boundary between the wire and the application.

| Project | Role | Explore |
| --- | --- | --- |
| **[server](https://github.com/datagram-messenger/server)** · Go | **Application toolkit.** `pkg/dgpserver` supplies routing, middleware, admission, principals and lifecycle around the transport. Start with the echo and service-info examples. | [Toolkit docs](https://github.com/datagram-messenger/server/tree/main/docs/dgpserver) |
| **[dgproto-go](https://github.com/datagram-messenger/dgproto-go)** · Go | **Wire and session runtime.** Go client/server transport, including a required-pin TCP client helper, cancellation and bounded queues. | [Go docs](https://github.com/datagram-messenger/dgproto-go/tree/main/docs) · [Wire draft](https://github.com/datagram-messenger/dgproto-go/blob/main/docs/protocol/dgproto-v1.md) |
| **[dgproto-rs](https://github.com/datagram-messenger/dgproto-rs)** · Rust / Tokio | **Client implementation.** The Rust initiator side of DGProto; not a Rust application server. | [Integration docs](https://github.com/datagram-messenger/dgproto-rs/tree/main/docs) · [API reference](https://docs.rs/dgproto/) · [Crate](https://crates.io/crates/dgproto) |
| **[dgproto-wireshark](https://github.com/datagram-messenger/dgproto-wireshark)** · Lua | **Inspection tooling.** A Wireshark dissector for TCP reassembly and Noise handshake inspection, with optional development-only decryption. | [Setup and usage](https://github.com/datagram-messenger/dgproto-wireshark/blob/main/README.md) · [Releases](https://github.com/datagram-messenger/dgproto-wireshark/releases/latest) |

## From bytes to behavior

```text
Go client or Rust/Tokio client (initiator)
                  │
                  │  TCP stream — current draft transport, not UDP/QUIC
                  ▼
DGProto wire + encrypted session     [dgproto-go on the server side]
  DGP1 framing · Noise handshake · authenticated payloads
                  │
                  ▼
Application dispatch                 [server / pkg/dgpserver]
  admission → middleware → routes → your service handlers

Wireshark tooling inspects the TCP/transport layer in development.
```

The transport manages sessions and frames. The application toolkit decides what requests **mean**. Messenger-level features belong above that boundary; transport encryption alone does not define an E2EE product architecture.

## Why this is interesting

- **A wire format you can inspect.** A fixed 40-byte little-endian `DGP1` header and an explicit protocol draft make frame boundaries and validation rules concrete.
- **Cryptography with defined session mechanics.** `Noise_XX_25519_ChaChaPoly_SHA256`, ChaCha20-Poly1305 payload protection, replay protection and directional rekeying are part of the transport design—not a substitute for independent security review.
- **Runtime edges matter.** The Go runtime addresses cancellation, socket ownership and bounded queues. The application toolkit adds bounded sending and a Recorder/Dispatch test surface. A completed send is not a peer acknowledgement.
- **More than one view of the wire.** Go, a Rust client and Wireshark tooling provide different ways to examine behavior. Shared test vectors cover specific cases; they are not an exhaustive cross-language interoperability guarantee.

Read each repository's current docs and dependency pins: a runtime capability is not automatically present in every consumer's pinned release.

## Start here

| I want to… | First step |
| --- | --- |
| **Build a service** | Explore [server's application toolkit](https://github.com/datagram-messenger/server/tree/main/docs/dgpserver) and its echo/service-info examples. |
| **Understand the protocol** | Read the [DGProto v1 draft](https://github.com/datagram-messenger/dgproto-go/blob/main/docs/protocol/dgproto-v1.md), then the [Go implementation docs](https://github.com/datagram-messenger/dgproto-go/tree/main/docs). |
| **Integrate a Rust client** | Start with [Rust integration docs](https://github.com/datagram-messenger/dgproto-rs/tree/main/docs) and the [API reference](https://docs.rs/dgproto/). |
| **Inspect a development session** | Install the [Wireshark plugin](https://github.com/datagram-messenger/dgproto-wireshark/blob/main/README.md). Use synthetic traffic only; never publish traffic keys or private captures. |
| **Help shape the foundations** | Pick a layer above and follow the [contribution guide](https://github.com/datagram-messenger/.github/blob/main/CONTRIBUTING.md). Reproducible tests, clearer docs and focused reviews all help. |

---

**Build with us.** Bring a concrete use case, a small fix or a question that makes the design clearer. Repository-specific instructions come first; suspected vulnerabilities belong only in a verified private reporting route, never public issues. See [safe reporting guidance](https://github.com/datagram-messenger/.github/blob/main/CONTRIBUTING.md#security-and-sensitive-data).

If the protocol work is useful to you, consider starring **[dgproto-go](https://github.com/datagram-messenger/dgproto-go)** to keep it on your radar. Follow the repository closest to what you are building.
