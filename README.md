# SecGrid Domain Security Scanner

[![Run on Apify](https://img.shields.io/badge/Apify_Store-Run_Actor-00C853?style=for-the-badge&logo=apify)](https://apify.com/secgrid/secgrid-domain-security-recon-scanner)
[![Maintained by SecGrid Labs](https://img.shields.io/badge/Maintained_by-SecGrid_Labs-1E293B?style=for-the-badge)](https://apify.com/secgrid)

An [Apify](https://apify.com) Actor that checks many domains in one run and returns an **A+ to F security grade**, SSL/TLS certificate details, security headers, a technology-stack guess and public contact information from the homepage.

**[Run it on the Apify Store](https://apify.com/secgrid/secgrid-domain-security-recon-scanner)**

## What it does

- **Security grade (A+ to F):** valid SSL/TLS certificate (40 points) plus 6 security headers (10 points each): `Strict-Transport-Security`, `Content-Security-Policy`, `X-Frame-Options`, `X-Content-Type-Options`, `Referrer-Policy`, `Permissions-Policy`.
- **SSL/TLS details:** certificate valid or not, issuer, days until expiry, TLS version.
- **Infrastructure hints:** IPv4 address, server banner, and technology hints (Cloudflare, Nginx, Apache, Vercel, Next.js, WordPress and others).
- **Homepage contacts (optional):** public email addresses and social profile links found on the homepage. Emails are **not verified**.
- **Integrations:** JSON, CSV and Excel export, Apify API, Make, n8n, Zapier.

## Quick start (Python)

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
    print(item["domain"], item["security_grade"], item["ssl_days_remaining"])
```

## Example output (illustrative values)

```json
{
  "domain": "example.com",
  "security_grade": "B",
  "security_score": "70/100",
  "http_status": 200,
  "ip_address": "203.0.113.10",
  "ssl_valid": true,
  "ssl_issuer": "Let's Encrypt",
  "ssl_days_remaining": 61,
  "detected_technologies": ["Nginx"],
  "security_headers_present": ["Strict-Transport-Security", "X-Content-Type-Options", "Referrer-Policy"],
  "security_headers_missing": ["Content-Security-Policy", "X-Frame-Options", "Permissions-Policy"],
  "public_emails": ["info@example.com"],
  "social_profiles": { "linkedin": "https://www.linkedin.com/company/example" },
  "page_title": "Example Domain",
  "audited_at_utc": "2026-01-01T12:00:00+00:00"
}
```

## Good to know

- The grade is a quick first look. It checks whether headers are present, not how strong their values are, and it does not check SPF/DMARC or old TLS versions.
- Technology detection is based on hints and can be wrong.
- It is a passive outside-in check: one DNS lookup, one TLS connection and one page request per domain.
- Only check domains you own, manage or have a legitimate reason to assess.

## Support

Open an issue here or on the Actor page, or email **secgrid.support@gmail.com**. We reply within 1 to 2 business days.

Built by [SecGrid Labs](https://apify.com/secgrid).
