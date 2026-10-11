<div align="center">

# Datagram

**A privacy-first messenger built on a purpose-built encrypted protocol.**

*Secure by design. Not by configuration.*

</div>

---

## What is Datagram?

Datagram is a production-grade messenger built from the transport layer up. Instead of layering encryption on top of an existing protocol, we designed **DGProto v1** — a custom binary wire protocol with mutual authentication, end-to-end encryption, replay protection, and forward secrecy baked in at the core.

The stack is intentionally minimal and auditable: a Go backend, a Rust client library, and a desktop app built with Tauri v2.

---

## DGProto v1

DGProto v1 is the secure transport protocol that powers Datagram. It is binary, session-oriented, and cryptographically secured end-to-end.

```
┌──────────────────────────────────────────────────────────────┐
│  L4  Application   Typed messages: chat, ping, ack, close    │
│  L3  Session       Sequences, epochs, replay, keepalive      │
│  L2  Cryptography  Noise XX · ChaCha20-Poly1305 · HKDF       │
│  L1  Framing       40-byte header · TLV encoding · padding   │
│  L0  Transport     TCP                                       │
└──────────────────────────────────────────────────────────────┘
```

**Security properties:**

- 🔐 **Mutual authentication** — `Noise_XX_25519_ChaChaPoly_SHA256` three-flight handshake
- 🔒 **End-to-end encryption** — ChaCha20-Poly1305 AEAD on every frame
- 🔁 **Forward secrecy** — directional rekeying via HMAC-SHA256 key ratchet
- 🛡️ **Replay protection** — 2048-entry sliding window, check-before-authenticate
- 📦 **Traffic shaping** — optional random padding, authenticated as AAD

---

## Repositories

| Repository | Language | Description |
|---|---|---|
| [`server`](https://github.com/datagram-messenger/server) | Go 1.25+ | Backend microservices — authenticated sessions, message routing, lifecycle |
| [`dgproto-go`](https://github.com/datagram-messenger/dgproto-go) | Go 1.25+ | DGProto v1 reference implementation and wire specification |
| [`dgproto-rs`](https://github.com/datagram-messenger/dgproto-rs) | Rust 1.80+ | DGProto v1 client library for the Tauri desktop app |

> `dgproto-go` is the canonical specification authority. All wire-visible behavior in `dgproto-rs` is validated byte-for-byte against shared wire vectors.

---

## Status

The project is under active development.

| Component | Status |
|---|---|
| DGProto v1 wire protocol | ✅ Implemented |
| Go server transport & lifecycle | ✅ Implemented |
| Rust client library | ✅ Implemented |
| Desktop client (Tauri v2) | 🔨 In progress |
| Messenger services (chat, users) | 🔨 In progress |

> DGProto v1 is a draft specification. Wire compatibility will be formally declared after stabilization.

---

## Security

DGProto v1 is security-sensitive infrastructure. We treat correctness and wire compatibility as release requirements, not best-effort goals.

If you discover a vulnerability, please report it privately — see [`SECURITY.md`](https://github.com/datagram-messenger/dgproto-go/blob/main/SECURITY.md) in `dgproto-go`. Do not open public issues for suspected security problems.

---

<div align="center">

*Built with care. Designed to last.*

</div>
