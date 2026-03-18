## 🚀 [Try the Live Tool →](https://jadhavdeepak27.github.io/indexforce/google-indexing-tool.html)

[![Live Demo](https://img.shields.io/badge/LIVE%20DEMO-Try%20IndexForce%20Now-00ff88?style=for-the-badge)](https://jadhavdeepak27.github.io/indexforce/google-indexing-tool.html)


[README.md](https://github.com/user-attachments/files/26087050/README.md)
# ⬡ IndexForce — Google Indexing API Automation Tool

> **Cut time-to-index from days to minutes.** Submit URLs directly to Google's Indexing API, bypassing crawl budget entirely.

![IndexForce Demo](https://img.shields.io/badge/Google-Indexing%20API%20v3-00ff88?style=for-the-badge&logo=google&logoColor=white)
![Status](https://img.shields.io/badge/Status-Production%20Ready-00ff88?style=for-the-badge)
![Zero Backend](https://img.shields.io/badge/Backend-None%20Required-7c6fcd?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-blue?style=for-the-badge)

---

## The Problem

Google's crawl budget is a bottleneck for large websites. If you have 10,000+ pages — job boards, course directories, local landing pages — Googlebot may take **days or weeks** to discover and re-index updated content. This directly kills organic visibility for time-sensitive pages.

## The Solution

IndexForce uses the **Google Indexing API v3** to programmatically notify Google the moment a page is created or updated. No waiting. No crawl queue. Google receives a direct signal and queues an immediate crawl.

> We used this to push 30+ priority pages into the Top 5 in minutes instead of days.

---

## ✨ Features

| Feature | Detail |
|---|---|
| 🔐 **Real OAuth2 Auth** | In-browser JWT signing with RSA-256 via SubtleCrypto — no server needed |
| 📋 **Bulk URL Submission** | Paste hundreds of URLs, one per line — live count as you type |
| 🧪 **Dry Run Mode** | Simulate the full pipeline without burning your 200/day quota |
| 📊 **Live Dashboard** | Real-time stats: Queued / OK / Errors / Pending |
| 📝 **Live Log** | Timestamped log of every action — JWT, token, per-URL result |
| 📈 **Progress Bar** | Animated progress across the full submission queue |
| 🗂️ **Queue & Results Tab** | Full table with status badges, timestamps, error messages |
| 📤 **CSV Export** | One-click export of all results for reporting |
| ⚙️ **Configurable Delay** | Set ms delay between requests to avoid 429 rate limits |
| 🗑️ **URL_DELETED Support** | Signal removed pages for faster deindexing |
| ✅ **JSON Validator** | Validates your Service Account key before submission |
| 📖 **Built-in Setup Guide** | Step-by-step instructions + rate limit reference, no external docs needed |

---

## 🚀 Quick Start

### 1. Download the tool
```bash
git clone https://github.com/YOUR_USERNAME/indexforce.git
cd indexforce
```
Then open `google-indexing-tool.html` in any modern browser. **No installation. No npm. No server.**

### 2. Set up Google Indexing API (one-time)

1. Go to [Google Cloud Console](https://console.cloud.google.com) → create a project
2. Enable **Web Search Indexing API**
3. Create a **Service Account** → Keys → Add Key → JSON → download
4. Go to [Google Search Console](https://search.google.com/search-console) → Settings → Users → Add your service account email as **Owner**

### 3. Submit URLs

1. Open `google-indexing-tool.html` in your browser
2. Paste your Service Account JSON key
3. Add your URLs (one per line)
4. Run **Dry Run** first to validate
5. Uncheck Dry Run → click **Submit to Google**

---

## 🔐 Authentication Flow

IndexForce implements the full Google OAuth2 Service Account flow **client-side** using the Web Crypto API:

```
Service Account JSON
        ↓
  Build JWT Payload  (iss, scope, aud, exp, iat)
        ↓
  Sign with RSA-256  (SubtleCrypto.sign)
        ↓
  POST to oauth2.googleapis.com/token
        ↓
  Receive Bearer Access Token  (TTL: 3600s)
        ↓
  POST /v3/urlNotifications:publish
  Authorization: Bearer {token}
```

---

## 📡 API Details

**Endpoint:**
```
POST https://indexing.googleapis.com/v3/urlNotifications:publish
```

**Request body:**
```json
{
  "url": "https://www.example.com/your-page",
  "type": "URL_UPDATED"
}
```

**Successful response:**
```json
{
  "urlNotificationMetadata": {
    "url": "https://www.example.com/your-page",
    "latestUpdate": {
      "type": "URL_UPDATED",
      "notifyTime": "2026-03-18T14:22:04.123Z"
    }
  }
}
```

**Notification types:**

| Type | When to use |
|---|---|
| `URL_UPDATED` | New page published or existing page updated |
| `URL_DELETED` | Page permanently removed (404/410) |

---

## ⚡ Rate Limits

| Limit | Value |
|---|---|
| URLs per day | **200** per verified GSC property |
| Resets | Midnight Pacific Time |
| Recommended delay | 200ms between requests |
| Token TTL | 3600s (re-auth automatically) |

---

## 🛡️ Security & Privacy

- ✅ Your Service Account JSON key is **never stored** — in-memory only, cleared on tab close
- ✅ API calls go **directly to Google** — no proxy, no third-party server
- ✅ Single HTML file — **fully auditable**, no minified or obfuscated code
- ✅ Zero dependencies — no npm, no CDN, no external scripts (except Google Fonts)

---

## 📁 Repository Structure

```
indexforce/
│
├── google-indexing-tool.html   # The complete tool — open in browser to use
├── README.md                   # This file
└── docs/
    └── IndexForce_Documentation.pdf   # Full technical documentation (optional)
```

---

## 💡 Use Cases

- **Job boards** — index new job postings instantly when published
- **Course directories** — push new program pages live immediately
- **Local landing pages** — get new city/location pages indexed same day
- **E-commerce** — signal product page updates to Google in real time
- **News sites** — ensure breaking content is indexed within minutes

---

## 📊 Results

Using this pipeline on a large career-education website:

- ⏱️ **Time-to-index**: reduced from 2–14 days → **minutes**
- 📈 **30+ priority pages** pushed to Top 5 positions rapidly
- 🎯 **Zero crawl budget wasted** on low-priority pages

---

## 🧰 Tech Stack

| Layer | Technology |
|---|---|
| UI | HTML5 + CSS3 (dark theme, CSS Grid, animations) |
| Auth | Web Crypto API — SubtleCrypto RSA-PKCS1-v1_5 |
| HTTP | Fetch API (native browser) |
| State | Vanilla JS ES6+ |
| Fonts | Space Mono + Syne (Google Fonts) |
| Dependencies | **Zero** |

---

## 🗺️ Roadmap

- [ ] Sitemap XML import (auto-parse URLs from sitemap)
- [ ] Scheduled/automated submission via cron + Node.js script version
- [ ] Multi-property support (submit to multiple GSC properties in one run)
- [ ] Slack/webhook notification on completion
- [ ] Chrome Extension version

---

## 📄 License

MIT License — free to use, modify, and distribute.

---

## 🙋 Contributing

Pull requests welcome. For major changes, open an issue first to discuss what you'd like to change.

---

<div align="center">
  <sub>Built with the Google Indexing API v3 · No crawl budget waiting · Just results</sub>
</div>
