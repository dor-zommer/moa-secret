# MOA Secret Redesign — Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Enhance the existing static site with atmospheric design elements (slideshow, breathing images, booking bar, practical info) while preserving all current content and responsiveness.

**Architecture:** Layer new sections and effects onto the existing index.html + style.css. No frameworks, no build tools. Minimal vanilla JS for slideshow and scroll animations only.

**Tech Stack:** HTML, CSS, vanilla JavaScript

---

### Task 1: Hero Slideshow

**Files:**
- Modify: `index.html:28-54` (hero section)
- Modify: `style.css:110-234` (hero styles)

- [ ] **Step 1: Add slideshow images to hero HTML**

Replace the single `<img>` hero background with multiple stacked images:

```html
<!-- Hero -->
<section class="hero">
  <div class="hero-slideshow">
    <img src="assets/hero-bg.jpg" alt="" class="hero-slide hero-slide--active">
    <img src="assets/exp-sunset-group.jpg" alt="" class="hero-slide">
    <img src="assets/exp-aerial.jpg" alt="" class="hero-slide">
    <img src="assets/exp-oasis.jpg" alt="" class="hero-slide">
    <img src="assets/gallery-exterior.jpg" alt="" class="hero-slide">
  </div>
  <div class="hero-overlay"></div>
  <div class="hero-content">
    <!-- keep all existing hero-content unchanged -->
  </div>
</section>
```

- [ ] **Step 2: Add slideshow CSS**

Replace `.hero-bg` styles with:

```css
.hero-slideshow {
  position: absolute;
  inset: 0;
}

.hero-slide {
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
  opacity: 0;
  transition: opacity 1.5s ease-in-out;
}

.hero-slide--active {
  opacity: 1;
}
```

- [ ] **Step 3: Add slideshow JS at bottom of body**

```html
<script>
(function() {
  const slides = document.querySelectorAll('.hero-slide');
  let current = 0;
  setInterval(function() {
    slides[current].classList.remove('hero-slide--active');
    current = (current + 1) % slides.length;
    slides[current].classList.add('hero-slide--active');
  }, 6000);
})();
</script>
```

- [ ] **Step 4: Make hero title larger**

In `style.css`, inside `.hero-content`, bump the logo wrap size:

```css
.hero-logo-wrap {
  width: 300px;
  height: 300px;
  margin-bottom: 32px;
}
```

- [ ] **Step 5: Refine date picker styling**

Update `.date-input`:

```css
.date-input {
  /* change border to thinner, more transparent */
  border: 1px solid rgba(255, 255, 255, 0.12);
  background: rgba(255, 255, 255, 0.06);
}
```

- [ ] **Step 6: Verify in browser, commit**

```bash
git add index.html style.css
git commit -m "feat: hero image slideshow with fade transitions"
```

---

### Task 2: Breathing Images

**Files:**
- Modify: `index.html` (add sections after About and after Accommodation)
- Modify: `style.css` (add breathing image styles)

- [ ] **Step 1: Add breathing image HTML after About section (line ~69)**

```html
<!-- Breathing Image -->
<div class="breathing-img" style="background-image: url('assets/exp-sunset-people.jpg')"></div>
```

- [ ] **Step 2: Add second breathing image after Accommodation closing tag (line ~165)**

```html
<!-- Breathing Image -->
<div class="breathing-img" style="background-image: url('assets/exp-ancient.jpg')"></div>
```

- [ ] **Step 3: Add CSS**

```css
/* ========== Breathing Images ========== */
.breathing-img {
  width: 100%;
  height: 50vh;
  background-size: cover;
  background-position: center;
  background-attachment: fixed;
}

@media (max-width: 768px) {
  .breathing-img {
    background-attachment: scroll;
    height: 40vh;
  }
}
```

- [ ] **Step 4: Commit**

```bash
git add index.html style.css
git commit -m "feat: add full-width breathing images between sections"
```

---

### Task 3: About Section — Two Column Layout

**Files:**
- Modify: `index.html:57-69` (about section)
- Modify: `style.css:264-299` (about styles)

- [ ] **Step 1: Restructure About HTML to two columns**

```html
<section id="about" class="about">
  <div class="about-inner">
    <div class="about-text-col">
      <p class="section-label">על המקום</p>
      <h2 class="section-title">הסוד של המדבר</h2>
      <p class="about-subtitle">נמצא בלב הערבה, בנווה מדבר של שלווה ושפע.</p>
      <div class="about-text">
        <p>נמצא במואה שבלב הערבה, בנווה מדבר של שלווה ושפע.</p>
        <p>המתחם בנוי מחומרים טבעיים, מתוך הטבע, כחלק ממנו. אנחנו מאמינים באורח חיים של שקט, של יופי והתבוננות.</p>
        <p>אתם מוזמנים למצוא מנוחה לצד האגם, להנות בשכשוכית או בהאט טאב, ולטבול בדממת המדבר.</p>
      </div>
    </div>
    <div class="about-image-col">
      <img src="assets/about-sculpture.jpg" alt="פסל היד במדבר בלילה" class="about-img">
    </div>
  </div>
</section>
```

