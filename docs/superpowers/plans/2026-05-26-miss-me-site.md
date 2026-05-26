# Miss Me Site Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build a single `index.html` static site with a "do you miss me?" page featuring a fleeing No button, and a Dunkin yes-page revealed on Yes click.

**Architecture:** All logic lives in one `index.html` — inline CSS and a single `<script>` block. Two "pages" are `<div>` sections toggled with `display: none / flex`. No build tools, no dependencies beyond Google Fonts and the Tenor embed script.

**Tech Stack:** Vanilla HTML/CSS/JS, Google Fonts (Pacifico), Tenor embed API

---

## File Map

| File | Action | Responsibility |
|------|--------|---------------|
| `index.html` | Create | Entire site — markup, styles, JS |
| `dunkin.jpg` | Pre-existing | User-provided Dunkin photo (must be in same folder) |

---

### Task 1: HTML skeleton + pink background + fonts

**Files:**
- Create: `index.html`

- [ ] **Step 1: Create `index.html` with base structure**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>do you miss me?</title>
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
  <link href="https://fonts.googleapis.com/css2?family=Pacifico&family=Nunito:wght@700;900&display=swap" rel="stylesheet" />
  <style>
    * { box-sizing: border-box; margin: 0; padding: 0; }

    body {
      background-color: #FF69B4;
      min-height: 100vh;
      font-family: 'Nunito', sans-serif;
      display: flex;
      align-items: center;
      justify-content: center;
    }

    .page {
      display: none;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      width: 100%;
      min-height: 100vh;
      padding: 24px 16px;
      text-align: center;
    }

    .page.active {
      display: flex;
    }
  </style>
</head>
<body>
  <div id="page1" class="page active"></div>
  <div id="page2" class="page"></div>

  <script>
    // JS goes here in later tasks
  </script>
</body>
</html>
```

- [ ] **Step 2: Open in browser and verify**

Open `index.html` in a browser. Expected: solid hot-pink full-screen page, no errors in console.

- [ ] **Step 3: Commit**

```bash
git init
git add index.html
git commit -m "feat: pink skeleton with page toggle structure"
```

---

### Task 2: Page 1 — GIF grid + heading

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add GIF grid styles to `<style>`**

Add inside the `<style>` block:

```css
.gif-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 12px;
  width: 100%;
  max-width: 560px;
  margin-bottom: 28px;
}

.gif-grid > div {
  border-radius: 16px;
  overflow: hidden;
  box-shadow: 0 4px 16px rgba(0,0,0,0.2);
}

h1 {
  font-family: 'Pacifico', cursive;
  font-size: clamp(2rem, 6vw, 3.5rem);
  color: #fff;
  text-shadow: 2px 4px 8px rgba(0,0,0,0.2);
  margin-bottom: 32px;
}
```

- [ ] **Step 2: Populate `#page1` with GIFs and heading**

Replace the empty `<div id="page1" class="page active"></div>` with:

```html
<div id="page1" class="page active">
  <div class="gif-grid">
    <div>
      <div class="tenor-gif-embed" data-postid="4338452386513641626" data-share-method="host" data-aspect-ratio="1" data-width="100%">
        <a href="https://tenor.com/view/cat-shield-bashing-warrior-banging-gif-4338452386513641626">Cat Shield GIF</a>
      </div>
    </div>
    <div>
      <div class="tenor-gif-embed" data-postid="10000605937555107357" data-share-method="host" data-aspect-ratio="1.02049" data-width="100%">
        <a href="https://tenor.com/view/kitty-cat-cat-in-love-in-love-cat-happy-gif-10000605937555107357">Kitty Cat Meme</a>
      </div>
    </div>
    <div>
      <div class="tenor-gif-embed" data-postid="3122588929262013745" data-share-method="host" data-aspect-ratio="0.564257" data-width="100%">
        <a href="https://tenor.com/view/cat-licking-popsicle-gif-3122588929262013745">Cat Licking GIF</a>
      </div>
    </div>
    <div>
      <div class="tenor-gif-embed" data-postid="13580267959542514666" data-share-method="host" data-aspect-ratio="0.924686" data-width="100%">
        <a href="https://tenor.com/view/goth-goth-cat-black-goth-cat-cat-black-cat-gif-13580267959542514666">Goth Cat GIF</a>
      </div>
    </div>
  </div>
  <h1>do you miss me? 🥺</h1>
  <!-- buttons added in Task 3 -->
</div>
<script type="text/javascript" async src="https://tenor.com/embed.js"></script>
```

- [ ] **Step 3: Open in browser and verify**

