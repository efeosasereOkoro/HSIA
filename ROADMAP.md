# Roadmap & Decision Log

A living record of what we've built and the ideas we deliberately set aside for
the MVP. **Keep this updated** as features land or decisions change.

_Last updated: 2026-06-16_

---

## ✅ Implemented

### Structure & navigation
- App shell: persistent left **sidebar** + sticky **topbar**, wide content area.
- Five sections: **Overview**, **Commitments**, **Communities**,
  **Recommendations**, **KPIs**.
- **Hash routing** — `#/overview`, `#/commitments?status=…&owner=…`,
  `#/communities/<id>`. Back button, bookmarks and refresh preserve the view
  and the active register filters.

### Overview dashboard
- **Hero-led layout** (decluttered 2026-06-16): the two consequence-carrying
  things lead the page — **Drilling readiness** (the five conditions precedent
  from Table 83 as a cleared / not-cleared gate, with per-CP status) and
  **Overdue** (count + the actual past-due list, or an "all on schedule" state).
- Then **Completion donut** (SVG, status legend) + **Upcoming deadlines** feed.
- **Communities** (priority-tier progress) and a slim **KPI link** strip.
- Dismissible first-run "Getting started" hint.
- _Moved to the Commitments page_ to reduce crowding: **Commitments by category**
  and **Workload by responsible officer** breakdowns (they're analysis, and
  belong where you act on them). The 4 stat tiles were folded into the hero/donut.

### Commitments register
- Master list of all 22 commitments.
- Search; filters by status, owner, condition-precedent; group-by-owner.
- Top-of-page breakdowns: **Workload by officer** and **By category** (moved
  here from the Overview).
- **Evidence gate** — a commitment can't be ticked complete until verification
  evidence is attached (mirrors the SIMP Tracker's evidence requirement).
- Captured **completion date** shown on completed items.
- **Provenance tags** — SIMP Tracker (verbatim) vs Derived, with table refs.

### Communities
- Seven communities ranked by composite risk (WASH, disease, vulnerability,
  livelihood); per-community progress ring and commitments.
- Community asks grouped by **impact-vs-effort quadrant**: Quick wins /
  Long-term planning / Consider / Don't do (replaced the scatter matrix).

### Data integrity
- **Set-once programme-start date** — locked by default, changed via an explicit
  Adjust → Set flow with a "set on …" provenance stamp (so status can't be
  quietly edited green).

### Craft
- **Teasoo Consulting palette** (deep navy / steel-blue with a crimson accent),
  Inter typography, light + dark themes, elevation/shadow system.
- **Persistence** — artifact storage when available, else `localStorage`.
- **Accessibility** — semantic headings, `aria-current` nav, donut `aria-label`,
  decorative bars hidden, global focus-visible styles.
- **Responsive** — verified laptop / tablet / phone: sidebar collapses to a
  horizontal bar (full labels on tablet, icon-only ≤760px with labels kept for
  screen readers), 12-col dashboard stacks, no horizontal overflow at any width.

---

## 🧭 Deferred — ideas we discussed but did NOT build for the MVP

Grouped roughly by how much they change the product. Each notes *why* it was held.

### Trust & verification (highest value, deferred on purpose)
- **Independent verification tier.** Distinguish "HEOSL claims complete" from
  "independently / community verified"; capture verifier identity + date; lock
  verified records. _Why deferred:_ explicitly out of scope for the first demo;
  self-attestation is acceptable to show the flow, not to be the system of record.
- **Audit trail / change history.** Who changed what, when (beyond a single
  completion date). _Why deferred:_ needs identity + a backend to be meaningful.

### Multi-user / system-of-record
- **Shared backend + authentication + roles.** Today every officer has their own
  device-local copy — there is no shared source of truth. _Why deferred:_ needs a
  server; the `localStorage` fallback makes the demo persist, but per-device only.
- **Regulator (NUPRC) view** and **export** — generate the quarterly SIMP Action
  Tracker / a defensible PDF snapshot. _Why deferred:_ depends on the backend and
  the verification tier landing first.

### Monitoring & outcomes
- **Live KPIs.** Let users log dated readings against each indicator and show a
  trend, instead of static baseline → target cards. _Why deferred:_ a feature
  build, and over-scoped for a first demo; targets are also stated as text.
- **Deadline reminders / escalation.** Notify owners as dates approach; an
  escalation path when a condition precedent goes overdue. _Why deferred:_ needs
  notifications infrastructure (and identity).

### Service design (the wider programme, beyond HEOSL's internal tool)
- **Community-facing accountability view** — a localised, low-bandwidth or
  printable scorecard ("here's what was promised to Oleh, and the status") that
  actually reaches a town hall. _Why deferred:_ a separate audience and surface;
  the current tool is HEOSL-internal.
- **Grievance / feedback loop** — a way for communities to confirm, dispute or
  raise an issue against a commitment. _Why deferred:_ needs the public surface
  and a backend.
- **Recommendations → commitments linking** — thread each general recommendation
  to the commitments that fulfil it. _Why deferred:_ content-modelling work, low
  ROI for the demo.

### Smaller polish ideas
- Per-change timestamps surfaced in the UI.
- Saved/named register filter views.
- A compact "what's overdue this week" digest.

---

## How to use this doc

When something moves from idea → built, cut it from **Deferred** and add it under
**Implemented** with a one-line note. Update the _Last updated_ date. If a
decision is reversed (e.g. we decide to add a backend), record the new direction
here so the rationale isn't lost.
