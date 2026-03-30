# 🦉 OSharp

<p align="center">
  <img src="https://img.shields.io/badge/Platform-Linux-informational?style=flat-square&logo=linux&logoColor=white&color=0a0c10"/>
  <img src="https://img.shields.io/badge/Category-OCore%20%2F%20Purple%20Team-blueviolet?style=flat-square"/>
  <img src="https://img.shields.io/badge/MITRE-ATT%26CK-red?style=flat-square"/>
  <img src="https://img.shields.io/badge/License-MIT-green?style=flat-square"/>
  <img src="https://img.shields.io/badge/Part%20of-OwlSec%20Toolkit-7b5ea7?style=flat-square"/>
  <img src="https://img.shields.io/badge/Version-2.0-cyan?style=flat-square"/>
</p>

> **OSharp** is a Purple Team simulator that safely emulates 7 MITRE ATT&CK adversary techniques on Linux — generating real telemetry for EDR, XDR, and SIEM validation without any actual exploitation or damage.

---

> ⚠️ **AUTHORISED SECURITY TESTING ONLY** — Use only on systems you own or have explicit written permission to test.

---

## 📌 Overview

OSharp executes benign but realistic adversary-like actions that your security stack should detect and alert on. Every action is logged with MITRE technique ID, severity, and context, and all artifacts are auto-cleaned after simulation. The session can be exported as a full JSON report for analyst review.

---

## 🛡️ Safety Guardrails

- ✅ **Non-destructive only** — no real exploitation, no payload execution
- ✅ **Lateral movement** — private and localhost IPs only by default, public requires explicit confirmation
- ✅ **No brute force** — no credentials, no authentication attempts
- ✅ **Auto-cleanup** — all created files removed after simulation (configurable per module)
- ✅ **No persistence** — no cron jobs, no run keys, no startup entries written

---

## 🖥️ Modules

| # | Module | MITRE | Description |
|---|--------|-------|-------------|
| **1** | **Process Injection** | T1055 | Reads `/proc/self/maps`, spawns Python/Bash child processes, attempts `/proc/self/mem` access — generates injection-like indicators |
| **2** | **Credential Access** | T1003 | Runs `id`, `whoami`, reads `/etc/passwd`, enumerates groups, recent logins, finds `.ssh` directories, attempts `/etc/shadow` access |
| **3** | **Script Execution** | T1059 | Executes benign Bash `-c`, Python `-c` with socket import, Perl `-e`, base64-encoded bash payload, and curl-pipe-bash simulation |
| **4** | **File Activity** | T1105 | Creates files in `/tmp`, `/dev/shm`, and `~/.config` with suspicious names, sets `chmod 755`, simulates dropper pattern (write + move) |
| **5** | **HTTP Beaconing** | T1071.001 | Sends configurable GET/POST HTTP beacons to a target URL with jitter delays, custom User-Agent rotation, and retry logic |
| **6** | **Payload Obfuscation** | T1027 | Generates XOR + Base64 encoded binary artifacts in `/tmp` with random filenames, writes a decoder reference note |
| **7** | **Lateral Movement** | T1021 | TCP connectivity probes to SSH, SMB, RDP, MySQL, Redis, VNC, NFS, and 3 more ports — no authentication, no exploitation |
| **8** | **Full Chain** | All | Runs all 7 modules in sequence with cleanup enabled |
| **9** | **Export Report** | — | Save full JSON report to `osharp_report_YYYYMMDD_HHMMSS.json` |

---

## 🎯 MITRE ATT&CK Coverage

| Technique | ID | What OSharp Simulates |
|-----------|----|-----------------------|
| Process Injection | T1055 | `/proc/self/maps` read, child process spawn, `/proc/self/mem` access |
| OS Credential Dumping | T1003 | `/etc/passwd` read, `.ssh` discovery, `/etc/shadow` access attempt |
| Command & Scripting Interpreter | T1059 | Bash / Python / Perl one-liners, base64-encoded command execution |
| Ingress Tool Transfer | T1105 | File drop to `/tmp` and `/dev/shm`, executable permissions set |
| Application Layer Protocol | T1071.001 | HTTP/S beaconing with jitter, user-agent rotation, retry with backoff |
| Obfuscated Files or Information | T1027 | XOR-encrypted + Base64-encoded binary artifacts |
| Remote Services | T1021 | TCP port probes to 10 lateral movement target ports |

---

## 🚨 Expected Detections

Use OSharp to verify your EDR/SIEM alerts on:

**Process & Memory**
- `/proc/self/maps` read by non-system process
- Python/Bash child process spawned with inline code
- `/proc/self/mem` access attempt

**Credential Access**
- `/etc/passwd` accessed by non-privileged process
- `.ssh` directory enumeration
- `/etc/shadow` access attempt

**Script Execution**
- `bash -c` / `python3 -c` / `perl -e` execution
- Base64-decoded command execution via `bash -c "... | base64 -d | bash"`

**File System**
- Executable files created in `/tmp`, `/dev/shm`, `~/.config`
- `chmod 755` applied to newly created files
- File write → move pattern (dropper behaviour)

**Network**
- Repeated HTTP requests with jitter (beaconing pattern)
- TCP connection attempts to SSH, SMB, RDP, Redis, VNC

**Obfuscation**
- Binary files with high entropy created in temp directories

---

## 📤 Report

Each module logs events in real-time and a full JSON report can be exported containing tool metadata, host, user, total event count, severity summary, and every individual event with timestamp, module, MITRE technique, action, severity, and details.

```
osharp_report_YYYYMMDD_HHMMSS.json
```

Severity levels: `Critical` · `High` · `Medium` · `Low` · `Info`

---

## ⚙️ Requirements

- **Linux** (any modern distro) — will not run on Windows
- **No Python installation needed** — runs as a standalone executable

---

## 🚀 Usage

```bash
./OSharp
```

---

## 📦 Part of OwlSec Toolkit

This tool is part of the **OwlSec** suite — a collection of 300+ security and privacy tools.

🔗 [owlsec.org](https://owlsec.org)

---

## ©️ License

MIT License — © Khaled S. Haddad

*Tools are distributed as pre-built executables. Source code is proprietary.*
