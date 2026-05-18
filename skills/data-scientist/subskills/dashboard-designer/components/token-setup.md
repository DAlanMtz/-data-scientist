# Token Setup

## Purpose

Define the canonical CSS custom properties every dashboard component uses. Apply this block first, before any other component. All components in this library reference these names — using different names will break the system.

## When to Use

Apply to every dashboard. This is step 3 of the assembly workflow: after selecting the archetype and before placing any component.

## Canonical Token Names

These are the authoritative names. Do not rename, abbreviate, or invent alternatives.

| Token | Role | clean-saas-analytics value |
|---|---|---|
| `--font` | Primary font stack | `system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", "Helvetica Neue", Arial, sans-serif` |
| `--font-mono` | Monospace font stack | `"SFMono-Regular", "Cascadia Mono", Menlo, Consolas, "Liberation Mono", monospace` |
| `--bg` | Page background | `#f7f8f9` |
| `--surface` | Card / panel background | `#ffffff` |
| `--surface-alt` | Table header, zebra row, muted fill | `#f0f2f5` |
| `--border` | Default border | `#e3e5e8` |
| `--border-strong` | Emphasized border | `#c8cbd0` |
| `--text` | Primary text | `#11141a` |
| `--text-secondary` | Supporting text | `#4a5060` |
| `--text-muted` | Labels, captions, metadata | `#848c9a` |
| `--accent` | Primary interactive / brand color | `#2952c4` |
| `--accent-light` | Accent tint for backgrounds | `#e8edfc` |
| `--positive` | Favorable / success text | `#1d7d4c` |
| `--positive-bg` | Favorable background fill | `#e8f7ee` |
| `--positive-mid` | Favorable mid-tone (borders, rule lines) | `#a8dfc0` |
| `--warning` | Caution / monitor text | `#a05c0a` |
| `--warning-bg` | Caution background fill | `#fef3e2` |
| `--warning-mid` | Caution mid-tone | `#f4c790` |
| `--negative` | Risk / failure / blocking text | `#b72b2b` |
| `--negative-bg` | Risk background fill | `#fdeaea` |
| `--negative-mid` | Risk mid-tone | `#f0aaaa` |
| `--neutral-bg` | Neutral metadata background | `#f0f2f5` |
| `--neutral-border` | Neutral metadata border | `#e3e5e8` |
| `--radius` | Default border radius | `6px` |
| `--radius-sm` | Small border radius (chips, cells) | `4px` |
| `--shadow` | Card shadow | `0 1px 3px rgba(0,0,0,0.08)` |
| `--shadow-sm` | Subtle shadow | `0 1px 2px rgba(17,20,26,0.07)` |

## Semantic Chip Tokens

These are compound tokens used specifically by chip and cell components. They are derived from the canonical tokens above — do not add new colors here.

| Token | Maps to | Role |
|---|---|---|
| `--positive-border` | `--positive-mid` | Chip border for ready/success states |
| `--warning-border` | `--warning-mid` | Chip border for monitor/caution states |
| `--negative-border` | `--negative-mid` | Chip border for danger/partial states |

## Token Naming Rules

**Do not use these names:**
- `--green`, `--red`, `--amber`, `--blue` — color names instead of semantic names
- `--panel`, `--card-bg`, `--ink`, `--line`, `--muted` — informal shorthand
- `--color-primary`, `--color-success` — generic design-token naming conventions that clash with this system
- Any name not listed in the table above

**Why this matters:**  
When an agent invents token names, the design system breaks silently. A dashboard using `--green` and `--panel` will not benefit from design system overrides and produces inconsistent output across builds.

## Switching Design Systems

When a design system other than `clean-saas-analytics` is selected, replace the **values** of these tokens — not the names. The component library always uses the same names; only the hex values change.

**Example — switching to `executive-editorial`:**

```css
/* Replace values; keep names identical */
--bg:           #fafaf8;   /* was #f7f8f9 */
--surface-alt:  #f5f4f0;   /* was #f0f2f5 */
--border:       #d8d4cc;   /* was #e3e5e8 */
--accent:       #1a2942;   /* was #2952c4 */
--accent-light: #eaecf2;   /* was #e8edfc */
--radius:       4px;       /* was 6px */
```

Open `../../design-systems/<name>/DESIGN.md` to get the full token table for the selected system. The Token Summary section lists every override value. Tokens not listed in that section keep their clean-saas-analytics defaults.

## Copy-Paste CSS Block

Apply this at the top of every dashboard `<style>` block.

```css
/* ── Design tokens ─────────────────────────────────────────────────── */
/* Source: clean-saas-analytics (default).
   To change visual direction: replace token values with those from
   design-systems/<name>/DESIGN.md — keep token names unchanged. */
:root {
  /* Typography */
  --font:        system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI",
                 "Helvetica Neue", Arial, sans-serif;
  --font-mono:   "SFMono-Regular", "Cascadia Mono", Menlo, Consolas,
                 "Liberation Mono", monospace;

  /* Surfaces */
  --bg:            #f7f8f9;
  --surface:       #ffffff;
  --surface-alt:   #f0f2f5;
  --border:        #e3e5e8;
  --border-strong: #c8cbd0;

  /* Text */
  --text:           #11141a;
  --text-secondary: #4a5060;
  --text-muted:     #848c9a;

  /* Accent */
  --accent:       #2952c4;
  --accent-light: #e8edfc;

  /* Semantic: positive */
  --positive:     #1d7d4c;
  --positive-bg:  #e8f7ee;
  --positive-mid: #a8dfc0;

  /* Semantic: warning */
  --warning:      #a05c0a;
  --warning-bg:   #fef3e2;
  --warning-mid:  #f4c790;

  /* Semantic: negative */
  --negative:     #b72b2b;
  --negative-bg:  #fdeaea;
  --negative-mid: #f0aaaa;

  /* Neutral */
  --neutral-bg:     #f0f2f5;
  --neutral-border: #e3e5e8;

  /* Geometry */
  --radius:    6px;
  --radius-sm: 4px;
  --shadow:    0 1px 3px rgba(0,0,0,0.08);
  --shadow-sm: 0 1px 2px rgba(17,20,26,0.07);
}

*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

body {
  font-family: var(--font);
  background: var(--bg);
  color: var(--text);
  font-size: 14px;
  line-height: 1.5;
  -webkit-font-smoothing: antialiased;
}
```

## Accessibility Rules

- Maintain a minimum contrast ratio of 4.5:1 for body text on its background.
- `--positive`, `--warning`, `--negative` on their respective `*-bg` fills all meet 4.5:1.
- Never use color as the only encoding. Pair with shape, text label, or icon.
- When overriding tokens for a dark design system (operational-command-center, financial-terminal), verify contrast ratios again — they differ from light-mode values.

## Common Mistakes

- Applying a design system by changing only the accent color and leaving all other tokens at defaults — this produces an inconsistent visual result.
- Using `var(--text-muted)` in place of `var(--text-secondary)` for body-weight supporting text — muted is for metadata and captions only.
- Forgetting `--font-mono` and falling back to the system monospace default — this makes code strings and rule names look inconsistent.

## Related Parent Files

- `../../design-systems/README.md` — chooser table
- `../../design-systems/clean-saas-analytics/DESIGN.md` — full token reference for the default system
- `../../references/visual-report-design-system.md` — original token definitions
