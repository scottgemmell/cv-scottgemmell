# Scott Gemmell — CV Design System

**v1.0** · A print-first system for a Front-end UI Developer's CV.
Minimal & editorial, cool slate/blue neutrals, sans + mono.

> This document is the written spec. The living, rendered version is **`Style Guide.dc.html`** — open it to see every token in use and to copy values.

---

## 1. Principles

1. **Whitespace is the layout.** Negative space does the structural work. Sections breathe; nothing is crowded to the edge. When in doubt, add space, not lines.
2. **One quiet accent.** Slate ink on cool paper carries the entire page. The blue accent appears only to guide the eye — a link, a single rule, a marker dot. Never as decoration.
3. **Mono signals system.** Monospace marks *data* — dates, labels, contact details, page numbers — visually separating the "chrome" from the human content set in sans.
4. **Designed for grayscale.** Hierarchy comes from scale, weight, and space — not color. The CV must read perfectly on a black-and-white office printer.

---

## 2. Color

Cool neutrals built in OKLCH for even perceptual steps. One vivid-but-restrained blue accent. Hex values are sRGB approximations for tooling that needs them.

| Token | OKLCH | Hex ≈ | Usage |
|---|---|---|---|
| `--ink` | `oklch(0.24 0.02 256)` | `#1d222b` | Primary text, name, headings |
| `--ink-soft` | `oklch(0.40 0.02 256)` | `#454c57` | Secondary text, item titles |
| `--muted` | `oklch(0.54 0.02 256)` | `#6b7280` | Body support, captions, meta |
| `--faint` | `oklch(0.74 0.015 256)` | `#a6acb6` | Disabled, placeholder text |
| `--line` | `oklch(0.91 0.008 256)` | `#e2e5ea` | Hairline rules, dividers |
| `--surface` | `oklch(0.97 0.006 256)` | `#f0f3f7` | Chips, subtle fills |
| `--paper` | `oklch(0.992 0.003 256)` | `#fbfcfd` | Page background |
| `--accent` | `oklch(0.55 0.18 256)` | `#2f64db` | Links, active marker, single rule |
| `--accent-ink` | `oklch(0.48 0.17 256)` | `#2a55c2` | Accent text needing AA on paper |

**Rules**
- Default text on paper is `--ink` / `--muted`. Body copy never lighter than `--muted` (AA at body size).
- The accent is used **once or twice per page**, maximum. Links, and at most one structural rule or marker.
- The system is **swappable at the accent only** — keep the neutrals fixed. Curated alternates (same L/C, rotated hue): warm clay `oklch(0.55 0.13 40)`, deep teal `oklch(0.55 0.10 200)`.
- Everything must survive `filter: grayscale(1)` — verify before shipping.

---

## 3. Typography

A pairing of **Hanken Grotesk** (display + body) and **Space Mono** (data labels): a friendly, highly readable humanist grotesk set against a technical monospace — warm content, machine-precise data.

- **Hanken Grotesk** — 400 / 500 / 600 / 700 / 800
- **Space Mono** — 400 / 700

Loaded from Google Fonts. For PDF export, embed both (or outline the mono labels).

### Type scale

Each step lists screen `px` and the print `pt` it maps to on A4.

| Role | Family / Weight | Size (screen → print) | Line height | Tracking | Case |
|---|---|---|---|---|---|
| Display XL — Name | Hanken 600 | 56px → 40pt | 1.02 | −0.02em | — |
| Display — Section | Hanken 600 | 34px → 24pt | 1.10 | −0.01em | — |
| Title — Entry role | Hanken 600 | 21px → 15pt | 1.25 | 0 | — |
| Lead — Summary | Hanken 400 | 20px → 14pt | 1.50 | 0 | — |
| Body | Hanken 400 | 16px → 11.5pt | 1.60 | 0 | — |
| Small — Meta | Hanken 400 | 14px → 10pt | 1.45 | 0 | — |
| Label — Kicker | **Mono 700** | 12px → 8.5pt | 1.0 | 0.14em | UPPER |
| Micro — Dates / pg | **Mono 400** | 13px → 9.5pt | 1.30 | 0.02em | — |

