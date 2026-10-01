# CLAUDE.md · Lieslcare

Standing orders for every session in this repository. Read this file in full before changing anything. If the owner's instructions in a session conflict with it, follow the owner and propose an update to this file in the same PR.

**Lieslcare** is a one-page care guide for Liesl, a Ragamuffin cat, written as a Habsburg-era Baedeker in the voice of the k. u. k. court. Its readers are the people who look after her (sitters, friends, family), almost always on a phone and often mid-task. Every flourish serves that reader; no instruction may be lost to ornament.

---

## 1. Structure and publishing

### Files

| Path | Purpose |
|---|---|
| `index.html` | The entire site: markup, inline `<style>` (≈460 lines) and inline `<script>` (≈155 lines). There are no other HTML, CSS or JS files. |
| `README.md` | One-line GitHub description. Not linked from the site. |
| `CLAUDE.md` | This file. |
| `LieslWaltz.mp3` | Background waltz: 13 MB, 8 min 59 s, loops; loaded only when it starts playing. Johann Strauss II, *An der schönen blauen Donau*, Op. 314, performed by the United States Marine Band, according to the file's original name (added in `fd8e1dd`, renamed in `ed442d7`). A US-government recording is public domain in the US. The ID3 comment lists YouTube URLs, so confirm the source before relying on this. |
| `IMG_*.jpeg`, `Liesl_Profile.png`, `Liesl_Profile2.jpg` | iPhone photographs, 960×1280 or 1280×960 (the profiles are 860×852). See the image register. |

The repository has no `.github/`, workflows, `_config.yml`, `.nojekyll`, `CNAME` or `package.json`.

#### Image register

The cover slideshow (`coverSlides` in the script) shows fifteen portraits in this order: `IMG_1243` (also `#slide-a`), `IMG_0197` (also `#slide-b`), `IMG_1799`, `IMG_0132`, `IMG_1868`, `IMG_4280`, `IMG_2041`, `IMG_0191`, `IMG_2816`, `IMG_3594`, `IMG_2943`, `IMG_5849`, `IMG_3345`, `IMG_0175`, `IMG_3351`. Each entry carries its alt text and its framing (see "Framing" in §7).

| File | Also used | Shows |
|---|---|---|
| `IMG_1243` | | Liesl reclining on a patterned rug, gazing upward |
| `IMG_0197` | | seated on a red throw, mouth open |
| `IMG_1799` | | on a green sofa, forepaws extended |
| `IMG_0132` | | reclining against a red throw |
| `IMG_1868`, `IMG_2816` | | seated on rugs (landscape / drawing room) |
| `IMG_4280` | | seated upright on a red throw |
| `IMG_2041` | | seated on a wooden stand |
| `IMG_0191`, `IMG_0175` | | lying on a rust-coloured bedspread (landscape) |
| `IMG_3594`, `IMG_2943` | | reclining on dark throws and cushions |
| `IMG_5849` | Ch. III figure | seated in a wooden stand, lit gold |
| `IMG_3345`, `IMG_3351` | | profile gazing upward; looking up, wide-eyed |
| `IMG_4468` | Dedication cameo (`#hommage`) and `og:image` | close portrait wearing a yellow flower collar |
| `IMG_4812` | Ch. I figure | frontal portrait |
| `IMG_4881` | Ch. II cameo | on a rust-coloured bedspread |
| `IMG_4894` | Ch. I lightbox "Preparation Precepts", plate 1 | closed lower cabinet beside the range |
| `IMG_4895` | plate 2 | the same cabinet, open: a food bag and a bottle |
| `IMG_4896` | plate 3 | jars, a can and a glass bowl on the counter |
| `IMG_4898` | plate 4 | food spread on a metal tray, bowl beside it |
| `IMG_4899` | plate 5 | the tray inside a countertop oven |
| `IMG_4901` | plate 6 | the finished bowl |
| `IMG_4900` | Ch. I lightbox "Royal Water Levels" | the water fountain, filled |
| `IMG_1603`, `IMG_3023`, `IMG_3233`, `IMG_3353`, `IMG_7867`, `IMG_9225` | unused (in the slideshow in earlier versions) | portraits; `IMG_9225` shows a window perch |
| `IMG_9769` | unused, never referenced | Liesl asleep |
| `Liesl_Profile.png`, `Liesl_Profile2.jpg` | unused (`Liesl_Profile2.jpg` was the profile image in early versions) | the same profile portrait (PNG 1 MB, JPG 156 KB) |

Pages still publishes unused files, so anyone can open them by URL. Delete them only on the owner's word.

### index.html anatomy

