# Multiplayer — website handoff

Static site. No build step, no dependencies, no server-side code. Just upload the files as-is.

## Contents

```
index.html                 Landing page ("Built by design. Not by default.")
default-diagnostic.html    The Default Audit interactive tool
assets/                    Images and SVGs used by both pages
README.md                  This file
```

## How to publish

Upload the entire folder (keeping the structure intact) to the web root of the
Multiplayer domain. The pages use relative paths, so the `assets/` folder must
sit alongside the two HTML files.

- `index.html` should be served at the site root (e.g. `https://multiplayer.studio/`).
- `default-diagnostic.html` is linked from the landing page's "Start the default
  audit" button and from the audit nav logo. It can live at the root next to
  `index.html`, or you can route it to a friendlier URL such as `/default-audit`
  (if you do, update the two links noted below).

Works on any static host (Netlify, Vercel, S3/CloudFront, Cloudflare Pages,
nginx, Apache, GitHub Pages). No environment variables or secrets.

## Fonts

Anton and Inter load from Google Fonts via `<link>` tags in each file's `<head>`.
If you prefer to self-host the fonts for performance or privacy, swap those tags
for local `@font-face` declarations. No other change needed.

## Things you will likely want to wire up

1. **Contact destination.** Both pages currently send to `hello@multiplayer.studio`
   via `mailto:` links (the homepage "Book a call" / "Let's chat", and the audit's
   send/book buttons). In `default-diagnostic.html` this is the `CONTACT_EMAIL`
   constant near the top of the `<script>`. To capture submissions in a CRM or
   form backend instead of opening the user's mail client, replace the `mailto:`
   handling in `submitConnect()` (and the homepage links) with a POST to your
   endpoint.

2. **Footer + nav links.** Cookies / Legal / Careers in the homepage footer are
   placeholders (`href="#"`). The LinkedIn icon points to `https://www.linkedin.com`.
   Point these at the real URLs.

3. **Diagnostic page URL.** If you rename or reroute `default-diagnostic.html`,
   update the link in `index.html` (the "Start the default audit" button) and the
   logo link inside `default-diagnostic.html` (which points back to `index.html`).

## Notes

- The diagnostic runs entirely in the browser. Answers stay client-side until the
  user chooses to send them; nothing is stored or transmitted automatically.
- Motion (scroll reveals, parallax, the stat count-up) is progressive enhancement
  and respects the user's "reduce motion" OS setting.
- Tested responsive down to ~360px wide.
