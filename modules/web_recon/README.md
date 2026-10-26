# Web Recon Module (External Attack Surface)

This module focuses on passive and low-noise reconnaissance for web assets, subdomains, and historical endpoints.

---

## 1. Toolset Overview

- **`subfinder`**: Fast, passive subdomain enumeration via public APIs.
- **`httpx`**: Multi-purpose HTTP probe (status codes, titles, technologies, response sizes).
- **`katana`**: Next-generation web crawler and JavaScript parser.
- **`gau` (GetAllURLs)**: Fetches historical URLs from AlienVault, Wayback Machine, and URLScan.

---

## 2. Agentic Recon Recipes

### Recipe 1: Passive Subdomain Discovery -> Live HTTP Probe (JSON Pipeline)
```bash
subfinder -d <target.com> -silent | httpx -silent -json -title -tech-detect -status-code -o live_hosts.json
```

### Recipe 2: Historical URL Extraction & Sensitive File Grep
```bash
gau <target.com> --subs | grep -E "\.(xls|xlsx|doc|docx|pdf|sql|conf|env|bak|log)$" | sort -u > sensitive_history.txt
```

### Recipe 3: High-Yield Crawler with Katana
```bash
katana -u https://<target.com> -silent -json -depth 3 -jc -o endpoints.json
```
*-jc parses JavaScript files automatically for hidden endpoints and secrets.*
