# HNG i14 — Frontend Stage 1a
## Advanced Todo Item Card

> Built upon Stage 0 · Plain HTML, CSS & JavaScript · No frameworks

---

## Live Demo

🔗 [View Live](https://d-g-r-i-d.github.io/hng-stage0-todo-card/)

## Repository

📁 [GitHub Repo](https://github.com/D-G-R-I-D/hng-stage0-todo-card)

---

## What Changed from Stage 0

### New Features Added

**1. Edit Mode**
Clicking the Edit button opens an inline form beneath the card. All core fields are editable: title, description, priority, and due date. Saving commits the changes to the card UI; cancelling restores the previous values exactly. Pressing `Escape` also cancels. Focus returns to the Edit button on close.

**2. Status Control Dropdown**
The static status display from Stage 0 has been replaced with an interactive `<select>` dropdown (`test-todo-status-control`) supporting all three allowed statuses: Pending, In Progress, and Done. The hidden `test-todo-status` span from Stage 0 is retained and kept in sync for backwards compatibility with automated tests.

**3. Priority Indicator**
A coloured left-border strip (`test-todo-priority-indicator`) has been added to the card. It visually changes colour based on priority — red for High, amber for Medium, blue for Low — and updates live when priority is changed via the edit form.

**4. Expand / Collapse**
If the task description exceeds 120 characters, the collapsible section (`test-todo-collapsible-section`) defaults to a collapsed state with a fade mask. A toggle button (`test-todo-expand-toggle`) reveals or hides the full content. Both are fully keyboard accessible.

**5. Overdue Indicator**
A dedicated overdue banner (`test-todo-overdue-indicator`) appears when the due date has passed. It includes a pulsing red dot and updates every 30 seconds alongside the time-remaining display.

**6. Granular Time Display**
Time remaining now shows granular values: `Due in 45m`, `Due in 3h 20m`, `Due in 2 days`, `Overdue by 1h`, etc. When status is Done, the display freezes at `Completed`.

**7. Status / Checkbox Sync**
All three status surfaces — checkbox, status dropdown, and the hidden status span — stay in sync at all times:
- Checking the checkbox → status becomes **Done**
- Setting dropdown to Done → checkbox becomes checked
- Unchecking after Done → status reverts to **Pending**

---

## All `data-testid` Attributes

### Carried over from Stage 0
| Attribute | Element |
|---|---|
| `test-todo-card` | `<article>` root |
| `test-todo-title` | `<h2>` task title |
| `test-todo-description` | `<p>` description |
| `test-todo-priority` | Priority badge span |
| `test-todo-due-date` | `<time>` element |
| `test-todo-time-remaining` | Time remaining span |
| `test-todo-status` | Hidden status span (synced) |
| `test-todo-complete-toggle` | `<input type="checkbox">` |
| `test-todo-tags` | `<ul>` tags list |
| `test-todo-tag-work` | Work tag `<li>` |
| `test-todo-tag-urgent` | Urgent tag `<li>` |
| `test-todo-edit-button` | Edit `<button>` |
| `test-todo-delete-button` | Delete `<button>` |

### New in Stage 1a
| Attribute | Element |
|---|---|
| `test-todo-priority-indicator` | Priority left-border strip |
| `test-todo-status-control` | Status `<select>` dropdown |
| `test-todo-edit-form` | Edit form container |
| `test-todo-edit-title-input` | Title `<input>` |
| `test-todo-edit-description-input` | Description `<textarea>` |
| `test-todo-edit-priority-select` | Priority `<select>` |
| `test-todo-edit-due-date-input` | Due date `<input type="date">` |
| `test-todo-save-button` | Save `<button>` |
| `test-todo-cancel-button` | Cancel `<button>` |
| `test-todo-expand-toggle` | Expand/collapse `<button>` |
| `test-todo-collapsible-section` | Collapsible description wrapper |
| `test-todo-overdue-indicator` | Overdue banner |

---

## Design Decisions

- **Single file** — everything lives in `index.html` per the stage requirement (plain HTML/CSS/JS, no build tools).
- **Single source of truth** — all UI is driven by a `state` object rendered through one `render()` function. No scattered DOM mutations.
- **Cancel snapshot** — on edit open, state is deep-copied into a `snap` variable. Cancel restores from snap, guaranteeing no partial mutations leak through.
- **Priority indicator as a left border strip** — chosen over a dot or icon because it gives a strong at-a-glance signal across the full card height without cluttering the badge row.
- **Collapse threshold of 120 chars** — long enough that short descriptions are never collapsed unnecessarily, short enough that the card stays compact by default.
- **30-second tick interval** — matches the lower bound of the spec requirement (30–60 s) for the most accurate live updates.
- **Fonts** — DM Serif Display (titles), Outfit (body), DM Mono (labels/badges/code). Chosen for editorial character; avoids generic AI-default font stacks.

---

## Accessibility Notes

- All form fields in the edit form have explicit `<label for="">` associations.
- Status dropdown has `aria-label="Task status"`.
- Expand toggle uses `aria-expanded` and `aria-controls` pointing to the collapsible section's `id`.
- Time remaining uses `aria-live="polite"` and `aria-atomic="true"` so screen readers announce updates without interrupting.
- Overdue indicator uses `role="alert"` and `aria-live="assertive"` for immediate announcement.
- All buttons have accessible names via visible text or `aria-label`.
- Priority and status badges carry `aria-label` describing their current value.
- Focus is returned to the Edit button when the edit form closes (save, cancel, or Escape).
- All interactive elements have visible `:focus-visible` outlines using the lime accent colour.
- Colour contrast meets WCAG AA on all text/background combinations.

### Keyboard Tab Order
`Checkbox` → `Status control` → `Expand toggle` → `Edit` → `Delete`

In edit mode: `Title input` → `Description` → `Priority` → `Due date` → `Cancel` → `Save`

---

## Known Limitations

- Tags are hard-coded (work, urgent, design). Tag editing is not part of the Stage 1a spec.
- Delete button fires a browser `alert()` as a dummy action — no persistence layer exists.
- The edit due date input uses `type="date"` which renders the native browser date picker; visual styling of the picker itself varies by browser/OS.
- No persistence — refreshing the page resets all state to defaults. LocalStorage integration is out of scope for this stage.

---

## Tech Stack

| Layer | Choice |
|---|---|
| Markup | Semantic HTML5 |
| Styling | Vanilla CSS (custom properties, no frameworks) |
| Behaviour | Vanilla JavaScript (ES2020, IIFE, no dependencies) |
| Fonts | Google Fonts (DM Serif Display, Outfit, DM Mono) |
| Hosting | GitHub Pages |

---

*HNG Internship i14 · Frontend · Stage 1a*