# MooseAI Website Maintenance Guide

This document maintains the public website for MooseAI, LLC. It belongs with the website repository and deliberately contains no OpenLifeSpan application-development instructions.

## Repository and live site

- Repository: `https://github.com/chiesennegs/mooseaillc.com`
- Production site: `https://mooseaillc.com`
- Hosting: GitHub Pages, deployed from the repository's `main` branch and root directory.

The site is a static, dependency-free page. Pushing a commit to `main` triggers GitHub Pages to publish it. Allow a few minutes for a normal Pages deployment and browser/CDN cache refresh.

## Files

| File | Purpose |
| --- | --- |
| `index.html` | Page content, project cards, links, metadata, and accessible image text. |
| `styles.css` | Site layout, color tokens, responsive rules, project-card styling. |
| `assets/mooseai-logo.png` | Current transparent MooseAI brand mark. |
| `assets/openlifespan-mark.png` | OpenLifeSpan project mark used on its card. |
| `CNAME` | Custom domain declaration: `mooseaillc.com`. Keep this file at the repository root. |
| `.nojekyll` | Prevents GitHub Pages from processing the site with Jekyll. Keep it unless the hosting approach intentionally changes. |

## Brand assets

Use `assets/mooseai-logo.png` anywhere the MooseAI organization mark is required. It is a transparent PNG. Replace the file in place when brand artwork changes so existing markup continues to work.

Avoid editing or reusing an app-specific image when adding a new organization-wide logo. Project artwork belongs in a clearly named file under `assets/` and should have meaningful `alt` text when it conveys content.

## Adding or updating a project

Projects are cards inside the `#projects` section of `index.html`.

1. Copy the existing `<article class="project-card">` pattern.
2. Add a concise name, one-sentence plain-language description, and a canonical public link.
3. Use a supplied project mark in `assets/` where one exists; otherwise use a simple CSS mark, as PlexExplorer does.
4. Preserve the `View on GitHub` link style and add a non-link "coming soon" item only for a known future destination (for example, Google Play).
5. Do not claim uploads, integrations, releases, or availability that do not yet exist.

The selector `#projects .project-card + .project-card` provides the vertical gap between adjacent project cards. Keep new cards within the same section so spacing remains consistent.

## Editing site content

- Keep the site sparse, direct, and human-readable.
- Maintain the local-first/privacy language for projects only where it is accurate.
- Update `<meta name="description">` and the visible content together when the organization positioning changes.
- Use absolute `https://` URLs for off-site links and `mailto:support@mooseaillc.com` for support contact.
- Do not put private credentials, mailbox configuration, API keys, or DNS secrets in this repository.

## Previewing locally

Because the site has no build step, open `index.html` directly in a browser for a quick visual check. For a closer HTTP-server preview, run this from the repository root:

```bash
python3 -m http.server 8080
```

Then visit `http://localhost:8080`. Stop the preview with `Ctrl-C`.

Check desktop and narrow/mobile widths after changes. In particular, verify that project cards retain spacing, images do not crop, links work, and contrast remains readable against the dark background.

## Deploying

```bash
git status
git add index.html styles.css assets/ README.md CNAME .nojekyll
git commit -m "Describe the website change"
git push origin main
```

Before committing, use `git diff --check` and review the diff. Do not stage unrelated files. After pushing, GitHub Pages deploys automatically from `main`.

## Domain and DNS context

GitHub Pages maps the custom domain using the `CNAME` file and its GitHub Pages configuration. The root domain uses GitHub Pages A records, and `www` is configured as a CNAME to the GitHub Pages user site. Website DNS records must remain separate from mail records (MX, SPF, DKIM, and DMARC) managed for the domain.

If HTTPS is temporarily unavailable after a DNS or domain change, wait for DNS propagation and GitHub Pages certificate issuance before enabling or re-enabling HTTPS enforcement in the repository's Pages settings.

## Maintenance checklist

- Confirm `git status` is clean before and after each change.
- Verify repository links point to the intended public repositories.
- Preview visual changes at desktop and mobile widths.
- Preserve `CNAME` and `.nojekyll`.
- Push only reviewed changes to `main`.
- Check the public site after GitHub Pages deploys.
