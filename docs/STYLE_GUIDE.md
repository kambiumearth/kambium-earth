# Kambium style guide: web essentials

Master copy: docs/STYLE_GUIDE.md in github.com/kambiumearth/kambium-earth. Version 20261103. The visual reference is the Kambium Design System artifact in Claude (README, Human Touch Rules, components). The original Claude Design system (claude.ai/design/p/b60a532f-ac62-48e1-980f-3ab309e87897) closes 14 Dec 2026. The live code tokens are in each repo's style.css; keep this file, the Design System and the code in step.

Rules marked (Joshua, 3 Nov 2026) come from his review of the mentoring page sketch and apply to every page from now on.

## Grounds (only two, never a third)
- Parchment #F7F0E8: page ground, most reading. Headings rust-600 #6E3A22, body #5a2c1a.
- Bark #401810: dark sections, footers, primary button. Text parchment; sun #F7E511 for one or two highlighted words only.
- The light sand band #EEDFCC counts as parchment. A photo band counts as bark.
- **Parchment and bark always alternate.** Never two light sections next to each other (parchment or sand band) (Joshua, 3 Nov 2026). If removing or moving a section puts two light sections together, change a ground or the order.

## Colour tokens
rust-500 #8B3A19 (K and wordmark, links, focus ring) · rust-600 #6E3A22 (headlines) · soil-700 #401810 (bark ground, CTA) · ember-400 #C0783F (marks, the one bold mark in a drawing) · clay-300 #C8A088 (hairlines, muted text on bark) · sand-200 #E1C9A9 (secondary button, accents on bark, rules under fact lines) · parchment-100 #F7F0E8 · sun-500 #F7E511 (bark only, never on parchment) · moss-500 #5E6139 (status words).
No cool greys, blue, purple or decorative gradients. Neutrals always warm.

## Type
- Tenor Sans: all headings, ALL-CAPS lines, kickers. Regular only, no bold. Tracking .14em on caps (.2em kickers), leading 1.08 to 1.22.
- Lato: body 400 on the web (300 for leads), 700 for labels and buttons. Only 300/400/700.
- Web section titles in Title Case; poster headlines ALL CAPS. Never a third font. Never letterspace lowercase body.
- Body measure max 64ch.

## Shape
- **Only buttons are pill-shaped** (fully rounded), so a pill always means "tap me" (Joshua, 3 Nov 2026).
- Places, prices, dates and URLs that aren't links are fact lines: Tenor caps tracked .14em with a 1px hairline underneath. Status tags (Draft) are not pills either.
- **No cards.** Group items with space, 1px hairlines and type: a thin line above each item, the title in Tenor, one line of Lato under it, no boxes, rounded corners or shadows (Joshua approved this on 3 Nov 2026). At most one boxed element per page, usually the Tally form card.
- Buttons: primary bark #401810, hover rust #6E3A22; on bark a parchment button and an outline button; secondary sand, hover clay.

## Layout
- **Hero text at the top of every page is left-aligned**: kicker, heading, line, place and buttons start from the left edge of the container, never centred (Joshua, 3 Nov 2026).
- Container 1160px, reading column 720px. Section padding 6rem (tight 4rem); vary it between neighbouring sections.
- Neighbouring sections never share the same layout: mix a photo spread, a two-column text spread, a drawing, a list.
- Uneven splits (5/7, 4/8) and photos that bleed off an edge, rather than equal columns of boxes.
- **Section heads stay short.** A heading on its own is usually enough. Cut taglines, sublines and keyword rails under headings unless they carry a fact the reader needs (Joshua cut each one on the mentoring page, 3 Nov 2026).
- **Similar sections need a difference.** When light and dark alternate over several sections, the two light ones (and the two dark ones) can look the same. Give one of each pair a photo beside or behind it, and mirror sides (one photo bleeding left, one right) (Joshua, 3 Nov 2026).
- **Section guide on long pages** (screens 901px and wider with a mouse): a slim tab of small grain dots at the left edge, one per section, appearing after the hero. Hovering it (or keyboard focus) opens a parchment panel with every section name in Tenor caps; the current section's dot is ember. Dots only, no numbers. Hidden on touch screens and below 901px, where the Menu button does this job (Joshua, 3 and 16 Nov 2026).
- "⇡ Back to Top" once, at the end of long pages, not after every section.
- Mobile first: see WEB_GUIDE.md section 1b for breakpoints, tap targets and global components. On phones, buttons may shrink slightly so a pair fits on one line.

