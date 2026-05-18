# Collapsible Appendix

## Purpose

A `<details>` / `<summary>` block that hides diagnostic, raw, or verbose content behind a click. The primary dashboard stays decision-led; the appendix preserves transparency and reproducibility without overwhelming the viewer.

## When to Use

Move content to the appendix when:
- A table has more than 15 rows and the viewer does not need to read every row to act on the dashboard decision
- The content is diagnostic or methodological rather than decision-relevant
- The information is important for reproducibility and auditability but not for the primary finding
- The section would push decision-relevant content below the fold

Common appendix candidates:
- Raw data tables (before aggregation)
- Feature coverage or availability tables
- Correlation / mutual information diagnostics
- Stability checks at a grain finer than the primary heatmap
- Model assumptions, exclusion rules, methodology notes
- Concentration diagnostics
- Long caveat or limitation lists

Content that must **not** go in the appendix:
- The supported decision and verdict
- Primary KPIs
- The chart or table the recommendation is based on
- Metric definitions — these belong in the visible footer or data contract

## Structure

```html
<details class="appendix">
  <summary>[Title of collapsed section]</summary>
  <div class="appendix-body">
    [content]
  </div>
</details>
```

The `<summary>` text should be descriptive enough for a viewer to know whether to open it. Prefix with a category if helpful: "Diagnostics — Feature Coverage" rather than just "Feature Coverage".

## Visual Rules

- Collapsed by default — `<details>` without the `open` attribute.
- Summary line: 13px, weight 600, `var(--text-secondary)`. Includes a rotating arrow indicator.
- Body: top border separates it from the summary; standard padding.
- Stack multiple appendix sections below the main content with a consistent visual weight — they should read as supplementary, not as navigation.

## Accessibility Rules

- `<details>` and `<summary>` are natively accessible — they support keyboard interaction and screen reader disclosure.
- The `<summary>` text should fully describe the section without relying on context from the surrounding page.
- Do not use `<details>` for content that must always be visible.
- Do not nest `<details>` more than one level deep.

## Common Mistakes

- Putting decision-critical content in the appendix to make the dashboard "cleaner" — if the viewer needs it to act, it belongs in the main view.
- Leaving the appendix open (`<details open>`) by default — this defeats the progressive disclosure purpose.
- Writing the summary text as a chart type ("Monthly table") instead of a description ("Monthly stability — all rows by period and group").
- Putting the metric definitions or data contract in the appendix — these must be visible (usually in the footer).

## Copy-Paste CSS

```css
/* ── Collapsible appendix ──────────────────────────────────────────── */
details.appendix {
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: var(--radius);
  margin-bottom: 10px;
  box-shadow: var(--shadow);
}

details.appendix summary {
  padding: 14px 18px;
  cursor: pointer;
  font-size: 13px;
  font-weight: 600;
  color: var(--text-secondary);
  list-style: none;
  display: flex;
  align-items: center;
  gap: 8px;
  user-select: none;
}

/* Remove default disclosure triangle */
details.appendix summary::-webkit-details-marker { display: none; }
details.appendix summary::marker { display: none; }

/* Custom indicator */
details.appendix summary::before {
  content: "▶";
  font-size: 10px;
  color: var(--text-muted);
  transition: transform 0.15s ease;
  flex-shrink: 0;
}

details.appendix[open] summary::before {
  transform: rotate(90deg);
}

details.appendix .appendix-body {
  padding: 0 18px 18px;
  border-top: 1px solid var(--border);
}

.appendix-intro {
  font-size: 12px;
  color: var(--text-muted);
  padding: 12px 0 10px;
  line-height: 1.6;
}
```

## Copy-Paste HTML

### Single appendix section

```html
<details class="appendix">
  <summary>Feature Coverage — data availability by field</summary>
  <div class="appendix-body">
    <p class="appendix-intro">
      7 enrichment fields are missing from the source. These are priority candidates
      for local enrichment before OVER family promotion.
    </p>
    <!-- table or content here -->
  </div>
</details>
```

### Multiple appendix sections

```html
<!-- Stack below the main dashboard content -->

<details class="appendix">
  <summary>Diagnostics — Feature Coverage</summary>
  <div class="appendix-body">
    <p class="appendix-intro">Coverage by feature across the full eligible pool.</p>
    <!-- feature coverage table -->
  </div>
</details>

<details class="appendix">
  <summary>Diagnostics — Signal Associations (Mutual Information and Correlation)</summary>
  <div class="appendix-body">
    <p class="appendix-intro">
      Top 5 features by mutual information and point-biserial correlation per family.
      These are descriptive diagnostics, not causal claims.
    </p>
    <!-- MI / correlation table -->
  </div>
</details>

<details class="appendix">
  <summary>Stability — Concentration Checks by Family</summary>
  <div class="appendix-body">
    <p class="appendix-intro">
      Player, line, and price concentration by selected pool. Price concentration above 50%
      is a diagnostic flag that the selector may be recreating a market filter.
    </p>
    <!-- concentration table -->
  </div>
</details>

<details class="appendix">
  <summary>Reference — Raw Baseline (Unadjusted)</summary>
  <div class="appendix-body">
    <p class="appendix-intro">
      Six-family denominator before any selection rule. UNDER families naturally sit above 50%;
      OVER families start below 50%.
    </p>
    <!-- raw baseline table -->
  </div>
</details>
```

## Related Parent Files

- `components/section-header.md` — primary sections use section headers
- `components/coverage-bar.md` — often appears inside the feature coverage appendix
- `../../workflow/design-preflight.md` — Step 7 (uncertainty/diagnostic content → appendix)
