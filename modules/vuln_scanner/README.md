# Vulnerability Scanner Module

This module orchestrates targeted, template-driven vulnerability scanning and misconfiguration detection.

---

## 1. Primary Engine: Nuclei

**`nuclei`** is the gold standard for targeted vulnerability scanning. It uses community-reviewed YAML templates and outputs clean structured data.

### Recipe 1: Targeted Exposure & Misconfiguration Scan
Scan live hosts for exposed panels, config files, and git leaks:
```bash
nuclei -l live_hosts.txt -tags exposure,misconfig,tokens -je nuclei_exposures.json -rate-limit 50
```

### Recipe 2: Targeted CVE Scan (Specific Technology)
Scan for known vulnerabilities matching WordPress or Apache:
```bash
nuclei -u https://<target.com> -tags cve,wordpress -je nuclei_wp_cves.json
```

### Recipe 3: Testing Single Template without Noise
```bash
nuclei -u https://<target.com> -t http/cves/2024/ -je results.json
```

---

## 2. Safe Probing Guidelines
- Always set `-rate-limit 30` to `50` to avoid triggering web application firewalls (WAF) or degrading target services.
- Never run active exploitation templates on production targets unless strictly permitted by program scope.
