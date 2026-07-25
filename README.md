# Security Translated — Hub Site

Single-file static site for [securitytranslated.substack.com](https://securitytranslated.substack.com).
Pages: Home · Pillars & Domains · Articles (RSS) · Products (funnels + full catalog) · Freebies · Portfolio.

Everything lives in `index.html`. No build step, no dependencies. Dark blue & gold brand theme.

## One-time setup

1. Push this repo to GitHub (repo name: `security-translated-site` or your pick).
2. Repo → **Settings → Pages** → Source: *Deploy from a branch* → Branch: `main`, folder `/ (root)`.
3. Site is live at `https://<username>.github.io/<repo>/` about a minute later.

`.nojekyll` is included so GitHub Pages serves the file as-is.

## Before launch: swap the placeholder links

All real URLs live in ONE config block near the top of the `<script>` in `index.html`
(look for the `CONFIG` banner comment):

| Key | Replace with |
|---|---|
| `STORE` | Your Lemon Squeezy storefront URL |
| `playbook` | Checkout URL for The Security Leader's Playbook (keep `?embed=1`) |
| `detection` | Checkout URL for the Detection-as-Code Playbook (keep `?embed=1`) |
| `boardTemplate` | Subscriber-only Substack post with the Board Briefing Template attached |
| `detectionChecklist` | Subscriber-only post with the Detection Pipeline Checklist |
| `phraseSlice` | Subscriber-only post with the phrase-translation free slice |

The subscriber-only posts ARE the email gate: Substack collects the email, then unlocks the PDF.

## Updating the site with Claude

The update loop:

1. Open a Claude chat in the Security Translated project.
2. Say what to change, and paste a GitHub token so Claude can push.
3. Claude clones, edits, commits, pushes. Pages redeploys automatically (~1 min).

Token rules (blast-radius control):

- **Fine-grained** personal access token only (GitHub → Settings → Developer settings → Fine-grained tokens)
- Scoped to **this repo only**
- Permission: **Contents: Read and write**. Nothing else
- Short expiry (90 days max). Revoke and reissue rather than extending

Claude's environment resets between conversations; the token is never stored, so paste it
each session. Worst case with this scoping is defacement of one static site: revoke the
token, re-push, done.

## Notes

- The Articles page pulls the Substack RSS feed through a public CORS proxy
  (`api.allorigins.win`, fallback `corsproxy.io`). If both are down, it degrades to a
  link to the Substack archive. For zero third-party dependency later: a Cloudflare
  Worker that proxies `/feed` is ~10 lines.
- Custom domain later: add the domain in Settings → Pages, create the CNAME record at
  your DNS, done. Or front the repo with Cloudflare Pages for nicer redirects.

© Security Translated. Site content free to share with attribution; not for resale.
