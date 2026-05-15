# Chart Style System

Use this system to produce charts that look like professional data journalism rather than defaults. Copy-paste the configurations below into your Python or R environment. The system is opinionated: it is designed to defeat the most common AI-generated chart fingerprints.

Override the palette or font when the user has a brand system. The structure and removal of defaults should remain regardless.

---

## Design Token Reference

These are the canonical values used across Python, R, HTML, and BI tools. Reference them when any tool asks for a color, font, or spacing value.

### Color palette

```python
# Paste-ready Python constants
ACCENT       = "#2952c4"   # deep corporate blue — primary highlight, selected state
TEXT_DARK    = "#11141a"   # near-black — chart text, axis labels
TEXT_MID     = "#4a5060"   # secondary — axis titles, legend text
TEXT_MUTED   = "#848c9a"   # quiet — tick labels, footnote text
BORDER       = "#e3e5e8"   # grid lines, spines, card borders
BG_PAGE      = "#f7f8f9"   # page/figure background (warm off-white)
BG_SURFACE   = "#ffffff"   # card/panel background

# Semantic status
POSITIVE     = "#1d7d4c"   # forest green (favorable)
POSITIVE_BG  = "#e8f7ee"
WARNING      = "#a05c0a"   # amber-brown (needs review)
WARNING_BG   = "#fef3e2"
NEGATIVE     = "#b72b2b"   # deep red (risk / alert)
NEGATIVE_BG  = "#fdeaea"

# Reference / baseline
REFERENCE    = "#9ba5b2"   # gray — baselines, averages, historical context
```

### Chart categorical sequence

Use in order. Do not skip to a later color to match a "feeling" about the data.

```python
CHART_COLORS = [
    "#2952c4",   # 1 — deep blue       (primary series)
    "#d4531c",   # 2 — burnt orange    (second series)
    "#2a7f62",   # 3 — forest green    (third series)
    "#7c3aac",   # 4 — deep purple     (fourth series)
    "#b5282f",   # 5 — brick red       (fifth series)
    "#1a8fa8",   # 6 — teal            (sixth series)
    "#c07d2e",   # 7 — amber           (seventh series)
    "#9ba5b2",   # 8 — slate gray      (reference / baseline)
]
```

This palette is:
- Distinct from the matplotlib tab10 and seaborn default cycles
- Readable in colorblind simulations (deuteranopia, protanopia)
- Usable in print and grayscale with additional markers/patterns
- Editorial in tone: earthy, desaturated relative to rainbow palettes

### Sequential palettes

For heatmaps, density, or single-metric intensity (light to dark):

```python
SEQ_BLUE = ["#e8edfc", "#adbdf0", "#7290e1", "#2952c4", "#1a347a"]
SEQ_GRAY = ["#f4f5f6", "#d1d5db", "#9ca3af", "#6b7280", "#374151"]
SEQ_GREEN = ["#e3f7ed", "#9ad9bb", "#4db584", "#1d7d4c", "#104d2f"]
```

### Diverging palette

For two-sided data: deviation from a baseline, positive vs negative change, above vs below threshold.

```python
DIVERGING = ["#d4531c", "#f2bfa6", "#f5f0ee", "#b3c7ee", "#2952c4"]
```

---

## Python: Matplotlib House Style

### Step 1 — Define rcParams dict

