# 🛡️ Week 3: Password Cracking & Hash Extraction Lab

[![Platform](https://img.shields.io/badge/Platform-Windows%20%7C%20Kali%20Linux-blue?style=flat-square&logo=linux)]()
[![Tools](https://img.shields.io/badge/Tools-John%20the%20Ripper%20%7C%20Johnny%20GUI%20%7C%20Networkwalks-red?style=flat-square)]()
[![Focus](https://img.shields.io/badge/Focus-Cryptographic%20Auditing%20%26%20Password%20Security-success?style=flat-square)]()

> **Disclaimer:** *All password cracking exercises and tools documented in this repository were executed strictly on authorized, sample password-protected PDF files (`My Locked PDF1.pdf`) within an isolated educational lab environment for cybersecurity training purposes only.*

---

## 📋 Overview

This repository documents the practical implementation of **Week 3 (Project Modules 1 & 2)** of my Cybersecurity & Ethical Hacking lab coursework. The primary objective of this lab was to understand cryptographic hashing versus encryption, extract password hashes from encrypted PDF documents, and perform dictionary attacks to audit password resilience using both local command-line/GUI utilities and browser-based security tools.

---

## 🛠️ Tools & Environment

* **Host Operating System:** Windows 10/11 (Compatible with Kali Linux)
* **Module 1 Tools (Local Auditing):**
  * **John the Ripper (JTR `1.9.0-jumbo-1`):** Open-source command-line password security auditing and recovery tool.
  * **Johnny GUI (`v2.2`):** Graphical user interface wrapper for John the Ripper.
  * **OnlineHashCrack PDF Hash Extractor (`pdf2john`):** Web utility used to extract compatible `$pdf$` hash strings from protected PDF files.
* **Module 2 Tools (Browser-Based Auditing):**
  * **Networkwalks Hash Calculator:** Local browser-based cryptographic hash generator and PDF hash extractor (`pdf2john`/`hashcat` format).
  * **Networkwalks Password Cracker:** Browser-based dictionary attack simulator utilizing built-in and custom wordlists.

---

## 🚀 Lab Execution & Methodology

### Module 1: Password Cracking with John the Ripper & Johnny GUI

#### 1. Environment Setup & Configuration
1. Downloaded the 64-bit Windows binaries for **John the Ripper (`john-1.9.0-jumbo-1-win64`)** from Openwall and extracted the archive.
2. Installed **Johnny GUI (`johnny_2.2_win.zip`)** on the host machine.
3. Configured Johnny to point to the core JTR executable under **Settings → John the Ripper executable**:
   ```text
   .../john-1.9.0-jumbo-1-win64/run/john.exe
   ```

![Johnny GUI Settings Configuration](screenshots/01-johnny-jtr-path-setup.png)

#### 2. PDF Hash Extraction (`pdf2john`)
1. Uploaded the target sample file (`My Locked PDF1.pdf`) to the `pdf2john` hash extractor.
2. Retrieved the raw cryptographic hash string starting with the `$pdf$` signature:
   ```text
   $pdf$4*4*128*-1060*1*16*55d1a5c14175da449753199e44971d32*32*777fd021a7f3c5ae598c0c6495c7f76e00000000000000000000000000000000*32*ceecdac74b19b5a62688d3b3524e1374c955cbb9cc3c45316494d9446ef81af1
   ```
3. Saved the clean hash string (ensuring no extraneous wrapper characters) into a plain text file named `hash1.txt`.

![PDF Hash Extraction Output](screenshots/02-pdf-hash-extraction.png)

#### 3. Executing the Attack in Johnny
1. Opened Johnny GUI and selected **Open password file → Open password file (PASSWD format)** to load `hash1.txt`.
2. Verified the hash loaded properly with format detected as `PDF`.
3. Clicked **Start new attack** to initiate the cracking session.
4. Recovered the plaintext password (`password1`) at 100% completion and unlocked `My Locked PDF1.pdf` (`networkwalks_flag1.pdf`) to capture the lab flag.

![Johnny Cracked Password Result](screenshots/03-johnny-cracked-result.png)

![Unlocked PDF Flag Verification](screenshots/04-unlocked-pdf-flag.png)

---

### Module 2: Password Cracking with Networkwalks Tools

#### 1. Local Hash Extraction via Networkwalks Hash Calculator
1. Navigated to the **Networkwalks Hash Calculator** (`networkwalks.com/hash-calculator/`).
2. Selected the **PDF** tab and loaded `My Locked PDF1.pdf` (parsed locally in the browser without uploading sensitive files).
3. Extracted the 128-bit Revision R4 / Version V4 `$pdf$` hash string.

![Networkwalks Hash Calculator Extraction](screenshots/05-nw-hash-calculator.png)

#### 2. Dictionary Attack via Networkwalks Password Cracker
1. Opened the **Networkwalks Password Cracker** (`networkwalks.com/password-cracker/`).
2. Pasted the extracted `$pdf$` hash into the input field and selected the built-in wordlist (`100 words`).
3. Clicked **START CRACKING** to execute the dictionary attack, matching and recovering `password1` within seconds.

![Networkwalks Password Cracker Success](screenshots/06-nw-password-cracker.png)

---

## 🔍 Key Takeaways & Security Insights

| Concept / Metric | Lab Observation & Industry Reality |
| :--- | :--- |
| **Encryption vs. Hashing** | **Encryption** is a two-way reversible function requiring a key to decrypt ciphertext back to plaintext. **Hashing** is a one-way mathematical function producing a fixed-length digest—yet weak inputs remain vulnerable to dictionary and rainbow-table lookups. |
| **Password Length & Entropy** | An 8-character password using only lowercase letters can be brute-forced in **minutes**, whereas a strong 12+ character password mixing uppercase, lowercase, numbers, and symbols can take **many years** to crack. |
| **Dictionary Vulnerability** | Predictable passwords such as `123456`, `password`, `qwert123`, and `password1` remain among the most frequently used credentials globally and are cracked almost instantaneously. |
| **Credential Exposure Scale** | Over **24 billion** username and password pairs from historical data breaches circulate on the dark web, fueling automated credential stuffing attacks. |

### Defensive Recommendations
* **Enforce Length & Complexity:** Require a minimum of 12–16 characters with high character-set entropy.
* **Implement Multi-Factor Authentication (MFA):** Ensure compromised passwords alone cannot grant unauthorized access.
* **Adopt Password Managers:** Generate and store unique, random credentials per service to eliminate password reuse.

---

## 📁 Repository Structure

```text
NETWORKWALKS-PENIUS-B084-WK3-PASSWORD-CRACKING/
├── README.md                                  # Lab documentation & methodology
└── screenshots/                               # Visual proof of lab execution
    ├── 01-johnny-jtr-path-setup.png
    ├── 02-pdf-hash-extraction.png
    ├── 03-johnny-cracked-result.png
    ├── 04-unlocked-pdf-flag.png
    ├── 05-nw-hash-calculator.png
    └── 06-nw-password-cracker.png
```

---

## 👤 Author

**Penius Jempa (Jay-P)**  
*B.Sc. Computer Science Student | Cybersecurity & Networking Enthusiast*  
