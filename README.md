
# Helpdesk Performance Dashboard (7 visuals) — with **Ticket Status** filter

This dashboard auto‑reads `tickets.json`, refreshes every 30 seconds, and now includes a **Ticket Status** multi‑select (maps to `CurrentStatus`).

## Deploy on GitHub Pages
1) Create/open a repo and commit these files to **main**:
   - `index.html`, `tickets.json` (array at root), `.nojekyll`, `.github/workflows/pages.yml`
2) The workflow auto‑publishes to Pages; see **Settings → Pages** for the URL.

### Why these implementation choices?
- **Plotly CDN pin (v3.4.0)** — Plotly advises using an explicit version; `plotly-latest.min.js` is *frozen* at v1.58.5 and not updated for v2+/v3+. (See Plotly’s getting‑started page and the GitHub issue note.)
- **Relative fetch with URL()** — `new URL('./tickets.json', location.href)` resolves correctly under project pages like `/yourrepo/…` and is the MDN‑documented way to resolve relative references.

## Data fields referenced
`Ticketid, Customername, ProjectName, CurrentStatus, NewgenSeverity, Subject, ReportingTime, FirstResponseTime, ClosingDate, UserEnvironmentType, Support_Scope, Newgen Issue Sub Category, Problem Type (Newgen), Problem Type (Customer), Response_TicketSLAMet, Resolution_TicketSLAMet, AssigntoUserName`.

## Quick checks
- Open `…/<repo>/tickets.json` — should show raw JSON `[ ... ]`.
- Hard‑reload after deploy; the app adds `?ts=<timestamp>` and `{cache:'no-store'}` to avoid stale caches.
