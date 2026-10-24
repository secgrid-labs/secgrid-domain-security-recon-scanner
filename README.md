# 🛡️ SecGrid Domain Security, SSL & Recon Scanner

[![Apify Actor](https://img.shields.io/badge/Apify_Store-Run_Actor-00C853?style=for-the-badge&logo=apify)](https://apify.com/secgrid/secgrid-domain-security-recon-scanner)
[![Security Grade](https://img.shields.io/badge/Security_Audit-A%2B_to_F-blue?style=for-the-badge)](https://apify.com/secgrid/secgrid-domain-security-recon-scanner)
[![Maintained by SecGrid Labs](https://img.shields.io/badge/Maintained_by-SecGrid_Labs-1E293B?style=for-the-badge)](https://apify.com/secgrid)

**SecGrid Domain Security, SSL & Recon Scanner** is an enterprise-grade, high-speed intelligence utility engineered by **SecGrid Labs**. It audits target domains at scale for SSL/TLS certificate validity, HTTP security headers, server infrastructure, web technology stacks, and public B2B contact intelligence.

👉 **[Run this Actor live on the Apify Store](https://apify.com/secgrid/secgrid-domain-security-recon-scanner)**  
👉 **[Try the Pre-Configured Example Task](https://apify.com/secgrid/secgrid-domain-security-recon-scanner/examples/secgrid-domain-security-recon-scanner-task)**

---

## 🚀 Key Capabilities

* **Institutional Security Grading (`A+` to `F`):** Evaluates SSL/TLS status alongside 6 core HTTP security headers (`Strict-Transport-Security`, `Content-Security-Policy`, `X-Frame-Options`, `X-Content-Type-Options`, `Referrer-Policy`, `Permissions-Policy`).
* **SSL/TLS Certificate Intelligence:** Extracts certificate issuer, validity state, and exact **days remaining until expiration** to prevent downtime.
* **Tech-Stack & Infrastructure Recon:** Resolves underlying IPv4 addresses, server software banners, and web frameworks (`Cloudflare`, `Nginx`, `Apache`, `Vercel`, `Next.js`, `Shopify`, `WordPress`, `Google Tag Manager`).
* **B2B Lead & Social Extraction:** Crawls target landing pages to harvest verified public business contact emails and official social media profiles (`LinkedIn`, `X/Twitter`, `Facebook`, `Instagram`).
* **AI & Automation Ready:** Seamlessly integrates with **Claude (MCP), Cursor, n8n, Make, Zapier**, and REST APIs.

---

## 📊 Sample Output (JSON)

```json
[
  {
    "domain": "cloudflare.com",
    "security_grade": "A+",
    "security_score": "100/100",
    "http_status": 200,
    "ip_address": "104.16.133.229",
    "ssl_valid": true,
    "ssl_days_remaining": 42,
    "ssl_issuer": "Google Trust Services",
    "detected_technologies": [
      "Cloudflare",
      "Google Tag Manager / Analytics",
      "Shopify"
    ],
    "server_software": "cloudflare",
    "public_emails": [],
    "social_profiles": {
      "linkedin": "[https://www.linkedin.com/company/cloudflare](https://www.linkedin.com/company/cloudflare)",
      "twitter_x": "[https://x.com/cloudflare](https://x.com/cloudflare)"
    },
    "security_headers_present": [
      "Strict-Transport-Security",
      "Content-Security-Policy",
      "X-Frame-Options",
      "X-Content-Type-Options",
      "Referrer-Policy",
      "Permissions-Policy"
    ],
    "security_headers_missing": [],
    "page_title": "Cloudflare: Build for the agent era",
    "audited_at_utc": "2026-10-23T20:35:11.451407+00:00"
  }
]
```

---

## ⚡ Quick Start via Apify API (Python)

You can trigger this scanner programmatically using the official `apify-client` package:

```python
from apify_client import ApifyClient

client = ApifyClient("YOUR_APIFY_API_TOKEN")

run_input = {
    "domains": ["apify.com", "github.com", "cloudflare.com"],
    "extractEmails": True,
    "timeoutSecs": 10,
}

run = client.actor("secgrid/secgrid-domain-security-recon-scanner").call(run_input=run_input)

for item in client.dataset(run["defaultDatasetId"]).iterate_items():
    print(item)
```

---

## 📫 Support & Enterprise Inquiries

Need a custom web scraper, dedicated security pipeline, or higher rate limits?  
* **Email:** `secgrid.support@gmail.com`  
* **Apify Profile:** [apify.com/secgrid](https://apify.com/secgrid)
