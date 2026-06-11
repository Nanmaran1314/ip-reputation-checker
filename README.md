# 🛡 IP Sentinel — SOC IP Reputation Checker

A fully client-side web tool for SOC analysts to quickly triage large lists of IPs.  
No backend needed — all API calls are made directly from the browser.

---

## ✅ Supported Sources

| Source        | Tier              | Daily Limit      | What it provides                        |
|---------------|-------------------|------------------|-----------------------------------------|
| **ip-api**    | Free, no key      | 45 req/min       | Country, ISP, ASN, proxy/hosting flag   |
| **VirusTotal**| Freemium          | 4 lookups/min    | AV engine detections, reputation score  |
| **AbuseIPDB** | Freemium          | 1,000/day        | Community abuse reports, confidence %   |
| **IPQualityScore** | Freemium   | 200/day          | Fraud score, proxy/VPN/Tor/bot flags    |

---

## 🚀 Deploy to Vercel (2 minutes)

### Option A — Drag & Drop
1. Go to [vercel.com](https://vercel.com) → New Project
2. Drag this folder into the browser upload zone
3. Click Deploy — done!

### Option B — CLI
```bash
npm i -g vercel
cd ip-reputation-checker
vercel
```

### Option C — GitHub
1. Push this folder to a GitHub repo
2. Import the repo on Vercel — auto-deploys on every push

---

## 🔑 Getting Free API Keys

| Service | Sign-up URL | Notes |
|---------|------------|-------|
| VirusTotal | https://www.virustotal.com/gui/join-us | Free: 4 req/min, 500/day |
| AbuseIPDB | https://www.abuseipdb.com/register | Free: 1,000 checks/day |
| IPQualityScore | https://www.ipqualityscore.com/create-account | Free: 200/day |

Keys are stored in the browser's `localStorage` — never sent anywhere except the respective API.

---

## ⚡ Features

- **Real-time results** — cards appear as each IP is checked
- **Verdict engine** — aggregates signals from all sources into Clean / Suspicious / Malicious
- **Summary bar** — quick overview of how many IPs are in each category
- **CSV export** — one click to download all results
- **JSON copy** — copy full raw data per IP for incident reports
- **Rate-limit aware** — adds a delay between IPs when VT key is present
- **Fully offline keys** — API keys stored in localStorage only

---

## 📊 Verdict Logic

| Condition | Verdict |
|-----------|---------|
| VT malicious ≥ 3 OR AbuseIPDB ≥ 80% OR IPQS fraud ≥ 85 | **Malicious** |
| VT malicious ≥ 1 OR AbuseIPDB ≥ 25% OR IPQS fraud ≥ 60 OR Proxy/Tor detected | **Suspicious** |
| All sources respond with no flags | **Clean** |
| No API keys configured, no data | **Unknown** |

---

## 🔒 Privacy & Security

- Zero backend — all API calls go directly from your browser to each provider
- API keys are stored only in `localStorage` on your own machine
- No data is logged or stored anywhere by this app
- Safe to self-host on an internal Vercel deployment or private network
