# Kambium style guide: web essentials

Master copy: docs/STYLE_GUIDE.md in github.com/kambiumearth/kambium-earth. Extracted from the Kambium Design System in Claude Design (claude.ai/design/p/b60a532f-ac62-48e1-980f-3ab309e87897), 23 Oct 2026. Standalone Claude Design closes 14 Dec 2026; export a copy. The live code tokens are in each repo's style.css; keep this file and the code in step.

## Grounds (only two, never a third)
- Parchment #F7F0E8: page ground, cards, most reading. Headings rust-600 #6E3A22, body bark-800.
- Bark #401810: dark sections, footers, dark hero, primary button. Text parchment-white; sun #F7E511 for one or two highlighted words only.
- Max two background colours per artefact: parchment + bark (or parchment + photo). So "alternating sections" = parchment / bark. (The site also uses sand-bg #EEDFCC for light bands.)

## Colour tokens
rust-500 #8B3A19 (K and wordmark, focus ring) · rust-600 #6E3A22 (headlines) · soil-700 #401810 (bark ground, CTA) · ember-400 #C0783F · clay-300 #C8A088 (muted text, hairline borders, keyword rail) · sand-200 #E1C9A9 (info capsules, secondary button) · parchment-100 #F7F0E8 · sun-500 #F7E511 (bark only, never on parchment) · moss-500 #5E6139 (tags, status).
No cool greys, blue, purple or decorative gradients. Neutrals always warm.

## Type
- Tenor Sans: all headings, ALL-CAPS lines, keyword rails. Regular only, no bold. Tracking .14em on caps (.22em rails), leading 1.08 to 1.22.
- Lato: body 300, UI/meta labels 700. Only 300/400/700.
- Web section titles in Title Case; poster headlines ALL CAPS. Never a third font. Never letterspace lowercase body.
- Body measure max 64ch.

## Shape
- Capsule (fully rounded): prices, URLs, info blocks, primary CTAs.
- Panels/cards: radius 10 to 16px (26px for big feature panels), parchment-raised fill, 1px clay hairline border at 55% (35% on bark), soft warm-brown shadow. No coloured left borders.
- Buttons: primary bark #401810, hover rust #6E3A22; secondary sand, hover clay.

## Layout
- Container 1160px, reading column 720px. Section padding 6rem (tight 4rem). "⇡ Back to Top" at the end of each section.
- Signature ornament: keyword rail of tracked uppercase words separated by • in clay.
- Mobile first: see WEB_GUIDE.md section 1b for breakpoints, tap targets and global components.

## House rule override
The design system lists the em dash as a workhorse. Joshua's standing rule wins: no em dashes anywhere. Organisation name only "Kambium•Earth-Based Learning" or "Kambium•Earth".
