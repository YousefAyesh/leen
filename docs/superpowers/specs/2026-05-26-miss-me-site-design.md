---
name: miss-me-site
description: Cute single-page "do you miss me?" site with fleeing No button and Dunkin yes page
metadata:
  type: project
---

# "Do You Miss Me?" Website

## Overview
A single `index.html` file (+ one image asset) deployed as a static site. Two pages rendered in-browser via JS — no server needed.

## Page 1 — Main Page
- Hot pink background (`#FF69B4`)
- 4 Tenor GIFs in a 2×2 responsive grid:
  - Cat warrior/shield (postid `4338452386513641626`)
  - Cat in love (postid `10000605937555107357`)
  - Cat licking popsicle (postid `3122588929262013745`)
  - Goth cat (postid `13580267959542514666`)
- Heading: "do you miss me? 🥺" — large, cute font (Google Fonts: Pacifico)
- Two buttons: **Yes 💕** and **No**
- "No" button behavior:
  - Desktop: `mousemove` listener detects cursor within 120px — button teleports to random safe position
  - Mobile: `touchstart` intercept — button teleports before tap registers, `pointer-events: none` during transition

## Page 2 — Yes Page (shown on Yes click)
- Same pink background
- Cat scuba dance GIF (postid `5034219186050115128`)
- Heading: "yay!! here is your favorite dunkin coffee ☕"
- Image: `dunkin.jpg` (user saves their Dunkin photo as this filename)

## Assets
- `dunkin.jpg` — user-provided Dunkin Iced Dunkalatte photo, placed in same folder as `index.html`
- All GIFs loaded via Tenor embed script

## Constraints
- Single `index.html` — no build tools, no frameworks
- Must work on iOS Safari and Android Chrome
- No button must be impossible to click on both desktop and mobile
