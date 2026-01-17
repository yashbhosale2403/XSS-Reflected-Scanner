````md
# XSS-Reflected-Scanner

**Reflected XSS hunting tool for authorized assessments.** Crawls endpoints, fuzzes params/forms using marker-based payloads, validates reflections with context checks to avoid noise, and outputs severity-driven results with charts.

---

## ⚡ What it does

This tool performs **reflected XSS testing** by:
- Crawling the target website (internal links only)
- Discovering URLs with query parameters
- Extracting forms + input fields
- Injecting marker-based XSS payloads
- Confirming reflection using context-aware checks (to reduce false positives)
- Reporting findings with severity + graphs

---

## ✅ Key Features

### 🔍 Smart Crawling
- Crawls internal endpoints up to a limit
- Extracts endpoints from:
  - `<a href>`
  - `<script src>`
  - URLs embedded inside JavaScript strings

### 🎯 Parameter Enumeration
- Automatically detects URLs with query parameters (example):
  - `https://site.com/search?q=test`
  - `https://site.com/page?id=1`

### 📝 Form Fuzzing
- Finds forms and inputs (`input`, `textarea`)
- Tests both GET and POST forms

### 💉 Payload Engine
- Multiple payload types: script/svg/img/iframe/attribute breakouts
- Auto-generates payload variants:
  - raw payload
  - URL encoded (1x)
  - double URL encoded (2x)
  - HTML entity encoded
  - mixed encoding

### 🧠 False-Positive Control
- Uses **unique marker per scan**
- Confirms only if marker appears in **executable context**
- Prevents noise from safely escaped reflections

### 🚨 Severity Scoring
- Severity levels:
  - **HIGH**
  - **MEDIUM**
  - **LOW**
  - **INFO**
- Final verdict is based on highest severity finding

### 📊 Charts / Reporting
Generates charts automatically:
- Findings by type (URL XSS vs Form XSS)
- Website status (Safe vs Vulnerable)
- Severity distribution

### ⚡ Multi-threaded Scanning
Uses `ThreadPoolExecutor` for faster scanning.

---

## 🎯 What it detects (Scope)

✅ Detects:
- Reflected XSS in:
  - URL parameters
  - GET/POST forms

❌ Not included:
- Stored XSS
- Blind XSS
- DOM-based XSS
- Exploitation/WAF bypass modules

---

## 🧰 Requirements

- Python **3.8+**
- Dependencies:
  - `requests`
  - `beautifulsoup4`
  - `matplotlib`

---

## 🚀 Installation

### 1) Clone Repository
```bash
git clone https://github.com/<your-username>/XSS-Reflected-Scanner.git
cd XSS-Reflected-Scanner
````

### 2) Install Dependencies

```bash
pip install -r requirements.txt
```

If you don’t have `requirements.txt`:

```bash
pip install requests beautifulsoup4 matplotlib
```

---

## ▶️ Usage

Run the scanner:

```bash
python scanner.py
```

Enter target URL:

```txt
Enter target URL (Legal only): https://example.com
```

---

## ⚙️ Configuration

Modify these values in the script:

```python
TIMEOUT = 12
MAX_THREADS = 10
CRAWL_LIMIT = 80
DELAY = 0.2
```

### Recommended tuning

* If target is **large** → increase `CRAWL_LIMIT`
* If target is **blocking / rate limiting** → increase `DELAY`
* If target is **stable / fast** → increase `MAX_THREADS` (responsibly)

---

## 📌 Output

The scanner prints a clean assessment report including:

* Total pages crawled
* Parameter URLs discovered
* Confirmed findings + evidence URLs
* Severity breakdown
* Final verdict
* Graphs/Charts for reporting

Example verdict:

* ✅ SAFE
* ⚠️ LOW-RISK
* ❌ VULNERABLE
* ❌ CRITICAL

---

## 🛡️ Legal / Ethics

This tool is intended only for:
✅ learning
✅ labs (DVWA / bWAPP / Juice Shop)
✅ bug bounty programs (in-scope targets only)
✅ pentesting with written permission

**Do NOT scan targets without permission.**
You are responsible for how you use this tool.

---

## 🤝 Contributing

PRs are welcome.
If you want to contribute, please include:

* affected target sample
* scanner output
* reproduction steps

---
