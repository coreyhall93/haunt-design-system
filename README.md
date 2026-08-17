# Haunt — Design System

Written 2026-08-17 as a standalone brief for Claude Design (or anyone/anything
else that needs to understand how this theme should look and feel without
reading the CSS). Every value below is pulled from the actual shipped code or
from decisions already made and recorded in `FUTURE_COREY.md` — nothing here
is invented for this document. Where something is still being tried rather
than decided, it's marked as such.

## 1. What this is

Haunt is a WordPress theme for daily blogging, forked from Automattic's
internal "Lately" theme — the design was kept, the product (Telegram capture,
friend-graph gating, subscriber walls) was stripped out entirely. The intent
is a site in the spirit of ma.tt: short posts and long posts are equally
first-class, and the habit of posting matters more than any format. Every
design decision below serves that: nothing ceremonial, nothing that makes a
ninety-second note feel like it needs to earn its place next to a long essay.

The visual language is quiet, editorial, and confident rather than
decorative. It reads as printed matter that happens to be on a screen — warm
paper, ink-like type, hairline rules — not as a SaaS product. No gradients as
decoration, no emoji as UI, no generic "AI-made" polish.

## 2. Color

| Role | Value | Notes |
|---|---|---|
| Ground (paper) | `#f5f3ee` | Warm grey with a hint of cream, never stark white. Every one of Corey's 19 saved font-pairing trials independently chose this exact value. |
| Ink (primary text) | `#23231f` | Near-black, warmed rather than a cold pure black. |
| Muted text | `#4a4842` | Secondary body-adjacent text. |
| Subtle text | `#86847c` | Dates, timestamps, byline-weight meta. |
| Hairline (thin) | `#e2dfd6` | Section dividers, the default rule weight. |
| Hairline (strong) | `#cfcbbf` | Input underlines, anything that needs to read as slightly more present than a thin divider. |
| Surface tint | `#ececeb` | Comment field background — barely off the paper, just enough to read as "field" rather than "text." |
| Accent — primary | `#63325e` (Plum) | Links, primary interactive color. Currently the live pick via the theme's own style switcher. |
| Accent — secondary | `#3a3d7a` (Indigo) | Nav underline, hover states, the permalink mark, small emphasis marks. |
| Accent — tertiary | `#8c2f39` (Oxblood) | One job only: the "Reply" / comment link. Never used anywhere else. |

The theme has a hand-rolled style-switcher (`styles/registry.php`) that swaps
which of Plum/Indigo plays primary vs. secondary. The description above is
the current live pairing.

**A subtle paper-grain texture** is painted directly onto the `<body>`
background (not a floating overlay), at low opacity (0.5) and
`background-attachment: fixed`, so the grain doesn't scroll with the page —
it reads as the texture of the page itself, like the paper has grain, not
like something is floating above the content.

**Explicitly rejected**, so they don't get re-proposed: rust or any orange
accent; a near-black accent color (a link that color is indistinguishable
from body text and signals nothing is clickable); any dark background as a
design target — the site optimizes for light only, a dark mode would be a
separate reader-facing toggle, not the default aesthetic.

## 3. Typography

