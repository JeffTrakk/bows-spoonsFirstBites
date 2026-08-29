# First Bites Design System

The canonical design language of the **Bows and Spoons First Bites** app, derived
from the app itself. Everything lives in this one folder. It builds on the **Nocturne**
foundation (now consolidated here) and formalizes the layer Nocturne never documented
but the app depends on: the **health-status semantics**.

The app links exactly one file — `styles.css`:

```html
<link rel="stylesheet" href="design-system/styles.css">
```

### Files

| File | What it is |
| --- | --- |
| `styles.css` | The stylesheet every page links. Pulls in `tokens.css`, then defines the component layer (Nocturne foundation + First Bites status components). |
| `tokens.css` | The complete, **source-of-truth** token set. Every colour, font, space, radius and shadow. Never hard-code a value a token already carries. |
| `index.html` | The living style guide — the whole system rendered. Open in a browser or view the [published reference](https://claude.ai/code/artifact/c3bd46f1-4a5e-4605-ac6e-6d2fe357d592). |
| `README.md` | This guide. |
| `_ds_bundle.js` | A tiny namespace stub the app loads; kept for compatibility. |
| `_ds_manifest.json`, `_adherence.oxlintrc.json` | Tooling metadata carried over from Nocturne. |

## What this is

A quiet, dense, dark interface for a parent working through a multi-day home
food-introduction protocol. The look is Nocturne — a near-neutral blue-grey ground,
Inter at 500, an 8px grid at 0.70× density, a single blurple accent (`#9184d9`) used as
a line and a glow rather than a flood, and rules that fade to transparent at their ends.

What makes it a *medical companion* rather than a generic dark app is the semantic layer.

## Health-status semantics — the First Bites layer

In a home allergy protocol, colour is not decoration; it tells a parent whether to carry
on, watch closely, or call 911. Three voices, each a **first-class role** — never the
accent, never each other:

| Role | Base | Text-on-dark | Meaning in the app |
| --- | --- | --- | --- |
| **Success** (safe) | `--color-success` `#5FAE87` | `--color-success-300` `#9FD6BB` | Dose taken, watch window clear, tolerated. |
| **Caution** (mild) | `--color-caution` `#D0A05C` | `--color-caution-300` `#E6C48D` | Mild reaction, review pending, watch running. |
| **Danger** (severe) | `--color-danger` `#D9736A` | `--color-danger-100…400` | Reaction plan, 911, severe symptoms. |

Each role carries a `-tint` (10–12% fill) and `-edge` (34% hairline) for the app's
standard status surface: a tinted background, a hairline inset border, and a light-step
text colour on top. Danger additionally carries `--color-danger-ink` (`#1B1015`) — the
only place text sits **on** a filled semantic surface (the 911 button).

### Rules

- Reserve each voice for its meaning. Danger is the emergency, never a highlight or a
  brand pop. Never style a status with the accent, and never borrow one semantic's colour
  for another.
- Danger is **the one filled button** in the system — because in an emergency it must win.
  Every other action is an accent outline.
- Semantics are separate from the accent hue and do not count as the accent.

## Foundation quick reference

- **Colour** — dark ground `#161826`, surface `#232532`, ink `#e9e9ed`, accent `#9184d9`.
  Each role has a 100–900 OKLCH ramp on a shared lightness scale; contrast comes from
  value, not saturation. No pure black or white.
- **Type** — Inter for headings (weight 500) over Inter for body. Hierarchy is size and
  space; never bolden headings past 500.
- **Spacing** — `--space-*`, density 0.70×, dense on purpose. Radius 4 / 8 / 14px.
- **Elevation** — a hairline edge plus ambient darkness (`--shadow-sm/md/lg`); don't
  stack heavy shadows.
- **Icons** — [Phosphor](https://phosphoricons.com), regular and fill.
- **Motion** — two signatures: `fb-halo` (the 3.4s emergency-button pulse) and `fb-rise`
  (an 8px opacity enter).

## Components

Build with these classes rather than inventing parallel ones. States (hover, pressed,
focus ring, disabled) are built in — don't restyle them per page.

| Class | What it is |
| --- | --- |
| `.btn` + `.btn-primary` / `.btn-secondary` / `.btn-ghost` / `.btn-icon` / `.btn-block` | Actions — primary is an accent **outline**, never a fill. |
| `.btn-danger` | The one **filled** button — the emergency action, so it wins. |
| `.tag` + `.tag-accent` / `.tag-neutral` / `.tag-outline` | Small labels tinted from the ramps. |
| `.tag-danger` / `.tag-success` / `.tag-caution` | Status tags in the three semantic voices. |
| `.field` + `label`, `.input`, `.radio` + `.dot`, `.seg` + `.seg-opt` | Form fields and choices on native elements — no script. |
| `.card` + `.card-kicker` / `.card-title` / `.card-body` / `.card-meta`; `.elev-sm/md/lg` | Surface-filled cards; elevation utilities. |
| `.nav` + `.nav-brand` | The header bar. |
| `.table` | Data tables with themed header and fading row rules. |
| `.dialog-backdrop` + `.dialog` (+ `-title` / `-body` / `-actions`) | A modal at the top elevation. |
| `.hr` | A rule that fades at its ends. This system prefers whitespace; use sparingly. |
| `.lighten` | Image wrapper — `mix-blend-mode: lighten` blends photographs into the page. |
| **`.status`** + `.status-success/caution/danger` | The reusable status surface: role tint, hairline role edge, light-step text. |
| **`.status-pill`** + `.is-success/caution/danger` | A coloured dot on a neutral pill. |
| **`.alert`** + `.alert-icon` / `.alert-text` / `.alert-call` | The pinned emergency bar. |
| **`.timer`** + `.timer-value` / `.timer-label` | The two-hour watch-window timer, success-tinted while clear. |

## Using it

```css
/* Follow the one status-surface recipe for any new health state. */
.reaction-surface {
  background: var(--color-danger-tint);
  box-shadow: inset 0 0 0 1px var(--color-danger-edge);
  color: var(--color-danger-100);
}
.dose-taken { color: var(--color-success-300); }
```

## Relationship to Nocturne

Nocturne was this app's original foundation and is now **consolidated into this folder**:
its component layer lives in `styles.css`, its tokens in `tokens.css`. This system doesn't
replace Nocturne — it absorbs it and adds the product's semantic colours and the
app-specific patterns (alert bar, watch-window timer, status pills, status surfaces) that
previously lived only as inline styles inside the app file.

---

**Not a medical device.** This app does not diagnose allergy. Clinician instructions
always take precedence over anything shown in the app.
