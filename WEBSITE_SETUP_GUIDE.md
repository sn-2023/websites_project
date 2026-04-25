# Website Setup — Ready Reckoner
Complete checklist for launching a new static website from scratch.

---

## PHASE 1 — Domain (Hostinger)

- [ ] Go to hostinger.com → search your domain name
- [ ] Choose `.org` / `.com` / `.io` — check availability
- [ ] Purchase domain (note: auto-renewal is ON by default — check settings)
- [ ] Go to **Hostinger Dashboard → DNS / Nameservers**
- [ ] You will update DNS here after Vercel setup (do not touch yet)

---

## PHASE 2 — GitHub Repository

- [ ] Go to github.com → New Repository
- [ ] Name it (e.g. `websites_project`)
- [ ] Set to **Public**
- [ ] Create the repo
- [ ] On your local machine, open Git Bash in your project folder:
```bash
git init
git remote add origin https://github.com/YOUR-USERNAME/YOUR-REPO.git
git add .
git commit -m "Initial commit"
git push origin main
```
- [ ] Verify files appear on GitHub

> **Folder structure tip:** If you have multiple sites in one repo,
> put each site in its own subfolder e.g. `myrepo/qrmake/index.html`
> Vercel will serve from the subfolder (set Root Directory in Vercel)

---

## PHASE 3 — Vercel Setup

- [ ] Go to vercel.com → Sign up with GitHub account
- [ ] Click **Add New Project**
- [ ] Import your GitHub repository
- [ ] **IMPORTANT — Set Root Directory:**
  - Settings → General → Root Directory
  - Enter the subfolder name (e.g. `qrmake`) if your site is in a subfolder
  - Leave blank if index.html is at repo root
- [ ] Click **Deploy** — Vercel gives you a `.vercel.app` URL
- [ ] Verify the site loads on the `.vercel.app` URL before connecting domain

---

## PHASE 4 — Connect Domain to Vercel

- [ ] In Vercel → Project → **Settings → Domains**
- [ ] Click **Add Domain** → type your domain (e.g. `qrmake.org`)
- [ ] Vercel will show you DNS records to add — copy them
- [ ] Go back to **Hostinger → DNS Settings**
- [ ] Add the records Vercel gave you:
  - Usually an **A record** pointing to Vercel IP `76.76.21.21`
  - And a **CNAME** for `www` pointing to `cname.vercel-dns.com`
- [ ] Back in Vercel → Domains → click **Refresh** — wait for green tick
- [ ] DNS propagation takes 10 min to 24 hours
- [ ] Add `www` redirect: Vercel → Domains → add `www.yourdomain.com` → set 307 redirect to root domain
- [ ] Verify both `yourdomain.com` and `www.yourdomain.com` load correctly

---

## PHASE 5 — Google Analytics

- [ ] Go to analytics.google.com
- [ ] Click **Create Property**
- [ ] Enter website name, URL, industry, timezone
- [ ] Choose **Web** platform
- [ ] Copy your **Measurement ID** (looks like `G-XXXXXXXXXX`)
- [ ] Add to every HTML page inside `<head>`:
```html
<script async src="https://www.googletagmanager.com/gtag/js?id=G-XXXXXXXXXX"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());
  gtag('config', 'G-XXXXXXXXXX');
</script>
```
- [ ] Deploy the pages with Analytics code
- [ ] Go to Analytics → **Realtime** → open your site → confirm green dot appears

---

## PHASE 6 — Google Search Console

- [ ] Go to search.google.com/search-console
- [ ] Click **Add Property** → choose **Domain** type
- [ ] Enter your domain (e.g. `qrmake.org`)
- [ ] Google gives you a DNS TXT record — copy it
- [ ] Go to **Hostinger → DNS** → add TXT record → paste value
- [ ] Back in Search Console → click **Verify**
- [ ] Go to **Sitemaps** → enter `sitemap.xml` → Submit
- [ ] Verify status shows **Success** and Discovered Pages > 0

---

## PHASE 7 — Sitemap & Robots.txt

- [ ] Create `sitemap.xml` in root folder:
```xml
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
  <url><loc>https://yourdomain.com/</loc><lastmod>2025-01-01</lastmod><priority>1.0</priority></url>
  <url><loc>https://yourdomain.com/page-name/</loc><lastmod>2025-01-01</lastmod><priority>0.8</priority></url>
</urlset>
```
- [ ] Create `robots.txt` in root folder:
```
User-agent: *
Allow: /
Sitemap: https://yourdomain.com/sitemap.xml
```
- [ ] Push to GitHub → Vercel deploys automatically
- [ ] Resubmit sitemap in Search Console after any new pages added

