# Amazon Category API: Geekflare Shows The Best Way To Extract Structured Category Data, How To Navigate Rate Limits, And Tips For Scaling Scrapes Efficiently — A Developer’s Guide

Welcome to the **Amazon Category Scraper API** guide, where a FinOps-mindful full-stack lead walks you through using the **Geekflare Web Scraping API** for large-scale Amazon category extraction, covering JavaScript rendering, anti-bot bypass, and clean structured data while keeping credit costs transparent.

---

## Modeling Monthly Request Volume Without Pricing Surprises

When you design an Amazon category scraper, the first question is **how many pages will you request each month?** That number translates directly into credits, and credits dictate which Geekflare tier you can stay in without hitting the 100% usage wall.

| Monthly pages (Amazon category) | Credits needed (standard) | Credits needed (proxy) | Credits needed (AI extraction) | Credits needed (proxy + AI) |
|--------------------------------|---------------------------|------------------------|--------------------------------|-----------------------------|
| 5 K pages                      | 5 K credits               | 25 K credits           | 40 K credits                  | 60 K credits                |
| 20 K pages                     | 20 K credits              | 100 K credits          | 160 K credits                 | 240 K credits               |
| 75 K pages                     | 75 K credits              | 375 K credits          | 600 K credits                 | 900 K credits               |
| 250 K pages                    | 250 K credits             | 1.25 M credits         | 2 M credits                   | 3 M credits                 |

*Why the jump?*  
- A **standard** scrape costs **1 credit** per request (JS rendering, CAPTCHA solving, anti-bot bypass are bundled).  
- Adding **proxy** adds **+4 credits**, making each request **5 credits** total.  
- Adding **AI extraction** adds **+7 credits**, for **8 credits** per request.  
- Combining both adds **12 credits** per request.

Now translate those credit totals into Geekflare tiers:

| Tier (monthly price) | Credit allotment | Cost per 1 K standard credits | Cost per 1 K proxy credits | Cost per 1 K AI credits |
|----------------------|------------------|------------------------------|----------------------------|--------------------------|
| **Free** – $0        | 500 credits      | — (free tier limits)         | — (proxy unavailable)      | — (AI unavailable)      |
| **Starter** – $19    | 10,000 credits   | $1.90                        | $9.50                      | $15.20                   |
| **Growth** – $69/mo (or $58 / yr) | 100,000 credits | $0.69 | $3.45 | $5.52 |
| **Business** – $349  | 1,000,000 credits| $0.35                        | $1.75                      | $2.79                    |
| **Enterprise** – custom | custom | custom | custom | custom |

If you plan to scrape **20 K Amazon category pages** with **proxy** (to avoid geo-blocks) and **no AI**, you need **100 K credits**. That fits exactly inside the **Growth** tier (100 K credits) and costs **$69 /mo** (or **$58 /mo** if you commit yearly). The same workload on **Starter** would require a **$50 Blaze pack** (50 K credits) plus the $19 subscription, but you'd still fall short, so you'd need **two Blaze packs**—an extra $100 on top of $19.

The key takeaway: **model your monthly page count, decide whether you need proxy or AI, then match the credit total to the nearest tier**. Because credits do **not roll over**, any unused credits disappear on the first of the next billing cycle, so over-provisioning a higher tier just to "save" credits is wasteful. Use the 90% usage alert as a safety net; Geekflare will pause requests at 100% until you upgrade or add a pack.

---

## Geekflare Subscription Lineup and Rate-Limit Caps

Below is a clean snapshot of every Geekflare plan that can power your Amazon category scraper. All numbers come directly from the official pricing page.