1. `<head>`: meta and Open Graph tags, an inline-SVG crown-emoji favicon, Google Fonts, Remix Icon.
2. `<style>`, divided by banner comments: tokens (`:root`), ribbon navigation, Baedeker welcome overlay, horizontal book, leaf variants, frontispiece, duet, gilt figures, rubric cards, rite list, video shrine, decree court, page arrows and waltz toggle, lightbox, "MOTION COURTESY" (reduced motion).
3. `#welcome`: the red Baedeker cover, with imprint, "BAEDEKER'S", "Kaiserin Liesl" in script, an arched slideshow button, the Sei Shōnagon precedent, the tap hint and the colophon. A tap turns the cover away like a page and starts the waltz.
4. `nav.ribbon`: fixed chapter ribbon. Every link has an `aria-label`. At 720 px and below, the `.word` spans hide, Roman numerals remain, and the Cover link shows a book icon (`.cover-icon`).
5. `main#book.book`: a horizontal scroll-snap book. Each chapter is a viewport-wide `section.page`:

   | id | Ribbon | Leaf | Contents |
   |---|---|---|---|
   | `hommage` | Cover | parchment | dedication cameo, Hoffmann epigraph |
   | `banquet` | I · Bankett | parchment | evening meal, dry food, treats and catnip, water fountain; two lightboxes |
   | `diversions` | II · Zerstreuungen | parchment | play |
   | `rituals` | III · Rituale | parchment | portrait (`IMG_5849`) beside coat, eyes and hygiene rubrics |
   | `alchemy` | IV · Alchemie | `.velvetine` (dark) | Litter-Robot 4 procedure, YouTube embed |
   | `decree` | Royal Decree | `.oxbloodine` (red) | veterinarian (Toebeans and Tails, 5561 Cardinal Place), 24-hour emergency hospital ("Nachtdienst": VEG ER, 4525 Duke Street, with phone) and household contacts, medical notes, copyright line |

6. Page arrows (768 px and wider only, on dark discs), `<audio loop preload="none">` with `#waltz-toggle`, and the `#lightbox` dialog.
7. `<script>`: a `reduceMotion` media query used throughout; the cover slideshow (`coverSlides`, each with `src`, `alt` and `frame`, the inline style applied while the slide is hidden; 3.8 s interval, never started under reduced motion, stopped once the book opens, fetching one portrait ahead); waltz start (attempted at load and on first gesture) and toggle; welcome overlay; `turnPage()` pagination; an IntersectionObserver that scrolls pages back to the top once they leave view; the lightbox (`precepts` array of `src`/`alt` plates, fetched on first opening, plus fountain mode); keyboard handling.

To add a chapter, copy a `section.page`, give it an id, renumber the eyebrow ("Chapter the Fifth") and medallion, and add `<a href="#id">V<span class="word"> · Wort</span></a>` to the ribbon before the decree link. Pagination and arrows need no changes.

### Publishing

- **GitHub Pages**, from the public repository `LieslTheRagamuffin/Lieslcare`, deploying from the branch `main`, folder `(root)` (confirmed by the owner, 2026-10-02). Address: `https://liesltheragamuffin.github.io/Lieslcare/`.
- **`main` is production.** A merge to `main` goes live within minutes, so work on a branch and open a PR.
- **No build step.** There is no package manager, bundler, preprocessor or generator, and files are served as committed.
- GitHub runs Jekyll over branch deployments without being asked. HTML files without front matter (all current files) are copied verbatim, with these consequences:
  - Markdown files without front matter are rendered too, so `CLAUDE.md` is expected to appear publicly at `/CLAUDE.html`. Write nothing here you would not publish.
  - Liquid template syntax is evaluated in rendered Markdown. In any `.md` file, never write a brace-percent tag opener, and never write an opening double brace without its closing pair. A Liquid syntax error fails the Pages build and freezes the live site at its last good version. Complete tokens such as `{{FEEDING_TIMES}}` are safe; they render blank in the HTML copy.
  - Never add YAML front matter to `index.html`, because Liquid would then swallow the placeholders.
  - Files and folders whose names begin with `_` or `.` are not published.
- The site is served under `/Lieslcare/`, so use relative URLs (`IMG_4812.jpeg`, never `/IMG_4812.jpeg`). Filenames are case-sensitive (`.jpeg` and `.jpg` are different). The one exception is `og:image`, which social crawlers need as an absolute URL.
- Local preview: run `python3 -m http.server 8000` in the repository root and open `http://localhost:8000/`.

---

## 2. House style

### Concept and voice

The site is *Baedeker's Kaiserin Liesl*, a red-and-gold guidebook ("Leipzig: Karl Baedeker · Third Edition", "K. u. K. Hoflieferant") to the realm of Her Imperial and Royal Majesty: *kaiserlich und königlich*, hence k. u. k. Two registers share every page.

1. **Court register** for titles, captions, epigraphs and framing. It is ceremonious, affectionate and gently self-mocking.
   - "Compiled for the faithful of her court, that no comfort be left to chance."
   - "Her Majesty presides over the evening service."
   - "Should the Empress interrupt the cycle, delicately extricate Her Majesty to an alternative salon, securely close the doors, and await completion."