```python
import matplotlib as mpl
import matplotlib.pyplot as plt

HOUSE_RCPARAMS = {
    # ── Typography ──────────────────────────────────────────────
    "font.family":          "sans-serif",
    "font.sans-serif":      ["Helvetica Neue", "Helvetica", "Arial",
                             "Nimbus Sans", "DejaVu Sans"],
    "font.size":            12,
    "axes.titlesize":       13,
    "axes.titleweight":     "bold",
    "axes.titlepad":        10,
    "axes.labelsize":       11,
    "axes.labelcolor":      "#4a5060",
    "xtick.labelsize":      10,
    "ytick.labelsize":      10,
    "legend.fontsize":      10,

    # ── Color ────────────────────────────────────────────────────
    "axes.prop_cycle":      mpl.cycler("color", CHART_COLORS),
    "figure.facecolor":     "#ffffff",
    "axes.facecolor":       "#ffffff",
    "axes.edgecolor":       "#e3e5e8",
    "axes.linewidth":       0.8,
    "text.color":           "#11141a",

    # ── Grid ─────────────────────────────────────────────────────
    "axes.grid":            True,
    "grid.color":           "#e3e5e8",
    "grid.linewidth":       0.5,
    "grid.alpha":           1.0,
    "axes.axisbelow":       True,   # grid behind data

    # ── Spines ───────────────────────────────────────────────────
    "axes.spines.top":      False,
    "axes.spines.right":    False,

    # ── Ticks ────────────────────────────────────────────────────
    "xtick.major.size":     3,
    "ytick.major.size":     3,
    "xtick.minor.size":     0,
    "ytick.minor.size":     0,
    "xtick.color":          "#848c9a",
    "ytick.color":          "#848c9a",
    "xtick.direction":      "out",
    "ytick.direction":      "out",
    "xtick.major.pad":      4,
    "ytick.major.pad":      4,

    # ── Lines and patches ────────────────────────────────────────
    "lines.linewidth":      1.8,
    "lines.solid_capstyle": "round",
    "patch.linewidth":      0.7,
    "scatter.marker":       "o",

    # ── Figure ───────────────────────────────────────────────────
    "figure.dpi":           150,
    "figure.titlesize":     14,
    "figure.titleweight":   "bold",

    # ── Save / export ─────────────────────────────────────────────
    "savefig.dpi":          220,
    "savefig.bbox":         "tight",
    "savefig.pad_inches":   0.15,
    "savefig.facecolor":    "#ffffff",

    # ── Legend ───────────────────────────────────────────────────
    "legend.frameon":       False,
    "legend.borderpad":     0,
    "legend.handlelength":  1.2,
    "legend.handletextpad": 0.5,
    "legend.labelspacing":  0.4,
}
```

### Step 2 — Apply as context manager or globally

```python
# Apply for the entire session (call once at top of file or notebook)
def use_house_style():
    """Apply the house rcParams globally."""
    mpl.rcParams.update(HOUSE_RCPARAMS)

# Apply for a single figure
with mpl.rc_context(HOUSE_RCPARAMS):
    fig, ax = plt.subplots(figsize=(10, 5))
    ax.plot(x, y)
```

### Step 3 — Standard figure sizes

```python
# Match size to information density, not just preference
FIG_WIDE    = (10, 5.0)   # full-width: main finding, trend, dashboard primary
FIG_HALF    = (6, 4.0)    # half-width: segment breakdown, secondary panel
FIG_SMALL   = (5, 3.2)    # supporting: diagnostic, appendix, residual plot
FIG_SQUARE  = (5, 5.0)    # scatter plots, confusion matrices, calibration curves
FIG_PRINT   = (7, 3.5)    # print/PDF column chart

# Usage
fig, ax = plt.subplots(figsize=FIG_WIDE)
```

### Step 4 — Spine and axis cleanup helper

```python
def clean_axes(ax, keep_bottom=True, keep_left=True, grid="y"):
    """Remove spines and configure grid for publication-quality axes."""
    ax.spines["top"].set_visible(False)
    ax.spines["right"].set_visible(False)
    ax.spines["bottom"].set_visible(keep_bottom)
    ax.spines["left"].set_visible(keep_left)

    if grid == "y":
        ax.yaxis.grid(True, color=BORDER, linewidth=0.5, zorder=0)
        ax.xaxis.grid(False)
    elif grid == "x":
        ax.xaxis.grid(True, color=BORDER, linewidth=0.5, zorder=0)
        ax.yaxis.grid(False)
    elif grid == "both":
        ax.grid(True, color=BORDER, linewidth=0.5, zorder=0)
    elif grid == "none":
        ax.grid(False)

    ax.set_axisbelow(True)
    return ax
```

### Step 5 — Direct label helper

