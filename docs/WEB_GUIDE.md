# Kambium websites: web dev guide

**Master copy:** https://github.com/kambiumearth/kambium-earth/blob/main/docs/WEB_GUIDE.md (read the latest at https://raw.githubusercontent.com/kambiumearth/kambium-earth/main/docs/WEB_GUIDE.md). Copies in Claude projects are snapshots; the GitHub file wins. After any structural change, update the GitHub file first, then refresh project copies. Style guide master: docs/STYLE_GUIDE.md in the same repo.

**Where to work:** the Claude project "Kambium Websites", in a chat started from the Claude desktop app with this computer linked (so Claude can use Chrome). One project for all website work; one chat per update session.

Version 20261102. Read this before any change to kambium.earth, sundays.kambium.earth or any page under them. It holds the rules, styling, hosting, DNS, file layout and workflow. If something here conflicts with an older handoff note, this guide wins. Update it (and its version date) whenever something structural changes.

---

## 1. Standing rules (always apply)

1. **Writing:** no em dashes anywhere. No "not X, it's Y" constructions. Plain, direct prose with personal and place-based grounding. Only verified, true quotes; never paraphrase a quote or put words in someone's mouth.
2. **Organisation name:** only "Kambium•Earth-Based Learning" or "Kambium•Earth" (with the • bullet).
3. **Dates in file and folder names:** no dashes, e.g. 20261102.
4. **Joshua's bio facts:** he has lived in Portugal 5 years (arrived 2021); Melina 8 years. Co-founded Kambium in 2024. Don't feature his Permaculture Design Certificate.
5. **Forms must be free.** Tally is the form tool.
6. **Every new event goes in two places:** the "Coming up" list on kambium.earth AND the Programs dropdown in the nav (on every page that has the nav).
7. **Bump the stylesheet version** (`style.css?v=YYYYMMDDx`) in every HTML file of that repo whenever style.css changes, so visitors never see a stale stylesheet.
8. **End of every update session:** ask Joshua whether he is finished with updates and whether he wants a debug run (checklist in section 10).
9. **Never edit without checking the live result afterwards.** Confirm the commit landed, then confirm the live page changed.
10. Joshua approves visual changes: for anything bigger than a text or link change, show a sketch or options first.
11. **Keep this guide current:** after any structural change, update docs/WEB_GUIDE.md in the kambium-earth repo in the same session.

---

## 1b. Responsive, mobile-first and global components (read before every change)

Most visitors arrive on phones (links from Telegram, WhatsApp, Instagram, email). Design and test for the phone first, then widen.

**Global components.** These exist on every page of every Kambium site and must stay identical in markup, CSS and behaviour. A change to one is a change to all, made in the same session, in every repo:
- Header and nav, including the **Menu button and phone menu** (CSS block marked "Site menu: GLOBAL component", script before `</body>`)
- Footer (© line, Policies, Back to top, Cookie settings, NIF line)
- Cookie banner + Google Analytics consent script
- Stylesheet link with version tag
- Floating phone CTA (`.mobile-book`, "Join an event" on kambium.earth, "Book" on Sundays)
- Tally embed loader, fonts, favicon, og/meta pattern

Before finishing any change, ask: "Does this touch a global component? Which other pages and repos have it?" Then apply it everywhere and test everywhere. Pages today: kambium.earth `/`, `/boys`; sundays.kambium.earth `/`.

**Breakpoints (shared by all sites):**
- ≤900px: Menu button replaces the nav (covers phones AND tablets; links hidden at this width must never be unreachable)
- ≤760px: phone layout, single columns, floating CTA
- >900px: full nav, hover/focus dropdowns

