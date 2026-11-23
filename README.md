# expo.gaubase.org

Website for the Expo, **10–12 April 2027**, SGCCI Sarsana (SIECC), Surat.

Right now this repo holds a "coming soon" placeholder. The expo committee's
technical team will build the full site here.

## How it goes live

- The site files are in [`site/`](site/). `site/index.html` is the home page.
- Every push or merged pull request to **`master`** runs
  [`.github/workflows/deploy.yml`](.github/workflows/deploy.yml), which publishes
  `site/` to GitHub Pages at **https://expo.gaubase.org**, usually within 1–2 minutes.
- Progress and errors show in the **Actions** tab.
- There are no secrets or tokens to manage.

### Using a framework or build step

If you use a static site generator or framework (Astro, Vite/React, Next.js
`output: "export"`, Hugo, etc.), edit `deploy.yml`:

1. Add `actions/setup-node` plus your install and build commands before `upload-pages-artifact`.
2. Change `path: site` to your build output folder (`dist`, `out`, `public`, ...).

GitHub Pages serves static files only, so there is no server-side code or database.
Forms and registrations need an external service or API.

## Custom domain

- DNS for `gaubase.org` is managed by GauBase on Cloudflare:
  `expo` → CNAME → `<repo-owner>.github.io` (DNS only, not proxied).
- The custom domain is set in **Settings → Pages → Custom domain** = `expo.gaubase.org`,
  with **Enforce HTTPS** on.

## Handover checklist (GauBase → expo technical team)

1. Transfer the repo: **Settings → General → Danger Zone → Transfer ownership**
   to the team's GitHub account or organization. Issues, PRs and Actions move with it,
   and the old URL redirects.
2. The new owner re-enters `expo.gaubase.org` in **Settings → Pages → Custom domain**
   if it was cleared, and turns on Enforce HTTPS.
3. GauBase updates the Cloudflare DNS record `expo` to point at `<new-owner>.github.io`.
4. Optional: the new owner verifies `gaubase.org` under their account/org Pages
   settings (GauBase adds the TXT record they are given) so no other account can claim the domain.
5. Optional: protect `master` (Settings → Branches) so changes land only via reviewed pull requests.
