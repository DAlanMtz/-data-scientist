# Filter Bar

## Purpose

A horizontal strip of toggle buttons that lets the viewer switch between subsets of the data shown in a heatmap, table, or chart. Each button corresponds to a category or group; clicking one updates the associated visualization without a page reload.

## When to Use

Use a filter bar when:
- A heatmap or table has too many columns to display simultaneously and grouping them by category helps focus
- The viewer's question is specific to one segment (e.g., "show me only Points families")
- The dashboard decision applies to multiple sub-populations and the viewer needs to inspect each

Do not use a filter bar when:
- Only one option would ever be selected (no value in filtering)
- The categories are not mutually exclusive or groupable — use multi-select controls instead
- The filter applies to the whole dashboard — use a dropdown or pill filter in the topbar instead

Common use cases:
- Family group filter on a stability heatmap (All | Points | Assists | Rebounds)
- Model type filter on a performance table
- Time horizon filter on a forecast grid
- Segment filter on a cohort table

## Behavior

- **Single active at a time** (default): clicking a button activates it and deactivates the previous active button.
- **All / None**: provide an "All" option as the default starting state; make it the first button.
- The associated visualization rerenders or shows/hides appropriate rows/columns when the active button changes.

## CSS Class Naming

```
.filter-bar         — flex row container
.filter-btn         — individual button
.filter-btn.active  — the currently selected button
.filter-btn:disabled— a button that is not available (no data for that group)
```

## Accessibility Rules

- Use `<button>` elements, not `<div>` or `<span>`, so keyboard navigation works natively.
- Add `aria-pressed="true"` to the active button; `aria-pressed="false"` to inactive ones.
- Update `aria-pressed` programmatically when the selection changes.
- The buttons should have clear labels — not icon-only.
- Add `aria-label` to the container describing what the filter controls.

## Visual Rules

- Active button: accent background (`var(--accent)`), white text.
- Inactive button: surface background, secondary text, border.
- Disabled button: muted text and border, `cursor: not-allowed`.
- Buttons use pill shape (high border-radius) to distinguish them from action buttons.
- Spacing: 6px gap between buttons.

## Common Mistakes

- Adding filter bars "because they might be useful" — only add filters that answer a real viewer question.
- Not updating `aria-pressed` when the selection changes.
- Using filter bars for global dashboard filters — those belong in the topbar area.
- Forgetting to set a default active state (always initialize with one button active).
- Putting filter bars above content they do not control — place them immediately above or inside the section they affect.

## Copy-Paste CSS

```css
/* ── Filter bar ────────────────────────────────────────────────────── */
.filter-bar {
  display: flex;
  gap: 6px;
  flex-wrap: wrap;
  margin-bottom: 12px;
}

.filter-btn {
  padding: 4px 14px;
  border-radius: 20px;
  border: 1px solid var(--border);
  background: var(--surface);
  color: var(--text-secondary);
  font-size: 12px;
  font-weight: 600;
  font-family: var(--font);
  cursor: pointer;
  transition: background 0.1s, color 0.1s, border-color 0.1s;
  white-space: nowrap;
}

.filter-btn:hover {
  background: var(--surface-alt);
  color: var(--text);
}

.filter-btn.active {
  background: var(--accent);
  color: #ffffff;
  border-color: var(--accent);
}

.filter-btn:disabled {
  opacity: 0.45;
  cursor: not-allowed;
}

.filter-btn:focus-visible {
  outline: 2px solid var(--accent);
  outline-offset: 2px;
}
```

## Copy-Paste HTML

```html
<div class="filter-bar" role="group" aria-label="Filter stability heatmap by family group">
  <button class="filter-btn active" data-group="all" aria-pressed="true">All families</button>
  <button class="filter-btn" data-group="points" aria-pressed="false">Points</button>
  <button class="filter-btn" data-group="assists" aria-pressed="false">Assists</button>
  <button class="filter-btn" data-group="rebounds" aria-pressed="false">Rebounds</button>
</div>

<!-- The controlled visualization: -->
<div id="heatmap-container">
  <!-- heatmap renders here -->
</div>
```

## Copy-Paste JavaScript

```javascript
/**
 * Initializes a filter bar and connects it to a render function.
 *
 * @param {string} barSelector — CSS selector for the .filter-bar element
 * @param {Function} renderFn — called with the active group value when selection changes
 */
function initFilterBar(barSelector, renderFn) {
  const bar = document.querySelector(barSelector);
  if (!bar) return;

  bar.addEventListener('click', (e) => {
    const btn = e.target.closest('.filter-btn');
    if (!btn || btn.disabled) return;

    // Update active state and aria-pressed
    bar.querySelectorAll('.filter-btn').forEach(b => {
      b.classList.remove('active');
      b.setAttribute('aria-pressed', 'false');
    });
    btn.classList.add('active');
    btn.setAttribute('aria-pressed', 'true');

    // Trigger render
    renderFn(btn.dataset.group);
  });
}

// Usage example with stability heatmap:
initFilterBar('#family-filter', (group) => {
  buildHeatmap(group); // call your heatmap render function with the selected group
});
```

## Related Parent Files

- `components/stability-heatmap.md` — the most common target of a filter bar
- `components/comparison-table.md` — can use a filter bar to toggle between benchmark approaches