2. **Baedeker register** for anything the reader must do. It is terse, exact and actionable, and gives quantity, frequency, place and object.
   - "Her royal water fountain must be renewed every two days." / "Caution: the top and base of the fountain are not connected; handle with care."
   - "Both sacred offerings are secreted within the lower left drawer of the grand media cabinet."

The two registers work best together, as in the Litter-Robot rite, where each step is both a ceremony and a concrete action ("Dress the drawer in a pure new liner, pressed flat lest the all-seeing OmniSense be deceived"). Test every instruction: could a first-time sitter, reading on a phone, do it correctly from this sentence alone? "The supply of dry delicacies is replenished by unseen magic" fails, because the reader cannot tell whether to refill it.

Conventions:

- **Names for Liesl:** Her Majesty, the Empress, Kaiserin Liesl, Her Imperial and Royal Majesty. She/her.
- **German for titles, English for instructions.** Chapter titles (h2) and rubric titles (h3) are German, with nouns capitalised and umlauts and ß written properly ("Die Wacht am Rücken", "Nektar der Götter"). Ribbon labels pair a Roman numeral with one German word ("III · Rituale"). Body copy is English, with British spelling to match Baedeker's English editions.
- **Ennobled objects, plainly identified.** Household things take court names: the Litter-Robot 4 is "der Vierte Thron", the fountain "der Lebensbrunnen", the litter "the sacred sands". Name the real object plainly at least once, as the Alchemie subtitle does: "Der Vierte Thron · Litter-Robot 4".
- **Court offices** for people: "K. u. K. Leibärzte" (veterinarians), "Oberste Hofdame", "Der Getreue Hofstaat". New roles take their titles from the same Hofstaat vocabulary.
- **Ordinals and dates:** "Chapter the First"; Roman numerals in medallions and the ribbon; "the Year of Grace 2026".
- **Edition:** "Third Edition" appears in the colophon and in the CSS banner comment. Keep the two in step, and change the edition only when the owner asks.
- **k. u. k.:** lowercase with spaces in the source. The `.smallcaps` class uppercases it in labels.
- **Quotation marks:** German „…“, French « … » with no-break spaces inside the guillemets (and before `?`), English “…”.
- **Code comments** share the voice ("names shall never again be beheaded", "MOTION COURTESY", "Courtly keyboard etiquette") and still say what the code does.

### Typography

A single Google Fonts `<link>` loads Cinzel 400–900, EB Garamond 400–700 with italics, and Great Vibes. Icons come from Remix Icon 3.5.0 via jsDelivr, and crown motifs (`ri-vip-crown-*`) recur.

| Role | Face and setting | Example |
|---|---|---|
| Body | EB Garamond (Georgia fallback), 1.15rem, line-height 1.62 | rubric paragraphs |
| Chapter title (h2) | EB Garamond italic 600, `clamp(1.9rem, 4.6vw, 2.7rem)` | "Das Bankett" |
| Cover title (h1) | Cinzel 900, tracking .08em, `clamp(2.4rem, 7.5vw, 4.2rem)` | "BAEDEKER'S" |
| Script | Great Vibes, used once, for "Kaiserin Liesl" on the cover. Keep it that rare. | "Kaiserin Liesl" |
| Rubric title (h3) | Cinzel .78rem, uppercase, tracking .15em, oxblood, after one gold Remix icon | "Der Lebensbrunnen" |
| Labels (`.smallcaps`) | Cinzel, uppercase, tracking .22em; .75rem (eyebrows, subtitles, attributions, roles, colophon, footer) | "Chapter the First" |
| Ribbon links, text buttons, chips | Cinzel .75rem, uppercase | "View Water Levels" |
| Placeholders | `mark.placeholder`: monospace .85em, ink on `--gold-pale` | `{{FEEDING_TIMES}}` |
| Captions | EB Garamond italic .9rem | "Her Majesty presides over the evening service." |
| Epigraph | italic .98rem; gloss .88rem in parentheses; attribution as a label after an em dash | each chapter opener |

No text is set below 0.75rem (12 px); keep it so, and keep body copy at 1rem or larger.

### Palette

Every colour is a token on `:root`; add new colours as tokens too. Literals outside the tokens: `#41566E` (blue chip text) and translucent overlays on the dark leaves, each chosen to pass AA. Ratios are WCAG contrast for small text.

