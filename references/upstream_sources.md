# Upstream Accelerated Sources & References

This document maps the world-class open-source repositories integrated into **Agentic Security Arsenal**. 
Instead of cloning heavy repositories, the agent references their proven architectures, rulesets, and APIs remotely on-demand.

---

## 1. Static Analysis & Code Audit (White-box)

| Repository | Upstream URL | How We Utilize It (Zero-Clone) |
| :--- | :--- | :--- |
| **Semgrep Registry** | `semgrep/semgrep` | Uses remote rule packs on-demand (`--config p/php`, `--config p/owasp-top-ten`) without storing gigabytes of rules locally. |
| **WordPress Coding Standards** | `WordPress/WordPress-Coding-Standards` | Ruleset specifications for nonces, unslashed inputs, and capability checks. |
| **PHP_CodeSniffer** | `PHPCSStandards/PHP_CodeSniffer` | Syntax and AST linting standards. |

---

## 2. External Attack Surface & Recon (Black-box)

| Repository | Upstream URL | How We Utilize It (Zero-Clone) |
| :--- | :--- | :--- |
| **Subfinder** | `projectdiscovery/subfinder` | Consumes pre-built binary; queries 30+ passive sources via official API keys. |
| **HTTPX** | `projectdiscovery/httpx` | Native JSON streamer (`-json`) for fingerprinting, status codes, and tech detection. |
| **Katana** | `projectdiscovery/katana` | Headless crawler recipes with JavaScript endpoint scraping (`-jc`). |
| **GAU** | `lc/gau` | On-demand querying of Wayback Machine, AlienVault, and URLScan without local DB. |

---

## 3. Vulnerability Scanning & Misconfiguration

| Repository | Upstream URL | How We Utilize It (Zero-Clone) |
| :--- | :--- | :--- |
| **Nuclei Templates** | `projectdiscovery/nuclei-templates` | Nuclei automatically downloads and syncs official verified community templates via `nuclei -update-templates` on first run. Zero manual cloning needed. |
| **WPScan Core** | `wpscanteam/wpscan` | API integration with WPVulnDB for known vulnerable plugin versions. |

---

## 4. Agentic AI & MCP Orchestration

| Repository | Upstream URL | How We Utilize It (Zero-Clone) |
| :--- | :--- | :--- |
| **PD Tools MCP** | `intelligent-ears/pd-tools-mcp` | Standard MCP JSON-RPC schema wrapper for ProjectDiscovery tools. |
| **Agentic Bug Hunter** | `Awarexone/Agentic-Bug-Hunter` | Triage workflow logic, verification gates, and prompt chaining patterns. |
| **PentestGPT** | `GreyDGL/PentestGPT` | Parsing & reasoning chain-of-thought methodologies. |
