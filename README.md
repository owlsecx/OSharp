# 🦉 OSharp

<p align="center">
  <img src="https://img.shields.io/badge/Platform-Linux-0a0c10?style=flat-square"/>
  <img src="https://img.shields.io/badge/Category-OAttack%20/%20Offensive-blue?style=flat-square"/>
  <img src="https://img.shields.io/badge/License-Proprietary-orange?style=flat-square"/>
  <img src="https://img.shields.io/badge/Part%20of-OwlSec%20Toolkit-7b5ea7?style=flat-square"/>
  <img src="https://img.shields.io/badge/Version-1.0-cyan?style=flat-square"/>
</p>

> **OSharp** — Purple Team Simulator

---

> ⚠️ **AUTHORISED USE ONLY** — Use only on systems you own or have explicit written permission to test. Unauthorised use is illegal.

---

## 📌 Overview


OSharp is a purple-team adversary-simulation tool for Linux that safely reproduces common attacker techniques for detection engineering. It runs non-destructively and keeps lateral simulation to localhost and private IPs by default. Each technique is mapped to MITRE ATT&CK (T1055, T1003, T1059, T1105, T1071.001 and more) so blue teams can validate their telemetry.

---

## ✨ Features


- Safe simulation of MITRE techniques: process injection, credential access, command execution, ingress transfer and C2 patterns
- Strictly non-destructive — no real exploitation, brute force, credentials or persistence
- Lateral-movement simulation restricted to localhost / private IPs by default
- Automatic cleanup of every file it creates, with strict timeouts and output capture on all subprocess calls
- JSON reporting plus a persistent osharp.cfg configuration and osharp_reports output directory
- Offline, sandboxed --self-test mode for verifying the engine without a target

---

## ⚙️ Requirements

- **Linux**
- **No Python installation needed** — runs as a standalone executable

---

## 🚀 Usage


```bash
./OSharp
./OSharp --self-test
./OSharp --help
```

---

## 📦 Part of OwlSec Toolkit

This tool is part of the **OwlSec** suite — a collection of 275+ security and privacy tools.

🔗 [owlsec.org](https://owlsec.org)

---

## ©️ License

Proprietary — © 2026 Owlsec LLC. All rights reserved.

*Tools are distributed as pre-built executables. Source code is proprietary.*

---

## 🔍 Verification & Transparency

This tool is closed-source. These files let you see exactly what is inside it,
without the source:

- [`SBOM.cdx.json`](SBOM.cdx.json) — CycloneDX inventory: SHA-256 of this
  binary, bundled CPython version, and every bundled library with its exact
  version and license. Feed it to Grype, Trivy or Dependency-Track to audit
  our dependencies for CVEs yourself.
- [`THIRD-PARTY-NOTICES.md`](THIRD-PARTY-NOTICES.md) — the full license text
  of every third-party component, extracted from this binary.

**No telemetry, no analytics, no licence check-in.** This tool does not phone
home. Verify that claim yourself:

```bash
sudo strace -f -e trace=network ./OSharp --help   # watch every network call
firejail --net=none ./OSharp --help               # deny the network entirely
```

Release signing, GPL compliance and vulnerability reporting:
[**TRUST.md**](https://github.com/owlsecx/owl-os/blob/main/TRUST.md)