**Mobile-first rules:**
1. Every nav link must be reachable at every width. Never hide a link without giving it a place in the phone menu.
2. Nothing may depend on hover alone. Dropdowns also open on keyboard focus, and on ≤900px they are listed inside the menu.
3. Tap targets at least 44px tall, with space between them.
4. No horizontal scrolling at 360px. Long words and buttons must wrap.
5. Body text at least 16px on phones; line length max 64ch.
6. Embeds (YouTube, Tally, maps) must work on phones: video uses the tap-to-play poster plus a "Watch on YouTube" link; Tally uses dynamic height.
7. Fixed elements (floating CTA, cookie banner, open menu) must not cover form fields or each other in a way that blocks use.
8. Images: `max-width:100%`, sensible `object-position` for phone crops, `loading="lazy"` below the fold.
9. Sticky header height is accounted for when jumping to anchors (`scroll-margin-top`).

**Test matrix for every change (Playwright in the cloud workspace, see section 8):** 360, 390 (iPhone), 768 (tablet portrait), 900, 1024 and 1440 wide. Check: no overflow, Menu opens and closes and lists every link, dropdown works on desktop, forms and video load, floating CTA visible on phones. Then check one real page in Chrome.

---

## 2. Sites, repos and URLs

| Site | Repo (GitHub, account kambiumearth) | Pages source | Status |
|---|---|---|---|
| https://kambium.earth (+ www) | kambiumearth/kambium-earth (public) | main, root | Live since 30 Oct 2026 |
| https://sundays.kambium.earth | kambiumearth/sundays-kambium-earth (public) | main, root | Live, HTTPS enforced |
| https://events.kambium.earth | Ticket Tailor box office "kambiumearth" | (not GitHub) | Live |

Pages on kambium.earth:
- `/` → `index.html` (the hub)
- `/boys` → `boys.html` (Kambium for Boys pre-registration, noindex)
- `/youth` → `youth.html` (redirect page to /boys, keep it so old links work)
- `carrd-archive.html` (copy of the old Carrd site, reference only, not linked)
- `docs/WEB_GUIDE.md`, `docs/STYLE_GUIDE.md` (these guides; public but not linked)

Retired: Carrd. The Carrd hub (site 4818175346712276) and the Carrd Sundays site (1249179278131184) should be unpublished by Joshua if not done yet.

---

## 3. Hosting, DNS and HTTPS

**Registrar and DNS:** Infomaniak (Manager → Domains → kambium.earth → DNS zone). Nameservers ns11/ns12.infomaniak.ch. Advanced view is a plain BIND text editor; versions can be restored from "Current version".

**Current zone (2 Nov 2026), what each record is for:**

| Name | Type | Value | Purpose |
|---|---|---|---|
| @ | A | 185.199.108.153 / .109.153 / .110.153 / .111.153 | kambium.earth → GitHub Pages |
| www | CNAME | kambiumearth.github.io. | www → GitHub Pages |
| sundays | CNAME | kambiumearth.github.io. | Sundays page |
| events | CNAME | custom.tickettailor.com. | Ticket Tailor box office (kambiumearth) |
| @ | MX 10 / MX 20 | mail.protonmail.ch. / mailsec.protonmail.ch. | Email (Proton) |
| @ | TXT | v=spf1 include:_spf.protonmail.ch ~all | Email SPF |
| @ | TXT | protonmail-verification=… | Proton domain verification |
| @ | TXT | google-site-verification=… | Google |
| 20250718._domainkey | TXT | v=DKIM1… | Email DKIM |
| _dmarc | TXT | v=DMARC1; p=quarantine | Email DMARC |
| _domainkey | NS | ns11/ns12.infomaniak.ch | DKIM delegation |
| autoconfig, autodiscover | CNAME | infomaniak.com. | Legacy mail autoconfig |
| community | A | 172.66.0.70 | OLD Carrd address. Delete if unused (open item) |

**Never touch** MX, TXT, DKIM, DMARC, _domainkey, sundays or events records when changing the website.