- [ ] **Step 2: Update About CSS**

Replace existing `.about` styles with:

```css
.about {
  padding: 120px 24px 80px;
  max-width: 1152px;
  margin: 0 auto;
}

.about-inner {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 64px;
  align-items: center;
}

.about-text-col {
  text-align: right;
}

.about-text-col .section-label,
.about-text-col .section-title {
  text-align: right;
}

.about-image-col {
  border-radius: 8px;
  overflow: hidden;
}

@media (max-width: 768px) {
  .about-inner {
    grid-template-columns: 1fr;
    gap: 40px;
  }

  .about-text-col .section-label,
  .about-text-col .section-title {
    text-align: center;
  }

  .about-text-col {
    text-align: center;
  }
}
```

- [ ] **Step 3: Commit**

```bash
git add index.html style.css
git commit -m "feat: about section two-column layout"
```

---

### Task 4: Gallery Hover Effects

**Files:**
- Modify: `style.css` (gallery img styles)

- [ ] **Step 1: Add hover effect to all gallery images**

```css
.gallery-img {
  /* add to existing rule */
  transition: transform 0.4s ease, filter 0.4s ease;
  overflow: hidden;
}

.gallery-col,
.exp-col {
  overflow: hidden;
  border-radius: 4px;
}

.gallery-img:hover {
  transform: scale(1.03);
  filter: brightness(1.05);
}
```

- [ ] **Step 2: Commit**

```bash
git add style.css
git commit -m "feat: gallery hover zoom effect"
```

---

### Task 5: Scroll Fade-In Animations

**Files:**
- Modify: `index.html` (add class to sections, add script)
- Modify: `style.css` (animation styles)

- [ ] **Step 1: Add CSS for fade-in**

```css
/* ========== Scroll Animations ========== */
.fade-in {
  opacity: 0;
  transform: translateY(24px);
  transition: opacity 0.8s ease, transform 0.8s ease;
}

.fade-in--visible {
  opacity: 1;
  transform: translateY(0);
}
```

- [ ] **Step 2: Add `fade-in` class to key sections in HTML**

Add `class="fade-in"` to: `.about-inner`, `.amenities`, `.gallery`, `.dark-panel` (each), `.experience-gallery`, `.dining-grid`

- [ ] **Step 3: Add IntersectionObserver script (before closing body)**

```html
<script>
(function() {
  var els = document.querySelectorAll('.fade-in');
  if (!('IntersectionObserver' in window)) {
    els.forEach(function(el) { el.classList.add('fade-in--visible'); });
    return;
  }
  var observer = new IntersectionObserver(function(entries) {
    entries.forEach(function(entry) {
      if (entry.isIntersecting) {
        entry.target.classList.add('fade-in--visible');
        observer.unobserve(entry.target);
      }
    });
  }, { threshold: 0.15 });
  els.forEach(function(el) { observer.observe(el); });
})();
</script>
```

- [ ] **Step 4: Commit**

```bash
git add index.html style.css
git commit -m "feat: scroll fade-in animations"
```

---

### Task 6: Booking Bar Section

**Files:**
- Modify: `index.html` (add section after dining)
- Modify: `style.css` (booking bar styles)

- [ ] **Step 1: Add booking bar HTML after dining section**

```html
<!-- Booking Bar -->
<section class="booking-bar" style="background-image: url('assets/exp-cabin-night.jpg')">
  <div class="booking-bar-overlay"></div>
  <div class="booking-bar-inner">
    <div class="booking-bar-field">
      <label class="booking-bar-label">כניסה</label>
      <input type="date" class="booking-bar-input" aria-label="תאריך כניסה">
    </div>
    <div class="booking-bar-field">
      <label class="booking-bar-label">יציאה</label>
      <input type="date" class="booking-bar-input" aria-label="תאריך יציאה">
    </div>
    <div class="booking-bar-field">
      <label class="booking-bar-label">אורחים</label>
      <select class="booking-bar-input booking-bar-select" aria-label="מספר אורחים">
        <option value="2">2</option>
        <option value="3">3</option>
        <option value="4">4</option>
      </select>
    </div>
    <button class="booking-bar-btn">הזמנה</button>
  </div>
</section>
```

- [ ] **Step 2: Add CSS**