```python
def direct_label(ax, line, label, color=None, offset=(4, 0), fontsize=10):
    """Place a text label at the end of a line instead of using a legend."""
    x_data = line.get_xdata()
    y_data = line.get_ydata()
    color = color or line.get_color()
    ax.annotate(
        label,
        xy=(x_data[-1], y_data[-1]),
        xytext=(x_data[-1] + offset[0], y_data[-1] + offset[1]),
        color=color,
        fontsize=fontsize,
        va="center",
        fontweight="medium",
    )
```

### Step 6 — Event annotation helper

```python
def annotate_event(ax, x, label, ypos=0.97, color="#848c9a", linestyle="--",
                   linewidth=0.8, fontsize=9):
    """Mark a vertical event line with a label (launch, outage, policy change)."""
    ax.axvline(x, color=color, linewidth=linewidth, linestyle=linestyle, zorder=1)
    ax.text(
        x, ypos, label,
        transform=ax.get_xaxis_transform(),
        ha="right", va="top",
        fontsize=fontsize, color=color,
        rotation=90,
    )
```

### Step 7 — Reference line helper

```python
def reference_line(ax, y, label, color=REFERENCE, axis="y", fontsize=9):
    """Draw a labeled reference line (baseline, target, threshold)."""
    if axis == "y":
        ax.axhline(y, color=color, linewidth=1.0, linestyle="--", zorder=1)
        ax.text(
            0.01, y, f" {label}", transform=ax.get_yaxis_transform(),
            va="bottom", ha="left", fontsize=fontsize, color=color,
        )
    elif axis == "x":
        ax.axvline(y, color=color, linewidth=1.0, linestyle="--", zorder=1)
```

### Step 8 — Number formatting helpers

```python
def fmt_number(n, decimals=1):
    """Format large numbers as 1.2K, 4.5M, etc."""
    if abs(n) >= 1_000_000:
        return f"{n / 1_000_000:.{decimals}f}M"
    elif abs(n) >= 1_000:
        return f"{n / 1_000:.{decimals}f}K"
    return f"{n:.{decimals}f}"

def fmt_pct(n, decimals=1):
    """Format a 0–1 float as a percentage string."""
    return f"{n * 100:.{decimals}f}%"
```

### Step 9 — Publication-quality export

```python
import pathlib

def save_chart(fig, path, dpi=220, fmt="png"):
    """Save a figure at publication quality with correct settings."""
    pathlib.Path(path).parent.mkdir(parents=True, exist_ok=True)
    fig.savefig(path, dpi=dpi, bbox_inches="tight", facecolor="white",
                format=fmt, pad_inches=0.15)
    print(f"Saved: {path}")
```

---

## Python: Seaborn Integration

Apply the house style before creating seaborn figures:

```python
import seaborn as sns

def use_seaborn_house_style():
    """Set seaborn to use the house palette and remove default background."""
    sns.set_theme(style="white", palette=CHART_COLORS, font="Arial")
    mpl.rcParams.update(HOUSE_RCPARAMS)
    # Remove the seaborn legend frame that overrides rcParams
    sns.set(rc={"legend.frameon": False})
```

For specific chart types:
```python
# Heatmaps: use SEQ_BLUE or DIVERGING, not the seaborn default
sns.heatmap(data, cmap=sns.color_palette(SEQ_BLUE, as_cmap=True))

# Distribution plots: use ACCENT for the primary distribution
sns.histplot(data, color=ACCENT, alpha=0.75, edgecolor="white", linewidth=0.5)
```

---

## R: ggplot2 House Theme

### Step 1 — Define the theme function

