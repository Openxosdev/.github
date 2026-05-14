<div align="center">

# Openxos

**Open-source security reconnaissance framework for bug bounty hunters and penetration testers**

[![License: MIT](https://img.shields.io/badge/license-MIT-00c896?style=flat-square)](./LICENSE)
[![Tools](https://img.shields.io/badge/tools-2%20active-00c896?style=flat-square)](#)
[![Language](https://img.shields.io/badge/language-Rust-orange?style=flat-square)](#)
[![Tests](https://img.shields.io/badge/tests-144%20passing-00c896?style=flat-square)](#)

*Building professional security tools that find real vulnerabilities in production environments*

[Tools](#-tools) • [Workflow](#-workflow) • [Validation](#-real-world-validation) • [Philosophy](#-philosophy)

</div>

---

## 🎯 Mission

Openxos provides purpose-built reconnaissance tools that bridge the gap between basic HTTP probing and comprehensive security analysis. Every tool in this ecosystem is designed to solve actual problems encountered during bug bounty hunting and penetration testing engagements, with proven effectiveness on production infrastructure.

The framework follows a two-stage reconnaissance methodology that mirrors professional red team operations. Initial surgical reconnaissance identifies defensive posture and safe operational parameters. Large-scale analysis then executes efficiently within those constraints, maximizing discovery while minimizing detection risk.

---

## 🛠️ Tools

### Openxos-ghost `v0.1.2`

Surgical reconnaissance tool that scouts target infrastructure before committing to large-scale analysis. Ghost identifies web application firewalls, determines safe request patterns, and provides intelligence that informs scanning strategy for subsequent tools.

**Core capabilities:** WAF detection and fingerprinting, defensive posture analysis, evasion pattern identification, professional markdown reporting with context explaining significance of findings, header rotation and request jitter for stealth operations.

**Use case:** Run ghost first on any new target to understand defensive infrastructure and establish safe operational parameters before executing broad reconnaissance.

[View Repository →](https://github.com/Openxosdev/openxos-ghost)

### Openxos-probe `v0.1.2`

High-performance HTTP reconnaissance engine built for speed and scale after initial target intelligence gathering. Probe analyzes hundreds of targets per minute while conducting comprehensive security assessment across multiple dimensions.

**Core capabilities:** Parallel HTTP and HTTPS probing with async execution, technology detection across 200+ signatures using SIMD-accelerated pattern matching, comprehensive security analysis including headers, cookies, TLS configuration, and caching behavior, subdomain takeover detection for AWS S3, Heroku, GitHub Pages, GitLab, and Bitbucket, WAF identification for Cloudflare, Akamai, Imperva, AWS WAF, Sucuri, Fastly, and Incapsula, cloud provider fingerprinting for AWS, GCP, Azure, Vercel, Netlify, DigitalOcean, Heroku, and Cloudflare, API surface discovery including GraphQL introspection, WebSocket endpoints, and OpenAPI documentation, HTTP method enumeration testing PUT, DELETE, TRACE, and WebDAV methods, certificate transparency integration for additional subdomain discovery.

**Performance:** Typical analysis completes in approximately twenty seconds for seven targets with full security assessment. Configurable scanning modes support fast surface checks, normal comprehensive analysis, or aggressive deep testing including method enumeration and rate limit probing.

**Use case:** Execute after ghost provides defensive intelligence, or use standalone for targets with known safe operational parameters.

[View Repository →](https://github.com/Openxosdev/openxos-probe)

---

## 🔄 Workflow

The Openxos framework implements a two-stage reconnaissance methodology validated through real-world testing on production infrastructure.

**Stage One: Surgical Reconnaissance**

Execute openxos-ghost against the primary target domain to identify defensive infrastructure and establish safe operational parameters. Ghost detects web application firewalls, analyzes response patterns, and generates intelligence about how to interact with the target without triggering defensive controls. The output includes specific recommendations for concurrency limits, timeout values, and request patterns that respect the target's infrastructure.

**Stage Two: Large-Scale Analysis**

Configure openxos-probe using intelligence gathered during stage one. Probe executes comprehensive security analysis across all discovered subdomains while respecting the defensive posture identified by ghost. The result is efficient reconnaissance that maximizes discovery while minimizing detection risk.

**Example workflow:** Initial ghost reconnaissance of microsoft.com identified defensive patterns and safe request parameters. Subsequent probe analysis of seven microsoft.com subdomains completed in approximately twenty seconds and discovered thirty-six security findings without triggering rate limits or defensive responses.

**Pipeline integration:** Tools accept input via file or stdin, enabling direct pipeline composition. Subdomain enumeration results flow directly into security analysis without intermediate file management.

---

## ✅ Real-World Validation

All Openxos tools undergo validation against production infrastructure before release. Version 0.1.2 has been tested against major technology companies and cloud service providers with documented results.

**Microsoft Corporation reconnaissance:** Analysis of seven microsoft.com subdomains identified thirty-six security issues across multiple severity levels. Testing validated that the two-stage approach successfully navigated defensive infrastructure while maintaining complete analysis coverage.

**Technology company testing:** Separate validation against ten production domains including api.stripe.com, sentry.io, api.github.com, auth.docker.io, and grafana.com discovered forty-seven total findings. Results included two high severity issues, seventeen medium severity findings, and twenty-eight low severity observations.

**Confirmed discoveries:** api.github.com supports PUT, DELETE, and TRACE methods representing exploitable attack surface. sentry.io exposes source maps constituting high severity information disclosure. auth.docker.io caches sensitive authentication endpoints creating session security risks. Multiple targets exhibit missing security headers, improper cookie configuration, and weak TLS cipher suites.

**Quality assurance:** The probe tool maintains 144 passing tests covering HTTP client behavior, technology detection, security analysis, database operations, and output formatting. All features undergo integration testing against controlled infrastructure before production deployment.

---

## 💡 Philosophy

**Operational sovereignty.** Every tool operates entirely on the user's infrastructure without external dependencies. No tool contacts remote services, transmits telemetry, or requires account creation. All reconnaissance data remains under the operator's exclusive control within local SQLite databases.

**Proven effectiveness.** Tools are validated against production infrastructure before release. Real-world testing against major technology companies confirms that Openxos tools discover actual vulnerabilities rather than theoretical issues. The framework has identified confirmed security findings in infrastructure operated by Stripe, GitHub, Docker, Sentry, and Microsoft.

**Performance through design.** Core tools are implemented in Rust using async execution patterns that maximize throughput while minimizing resource consumption. Technology detection uses SIMD-accelerated algorithms rather than sequential pattern matching. DNS resolution employs aggressive caching with measured hit rates exceeding ninety percent on typical workloads.

**Professional workflow.** The two-stage reconnaissance methodology mirrors how experienced security practitioners actually operate. Initial surgical reconnaissance establishes situational awareness before committing to large-scale analysis. This approach reduces operational risk while improving efficiency compared to naive scanning strategies.

**Permanent availability.** All tools carry MIT licenses guaranteeing perpetual free availability without usage restrictions or commercial pressure. The organization maintains no venture backing, corporate sponsorship, or monetization strategy that could compromise tool independence or introduce usage limitations.

---

## 🔬 Technical Foundation

The Openxos framework is built on carefully selected technologies chosen for operational characteristics rather than popularity or familiarity.

**Core implementation language:** Rust provides memory safety guarantees that prevent entire vulnerability classes while delivering performance characteristics suitable for security tooling. The async execution model using the Tokio runtime enables efficient concurrent operations across hundreds of targets without proportional resource scaling.

**Pattern matching optimization:** Technology detection employs the Aho-Corasick algorithm for literal string matching and compiled regular expression sets for parallel pattern evaluation. These approaches deliver five to ten times faster matching compared to sequential regex testing while maintaining accuracy.

**Network optimization:** HTTP client configuration includes connection pooling with per-host limits, HTTP/2 multiplexing eliminating protocol negotiation overhead, aggressive timeout values preventing resource waste on unresponsive targets, and TLS session resumption enabling fast reconnection without full handshake overhead.

**Storage architecture:** SQLite provides embedded persistence without external database dependencies. Write-ahead logging mode enables concurrent reads during write operations. Prepared statement caching eliminates parse overhead on repeated queries. Batched transaction writes reduce fsync calls while maintaining crash safety.

**DNS resolution:** Custom resolver implementation uses trust-dns-resolver with in-memory caching and five-minute TTL. Measured cache hit rates exceed ninety percent on reconnaissance workloads. Parallel A and AAAA record queries eliminate sequential lookup overhead for dual-stack targets.

---

## 📊 Development Status

The Openxos organization maintains an active development schedule with regular minor version releases addressing functionality improvements and bug fixes. Current focus areas include deeper integration between ghost and probe tools through shared configuration profiles, unified database schemas enabling cross-tool intelligence correlation, and synchronized signature databases eliminating redundant fingerprinting logic.

**Version 0.1.2** represents the current stable release across both tools. This version includes all core reconnaissance capabilities, comprehensive security analysis features, and validated effectiveness against production infrastructure. The codebase maintains 144 passing tests with complete coverage of critical functionality paths.

**Upcoming development priorities** include export of evasion profiles from ghost for direct import into probe, shared SQLite schema enabling unified security intelligence databases, signature synchronization allowing probe to leverage ghost's advanced fingerprinting capabilities, and HTML report generation for client deliverables and program submissions.

---

## 🤝 Contributing

Openxos welcomes contributions from security practitioners who share the vision of building professional reconnaissance tools with proven real-world effectiveness. Priority areas for community contribution include expanding technology signature databases to cover additional frameworks and platforms, adding WAF fingerprints for defensive products not currently detected, identifying cloud provider patterns for emerging infrastructure services, and improving documentation based on actual operational usage.

The organization maintains clear contribution guidelines prioritizing code quality, test coverage, and alignment with the existing architecture. All contributions undergo review for technical correctness, performance impact, and compatibility with the framework's operational sovereignty principles.

---

## 📄 License

All Openxos tools are released under the MIT License, guaranteeing perpetual free availability without restrictions on usage, modification, or redistribution. The license explicitly permits commercial use, private modification, and distribution of modified versions while requiring only attribution preservation.

This licensing choice reflects the organization's commitment to permanent public availability and rejection of monetization strategies that could introduce usage restrictions or compromise tool independence.

---

## 💰 Support

Openxos operates as an independent, unfunded project maintained by a single developer without corporate sponsorship or venture backing. All tool development occurs during personal time without external financial support or commercial pressure.

If the Openxos framework has provided value during your security research or bug bounty hunting activities, financial contributions help sustain continued development and maintenance. Support is entirely voluntary and carries no expectation of priority support, feature implementation, or special access.

**Monero (XMR)** — privacy-preserving cryptocurrency without intermediary services

```
49DDzakQJoKKq5caPdeZMH1JoC1GERzbnTw7RFx5Zq4xFLiXgkNgxuEau4rXH3f5V29cbXPB4bxk1dy1YKxAiwZ9LvkaUCv
```

---

<div align="center">

**Openxos** • Building professional security tools for practitioners who demand sovereignty

Maintained by [@getxeyronoxz](https://github.com/getxeyronoxz) • [openxos-ghost](https://github.com/Openxosdev/openxos-ghost) • [openxos-probe](https://github.com/Openxosdev/openxos-probe)

</div>

**Sovereignty.** No tool contacts external services, collects telemetry, or requires an account. All data stays on the operator's machine.

**Efficiency.** Core tooling is written in Rust to minimize memory consumption and maximize execution speed — a deliberate choice, not a default.

---

### Support

Openxos is an independent, unfunded project maintained by a single developer. If this work has been of value to you, contributions are appreciated.

**Monero (XMR) — private, no intermediary**

```
49DDzakQJoKKq5caPdeZMH1JoC1GERzbnTw7RFx5Zq4xFLiXgkNgxuEau4rXH3f5V29cbXPB4bxk1dy1YKxAiwZ9LvkaUCv
```

---

<div align="center">
<sub>Maintained by <a href="https://github.com/getxeyronoxz">@getxeyronoxz</a> &nbsp;·&nbsp; MIT License</sub>
</div>
