# Firmware Persistence Techniques

**Advanced UEFI &amp; Embedded Persistence Analysis**

**Author:** Maciej Gojny — GG Advanced IT Security ([ggsec.de](https://ggsec.de))
**Version:** 1.2
**Date:** July 2026
**Classification:** TLP:WHITE — Public Release

---

## 📄 Overview

This whitepaper provides a technical overview of firmware-based persistence techniques observed in modern cyber operations targeting UEFI firmware, embedded systems, storage controllers, and boot environments.

Unlike traditional OS persistence, firmware-level mechanisms may survive:

- Operating system reinstallation
- Disk formatting and replacement
- Conventional EDR/AV remediation

The document is written for defensive security practitioners, firmware auditors, and enterprise security architects. Offensive implementation detail is deliberately omitted.

---

## 🆕 What's new in 1.2

| Section | Change |
|---------|--------|
| **§4.1** | New — **bootkit vs. firmware implant**: side-by-side comparison of ESP-resident and SPI-resident persistence, including the "survives disk replacement" distinction that determines remediation cost |
| **§3.5** | Expanded — OEM persistence modules as a distinct threat class, with structural detection guidance |
| **§9** | New — **the 2026 Secure Boot trust anchor transition** and the revocation-freeze failure mode |
| **§5.2** | Updated — tooling table now leads with `ggfw`, GGSEC's firmware analysis toolkit |
| **§5.5** | New — SPI acquisition caveat: a host-side dump may return a blank ME region under descriptor denial |
| **§8** | Timeline extended through 2025 (Gigabyte App Center, PKfail, HybridPetya) |
| **§11** | New — methodology and limitations |
| Throughout | CVE references verified against primary vendor and researcher sources |

---

## 🎯 Key Topics

| Category | Techniques covered |
|----------|--------------------|
| **Persistence** | WPBT abuse, NVRAM/UEFI variables, SPI flash modification, storage controller firmware (HPA/DCO) |
| **Bootkits** | BlackLotus (**CVE-2022-21894 "Baton Drop"**), ESPecter, Bootkitty |
| **Firmware implants** | LoJax (APT28), MosaicRegressor, MoonBounce (APT41, `CORE_DXE`), CosmicStrand |
| **OEM persistence modules** | Absolute Computrace/LoJack, Lenovo Service Engine, GIGABYTE App Center, vendor password-recovery paths (ASUS, HP) |
| **Supply chain** | PKfail (CVE-2024-8105), leaked AMI test Platform Keys |
| **Trust anchors** | June 2026 Secure Boot certificate expiry; KEK/DB/DBX lifecycle |
| **Detection** | `ggfw`, CHIPSEC, UEFITool, Binwalk, Ghidra, fwupd/LVFS; Sigma rules; Splunk queries |
| **Mitigations** | Secure Boot, TPM 2.0, Boot Guard / AMD PSP, WDAC, HVCI, SPI write protection, P1–P3 roadmap |

---

## ⚠️ Frequently confused

Two clarifications that recur in public reporting and are addressed explicitly in the paper:

- **BlackLotus exploits CVE-2022-21894 ("Baton Drop")**, a Secure Boot bypass in the Windows Boot Manager. CVE-2023-24932 is a related but separate bypass whose fix required manual opt-in activation. Both matter; they are not the same issue.
- **BlackLotus persists on the EFI System Partition, not in SPI flash.** It is a bootkit, not a firmware implant. ESP wipe plus OS reinstall is sufficient — physical reflash is not required. Reserve reflash for confirmed SPI-resident implants such as LoJax or MoonBounce.

---

## 📁 Repository contents

| Path | Description |
|------|-------------|
| `GGSEC_Firmware_Persistence_v12.pdf` | Full whitepaper (14 pages) |
| `sigma_rule_uefi_esp.yml` | Sigma rule — unsigned `.efi` written to the ESP |
| `splunk_secureboot_tampering.txt` | Splunk query — Secure Boot / BitLocker tampering events |
| `diagrams/` | Boot flow diagrams (SEC → PEI → DXE → BDS → TSL → RT) |
| `src/` | HTML source and build script — the PDF is generated, not hand-edited |

---

## 🚀 Quick start

1. Read the whitepaper, or jump to §10 for the prioritized action list
2. Implement the **P1** controls: Secure Boot + TPM 2.0 + BitLocker, WDAC policy, DBX currency
3. **Inventory KEK certificate vintage across your fleet** — 2011 versus 2023 — ahead of the June 2026 expiry
4. Deploy the Sigma rule via Sysmon for ESP monitoring
5. Run an offline SPI analysis on a representative device sample

---

## 🔧 Building the PDF

The PDF is generated from HTML. Edit the source, rebuild, commit both.

```bash
pip install weasyprint
cd src/
python3 build_pdf.py
```

The build is fully offline — fonts are bundled in `src/fonts/`. No network access required.

---

## 📚 References

ESET Research · Kaspersky GReAT · Microsoft MSRC · NSA · Binarly REsearch · Eclypsium · MITRE ATT&amp;CK · NIST SP 800-193 · UEFI Forum

Full citation list in §12 of the whitepaper.

---

## 🔗 Related

- **UEFI Attack Surface Research** — companion paper covering bootkit architecture, Secure Boot bypass techniques, SMM (Ring -2), DXE driver analysis, and practical firmware artifacts

---

## 📝 License

CC BY-NC 4.0 — GGSEC Research

---

## 👤 Author

**Maciej Gojny** — GGSEC Research
GitHub: [@patapik](https://github.com/patapik) · Web: [ggsec.de](https://ggsec.de)
