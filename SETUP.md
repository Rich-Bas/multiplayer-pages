# Multiplayer — bydefault + defaultdiagnostic hosting (GitHub Pages + Webflow iframe)

Two self-contained static pages hosted on GitHub Pages, embedded into Webflow at
`multiplayer.studio/bydefault` and `multiplayer.studio/defaultdiagnostic`
via auto-resizing iframes. Each page has its own nav/footer/styles built in —
nothing is shared with the Webflow site.

## What's in here
- `index.html` — landing page (served at /bydefault)
- `default-diagnostic.html` — lead-gen tool (served at /defaultdiagnostic)
- `assets/` — all images (relative paths, resolve automatically on Pages)
- `.nojekyll` — stops GitHub Pages running Jekyll on the folder
- `README.md` — Shane's original handoff note
- `webflow-embed-bydefault.html` — paste into the Webflow /bydefault page
- `webflow-embed-defaultdiagnostic.html` — paste into the Webflow /defaultdiagnostic page

Both source files have a small height-reporter script injected before `</body>`
so the Webflow iframe auto-sizes to content (no fixed-height guessing, no inner
scrollbar).

## Steps (~15 min)

### 1. Create the repo + push
- New PUBLIC GitHub repo (Pages on the free tier needs public).
- Push everything in this folder to the default branch.

### 2. Enable GitHub Pages
- Repo → Settings → Pages.
- Source: "Deploy from a branch", branch = default branch, folder = `/ (root)`.
- Save, wait ~1 min, then confirm both URLs load directly AND images render:
  - `https://USERNAME.github.io/REPO/index.html`
  - `https://USERNAME.github.io/REPO/default-diagnostic.html`
- This is the key checkpoint. If these load cleanly, the embeds will work.

### 3. Drop your repo details into the embeds
In BOTH `webflow-embed-*.html`, replace:
- `__USER__` → your GitHub username
- `__REPO__` → your repo name

### 4. Webflow
- Create a BLANK page, slug `bydefault`. Add only an Embed element. Paste the
  contents of `webflow-embed-bydefault.html`. Delete any default Webflow
  sections so the iframe is the only thing on the page. Save.
- Create a BLANK page, slug `defaultdiagnostic`. Add only an Embed element.
  Paste `webflow-embed-defaultdiagnostic.html`. Save.
- Publish.

### 5. Verify (staging .webflow.io first, then production)
- Both pages scroll naturally; iframe grows to full content height (no inner
  scrollbar, no cut-off).
- Diagnostic runs to the end and the mailto: opens with prefilled subject/body
  (CONTACT_EMAIL is already set to hello@multiplayer.studio).

## Known post-launch polish (not blockers)
- **Cross-page button:** the landing page's "Start the default audit" button
  links to default-diagnostic.html relatively, so inside the iframe it loads the
  diagnostic on the *Pages* origin rather than flipping the parent URL to
  multiplayer.studio/defaultdiagnostic. Works fine; just doesn't change the
  pretty URL. Decided to leave for post-launch.
- **In-page anchors aren't shareable:** nav buttons scroll correctly inside the
  frame, but multiplayer.studio/bydefault#section won't deep-link (the hash
  doesn't reach into the iframe). Fixable later if needed.
- **SEO:** iframe content isn't indexed against the Webflow page URL. Fine for a
  lead-gen tool; revisit only if /bydefault must rank organically.
- **Footer placeholders:** Cookies/Legal/Careers are href="#"; LinkedIn icon
  points to a generic URL. Cosmetic — point at real URLs when convenient.
