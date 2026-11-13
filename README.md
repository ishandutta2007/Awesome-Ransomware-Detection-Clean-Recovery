# Awesome Ransomware Detection & Clean Recovery

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![Track Awesome List](https://www.trackawesomelist.com/badge.svg)](https://www.trackawesomelist.com/ishandutta2007/Awesome-Ransomware-Detection-Clean-Recovery/)
[![License: CC0-1.0](https://img.shields.io/badge/License-CC0_1.0-lightgrey.svg)](http://creativecommons.org/publicdomain/zero/1.0/)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](https://github.com/ishandutta2007/Awesome-Ransomware-Detection-Clean-Recovery/pulls)

> A curated list of top **Ransomware Detection and Clean Recovery** platforms — both enterprise SaaS/Hosted commercial security suites and open-source software for behavioral ransomware detection, canary tripwires, instant rollback, automated isolation, and clean data recovery.
>
> 🌟 Star this repo if you find it useful! 🌟

---

## 📋 Table of Contents

- [Sector Overview & Market Dynamics](#-sector-overview--market-dynamics)
- [SaaS / Hosted Platforms](#-saas--hosted-platforms)
- [Open-Source Software](#-open-source-software)
- [Comparison at a Glance](#-comparison-at-a-glance)
- [Contributing](#-contributing)
- [License](#-license)

---

## 🌐 Sector Overview & Market Dynamics

The global ransomware protection and recovery market is estimated at **$30.0 Billion to $32.0 Billion** and is projected to expand to **$87.6 Billion to $109.9 Billion** by the mid-2030s, exhibiting a compound annual growth rate (CAGR) of **14.5% to 16.5%**. The sector is **moderately to highly fragmented** rather than a winner-take-all landscape: while platform titans dominate core endpoint XDR and enterprise backup infrastructure, specialized niche vendors thrive across honeypot/canary detection, zero-trust storage validation, memory-dump key extraction, and family-specific decryptor tools.

---

## 🟦 SaaS / Hosted Platforms

Commercial, cloud-hosted Ransomware Detection and Clean Recovery suites. Listed in descending order of company size (valuation / market capitalization).

| Platform | Company Size (Valuation / Market Cap / Revenue) | Starting Pricing (Specific Tier) | Free Tier / Trial Limit | Key Ransomware Detection & Clean Recovery Capabilities |
| :--- | :--- | :--- | :--- | :--- |
| **CrowdStrike Falcon** | **$225B+ Market Cap** (~$4.81B Annual Revenue) | **$59.99 / device / year** ($4.99/mo equivalent, Falcon Go tier; Falcon Pro starts at $99.99/device/year) | **15-day free trial** (up to 100 devices; full access to Falcon Prevent NGAV, Device Control, and USB inspection without credit card) | AI-native endpoint detection and response (EDR/XDR), automated host network isolation, real-time response (RTR) forensic remediation, and Overwatch threat hunting. |
| **Rubrik Security Cloud** | **$22B+ Market Cap** (~$1.32B Annual Revenue) | **$150+ / TB / year** (Universal Cloud Data Management subscription; typical enterprise deployments start at ~$25,000 to $50,000/year contract value) | **30-day free trial** (SaaS protection trial strictly capped at **500 M365 users** and **10 TB Data Protection Capacity**, or Google Workspace trial capped at 10 users & 500 GB) | Immutable backup snapshots, YARA threat hunting across historical backup snapshots, anomaly encryption blast-radius detection, and quarantine recovery to prevent reinfection. |
| **Veeam Data Platform** | **$15B Valuation** (~$2.0B+ ARR) | **$155 / workload / year** (Veeam Universal License [VUL] Foundation tier, sold in 10-workload packs at $1,550/year; Advanced tier starts at $189/workload/year) | **Forever-free plan (Community Edition): up to 10 workloads** with full backup & recovery; **30-day free trial** of Enterprise/Premium tier with unlimited workloads | Pre-hardened software appliance, zero-trust immutable backup repositories, real-time inline I/O entropy scanning, and automated clean disaster recovery orchestration. |
| **SentinelOne Singularity** | **$8.0B+ Market Cap** (~$1.0B ARR) | **$69.99 / endpoint / year** (Singularity Core tier; Singularity Complete EDR with Rollback starts at $179.99/endpoint/year) | **30-day free trial** (Proof-of-Concept license through sales/authorized partners, supporting up to 100-500 test endpoints; no credit-card required) | Autonomous behavioral AI engine, Storyline cross-process telemetry correlation, and instant 1-click VSS/kernel-driver automated rollback to restore pristine unencrypted files. |
| **Sophos Intercept X** | **$4.0B Valuation** (~$1.0B+ Revenue) | **$35.00 / user / year** (Intercept X Advanced endpoint license for 100-499 seats; ~$59.00/user/year for smaller 10-49 seat deployments) | **30-day free trial** (Full access to Sophos Central and Intercept X Advanced with XDR for up to 1,000 users/endpoints) | CryptoGuard anti-ransomware driver that inspects file header modifications and automatically halts rogue encryption processes while rolling back affected files from local cache. |
| **Druva Cyber Resilience** | **$2.0B Valuation** (~$200M+ SaaS ARR) | **$2.50 / user / month** (~$30.00/user/year, Druva inSync Cloud Apps Enterprise; Endpoint Protection starts at $4.00/user/month billed annually) | **30-day free trial** (Self-service evaluation tenant with interactive onboarding; extendable up to a **hard cap of 60 days** before requiring commercial upgrade) | 100% cloud-native SaaS backup, air-gapped immutable cloud vault, automated unusual entropy and bulk modification anomaly detection, with curated clean recovery points. |

---

## 🟩 Open-Source Software

Self-hosted, community-driven tools for behavioral detection, canary file tripwires, kernel-level eBPF monitoring, and free cryptographic recovery decryptors. 

Sorted in descending order by GitHub stargazers count:

### 1. [Raccine](https://github.com/Neo23x0/Raccine) [![GitHub stars](https://img.shields.io/github/stars/Neo23x0/Raccine?style=social&color=white)](https://github.com/Neo23x0/Raccine/stargazers)
- **GitHub:** [Neo23x0/Raccine](https://github.com/Neo23x0/Raccine)
- **Stack:** C++ / Windows (Registry Hooks & Image File Execution Options - IFEO) | **License:** Apache-2.0
- **Capabilities:** A lightweight ransomware vaccine that intercepts process creation calls to `vssadmin.exe`, `wmic.exe`, `wbadmin.exe`, `bcdedit.exe`, and `powershell.exe`. By preemptively intercepting command-line parameters commonly used by ransomware families to delete Shadow Copies or disable recovery options, Raccine immediately kills the calling process tree before encryption starts.
- **Best for:** Windows endpoints and servers requiring an instant, zero-overhead behavioral vaccine against shadow copy deletion.

### 2. [Decryptonite](https://github.com/DecryptoniteTeam/Decryptonite) [![GitHub stars](https://img.shields.io/github/stars/DecryptoniteTeam/Decryptonite?style=social&color=white)](https://github.com/DecryptoniteTeam/Decryptonite/stargazers)
- **GitHub:** [DecryptoniteTeam/Decryptonite](https://github.com/DecryptoniteTeam/Decryptonite)
- **Stack:** Python / C / Windows & Linux | **License:** Open Source
- **Capabilities:** A dedicated ransomware detection and mitigation software engine that inspects active file modifications across monitored directories. Utilizes behavioral heuristics to flag rapid mass file renames, unexpected extensions, and entropy spikes, killing malicious threads and isolating untrusted processes.
- **Best for:** Blue teams and system operators seeking a stand-alone ransomware mitigation and detection prototype.

### 3. [RansomWatch](https://github.com/RafWu/RansomWatch) [![GitHub stars](https://img.shields.io/github/stars/RafWu/RansomWatch?style=social&color=white)](https://github.com/RafWu/RansomWatch/stargazers)
- **GitHub:** [RafWu/RansomWatch](https://github.com/RafWu/RansomWatch)
- **Stack:** C / C++ / Windows Kernel Minifilter Driver | **License:** MIT
- **Capabilities:** An advanced Windows kernel-mode Minifilter filesystem driver designed specifically for real-time ransomware behavioral interception. It monitors `IRP_MJ_CREATE` and `IRP_MJ_WRITE` requests, evaluates write-frequency thresholds and entropy metrics directly at the file system level, and blocks suspicious processes before they can encrypt disk sectors.
- **Best for:** Security engineers and researchers seeking kernel-level Windows filesystem protection against rapid cryptographic modification.

### 4. [ebpfangel](https://github.com/TomasPhilippart/ebpfangel) [![GitHub stars](https://img.shields.io/github/stars/TomasPhilippart/ebpfangel?style=social&color=white)](https://github.com/TomasPhilippart/ebpfangel/stargazers)
- **GitHub:** [TomasPhilippart/ebpfangel](https://github.com/TomasPhilippart/ebpfangel)
- **Stack:** C / Go / Linux eBPF / Machine Learning | **License:** GPL-3.0
- **Capabilities:** Real-time Linux ransomware detection powered by eBPF probe tracing and machine learning inference. Monitors Linux system calls (`sys_enter_write`, `sys_enter_openat`, `sys_enter_unlink`) in kernel space with virtually zero latency, feeding file write velocity and entropy characteristics into an ML scoring engine to detect encryption in progress.
- **Best for:** Linux production environments, Kubernetes worker nodes, and container hosts needing lightweight, kernel-native behavioral monitoring.

### 5. [Ransomware-Json-Dataset](https://github.com/codingo/Ransomware-Json-Dataset) [![GitHub stars](https://img.shields.io/github/stars/codingo/Ransomware-Json-Dataset?style=social&color=white)](https://github.com/codingo/Ransomware-Json-Dataset/stargazers)
- **GitHub:** [codingo/Ransomware-Json-Dataset](https://github.com/codingo/Ransomware-Json-Dataset)
- **Stack:** JSON / Python | **License:** MIT
- **Capabilities:** A comprehensive machine-readable dataset compiling metadata, behavioral properties, known file extensions, ransom note filenames, and mitigation indicators for over 1,000+ ransomware variants. Directly powers automated threat detection pipelines and incident response triage tools.
- **Best for:** SOC engineers and threat detection researchers building automated YARA/SIEM rules or training behavioral ML classifiers.

### 6. [Prometheus-Decryptor](https://github.com/cycraft-corp/Prometheus-Decryptor) [![GitHub stars](https://img.shields.io/github/stars/cycraft-corp/Prometheus-Decryptor?style=social&color=white)](https://github.com/cycraft-corp/Prometheus-Decryptor/stargazers)
- **GitHub:** [cycraft-corp/Prometheus-Decryptor](https://github.com/cycraft-corp/Prometheus-Decryptor)
- **Stack:** Python / Cryptography | **License:** MIT
- **Capabilities:** A forensic clean-recovery tool developed by CyCraft to decrypt files encrypted by the Prometheus ransomware family (a Thanos ransomware variant). Recovers original filenames and unencrypts customer data without paying ransom demands.
- **Best for:** Incident response teams recovering systems encrypted by Prometheus ransomware variants.

### 7. [talus-process-monitor](https://github.com/Hartwell-Labs/talus-process-monitor) [![GitHub stars](https://img.shields.io/github/stars/Hartwell-Labs/talus-process-monitor?style=social&color=white)](https://github.com/Hartwell-Labs/talus-process-monitor)
- **GitHub:** [Hartwell-Labs/talus-process-monitor](https://github.com/Hartwell-Labs/talus-process-monitor)
- **Stack:** Rust / Linux eBPF | **License:** MIT
- **Capabilities:** A self-contained, single static-binary eBPF ransomware detection and response agent for Linux. Requires no external kernel modules; performs behavioral scoring directly on filesystem system calls and provides automated process pausing (`SIGSTOP`) and process termination (`SIGKILL`) when encryption bursts occur.
- **Best for:** DevOps and Linux server administrators needing an easily deployable, standalone binary for Linux server ransomware protection.

### 8. [Warden](https://github.com/Spellskite-coding/Warden) [![GitHub stars](https://img.shields.io/github/stars/Spellskite-coding/Warden?style=social&color=white)](https://github.com/Spellskite-coding/Warden/stargazers)
- **GitHub:** [Spellskite-coding/Warden](https://github.com/Spellskite-coding/Warden)
- **Stack:** Rust / Linux (fanotify / GTK4) | **License:** GPL-3.0
- **Capabilities:** An open-source EDR built for Linux workstations. Features fanotify filesystem monitoring, YARA rule scanning, and multi-tier ransomware detection tracking per-PID, per-directory, and global event burst counters. Isolates ransomware processes with setuid-stripping quarantine and includes a GTK4 live dashboard.
- **Best for:** Linux desktop users and engineers requiring a transparent, workstation-focused anti-ransomware EDR with local GUI control.

### 9. [RansomShield](https://github.com/Spellskite-coding/RansomShield) [![GitHub stars](https://img.shields.io/github/stars/Spellskite-coding/RansomShield?style=social&color=white)](https://github.com/Spellskite-coding/RansomShield/stargazers)
- **GitHub:** [Spellskite-coding/RansomShield](https://github.com/Spellskite-coding/RansomShield)
- **Stack:** Rust / Linux (fanotify) | **License:** GPL-3.0
- **Capabilities:** High-performance Linux security daemon combining Shannon entropy calculation, burst-rate file event detection, and honeypot canary files. Stops active encryption within 8 files, automatically isolating rogue PIDs and storing recoverable copies in an isolated quarantine directory.
- **Best for:** Linux server administrators wanting a production-tested, low-overhead daemon (~2 MB RSS) that protects directories and preserves unaffected files.

### 10. [honeyfile](https://github.com/dispersal-wolves/honeyfile) [![GitHub stars](https://img.shields.io/github/stars/dispersal-wolves/honeyfile?style=social&color=white)](https://github.com/dispersal-wolves/honeyfile/stargazers)
- **GitHub:** [dispersal-wolves/honeyfile](https://github.com/dispersal-wolves/honeyfile)
- **Stack:** Python / Linux (inotify) | **License:** MIT
- **Capabilities:** Plants decoy tripwire files (`passwords.txt`, `backup.sql`, `payroll.xlsx`, `.env`) in critical directories and monitors them for modification, deletion, or unauthorized reading via inotify. Emits real-time webhook and executable trigger alerts at the very first moment an intruder or ransomware touches a decoy.
- **Best for:** System administrators wanting an ultra-lightweight, zero-false-positive early-warning tripwire without deploying complex agent software.

### 11. [endpoint-security-ai-agent](https://github.com/MuthoniGathiithi/endpoint-security-ai-agent) [![GitHub stars](https://img.shields.io/github/stars/MuthoniGathiithi/endpoint-security-ai-agent?style=social&color=white)](https://github.com/MuthoniGathiithi/endpoint-security-ai-agent/stargazers)
- **GitHub:** [MuthoniGathiithi/endpoint-security-ai-agent](https://github.com/MuthoniGathiithi/endpoint-security-ai-agent)
- **Stack:** Python / FastAPI / Next.js / Docker | **License:** MIT
- **Capabilities:** An end-to-end AI EDR platform that detects ransomware, Cobalt Strike beacons, and living-off-the-land attacks in real time. Combines ML file-entropy scoring, osquery telemetry, automated host isolation, and an interactive ChatGPT-style natural-language analyst interface with a Next.js web dashboard.
- **Best for:** Security teams looking for an open-source EDR platform with modern web dashboards and conversational AI threat investigation.

### 12. [VaultSentry](https://github.com/Egyan07/VaultSentry) [![GitHub stars](https://img.shields.io/github/stars/Egyan07/VaultSentry?style=social&color=white)](https://github.com/Egyan07/VaultSentry/stargazers)
- **GitHub:** [Egyan07/VaultSentry](https://github.com/Egyan07/VaultSentry)
- **Stack:** Python / SQLite / GUI | **License:** MIT
- **Capabilities:** Backup file integrity watchdog that computes nightly SHA-256 hashes of critical backup files to detect silent corruption, tampering, ransomware encryption, or unexpected file size drops. Features multi-snapshot diffing, one-click restore capabilities, and automated email summary digests.
- **Best for:** Verifying the integrity of local and NAS backup repositories against stealthy ransomware encryption.

### 13. [sentinel-watch](https://github.com/HahaAhhDev/sentinel) [![GitHub stars](https://img.shields.io/github/stars/HahaAhhDev/sentinel?style=social&color=white)](https://github.com/HahaAhhDev/sentinel/stargazers)
- **GitHub:** [HahaAhhDev/sentinel](https://github.com/HahaAhhDev/sentinel)
- **Stack:** Python (PyPI `sentinel-watch`) | **License:** MIT
- **Capabilities:** A folder watchdog utility combining burst rate detection, Shannon entropy calculations on the first 1 MB of altered files, canary file traps, and suspicious extension filtering (`.locked`, `.crypto`, `READ_ME.txt`). Automatically backs up pristine copies to a protected local vault before encryption can compromise them.
- **Best for:** Lightweight workstation folder monitoring and developer environments.

### 14. [RansomTriage](https://github.com/redhat1032/ransomware-triage) [![GitHub stars](https://img.shields.io/github/stars/redhat1032/ransomware-triage?style=social&color=white)](https://github.com/redhat1032/ransomware-triage/stargazers)
- **GitHub:** [redhat1032/ransomware-triage](https://github.com/redhat1032/ransomware-triage)
- **Stack:** Python (PyPI `ransomtriage`) | **License:** MIT
- **Capabilities:** An offline, privacy-first first-hour incident response triage tool. Matches ransom note signatures against 27+ known families (LockBit, Akira, BlackCat, Phobos, Dharma, WannaCry, STOP/Djvu), verifies cryptocurrency address checksums, checks for free decryptor availability, and generates a CISA/NIST-aligned incident response checklist.
- **Best for:** Incident responders and blue teams needing fast offline ransomware attribution and decryptor discovery without exfiltrating confidential forensic notes.

---

## 📊 Comparison at a Glance

| Solution | Deployment Type | Primary Detection Strategy | Automated Defense Action | Recovery & Rollback Mechanism | Target Environment |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **CrowdStrike Falcon** | Enterprise SaaS / Agent | Behavioral AI + Threat Intel | Process Kill + Host Network Isolation | Backup / RTR Remediation | Windows, macOS, Linux, Cloud Workloads |
| **Rubrik Security Cloud** | SaaS + Appliance Hybrid | Backup Anomaly & Entropy Analysis | Snapshot Quarantine | Immutable Air-Gapped Clean Restore | Enterprise Virtualization, Cloud, M365 |
| **Veeam Data Platform** | Hybrid SaaS / Self-Hosted | Inline I/O Entropy + Malware Scans | Automated Alert & Quarantine | Instant VM Recovery + Orchestrated Rollback | Hyper-V, VMware, Physical & Cloud Workloads |
| **SentinelOne Singularity** | Enterprise SaaS / Agent | Kernel Behavioral AI Engine | Process Termination & Network Quarantine | 1-Click Automated VSS Rollback | Multi-OS Enterprise Endpoints & Servers |
| **Sophos Intercept X** | Enterprise SaaS / Agent | CryptoGuard Deep Learning Detection | Kill Encryption Thread + Isolate | Automatic File Cache Rollback | Windows & macOS Endpoints & Servers |
| **Druva Cyber Resilience** | 100% Cloud SaaS | Unusual Entropy & Modification Spikes | Remote Lock & Wipe | Multi-Cloud Immutable Snapshot Recovery | SaaS Apps, Endpoints, Hybrid Cloud Workloads |
| **Raccine** | Open-Source Tool | IFEO Preemptive Process Interception | Kills process tree invoking VSS deletion | Preserves existing Windows Volume Shadow Copies | Windows Desktops & Servers |
| **Decryptonite** | Open-Source Tool | Behavioral Thresholds & Renames | Process Termination | Quarantine File Restore | Windows & Linux Systems |
| **RansomWatch** | Open-Source Driver | Minifilter Driver I/O Inspection | Blocks File System `IRP_MJ_WRITE` | Native Filesystem Write Prevention | Windows Desktops & Servers |
| **ebpfangel** | Open-Source Daemon | eBPF System Call Tracing + ML | Process Termination / Alert | Telemetry-Guided Restoration | Linux Kernels & Container Nodes |
| **Ransomware-Json-Dataset** | Open-Source Data | Signature & Metadata Taxonomy | Threat Feed Integration | Reference for Decryptor Matching | SIEM, EDR & Research Platforms |
| **Prometheus-Decryptor** | Open-Source Tool | Cryptographic Keystream Exploitation | Post-Incident Execution | Decrypts Prometheus/Thanos-encrypted files | Compromised Windows Systems |
| **talus-process-monitor** | Open-Source Daemon | Static eBPF Behavioral Scoring | Process `SIGSTOP` / `SIGKILL` | Blocks Further Encryption In-Flight | Linux Servers & Containers |
| **Warden** | Open-Source EDR | fanotify + YARA + Event Burst | Process Termination & File Quarantine | Setuid-stripped Quarantine Restore | Linux Workstations |
| **RansomShield** | Open-Source Daemon | Entropy Scoring + fanotify Burst + Canaries | Kills Rogue PID within 8 files | Restores Affected Files from Quarantine | Linux Servers |
| **honeyfile** | Open-Source Script | inotify Canary Trap Modification | Webhook Alert / Custom Script Execution | Early Warning (Pre-encryption) | Linux Servers & NAS Shares |
| **endpoint-security-ai-agent** | Open-Source EDR | ML Entropy Scoring + osquery Telemetry | Process Kill & Host Network Isolation | Quarantine Vault Restoration | Cross-Platform Workstations & Servers |
| **VaultSentry** | Open-Source Watchdog | Daily SHA-256 Checksum Diffing | Tamper Alert & Digest Notification | 1-Click Clean Snapshot Restoration | Backup Storage Repositories & Local Folders |
| **sentinel-watch** | Open-Source Tool | Shannon Entropy + Canary File + Extensions | Process Termination | Clean Local Directory Vault | Local Files & Workstation Directories |
| **RansomTriage** | Open-Source CLI | Ransom Note Regex Pattern Matching | Generates CISA/NIST Incident Plan | Matches Known Free Decryptors | Incident Response Forensics |

---

## 🤝 Contributing

Contributions are welcome! If you know of an open-source Ransomware Detection or Clean Recovery tool that should be listed here, please open a pull request with:

- Project name and GitHub repository URL
- Brief description (1–2 sentences)
- Technology stack and license
- Why it stands out in detection or recovery capabilities

Please ensure the project is actively maintained, genuinely open-source, and includes meaningful detection or clean-recovery features.

---

## 📄 License

This repository is licensed under the [Creative Commons Zero v1.0 Universal](LICENSE) (CC0 1.0) Public Domain Dedication.

---

⭐ **If this curated list helps you safeguard your infrastructure, please star the repository!** ⭐
