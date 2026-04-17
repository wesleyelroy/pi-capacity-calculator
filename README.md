# PI Planning — Team Capacity Calculator

A browser-based tool for calculating team capacity across sprints during SAFe PI Planning. No installation or server required — open `index.html` directly in any modern browser.

## What it does

The calculator helps Agile teams determine how many story points they can realistically commit to per sprint in a Program Increment (PI). It accounts for:

- **Part-time team members** — capacity is scaled proportionally (e.g. 4 days/week → 6.4 pts instead of 8)
- **Vacation and absence** — each day off deducts 1 point from that sprint
- **Reserved capacity** — configurable percentages for new features and bug fixes are set aside before calculating net capacity
- **SAFe roles** — Scrum Masters and Product Owners are automatically excluded from capacity

All data is saved automatically in your browser's local storage, so it persists between sessions.

---

## How to use

### Step 1 — Team composition

1. Enter a **team name** (optional).
2. For each team member, fill in:
   - **Name**
   - **Role** — Developer, Tester, Scrum Master, or Product Owner
   - **Days per week** — supports half-days (e.g. `3.5`)
3. Click **+ Toevoegen** (or press Enter) to add the member.

Scrum Masters and Product Owners are shown as "uitgesloten" (excluded) and do not count toward capacity.

### Step 2 — PI configuration

| Setting | Description |
|---|---|
| **Aantal sprints** | Number of sprints in the PI (1–12) |
| **Basisberekening** | `Nieuw team` uses 8 pts per FTE; `Historische velocity` uses a fixed average you supply |
| **Reservering nieuwe kenmerken** | % of each sprint's capacity reserved for new features |
| **Reservering bugs** | % reserved for bug fixes |

### Step 3 — Sprints & days off

Each sprint card shows:
- An editable sprint name
- Start and end date fields
- A row per capacity team member where you can enter the number of **vacation/absence days** for that sprint

The sprint's total capacity is shown in the header chip and updates live.

### Step 4 — PI Overview

A summary table shows for every sprint:

| Column | Meaning |
|---|---|
| Basis capacity | Raw team capacity before deductions |
| Aftrek | Points lost to vacation |
| Nieuwe kenmerken | Points reserved for new features |
| Bugs | Points reserved for bug fixes |
| Netto capacity | Remaining points available for stories |
| Bezetting | % of base capacity actually available (color-coded) |

The **totals row** sums across all sprints to give the full PI capacity.

---

## Capacity formula

```
Base points per member  = (days_per_week / 5) × 8
Sprint base capacity    = sum of base points for all Developers + Testers
Sprint capacity         = base capacity − vacation deductions
Net capacity            = sprint capacity × (1 − %new_features − %bugs)
```

---

## Header buttons

| Button | Action |
|---|---|
| **Reset** | Clears all data after confirmation |
| **Print / PDF** | Opens the browser print dialog; non-essential UI elements are hidden |

---

## Data storage

All data is stored in `localStorage` under the keys `pi-cap-state` and `pi-cap-nextid`. Nothing is sent to any server. Clearing browser data or using a different browser will start fresh.