**Email:** info@kambium.earth is on Proton (Joshua's Proton Family plan). Infomaniak stays registrar only.

**GitHub Pages custom domains:** kambium-earth repo has `CNAME` file = kambium.earth. sundays repo has its own CNAME = sundays.kambium.earth.

**HTTPS:** the certificate for kambium.earth is issued and https works. "Enforce HTTPS" (repo Settings → Pages) did not stay ticked when clicked by script; Joshua should tick it by hand. Sundays has HTTPS enforced.

**Caching:** GitHub Pages caches pages up to 10 minutes (cannot be changed). The stylesheet version tag (rule 7) makes CSS changes show at once; HTML text can lag up to 10 minutes.

---

## 4. Connected services

| Service | Detail |
|---|---|
| **Ticket Tailor** | Two box offices: **kambiumearth** (events.kambium.earth) and **kambiumpartners** (tickettailor.com/events/kambiumpartners/…). events.kambium.earth shows only kambiumearth events, so the site's own Events section is the full list. The Claude Ticket Tailor connector reaches only the kambiumearth box office. |
| Sundays event | Ticket Tailor series es_2482274; Book links go to checkout for 29 Nov (ev_9314775). |
| Foundation Training | kambiumpartners event 2012165: Deep Nature Connection Mentoring Foundation Training, 11 to 14 Mar 2027, Relíquias (Vale da Lua). Early bird €265 until 5 Jan 2027, register by 14 Feb 2027. |
| **Tally** | Contact form aO99oq "Write to us" (home page, free plan, owner email on; cannot set reply-to). Kambium for Boys pre-registration rDyoBR (boys page, password removed 2 Nov 2026). Embeds use `data-tally-src` + Tally embed.js + a 2.5 s fallback loader. |
| **Proton Calendar booking** | Free discovery call: https://calendar.proton.me/bookings#GZW1XOMPQpm2MHKZGPfYGZZsphySYwBGRJtuwtjv81U= |
| **Google Analytics 4** | Account "Kambium Earth", property kambium.earth, stream "Kambium websites", ID **G-C5XQDPP2Z3**, on every page. Consent Mode v2: denied by default, granted only after "Yes, that's fine". Choice stored in localStorage key `kc`. Footer "Cookie settings" reopens the banner. Joshua's uBlock blocks his own visits. To do: add the ID in Ticket Tailor settings; mention GA in the Policies doc. |
| **Substack** | joshuaglass.substack.com, Articles section auto-loads the 3 latest posts via rss2json, with a static fallback of 3 posts in the HTML. |
| Telegram | https://t.me/kambiumearth |
| Instagram | https://instagram.com/kambium.earth |
| YouTube | 4-day program video 8SbpHIgsKYU, shown as a tap-to-play poster (loads youtube-nocookie on tap) with a "Watch on YouTube" link underneath. |
| Policies | Proton Drive link in the footer. |
| Joshua's site | https://www.joshuaglass.net/mentoring-young-men (Mentoring nav link) |

---

## 5. File structure

### kambium-earth repo
```
index.html        hub page
boys.html         Kambium for Boys (noindex)
youth.html        redirect to /boys
style.css         shared styles (Sundays base + hub additions appended at the end)
CNAME             kambium.earth
.nojekyll
docs/             WEB_GUIDE.md (this guide, master copy), STYLE_GUIDE.md
images/           photos (container01.jpg hero, image02-14.jpg, gallery*.jpg, logo.webp,
                  sundays.webp, og-home.jpg 1200x630, favicon.png, apple-touch-icon.png)
shapes/           riso masks: slab.webp, bium.webp, u.webp, b.webp
carrd-archive.html
```

### sundays-kambium-earth repo
```
index.html, style.css, CNAME, images/ (incl. og-sundays.jpg), shapes/
```

### Joshua's MacBook Air (macbook-air-jg-local)
- `~/KAMBIUM/` contains: `Claude outputs`, `Kambium Media`, `Learning Materials KEBL`, `NCX Promo (Nature Connection)`, `.obsidian` (an Obsidian vault).
- Website working files and photo candidates live in **Proton Drive** under `kambium.earth website/` (e.g. `sundays-site/_tmp/hubhero/` holds resized hero options).
- The repos are NOT cloned on the Mac. GitHub is the only source of truth for site code. Nothing on the Mac needs syncing after an edit.
- Video editing: DaVinci Resolve on the Mac (`~/DaVinci Resolve Media`).

To give Claude file access in a future chat, connect a folder in the Claude desktop app (e.g. `~/KAMBIUM/Kambium Media`).

---

## 6. Page structure

### Nav (same on index.html and boys.html)
About (`#about`) · **Programs ▾** (link to `#events`; dropdown: Community Sundays → sundays.kambium.earth, Mentoring Foundation Training → Ticket Tailor 2012165, Boys → /boys) · Articles (`#articles`, hidden under 900px) · Mentoring (joshuaglass.net, hidden under 900px) · Contact (`#contact`, dark capsule).
On boys.html every `#anchor` is written `/#anchor`.
At 900px and below (phones and tablets): a "Menu" capsule button opens the full list, dropdown items shown indented. Same component on sundays.kambium.earth. The script sits just before `</body>`.

### kambium.earth home sections (ids)
1. Hero (`.hero.home`, photo container01.jpg, text left-aligned, buttons "Join an event →" #events and "Write to us" #contact)
2. `#about` What we do: three cards, each with one bottom-aligned button (`.offer-btn`): Book a discovery call (Proton) / Join a Community Sunday / Foundation Training, March 2027
3. Photo strip
4. `#team` Your Guides (Joshua, Melina). `#lineage` (Jeannine Tidwell, Tim Corcoran) is HIDDEN with the `hidden` attribute until Joshua rewrites it
5. `#events` (dark): Sundays feature card → "Coming up" programme list (`ul.prog`) → Telegram text line → `#past` collapsed `<details>` list (text only)
6. `#taste` light band: 4-day program video
7. `#articles` Substack feed (`#kb-feed`)
8. `#apply` Work or volunteer (sand)
9. Photo band
10. `#contact` (dark) Write to us: links + Tally aO99oq
11. `#order-complete` (shown only when linked, Ticket Tailor return page)
12. Footer: © line, Community Sundays, Policies, Back to top, Cookie settings; "Joshua Glass · NIF 320036120"
13. Floating "Join an event" capsule on phones (`.mobile-book`)

### boys.html
Intro (kicker "Kambium for Boys · Winter 2027", h1, paragraph, Who / Where / When / With, "Skip to the questions ↓" button) + photo image03.jpg, then `#questions` Tally rDyoBR card, then email line. Facts come from the Tally form: boys 9 to 14, Sintra-Colares (place TBC), January to May 2027, Joshua Glass and Dylan Vincent.

### sundays.kambium.earth sections (ids)
`#glance` The Day · `#sundays` The Sundays · `#join` (nav label "Price") · `#details` · `#families` · `#guides` · `#faq` · `#contact`. Nav has no link back to kambium.earth (Joshua removed it); the logo links to kambium.earth. Book button goes to Ticket Tailor checkout. Has the global Menu button at 900px and below (added 2 Nov 2026).

---

## 7. Styling

Source: Kambium Design System (Claude Design, extracted 23 Oct 2026; master written copy docs/STYLE_GUIDE.md in this repo; standalone Claude Design closes 14 Dec 2026, export a copy).

Where the style actually lives: the live sites use the `:root` tokens and component CSS in each repo's `style.css` (kambium-earth and sundays-kambium-earth share the same base). A style change is a global change: update both style.css files, bump both version tags, and update docs/STYLE_GUIDE.md so the written guide matches the code. Current stylesheet version: 20261102e.

**Grounds:** only two. Parchment #F7F0E8 (page, cards, most reading) and Bark #401810 (dark sections, footer, primary buttons). The site also uses `--sandbg #EEDFCC` for the light video and Work-with-us bands. Never add a third ground colour.

**Tokens (in style.css :root):**
`--parchment #F7F0E8` · `--bark #401810` · `--rust #8B3A19` (links, kickers, focus) · `--rust6 #6E3A22` (headlines) · `--ember #C0783F` · `--clay #C8A088` (muted text, hairlines) · `--sand #E1C9A9` (capsules, secondary button, text accents on bark) · `--sandbg #EEDFCC` · `--moss #5E6139` · `--body #5a2c1a` · `--wrap 1160px` · `--pad clamp(20px,5vw,56px)` · `--sec clamp(56px,8vw,96px)` · `--nav-h 84px` (64px on phones).
Sun #F7E511: on bark only, one or two highlighted words at most. No cool greys, blues, purples or decorative gradients.

**Type:** Tenor Sans for all headings, caps lines, kickers and rails (regular weight only, caps tracked .14 to .22em). Lato for body (400 on the site; 300/400/700 allowed). Section titles in Title Case. Never a third font. Body measure max 64ch.

**Components (class names):**
- Buttons: `.btn.primary` (bark), `.btn.light` (parchment on dark), `.btn.ghost` (outline on dark), `.btn.sandbtn` (sand). All capsules. Outline on parchment: `.offer-btn`.
- `.kicker` small tracked caps label above an h2. `.subhead` caps subheading. `.rail` keyword rail (words separated by • in clay).
- `.sec` section, `.sec.dark` bark section, `.sec.sand` sand section. Each `.sec` gets riso grain and a large faded logo shape via `::before` (set per section with `--sm` mask, `--sc` colour, `--so` opacity).
- `.photo` wrapper (rounded, striped placeholder if the image fails; images use `onerror="this.classList.add('missing')"`).
- `.form-card` parchment card holding Tally iframes.
- `.prog` Coming up list rows: `.pdate` (big day number + month/year), `.pthumb` 72px thumbnail, `.ptext` (h4 title + place), Book button.
- `.yt` tap-to-play video poster.
- `.menu-btn` + `.nav.open` global phone and tablet menu.
- Cards: radius 10 to 16px, 1px clay hairline (55% on parchment, 35% on bark), soft warm shadow, no coloured left borders.

**Layout:** container 1160px, reading column 720px, breakpoints 900px (Menu button, single-column cards) and 760px (phone layout, floating Join button).

---

## 8. How Claude makes changes

Claude edits through the **Claude in Chrome extension**, which is logged in to GitHub (kambiumearth) and Infomaniak on Joshua's Mac. Joshua's computer must be awake with Chrome open. The desktop app's built-in Browser pane is NOT logged in to GitHub.

**Commit a text file change:**
1. Open `https://github.com/kambiumearth/<repo>/upload/main` in a Chrome tab.
2. In JS: get the latest commit SHA from `api.github.com/repos/kambiumearth/<repo>/commits?per_page=1` (from the Chrome tab), fetch each file at that SHA from `raw.githubusercontent.com` (fetching `/main/` can be stale for minutes), apply exact string or regex replacements that must match exactly once, build `File` objects, attach them to `input[type=file]` with `DataTransfer`, set `[name=message]` with the native value setter, then click "Commit changes".
3. Keep each JS call under about 40 seconds (long sleeps time out). Click Commit in a separate call if needed and confirm via the API that the commit message appears.
4. Verify live: fetch the page with `?x=<timestamp>` and `cache:'no-store'` until the change appears (deploys take 1 to 3 minutes), then check visually.
5. To reuse the same edit across repos, store the edit code in `localStorage` on github.com and run it in each repo's upload tab.

**Binary files** (images): fetch as Blobs from raw.githubusercontent.com inside the upload tab. New images: draw in a canvas on a live Kambium page, then hand the Blob to the upload tab.

**GitHub settings pages** block screenshots; use JS only there.

**Phone-width testing:** in the cloud workspace, download the repo files from raw.githubusercontent.com into a folder and render with Playwright at the test-matrix widths, external requests aborted. The cloud cannot reach *.github.io, kambium.earth, dns.google or most external hosts (proxy 403), and has no GitHub token. Check DNS by opening `https://dns.google/resolve?name=…&type=…` in Chrome.

**DNS edits:** Infomaniak DNS zone → Advanced view textarea; set the value with the native setter + input event, Save, then check Google DNS. Only with Joshua's explicit go-ahead.

**Claude cannot:** create GitHub repos, sign in to anything, enter the NIF or any financial data, or tick some GitHub settings that need a real click.

**After editing:** if Joshua edits files on GitHub himself, check his diff for accidental deletions (on 2 Nov an edit removed the hero buttons and a closing `</div>`).

---

## 9. Recurring tasks

**Add an event**
1. Add a row to `ul.prog` in index.html (date, 72px thumbnail, title, place and key price/deadline, Book link to that event's own checkout in whichever box office).
2. Add it to the Programs dropdown in index.html AND boys.html.
3. If the event has a page-level offer (like the Foundation Training card button), update that too.
4. When it ends: remove it from Coming up and the dropdown, add it to the top of the `#past` list.

**Change styles:** edit style.css in both repos, then bump `?v=` in every HTML file.

**New page:** copy the head, header (with Menu button) and footer/scripts from index.html, fix `#anchor` links to `/#anchor`, give it its own title, description, canonical and og tags, add `noindex` if it's not public yet, add it to the nav where Joshua says, test at all widths.

**Unhide lineage:** remove the `hidden` attribute from `div#lineage` once Joshua sends the new text.

**Social previews:** after changing an og image, run Facebook Sharing Debugger "Scrape Again". Use `?v=` on og image URLs.

---

## 10. Debug and QA

**Weekly scheduled task** "Weekly Kambium website debug": Mondays 08:43 Lisbon, cloud only, read-only, sends a summary to Joshua's phone and saves a dated report in the Claude project.

**Debug checklist (end of session or on request), at the test-matrix widths:**
1. HTML validity (`npx html-validate@8` on raw files): unclosed tags, duplicate ids.
2. Every local asset referenced in HTML/CSS exists in the repo.
3. Every external link and embed responds (check from Chrome; the cloud can't reach most hosts).
4. Phones and tablets: no horizontal scroll, Menu button opens and lists every link, tap targets 44px, floating CTA visible, Tally forms load, video poster plays or falls back to YouTube.
5. Desktop: dropdown works on hover and keyboard focus, hero buttons present.
6. Global components identical on every page and repo.
7. Events: no past dates under Coming up or in the dropdown; site dates match Ticket Tailor.
8. Meta: title, description, canonical, og image reachable; GA tag and cookie banner present.
9. No leftover placeholders ("TODO", "KEY_PENDING", "lorem").

**Last full debug (2 Nov 2026):** HTML valid on all pages (only a cosmetic lowercase doctype note), all local assets present, no horizontal overflow at 360 to 1440px. Fixed: no menu on phones and tablets (global Menu button on both sites, 44px targets), video black on phones (tap-to-play poster plus YouTube link).

---

## 11. Open items

- Tick "Enforce HTTPS" for kambium.earth (Joshua, by hand).
- Unpublish both Carrd sites (Joshua).
- Delete the old `community` DNS record if unused.
- Lineage text rewrite, then unhide.
- Foundation Training thumbnail: Melina is updating the Ticket Tailor image (Todoist task, label `melina`).
- Crossed-out €300 on the All Six Sundays card: keep or remove?
- Testimonials: only Mathilde's verified quote so far.
- Melina's bio check.
- Add GA ID in Ticket Tailor; mention GA in the Policies doc.
- Later: automatic events sync (daily GitHub Action reading both Ticket Tailor box offices via API; Joshua adds the API keys as GitHub secrets).
- Lesson logged 2 Nov 2026: the phone menu was added to kambium.earth but not to Sundays, and tablets (761 to 900px) had hidden nav links. Both fixed. Always treat nav, footer, banner and CTA as global components (section 1b).
