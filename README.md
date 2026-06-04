# 🛡️ Phishing Email Analysis Report

## 📌 1. Executive Summary
This report provides a step-by-step technical analysis of a real-world phishing attack. The attacker attempts to scare the victim by impersonating the **Microsoft Account Team**, claiming there was a suspicious login attempt from Russia. 

By analyzing the raw email headers and validating them through **MXToolbox**, we expose the underlying techniques used by the attacker to bypass standard checks, spoof identities, and attempt credential harvesting.



------------------------------------------------------------------------------------------------------------------



## 🏢 2. Attack Overview (At a Glance)

| Component | Attacker's Fake Claim | Actual Technical Reality |
| :--- | :--- | :--- |
| **Sender Name** | Microsoft account team | Unauthorized External Relay |
| **Sender Email** | `no-reply@access-accsecurity.com` | `bounce@nonkfrgr.co.uk` |
| **Source IP** | 103.225.77.255 (Claimed Russia IP) | **89.144.9.87** (Actual Sending Server) |
| **Action Button** | "Report The User" Portal | Direct `mailto:` link to a rogue Gmail account |
| **Email Status** | Critical Security Alert | **Malicious Phishing Attempt** |



--------------------------------------------------------------------------------------------------------------------------



## ⚙️ 3. The Attacker's Blueprint (How the Scam Works)

### 🚨 Step 1: Creating Panic (Social Engineering)
The email uses immediate scare tactics. It tells the user that someone from **Russia/Moscow** just logged into their Windows 10 account. This creates instant panic, forcing the user to act quickly without thinking.

### 🎭 Step 2: Display Name Spoofing
The inbox displays the sender as `Microsoft account team`. However, the domain attached to it is `access-accsecurity.com`. This is a classic **look-alike domain** designed to look official by including the word "security".

### 🪤 Step 3: The "Mailto" Trap (Hidden Payload)
Inside the email body, there is a prominent blue button labeled **"Report The User"**. 
* **The Trick:** Instead of leading to an official Microsoft website, the button's underlying HTML link contains a `mailto:` command: `href="mailto:solutionteamrecognizd02@gmail.com"`.
* **The Impact:** If the victim clicks the button, it automatically opens their local email app to send an email straight to the attacker's personal Gmail inbox. 

### 👁️ Step 4: Invisible Tracking (Spy Pixel)
The attacker embedded a tiny, invisible $1 \times 1$ pixel image at the bottom of the email:
```html
<img alt="" src="[http://thebandalisty.com/track/](http://thebandalisty.com/track/)..." width="1px" height="1px" style="visibility:hidden">
```



-----------------------------------------------------------------------------------------------------------------------------



## ❓ 4. Interview Q&A (Technical Defense)

Here are the conceptual breakdowns required for security engineering entry-level roles based on this task:

#### Q1. What is vulnerability scanning?
**Answer:** Vulnerability scanning is an automated process used to identify, evaluate, and report security weaknesses, misconfigurations, and outdated software versions within an asset, network, or application infrastructure.

#### Q2. What is the difference between vulnerability scanning and penetration testing?
**Answer:** 
* **Vulnerability Scanning:** An automated, non-destructive tool-based approach that searches for known vulnerabilities and catalogs them. It shows *where* the holes are.
* **Penetration Testing:** A manual, active hacking simulation performed by a human specialist to actively exploit those vulnerabilities to see how far an attacker can penetrate into the network.

#### Q3. What are some common vulnerabilities in personal computers?
**Answer:** Unpatched operating systems (missing Windows updates), outdated third-party software (browsers, Adobe Reader, Java runtime), disabled firewalls, weak local account passwords, and insecure default protocols enabled (like SMBv1).

#### Q4. How do scanners detect vulnerabilities?
**Answer:** Scanners use a database of **Plugins** containing signatures of known vulnerabilities (CVEs). They ping open ports, banners, software version headers, and registry values from the target machine, then compare them against their database to find matches.

#### Q5. What is CVSS?
**Answer:** **CVSS (Common Vulnerability Scoring System)** is a standardized, open industry framework used to communicate the characteristics and severity of software vulnerabilities. It rates flaws on a scale from `$0.0$` to `$10.0$`, where `$9.0-10.0$` is deemed Critical.

#### Q6. How often should vulnerability scans be performed?
**Answer:** Ideally, scans should be performed **weekly** or at least **monthly**, as well as immediately after installing new infrastructure, pushing code updates, or when a major zero-day vulnerability is announced globally.

#### Q7. What is a false positive in vulnerability scanning?
**Answer:** A false positive occurs when a security scanner incorrectly flags a clean, safe system configuration or file as a vulnerability or threat. It requires human validation to filter out.

#### Q8. How do you prioritize vulnerabilities?
**Answer:** Prioritization is determined by combining the **CVSS Severity Score** with **Asset Criticality** and **Exploit Availability**. A Medium severity bug on a critical web server facing the internet often takes priority over a High severity bug on an isolated local machine.
