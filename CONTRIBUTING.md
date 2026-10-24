# Contributing to Datagram Messenger

Help make the protocol easier to reason about, the implementations safer to change and the documentation easier to use. A small, reproducible fix or a clear question is a useful contribution.

**Start with the target repository's README, CONTRIBUTING file and any local instructions. Those take precedence over this organization-level guide.** Build commands, toolchain requirements, test suites and license terms belong to the repository you are changing.

## Find the right home

| Your change or question | Repository | Read first |
| --- | --- | --- |
| Application handlers, routing, middleware, admission or service lifecycle | [server](https://github.com/datagram-messenger/server) | [Application toolkit docs](https://github.com/datagram-messenger/server/tree/main/docs/dgpserver) |
| Wire format, Go session runtime or Go TCP client/server behavior | [dgproto-go](https://github.com/datagram-messenger/dgproto-go) | [Go docs](https://github.com/datagram-messenger/dgproto-go/tree/main/docs) · [Protocol draft](https://github.com/datagram-messenger/dgproto-go/blob/main/docs/protocol/dgproto-v1.md) |
| Rust/Tokio client integration or Rust behavior | [dgproto-rs](https://github.com/datagram-messenger/dgproto-rs) | [Rust docs](https://github.com/datagram-messenger/dgproto-rs/tree/main/docs) · [API reference](https://docs.rs/dgproto/) |
| Wireshark dissection, TCP reassembly or inspection tooling | [dgproto-wireshark](https://github.com/datagram-messenger/dgproto-wireshark) | [Plugin README](https://github.com/datagram-messenger/dgproto-wireshark/blob/main/README.md) |
| Organization profile, artwork or these shared templates | [.github](https://github.com/datagram-messenger/.github) | [Maintenance guide](https://github.com/datagram-messenger/.github/blob/main/README.md) |

If a non-sensitive bug crosses layers, open one report in the closest repository and link related work rather than duplicating it everywhere. For a suspected vulnerability, skip the public issue workflow and use the guidance below.

## Before opening an issue

- Search existing issues and read the relevant docs.
- For bugs, include expected and actual behavior, a minimal synthetic reproduction, the repository revision or package version, and relevant OS/runtime/tool details. A failing test is especially helpful.
- For features, explain who needs the capability, the workflow it enables and alternatives you have considered. Proposals start a design conversation; they are not delivery commitments.
- For wire changes, identify compatibility implications and the relevant draft section. Shared vectors establish coverage for their cases, not universal interoperability.

Keep reports focused. Missing information can be added during triage; there is no need to write a project proposal for a typo.

## Sending a pull request

1. Check repository-specific setup and contribution instructions. For broad API or protocol changes, discuss the use case in a non-sensitive issue before investing in a large patch.
2. Make one coherent change. Avoid unrelated formatting, generated-file churn or dependency upgrades.
3. Add a regression test where behavior changes. For protocol work, consider malformed frames, lifecycle/cancellation, queue bounds and relevant vectors; run the target repository's documented checks.
4. Explain why the change is needed, how it was checked and any compatibility impact. Say explicitly when a check was not run.

Documentation, examples and review are welcome too. Maintainers may ask for a smaller scope, more evidence or a different layer for the fix. Triage and review happen as capacity allows; this guide promises no response or release schedule.

## Security and sensitive data

**Never open a public issue or pull request with vulnerability details.** Do not attach secrets, private keys, tokens, traffic keylogs, decrypted private payloads or real private packet captures. Use synthetic fixtures and test-only identities for ordinary bug reports. Check logs and attachments before posting; redaction alone is not a reason to upload a real private capture.

For the Go and Rust projects, follow their existing security policies first:

- [dgproto-go SECURITY.md](https://github.com/datagram-messenger/dgproto-go/blob/main/SECURITY.md)
- [dgproto-rs SECURITY.md](https://github.com/datagram-messenger/dgproto-rs/blob/main/SECURITY.md)

Use GitHub's **Security → Advisories → Report a vulnerability** private reporting route only if the target repository has private vulnerability reporting enabled and that option is available. An advisories page by itself does not establish a private reporting channel.

If no private route is documented or enabled, **do not publish the details**. Ask a maintainer privately for a reporting route through an existing, verified private channel, without sending exploit details until the route is confirmed. If no such channel is known, keep the details private until a verified route becomes available. This organization guide invents no email address, disclosure policy or response SLA.

## Working together

Be specific and considerate: explain trade-offs, review the change rather than the person and separate observed behavior from assumptions. Respect any repository-specific conduct policy. Thank you for helping build an inspectable engineering foundation for a privacy-first messenger.
