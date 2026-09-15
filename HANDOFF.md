# CREATE AI Research Page — Developer Handoff

Drop-in redesign for:
https://create.usc.edu/create-research-on-artificial-intelligence/

Confirmed CMS: **WordPress** (Academix child theme + KingComposer).

## What’s in this folder

| Path | Purpose |
|------|---------|
| [`preview/index.html`](preview/index.html) | Standalone local preview with mock CREATE chrome |
| [`wordpress/content-fragment.html`](wordpress/content-fragment.html) | Paste-ready page body (no site header/footer) |
| [`wordpress/create-ai-research.css`](wordpress/create-ai-research.css) | Scoped stylesheet (`create-ai-` prefix) |
| [`assets/cascade.svg`](assets/cascade.svg) | Standalone interconnection diagram (no longer used on the page; kept for reuse elsewhere) |
| [`HANDOFF.md`](HANDOFF.md) | This file |

## Preview locally

The preview shell loads `wordpress/content-fragment.html` live — edit that file (and the CSS), then refresh.

1. From the project root, start a local server (required; `file://` cannot fetch the fragment):

   ```bash
   python3 -m http.server 8765
   ```

2. Open http://127.0.0.1:8765/preview/index.html
3. Edit `wordpress/content-fragment.html` or `wordpress/create-ai-research.css`, save, refresh.
4. Review expand/collapse bios and references; check mobile stacking.

## Install on create.usc.edu

1. **Upload CSS**  
   Upload `wordpress/create-ai-research.css` via Media Library **or** place it under the child theme / uploads and note the public URL.

2. **Fix the stylesheet path**  
   At the top of `content-fragment.html` there is:

   ```html
   <link rel="stylesheet" href="/wp-content/uploads/create-ai-research.css" />
   ```

   Update that `href` to the real uploaded URL (or enqueue the file in the child theme / a small custom plugin instead of a `<link>` in content).

3. **Replace page content**  
   Edit the existing page *CREATE Research on Artificial Intelligence* (page ID `5327`).  
   Keep the CREATE theme header, campus page banner/title bar, breadcrumbs, and footer.  
   Replace only the **main content body** with `wordpress/content-fragment.html`.

4. **Optional headshots**  
   Researcher cards use initials placeholders (`.create-ai-avatar`). Swap for `<img>` tags when photos are available.

5. **Publish & smoke-test**  
   Check desktop + mobile, expand/collapse bios and references, and verify citation links.

**Preview chrome:** `preview/index.html` approximates the live CREATE nav (logo), USC campus page banner, uppercase title bar, breadcrumbs, and a neater four-column version of the existing footer (same address, contact, partner logos, social links). Do not paste that chrome into WordPress — the theme already provides it.

## Content map (what replaced the wall of text)

The page is written for a general public audience: plain language, present tense, and every framing
section links down to the researchers and publications that back it up.

1. Hero — *Securing Critical Infrastructure in the Age of AI*, two short paragraphs, and three CREATE facts (20+ years, 8 fellows, 24 publications)  
2. On this page — jump links to every section (anchors have `scroll-margin-top` for the sticky nav)  
3. Three challenges — adversaries / defensive AI / reliability & control, each with an "In practice" example and researcher links  
4. Research areas — eight concrete topics drawn from the fellows' work, each linking to the fellow  
5. How we work — simulate → build decision tools → evaluate, using real artifacts (Disaster World, E-CAT, Game of Hidden Rules)  
6. About CREATE — DHS Center of Excellence, USC Viterbi/ISI, national network  
7. All 8 Research Fellows — short blurbs, challenge tags linking back up, full bios on expand  
8. Full AI reference list — collapsed by default; all links retained (libproxy URLs normalized to public DOIs where possible)  
9. Contact — email, related CREATE pages, one-line support note

Removed from the earlier draft: the IEA `$110B` stat (not CREATE's research), the "Distinctive contribution"
section (merged into the hero), the interconnection diagram (generic; the point is now one sentence in the
challenges lede), the "2028 Games" and "Los Angeles laboratory" tiles, and the philanthropy callout
(now a single line in Contact).

If facts change (fellow count, publication count), update the hero `create-ai-facts` block and the
references `<summary>` count together.

## Accessibility checklist

- [ ] Headings remain in logical order under the site title (fragment starts at `h2`; section titles are `h2`, cards are `h3`)
- [ ] “Read more” / references use native `<details>` (keyboard accessible)
- [ ] Color contrast holds on cardinal red links, white-on-cardinal tags, and white-on-dark hero text
- [ ] `prefers-reduced-motion` disables card hover lifts
- [ ] All in-page anchors (`#create-ai-*`) resolve; challenge ↔ fellow links go both ways

## Notes for KingComposer / Academix

- Prefer a single **HTML** / raw content module for the fragment so nested markup is not stripped.
- If the editor strips `<details>` or inline SVG, paste via the Text/HTML mode or a Custom HTML widget, or ask hosting to allow those tags in `wp_kses`.
- Scoped classes (`create-ai-*`) should not collide with Academix / KingComposer styles; if spacing looks off, wrap only the fragment and avoid applying theme column padding twice.

## Out of scope

- Live WordPress edits from this repo  
- Full CREATE theme redesign  
- New research claims beyond the vision brief + current page
