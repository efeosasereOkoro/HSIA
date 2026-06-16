# Roadmap & Decision Log

A living record of what we've built and the ideas we deliberately set aside for
the MVP. **Keep this updated** as features land or decisions change.

_Last updated: 2026-06-16_

---

## ✅ Implemented

### Structure & navigation
- App shell: persistent left **sidebar** + sticky **topbar**, wide content area.
- Six sections: **Overview**, **Commitments**, **Communities**,
  **Recommendations**, **KPIs**, **Help**.
- **Help page** — plain-language how-to: 4-step quick start, what each section
  does (clickable cards), status legend, conditions-precedent explainer,
  data-provenance guide, and saving/theme/links notes.
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
- **Community asks are now trackable** — each ask has the same checkbox +
  evidence-gate + completion-date flow as commitments (mark *Addressed* once
  evidence is attached). Tracked independently of commitments.

### Data integrity
- **Set-once programme-start date** — locked by default, changed via an explicit
  Adjust → Set flow with a "set on …" provenance stamp (so status can't be
  quietly edited green).
- **Verified against the report (2026-06-16).** Communities (Table 69), all 14
  SIMP-Tracker commitments (Table 73), the 8 derived commitments (Tables 70–71),
  all 11 KPIs (Table 74) and the recommendations (§16.3–16.6) reconcile with the
  source. Fixes applied: borehole targets trimmed to Eriemu + Emeragha (Table 73);
  the Oleh health-centre ask flagged mandatory (Table 70 `[MANDATORY]`); SEA/SH
  "(pre-drilling)" qualifier removed for consistency with the chosen CP source.
- **Decision — conditions precedent source.** The report contradicts itself:
  Table 83/§16.2 names the public-health investigation as the 5th CP; §1.6 and
  Table 73's red rows name the SEA/SH action plan instead. **We follow Table 83**
  (the explicit "Mandatory Conditions Precedent" table); a note in the footer
  discloses the discrepancy. Revisit if Teasoo issues a corrected report.

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

## 🧭 Backlog — prioritised

Everything we've discussed but not yet built, ordered by priority.

**Legend:** effort `S` (hours) · `M` (a day or two) · `L` (multi-day) — `⛓ backend`
marks items that need a server / identity and so cannot ship in the single file.

**How we prioritised:** (1) what most strengthens the HEOSL stakeholder demo and
makes the tool *cover the SIMP*, and is buildable in-file → (2) operator utility,
in-file → (3) structural "system-of-record" work that needs a backend →
(4) the wider programme and polish.

### P0 — Next up (high value, in-file, no backend)
- **Quarterly SIMP Action Tracker export (print / PDF).** `M` One click →
  a regulator-ready report: every commitment's status, owner, evidence,
  completion date, the CP gate and the KPI scorecard. The report (§16.6, Table 75)
  calls for exactly this as a quarterly licence deliverable — turns the tool from
  a tracker into the artefact NUPRC wants. Most persuasive single demo feature.
- **Sample-data toggle.** `S` A "load example progress" switch so demos show a
  healthy programme (evidence attached, items complete, gate cleared) instead of
  the empty 0% / all-red first-run state.
- **Grievance (GRM) log.** `M` Log → assign → resolve, with the >30-day-unresolved
  flag. The GRM is a first-class SIMP element (Table 72 CR-Manager duty, Table 80
  escalation pathway, and a dedicated KPI) and is currently absent — this makes
  the platform cover the SIMP, not just the commitment list.

### P1 — High value, in-file
- **Live KPIs + adaptive thresholds.** `M` Log dated readings per indicator with
  a simple trend; surface Table 81's adaptive-management thresholds that trigger
  action. The one *monitoring* section that currently doesn't monitor.
- **Timeline / sequencing view.** `M` CPs and Year-1 deadlines on a horizontal
  timeline anchored to the start date — turns the register into a plan and shows
  bottlenecks/clustering at a glance.
- **"My commitments" by-owner landing.** `S` Each officer (CR Manager, HSE, Local
  Content, HCDT, MD) sees their own list first.
- **Budget framework view.** `M` The ≥3%-of-opex commitment and prioritised cost
  categories (§11.6, Table 76), tied to commitments.
- **Evidence attachment.** `S` A filename/link field on evidence — a step closer
  to real verification artefacts (full upload needs a backend).

### P2 — System-of-record (⛓ backend / identity; post-demo)
- **Shared backend + authentication + roles.** `L ⛓` A real shared source of
  truth — today every officer has a device-local copy. Unblocks most of the rest.
- **Independent verification tier.** `M ⛓` Distinguish "HEOSL claims complete"
  from "independently / community verified"; capture verifier identity + date;
  lock verified records. (Deliberately deferred for the first demo.)
- **Audit trail / change history.** `M ⛓` Who changed what, when — beyond the
  single completion date.
- **Deadline reminders / escalation.** `M ⛓` Notify owners as dates approach; an
  escalation path when a condition precedent goes overdue.

### P3 — Wider programme & polish
- **Community-facing accountability scorecard.** `L` A localised, low-bandwidth /
  printable "what was promised to your community, and the status" surface that
  actually reaches a town hall. (Separate audience from the HEOSL-internal tool.)
- **Public grievance / feedback loop.** `L ⛓` Extends the P0 GRM log so
  communities can confirm, dispute or raise issues against a commitment.
- **Recommendations → commitments linking.** `S` Thread each §16 recommendation
  to the commitments that fulfil it.
- **Saved / named register filter views.** `S`
- **Per-change timestamps surfaced in the UI.** `S`
- **"What's overdue this week" digest.** `S`

---

## How to use this doc

When something moves from idea → built, cut it from the **Backlog** and add it
under **Implemented** with a one-line note; bump the next P0 item up. Update the
_Last updated_ date. If a decision is reversed (e.g. we decide to add a backend),
record the new direction here so the rationale isn't lost.