| Token | Hex | Role | As small text |
|---|---|---|---|
| `--parchment` | `#F7F1E4` | ribbon, lightbox panel | background |
| `--parchment-deep` | `#EFE5CF` | leaf gradient, bottom right | background |
| `--cream` | `#FFFDF6` | leaf gradient top left, rubric cards, mats | background |
| `--ink` | `#2B2118` | body text | 15.5:1 on cream ✓ |
| `--ink-soft` | `#5C4C3B` | epigraphs, notes, ribbon links | 6.6:1 on parchment-deep ✓ |
| `--ink-faint` | `#6B5C48` | captions, subtitles, counters | 6.4:1 cream, 5.2:1 parchment-deep ✓ |
| `--gold` | `#A8863D` | hairlines, borders, icons, medallion numerals, flourish (never small text) | 3.4:1 cream ✗ for small text |
| `--gold-text` | `#7A5E22` | gold small text on parchment: eyebrows, attributions, text buttons, hovers | 6.0:1 cream, 4.9:1 parchment-deep ✓ |
| `--gold-bright` | `#C9A75C` | gold on the dark velvet leaf, page arrows, waltz toggle | 7.4:1 on velvet ✓; 3.9:1 on baedeker ✗ |
| `--gold-pale` | `#E4D3A8` | gold on red: cover imprint and attributions, decree eyebrow, roles; placeholder ground | 6.0:1 on baedeker ✓ |
| `--oxblood` | `#7E2A23` | rubric titles, links, chips, seal | 9.2:1 on cream ✓ |
| `--baedeker` | `#8E1F1F` | Baedeker-cover red: welcome, decree leaf, `theme-color` | background |
| `--baedeker-deep` | `#5E1414` | decree gradient edge | background |
| `--velvet` | `#241A16` | page background, Alchemie leaf | background |
| `--velvet-deep` | `#171009` | video well, lightbox scrim | background |
| `--sissi` | `#8FA3BE` | blue tint (named for Empress Elisabeth) | tint only |
| `--emerald` | `#4C6B52` | green chip | 5.1:1 on its tint ✓ |

Chip colours follow real objects where they can (the green brush, the blue comb).

### Layout and components

- **Book of leaves.** Each chapter is a viewport-wide `section.page` in a horizontal scroll-snap book, under a fixed ribbon. Each page holds a `.leaf` (framed parchment card with gilt corner brackets), which holds `.page-scroll` (owns vertical overflow), which holds `.page-content` (`margin:auto`). This is the **centering law**: short pages sit centred and tall pages open at their heading. Keep it.
- **Leaf variants:** parchment by default, `.velvetine` (dark, dotted) for Alchemie, `.oxbloodine` (Baedeker red) for the Royal Decree. Each has colour overrides elsewhere in the stylesheet.
- **Frontispiece** opens every chapter: eyebrow, medallion (Roman numeral), h2, optional subtitle, epigraph, optional flourish.
- **`.duet`** puts a figure and rubrics in two columns from 880 px (`.flip` swaps the sides) and stacks them below that width.
- **`figure.gilt`** is a matted 3:4 photograph with an italic caption. `.cameo` makes it circular and `.hero-cameo` adds a crown.
- **`.rubric`** cards hold an icon and German h3, short paragraphs, `.note` for cautions and locations, `.chip` for quantities and objects, and `.text-btn` to open a lightbox plate. `.pair` sets two rubrics side by side from 640 px.
- **`.rite`** is a numbered italic procedure with Cinzel numerals in gilt circles. Use it for any step-by-step task.
- **Lightbox plates** are photographic plates opened from a `.text-btn`, with carousel mode for sequences. Each plate's caption repeats its alt text so the plate can be understood without the picture.
- **`.crop`** is the clipping well inside every `figure.gilt` mat (3:4, or round in a `.cameo`); it lets a portrait be shifted and zoomed for framing.
- **`.court` / `.courtier`** are the contact cards on the decree page.

### Baedeker conventions

These guidebook devices give the site its form. Asterisk ratings and fold-out plans are not yet in use; introduce them in the manner described here.

#### Asterisk ratings

Baedeker marked objects of special interest with an asterisk and the most remarkable with two.

- `*` means noteworthy and `**` exceptional. Set them as type (the asterisk character, in gold, never an icon) directly before the name: `*Lebensbrunnen`, `**Kaiserin Liesl`.
- Use them sparingly. Most items carry none, and each chapter has at most one `**`.
- Rate only sights already on the site or supplied by the owner. A rating expresses the court's admiration; inventing a favourite spot or habit in order to rate it breaks §5.
- Explain the system once, on the cover or dedication page, in Baedeker's manner: "Objects of special interest are indicated by asterisks."
- Screen readers announce `*` inconsistently, so mark it up like this, adding a standard `.visually-hidden` utility class the first time:

  ```html
  <span class="star" aria-hidden="true">**</span><span class="visually-hidden">Exceptional: </span>Kaiserin Liesl
  ```

#### Hints for Travellers

Not used. The owner removed the Hints for Travellers sections (2026-10-02); do not add them back or build anything like them.

#### Fold-out plans

Baedeker bound in folding plans with numbered keys, and the text referred to them by grid square ("Pl. B 2").

