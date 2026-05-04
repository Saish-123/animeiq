# 🎌 AnimeIQ — Full Deployment Guide

> Anime discovery platform with Ezoic monetization setup

---

## 📁 Project Structure

```
animeiq/              ← Frontend (deploy to Netlify)
├── homepageblog.html
├── shows.html
├── explore.html
├── binge.html
├── watchorder.htnl.html
├── about.html
├── contactus.html
├── privacy.html
├── disclaimer.html
├── termsandcondition.html
├── netlify.toml       ← ADD THIS FILE
├── .gitignore         ← ADD THIS FILE
└── README.md

anime-backend/        ← Backend (deploy to Render)
├── src/
│   ├── services/
│   │   └── scraping.js
│   ├── index.js
│   ├── index.json
│   ├── filler.json
│   ├── shows.json
│   └── relations_cache.json
├── Ecosystem.config.js
├── fetchAllAnime.js
├── package.json
├── render.yaml        ← ADD THIS FILE
└── .gitignore         ← ADD THIS FILE
```

---

## 🚀 Step-by-Step Deployment

### STEP 1 — Push Frontend to GitHub

```bash
cd Desktop/animeiq

# Copy netlify.toml and .gitignore into this folder first!

git init
git add .
git commit -m "initial commit: animeiq frontend"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/animeiq.git
git push -u origin main
```

### STEP 2 — Deploy Frontend to Netlify

1. Go to [netlify.com](https://netlify.com) → Sign up / Login
2. Click **"Add new site"** → **"Import an existing project"**
3. Connect **GitHub** → select `animeiq` repo
4. Build settings:
   - **Build command:** *(leave empty)*
   - **Publish directory:** `.`
5. Click **Deploy site** ✅
6. Go to **Domain settings** → Add your custom domain (e.g. `animeiq.com`)

### STEP 3 — Push Backend to GitHub

```bash
cd Desktop/anime-backend

# Copy render.yaml and .gitignore into this folder first!

git init
git add .
git commit -m "initial commit: anime-backend"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/anime-backend.git
git push -u origin main
```

### STEP 4 — Deploy Backend to Render

1. Go to [render.com](https://render.com) → Sign up / Login
2. Click **"New"** → **"Web Service"**
3. Connect GitHub → select `anime-backend` repo
4. Settings:
   - **Environment:** Node
   - **Build Command:** `npm install`
   - **Start Command:** `node src/index.js`
   - **Region:** Singapore *(closest to India for low latency)*
5. Click **Create Web Service** ✅
6. Copy the Render URL (e.g. `https://anime-backend.onrender.com`)
7. Update your frontend HTML files to use this backend URL

---

## 🌐 Custom Domain Setup (Required for Ezoic)

Ezoic requires a **custom domain** with real traffic.

### Recommended Domain Registrars:
- **Namecheap** — cheapest (~$8-12/year for .com)
- **GoDaddy** — popular option
- **Porkbun** — very affordable

### DNS Setup After Buying Domain:
1. In Netlify → **Domain Settings** → Add custom domain
2. Netlify will give you **DNS nameservers** or a CNAME
3. Go to your domain registrar → Update nameservers to Netlify's
4. Wait 10-30 min for propagation ✅

---

## 💰 Ezoic Setup (Monetization)

### Requirements Checklist:
- [ ] Custom domain (not `.netlify.app`)
- [ ] SSL certificate (Netlify gives this free ✅)
- [ ] Privacy Policy page ✅ (`privacy.html` exists)
- [ ] About page ✅ (`about.html` exists)
- [ ] Contact page ✅ (`contactus.html` exists)
- [ ] Real content (anime articles, reviews, etc.)
- [ ] At least some organic traffic

### How to Apply:
1. Go to [ezoic.com](https://ezoic.com) → Create account
2. Add your website URL
3. Choose integration: **Cloudflare** (easiest) or **Name Server**
4. Ezoic will verify your site and content
5. Once approved → ads start showing automatically

### Ezoic + Netlify Integration (Recommended: Cloudflare):
1. Sign up for [Cloudflare](https://cloudflare.com) (free)
2. Add your domain to Cloudflare
3. Update nameservers at your registrar to Cloudflare's
4. In Ezoic → choose **Cloudflare Integration**
5. Connect Cloudflare account to Ezoic ✅

---

## ⚡ Performance Tips for More Ezoic Revenue

- Add `<meta>` descriptions to every HTML page (better SEO)
- Add Open Graph tags for social sharing
- Make sure all pages load under 3 seconds
- Add a `sitemap.xml` (Netlify plugin or generate manually)
- Add `robots.txt` to allow crawlers

### robots.txt (create this file in animeiq folder):
```
User-agent: *
Allow: /

Sitemap: https://yourdomain.com/sitemap.xml
```

---

## 🔧 Environment Variables

### Backend (set in Render dashboard):
| Variable | Value |
|----------|-------|
| `NODE_ENV` | `production` |
| `PORT` | `3000` |
| `FRONTEND_URL` | `https://yourdomain.com` |

---

## 📊 Monitoring

- **Netlify Analytics** — built-in, free basic stats
- **Google Analytics 4** — add to all HTML pages
- **Google Search Console** — submit sitemap, track SEO
- **Render Dashboard** — monitor backend health & logs

---

## 🛠️ Common Issues

| Problem | Fix |
|---------|-----|
| Backend sleeping on Render free tier | Upgrade to $7/mo plan or use UptimeRobot to ping it |
| Ezoic not approving | Need more content + traffic first |
| CORS errors | Add CORS headers in `src/index.js` for your domain |
| Custom domain not working | Wait 24-48hrs for DNS propagation |

---

## 📞 Support

- Netlify Docs: https://docs.netlify.com
- Render Docs: https://render.com/docs
- Ezoic Help: https://support.ezoic.com

---

*Built with ❤️ — AnimeIQ*