Expected: 2×2 grid of cat GIFs above the pink-background heading "do you miss me? 🥺". GIFs animate. No console errors.

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add GIF grid and heading to page 1"
```

---

### Task 3: Buttons — layout and base styles

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add button styles to `<style>`**

```css
.btn-row {
  display: flex;
  gap: 20px;
  align-items: center;
  justify-content: center;
  flex-wrap: wrap;
}

.btn {
  font-family: 'Nunito', sans-serif;
  font-size: 1.4rem;
  font-weight: 900;
  padding: 14px 40px;
  border: none;
  border-radius: 50px;
  cursor: pointer;
  box-shadow: 0 6px 20px rgba(0,0,0,0.2);
  transition: transform 0.1s;
}

.btn-yes {
  background: #fff;
  color: #FF69B4;
}

.btn-yes:hover { transform: scale(1.06); }

.btn-no {
  background: #c0392b;
  color: #fff;
  position: fixed; /* repositioned by JS */
  transition: left 0.08s, top 0.08s;
}
```

- [ ] **Step 2: Add button markup inside `#page1` below the `<h1>`**

Replace the `<!-- buttons added in Task 3 -->` comment:

```html
<div class="btn-row">
  <button class="btn btn-yes" id="btnYes">yes 💕</button>
  <button class="btn btn-no"  id="btnNo">no</button>
</div>
```

- [ ] **Step 3: Open in browser and verify**

Expected: Two styled buttons below the heading. Yes button is white/pink, No button is red. Neither does anything yet.

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add styled yes/no buttons"
```

---

### Task 4: No button — desktop flee logic

**Files:**
- Modify: `index.html` (`<script>` block)

- [ ] **Step 1: Replace the empty script block with flee logic**

```html
<script>
  const btnNo = document.getElementById('btnNo');

  // ── Initial placement ──────────────────────────────────────────────
  // Position the No button at its natural layout spot on load,
  // then switch it to fixed so JS can reposition freely.
  function initNoBtn() {
    const rect = btnNo.getBoundingClientRect();
    btnNo.style.left = rect.left + 'px';
    btnNo.style.top  = rect.top  + 'px';
    btnNo.style.width = rect.width + 'px';
  }

  window.addEventListener('load', initNoBtn);
  window.addEventListener('resize', initNoBtn);

  // ── Desktop flee ───────────────────────────────────────────────────
  const FLEE_RADIUS = 130; // px — how close the mouse has to get

  function randomSafePos(bw, bh) {
    const margin = 20;
    const x = margin + Math.random() * (window.innerWidth  - bw - margin * 2);
    const y = margin + Math.random() * (window.innerHeight - bh - margin * 2);
    return { x, y };
  }

  document.addEventListener('mousemove', (e) => {
    const rect = btnNo.getBoundingClientRect();
    const cx = rect.left + rect.width  / 2;
    const cy = rect.top  + rect.height / 2;
    const dist = Math.hypot(e.clientX - cx, e.clientY - cy);

    if (dist < FLEE_RADIUS) {
      const { x, y } = randomSafePos(rect.width, rect.height);
      btnNo.style.left = x + 'px';
      btnNo.style.top  = y + 'px';
    }
  });

  // ── Yes button ─────────────────────────────────────────────────────
  document.getElementById('btnYes').addEventListener('click', () => {
    document.getElementById('page1').classList.remove('active');
    document.getElementById('page2').classList.add('active');
  });
</script>
```

- [ ] **Step 2: Open in browser and verify on desktop**

Move the mouse toward the No button. Expected: button jumps away before the cursor gets within ~130px. Button stays within the viewport. Yes button does nothing yet (page2 is empty).

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "feat: no button flees cursor on desktop"
```

---

### Task 5: No button — mobile flee logic

**Files:**
- Modify: `index.html` (`<script>` block)

- [ ] **Step 1: Add touch handler inside the `<script>` block, after the `mousemove` listener**

```js
// ── Mobile flee ────────────────────────────────────────────────────
btnNo.addEventListener('touchstart', (e) => {
  e.preventDefault(); // block the tap from registering as a click
  const rect = btnNo.getBoundingClientRect();
  const { x, y } = randomSafePos(rect.width, rect.height);
  btnNo.style.left = x + 'px';
  btnNo.style.top  = y + 'px';
}, { passive: false });
```

- [ ] **Step 2: Verify on mobile (or DevTools device mode)**

Open DevTools → toggle device toolbar (iPhone or Android preset). Tap toward the No button. Expected: button slides to a random spot before the tap lands, never triggering a click. Yes button still works.

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "feat: no button flees on mobile touch"
```

---

### Task 6: Page 2 — Yes page (scuba cat + Dunkin)

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add page 2 styles to `<style>`**

```css
.yes-page {
  gap: 24px;
}

