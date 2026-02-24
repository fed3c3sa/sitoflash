---
description: How to build a stunning single-page website for an influencer/creator
---

# Influencer Website Builder

Build a premium, responsive, bilingual (IT/EN) single-page website for an influencer, using only their `info.txt` and local `assets/` folder.

---

## 1. Read the influencer's info

- Read the `info.txt` file inside the influencer's project folder to extract:
  - **Name** and brand/handle
  - **Bio / Who they are**
  - **What they do** (content pillars, services, niches)
  - **Social links** (Instagram, TikTok, YouTube, etc.)
  - **Any extra channels** (radio, podcast, collaborations, etc.)
  - **Contact method** (DM, email, booking link — use only what they provide)

## 2. Inventory the assets

- List all files inside the `assets/` folder.
- Identify which image is the **profile picture** (user will specify, or ask).
- All remaining images are **content screenshots / gallery photos**.
- **Never invent or generate images** — only use what is provided.

## 3. Fetch YouTube video IDs (if applicable)

- If the influencer has a YouTube channel, use the **browser subagent** to visit the channel's `/videos` or `/shorts` page and extract video IDs.
- Accept any cookie/consent dialogs first.
- Collect 6 video IDs and their titles.
- **Do NOT use iframes** for YouTube embeds. YouTube blocks `<iframe>` embeds when the page is opened via `file://` protocol.
- Instead, use **clickable thumbnail cards**:
  - Thumbnail image: `https://img.youtube.com/vi/{VIDEO_ID}/oar2.jpg`
  - Link: `https://www.youtube.com/shorts/{VIDEO_ID}` (for Shorts) or `https://www.youtube.com/watch?v={VIDEO_ID}` (for regular videos)
  - Add a play-button overlay and the video title as a label.

## 4. Build the HTML file

Create a single `index.html` file in the influencer's project folder with these sections:

### Design system (CSS custom properties)

- Use a **dark premium theme** (not white — dark charcoal backgrounds like `#1a1714`).
- Warm accent color (e.g. terracotta `#d85c41`) with a gold secondary (`#c9a96e`).
- Adapt the palette to match the influencer's brand colors if known.
- Google Fonts: `Outfit` (sans-serif body) + `Playfair Display` (serif headings).
- FontAwesome 6 for icons.
- Use CSS custom properties for all tokens so the palette is easy to swap.

### Page structure

1. **Header (fixed)**: Logo (influencer name), nav links, social icon buttons (Instagram/TikTok/YouTube), language toggle `[IT | EN]`.
2. **Hero**: Greeting + name (large serif heading with gradient accent), short bio paragraph, two CTA buttons ("Explore" + "Collaborate"), circular profile picture with floating animation and decorative rotating ring.
3. **Services / What I Do**: 4-column card grid showing content pillars with FontAwesome icons, title, and description. Cards have hover lift + gradient top-bar reveal.
4. **Beyond Instagram** (optional): Rounded card highlighting extra channels (YouTube, collaborations, radio, podcast) — only include channels the influencer actually has. 2-column grid with icon circles.
5. **Auto-scrolling Photo Gallery**: Infinite horizontal marquee of all content screenshots. Clone items via JS for seamless loop. Pauses on hover.
6. **YouTube section** (if applicable): 3-column grid of clickable thumbnail cards (NOT iframes). Each card has the video thumbnail, a play button overlay, and the video title as a bottom label.
7. **Footer**: Closing message, social links (larger icons), copyright.

### Bilingual system (IT/EN)

- Default language: Italian.
- Add `data-i18n="key"` attributes to every translatable element.
- Define a `translations` JS object with `it` and `en` keys.
- `setLang(lang)` function swaps `innerHTML` of all `[data-i18n]` elements.
- Language toggle buttons in the header switch between IT/EN.

### Animations

- **Scroll reveal**: Use `IntersectionObserver` to add `.active` class when elements enter the viewport.
- Offer multiple reveal directions: `reveal` (fade up), `reveal-left` (slide from left), `reveal-right` (slide from right), `reveal-scale` (scale in).
- Use staggered `transition-delay` on grid items for cascading effect.
- **Hero floating animation**: `@keyframes float` for the profile picture (gentle up/down bobbing).
- **Decorative ring**: `@keyframes spin` — slow rotation around the profile picture with emoji accents.
- **Service cards**: Gradient top-bar that scales in on hover (`transform: scaleX`).
- **Gallery marquee**: `@keyframes marquee` — continuous horizontal scroll, `animation-play-state: paused` on hover.

### Responsive breakpoints

- `992px`: Stack hero to 1-column, shrink profile image, adjust grids.
- `768px`: Hide desktop nav links, reduce font sizes, adjust gallery item sizes.
- `480px`: Single-column YouTube grid, smaller gallery items, smaller social icons.

## 5. Verify the result

// turbo
- Open the `index.html` file in the browser using the browser subagent.
- Scroll through each section to check layout, images, and animations.
- Test the language toggle (click EN, verify text changes, click IT back).
- Confirm all images load from the local `assets/` folder.
- Confirm YouTube thumbnails load (they require internet but work from `file://`).

---

## Checklist before delivery

- [ ] Profile picture is the correct image specified by the user
- [ ] All local assets are used (no invented images)
- [ ] No Radio/email/channels the influencer doesn't have
- [ ] YouTube thumbnails (not iframes) with working links
- [ ] IT/EN toggle works on all text
- [ ] Fully responsive (desktop, tablet, mobile)
- [ ] Dark premium theme with warm accents
- [ ] Smooth scroll-reveal animations on all sections
- [ ] Auto-scrolling gallery with pause-on-hover
- [ ] Social links in the header AND footer
- [ ] Single `index.html` file, no external dependencies beyond CDN fonts/icons
