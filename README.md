# 🌪️ LFI Tornado — Pro Burp Suite Extension (v5.5.0)

[![Release](https://img.shields.io/badge/Release-v5.5.0-blue.svg?style=for-the-badge&logo=github)](https://github.com/XploitAsh/lfi-tornado/releases)
[![Burp Suite](https://img.shields.io/badge/Burp%20Suite-Community%20%7C%20Professional-orange?style=for-the-badge&logo=portswigger)](https://portswigger.net/burp)
[![Java](https://img.shields.io/badge/Java-8%20or%20higher-red?style=for-the-badge&logo=openjdk)](https://www.java.com)
[![License](https://img.shields.io/badge/License-Educational%20%2F%20Pentest-green?style=for-the-badge)](LICENSE)
[![Platform](https://img.shields.io/badge/Platform-Windows%20%7C%20Linux%20%7C%20macOS-lightgrey?style=for-the-badge)](https://github.com)

> **LFI Tornado** is a high-performance, automated Local File Inclusion (LFI) and Path Traversal vulnerability scanner designed specifically for **Burp Suite (Community & Professional)**. Created for cybersecurity students, ethical hackers, and penetration testers to automate target crawling, parameter discovery, intelligent payload fuzzing, and vulnerability triaging with zero friction.

---

## ⚡ Direct Download

Download the compiled, standalone JAR file ready to load into Burp Suite:

👉 **[📥 Download LFI-Tornado-5.5.0.jar (Latest Release)](https://github.com/XploitAsh/lfi-tornado/releases/download/v5.5.0/LFI-Tornado-5.5.0.jar)**

*(No compilation or Gradle installation required! Works directly out of the box).*

---

## 📑 Table of Contents

- [Features](#-features)
- [Why LFI Tornado?](#-why-lfi-tornado)
- [Installation Guide](#-installation-guide)
- [Quick Start Guide for Students](#-quick-start-guide-for-students)
- [Severity & Detection Categories](#-severity--detection-categories)
- [System Requirements](#-system-requirements)
- [Disclaimer & Ethical Notice](#-disclaimer--ethical-notice)
- [Author & Credits](#-author--credits)

---

## ✨ Features

- 🕷️ **Intelligent Spider & Crawler**:
  - Automatically crawls targets and extracts endpoints with injectable parameters.
  - **Form Suppression Engine**: Automatically suppresses/dismisses modal dialogs (e.g., "Submit Form", "Clear Queues") so your scans run completely unattended.
  - **Native Spider Control**: Safe pause and cancellation of Burp's native spidering jobs at any time.

- 🎯 **Smart Parameter Extraction**:
  - Targets high-risk parameter names (e.g., `file`, `page`, `path`, `doc`, `view`, `include`, `template`, etc.).
  - Deduplicates endpoints automatically to avoid scanning the same endpoint repeatedly.

- ⚡ **High-Speed Fuzzing Engine**:
  - Multi-threaded testing of custom path traversal payloads, null bytes (`%00`), PHP wrappers (`php://filter`, `php://input`), and OS-specific files (`/etc/passwd`, `C:\boot.ini`, `win.ini`).
  - Customizable request delay and concurrency to prevent target rate-limiting or WAF bans.

- 🚨 **Flagged & Triaging Dashboard**:
  - **Dynamic Table Sorting**: Sort logs and flagged findings by *Status Code, Response Length, Severity, Timestamp, or HTTP Method*.
  - **One-Click Quick Filters**: Instantly filter findings by:
    - 🚨 `RCE Potential`
    - ⚠️ `Confirmed LFI`
    - 📄 `Source Disclosure`
    - ℹ️ `Warnings`
    - 🔍 `Anomalies`
  - Integrated HTTP Request/Response viewer for instant manual verification.

- 📊 **Export Reports**:
  - Export full scan logs and verified vulnerabilities to `.csv` format for documentation and client reporting.

---

## 💡 Why LFI Tornado?

In real-world penetration testing and bug bounty engagements, manual LFI testing across hundreds of parameters takes hours:
1. Manually sending each URL to Burp Intruder.
2. Configuring payload injection positions.
3. Loading LFI wordlists.
4. Manually grepping for system file signatures (`root:x:0:0:`, `[fonts]`, `PD9waHA=`, etc.).

**LFI Tornado automates this entire lifecycle** with a single click — finding, injecting, detecting, and categorizing results while you focus on deeper security analysis.

---

## 🔧 Installation Guide

### For Modern Burp Suite (2023.x / 2024.x / 2025.x):

1. Download **`LFI-Tornado-5.5.0.jar`**.
2. Open **Burp Suite**.
3. Navigate to the **Extensions** tab ➡️ **Installed** sub-tab.
4. Click the **Add** button.
5. In the *Load Burp Extension* popup:
   - **Extension type**: Select `Java`.
   - **Extension file**: Click *Select file...* and choose `LFI-Tornado-5.5.0.jar`.
6. Click **Next**.
7. You should see `LFI Tornado v5.5.0 loaded successfully` in the Output tab. A new top-level tab named **🌪️ LFI Tornado** will now appear!

### For Burp Suite 1.7.x (Legacy):
1. Navigate to **Extender** ➡️ **Extensions**.
2. Click **Add** ➡️ Type: `Java` ➡️ Select `LFI-Tornado-5.5.0.jar` ➡️ Click **Next**.

---

## 🚀 Quick Start Guide (For Students)

### Step 1: Add Target
- Navigate to the **🌪️ LFI Tornado** ➡️ **🎯 Target** tab.
- Enter your authorized target URL (e.g., `http://testphp.vulnweb.com/`).
- Alternatively, right-click any request in Burp's **Proxy** or **Site map** and select:
  > **Send to LFI Tornado**

### Step 2: Spider Target
- Click **Spider Target**.
- LFI Tornado will automatically crawl the website and populate the **Parameters** list.
- If you wish to stop crawling early, simply click **Stop Spider**.

### Step 3: Start Testing
- Check the **Dictionary** tab to review or customize your payloads (standard traversal lists are pre-configured).
- Go to the **Targets** tab and click **Start Run**.
- Monitor live HTTP traffic in the **📜 Request Log** tab.

### Step 4: Analyze Findings
- Switch to the **🚩 Flagged** tab.
- Use the **Quick Filter Checkboxes** at the top:
  - Check **🚨 RCE Potential** to see if `/proc/self/environ` or log injection vectors were discovered.
  - Check **⚠️ Confirmed LFI** to view verified system file reads (e.g., `/etc/passwd`).
- Click on any row to inspect the full HTTP Request and Response directly in Burp.

---

## 🛡️ Severity & Detection Categories

| Badge / Severity | Description | Action Required |
| :--- | :--- | :--- |
| 🚨 **CRITICAL (RCE Potential)** | Matched environment variables or log files (`/proc/self/environ`, auth logs). | Check for log poisoning or command injection possibilities. |
| ⚠️ **HIGH (Confirmed LFI)** | Matched definite OS file signatures (`root:x:0:0:`, `[boot loader]`, `daemon:`). | Confirmed Local File Inclusion. Document for report! |
| 📄 **MEDIUM (Source Disclosure)** | Disclosed base64 encoded PHP source code (`PD9waH`, `php://filter`). | Decode base64 to inspect backend application source code. |
| ℹ️ **LOW (Warning / Signature Match)** | Matched partial path or configuration clues. | Verify manually in Burp Repeater. |
| 🔍 **ANOMALY (Differential)** | Significant response length difference detected. | Server behavior changed; possible blind LFI. |

---

## 💻 System Requirements

- **Burp Suite**: Community Edition or Professional Edition (v1.7.x - 2025.x+)
- **Java Runtime**: JRE / JDK 8 or higher (Burp Suite's bundled Java works automatically)
- **Supported OS**: Windows, Kali Linux, Ubuntu, macOS

---

## ⚠️ Disclaimer & Ethical Notice

> [!CAUTION]
> **For Educational and Authorized Security Testing Only.**
> This tool is developed strictly for authorized penetration testing, vulnerability assessments, security research, and educational training. Testing targets without prior mutual written consent is illegal under cyber law (e.g., CFAA, Bangladesh Cyber Security Act, and international computer misuse laws). The developer assumes no liability for misuse or damage caused by this program.

---

## 👨‍💻 Author & Credits

- **Developer**: **MD Asif Islam** ([@XploitAsh](https://github.com/XploitAsh))
- **Organization**: **Arena Web Security**
- **Community & Support**: Feel free to submit issues or feature requests via GitHub Issues!

⭐ **If you find this tool helpful, please give this repository a Star!**
