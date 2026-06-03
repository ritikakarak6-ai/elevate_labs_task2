# 🛡️ Phishing Email Analysis Report

## 📌 1. Executive Summary
This report provides a step-by-step technical analysis of a real-world phishing attack. The attacker attempts to scare the victim by impersonating the **Microsoft Account Team**, claiming there was a suspicious login attempt from Russia. 

By analyzing the raw email headers and validating them through **MXToolbox**, we expose the underlying techniques used by the attacker to bypass standard checks, spoof identities, and attempt credential harvesting.

---

## 🏢 2. Attack Overview (At a Glance)

| Component | Attacker's Fake Claim | Actual Technical Reality |
| :--- | :--- | :--- |
| **Sender Name** | Microsoft account team | Unauthorized External Relay |
| **Sender Email** | `no-reply@access-accsecurity.com` | `bounce@nonkfrgr.co.uk` |
| **Source IP** | 103.225.77.255 (Claimed Russia IP) | **89.144.9.87** (Actual Sending Server) |
| **Action Button** | "Report The User" Portal | Direct `mailto:` link to a rogue Gmail account |
| **Email Status** | Critical Security Alert | **Malicious Phishing Attempt** |

---

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