```r
# Install required packages if needed:
# install.packages(c("ggplot2", "scales"))

library(ggplot2)

# House color constants
CHART_COLORS <- c(
  "#2952c4",  # deep blue
  "#d4531c",  # burnt orange
  "#2a7f62",  # forest green
  "#7c3aac",  # deep purple
  "#b5282f",  # brick red
  "#1a8fa8",  # teal
  "#c07d2e",  # amber
  "#9ba5b2"   # slate gray
)

REFERENCE_COLOR <- "#9ba5b2"
GRID_COLOR      <- "#e3e5e8"
TEXT_MID        <- "#4a5060"
TEXT_MUTED      <- "#848c9a"

theme_house <- function(base_size = 12, base_family = "") {
  theme_minimal(base_size = base_size, base_family = base_family) %+replace%
  theme(
    # Titles and labels
    plot.title = element_text(
      size = base_size + 1, face = "bold", color = "#11141a",
      margin = margin(b = 4), hjust = 0
    ),
    plot.subtitle = element_text(
      size = base_size - 1, color = TEXT_MUTED,
      margin = margin(b = 12), hjust = 0
    ),
    plot.caption = element_text(
      size = base_size - 2, color = TEXT_MUTED,
      hjust = 0, margin = margin(t = 10)
    ),
    # Axes
    axis.title = element_text(size = base_size - 1, color = TEXT_MID),
    axis.title.x = element_text(margin = margin(t = 6)),
    axis.title.y = element_text(margin = margin(r = 6), angle = 90),
    axis.text  = element_text(size = base_size - 2, color = TEXT_MID),
    axis.line  = element_blank(),
    axis.ticks = element_line(color = GRID_COLOR, linewidth = 0.4),
    # Panel
    panel.grid.major = element_line(color = GRID_COLOR, linewidth = 0.4),
    panel.grid.minor = element_blank(),
    panel.border     = element_blank(),
    panel.background = element_rect(fill = "white", color = NA),
    # Plot
    plot.background  = element_rect(fill = "white", color = NA),
    plot.margin      = margin(12, 16, 12, 12),
    # Legend
    legend.position    = "top",
    legend.direction   = "horizontal",
    legend.title       = element_blank(),
    legend.text        = element_text(size = base_size - 2, color = TEXT_MID),
    legend.key.size    = unit(0.8, "lines"),
    legend.margin      = margin(b = 4),
    legend.background  = element_rect(fill = NA, color = NA),
    # Facets
    strip.text       = element_text(size = base_size - 1, face = "bold", color = "#11141a"),
    strip.background = element_rect(fill = "#f7f8f9", color = NA)
  )
}
```

### Step 2 — Color scale helpers

```r
# Categorical
scale_color_house <- function(...) {
  scale_color_manual(values = CHART_COLORS, ...)
}

scale_fill_house <- function(...) {
  scale_fill_manual(values = CHART_COLORS, ...)
}

# Sequential (blue)
SEQ_BLUE <- c("#e8edfc", "#adbdf0", "#7290e1", "#2952c4", "#1a347a")

scale_fill_seq_blue <- function(...) {
  scale_fill_gradientn(colors = SEQ_BLUE, ...)
}

# Diverging
DIVERGING <- c("#d4531c", "#f2bfa6", "#f5f0ee", "#b3c7ee", "#2952c4")

scale_fill_diverging <- function(...) {
  scale_fill_gradientn(colors = DIVERGING, ...)
}
```

### Step 3 — Standard figure sizes for ggsave

```r
# Standard sizes (inches)
FIG_WIDE  <- list(width = 10,   height = 5.0)
FIG_HALF  <- list(width = 6,    height = 4.0)
FIG_SMALL <- list(width = 5,    height = 3.2)
FIG_SQ    <- list(width = 5,    height = 5.0)
FIG_PRINT <- list(width = 7,    height = 3.5)

# Usage:
# ggsave("chart.png", p, width = FIG_WIDE$width, height = FIG_WIDE$height,
#         dpi = 220, bg = "white")
```

### Step 4 — Reference line and event annotation helpers

```r
# Reference line with label
geom_reference <- function(yintercept, label, color = REFERENCE_COLOR) {
  list(
    geom_hline(yintercept = yintercept, linetype = "dashed",
               color = color, linewidth = 0.7),
    annotate("text", x = -Inf, y = yintercept, label = paste0(" ", label),
             hjust = 0, vjust = -0.3, color = color, size = 3)
  )
}

# Event annotation
geom_event <- function(xintercept, label, color = TEXT_MUTED) {
  list(
    geom_vline(xintercept = xintercept, linetype = "dashed",
               color = color, linewidth = 0.7),
    annotate("text", x = xintercept, y = Inf, label = label,
             hjust = 1.05, vjust = 1.4, color = color, size = 3, angle = 90)
  )
}
```

