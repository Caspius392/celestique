# CELESTIQUE Static Website — Deployment Guide

## Overview
This is a **production-ready static website** (HTML/CSS/JavaScript only). No server, no database, no backend required.

## Contents
```
celestique-static/
├── index.html              # Main entry point
├── robots.txt              # SEO robots configuration
├── sitemap.xml             # XML sitemap for search engines
├── assets/
│   ├── index-[hash].css    # Compiled Tailwind CSS
│   └── index-[hash].js     # Compiled React + application code
└── images/                 # All product and brand images
```

## Deployment Options

### 1. **Vercel** (Recommended - Easiest)
```bash
npm i -g vercel
vercel --prod
```
- Auto-detects static site
- CDN included
- Free tier available
- Custom domain support

### 2. **Netlify**
```bash
npm i -g netlify-cli
netlify deploy --prod --dir=.
```
- Drag & drop deployment
- Free tier with custom domain
- Built-in CDN

### 3. **GitHub Pages**
```bash
# Push to gh-pages branch
git subtree push --prefix celestique-static origin gh-pages
```
- Free hosting
- Custom domain support
- No build step needed

### 4. **AWS S3 + CloudFront**
```bash
aws s3 sync . s3://your-bucket-name
```
- Scalable
- Global CDN
- Pay-as-you-go

### 5. **Cloudflare Pages**
- Connect GitHub repo
- Auto-deploys on push
- Free tier with custom domain

### 6. **Your Own Server**
```bash
# Copy entire folder to web root
scp -r celestique-static/* user@server:/var/www/html/
```
- Apache, Nginx, or any static file server
- Full control
- Configure for SPA routing (optional)

## Important Notes

### SPA Routing
If using a traditional web server (Apache/Nginx), configure to serve `index.html` for all routes:

**Nginx:**
```nginx
location / {
  try_files $uri $uri/ /index.html;
}
```

**Apache (.htaccess):**
```apache
<IfModule mod_rewrite.c>
  RewriteEngine On
  RewriteBase /
  RewriteRule ^index\.html$ - [L]
  RewriteCond %{REQUEST_FILENAME} !-f
  RewriteCond %{REQUEST_FILENAME} !-d
  RewriteRule . /index.html [L]
</IfModule>
```

### SEO
- `robots.txt` is included
- `sitemap.xml` is included
- Submit both to Google Search Console

### Performance
- All assets are minified and optimized
- Images are compressed
- CSS and JS are bundled
- Gzip compression recommended on server

### HTTPS
Always use HTTPS in production. Most modern hosts provide free SSL certificates.

## File Size Reference
- Total: ~57 MB (zip compressed)
- Uncompressed: ~400 MB
- Gzip compressed assets: ~25 MB

## Support
For questions or issues, refer to the original source code at `/home/ubuntu/celestique-website/`
