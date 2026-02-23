# PC Diagnostic Report
**Date:** 2026-02-21
**Machine:** Watchtower-HQ

---

## System Specifications

| Component | Details |
|-----------|---------|
| **CPU** | AMD Ryzen 5 5600X 6-Core, 3701 MHz, 6 Cores / 12 Logical Processors |
| **GPU** | NVIDIA GeForce RTX 3060 (ASUS ROG STRIX RTX 3060 V2 LHR) |
| **RAM** | 32GB |
| **Storage** | 2x Corsair Force MP600 NVMe M.2 SSD (1TB each) |
| **Motherboard** | ASUS ROG Strix B550-F Gaming (Wi-Fi) |
| **OS** | Windows 11 25H2 |

---

## Diagnostic Results

### ✅ Storage Health
| Drive | Health | Temperature | Power On Hours | Firmware |
|-------|--------|-------------|----------------|----------|
| C: (Boot) | Good — 92% | 38°C | 28,977 hrs (~3.3 years) | EGFM13.0 |
| D: (Storage) | Good — 99% | 36°C | 28,268 hrs | EGFM13.0 |

**Notes:**
- C: drive health slightly degraded due to being the primary boot drive — monitor periodically
- Both drives running healthy temperatures (under 50°C is ideal)
- Firmware confirmed current on both drives
- Tools used: CrystalDiskInfo, Corsair SSD Toolbox

---

### ✅ Memory
- **Windows Memory Diagnostic:** Passed — no issues found
- **MemTest86:** Pending — scheduled to run tonight for deep validation
- Tool: Windows Memory Diagnostic (built-in), MemTest86 (bootable USB prepared)

---

### ✅ CPU Thermals & Performance
| Metric | Value | Notes |
|--------|-------|-------|
| Idle Temp (Tctl/Tdie) | ~45°C avg | Healthy |
| Idle Temp (CCD1 Tdie) | High 40s°C | Healthy |
| Load Temp Peak | 80.4°C (Tctl) / 81.2°C (CCD1) | Acceptable, near stock cooler limit |
| Cinebench R23 (Balanced plan) | 8,494 | Below expected range |
| Cinebench R23 (High Performance) | 9,929 | Improved, still slightly below potential |
| Expected R23 Range | 11,000–12,000 | Gap due to thermal throttling |

**Notes:**
- Power plan changed from **Balanced** to **High Performance** — significant performance improvement
- Stock Wraith Stealth cooler working near its thermal limits under sustained load
- Thermal paste replacement and case cleaning will recover additional performance
- Aftermarket cooler recommended for closing remaining performance gap (e.g. DeepCool AK400, be quiet! Pure Rock 2)
- Tool used: HWiNFO64, Cinebench R23

---

### ✅ GPU Thermals & Performance
| Metric | Value | Notes |
|--------|-------|-------|
| Idle Temp | 41°C | Excellent |
| Idle Hot Spot | 51.4°C | Normal |
| Load Temp Peak | 66.4°C | Excellent — well under 83°C thermal limit |
| Load Hot Spot Peak | 86°C | Normal (under 95°C limit) |
| GPU Clock (load) | 1,957 MHz | Expected |
| GPU Power (load) | ~170W | At rated TDP |
| PCIe Link Speed | 16.0 GT/s (PCIe 4.0 x16) | Full bandwidth confirmed |
| 3DMark Time Spy — Graphics Score | 8,746 | Within expected range ✅ |
| 3DMark Time Spy — CPU Score | 7,199 | Low due to CPU thermal throttling |
| 3DMark Time Spy — Overall Score | 8,481 | Dragged down by CPU score |
| Performance Limiter | Power | Normal behavior for RTX 3060 at stock settings |

**Notes:**
- GPU itself is healthy and performing within expected range
- Lower overall Time Spy score is attributed to CPU bottleneck, not GPU issue
- Tool used: HWiNFO64, 3DMark Time Spy

---

### ✅ Windows System Health
- **SFC (System File Checker):** No integrity violations found
- **DISM /RestoreHealth:** Completed successfully — Windows component store healthy
- Both scans confirm clean Windows installation

---

## Software & Driver Updates

### BIOS
| Item | Before | After |
|------|--------|-------|
| BIOS Version | 2423 (08/10/2021) | 3634 (09/22/2025) |

**Notable improvements in 3634:**
- Critical fTPM firmware upgrade
- AGESA version updated to ComboV2 PI 1.2.0.E
- Security updates
- Improved game compatibility

> ⚠️ **BitLocker Recovery Key stored** — required during BIOS update due to fTPM changes

---

### Drivers Updated
| Driver | Previous Version | Updated Version | Method |
|--------|-----------------|-----------------|--------|
| NVIDIA GPU | Previous | Latest | DDU clean reinstall |
| Intel Wi-Fi 6 AX200 | — | 24.20.0.3 | Intel Driver & Support Assistant |
| Intel Bluetooth AX200 | 23.90.0.8 | 24.20.0.3 | Windows Update (Optional Updates) |
| AMD Chipset | Previous | Latest | AMD support site |
| Corsair MP600 Firmware | EGFM13.0 | EGFM13.0 | Already current |
| Intel I225-V Ethernet | — | 2.1.3.15 | Manual (one minor revision behind 2.1.5.7) |

