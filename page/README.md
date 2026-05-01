# Benchmark Page Deployment

> The deployable HTML for the Company Brain Benchmark. Mobile-first, dark theme, no purple.

## Personalize before deploying

Replace `[PLACEHOLDER]` markers in `index.html`:
- Open Graph URL
- GitHub repo URL (methodology repo)
- Spec repo URL (`brain-skill-bundle`)
- Demo URL (BizBrain OS live demo)
- Per-scoring URLs (`scoring/*.md` on the methodology repo)
- Author name + contact

## Deploy

```bash
# Cloudflare Pages
npx wrangler pages deploy . --project-name=companybrain-benchmark

# Netlify
npx netlify-cli deploy --dir . --prod

# Or any static host — it's two files (index.html + styles.css + favicon.svg)
```

## Custom domain

Point `companybrain.report` (or chosen domain) at the static host. SSL handled by the host.

## What to add before public launch

- [ ] Plausible analytics (privacy-respecting; not Google)
- [ ] Real `og:image` (1200×630 PNG generated from the hero)
- [ ] Update Twitter card image
- [ ] Consider an `og:image` per scoring page (linkable per-product cards)

## What NOT to add

- ❌ Cookie banner (no cookies = no banner)
- ❌ Email capture
- ❌ Comments
- ❌ Sales-y "Get a demo" CTA — this is a methodology page, not a marketing page
