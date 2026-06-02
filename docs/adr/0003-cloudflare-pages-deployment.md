# Cloudflare Pages for deployment and hosting

The blog deploys to **Cloudflare Pages** via automatic Git-based builds. Push to `main` → Cloudflare builds with Hugo and deploys to `blog.coffeecoded.dev`. No separate CI pipeline, no manual upload step, no DNS configuration needed beyond Cloudflare's dashboard.

## Considered options

- **GitHub Pages.** Already configured (later removed). Rejected because it requires managing DNS separately from the hosting provider, and Cloudflare is already the domain registrar — keeping everything in one vendor is simpler for a single-maintainer project.
- **Netlify/Vercel.** Better build caching and preview deployment UX. Rejected because they add a third vendor (Cloudflare for DNS, GitHub for code, Netlify/Vercel for hosting) when Cloudflare can do it all. The DX gain doesn't justify the operational fragmentation.
- **Self-hosted (S3 + CloudFront, VPS).** Rejected — overkill for a static blog, and contradicts the resilience priority (more infra to maintain).

## Consequence

The blog's entire deploy surface is: Cloudflare Pages project connected to the GitHub repo. DNS, HTTPS, CDN, and build pipeline are handled by one vendor. Future-you touches one dashboard, not three.