Two families, five independently-tunable roles. The split is deliberate: one
family carries every literal *title* on the site (the site's own name, and a
post or page's own title), the other carries everything else that isn't
running text's polar opposite — navigation chrome, in-content headings, and
body copy — all sharing one family so they read as one voice at different
weights rather than competing typefaces.

**No italics, anywhere, full stop.** `font-style: normal !important` is
forced site-wide, and `font-synthesis-style: none` stops browsers from faking
an oblique when a face has no real italic. Emphasis is carried by weight, not
slant.

### 3a. Title family — Perfectly Nineties

A nostalgic, characterful serif (Jen Wagner Co.) — not a neutral workhorse
text face, it has real personality and a slightly vintage feel, closer to a
letterpress or typewriter-adjacent serif than a classical book serif. It's
used *only* for identity moments: the two places an actual "title" appears.
Never for body copy, never for in-content headings.

**Commercial license required** — not open source. A desktop license covers
design work; a separate web/embed license is needed to self-host it on the
live site. Confirm this is actually held before shipping.

Two roles, both fixed to this family, sized and weighted independently:

| Role | Where | Size | Weight | Tracking |
|---|---|---|---|---|
| **Site title** | The site's own name in the masthead ("my browser is haunted"). Present on every single page, unconditionally. | 18px | 700 | −0.015em |
| **Post title** | A post or page's own title, when it has one. Optional by design — asides and titleless posts intentionally hide theirs — but whenever a title shows, it's this family. | 27px | 700 | −0.015em |

### 3b. Reading family — Overused Grotesk

A Swiss-style neo-grotesque sans, clean and geometric, in the Helvetica /
Akzidenz lineage but with more character than a purely neutral grotesk — a
variable typeface with a full weight range. This is the "everything else"
family: it carries the site's UI chrome and its actual reading experience.

**Open source** — SIL Open Font License 1.1, free for any use including
commercial self-hosting, no license purchase needed.

Three roles, all drawing from this one family selection, each sized and
weighted on its own dial:

| Role | Where | Size | Weight | Tracking |
|---|---|---|---|---|
| **Nav** | The primary menu (Home / Archive, or a real WP menu if assigned) | 14px | 700 | 0em |
| **Heading** | Headings *inside* a post's own content — e.g. the emoji-prefixed subheadings like "📚 Reading" or "🔧 Building" in a roundup-style post. Not the post's own title. | 20px | 600 | −0.015em |
| **Body** | Running text. Line-height 1.7. | 16px | 400 | 0em |

### 3c. Meta text

Dates, timestamps, and byline-weight text ride on the body family regardless
of context — small (11–12px), frequently set in uppercase with wide tracking
(0.08–0.1em), and colored subtle (`#86847c`), so they read clearly as
secondary information without competing with a post's actual title or body.

### 3d. Measure

The reading column is capped at **760px**. This came out of the font-pairing
tool the same way the ground color did — every one of Corey's saved trials
converged on it independently. It's still technically an open question
whether 760px reads too wide at 16px body text (past the classic 45–75
character measure, closer to 95); that can only be judged by reading a
genuinely long post on the live site, not by looking at a specimen.

## 4. Layout & spacing

- **Right angles only.** Zero `border-radius` anywhere in the theme — not on
  buttons, not on form fields, not on the comment box. A single 6px radius was
  tried once and rejected: it was the only soft edge on an otherwise entirely
  flat, square page, and it read as borrowed from somewhere else rather than
  intentional.
- **Separation is whitespace plus a single hairline rule** — never a filled
  card, never a background tint, and specifically never ma.tt's technique of
  alternating post background colors (considered and rejected).
- **Feed rhythm:** an 88px gap plus a hairline rule between full posts on the
  home page.
- **Title-to-content gap:** 16px between a post's title and the start of its
  content (tightened 2026-08-17 — previously 24px on the home feed and 40px
  on a single post's date line, both of which read as too much air).
- **Comments:** 72px of top margin separates the comment section from the
  post body above it.

## 5. The permalink mark

A distinctive, fully-decided piece of the design, present identically on
every post footer across the home feed and archive.

**Construction:** a small `#` glyph (literally the hash / URL-fragment
character — the only symbol tried across two rounds of exploring roughly a
dozen glyphs that actually *means* something related to permalinks) rendered
in the secondary accent color, immediately followed by the post's full date
and time — e.g. `# Aug 6, 11:00 am` — then, with a gap, a "Comment" (or
"N comments") link in the tertiary accent color.

**Why the full date, not just the time:** chosen 2026-08-17 specifically
because the permalink text needs to stand on its own *out of context* — in a
feed reader, or anywhere else the surrounding post date has been stripped
away by whatever's displaying it.

**Hover:** the `#` mark and the date text slide together 3px to the right,
and the whole thing shifts to the primary accent color. The slide is a single
composited `transform`, kept on `translateZ(0)` in both the resting and
hovered states (not toggled on hover) — toggling it would promote and demote
the element's compositing layer and cause the text to re-rasterize a subpixel
off between states, which reads as a visible 1px jitter.

## 6. Components

### Subscribe block (Jetpack Subscriptions)

Treatment "S5" — the shipped choice, out of six explored options. The block
sits inside a distinct region marked by two hairlines only — one above, one
below — no box, no fill, no card. This is the same visual device the post
footer / feed separator already uses elsewhere on the page, so subscribing
doesn't introduce new visual vocabulary.

Inside: a one-line pitch ("A short letter most weeks."), then a row holding
the email field and the Subscribe control. Both are stripped of any box — the
field is a bare underline (1px, going to the accent color on focus) and the
button is text-only with a 2px rule beneath it that doubles in weight and
takes the accent color on hover. The row is aligned to its *bottom* edge, not
centered — centering aligns midpoints, and both the field's and button's
rules live on their bottom edges, so a centered row put those rules at
slightly different heights.

### Comment submit — "Treatment B"

Not a filled button. A text label with a rule underneath that doubles in
weight and switches to the accent color on hover — the identical mechanism
(see Motion, below) as the subscribe button, so every "text acting as a
button" moment on the site shares one visual grammar.

### Pagination (Older / Newer)

Plain text links, deliberately never styled as buttons — navigation goes to
a URL and changes nothing about the current view. Each arrow is
direction-aware: the "Newer" link's arrow points left and slides left on
hover, "Older" points and slides right — the arrow always moves toward where
the click actually takes you.

### What's deliberately not built

- No "read more" button — the title and the permalink footer already do
  that job.
- No share bar.
- No "load more" — pagination is honest and linkable instead.
- No cookie banner — nothing on the site sets a cookie that would need one.
- No featured images rendered in any template. The owner can still set them
  for social-card metadata; they're just never displayed on the page itself.

## 7. Motion

Two hard rules, both written down after real, reproduced bugs — not
theoretical guidance:

1. **Never animate `border-width`.** Growing a border changes the element's
   box, which reflows everything sitting on that baseline — the visible
   symptom is a wiggle (first caught on the comment submit control). Instead,
   draw the rule as an absolutely-positioned pseudo-element and animate
   `transform: scaleY()`, which cannot affect layout.
2. **Keep `translateZ(0)` on a transformed element in *both* its resting and
   hovered states — never add it only on hover.** Toggling it promotes and
   demotes the element to its own compositing layer, and the text
   re-rasterizes at a slightly different subpixel offset each time, which
   reads as a visible 1px vertical jitter (first caught on the permalink
   mark's hover slide).

Corollary: baseline alignment in a flex row (`align-items: center`)
recomputes whenever a child's box changes size mid-transition; `flex-end` or
explicit baseline alignment does not, which is why rows with motion in them
(like the subscribe row) are aligned to an edge rather than centered.

## 8. Masthead & navigation — current, shipped

Left-aligned, plain text, no chrome. A small circular avatar, the site title
(in Perfectly Nineties), and a dateline sit in one row; underneath, a simple
horizontal row of plain text links — Home / Archive by default, or a real
WordPress menu if one's assigned in that theme location. No background bar
behind the nav, no borders or pill shapes around individual links. The
current page is marked with a hairline underline, nothing louder.

## 9. Exploratory — researched, not built, not decided

Investigated 2026-08-17 at Corey's request, purely as reference — nothing in
this section is implemented, and it's included here only because it's an
active line of thinking about where the masthead could go next.

The source is **ped.ro/writing** (Pedro Duarte's personal site), specifically
its fixed header and the soft "fade" that appears as content scrolls beneath
it. Inspected directly (computed styles, not a guess):

- The nav is `position: fixed; top: 0`, left-aligned, just plain text links
  over the page — no background box of its own.
- Directly behind the nav text sits a separate `pointer-events: none` div,
  100px tall, with `background: linear-gradient(page-background 25%,
  transparent)`. This is the entire trick: it isn't a blur and isn't a
  box-shadow, it's a flat gradient that fades from the *page's own
  background color* at the top down to fully transparent. As content scrolls
  up underneath the fixed nav, it visually dissolves into the page's ground
  color over that 100px band before it ever reaches the nav's actual pixels
  — which is what reads as the nav floating softly "above" the content
  rather than sitting on a hard-edged bar.

If Haunt adopted this, the existing masthead structure (`.haunt-mast` +
`.haunt-tabs`, both already left-aligned per the section above) would need:
`position: fixed` on the masthead, one new div behind the nav text using
`linear-gradient(var(--haunt-bg) 25%, transparent)` in place of ped.ro's
black, top padding added to the page content so it doesn't start underneath
the now-fixed bar, and z-index ordering so the fade scrim sits behind the nav
text but above scrolling content.

## 10. Open questions, as of 2026-08-17

- **Final font pairing** is still being tried, not shipped. The current
  working combination — and the values used throughout this document — is:
  Perfectly Nineties for both title roles, Overused Grotesk for nav/heading/
  body at weights 700/600/400 respectively, site title 18px, post title
  27px, body 16px, 760px measure. Being judged on **near-white (`#fdfdfc`)**
  as a trial background for evaluating the pairing itself — this is not a
  change to the theme's decided ground color, which remains the warm grey
  `#f5f3ee` above.
- **760px measure** at current body size still needs judgment from reading
  an actual long post, not a specimen page.
- **Fixed masthead + fade scrim** (section 9) — proposed only, needs a
  decision before any code gets written.

## Licensing

| Font | Role | License |
|---|---|---|
| Perfectly Nineties | Both title roles | **Commercial** — Jen Wagner Co. Requires a paid license beyond personal use; separate desktop and web licenses. |
| Overused Grotesk | Nav / heading / body | **Open source** — SIL Open Font License 1.1, free for any use. |

Confirm the Perfectly Nineties license actually covers self-hosted webfont
embedding on a live commercial site before this pairing ships to production.
