# MotoData VE - Deployment Guide

MotoData VE is built as a static Single Page Application (SPA) with zero external compilation steps. It can be served from any web server, Content Delivery Network (CDN), or object storage provider.

---

## 1. Cloudflare Pages & Cloudflare Workers

Cloudflare provides global CDN caching, automatic HTTPS, and fast asset delivery.

### Option A: Cloudflare Pages (Recommended)
1. Log in to the [Cloudflare Dashboard](https://dash.cloudflare.com/).
2. Navigate to **Workers & Pages** -> **Create application** -> **Pages** -> **Connect to Git**.
3. Select your repository: `alciditox/motoRepuesto`.
4. Configure build settings:
   - **Framework preset**: None / Static HTML.
   - **Build command**: *(Leave blank)*
   - **Build output directory**: `/` (root directory).
5. Click **Save and Deploy**.

### Option B: Cloudflare Workers Static Assets
If deploying via `wrangler`:
```bash
npx wrangler deploy
```

---

## 2. GitHub Pages

GitHub Pages hosts the site directly from your GitHub repository for free:

1. Navigate to your repository: [https://github.com/alciditox/motoRepuesto](https://github.com/alciditox/motoRepuesto).
2. Go to **Settings** -> **Pages**.
3. Under **Build and deployment**:
   - **Source**: `Deploy from a branch`.
   - **Branch**: `main` / `/(root)`.
4. Click **Save**.
5. Within 1-2 minutes, your site will be live at:
   `https://alciditox.github.io/motoRepuesto/`

---

## 3. Local Nginx or Apache Deployment

To host MotoData VE on an existing VPS or dedicated Linux server:

### Nginx Configuration
```nginx
server {
    listen 80;
    server_name motodata.yourdomain.com;

    root /var/www/motoRepuesto;
    index index.html;

    location / {
        try_files $uri $uri/ /index.html;
    }

    # Enable gzip compression for fast delivery
    gzip on;
    gzip_types text/html text/css application/javascript;
}
```

---

## 4. Progressive Web App (PWA) Verification

To ensure full PWA compatibility on Android and iOS:
1. Ensure the site is delivered over **HTTPS** (mandatory for Service Workers and install prompts).
2. Verify that `<meta name="viewport">` and `<meta name="theme-color">` headers are properly recognized.
3. Test using Chromium DevTools:
   - Open Developer Tools (`F12`).
   - Navigate to the **Application** or **Lighthouse** tab.
   - Run a **PWA Audit** to confirm installability criteria.
