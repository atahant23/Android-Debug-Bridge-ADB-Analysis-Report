# Android-Debug-Bridge-ADB-Analysis-Report

# 📱 Advanced Android Forensic & ADB System Analysis
> **Institution:** İstinye University  
> **Department:** Information Security Technologies  
> **Analyst:** Atahan  
> **Date:** March 31, 2026

---

## 📑 Project Overview
This project demonstrates a comprehensive security audit of an Android environment using the **Android Debug Bridge (ADB)**. It covers the full lifecycle of a mobile forensic investigation: from establishing a secure bridge and extracting application binaries (APKs) to performing static reverse engineering and dynamic log analysis.

---

## 💻 Environment & Toolset
| Component | Specification |
| :--- | :--- |
| **Analysis Platform** | **Kali Linux 2024.x** (Virtualized via VirtualBox) |
| **Bridge Protocol** | ADB (Android Debug Bridge) v34.x |
| **Reverse Engineering** | **JADX-GUI** (Dex-to-Java Decompiler) |
| **Target Device** | Physical Android Device (Debugging Mode: Enabled) |

---

## 🛠 Technical Methodology

### 1. Forensic Acquisition (Phase I)
The connection was secured by mapping the physical USB port to the Kali environment. RSA fingerprint authorization was completed to establish a trusted link.
```bash
sudo adb start-server
adb devices # Verification of 'device' status
```

2. Application Extraction (Phase II)
The YouTube package (com.google.android.youtube) was targeted for analysis. The physical APK was located via the Package Manager and pulled to the local analysis machine.
```bash
# Locate and extract binary
adb shell pm path com.google.android.youtube
adb pull /product/app/YouTube/YouTube.apk ./assets/youtube_analysis.apk
```
2. Application Extraction (Phase II)
The YouTube package (com.google.android.youtube) was targeted for analysis. The physical APK was located via the Package Manager and pulled to the local analysis machine.
```bash
adb shell screencap -p /sdcard/evidence.png
adb pull /sdcard/evidence.png ./assets/ui_evidence.png
```

🔍 Security Analysis & Findings
A. Static Analysis (JADX Inspection)
After decompiling the APK, the AndroidManifest.xml was audited for privilege escalation risks.

Sensitive Permissions: Identified CAMERA, RECORD_AUDIO, and ACCESS_FINE_LOCATION.

Exported Activities: Multiple activities were found with android:exported="true", marking potential entry points for Intent Injection attacks.

B. Dynamic Analysis (Logcat Monitoring)
Real-time system logs were captured to monitor background data leaks and application behavior.
```bash
# Filtering for system warnings and errors
adb logcat -d *:W > logs/cihaz_log_analizi.txt
```

Findings: No plaintext PII (Personally Identifiable Information) was leaked in the logs during the testing session, indicating secure logging implementation by the developer.