## Photos (Joshua, 3 Nov 2026)
- Real photos from Kambium's own gatherings only. No stock, no AI images.
- **No captions** unless Joshua asks for one on a specific photo. Alt text still describes every meaningful photo.
- Credit the photographer once, in the footer ("Photos: Melanie Pyne").
- **Sharp on retina screens.** Export from the original camera files at: full-width hero and photo bands 2400px wide; half-width photos 2000px; tall inline photos about 1700px on the long edge; portraits about 1400px. Never upscale a small export.
- **Phones keep the main person in frame.** Crop the same photo with object-position so the main person in the photo sits in the centre (on the mentoring hero that is Melina; Joshua chose this on 3 Nov 2026), and check that faces sit clear of text and buttons at 360, 390 and 430px. Don't swap in a different photo that loses them.
- Over a photo: the flat bark shade rgba(40,14,8,.6) by default. In the hero and the closing photo band only, a **soft bark fade** keeps faces and sky clear: start no darker than about 50% behind the words and ease out over several stops (for example .5, .4, .26, .12, .04, 0 by about 70% of the photo); on phones it runs top to bottom. Never a hard band of bark or a fade that turns the sky brown. Words over a photo get a very soft shadow (0 1px 18px, 45%) for legibility.
- Mentoring pages: Joshua and Melina appear only in the hero, Your Mentor and the closing band. The mentor portrait is the long-hair portrait (images/image04.jpg).

## Drawings
- **Riso texture on every drawn graphic** (rings, willow shoot, wheel): a soft tonal gradient inside fills in brand inks (heartwood sand denser at the centre, bark band clay, buds sand to clay, the one bold mark light ember to deep ember) plus light speckled knock-outs, like the white flecks in the printed logo. Thin lines get a finer, lighter speckle. Never on body text or photos.
- Speckle settings (approved 3 Nov 2026, after two reductions): SVG filter feTurbulence fractalNoise, baseFrequency .85, 2 octaves, feColorMatrix alpha row "0 0 0 -2.4 1.73", composited "in" with the shape. Thin lines: baseFrequency 1.6, alpha "0 0 0 -2 1.76".
- **Small dots and bullets are simple flat circles**: one brand colour with the same light grain. No gradient, highlight, shine or outline (Joshua, 3 Nov 2026).
- **Growth rings follow the rings in the Kambium logo**: thin, smooth, nested rings that never touch or cross, a sand heartwood at the centre and a clay bark band around the outside. Stages are a few rings drawn heavier, each with a dot and a fine leader line to its label (Joshua, 3 Nov 2026).
- **Circles that carry meaning:** growth rings for growth over a mentoring journey or training arc; the quartered four-directions wheel for journeys through the seasons, with each point placed at its real date (the Winter Arc). Draw on the circle and the four directions as Kambium teaches them through the 8 Shields model, without copying any nation's medicine wheel colours or symbols.
- Drawn stand-ins are replaced by scans of Joshua's or Melina's own ink or pencil drawings when they exist, in the same positions.

## Writing on the page
- No em dashes anywhere. No "not X, it's Y". Organisation name only "Kambium•Earth-Based Learning" or "Kambium•Earth". Only verified quotes, word for word.
- Mentoring pages speak as "I", including the mentor bio (first person). The bio comes from the kambium.earth hub bio, plus the iArts line.
- Say "journey" or "mentoring journey", never "container". Prefer "people" over "men and women".
- No prices for mentoring. Between sessions I reply to voice-note debriefs and quick questions within a day (Joshua, 16 Nov 2026); the discovery call is 30 minutes. Don't promise fixed days or times: they are "agreed with you before the first session".

## House rule override
The original design system lists the em dash as a workhorse. Joshua's standing rule wins: no em dashes anywhere.