```css
/* ========== Booking Bar ========== */
.booking-bar {
  position: relative;
  background-size: cover;
  background-position: center;
  padding: 80px 24px;
}

.booking-bar-overlay {
  position: absolute;
  inset: 0;
  background: rgba(0, 0, 0, 0.6);
}

.booking-bar-inner {
  position: relative;
  z-index: 1;
  display: flex;
  align-items: flex-end;
  justify-content: center;
  gap: 16px;
  max-width: 800px;
  margin: 0 auto;
  flex-wrap: wrap;
}

.booking-bar-field {
  display: flex;
  flex-direction: column;
  gap: 4px;
  flex: 1;
  min-width: 160px;
}

.booking-bar-label {
  font-size: 10px;
  font-weight: 400;
  letter-spacing: 0.5px;
  text-transform: uppercase;
  color: var(--white-60);
  text-align: center;
}

.booking-bar-input {
  width: 100%;
  padding: 12px 16px;
  background: rgba(255, 255, 255, 0.1);
  border: 1px solid rgba(255, 255, 255, 0.2);
  border-radius: 6px;
  color: var(--white);
  font-family: var(--font-body);
  font-size: 14px;
  text-align: center;
  outline: none;
  transition: border-color 0.2s;
}

.booking-bar-input:focus {
  border-color: rgba(255, 255, 255, 0.4);
}

.booking-bar-select {
  appearance: none;
  cursor: pointer;
}

.booking-bar-input::-webkit-calendar-picker-indicator {
  filter: invert(1);
  opacity: 0.6;
  cursor: pointer;
}

.booking-bar-btn {
  font-family: var(--font-body);
  font-weight: 500;
  font-size: 12px;
  letter-spacing: 1.2px;
  text-transform: uppercase;
  color: var(--pampas-bg);
  background: var(--toast);
  border: none;
  border-radius: 6px;
  padding: 14px 40px;
  cursor: pointer;
  transition: background 0.2s;
}

.booking-bar-btn:hover {
  background: var(--tobacco);
}

@media (max-width: 768px) {
  .booking-bar-inner {
    flex-direction: column;
    align-items: stretch;
  }

  .booking-bar-field {
    min-width: auto;
  }

  .booking-bar-btn {
    width: 100%;
  }
}
```

- [ ] **Step 3: Commit**

```bash
git add index.html style.css
git commit -m "feat: booking bar with desert background"
```

---

### Task 7: Practical Info Section

**Files:**
- Modify: `index.html` (add section before footer)
- Modify: `style.css` (practical info styles)

- [ ] **Step 1: Add practical info HTML before footer**

```html
<!-- Practical Info -->
<section class="practical-info">
  <div class="practical-inner">
    <div class="practical-col practical-col--booking">
      <h2 class="practical-title">הזמינו חופשה בלב הערבה</h2>
      <div class="practical-times">
        <p>צ׳ק אין ב-15:00</p>
        <p>צ׳ק אאוט ב-11:00</p>
      </div>
    </div>
    <div class="practical-col practical-col--policy">
      <div class="policy-block">
        <h3 class="policy-heading">מדיניות ביטולים והחזרים:</h3>
        <p>ביטול עד 30 יום ממועד האירוח: החזר מלא של המקדמה או שתוכלו להשאיר את המקדמה לזכותכם למועד אחר.</p>
        <p>ביטול עד 14 ימים ממועד האירוח: החזר של 50% מסכום המקדמה.</p>
        <p>ביטול של פחות מ-14 יום יחויב ב-75% מהעלות.</p>
      </div>
      <div class="policy-block">
        <h3 class="policy-heading">ביטולים בחגים:</h3>
        <p>ביטול עד 60 יום ממועד האירוח: החזר מלא של המקדמה.</p>
        <p>ביטול עד 30 ימים ממועד האירוח: החזר של 50% מסכום המקדמה.</p>
        <p>ביטול של פחות מ-14 יום יחויב ב-75% מהעלות.</p>
      </div>
    </div>
  </div>
</section>
```

- [ ] **Step 2: Add CSS**

```css
/* ========== Practical Info ========== */
.practical-info {
  padding: 80px 24px;
  max-width: 1152px;
  margin: 0 auto;
  border-top: 1px solid var(--wafer);
}

.practical-inner {
  display: grid;
  grid-template-columns: 1fr 1.5fr;
  gap: 64px;
  align-items: start;
}

.practical-title {
  font-family: var(--font-serif);
  font-weight: 600;
  font-size: 28px;
  color: var(--tobacco-80);
  margin-bottom: 24px;
  line-height: 1.3;
}

.practical-times p {
  font-size: 18px;
  color: var(--tobacco-80);
  line-height: 32px;
}

.policy-block {
  margin-bottom: 24px;
}

.policy-heading {
  font-family: var(--font-body);
  font-weight: 500;
  font-size: 15px;
  color: var(--tobacco);
  margin-bottom: 8px;
}

.policy-block p {
  font-size: 14px;
  line-height: 26px;
  color: var(--tobacco-60);
  margin-bottom: 4px;
}

@media (max-width: 768px) {
  .practical-inner {
    grid-template-columns: 1fr;
    gap: 40px;
    text-align: center;
  }
}
```

- [ ] **Step 3: Commit**

```bash
git add index.html style.css
git commit -m "feat: practical info section with check-in times and cancellation policy"
```

---

### Task 8: Final Polish & Verify

- [ ] **Step 1: Verify all sections render correctly in browser**
- [ ] **Step 2: Test responsive at 768px and 480px**
- [ ] **Step 3: Check RTL alignment across all new sections**
- [ ] **Step 4: Final commit**

```bash
git add -A
git commit -m "polish: final responsive and RTL adjustments"
```
