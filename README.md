# Does Money Win? — Louisiana elections

A single-page data story: how often does the candidate with the biggest campaign
war chest actually win a Louisiana election, and does it depend on the office?

Live at **https://moneywins.charliestephens.xyz**

It's one self-contained `index.html` (inline CSS/JS, hand-drawn SVG charts — no
framework, no build step) reading one small `data/la_money_wins.json`.

## Where the data comes from

`la_money_wins.json` is produced by
[`la-campaign-finance`](https://github.com/doombot50/la-campaign-finance)
(`build_money_wins.py`), which joins 25 years of Secretary of State results to
Board of Ethics fundraising. That repo regenerates it nightly. This site's
GitHub Actions workflow (`.github/workflows/deploy.yml`) pulls the freshest copy
from that repo's public raw URL on every deploy and on a daily schedule, so this
repo only carries the page plus a seed copy of the data — no manual updates.

## One-time setup

1. **Push this repo** (see the tarball's accompanying instructions, or if you're
   reading this after cloning, just `git push`).

2. **Enable Pages via Actions** — repo **Settings → Pages → Build and deployment
   → Source: GitHub Actions**. (Not "Deploy from a branch" — this repo deploys
   with the included workflow.)

3. **Point the subdomain at Pages** — add this DNS record at your `charliestephens.xyz`
   DNS provider:

   | Type  | Name / Host | Value               |
   |-------|-------------|---------------------|
   | CNAME | `moneywins` | `doombot50.github.io` |

   The `CNAME` file in this repo already tells Pages the custom domain is
   `moneywins.charliestephens.xyz`; GitHub provisions the HTTPS cert once DNS
   resolves (can take a few minutes to an hour).

That's it. Every push, plus a daily cron, redeploys with fresh data.

## Local preview

```bash
python3 -m http.server 8080   # then open http://localhost:8080
```