**Notes:**
- Bluetooth driver required extensive troubleshooting due to driver store accumulation (17 duplicate entries found and cleaned)
- Ethernet driver (2.1.3.15) is one minor revision behind latest (2.1.5.7) — functional and acceptable
- Intel Driver & Support Assistant does not reliably detect the I225-V ethernet adapter

---

### Windows Updates Applied
- 2026-02 Security Update KB5077181 (Build 26100.7840)
- 2025-10 Cumulative Update for .NET Framework 3.5 and 4.8.1 (KB5066131)
- Windows 11 version 25H2 feature update

---

## Security Configuration

### Windows Security Status
| Feature | Status |
|---------|--------|
| Virus & Threat Protection | ✅ On |
| Firewall & Network Protection | ✅ On (all profiles) |
| App & Browser Control | ✅ On |
| Secure Boot | ✅ On |
| Memory Integrity | ✅ Enabled (enabled during diagnostic) |
| Kernel-mode Hardware-enforced Stack Protection | ✅ Enabled (enabled during diagnostic) |
| Virtualization-based Security | ✅ Enabled (SVM Mode enabled in BIOS) |

**Notes:**
- SVM Mode was disabled in BIOS — enabled during diagnostic session to support Memory Integrity
- Memory Integrity and Kernel-mode Stack Protection were both off prior to this session

---

## Known Issues & Items to Monitor

### 🔄 Intermittent Black Screen on Complex Reboots
- **Symptom:** During complex reboots (Advanced Startup, DDU restarts, etc.) screens remain black while PC stays powered
- **Suspected cause:** GPU driver failing to reinitialize displays properly during non-standard restart sequences
- **Frequency:** Intermittent — does not occur on normal everyday restarts
- **Recovery shortcut:** `Windows + Ctrl + Shift + B` — resets graphics driver without rebooting
- **Status:** Monitoring — not severe enough to require immediate action

### 🔄 CPU Thermal Throttling Under Sustained Load
- **Symptom:** Cinebench R23 score below expected range (9,929 vs 11,000–12,000)
- **Cause:** Stock Wraith Stealth cooler reaching thermal limits under 100% CPU load
- **Fix:** Fresh thermal paste + case cleaning (short term), aftermarket cooler (long term)
- **Status:** Planned maintenance

### 🔄 C: Drive Health at 92%
- **Status:** Good — not concerning currently
- **Action:** Monitor periodically with CrystalDiskInfo
- **Note:** Expected degradation for a primary boot drive with ~3.3 years of runtime

### ⏳ MemTest86 Deep RAM Validation
- **Status:** Pending — bootable USB prepared, scheduled to run tonight
- **Instructions:** Boot from USB using F8 boot menu, let run overnight for full validation

---

## Recommended Maintenance

| Task | Priority | Notes |
|------|----------|-------|
| Run MemTest86 overnight | High | USB prepared and ready |
| Case cleaning | Medium | Dust buildup affecting thermals |
| Thermal paste replacement (CPU) | Medium | Will improve load temps and performance |
| Aftermarket CPU cooler | Low | Optional upgrade — DeepCool AK400 or be quiet! Pure Rock 2 recommended |
| Update Intel I225-V ethernet to 2.1.5.7 | Low | Minor revision, not urgent |
| Monitor C: drive health | Ongoing | Check with CrystalDiskInfo periodically |

---

## Tools Used

| Tool | Purpose |
|------|---------|
| CrystalDiskInfo | Drive S.M.A.R.T. health monitoring |
| Corsair SSD Toolbox | MP600 firmware verification |
| HWiNFO64 | Temperature and sensor monitoring |
| Cinebench R23 | CPU performance benchmark |
| 3DMark Time Spy | GPU performance benchmark |
| MemTest86 | Deep RAM validation (pending) |
| DDU (Display Driver Uninstaller) | Clean GPU driver removal |
| Intel Driver & Support Assistant | Driver detection and update |
| Windows Memory Diagnostic | Basic RAM check |
| SFC (sfc /scannow) | Windows system file integrity |
| DISM /RestoreHealth | Windows component store repair |
| ASUS EZ Flash 3 | BIOS update utility |
| Event Viewer | System error and warning log review |

---

## BIOS Access Reference

| Action | Key |
|--------|-----|
| Enter BIOS | DEL |
| Boot Menu | F8 |

---

## Key File & System Paths Referenced

- Driver Store: `C:\Windows\System32\DriverStore\FileRepository\`
- Bluetooth driver (current): `ibtusb.inf_amd64_32a4be4c5148d1c2` (v24.20.0.3)
- Intel Ethernet hardware ID: `USB\VID_8087&PID_0029`

---

*Report generated following full diagnostic session on 2026-02-21*
