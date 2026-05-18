# Status Chips

## Purpose

Small inline labels that classify an entity, model, family, state, or finding into a discrete status category. Chips encode semantic meaning through color and label together — color alone is never sufficient.

## When to Use

Use chips to:
- Show the status of an item in a table row (ready, monitoring required, partial, warning, etc.)
- Label a finding category inline in a sentence or header
- Classify flags, alerts, or states in a list

Do not use chips for:
- Metric values — use metric color cells (`components/metric-color-cell.md`) instead
- Navigation or interactive filters — use the filter bar (`components/filter-bar.md`) instead
- Long text labels — chips are for 1–4 word status terms only

## Chip Vocabulary

| Class | Semantic meaning | Color |
|---|---|---|
| `chip-ready` | Validated, usable, cleared all checks | Green (positive) |
| `chip-monitor` | Usable but requires active monitoring; instability or caveat present | Amber (warning) |
| `chip-partial` | Incomplete; not fully ready; missing components or failing a check | Red (negative) with border |
| `chip-warn` | Caution required; review before use; flag present | Amber (warning) |
| `chip-danger` | Blocking risk; failed threshold; cannot proceed without resolution | Red (negative) |
| `chip-neutral` | Metadata, classification, type label; no directional signal | Grey (neutral) |
| `chip-accent` | Selected, highlighted, primary category, or the recommended option | Accent blue |

## Semantic Rules

- **`chip-ready` vs `chip-monitor`:** Both indicate the item is usable. `chip-monitor` means usable with known instability or a caveat that requires ongoing attention. `chip-ready` means clean — no active flags.
- **`chip-partial` vs `chip-danger`:** `chip-partial` means incomplete but not necessarily broken. `chip-danger` means a blocking failure that stops progression. Use `chip-partial` for "not yet ready"; use `chip-danger` for "this is wrong and must be fixed."
- **`chip-warn` vs `chip-monitor`:** `chip-warn` is a finding-level flag on a specific issue (e.g., `price_conc` warning). `chip-monitor` is an entity-level status indicating the whole item is usable-but-watched.
- **Color discipline:** Green means favorable status only. Do not use `chip-ready` for items that are merely present, populated, or passing one check. Reserve it for items that have cleared all relevant quality gates.

## CSS Class Naming

```
.chip             — base styles (all chips)
.chip-ready       — positive state
.chip-monitor     — warning state, bordered
.chip-partial     — negative state, bordered
.chip-warn        — warning state
.chip-danger      — negative state
.chip-neutral     — neutral / metadata
.chip-accent      — accent / selected
```

## Accessibility Rules

- Every chip must have a text label — color alone is not sufficient for accessibility.
- If a chip appears in a context where its meaning is not obvious from surrounding text, add a `title` attribute with the full status description.
- Do not use chips as interactive buttons unless they have `role="button"` and keyboard support.

## Common Mistakes

- Using `chip-ready` for items that are simply "present" or "populated" — reserve it for items that have passed quality gates.
- Using green chips for categories or labels that happen to be positive in context — semantic colors are for status classification, not sentiment.
- Creating new chip classes (`chip-ok`, `chip-good`, `chip-flag`) — use the vocabulary above; add a `title` attribute for specificity instead.
- Mixing chip classes with arbitrary background colors using inline styles.

## Copy-Paste CSS

```css
/* ── Status chips ──────────────────────────────────────────────────── */
.chip {
  display: inline-block;
  font-size: 11px;
  font-weight: 600;
  font-family: var(--font-mono);
  padding: 2px 8px;
  border-radius: 20px;
  white-space: nowrap;
  line-height: 1.6;
}

.chip-ready {
  background: var(--positive-bg);
  color: var(--positive);
}

.chip-monitor {
  background: var(--warning-bg);
  color: var(--warning);
  border: 1px solid var(--warning-mid);
}

.chip-partial {
  background: var(--negative-bg);
  color: var(--negative);
  border: 1px solid var(--negative-mid);
}

.chip-warn {
  background: var(--warning-bg);
  color: var(--warning);
}

.chip-danger {
  background: var(--negative-bg);
  color: var(--negative);
}

.chip-neutral {
  background: var(--neutral-bg);
  color: var(--text-secondary);
  border: 1px solid var(--neutral-border);
}

.chip-accent {
  background: var(--accent-light);
  color: var(--accent);
}
```

## Copy-Paste HTML

```html
<!-- Ready — passed all quality gates -->
<span class="chip chip-ready">ready</span>

<!-- Monitor — usable with active instability flag -->
<span class="chip chip-monitor">ready · monitor</span>

<!-- Partial — incomplete, not yet ready for use -->
<span class="chip chip-partial">partial</span>

<!-- Warn — specific flag or caution item -->
<span class="chip chip-warn">price_conc</span>
<span class="chip chip-warn">month_instability</span>

<!-- Danger — blocking issue -->
<span class="chip chip-danger">oot_weakness</span>

<!-- Neutral — metadata classification -->
<span class="chip chip-neutral">nba_model_score</span>
<span class="chip chip-neutral">classification</span>

<!-- Accent — selected or highlighted category -->
<span class="chip chip-accent">recommended</span>
```

## Using Chips in Table Cells

```html
<table>
  <thead>
    <tr>
      <th>Family</th>
      <th>Status</th>
      <th>Flags</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Points UNDER</td>
      <td><span class="chip chip-monitor">ready · monitor</span></td>
      <td style="display:flex; gap:4px; flex-wrap:wrap; padding-top:8px;">
        <span class="chip chip-warn">price_conc</span>
        <span class="chip chip-warn">month_instability</span>
      </td>
    </tr>
    <tr>
      <td>Points OVER</td>
      <td><span class="chip chip-partial">partial</span></td>
      <td style="display:flex; gap:4px; flex-wrap:wrap; padding-top:8px;">
        <span class="chip chip-warn">price_conc</span>
        <span class="chip chip-warn">month_instability</span>
        <span class="chip chip-danger">oot_weakness</span>
      </td>
    </tr>
  </tbody>
</table>
```

## Related Parent Files

- `components/metric-color-cell.md` — for metric value coloring (not status classification)
- `components/filter-bar.md` — for interactive group filters
- `../../checklists/dashboard-self-critique-checklist.md` — Design Craft dimension
