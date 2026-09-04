# Theme tokens — The Healing Haven Employee Manual

For whoever themes the docs site. The Markdown content is unstyled by design; apply these at the platform level (in Mintlify, `docs.json` already carries the primary set).

This is a **web surface**, so it uses the social/web brand (Fraunces + Manrope), not the email/PDF brand (Fraunces + Inter). Don't conflate them.

## Light mode

| Token | Hex | Use |
|---|---|---|
| Charcoal | `#252220` | Primary text, dark surfaces, headings |
| Charcoal soft | `#3A352F` | Body text |
| Gold | `#B89968` | Accent, links, rules |
| Gold deep | `#8C7344` | Accent text on light backgrounds (passes AA on cream) |
| Gold light | `#DDC9A3` | Subtle fills, hover states |
| Cream | `#F5EEE0` | Page ground |
| Cream light | `#FAF6EE` | Cards, sidebar |
| Cream deep | `#ECE2CE` | Wells, hairlines, table borders |
| Stone | `#A89F92` | Muted text, captions |
| Fire | `#A53F3F` | Critical / stop (use for "Important" callouts) |
| Wood | `#7A8B6F` | Success / affirmative |
| Water | `#7BA7A6` | Informational (use for "Why" callouts) |

## Dark mode

| Token | Hex | Use |
|---|---|---|
| Ground | `#252220` | Page background (Charcoal) |
| Surface | `#2E2A26` | Cards, sidebar |
| Surface raised | `#3A352F` | Wells, code blocks, table header |
| Hairline | `#4A443D` | Borders, rules |
| Text | `#F5EEE0` | Primary text (Cream) |
| Text soft | `#DDC9A3` | Body text (Gold light) |
| Text muted | `#A89F92` | Captions (Stone) |
| Accent | `#DDC9A3` | Links, active nav (Gold light: contrast on charcoal) |
| Accent hover | `#B89968` | Link hover (Gold) |
| Fire | `#C95A5A` | Critical, lifted for dark contrast |
| Wood | `#94A688` | Success, lifted |
| Water | `#8FBDBC` | Informational, lifted |

## Typography

| Role | Family | Notes |
|---|---|---|
| Display / headings | Fraunces | Google Fonts. Optical size axis on; weight 500–600 for H1–H2, 500 for H3. |
| Body | Manrope | Google Fonts. Weight 400 body, 600 for bold. 16–17px base, 1.6 line-height. |
| Code / monospace | System mono | Only for the `OPEN-` markers and slugs. |

## Callout mapping (Mintlify)

The manual uses plain blockquotes with a bolded lead so it renders anywhere. If you convert them to Mintlify components later:

| Lead | Component | Color |
|---|---|---|
| `> **Important.**` | `<Warning>` | Fire |
| `> **Why.**` | `<Info>` | Water |
| `> **Not yet set.**` | `<Note>` | Gold |

## Mintlify docs.json mapping

- `colors.primary` → Gold deep `#8C7344` (readable on cream)
- `colors.light` → Gold light `#DDC9A3` (dark-mode emphasis)
- `colors.dark` → Gold `#B89968` (buttons, hover)
- `background.color.light` → Cream `#F5EEE0`
- `background.color.dark` → Charcoal `#252220`
- `fonts.heading.family` → Fraunces; `fonts.body.family` → Manrope
- `theme` → `willow` (stripped-back, reads like a document). `mint` is the safe alternative.

## Logo and favicon

`docs.json` references `/logo/light.svg`, `/logo/dark.svg`, and `/favicon.svg`. A placeholder gold-mark favicon is included. Replace the logo files with the practice's wordmark (charcoal on light, cream on dark) before publishing; until then, remove the `logo` block from `docs.json` so the build doesn't 404.
