<h1 align="center">Openxos</h1>

<p align="center">
  Open-source security and developer tooling.<br>
  CLI-first · Plugin-driven · Privacy-first · Zero telemetry
</p>

<p align="center">
  <img src="https://img.shields.io/badge/license-MIT-green?style=flat-square" />
  <img src="https://img.shields.io/badge/status-active-brightgreen?style=flat-square" />
  <img src="https://img.shields.io/badge/built%20with-Rust%20%7C%20Python-orange?style=flat-square" />
  <img src="https://img.shields.io/badge/platform-Linux%20%7C%20Windows%20%7C%20Android-blue?style=flat-square" />
</p>

---

## What is Openxos?

Openxos is a collection of free, open-source tools for security practitioners,
bug bounty hunters, and developers. Every tool is self-hosted, runs offline,
and produces clean JSON or Markdown output that integrates with any workflow.

No accounts. No cloud dependency. No tracking.

---

## Tools

| Tool | Description | Language | Status |
|---|---|---|---|
| [`openxos-recon`](./openxos-recon) | Subdomain enumeration + asset discovery | Rust | 🔨 Building |
| [`openxos-audit`](./openxos-audit) | HTTP header + TLS configuration auditor | Python | 📋 Planned |
| [`openxos-scan`](./openxos-scan) | Port scanner with service fingerprinting | Rust | 📋 Planned |
| [`openxos-fuzz`](./openxos-fuzz) | Parameter fuzzer for bug bounty workflows | Python | 📋 Planned |
| [`openxos-report`](./openxos-report) | Vulnerability report generator (MD + JSON) | Python | 📋 Planned |
| [`openxos-sdk`](./openxos-sdk) | Python plugin SDK — extend any Openxos tool | Python | 🔨 Building |

---

## Quick Start

```bash
# Install openxos-recon (available after v0.1 release)
cargo install openxos-recon

# Run subdomain enumeration
openxos-recon --target example.com --output report.json
```

---

## Philosophy

- **Free core, always.** Every tool in this org is MIT-licensed and free forever.
- **Self-hosted.** Nothing calls home. You own your data and your results.
- **Plugin-first.** Every tool accepts plugins via the `openxos-sdk`.
- **Low footprint.** Core tools written in Rust — minimal memory, maximum speed.

---

## Contributing

Read [CONTRIBUTING.md](https://github.com/Openxosdev/.github/blob/main/CONTRIBUTING.md)
before submitting a PR. Issues and feature requests are open.

---

## Support Openxos

Openxos is built solo, in free time, with zero funding.
If these tools saved you time on a bug bounty or audit, consider supporting:

**Monero (XMR) — fully anonymous, no middleman:**

49DDzakQJoKKq5caPdeZMH1JoC1GERzbnTw7RFx5Zq4xFLiXgkNgxuEau4rXH3f5V29cbXPB4bxk1dy1YKxAiwZ9LvkaUCv

Monero transactions are cryptographically private.
No account, no KYC, no tracking.
Funds go toward domain registration, hosting, and development time.

---

<p align="center">
  <sub>Built by <a href="https://github.com/getxeyronoxz">@getxeyronoxz</a> ·
  License · No corporate backing</sub>
</p>

