# CREATE AI Research Page

Drop-in redesign for CREATE’s public AI research page:

**[create.usc.edu/create-research-on-artificial-intelligence](https://create.usc.edu/create-research-on-artificial-intelligence/)**

Two files go on the live site. Everything else is only for preview.

**Share this preview:** [https://create-ai-research-page.vercel.app](https://create-ai-research-page.vercel.app)

Anyone with the link can open it. This GitHub repo stays private. It is not the live create.usc.edu page.

![Preview of the CREATE AI research page](docs/preview.png)

## What’s in this folder

| File | Use it for |
|------|------------|
| [`wordpress/content-fragment.html`](wordpress/content-fragment.html) | Paste this into the WordPress page body |
| [`wordpress/create-ai-research.css`](wordpress/create-ai-research.css) | Upload this stylesheet with the page |
| [`preview/index.html`](preview/index.html) | Local preview only — **do not** paste this into WordPress |

The preview includes a mock CREATE header and footer so you can see how the page will sit on the live site. The real site already has those, so they are not in the WordPress files.

---

## Preview on your computer

You need a small local server. Opening the HTML file directly will not work.

1. In a terminal, from this folder, run:

   ```bash
   python3 -m http.server 8765
   ```

2. Open [http://127.0.0.1:8765/preview/index.html](http://127.0.0.1:8765/preview/index.html)

3. Edit `wordpress/content-fragment.html` or `wordpress/create-ai-research.css`, save, then refresh the browser.

Check that fellow bios expand, the references list opens, and the layout stacks cleanly on a narrow window.

---

## Put it on the website

WordPress setup: Academix child theme + KingComposer. Edit the existing page **CREATE Research on Artificial Intelligence** (page ID `5327`).

Keep the CREATE header, campus banner, title bar, breadcrumbs, and footer. Replace **only the main content**.

1. **Upload the CSS**  
   Upload `wordpress/create-ai-research.css` through the Media Library, or place it in the child theme / uploads folder. Copy the public URL.

2. **Point the HTML at that CSS**  
   At the top of `wordpress/content-fragment.html` is:

   ```html
   <link rel="stylesheet" href="/wp-content/uploads/create-ai-research.css" />
   ```

   Change the `href` to the real URL from step 1 if it is different.

3. **Paste the page body**  
   Open `wordpress/content-fragment.html`, copy everything, and paste it as **raw HTML** (Text/HTML mode, or a Custom HTML module). Avoid the visual editor — it can strip tags.

4. **Publish, then click through**  
   On desktop and phone, expand a fellow bio, open the references list, and click a citation link.

### Optional

- Researcher cards currently show initials. Swap in photos later with `<img>` tags inside `.create-ai-avatar`.
- If WordPress strips `<details>` or inline SVG, stay in HTML mode, or ask hosting to allow those tags in `wp_kses`.
- All classes are prefixed `create-ai-` so they should not collide with the theme. If spacing looks doubled, the fragment is probably wrapped in an extra theme column.

---

## What’s on the page

1. Mission statement  
2. Three challenges — adversaries, defensive AI, reliability & control  
3. Eight research areas, each linked to a fellow  
4. How we work — simulate → build decision tools → evaluate  
5. All eight Research Fellows (short blurb; full bio on expand)  
6. Full AI reference list (collapsed by default)  
7. Contact  

If the number of publications changes, update the count in the references `<summary>` line.
