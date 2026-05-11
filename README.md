# pursuingtruth.faith

Source for <https://pursuingtruth.faith/>. A friend's notebook of reasons —
classical arguments, the historical case for Christianity, philosophy of
religion, and the scientific evidence that doesn't always make the news.

## Stack

Built with [juicer](https://github.com/edadma/juicer), the Scala SSG, and
themed with `juicerdocs` (vendored under `themes/juicerdocs/` so this repo
stays self-contained). Math via KaTeX; opt-in per-site.

## Layout

```
pursuingtruth.faith/
├── content/                # markdown content (.md files + section indexes)
├── static/                 # CSS, images, etc. served at the URL root
├── themes/juicerdocs/      # vendored theme — edit freely
├── site.toml               # site config, palette, [juicerdocs] options
└── .github/workflows/      # CI: build & deploy on push to `stable`
```

## Local preview

This repo expects the [juicer](https://github.com/edadma/juicer) repo to live
as a sibling directory (e.g. `~/dev/juicer/` alongside `~/dev/pursuingtruth.faith/`).
From the juicer repo:

```bash
sbt 'juicerJVM/run serve -s ../pursuingtruth.faith -L'
```

The `-L` flag enables live reload — edits rebuild automatically and connected
browser tabs reload via SSE.

## Build (production-equivalent)

```bash
sbt 'juicerJVM/run build -s ../pursuingtruth.faith -d ../pursuingtruth.faith/_site -b https://pursuingtruth.faith/'
```

## Deploy

Push to the `stable` branch. `.github/workflows/deploy.yml` builds the site,
writes a `CNAME` for the custom domain, and publishes to GitHub Pages.

One-time setup on GitHub:

1. **Settings → Pages →** *Source* = "GitHub Actions"
2. **Custom domain** = `pursuingtruth.faith` (creates `_pages-cf` health check)
3. **DNS** on the registrar — either four A records to GitHub Pages, or a
   CNAME at `www` pointing at `edadma.github.io`:
   - `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
4. **HTTPS** — wait for Pages to issue a Let's Encrypt cert (a few minutes
   after DNS propagates), then tick "Enforce HTTPS".

## License

Content © Ed Maxedon. Theme adapted from juicer's `juicerdocs` (MIT).
