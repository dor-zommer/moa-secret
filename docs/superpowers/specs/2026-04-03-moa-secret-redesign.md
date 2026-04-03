# MOA Secret Website Redesign Spec

## Goal

Enhance the existing static HTML/CSS site with atmospheric design elements from the old WordPress site, while preserving all current content, responsiveness, and clarity.

**Base:** Current static site (index.html + style.css) — all content, icons, marketing text, sections stay.
**Layer on top:** Artistic/emotional motifs from the old site (Figma capture) — slideshows, cinematic photos, breathing space.

## Sections (top to bottom)

### 1. Header
- **No changes** to structure (fixed, blur backdrop, logo + nav)
- Keep "ניהול" + "הזמינו מקום" buttons

### 2. Hero
- **Replace** static background image with a **CSS/JS image slideshow** (fade transitions, ~5-8 second intervals)
- Use existing `hero-bg.jpg` + additional desert photos from `assets/`
- "סוד מדבר" text stays, but **larger and more dramatic** (bump Playfair Display size)
- Tagline "להגדיר שקט מחדש" stays
- Date pickers stay but get **more transparent/elegant styling** (thinner borders, subtle glass effect)
- Scroll arrow stays

### 3. Breathing Image #1 (NEW)
- Full-width cinematic desert landscape photo
- `height: 50vh`, `object-fit: cover`
- CSS `background-attachment: fixed` for subtle parallax effect
- No text overlay — pure visual breathing space

### 4. About
- **Change layout** from single centered column to **two columns** (RTL):
  - Right: section label + title "הסוד של המדבר" + subtitle + text paragraphs
  - Left: sculpture photo (or film photo)
- All existing text content preserved
- On mobile: stacks vertically (text above, image below)

### 5. Accommodation (amenities + gallery + booking)
- **No changes** to content or structure
- Gallery images get **hover effect**: subtle zoom (scale 1.03) + slight brightness shift
- Optional: CSS lightbox on click (stretch goal)

### 6. Breathing Image #2 (NEW)
- Another full-width cinematic photo between accommodation and dark section
- Same treatment as Breathing Image #1

### 7. Dark Section (שקט / זה סוד / בינינו)
- **No changes** — already has the right artistic atmosphere
- Optional enhancement: **fade-in animation** on scroll (CSS `@keyframes` + `IntersectionObserver`)

### 8. Experience (חוויית אירוח מדברית)
- **No changes** to content
- Gallery images get same hover effect as accommodation gallery

### 9. Dining (לאכול במדבר)
- **No changes** — cards + restaurant modal stay as-is

### 10. Booking Bar (NEW)
- Full-width section with **desert background image** (dark, atmospheric)
- Horizontal form: תאריך כניסה | תאריך יציאה | אורחים (dropdown) | כפתור "הזמנה"
- Light text on dark background
- On mobile: stacks vertically
- Mirrors the booking bar from the Figma design

### 11. Practical Info (NEW)
- Two columns on light background:
  - Right column: "הזמינו חופשה בלב הערבה" heading + check-in 15:00 / check-out 11:00
  - Left column: cancellation policy (regular + holidays) — exact text from Figma:
    - Regular: 30 days = full refund, 14 days = 50%, <14 days = 75% charge
    - Holidays: 60 days = full refund, 30 days = 50%, <14 days = 75% charge
- On mobile: stacks vertically

### 12. Footer
- **No changes** — logo, address, contact, map, copyright

## Technical Approach

- **No new dependencies** — pure HTML/CSS, minimal vanilla JS
- Hero slideshow: JS for image rotation + CSS transitions for fade
- Parallax: CSS `background-attachment: fixed` (degrades gracefully on mobile)
- Scroll animations: `IntersectionObserver` + CSS classes (progressive enhancement)
- Gallery hover: CSS only (`transform: scale(1.03)` on `.gallery-img:hover`)
- All new sections use existing CSS custom properties (colors, fonts)
- Responsive: same breakpoints (768px, 480px)

## Design Tokens (unchanged)
- Fonts: Heebo (body), Playfair Display (headings)
- Colors: tobacco (#715141), toast (#A47760), pampas (#F0EBE5), wafer (#DFD5C8), dark (#1E1E1E), pink (#E91E8C)

## Files Changed
- `index.html` — add new sections (breathing images, booking bar, practical info), modify about layout, add slideshow markup
- `style.css` — new styles for slideshow, breathing images, two-column about, booking bar, practical info, hover effects, scroll animations
- `assets/` — may need additional photos for slideshow and breathing images

## Out of Scope
- Booking/reservation management system (future phase)
- Real phone/email (still placeholders)
- Restaurant recommendations content
- Exact map coordinates