**Rules**
- One weight does one job: 600 for display + titles, 400 for everything read in volume. Hanken's 500 is reserved for the type-scale Medium specimen. Avoid 700+ in sans except where genuinely needed.
- Mono is reserved for *machine-readable data*: dates, locations, contact, page numbers, eyebrow labels. Never set a sentence in mono.
- `text-wrap: pretty` on headings; `text-wrap: balance` on the name and section titles.
- Body measure: 60–72 characters. On A4 that's roughly the content column width.

---

## 4. Spacing & layout grid

**Base unit: 4px.** All spacing is a multiple. Print uses the mm equivalents.

| Token | px | mm (print) | Typical use |
|---|---|---|---|
| `space-2xs` | 4 | 1.0 | Icon/text gap |
| `space-xs` | 8 | 2.0 | Chip padding, tight stacks |
| `space-sm` | 12 | 3.0 | Inside a row |
| `space-md` | 16 | 4.0 | Between related lines |
| `space-lg` | 24 | 6.0 | Between entries |
| `space-xl` | 32 | 8.0 | Column gap |
| `space-2xl` | 48 | 12.0 | Between sections |
| `space-3xl` | 64 | 16.0 | After the masthead |
| `space-4xl` | 96 | 24.0 | Major breaks / page top |

**Radii** (editorial = nearly sharp): `0` default · `2px` print chips · `4px` screen chips · `999px` pill tags.

### The "ledger" grid

The CV is a **two-zone ledger**: a fixed mono meta rail on the left, flexible content on the right.

```
│ meta rail │  content column                        │
│  32mm     │  flexible                               │
│  2017—Now │  Senior Front-end Developer  ↗          │
│  Glasgow  │  Acme Co. · built the design system …   │
```

- Meta rail: **32mm** (≈120px screen), right-aligned mono, holds dates + location.
- Column gap: `space-xl` (8mm / 32px).
- Optional **third zone** (skills sidebar, ≈40mm) for a denser one-pager — mirror of the Cristal Fay reference. Keep to two zones when content is light; whitespace > density.
- Screen style-guide grid: single centered column, max-width **920px**.

---

## 5. Print specifications

| Spec | Value |
|---|---|
| Primary page | **A4 — 210 × 297 mm** |
| Alternate | US Letter — 8.5 × 11 in |
| Margins | **20 mm** all sides (≈ 0.79 in) |
| Content width (A4) | 170 mm |
| Body leading | 11.5pt / 1.6 ≈ 18.4pt |
| Color | Single accent; design holds in grayscale |
| Image resolution | 300 dpi; photos grayscale or slate duotone |
| Export | PDF, fonts embedded; mono labels may be outlined |
| Page count | 1 page preferred, 2 maximum |

**Print rules**
- Never let an entry break across pages — keep `break-inside: avoid` on entries and section headers.
- Hairlines print at `0.5pt` minimum (use `--line`, not pure black).
- Leave the bottom 20mm margin clear; no content bleeds to the page edge.

---

## 6. Components

The living spec for each is in `Style Guide.dc.html`. Summary:

- **Mono kicker** — uppercase mono label, `--muted`, `0.14em` tracking. Eyebrow above a name or section.
- **Numbered section header** — `01` mono + Display title + a hairline rule filling the row. One per section.
- **Experience entry** — ledger row: meta rail (`years` mono + `location`) → content (role title with `↗` link, company, one-line description, optional bullets). `break-inside: avoid`.
- **Skill tag** — pill chip, `--surface` fill, mono text, `space-xs` padding. Used in clusters.
- **Contact row** — mono label + value, optionally with `↗`. Sits in the masthead or footer.
- **Hairline divider** — `1px`/`0.5pt` `--line`, used sparingly between major zones, never between every item.
- **External link** — `--accent`, no underline at rest, trailing `↗` glyph; underline on hover (screen only).

---

## 7. Do & Don't

**Do** — lead with space; keep the accent rare; align everything to the 4px grid; let mono carry the data; test in grayscale; keep to one page.

**Don't** — add gradients, drop shadows, or rounded "card" containers with a left accent border; set body or sentences in mono; use more than one accent on a page; fill whitespace just because it's empty; drop below `--muted` for readable text.
