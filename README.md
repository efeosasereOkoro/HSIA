# HEOSL HSIA Commitment Platform

A single-page tool for **HEOSL** (the operating company) to track, manage and
evidence the commitments made in the **Health & Social Impact Assessment**
for the *Aferolow–Uzere New Field Development* (OML 30, Delta State, Nigeria).

It turns the HSIA report's tables into a live operations dashboard: what was
promised, who owns it, when it is due, what evidence proves it, and whether the
conditions precedent that gate drilling have been met.

**Live demo:** https://efeosasereokoro.github.io/HSIA/

> ⚠️ **MVP / demo.** Data is stored on the local device (browser), not a shared
> server, and completion is self-asserted (no independent verification step yet).
> See [ROADMAP.md](ROADMAP.md) for what is and isn't built, and why.

---

## Who it's for

The HEOSL operating team — Community Relations Manager, HSE Manager, Local
Content Officer, HCDT Board and the MD — who are accountable for delivering the
commitments and, ultimately, for defending that record to the regulator (NUPRC).

## What it does

- **Overview dashboard** — completion donut, status by category, the
  **drilling-readiness gate** (the five conditions precedent from Table 83),
  upcoming deadlines, and workload by responsible officer.
- **Commitments register** — all 22 obligations with search; filters by status,
  owner and condition-precedent; group-by-owner; an evidence gate (you must
  attach evidence before marking complete); and captured completion dates.
- **Communities** — the seven host communities ranked by composite risk, each
  with its commitments and its asks grouped by impact-vs-effort
  (quick wins / long-term planning / consider / don't do).
- **Recommendations** and **KPIs** drawn verbatim from the report.

## Data provenance

Everything is drawn from the HSIA report (Teasoo Consulting, 2026). Of the 22
tracked commitments, **14 are verbatim** from the SIMP Action Tracker (Table 73)
— including owner and required verification — and **8 are derived** from the
community-asks and mitigation tables (Tables 70–71), with owners mapped to the
SIMP governance roles (§11.2) and *suggested* verification. Each commitment is
labelled **SIMP Tracker** or **Derived** so the distinction is never lost.
Deadlines are computed from an editable, set-once programme-start date because
the report states obligations as relative timeframes.

## Tech

- A single static `index.html` — no build step, no dependencies beyond two CDN
  assets (Inter font, Tabler icons). Vanilla JS, CSS variables, light/dark themes.
- **State** persists to the artifact storage API when available, otherwise to
  `localStorage`.
- **Routing** is hash-based (`#/overview`, `#/commitments?status=over`,
  `#/communities/oleh`), so Back, bookmarks and refresh all work.
- **Deployed** via GitHub Pages from `main` (root).

## Running locally

It's a static file — open `index.html`, or serve the folder:

```bash
npx serve .
# or
python -m http.server 8000
```

## Project docs

- [ROADMAP.md](ROADMAP.md) — what's implemented, and the ideas deferred for the MVP.