- Build each plan as a native `<details class="plan">` with a `<summary>` such as "Plan of the Kitchen (unfold)". It opens without JavaScript, works with keyboard and touch, and needs no library.
- Draw it as inline SVG with `role="img"`, `<title>` and `<desc>`, coloured with the palette tokens, or use an image with full alt text. Follow it with a numbered key in HTML so that every location also exists as text.
- Use letters for columns and numbers for rows, and cite them in the text as `(Pl. B 2)`.
- Keep plans schematic and draw them only from owner-supplied facts or the existing photographs. Show unknown positions as placeholders.
- Never show the address, entrances, key or lockbox locations, or any access code.
- Put any unfolding animation inside `@media (prefers-reduced-motion: no-preference)`. Every label must stay legible at 360 px wide; otherwise link to the full-size SVG.
- The lightbox plates (Preparation Precepts, Royal Water Levels) are the site's photographic plates; plans are their drawn counterpart.

---

## 3. Quotations

### Rules for new quotations

- The original **and** the translation must both be public domain. A text published in 1930 or earlier is public domain in the US as of 2026, and the cutoff moves forward every 1 January. Prefer translators who died more than 70 years ago, so the text is also free in the UK and EU.
- Never write a translation yourself. If no public-domain translation exists, show the original alone, with no gloss (owner's ruling, 2026-10-02).
- Copy the text from a scan or a reputable transcription (Internet Archive, Project Gutenberg, Wikisource, Gallica, Projekt Gutenberg-DE, Aozora Bunko) and quote it exactly, keeping the translator's spelling. Mark omissions with an ellipsis. Never quote from memory or from a quotation website.
- Put an HTML comment directly beside every quotation. It records the author, work and exact location, the edition of the original, the translator, the translation's edition (title, place, publisher, year), and the URL consulted with the date.
- Mark the original's language (`lang="fr"`, `lang="de"`, `lang="la"`, `lang="ja"`).
- Label a paraphrase "after …", as on the cover, and give it the same comment.
- Use one epigraph per chapter frontispiece. The cover keeps its single "precedent".
- Preferred authors: Sei Shōnagon, E. T. A. Hoffmann, Brillat-Savarin, Montaigne, Baudelaire, Frederick the Great. Others are allowed under the same rules.
- Update the inventory below in the same commit as any quotation change.

```html
<!-- Quotation · Montaigne, Essais II.12, "Apologie de Raimond Sebond"
     Original: [edition, place, year]
     Translation: [translator], [title] ([place]: [publisher], [year]), [vol., page]
     Public domain: original (1580–95); translation ([year])
     Checked against: [URL], [YYYY-MM-DD] -->
<blockquote class="epigraph">
  <span lang="fr">« … »</span>
  <span class="gloss">(…)</span>
  <span class="attrib smallcaps">— Michel de Montaigne, Essais</span>
</blockquote>
```

### Public-domain translations to start from

Before using one, check its wording and confirm that it contains the passage you want.

| Author | Translations |
|---|---|
| Sei Shōnagon | Arthur Waley, *The Pillow-Book of Sei Shōnagon* (London: Allen & Unwin, 1928). A selection, public domain in the US only. |
| E. T. A. Hoffmann | *Kater Murr* has no known pre-1931 English translation. For other works: Thomas Carlyle, "The Golden Pot", in *German Romance* (1827); J. T. Bealby, *Weird Tales* (1885); Alex. Ewing, *The Serapion Brethren* (1886–92). |
| Brillat-Savarin | Fayette Robinson, *The Physiology of Taste* (Philadelphia, 1854); R. E. Anderson, *Gastronomy as a Fine Art* (London, 1877). |
| Montaigne | John Florio (1603); Charles Cotton (1685–86), revised by W. Carew Hazlitt (1877); George B. Ives (1925). |
| Baudelaire | Arthur Symons, *Poems in Prose from Charles Baudelaire* (London: Elkin Mathews, 1905). |
| Frederick the Great | He wrote in French. English: Thomas Holcroft, *Posthumous Works of Frederic II, King of Prussia* (London, 1789). |

### Inventory of quotations on the site (2026-10-02)

There are seven, each with a source comment beside it in `index.html`. Search-extract wordings were taken while direct fetches were blocked; re-check them against the page when you can reach it, then delete the "re-check" note from the comment.

| # | Where | Text on the site | Source | Gloss | Status |
|---|---|---|---|---|---|
| 1 | Welcome cover, `.precedent` | "At the court of Emperor Ichijō, a cat of the palace was raised to the Fifth Rank and styled Myōbu no Omoto." — *after Sei Shōnagon, Makura no Sōshi* | Sei Shōnagon, *Makura no Sōshi* (c. 1000), the passage beginning 上にさぶらふ御猫は | none: the court's own paraphrase | Complete. |
| 2 | Dedication (`#hommage`) | „Es ist doch etwas Schönes, Herrliches, Erhabenes um das Leben!“ | Hoffmann, *Lebens-Ansichten des Katers Murr*, vol. 1 (1819/20), first sentence of "Gefühle des Daseins. Die Monate der Jugend" | none (no public-domain translation) | Complete. |
| 3 | Ch. I, Das Bankett | « Dis-moi ce que tu manges, je te dirai ce que tu es. » | Brillat-Savarin, *Physiologie du goût* (1825), "Aphorismes du professeur", IV | "Tell me what kind of food you eat, and I will tell you what kind of man you are." Fayette Robinson (1854) | Re-check wording against Gutenberg #5434. |
| 4 | Ch. II, Kaiserliche Zerstreuungen | « Quand je me joue à ma chatte, qui sait si elle passe son temps de moi plus que je ne fais d'elle ? » | Montaigne, *Essais* II.12, "Apologie de Raimond Sebond" | "When I play with my cat who knows whether I do not make her more sport than she makes me?" Charles Cotton, ed. W. C. Hazlitt (1877) | Misquotation corrected. Re-check wording against Gutenberg #3600. |
| 5 | Ch. III, Die Rituale der Schönheit | « Les Chinois voient l'heure dans l'œil des chats. » | Baudelaire, "L'Horloge", *Petits poèmes en prose* XVI (1857; collected 1869) | "The Chinese can tell the hour of the day by the eyes of their cats." *The World's Best Essays*, ed. David J. Brewer (1900), translator unnamed | Re-check wording against a scan; prefer a named translator (Symons 1905) if it can be verified. |
| 6 | Ch. IV, Die Alchemie | « Sic transit gloria mundi. » — *from the papal coronation rite* | Anonymous: acclamation of the papal coronation rite (recorded from 1409), perhaps after Thomas à Kempis, *Imitatio Christi* I.3 | none (no verified public-domain translation) | Attribution corrected. A verified PD gloss may be added. |
| 7 | Royal Decree | „Der Fürst ist der erste Diener seines Staates.“ — *after Friedrich II. von Preußen* | A common German rendering of Frederick's French ("premier serviteur de l'État"), *Politisches Testament* (1752), *Essai sur les formes de gouvernement* (1777) | none (no verified public-domain translation) | Now labelled a paraphrase. A verified PD source for the exact German, or Frederick's French with Holcroft's English (1789), would improve it. |

### Music

Audio meets the same public-domain standard. Record the provenance of any new recording in an HTML comment beside its `<audio>` element.

---

## 4. Copy rules

1. **Never begin a heading with "The".** This covers h1–h6, `<title>`, `og:title`, `<summary>`, lightbox and plan titles, and heading-like labels such as eyebrows and ribbon links. Drop the article or recast the heading: "Royal Water Levels", "Plan of the Kitchen", "Of the Fourth Throne".
   - The current `<title>` and `og:title`, "Lieslcare | The Imperial Standard", put "The" at the head of their second segment. Treat that as a conflict.
   - The rule applies to the English word only. German headings beginning with Der/Die/Das are fine, existing and new alike (owner's ruling, 2026-10-02).
2. **Never use the construction "it's not X, it's Y"** or any rewording of the same move ("this isn't X — it's Y", "not X; rather Y", "not merely X, but Y"). State the positive claim directly. The rule covers everything you write: site copy, alt text, captions, code comments, commit messages and PR descriptions. Public-domain quotations are reproduced exactly as published.

---

## 5. Facts about Liesl

- The owner is the only source of facts. Text already on the site was written by the owner and stands as fact. When you restyle it, keep its substance: quantity, frequency, place and object.
- Never invent, estimate or infer any of these: age, birthday, weight, diet, portions, food or treat brands, supplements, medical history, conditions, medications, schedule, routines, likes and dislikes, favourite places, temperament, household layout, or people. Do not extrapolate from photographs; for example, do not guess what the countertop-oven plate is for or what setting it uses.
- Alt text may describe what a photograph plainly shows (a cream coat, a flower collar).
- Where a needed fact is unknown, insert a visible placeholder, list it below, and ask the owner for the value in the PR.
- Placeholders take the form `{{UPPER_SNAKE_CASE}}` and appear on the page as `<mark class="placeholder">{{FEEDING_TIMES}}</mark>`. Never hide one: no `display:none`, no HTML comment, no alt-only text. The first time a placeholder is added, also add a `.placeholder` style that passes AA contrast.
- Update the register below in the same commit whenever a placeholder is added or resolved.
- The Royal Decree page lists the veterinarian and household contacts with phone numbers supplied by the owner. Change them only on the owner's instruction, and never copy them anywhere else, including this file.
- The site is public. Never publish the home address, door, lockbox or alarm codes, Wi-Fi passwords, or where keys are kept.

### PLACEHOLDERS

**In use on the site:** none (2026-10-02).

**Resolved** (2026-10-02, supplied by the owner): `{{EMERGENCY_VET}}` → VEG ER, 4525 Duke Street, Alexandria, open 24 hours (street number and phone found by web search at the owner's request, 2026-10-02); `{{MEDICAL_HISTORY}}` → "no medical history of note".

**Reserved tokens.** These facts are still unknown but not shown, since the Hints sections that held them were removed. Use these exact names if a placeholder is needed again; add new rows as needed.

| Token | Meaning | Natural home |
|---|---|---|
| `{{FEEDING_TIMES}}` | times of day meals are served | Ch. I |
| `{{WET_FOOD_BRAND}}` | brand and flavour of the evening pâté | Ch. I, Das Abendmahl |
| `{{WET_FOOD_PORTION}}` | amount per meal | Ch. I, Das Abendmahl |
| `{{MEAL_PREPARATION_STEPS}}` | the six Preparation Precepts plates in words, including the oven step | Ch. I lightbox |
| `{{DRY_FOOD_ARRANGEMENT}}` | whether and how the sitter refills dry food | Ch. I, Trockene Gaben |
| `{{DRY_FOOD_BRAND}}` | dry food brand | Ch. I, Trockene Gaben |
| `{{TREAT_ALLOWANCE}}` | how much Churu, and how often | Ch. I, Nektar der Götter |
| `{{GROOMING_FREQUENCY}}` | how often to brush and comb | Ch. III, Der Kaiserliche Mantel |
| `{{LITTER_TYPE}}` | litter used in the Litter-Robot 4 | Ch. IV |
| `{{LIGHT_TOY}}` | which toy casts the "beam of light" | Ch. II |
| `{{AGE}}` | age or date of birth | dedication |
| `{{WEIGHT}}` | current weight | dedication |
| `{{DAILY_SCHEDULE}}` | outline of her day | dedication |


---

## 6. Health content

Health content is anything about eating, drinking, elimination, weight, coat, eyes, hygiene, illness, injury, toxins or emergencies.

- **Keep it practical and conservative.** Tell the sitter what to watch for and when to call. Never diagnose or suggest a treatment.
- **No medication names or doses.** The rule covers medicines, supplements and anything given for a health purpose: no product names, amounts or frequencies. Write "as her veterinarian has directed" and leave the specifics to the owner's offline instructions.
- **Owner's exception (2026-10-02):** the two supplement instructions in Ch. I, Das Abendmahl ("⅛ tsp Lysine" and "½ scoop Proden PlaqueOff", the small scoop packed with the product) stay on the site. Keep their wording exact when restyling, change them only on the owner's instruction, and add no other names or amounts.
- **Defer to her veterinarian.** End every health rubric with a link to the Royal Decree page (`#decree`), where the K. u. K. Leibärzte are listed. Link to the page instead of repeating numbers.
- **Cite reputable sources only:** AAFP (catvets.com), Cornell Feline Health Center (vet.cornell.edu), International Cat Care (icatcare.org), and ASPCA (aspca.org, including Animal Poison Control). Open the page, confirm it supports the claim, link that page, and add an HTML comment with its title and the date you consulted it. If you cannot reach the source (cloud sessions often block outbound fetches), leave the claim out. Never cite from memory.
- Show the citation in Baedeker style, as a small line after the advice: "Authority: Cornell Feline Health Center, ‘[page title]’".
- For lists of toxic plants or foods, link the ASPCA's list instead of copying it.
- Write warnings plainly. The court voice may frame a warning but must never soften it.

---

## 7. Engineering

### Static files only

- The site is made of HTML, CSS, vanilla JavaScript, images and audio. Add no frameworks, libraries, preprocessors, package managers, build tools, CSS frameworks, analytics or trackers.
- The only external dependencies allowed are the existing ones: Google Fonts (the three families above), Remix Icon 3.5.0 from jsDelivr (pinned), and the YouTube iframe. Add no others.
- CSS and JS stay inline in `index.html`. If a second page is ever added and needs to share them, plain `styles.css` and `script.js` files are acceptable.

### Reduced motion

- `@media (prefers-reduced-motion: reduce)` ("MOTION COURTESY") covers book smooth-scrolling, the cover's page turn (reduced to a fade), the pulsing tap hint, the slideshow and lightbox fades, and hover zooms. In script, `reduceMotion` keeps `turnPage()` instant and the cover slideshow still.
- Every new animation, moving transition, smooth scroll, auto-advancing element or unfolding effect needs a reduced-motion path in both CSS and JavaScript. Script that animates must check `matchMedia('(prefers-reduced-motion: reduce)').matches`: for example, pass `behavior:'auto'` to `scrollBy`, and don't start interval slideshows.

### Contrast (WCAG 2.x AA)

- Normal text needs 4.5:1. Large text (24 px or larger, or 18.66 px bold) and meaningful icons, borders and controls need 3:1. Every Cinzel label at .78rem or smaller counts as normal text.
- Composite translucent colours over their real background before measuring. Measure pulsing or fading text at its faintest point.
- Use the ✓ pairs in the palette table. Don't set small text in `--gold` or `--ink-faint` on parchment, or in `--gold-bright` on `--baedeker` red.
- On red, use `--gold-pale` or parchment at 0.75 opacity or more; translucent gold-pale text needs at least 0.82 opacity. Anything that pulses must stay at or above its passing opacity throughout.
- Contrast checker:

  ```python
  def lum(h):
      c = [int(h[i:i+2], 16) / 255 for i in (1, 3, 5)]
      c = [v / 12.92 if v <= 0.03928 else ((v + 0.055) / 1.055) ** 2.4 for v in c]
      return 0.2126 * c[0] + 0.7152 * c[1] + 0.0722 * c[2]

  def ratio(a, b):
      hi, lo = sorted((lum(a), lum(b)), reverse=True)
      return (hi + 0.05) / (lo + 0.05)

  print(round(ratio('#2B2118', '#FFFDF6'), 2))  # 15.47
  ```

### Framing

Every portrait of Liesl is framed with her face centred left to right and her eyes on the upper third line, as far as the frame allows.

- Frames have fixed shapes: the cover arch is 2:3, `figure.gilt` 3:4, and `.cameo` a 1:1 circle, so one framing holds at every screen width.
- Find the midpoint of her eyes as a fraction of the photo's width and height (lay a 10% grid over it). Then set, on the `<img>`:
  1. `object-position` to slide the photo along the axis the frame crops, then
  2. where that is not enough, `transform:scale(z)` with a `transform-origin` that leaves her eyes at (50%, 33%). Keep `z` at 1.3 or below, so ear tips stay inside the arch's dome, and skip zooms under 1.06.
- Zoomed images must sit inside a clipping parent (`.crop` in figures, `.well` in the arch). Render the crop and look at it before committing.
- For cover slides, put the style in the slide's `frame` field; the script applies it while the slide is hidden.
- `IMG_3351` reaches only 44% at the 1.3 cap; its eyes sit low in the original.

### Images and media

- Give every `<img>` descriptive alt text. For a portrait, describe Liesl's pose and setting. For an instructional plate, state the instruction itself (which cabinet, which line to fill to), either in the alt text or in visible text beside the image. When script swaps an image's `src`, update its `alt` as well.
- Give decorative icon `<i>` elements `aria-hidden="true"`. A link or button whose only content is an icon needs an `aria-label`.
- Strip metadata from every new photograph before committing it; iPhone photos carry GPS coordinates. Use `mogrify -strip FILE` (ImageMagick) or `exiftool -all= -overwrite_original FILE`. If `identify -verbose FILE | grep -i gps` prints nothing, the file is clean.
- Match the existing format: JPEG with a 1280 px long edge at about quality 80, keeping the camera's `IMG_####.jpeg` name. Give new `<img>` elements `width` and `height`, plus `loading="lazy"` when they sit below the first screen.
- Keep the waltz pausable from `#waltz-toggle` at all times.

### Phones first

- Check every change at 360 px and 390 px wide, in portrait, with touch.
- Allow no horizontal overflow within a page. The book's paging is the only horizontal movement.
- Make tap targets at least 44×44 px where possible, and never smaller than 24×24 px.
- Leave pinch-zoom enabled: put no `user-scalable=no` or `maximum-scale` in a viewport tag.
- Make nothing depend on hover.
- Mark foreign-language passages with `lang` (WCAG 3.1.2), including German headings when you touch them.
- Keep page weight down; everything loads over a phone connection. The waltz (13 MB) stays `preload="none"`, slides are fetched one ahead, and lightbox plates load on first opening.

### Checks before every commit

- Preview locally (`python3 -m http.server`) in Chromium. Playwright works for this; at the time of writing it was available to Node in cloud sessions. Test at 390×844 with `reducedMotion: 'reduce'` and again with `'no-preference'`. Turn every page, open each lightbox, toggle the waltz, and watch the console for errors.
- `grep -nE '<h[1-6][^>]*>(\s|<i[^>]*></i>)*The\b' index.html` must print nothing.
- `grep -oE '\{\{[A-Z_]+\}\}' index.html | sort -u` must match the PLACEHOLDERS register.
- `grep -c '<img' index.html` must equal `grep -c '<img[^>]* alt="[^"]' index.html`.

### Git

- Branch from `main` and open a PR, since merging publishes.
- Make one logical change per commit and describe it plainly.
- Binaries stay in history forever, so compress them before committing.

---

## Known conflicts in the current site

Updated 2026-10-02. Fix them only when the owner asks, and delete each line once it is fixed.

- **Health (§6):** no health content cites a source; the eyes and rear rubrics defer to the Leibärzte instead. Add citations only after opening the source page (blocked from cloud sessions so far).
- **Quotations (§3):** the glosses for Brillat-Savarin, Montaigne and Baudelaire were taken from search extracts; re-check them against the pages named in their comments.
- **Privacy:** 24 of the older `IMG_*.jpeg` files carry GPS coordinates in their EXIF data, and Pages serves them publicly. The seven photos added on 2026-10-02 were stripped losslessly, but their originals, like the older ones, stay in git history unless history is rewritten.
- **Placeholders (§5):** none on the site; thirteen facts remain unknown and reserved (see the register).

## Open questions for the owner

None at present (2026-10-02).
