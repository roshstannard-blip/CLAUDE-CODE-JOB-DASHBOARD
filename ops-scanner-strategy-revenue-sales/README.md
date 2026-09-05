# Strategy / Revenue / Sales Ops Job Scanner

A standalone job scanner for **Strategy Operations, Revenue Operations, and Sales Operations** roles — built separately from any other job-search tooling in this account. Single self-contained HTML file, no build step, no dependencies. Open `index.html` in any browser.

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

This file is a snapshot, not a live feed. To refresh:
1. Open the file and click the live search links in each tab (they always compute against today's date).
2. Add any new roles you find as new objects in the `ROLES` array in the `<script>` block at the bottom of `index.html` — same shape as the existing entries.
3. For true daily 24-hour alerting, consider a paid job-alert API (LinkedIn Recruiter, SerpAPI Google Jobs, or Indeed's API) — that's the only way to get minute-level freshness that public search snippets can't provide.

## Fit % methodology

Graded against Rosh's Director, Strategy & Operations positioning (15+ yrs, B2B SaaS & professional services, operating cadence / GTM / RevOps / forecasting, Salesforce & Power BI/Tableau, NYC metro; open to both Director-track and individual-contributor roles) on: function match, seniority, industry fit, location/work-mode fit, and confirmed comp. 80%+ = strong structural match; 65-79% = good match with one or more open questions; below 65% = present but with a real gap (location, seniority, or scope) worth weighing before investing outreach time.
