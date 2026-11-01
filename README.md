# Public Static Assets & Media CDN

A centralized, vendor-agnostic repository for hosting public brand assets, logos, icons, and media across all apps, services, and documentation.

Delivered globally via **Edge CDNs** with automated SSL, HTTP/3, and edge caching.

---

## 📁 Directory Architecture

Organize assets by project or application name:

```text
├── <project-or-app-name>/
│   ├── logos/
│   │   ├── logo-light.png
│   │   ├── logo-dark.png
│   │   └── logo.svg
│   ├── icons/
│   │   ├── favicon.ico
│   │   ├── icon-192.png
│   │   └── icon-512.png
│   ├── banners/
│   │   └── og-image.png
│   └── docs/
│       └── diagram.svg
├── shared/
│   └── placeholders/
└── README.md
```

---

## 🌐 CDN Delivery Endpoints

Any asset committed to this repository can be fetched globally via the following edge networks:

### 1. jsDelivr Edge CDN (Primary / Recommended)
Global Cloudflare + Fastly multi-CDN network with automatic minification and zero rate limits.

- **Latest from branch (`main`):**
  ```text
  https://cdn.jsdelivr.net/gh/<USER>/<REPO>@main/<APP>/<PATH>/<FILE>
  ```
- **Immutable / Production Release Tag (Guaranteed never to break or change):**
  ```text
  https://cdn.jsdelivr.net/gh/<USER>/<REPO>@v1.0.0/<APP>/<PATH>/<FILE>
  ```

### 2. Statically CDN (Alternative)
Multi-CDN edge powered by Cloudflare, Fastly, and BunnyCDN:
```text
https://cdn.statically.io/gh/<USER>/<REPO>/main/<APP>/<PATH>/<FILE>
```

### 3. GitHub Raw (Direct Fallback)
```text
https://raw.githubusercontent.com/<USER>/<REPO>/main/<APP>/<PATH>/<FILE>
```

---

## 💻 Integration Examples

### HTML & Transactional Email
```html
<!-- Transactional Email Header (Compatible with Gmail, Outlook, Apple Mail) -->
<img 
  src="https://cdn.jsdelivr.net/gh/<USER>/<REPO>@main/<APP>/logos/logo-light.png" 
  alt="Brand Logo" 
  width="36" 
  height="36" 
  style="display:block;border:0;outline:none;"
/>
```

### Next.js / React
```tsx
import Image from "next/image";

export function BrandLogo() {
  return (
    <Image
      src="https://cdn.jsdelivr.net/gh/<USER>/<REPO>@main/<APP>/logos/logo-light.png"
      alt="Brand Logo"
      width={120}
      height={32}
      priority
    />
  );
}
```

### Backend `.env`
```env
# Email Template Branding
EMAIL_TEMPLATE_LOGO_URL=https://cdn.jsdelivr.net/gh/<USER>/<REPO>@main/<APP>/logos/logo-light.png
```

---

## ⚡ Cache Management

### Instant Cache Invalidation
When updating an existing file with the same name, purge the CDN edge cache immediately:
```text
https://purge.jsdelivr.net/gh/<USER>/<REPO>@main/<APP>/<PATH>/<FILE>
```

### Production Stability Tip
For mission-critical production environments, use Git Release Tags instead of branch names (e.g. `@v1.2.0` instead of `@main`). Tagged URLs are immutable and cached forever, preventing unexpected visual regressions.

---

## 📐 Asset Guidelines

1. **Vector First**: Prefer `.svg` for geometric icons, diagrams, and vector logos.
2. **Raster Optimization**: Compress `.png` and `.jpg` files using lossless tools (e.g., TinyPNG, pngquant) prior to commit.
3. **Naming Convention**: Use lowercase kebab-case (e.g., `logo-mark.png`, `hero-dark.svg`).
4. **Transparency**: Always export icon and logo PNGs with an alpha channel.