---

## PHASE 8 — SEO Basics (Every Page)

- [ ] Unique `<title>` tag — include main keyword
- [ ] `<meta name="description">` — 150-160 characters
- [ ] `<link rel="canonical" href="https://yourdomain.com/page/">` 
- [ ] `<meta name="robots" content="index, follow">`
- [ ] H1 tag — one per page, includes main keyword
- [ ] Internal links — every page links to at least 3 other pages
- [ ] Footer navigation — links to all main pages

---

## PHASE 9 — GEO (AI Chatbot Visibility)

For each page, add inside `<head>`:

- [ ] **FAQPage JSON-LD schema** — 5-6 Q&A pairs, direct quotable answers
- [ ] **SoftwareApplication / Article / HowTo schema** depending on page type
- [ ] **Statistics box** in content — quantified data with source names
- [ ] **"According to [Source], [stat]"** sentences in paragraphs
- [ ] **Expanded FAQ section** — 2-3 sentence answers, conversational prose

```html
<script type="application/ld+json">
{"@context":"https://schema.org","@type":"FAQPage","mainEntity":[
  {"@type":"Question","name":"YOUR QUESTION?",
   "acceptedAnswer":{"@type":"Answer","text":"Direct 2-3 sentence answer."}}
]}
</script>
```

---

## PHASE 10 — Keyword Research (Ahrefs)

- [ ] Keywords Explorer → search your main topic
- [ ] Filter: **KD max 30**, **SV min 200**, Country: US (then repeat for IN)
- [ ] Separate tool pages (generator/creator) from guide pages (how-to/what-is)
- [ ] Tool pages → build a working generator
- [ ] Guide pages → 600-900 words of genuine helpful content
- [ ] Check India market separately — set country to **India** in Ahrefs
- [ ] Look for branded payment/platform keywords (UPI, GPay, PhonePe etc.)

---

## PHASE 11 — Indexing New Pages

After deploying new pages:
- [ ] Google Search Console → **URL Inspection**
- [ ] Paste each new URL → click **Request Indexing**
- [ ] Limit: **10 requests per day**
- [ ] Re-submit sitemap if more than 5 new pages added
- [ ] Wait 24-72 hours for indexing, 2-4 weeks for rankings

---

## PHASE 12 — Backlinks

- [ ] **AlternativeTo** — add your tool, mark as alternative to competitors
- [ ] **Futurepedia** — futurepedia.io/submit-tool
- [ ] **Toolify** — toolify.ai/submit
- [ ] **There's An AI For That** — theresanaiforthat.com/submit
- [ ] **Product Hunt** — write tagline, description, first comment, launch
- [ ] **Reddit** — answer questions naturally in relevant subreddits
- [ ] **Quora** — answer questions, link to specific tool pages
- [ ] **Ahrefs competitor gap** — Site Explorer → competitor → Backlinks → filter DR 10-40 → email those sites

---

## PHASE 13 — Ongoing Monitoring

**Weekly:**
- [ ] Check Vercel → Deployments — all green?
- [ ] Check Google Analytics → Realtime — traffic flowing?

**Every 2 weeks:**
- [ ] Google Search Console → Performance → check impressions + clicks
- [ ] Note which pages are getting impressions but low clicks (fix title/description)
- [ ] Note which keywords are ranking on page 2 (these need more internal links)

**Monthly:**
- [ ] Ahrefs — new keyword opportunities
- [ ] Add 3-5 new pages targeting low KD keywords
- [ ] Update sitemap → resubmit to Search Console
- [ ] Request indexing for new pages

---

## Quick Reference — Deploy Flow

Every time you add new pages:
```bash
# 1. Make changes in local folder
# 2. Open Git Bash in /tmp/YOUR_CLONED_REPO
git add qrmake/
git commit -m "Add [page name] pages"
git push origin main
# 3. Vercel auto-deploys in ~30 seconds
# 4. Request indexing in Google Search Console
```

---

## Tools & URLs

| Tool | URL | Purpose |
|---|---|---|
| Hostinger | hpanel.hostinger.com | Domain & DNS |
| GitHub | github.com | Code repository |
| Vercel | vercel.com | Hosting & deployment |
| Google Analytics | analytics.google.com | Traffic tracking |
| Google Search Console | search.google.com/search-console | Indexing & rankings |
| Ahrefs | app.ahrefs.com | Keyword research |
| Bing Webmaster | bing.com/webmasters | Bing indexing |

---

*Created: April 2026 — based on qrmake.org setup*
