# Ops Job Radar

A standalone job scanner for **Strategy Operations, Revenue Operations, and Sales Operations** roles — built separately from any other job-search tooling in this account.

**Live version (auto-refreshes daily):** https://claude.ai/code/artifact/96482e68-100c-4b30-8541-045257f53d46
**Daily scan Routine:** `trig_014uFnBTmRe3bJVP657c3qjs` (fires ~8am ET / 12:00 UTC) — re-runs the search, re-grades fit, and replaces the artifact's database contents. Manage it (pause, change time, delete) via the Claude Code Routines UI or by asking Claude to update trigger `trig_014uFnBTmRe3bJVP657c3qjs`.

`index.html` in this repo is the source file for that artifact — it also runs standalone (open it directly in a browser) but without the daily auto-refresh: without a `window.claude` runtime it just shows the 2026-09-05 seed snapshot below and the "Check Live Post Dates" button. No build step, no dependencies.

## What it does

- Runs Method #1 from the brief (boolean `site:` search across Greenhouse, Ashby, Lever, Workable, WeWorkRemotely, Remote.co, Himalayas, Wellfound, Remotive, Jobspresso, Dynamite Jobs, Remote100k) against the target role/industry keyword set.
- Organizes results into three tabs — Last 24 Hours, Last 3 Days, Last 7 Days (cumulative) — plus a fourth "All Verified Matches" tab for real, currently-live roles whose exact post date couldn't be confirmed (see Limitations below).
- Each row: role, company, location, work mode (remote/hybrid), salary range (or "Not listed"), industry, source, direct job posting link, company careers-page link, likely hiring manager (only when publicly sourced), 2026 employee-review signal (Glassdoor, only when found), and a fit % graded against Rosh's resume.
- Dropdown filters: state/location, salary band, industry, work mode. Free-text search box for company/title.
- Each time-window tab includes **live, clickable Google search links** (one per source site) that auto-compute the correct date range off today's date — `tbs=qdr:d` for 24h, a custom `cdr` range for 3 days, `tbs=qdr:w` for 7 days. These are the real way to catch same-day postings; re-click them each time you open the file.

## Limitations — read before trusting a date

Google/Bing search snippets do not reliably expose "posted X hours/days ago" for ATS-hosted postings (Greenhouse, Ashby, Lever, Workable) — that data lives only inside each board's own live UI, which this environment cannot directly fetch (egress to those domains is blocked at the network level in this session). Of the 34 roles in the 2026-09-05 snapshot, exactly **one** (Nooks) had a source-confirmed post-date inside 7 days. Everything else is a verified, currently-live posting placed in the "All Verified Matches" tab rather than guessed into a time bucket.

**No field is fabricated.** Hiring manager names and employee-review scores appear only where a public source confirmed them; every other cell says "Not publicly confirmed" or "Not pulled this pass" rather than inventing an answer.

## Refreshing

**On the live artifact, this is now automatic.** The daily Routine re-runs the full search every morning and rewrites the artifact's database; the page reads from that database live (via the `db` capability) and updates for every viewer without anyone touching the file. The banner at the top of the page shows the last scan time and board-coverage count, and flags itself if the daily job runs more than ~30 hours late.

On top of that automatic layer, two manual options remain:
1. Click **"Check Live Post Dates"** at the top of the page. This calls Greenhouse's, Lever's, and Ashby's public, CORS-enabled job-board APIs directly from your browser — the same read-only endpoints those companies use to embed their own job boards on their career pages — and pulls a real post/update timestamp for roles hosted on those three ATS platforms, re-sorting them into the correct 24h/3-day/7-day tab. Roles it can't confirm keep their "not publicly confirmed" status rather than showing a guess.
2. For the aggregator-sourced roles (Wellfound, Himalayas, Remotive, WeWorkRemotely, Dynamite Jobs, Remote100k, Workable — no public API), use the live search links in each tab; they always compute against today's date.

For true sub-day alerting across *all* sources (including the aggregators), a paid job-alert API (LinkedIn Recruiter, SerpAPI Google Jobs, or Indeed's API) is still the only option the daily Routine doesn't close.

If you open `index.html` as a plain local file (not the published artifact), there is no `window.claude` runtime, so it falls back to the 2026-09-05 seed data baked into the `SEED_ROLES` array in the `<script>` block — edit that array directly if you want to hand-maintain a local copy.

## Fit % methodology

Graded against Rosh's Director, Strategy & Operations positioning (15+ yrs, B2B SaaS & professional services, operating cadence / GTM / RevOps / forecasting, Salesforce & Power BI/Tableau, NYC metro; open to both Director-track and individual-contributor roles) on: function match, seniority, industry fit, location/work-mode fit, and confirmed comp. 80%+ = strong structural match; 65-79% = good match with one or more open questions; below 65% = present but with a real gap (location, seniority, or scope) worth weighing before investing outreach time.
