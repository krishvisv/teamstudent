---
layout: post
title: "Background Hack — Mountains Sunset"
date: 2025-09-16
permalink: /sprint/1/background-hack-update
tags: [background-hack, platformer, assets]
background: "images/platformer/backgrounds/starwars background.jpeg"
---

# Background Hack Update

**Updated site (with new background):** https://krishvisv.github.io/student/background

**Short write-up (what we changed & how):**

- We replaced the original "space" background with a mountains and sunset background.
- How we did it:
  1. Downloaded the desired background image from the web and saved it locally.
  2. Added the image file into the repository under `images/platformer/backgrounds/` and named the file `starwars background.jpeg`.
     - (Note: I originally downloaded the picture as a PNG, but the file in the repo is placed/renamed as `starwars background.jpeg` so the front matter references that filename.)
  3. Updated the page's YAML front matter to point to the new image by setting the `background` field to:
     ```
     background: "images/platformer/backgrounds/starwars background.jpeg"
     ```
  4. Committed and pushed the change to the repo so the GitHub Pages site (linked above) now serves the new mountains + sunset background.