### Step 5 — Complete example

```r
library(ggplot2)
library(scales)

# Apply house style to a time-series plot
ggplot(revenue_data, aes(x = date, y = revenue, color = segment)) +
  geom_line(linewidth = 1.4) +
  geom_reference(yintercept = target_revenue, label = "Target") +
  geom_event(xintercept = launch_date, label = "Product launch") +
  scale_color_house() +
  scale_y_continuous(labels = label_number(scale_cut = cut_short_scale())) +
  scale_x_date(date_breaks = "1 month", date_labels = "%b") +
  labs(
    title    = "Revenue exceeded target in Q3 for the first time since launch",
    subtitle = "Monthly revenue by segment, Jan–Dec 2025, n = 12 months",
    caption  = "Source: finance DW | Caveats: excludes refunds and partner revenue",
    x = NULL, y = "Revenue"
  ) +
  theme_house()
```

---

## BI Tool Guidance

When working in Tableau, Power BI, Looker, Superset, or Metabase, the principles remain the same. Most BI tools have a default theme that should be overridden.

### Tableau

- Use a custom color palette with the CHART_COLORS hex values.
- Set the default font to the system UI font for the platform (Tableau Benton Sans is acceptable; avoid Comic Sans or Impact defaults).
- Remove chart borders. Set the background to white, not the default gray.
- Use Format > Shading: none on rows. Use light gray horizontal reference lines.
- Set tooltip text to match the caption format: metric, population, time window, caveat.

### Power BI

- Create a custom theme JSON with the CHART_COLORS values.
- Set canvas background to `#f7f8f9` and card fill to `#ffffff`.
- Remove default drop shadows or set them to 0.08 opacity.
- Use the system font: Segoe UI on Windows, San Francisco on macOS via web.
- Hide chart borders. Use the top-accent line style for cards instead.

### Streamlit / Shiny / Dash

- Pass `color_discrete_sequence=CHART_COLORS` to Plotly figures.
- Set Plotly layout: `plot_bgcolor="white"`, `paper_bgcolor="white"`.
- Set template: `go.layout.Template` with the house rcParams mapped to Plotly.
- Apply the house theme function in Shiny with `thematic::thematic_shiny()` or a custom CSS file.

---

## Plotly Configuration

For interactive HTML exports using Plotly:

```python
import plotly.graph_objects as go
import plotly.io as pio

PLOTLY_HOUSE_TEMPLATE = go.layout.Template(
    layout=go.Layout(
        font=dict(family="Helvetica Neue, Helvetica, Arial, sans-serif",
                  color="#11141a", size=12),
        paper_bgcolor="#ffffff",
        plot_bgcolor="#ffffff",
        colorway=CHART_COLORS,
        xaxis=dict(
            showgrid=False,
            showline=True,
            linecolor="#e3e5e8",
            linewidth=0.8,
            tickfont=dict(color="#848c9a", size=10),
            title_font=dict(color="#4a5060", size=11),
        ),
        yaxis=dict(
            showgrid=True,
            gridcolor="#e3e5e8",
            gridwidth=0.5,
            showline=False,
            tickfont=dict(color="#848c9a", size=10),
            title_font=dict(color="#4a5060", size=11),
        ),
        legend=dict(bgcolor="rgba(0,0,0,0)", borderwidth=0,
                    orientation="h", yanchor="bottom", y=1.02,
                    xanchor="left", x=0),
        margin=dict(t=40, l=50, r=20, b=50),
    )
)

# Register and use
pio.templates["house"] = PLOTLY_HOUSE_TEMPLATE
pio.templates.default = "house"
```

---

## Related Files

- `references/design-craft-guide.md` — craft principles and anti-pattern reference
- `references/visual-report-design-system.md` — design tokens, page layout, editorial standards
- `references/visualization-guide.md` — chart type selection by question
- `templates/html-report-template.md` — HTML report with design tokens applied
- `templates/dashboards/html-dashboard-starter-template.md` — dashboard HTML with design tokens applied
