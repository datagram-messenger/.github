<div align="center">

<h1>Datagram</h1>

<p>A privacy-first messenger built on a purpose-built encrypted transport protocol.</p>

[![Protocol](https://img.shields.io/badge/protocol-DGProto%20v1-6f42c1)](https://github.com/datagram-messenger/dgproto-go)
[![Go](https://img.shields.io/badge/Go-1.25+-00ADD8?logo=go&logoColor=white)](https://github.com/datagram-messenger/server)
[![Rust](https://img.shields.io/badge/Rust-1.80+-orange?logo=rust&logoColor=white)](https://github.com/datagram-messenger/dgproto-rs)
[![License](https://img.shields.io/badge/license-Apache--2.0-blue)](https://github.com/datagram-messenger/dgproto-go/blob/main/LICENSE)

</div>

---

Datagram is a production-grade messenger built from the transport layer up. At its core is **DGProto v1** — a custom binary wire protocol with mutual authentication, end-to-end encryption, replay protection, and forward secrecy. Not bolted on. Built in.

The stack: Go backend · Rust client library · Tauri v2 desktop app.

---

### Core repositories

| | Repository | Description |
|---|---|---|
| 🖥️ | [**datagram-messenger/server**](https://github.com/datagram-messenger/server) | Go backend — authenticated sessions, message routing, lifecycle management |
| 🔬 | [**datagram-messenger/dgproto-go**](https://github.com/datagram-messenger/dgproto-go) | DGProto v1 reference implementation in Go · wire spec authority |
| 🦀 | [**datagram-messenger/dgproto-rs**](https://github.com/datagram-messenger/dgproto-rs) | DGProto v1 Rust client library for the desktop app |

---

### Security model

DGProto v1 is built on well-understood, auditable primitives:

- **Noise\_XX\_25519\_ChaChaPoly\_SHA256** — mutual authentication, three-flight handshake
- **ChaCha20-Poly1305 AEAD** — every frame encrypted, header authenticated
- **HMAC-SHA256 key ratchet** — directional forward secrecy via epoch-based rekeying
- **Sliding replay window** — 2048-entry, check-before-authenticate

> Found a vulnerability? Report it privately via [SECURITY.md](https://github.com/datagram-messenger/dgproto-go/blob/main/SECURITY.md). Please do not open public issues for security concerns.

---

<div align="center">

*Correctness and security over delivery speed.*

</div>
