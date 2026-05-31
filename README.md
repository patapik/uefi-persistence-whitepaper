# Firmware Persistence Techniques
## Advanced UEFI & Embedded Persistence Analysis

**Author:** Maciej Gojny (GG Advanced It Security GGSEC.DE)  
**Version:** 1.1 FINAL  
**Date:** May 2026  
**Classification:** TLP:WHITE – Public Release

---

## 📄 Overview

This whitepaper provides a technical overview of firmware-based persistence techniques observed in modern cyber operations targeting UEFI firmware, embedded systems, storage controllers, and boot environments.

Unlike traditional OS persistence, firmware-level mechanisms survive:
- Operating system reinstallation
- Disk formatting and replacement
- Conventional EDR/AV remediation

---

## 🎯 Key Topics

| Category | Techniques Covered |
|----------|-------------------|
| **Persistence** | WPBT abuse, NVRAM variables, SPI flash modification |
| **Bootkits** | BlackLotus (CVE-2023-24932), LoJax, MoonBounce |
| **OEM backdoors** | ASUS (ALT+R), HP (password generator) |
| **Detection** | Sigma rules, Splunk queries, CHIPSEC, UEFITool |
| **Mitigations** | Secure Boot, TPM, WDAC, HVCI, P1-P3 roadmap |

---

## 📁 Repository Contents

| File | Description |
|------|-------------|
| `GGSEC_Firmware_Persistence_v11.pdf` | Full whitepaper (14 pages) |
| `sigma_rule_uefi_esp.yml` | Sigma rule for unsigned .efi in ESP |
| `splunk_secureboot_tampering.txt` | Splunk query for Secure Boot events |
| `diagrams/` | Mermaid boot flow diagrams (SEC→PEI→DXE→BDS→TSL→RT) |

---

## 🚀 Quick Start

1. Download the PDF
2. Implement P1 mitigations (Section 9)
3. Deploy Sigma rule via Sysmon
4. Run CHIPSEC audit on representative devices

---

## 📚 References

- ESET, Kaspersky GReAT, Huntress, AMI, MITRE ATT&CK, NIST SP 800-193

---

## 📝 License

CC BY-NC 4.0 – GGSEC Research

---

## 🔗 Author

**Maciej Gojny** – GGSEC Research  
GitHub: [@patapik](https://github.com/patapik)