.yes-page h1 {
  font-size: clamp(1.8rem, 5vw, 3rem);
}

.yes-gif {
  width: 100%;
  max-width: 340px;
  border-radius: 20px;
  overflow: hidden;
  box-shadow: 0 6px 24px rgba(0,0,0,0.25);
}

.dunkin-img {
  width: 100%;
  max-width: 300px;
  border-radius: 20px;
  box-shadow: 0 6px 24px rgba(0,0,0,0.25);
  object-fit: cover;
}
```

- [ ] **Step 2: Populate `#page2`**

Replace the empty `<div id="page2" class="page"></div>` with:

```html
<div id="page2" class="page yes-page">
  <h1>yay!! here is your favorite dunkin coffee ☕</h1>
  <div class="yes-gif">
    <div class="tenor-gif-embed" data-postid="5034219186050115128" data-share-method="host" data-aspect-ratio="0.995984" data-width="100%">
      <a href="https://tenor.com/view/cat-scuba-dance-gif-5034219186050115128">Cat Scuba GIF</a>
    </div>
  </div>
  <p style="font-size:1.3rem;color:#fff;font-weight:900;text-shadow:1px 2px 6px rgba(0,0,0,0.2);">
    Medium Iced Dunkalatte 🧋
  </p>
  <img class="dunkin-img" src="dunkin.jpg" alt="Medium Iced Dunkalatte" />
</div>
```

- [ ] **Step 3: Save `dunkin.jpg`**

Save the Dunkin Iced Dunkalatte photo to the same folder as `index.html`, named exactly `dunkin.jpg`.

- [ ] **Step 4: Open in browser and verify**

Click "yes 💕". Expected: page switches to the scuba cat GIF, "yay!!" heading, "Medium Iced Dunkalatte 🧋" label, and the Dunkin photo. All centered on pink background.

- [ ] **Step 5: Commit**

```bash
git add index.html dunkin.jpg
git commit -m "feat: add yes page with scuba cat and dunkin coffee"
```

---

### Task 7: Final polish + cross-device check

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add a heart-confetti animation on Yes click**

Add to `<style>`:

```css
@keyframes floatUp {
  0%   { opacity: 1; transform: translateY(0) scale(1); }
  100% { opacity: 0; transform: translateY(-120px) scale(1.4); }
}

.heart {
  position: fixed;
  font-size: 2rem;
  pointer-events: none;
  animation: floatUp 1.2s ease-out forwards;
  z-index: 999;
}
```

Replace the Yes click handler in the `<script>` with:

```js
document.getElementById('btnYes').addEventListener('click', (e) => {
  // spawn hearts at click position
  for (let i = 0; i < 8; i++) {
    const h = document.createElement('span');
    h.className = 'heart';
    h.textContent = ['💕','💖','🩷','💗'][Math.floor(Math.random()*4)];
    h.style.left = (e.clientX + (Math.random()-0.5)*80) + 'px';
    h.style.top  = (e.clientY + (Math.random()-0.5)*40) + 'px';
    document.body.appendChild(h);
    h.addEventListener('animationend', () => h.remove());
  }
  setTimeout(() => {
    document.getElementById('page1').classList.remove('active');
    document.getElementById('page2').classList.add('active');
  }, 400);
});
```

- [ ] **Step 2: Full cross-device smoke test**

| Check | Expected |
|-------|----------|
| Desktop Chrome — hover near No | Button flees |
| Desktop — click Yes | Hearts burst, page 2 appears |
| DevTools iPhone SE — tap No | Button jumps away |
| DevTools iPhone SE — tap Yes | Hearts + page 2 |
| GIFs load | All 5 Tenor GIFs animate |
| `dunkin.jpg` shows | Photo visible on yes page |
| No horizontal scroll | Layout contained on all sizes |

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "feat: heart confetti on yes click, final polish"
```

---

## Self-Review

**Spec coverage:**
- ✅ Pink background
- ✅ 4 GIFs on main page (warrior cat, cat in love, cat licking popsicle, goth cat)
- ✅ "do you miss me? 🥺" heading
- ✅ Yes / No buttons
- ✅ No button flees mouse on desktop
- ✅ No button flees on mobile tap
- ✅ Yes → scuba cat GIF + Dunkin photo + coffee name
- ✅ Mobile-friendly (viewport meta, clamp fonts, responsive grid)

**Placeholders:** None — all code blocks are complete.

**Type consistency:** `btnNo`, `randomSafePos`, `initNoBtn` used consistently across Tasks 4 and 5.
