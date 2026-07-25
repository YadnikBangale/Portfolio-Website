# Yadnik Bangale's Portfolio

A single-page, animated "backstage" themed portfolio site. Visitors open on a first-person drummer's POV, hit the crash cymbal to "walk backstage" through an animated corridor, and land in a green-room hub where six doors lead to About, Skills, Projects, Experience, Achievements, and Contact.

Built as a single self-contained HTML file — no framework, no build step, no dependencies beyond Google Fonts.

## Live Preview

Open `index.html` directly in any modern browser. No server required.

## Tech Stack

- **HTML5** — page structure
- **CSS3** — custom properties, Flexbox, Grid, keyframe animations, gradients, pseudo-elements, media queries
- **Vanilla JavaScript (ES6)** — scene transitions, DOM manipulation, event handling
- **Web Audio API** — synthesizes the cymbal-crash sound in-browser (no audio file used)
- **Google Fonts** — Fraunces (display serif), Inter (body), Space Mono (labels/UI)
- **Inline SVG** — icons (GitHub, LinkedIn, download) and cursor/texture data-URIs

## Project Structure

```
index.html          # entire site — markup, styles, and scripts in one file
images/
  └── profile.jpg    # optional — portrait shown in the hero section
```

> If `images/profile.jpg` is missing, the frame gracefully falls back to a placeholder ("Your Photo Goes Here") instead of a broken image icon.

## Page Flow

1. **Intro (drum kit, FPP)** — `#intro`
   Interactive drum kit rendered in CSS. Clicking/tapping the crash cymbal:
   - Plays a synthesized cymbal sound (Web Audio API)
   - Triggers a hit animation, screen flash, and screen shake
   - Transitions into the corridor scene

   A **Skip intro →** button is always available to jump straight to the hub.

2. **Corridor (transition run)** — `#corridor`
   A fake first-person "running" animation: scrolling floor/wall textures, doors flying past, and a room-name label cycling through the six sections — purely cosmetic, auto-advances to the hub after ~2.4s.

3. **Hub (main site)** — `#hub`
   - **Header** — logo mark + nav (`Rooms`, `Contact`)
   - **Hero** — framed portrait, name/role eyebrow, headline, intro paragraph, résumé download button
   - **Stage & Tour Log** — a GitHub-contributions-style activity heatmap (randomly generated client-side, purely decorative)
   - **The Hallway** — six doors, one per portfolio section
   - **Footer** — GitHub/LinkedIn links, copyright

4. **Room overlays** — six full-screen panels, opened by clicking a door:

   | Room | Content |
   |---|---|
   | 01 · About Me | Short bio |
   | 02 · Skills | Pedalboard-style tag grid of technologies |
   | 03 · Projects | Gig-poster cards for each project |
   | 04 · Experience | Tour "setlist" of internship/education history |
   | 05 · Achievements | Trophy-shelf badges + certificate links |
   | 06 · Contact | Email, phone, location |

   Each panel closes via its **✕** button or by clicking the backdrop.

## Customizing Content

All content lives directly in the HTML — no CMS or data file. To edit:

- **Text** — edit the relevant `<div class="room" data-panel="...">` block near the bottom of `index.html`.
- **Photo** — drop an image at `images/profile.jpg` (any aspect ratio; it's cropped via `object-fit: cover`).
- **Résumé link** — update the `href` on the `.btn-resume` anchor in the hero section.
- **Social links** — update the `href`s inside `.footer-links` in the `<footer>`.
- **Colors** — all theme colors are CSS custom properties defined once in `:root`:
  ```css
  --wood-dark, --wood-mid, --wood-plank, --amber, --amber-hot, --brass, --cream, --cream-dim
  ```
- **Doors / rooms** — to add or remove a room, add/remove a `.door` element in `.doors-grid` (with a matching `data-room` value) and its corresponding `.room[data-panel="..."]` overlay block.

## Responsive Behavior

The layout adapts across four breakpoints (`1024px`, `900px`, `640px`, `380px`):

- Hero switches from a two-column (portrait + text) to a stacked single-column layout
- Doors grid reflows from 3 → 2 → 1 columns
- The drum-kit intro scene scales down and repositions so nothing clips off-screen on phones
- Room panels, pedal/poster grids, setlist rows, achievement badges, and footer links all reflow for narrow viewports

`prefers-reduced-motion` is also respected — animations are effectively disabled for users who request reduced motion at the OS level.

## Browser Support

Uses standard modern CSS/JS (custom properties, Grid, `clamp()`, `backdrop-filter`, Web Audio API). Works in current versions of Chrome, Firefox, Safari, and Edge. No polyfills included.

## Known Notes

- The gig/activity heatmap under the hero is randomly generated on every page load — it's decorative, not backed by real data.
- The Web Audio crash sound requires a user gesture to start (browser autoplay policy) — this is naturally satisfied since it only plays on click/tap.

## License

Personal portfolio — content and imagery belong to Yadnik Bangale. Feel free to reference the code structure/techniques for your own projects.
