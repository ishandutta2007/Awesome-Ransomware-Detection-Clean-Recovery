# Awesome-Ransomware-Detection-Clean-Recovery

# Awesome Ransomware Detection & Clean Recovery

> A curated list of top Ransomware Detection and Clean Recovery platforms — both SaaS/Hosted commercial security suites and open-source alternatives for detecting encryption behavior, stopping active attacks, and restoring clean data.
> 🌟 Star this repo if you find it useful! 🌟

---

## 📋 Table of Contents

- [SaaS / Hosted Platforms](#-saas--hosted-platforms)
  - [SentinelOne Singularity](#sentinelone-singularity)
  - [CrowdStrike Falcon](#crowdstrike-falcon)
  - [Sophos Intercept X](#sophos-intercept-x)
  - [Rubrik Security Cloud](#rubrik-security-cloud)
  - [Druva Ransomware Defense](#druva-ransomware-defense)
  - [Veeam Ransomware Guarantee](#veeam-ransomware-guarantee)
- [Open-Source Software](#-open-source-software)
  - [RansomShield](#ransomshield)
  - [Warden](#warden)
  - [honeyfile](#honeyfile)
  - [sentinel-watch](#sentinel-watch)
  - [endpoint-security-ai-agent](#endpoint-security-ai-agent)
  - [LockBit Rescue](#lockbit-rescue)
  - [RansomTriage](#ransomtriage)
  - [VaultSentry](#vaultsentry)
- [Comparison at a Glance](#-comparison-at-a-glance)
- [Contributing](#-contributing)

---

## 🟦 SaaS / Hosted Platforms

Commercial, cloud-hosted Ransomware Detection and Clean Recovery platforms. These are not open-source but are included as reference points for feature comparison.

### SentinelOne Singularity
**Type:** Autonomous endpoint protection with ransomware rollback
SentinelOne is known for its autonomous response capabilities, including automatic ransomware rollback to a clean state without analyst intervention. Its Storyline visualization connects related events across endpoints, and the agent is lightweight. It is often cited as the most autonomous of the major platforms for minimizing dwell time and automating containment.

### CrowdStrike Falcon
**Type:** AI-native endpoint protection with threat intelligence
CrowdStrike is strong for threat detection and visibility, with top-tier threat intelligence and named-adversary attribution. Its Falcon platform provides EDR with real-time response capabilities (RTR) for direct system access. It is particularly strong for heterogeneous OS fleets and large Linux server environments.

### Sophos Intercept X
**Type:** Deep learning endpoint protection with anti-ransomware
Intercept X is known for best-in-class ransomware defense through CryptoGuard and deep learning malware detection, with strong ransomware rollback capabilities. It is positioned for mid-market and lean-SOC organizations, often delivered through managed services (Taegis MDR).

### Rubrik Security Cloud
**Type:** Zero-trust data security with ransomware investigation
Rubrik provides immutable backup protection, advanced threat detection, and ransomware investigation. Its Threat Monitoring uses Rubrik threat intelligence feeds (YARA rules, file hashes) to scan backups, while Turbo Threat Hunting identifies affected snapshots across thousands of backups in seconds. Quarantining prevents malware reinfection during recovery.

### Druva Ransomware Defense
**Type:** SaaS data protection with ransomware resilience
Druva provides immutable, air-gapped backups in the Druva Cloud, with threat hunting capabilities over backup data. Its Cyber Resiliency features include ransomware detection, anomaly analysis, and audit trails, with view-only administrator roles for separation of duties. Remote data wipe capabilities protect data on lost or stolen devices even without an internet connection.

### Veeam Ransomware Guarantee
**Type:** Data resilience with immutable backups and AI-assisted security
Veeam Data Platform v13 includes immutable backups by default, a pre-hardened software appliance with automated patching, and AI-powered malware analysis. Its Malware Analysis Agent and Deep Data Analysis Agent within Veeam Intelligence help detect and respond to threats, with integrations into CrowdStrike, Palo Alto Networks, and Microsoft Sentinel.

---

## 🟩 Open-Source Software

Self-hosted, community-driven Ransomware Detection and Clean Recovery tools. The open-source ecosystem is **active and growing**, with strong options for behavioral detection, canary files, and recovery utilities.

### RansomShield
**Stack:** Rust / Linux (fanotify) | **License:** Open Source
RansomShield is a security daemon for Linux servers that protects against ransomware by monitoring file system activity through fanotify. It combines **entropy scoring**, **burst detection**, and **honeypot files** to identify and stop encryption. In testing across five distros, simulated ransomware was consistently detected and killed after 8 files (default `burst_file_count`), leaving the rest untouched, with only 8 of 300 files (2.7%) affected in a stress run—all recovered intact from quarantine. It includes a **directory-baseline gate** that prevents false positives on legitimate backup workloads, and an **allowlist** that narrows burst/entropy heuristics for trusted tools without disabling honeypot detection. Overhead is negligible (~2 MB RSS). It has been hardened through adversarial testing, fixing gaps like intermittent/partial-encryption evasion (now samples start, middle, and end) and brand-new-subdirectory bypasses [citation:5].
**Best for:** Linux server administrators wanting a production-tested, low-overhead daemon that detects and kills ransomware behavior while preserving untouched files and quarantining affected ones.

### Warden
**Stack:** Rust / Linux (fanotify / GTK4) | **License:** Open Source
Warden is a free, open-source EDR for Linux workstations written in Rust, with ransomware-specific defenses. It includes **fanotify filesystem monitoring**, **YARA scanning**, and **ransomware detection with per-PID, per-directory, and global counters** to catch fork-per-file attacks. Quarantine includes setuid-stripping and cross-process locking. The security model is hardened through adversarial testing: package-manager spoofing detection (checks directory, not just name), TOCTOU mitigations, and privileged action gating via `pkexec`. The GTK4 GUI provides live status, detection history, quarantine management, and exception management, with consequential actions requiring real authentication. It runs as root with systemd sandboxing (`ProtectSystem=strict`, `NoNewPrivileges`, `RestrictSUIDSGID`) [citation:14].
**Best for:** Linux workstation users wanting a focused, hardened open-source EDR with a desktop dashboard and ransomware-specific detection logic.

### honeyfile
**Stack:** Python | **License:** Open Source (PyPI)
honeyfile plants decoy files (Payroll, passwords, .env, backup.sql) and watches for any modification, deletion, or opening—any change is a tripwire signaling ransomware or an intruder. It uses **sha256 + size fingerprinting** to catch changes even when byte count is preserved, and the baseline manifest carries its own checksum to detect tampering. On Linux, it uses **inotify** to react instantly, catching a decoy merely being opened or read before anything is changed. It supports profiles (office, dev, db), webhook/exec alerts, and one-shot checks for cron. It is explicitly a detection tool, not an encryptor [citation:4].
**Best for:** Teams wanting a lightweight, low-false-positive tripwire that alerts the moment ransomware touches decoy files, without deploying a full EDR.

### sentinel-watch
**Stack:** Python | **License:** Open Source (PyPI)
sentinel-watch is a tiny folder watchdog that spots ransomware-like behavior and can block it. It uses four stacked rules: **burst** (N events in M seconds), **entropy** (Shannon on first 1MB), **canary** (`.sentinel/canary.txt` touched), and **notes/exts** (`.locked`, `READ_ME.txt`, words like bitcoin/decrypt). It maintains a **vault of clean copies** for restore, calculates a **risk score** for CI, and supports `watch --response auto` for automated response. It works on Linux and Windows, with no server or signup required [citation:11].
**Best for:** Users wanting a simple, pip-installable watchdog with clean-copy restore and risk scoring, particularly for personal or small-team folders.

### endpoint-security-ai-agent
**Stack:** Python / FastAPI / Next.js / Docker | **License:** Open Source
A full open-source **AI EDR** that detects and stops ransomware, Cobalt Strike, and living-off-the-land attacks in real time. Features include **ML-powered ransomware detection** (encrypted extensions, high entropy, rapid file changes), autonomous response (auto-kill, quarantine, host isolation), a **Next.js web dashboard** with real-time WebSocket updates, and a **ChatGPT-style AI analyst** for natural language incident queries. It uses osquery for telemetry and supports Windows, macOS, and Linux via Docker Compose [citation:6][citation:15].
**Best for:** Teams wanting a comprehensive open-source EDR with a modern web dashboard and AI-assisted analysis, accepting the Docker/FastAPI/Next.js stack requirements.

### LockBit Rescue
**Stack:** Python / C | **License:** Open Source
LockBit Rescue is a toolkit for recovering files encrypted by **LockBit 3.0 ("Black")** ransomware without paying, by exploiting a known keystream-reuse weakness. It auto-detects the ransomware extension, groups encrypted files by their RSA-encrypted KEK fingerprint, and recovers the Salsa20 keystream from a long-named file in each group (known-plaintext). It then decrypts other files in the group whose footer fits within the recovered keystream coverage. It is resumable and skips botched decryptions. **Limitation:** Specific to LockBit 3.0 and requires Linux x86_64 with gcc/make/Python [citation:3].
**Best for:** Victims of LockBit 3.0 ransomware with encrypted files on Linux, wanting a free recovery attempt without paying the ransom, accepting the narrow family-specific scope.

### RansomTriage
**Stack:** Python | **License:** Open Source (PyPI)
RansomTriage is a ransomware identification and triage tool that matches ransom-note text to known families and provides recovery guidance. It includes a catalog of **27+ families** (STOP/Djvu, LockBit, Akira, BlackCat, Black Basta, Phobos, Dharma, Play, Babuk, Hive, Rhysida, BianLian, WannaCry, GandCrab, REvil, and more) with decryptor status, free tools, and source URLs. It confirms a family only when note text matches distinctive phrases (not filenames or extensions alone), checks Bitcoin address checksums, and includes a **first-hour checklist** based on CISA/NIST guidance [citation:7].
**Best for:** Incident responders and victims needing rapid ransomware family identification and decryptor availability before deciding on recovery strategy.

### VaultSentry
**Stack:** Python | **License:** Open Source
VaultSentry monitors backup files nightly, hashing every file to detect tampering, ransomware encryption, corruption, missing files, and sudden size drops. It supports **named snapshots** at any point in time, diffing any two to see exactly what changed, one-click GUI restore, and a daily HTML digest email. It is focused specifically on backup integrity monitoring rather than live endpoint detection [citation:1].
**Best for:** Teams wanting to verify the integrity of their backup files against tampering or encryption, complementing live endpoint detection with a recovery-focused safety net.

---

## 📊 Comparison at a Glance

| Software | License | Stack | Detection Method | Automated Response | Recovery Focus | Self-Hosted | Best For |
|----------|---------|-------|------------------|---------------------|----------------|-------------|----------|
| **SentinelOne** | Proprietary | Cloud | Behavioral AI | ✅ Rollback | ✅ | ❌ | Autonomous endpoint rollback |
| **CrowdStrike** | Proprietary | Cloud | AI + threat intel | ✅ RTR | (Backup dependent) | ❌ | Threat intel + response |
| **Rubrik** | Proprietary | Cloud/Appliance | YARA + threat intel | ✅ Quarantine | ✅ Immutable backups | (Appliance) | Ransomware investigation + recovery |
| **Druva** | Proprietary | Cloud | Anomaly + audit | ✅ Remote wipe | ✅ Air-gapped backups | ❌ | SaaS data protection + recovery |
| **RansomShield** | Open Source | Rust/Linux | Entropy + burst + honeypot | ✅ Kill process | ✅ Quarantine restore | ✅ | Linux server protection |
| **Warden** | Open Source | Rust/Linux | Entropy + YARA + honeypot | ✅ Kill + quarantine | ✅ Quarantine | ✅ | Linux workstation EDR |
| **honeyfile** | Open Source | Python | Canary tripwire | ✅ Alert/webhook/exec | (Alert only) | ✅ | Early warning tripwire |
| **sentinel-watch** | Open Source | Python | Burst + entropy + canary | ✅ Kill (auto mode) | ✅ Clean vault | ✅ | Simple folder watchdog |
| **endpoint-security-ai-agent** | Open Source | Python/FastAPI | ML + heuristics | ✅ Kill + isolate | ✅ Quarantine | ✅ | Full EDR + AI dashboard |
| **LockBit Rescue** | Open Source | Python/C | N/A (recovery tool) | N/A | ✅ Decrypt LockBit 3.0 | ✅ | LockBit 3.0 file recovery |
| **RansomTriage** | Open Source | Python | Note text matching | ❌ (Guidance) | (Guidance) | ✅ | Family ID + decryptor guidance |

---

## 🤝 Contributing

Contributions are welcome! If you know of an open-source Ransomware Detection or Clean Recovery tool that should be listed here, please open a pull request with:

- Project name and URL
- Brief description (1–2 sentences)
- Stack and license
- Why it stands out

Please ensure the project is actively maintained (releases within the last 12 months) and genuinely open-source. Note that the open-source ecosystem **splits** between **detection and response** (RansomShield, Warden, honeyfile, sentinel-watch, endpoint-security-ai-agent) and **recovery utilities** (LockBit Rescue, RansomTriage, VaultSentry). **RansomShield** and **Warden** are the most hardened open-source detection daemons for Linux, both validated through adversarial testing and offering quarantine-based recovery [citation:5][citation:14]. **honeyfile** offers a uniquely simple tripwire approach with strong false-positive avoidance [citation:4]. For recovery, **LockBit Rescue** provides a free decryption path for LockBit 3.0 victims [citation:3], while **RansomTriage** helps identify the family and available decryptors before committing to a recovery strategy [citation:7]. Commercial platforms like SentinelOne and Rubrik remain far more capable for enterprise-scale autonomous response and immutable backup recovery.

---

## 📄 License

This list is released under CC0 1.0 Universal (Public Domain). The software projects listed retain their respective licenses.

---

⭐ **If this list helped you discover a useful tool, please star the repo!** ⭐
