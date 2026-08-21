# Design System — Tony Huang portfolio (heatescape.github.io)

Created 2026-08-21 by /design-consultation. This file is the source of truth for
every visual decision on this site. Do not change fonts, colours or spacing
without updating this file first.

## Product Context

- **What this is:** a one page personal portfolio used as the link in a resume
  header, a LinkedIn website field, and cover letter signatures.
- **Who it is for:** Australian hiring managers and technical recruiters. The
  employers currently in the funnel are institutional: a public broadcaster, a
  state government museums body, and universities.
- **Space:** engineer and AI practitioner portfolios.
- **Project type:** single page editorial site, not an app and not a marketing site.
- **The one thing to remember:** this person shows you the guardrails, not just
  the build.

## Research findings that drove the decisions

- Category baseline for engineer portfolios in 2026: lead with the work rather
  than words, one clear action, fast load, scannable on mobile.
- A recognised genre in this category is the terminal or IDE look: monospace
  type, dark theme, command style navigation.
- Current typographic direction in premium work: neo grotesques have displaced
  geometric sans serifs, and editorial serifs are having their strongest run in
  decades.

**The deliberate departure.** The category norm is the terminal look, and it is
aimed at other engineers. The readers of this site are not engineers. They are
recruiters and hiring managers at a broadcaster, a government body and
universities. So the site borrows from the institutional editorial register
instead of the developer register. That is the one large risk in this system and
it is taken on purpose.

## Aesthetic Direction

- **Direction:** Editorial, Swiss International.
- **Decoration level:** minimal. Typography and rules do all the work.
- **Mood:** serious, printed, checked. Closer to an annual report than a product page.
- **Explicitly excluded:** cards, drop shadows, rounded corners, gradients,
  decorative icons, three column feature grids, centered everything.

## Typography

Kept after review rather than changed. Neither family appears on the overused
list that contains Inter, Roboto, Helvetica, Open Sans, Lato, Montserrat,
Poppins and Space Grotesk, and the pairing matches the current direction of
neo grotesque display over editorial serif body.

- **Display and UI:** Archivo. Neo grotesque, wide weight range, holds up at
  92px for the name and at 12px for uppercase labels.
- **Body:** Newsreader. Editorial serif with optical sizing, built for reading
  at paragraph length on screen.
- **Data and figures:** Archivo with `font-variant-numeric: tabular-nums` so the
  three hero figures align on the same digit width.
- **Loading:** Google Fonts via a single link tag. No self hosting, no build step.
- **Scale:** fluid `clamp()` throughout.
  - name `clamp(2.6rem, 7.25vw, 5.75rem)`
  - thesis `clamp(1.25rem, 0.9rem + 2.5vw, 2.75rem)`
  - h2 `clamp(1.5rem, 1.1rem + 1.6vw, 2.5rem)`
  - h3 and lede `clamp(1.25rem, 1.05rem + 0.85vw, 1.75rem)`
  - body `clamp(1.0625rem, 0.98rem + 0.35vw, 1.1875rem)`
  - label `0.75rem` uppercase, tracking `0.16em`
- **Rule:** the name must always outrank the thesis line. Check this at 390px,
  not only at 1440px. It broke once already.

## Colour

Approach: restrained. One accent, cool neutrals, colour is rare and always means
something.

| Token | Value | Use | Contrast on paper |
|---|---|---|---|
| `--paper` | `#E9EFF1` | page background | |
| `--ink` | `#14171A` | body and headings | 15.5:1 |
| `--muted` | `#4B5356` | secondary text, figure captions | 6.8:1 |
| `--accent` | `#14452F` | second line of the name, the emphasis half of the thesis, the three figures, section numbers | 9.4:1 |
| `--rule` | `#CBD5D8` | hairlines | |
| `--rule-strong` | `#14171A` | structural rules | |

**Hard constraint: measurable distance from AI vendor brand palettes.** The
first version of this site used cream `#FBFAF7` with terracotta `#C43A1E`, which
is deltaE 0.9 from Anthropic's `#FAF9F5`. A human recognised it on sight as
machine made. Every colour here is checked in CIELAB against Anthropic cream and
terracotta, the OpenAI green, the common AI purple and indigo, and the Gemini
blue.

- Paper `#E9EFF1` has `b* = -1.7`. Negative means no yellow cast, which is the
  specific tell in the cream family.
- Accent `#14452F` sits deltaE 40.3 from its nearest AI vendor colour, the
  OpenAI green. An earlier green, `#0F5C3F`, measured only 29.1 and was rejected
  for that reason even though it looked fine.

**Rule for any future colour change:** compute deltaE against that vendor set
before adopting it. Do not judge by eye. The eye is the thing that failed.

## Spacing

- **Base:** 4px, expressed as fluid `clamp()` pairs.
- **Density:** spacious. This is a reading page, not a dashboard.
- **Scale:** gap `clamp(20px,3vw,44px)`, page padding `clamp(20px,5vw,84px)`,
  small stack `clamp(28px,4vw,52px)`, medium stack `clamp(52px,7vw,104px)`,
  large stack `clamp(72px,10vw,152px)`.

## Layout

- **Approach:** grid disciplined with editorial asymmetry.
- **Max content width:** 1400px.
- **Section grid:** single column below 1000px, then 3 and 9 columns. The label
  column carries the section number and heading; the wide column carries the prose.
- **Hero:** 7 and 4 columns at 1000px and above. Left is the name and the thesis
  line. Right is the three figures. Below 1000px the figures stack under the thesis.
- **Border radius:** 0 everywhere. This is deliberate and is part of the direction.
- **Breakpoints:** 390, 700, 768, 1000, 1024, 1440. Verified for zero horizontal
  overflow at each.

## Motion

- **Approach:** minimal functional.
- Only `opacity` and `transform` are animated. Entrance reveal is 620ms on
  `cubic-bezier(0.16, 1, 0.3, 1)`.
- `prefers-reduced-motion: reduce` disables all transitions and shows every
  element at full opacity.
- **Hard rule:** the page must be fully readable with JavaScript disabled.
  Verified: zero elements below 0.5 opacity with JS off.

## Non negotiable content and accessibility rules

These come from the job hunt brief and outrank any visual preference.

1. ASCII only in the rendered file. No em dashes, en dashes, smart quotes or
   ellipsis characters.
2. Body text contrast at least 4.5:1.
3. The work rights line must be visible without scrolling at 1440x900.
4. No horizontal overflow at 390, 768, 1024 or 1440.
5. Visible keyboard focus on every link. Touch targets at least 44px on mobile.
6. No factual claim may appear that is not already in the source resume.

## Decisions Log

| Date | Decision | Rationale |
|---|---|---|
| 2026-08-21 | Editorial Swiss direction, not the terminal or IDE genre | The readers are institutional hiring managers, not engineers |
| 2026-08-21 | Keep Archivo and Newsreader | Neither is on the overused list, and the pairing matches current premium practice |
| 2026-08-21 | Drop cream and terracotta | Measured deltaE 0.9 from the Anthropic brand cream and was recognised on sight |
| 2026-08-21 | Accent `#14452F`, not `#0F5C3F` | 40.3 versus 29.1 deltaE from the OpenAI green, and 9.4:1 versus 6.9:1 contrast |
| 2026-08-21 | Three figures promoted into the hero | The six second scan needs proof, not just a name |
| 2026-08-21 | AI mockup generation not run | The gstack design binary requires an OpenAI API key that is not configured |