| Plan | Monthly price | Credits / month | Cost per 1 K standard | Req / s | Team members | Log retention | Proxy add-on  | Link |
|------|---------------|-----------------|-----------------------|---------|--------------|---------------|-------------- | --- |
| **Free** | $0 | 500 | — (free tier) | 1 | 1 | 7 days | No  | [Start Free](https://geekflare.com/pricing/) |
| **Starter** | $19 | 10,000 | $1.90 | 5 | 3 | 30 days | +4 credits (paid only)  | [Get Starter](https://geekflare.com/pricing/) |
| **Growth** | $69 /mo **or** $58 /mo billed yearly | 100,000 | $0.69 | 10 | 5 | 30 days | +4 credits  | [Get Growth](https://geekflare.com/pricing/) |
| **Business** | $349 | 1,000,000 | $0.35 | 25 | 25 | 90 days | +4 credits  | [Get Business](https://geekflare.com/pricing/) |
| **Enterprise** | Custom | Custom | Custom | up to 1,000 | Custom | Custom | Custom  | [Contact Sales](https://geekflare.com/pricing/) |

**Important billing rules**

* **No credit rollover** – each month's credit pool resets on the 1st.  
* **Failed 5xx requests are free** – you won't lose credits on server errors.  
* **90% usage email alert** – Geekflare notifies you before you hit the limit.  
* **Requests pause at 100%** – you must upgrade or add a credit pack to resume.  
* **7-day refund guarantee** – if you consumed less than 10% of your credits, you can cancel for a full refund.  

**One-Time Credit Packs (Stackable, Valid 1 Year)**

| Pack | Price | Credits | Approx. $/1 K credits |
|------|-------|---------|-----------------------|
| **Spark** | $10 | 5,000 | $2.00 |
| **Blaze** | $50 | 50,000 | $1.00 |
| **Inferno** | $100 | 100,000 | $1.00 |
| **Supernova** | $200 | 200,000 | $1.00 |

You can buy any pack and stack it on top of a Free or paid plan. For example, a **Free** user who needs 5 K extra standard pages can buy a **Spark** pack for $10 and instantly gain 5,000 credits for that month.

---

## How the Major Alternatives Honestly Stack Up

| Provider | Strength | Trade-off | Pricing |
|----------|----------|----------|---------|
| **Geekflare** | Unified credit model, built-in JS rendering, CAPTCHA solving, AI extraction, 99.9% uptime, 4.9 overall rating | Proxy add-on only on paid plans, no custom interactive browser scripting | See Geekflare pricing |
| **Zyte** | Scrapy-native ecosystem, managed data delivery for e-commerce | Dynamic per-request pricing varies with target complexity | See Zyte pricing |
| **Scrapfly** | Adaptive Anti-Scraping Protection (ASP) and request debugging tools | Credit multipliers for JS rendering; smaller AI/no-code ecosystem | See Scrapfly pricing |
| **ScraperAPI** | Structured endpoints for Amazon and Google, DataPipeline batch scheduling | Credit multipliers up to 75× for JS rendering, geotargeting, protected sites; HTML-first output | See ScraperAPI pricing |

**Takeaway:** Geekflare keeps the math transparent—every extra feature is a fixed credit addition, and the per-1 K credit cost is published for each tier. Competitors either hide the exact dollar cost behind dynamic pricing or multiply credits heavily for rendering and geo-targeting, making budgeting far less predictable. If you value a **predictable, credit-based spend model** and need built-in AI extraction, Geekflare is the most financially honest choice.

---

## Which Geekflare Plan Makes Sense for Your Team Stage?

| Monthly request volume (Amazon category pages) | Required credits (standard) | Recommended plan | Reason |
|-----------------------------------------------|-----------------------------|------------------|--------|
| ≤ 500 pages                                    | 500 credits                 | **Free** | No credit card needed, perfect for prototyping or low-traffic niches. |
| 1 K – 8 K pages                                 | 1 K – 8 K credits           | **Starter** | $19 /mo gives 10 K credits, enough headroom plus 5 req/s. |
| 10 K – 80 K pages (no proxy)                   | 10 K – 80 K credits         | **Growth** (monthly) | $69 /mo covers up to 100 K credits; rate limit 10 req/s handles parallel category pulls. |
| 10 K – 80 K pages (proxy required)             | 50 K – 400 K credits (proxy) | **Growth** + **Blaze** pack | Proxy adds +4 credits per request; a Blaze pack gives 50 K extra credits. |
| 150 K – 900 K pages (proxy + AI)               | 1.8 M – 10.8 M credits       | **Business** (or Enterprise) | $349 /mo provides 1 M credits; add Inferno or Supernova packs for overflow. |
| > 1 M pages (enterprise workloads)             | > 12 M credits               | **Enterprise** (custom) | Custom volume and up to 1,000 req/s for massive parallel crawling. |

**Example scenario:** You run a weekly Amazon "Best-Sellers" category scrape that pulls 20 K pages, needs proxy to avoid regional throttling, and you want the AI to summarize each page. That's **20 K × 5 credits = 100 K credits**. The **Growth** plan (100 K credits) covers it exactly, at $69 /mo (or $58 /mo yearly). No extra pack needed.

---

## A Closer Look at Geekflare's Architecture, Formats, and Throughput

**How the Amazon Category Scraper Works**

1. **Request ingestion** – You POST to `https://api.geekflare.com/webscraping` with a JSON payload containing the target Amazon category URL, optional `proxyCountry` (+4 credits, paid plans only), and any `aiPrompt` (+7 credits).
2. **Headless Chrome spin-up** – Geekflare runs a single-credit headless Chrome instance that fully renders the page, executes any client-side JavaScript, and automatically solves CAPTCHAs.  
3. **Anti-bot bypass** – Built-in fingerprint rotation and IP rotation (when proxy is enabled) keep Amazon from serving block pages.  
4. **Output formatting** – The service can return **markdown**, **html**, **text**, or **json**. Adding `-llm` suffix (e.g., `markdown-llm`) runs a lightweight LLM cleanup that strips navigation, ads, and cookie banners, reducing token count by roughly three-quarters.  
5. **AI extraction (optional)** – When you include `aiPrompt` or select a `template` (e.g., `product`), an additional 7 credits are charged, and the response includes a structured JSON object with fields like `title`, `price`, `currency`, `stock`, and `rating`.  

**Supported Output Formats (all within the same 1-credit request)**

| Format | Typical use case | Token reduction |
|--------|------------------|-----------------|
| `html` (default) | Full page capture for downstream parsing | — |
| `json` | Direct machine consumption, no post-processing | — |
| `markdown` | Human-readable notes, quick copy-paste | ~60% of raw HTML |
| `markdown-llm` | Clean article-style content, minimal noise | ~75% reduction |
| `text` | Plain text for simple keyword extraction | ~70% reduction |
| `text-llm` | Summarized text, ready for LLM prompting | ~85% reduction |
| `html-llm` | Stripped HTML, lighter payload | ~60% reduction |

You can request up to **three formats in a single call** without extra credit cost, which is handy when you need both raw HTML for debugging and a clean markdown for downstream pipelines.

**Rate-Limit Mechanics**

- **Free**: 1 req/s – suitable for occasional checks.  
- **Starter**: 5 req/s – allows modest parallelism across a few category pages.  
- **Growth**: 10 req/s – ideal for daily batch jobs that scrape dozens of categories.  
- **Business**: 25 req/s – supports high-frequency monitoring across many marketplaces.  
- **Enterprise**: Up to 1,000 req/s – reserved for large SaaS platforms that need near-real-time price feeds.

All limits are **requests per second**, not concurrent connections, so your client can throttle locally to stay within the allowed bandwidth.

---

## Quickstart Implementation You Can Drop Into Your Repo

Below are two runnable snippets. The first uses plain **cURL** with an MCP JSON payload; the second shows how to invoke the same request via the **Geekflare MCP** hosted UI.

### 1️⃣ cURL + MCP JSON (standard scrape, no proxy, no AI)

```bash
curl -X POST https://mcp.geekflare.com/mcp \
-H "Content-Type: application/json" \
-d '{
  "apiKey": "YOUR_GEekflare_API_KEY",
  "endpoint": "https://api.geekflare.com/webscraping",
  "method": "POST",
  "payload": {
    "url": "https://developer.mozilla.org/en-US/docs/Web/JavaScript",
    "output": ["json","markdown-llm"]
  }
}'
```

**What happens:**  
- The request costs **1 credit** (standard).  
- You receive a JSON body containing the raw page data and a cleaned markdown version.  
- No proxy is used, so the request runs from Geekflare's default egress IP pool.

### 2️⃣ cURL + MCP JSON (proxy + AI extraction for Amazon category)

```bash
curl -X POST https://mcp.geekflare.com/mcp \
-H "Content-Type: application/json" \
-d '{
  "apiKey": "YOUR_GEekflare_API_KEY",
  "endpoint": "https://api.geekflare.com/webscraping",
  "method": "POST",
  "payload": {
    "url": "https://www.amazon.com/dp/B09G3HRMVS",
    "proxyCountry": "us",
    "extractionMode": "template",
    "template": "product",
    "aiPrompt": "Summarize key product details in 2 sentences.",
    "output": ["json","markdown-llm"]
  }
}'
```

**Cost breakdown:**  
- **Standard** = 1 credit  
- **Proxy** = +4 credits → total **5 credits**  
- **AI extraction** = +7 credits → total **12 credits**  

The response includes a structured `product` JSON object plus a concise markdown summary, all for **12 credits**.

---

## Making Sense of Annual Discounts, Packs, and Refunds

**Annual Billing Advantage**

Geekflare offers a **2-month free** discount on yearly commitments. The **Growth** tier drops from **$69 /mo** to **$58 /mo** when you pay annually. That's a straightforward **$58 /mo billed yearly**—no hidden calculations, just two months you don't pay. The same structure applies to other paid tiers (Starter, Business) if you choose the yearly option.

**Refund Policy**

If you cancel within **7 days** and have consumed **less than 10%** of your allocated credits, Geekflare will refund the full amount. This safety net encourages experimentation without fear of sunk cost.

**Credit Packs in Action**

- **Scenario:** You're on the **Free** tier but need to run a one-off bulk scrape of **5 K** Amazon pages with proxy. Purchase a **Spark** pack for **$10**, gaining 5,000 extra credits. The request will cost **5 credits each** (proxy), so you can run **1,000** proxied pages before the pack depletes. Add a second Spark pack if you need the full 5 K pages.
- **Scenario:** Your **Growth** plan is at 85% usage and you anticipate a spike. Buying a **Blaze** pack for **$50** instantly adds 50,000 credits, pushing you safely past the 90% alert threshold.

All packs are valid for **one year**, so you can stock them ahead of seasonal campaigns.

---

## Using Geekflare Across Code, AI Agents, and No-Code Flows

**Official SDKs**

| Language | Package | Install command |
|----------|---------|-----------------|
| Python   | `geekflare-api` | `pip install geekflare-api` |
| Node/TypeScript | `@geekflare/api-node` | `npm install @geekflare/api-node` |

Both SDKs expose a `webScraping` method that mirrors the raw REST payload, handling the `x-api-key` header automatically.

**Managed Control Plane (MCP)**

The hosted MCP at `https://mcp.geekflare.com/mcp` provides a UI for all 18 tools, including **webScrape**, **search**, **screenshot**, and **metaScrape**. You can chain tools together—e.g., run a `search` to discover Amazon category URLs, pipe the results into `webScrape` with proxy and AI extraction, and finally store the JSON output in a Google Sheet.

**AI Framework Integrations**

- **LangChain** – Install `langchain-geekflare` and use `GeekflareWebScraper` as a tool node.  
- **LlamaIndex** – Install `llama-index-tools-geekflare` to add a `GeekflareWebScrapingTool`.  
- **Vercel AI SDK** – The package `@geekflare/ai-sdk` lets you call the AI extraction endpoint directly from Vercel functions.

These integrations let you embed Amazon category scraping into autonomous agents that decide when to fetch, when to summarize, and when to store results.

**No-Code Automation**

- **n8n** – Use the official Geekflare node to schedule daily category scrapes, then route the JSON to a PostgreSQL node.  
- **Zapier** – Trigger a Zap when a new Amazon bestseller appears, run the Geekflare webScrape action, and push the summary to Slack.  
- **Make (formerly Integromat)** – Build a scenario that fetches category pages, applies the `product` template, and writes rows to an Airtable base.  

All three platforms require only your API key; no extra server code is needed.

**Companion Free Tools**

- **Webpage to Markdown** – Convert any URL to clean markdown instantly.  
- **Scraping Feasibility Checker** – Test whether a target page is likely to be blocked before you spend credits.

These tools are great for quick validation before you launch a full-scale Amazon category scrape.

---

## Where Geekflare Wins — And Where You Should Honestly Look Elsewhere

**Strengths**

- **Transparent credit model** – Every extra feature (proxy, AI) is a fixed credit addition, making budgeting painless.  
- **Built-in JS rendering + CAPTCHA solving** for just **1 credit**; no hidden multipliers.  
- **High uptime (99.9%)** across GCP and Cloudflare.
- **Strong community feedback** – 4.9 overall rating, with G2 4.8, Google 4.9, Product Hunt 5.0.  
- **Rich ecosystem** – SDKs, MCP, AI framework adapters, and no-code connectors all share a single API key and credit pool, simplifying ops.

**Limitations**

- **No custom interactive browser scripting** – You cannot program click-through flows or fill forms beyond the single-page render.  
- **Proxy only on paid plans** – Free users cannot access geo-targeted IPs.  
- **Credits do not roll over** – Unused credits vanish each month, so you must size your plan accurately.  
- **Service is cloud-hosted only** – No self-hosted or open-source alternative if you need on-prem isolation.

If your workflow demands complex multi-step navigation (e.g., logging into Amazon seller dashboards) or you require a self-hosted solution for compliance reasons, you may need to explore other vendors. Otherwise, for straightforward category extraction, structured product templates, and optional AI summarization, **Geekflare delivers the most financially predictable experience**.

---

## Frequently Asked Questions

**What is the difference between a "standard" scrape and a "proxy" scrape in terms of credits?**  
A standard scrape costs **1 credit** per request and uses Geekflare's default egress IPs. Adding `proxyCountry` activates the proxy add-on, which adds **+4 credits**, making each request **5 credits** total. Proxy is only available on paid plans.

**Can I combine multiple output formats in one API call?**  
Yes. You can request up to **three formats** (e.g., `json`, `markdown-llm`, `html`) in a single request, and it still consumes only the base credit amount (plus any proxy or AI credits you've added).

**How do I know when I'm approaching my credit limit?**  
Geekflare sends an email alert at **90%** consumption. Once you hit **100%**, further requests are paused until you upgrade or add a credit pack.

**Is there a way to get a refund if I over-estimate my usage?**  
If you cancel within **7 days** and have used **less than 10%** of your allocated credits, you receive a full refund. This applies to any subscription tier.

**Do failed 5xx responses cost me credits?**  
No. Any server-side error (5xx) or failed capture does **not** deduct credits from your pool.

---
