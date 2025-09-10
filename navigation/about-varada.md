---
layout: post
title: About
permalink: /about_Varada/
comments: true
---

## Hi, my name is Varada

## As a conversation starter


Here are some places I have lived.

<comment> Flags are made using Wikipedia images. Click flags for surprises! </comment>

<style>
.grid-container {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(150px, 1fr));
    gap: 10px;
}
.grid-item {
    text-align: center;
}
.grid-item img {
    width: 100%;
    height: 100px;
    object-fit: cover;
    border-radius: 10px;
}
.grid-item p {
    margin: 5px 0;
}
.food-gallery {
    display: flex;
    flex-wrap: wrap;
    gap: 12px;
    margin-top: 20px;
}
.food-tile {
    width: 120px;
    height: 120px;
    border-radius: 12px;
    background: #fff;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    box-shadow: 0 6px 14px rgba(16,24,40,0.06);
    cursor: pointer;
    font-size: 36px;
}
.food-tile p {
    margin: 6px 0 0 0;
    font-size: 14px;
    color: #333;
}
.fall-layer {
    position: fixed;
    left: 0;
    top: 0;
    right: 0;
    bottom: 0;
    pointer-events: none;
    z-index: 9999;
}
.emoji {
    position: fixed;
    left: 0;
    top: 0;
    font-size: 28px;
    will-change: transform, opacity;
    pointer-events: none;
    display: inline-block;
}
@keyframes fall {
    0% { transform: translateY(-20vh) rotate(0deg); opacity: 1; }
    80% { opacity: 1; }
    100% { transform: translateY(110vh) rotate(720deg); opacity: 0; }
}
</style>

<div class="grid-container" id="flag_grid"></div>

<script>
var flag_grid = document.getElementById("flag_grid");
var http_source = "https://upload.wikimedia.org/wikipedia/commons/";
var flags = [
    {flag: "0/01/Flag_of_California.svg", label: "California", emoji: "🐻"},
    {flag: "4/41/Flag_of_India.svg", label: "India", emoji: "🪷"}
];
for (const item of flags) {
    var gridItem = document.createElement("div");
    gridItem.className = "grid-item";

    var btn = document.createElement("button");
    btn.className = "flag-button";
    btn.style.border = "none";
    btn.style.background = "none";
    btn.title = `${item.label} flag — click for fun!`;

    var img = document.createElement("img");
    img.src = http_source + item.flag;
    img.alt = item.label + " flag";
    btn.appendChild(img);

    btn.addEventListener('click', function () {
        burstEmojis(item.emoji);
    });

    var label = document.createElement("p");
    label.textContent = item.label;

    gridItem.appendChild(btn);
    gridItem.appendChild(label);
    flag_grid.appendChild(gridItem);
}
</script>

<div class="fall-layer" id="fallLayer" aria-hidden="true"></div>

<script>
const fallLayer = document.getElementById('fallLayer');
function spawnEmojiAt(emoji, x, y, options = {}) {
    const el = document.createElement('div');
    el.className = 'emoji';
    el.textContent = emoji;
    const size = options.size || (18 + Math.floor(Math.random() * 30));
    el.style.fontSize = size + 'px';
    el.style.left = (x - size / 2) + 'px';
    el.style.top = (y - size / 2) + 'px';
    const duration = (options.duration || (2.5 + Math.random() * 3)).toFixed(2) + 's';
    el.style.animation = `fall ${duration} linear forwards`;
    fallLayer.appendChild(el);
    el.addEventListener('animationend', () => el.remove());
}
function burstEmojis(emoji, count = 12) {
    for (let i = 0; i < count; i++) {
        const x = Math.random() * window.innerWidth;
        const y = -20;
        spawnEmojiAt(emoji, x, y, {
            size: 22 + Math.random() * 28,
            duration: 2.6 + Math.random() * 3
        });
    }
}
</script>

---

### Background

Here's a bit about me.

- **Schools**  
  Torrey Hills Elementary, OVMS, CVMS  
  Del Norte High School

- **Family**  
  I have a 3-year-old sister.  
  I live with my parents and my sister.  
  I am the eldest child.

- **About Me**  
  My birthday is **October 9, 2009** 🎂  
  I'm **15 years old**  
  I'm a **Libra ♎**

---

### Favorite Foods

Click a food tile to drop emoji from the top of the screen 🍕🍪🍜

<div class="food-gallery">
  <div class="food-tile" data-emoji="🍜" role="button" tabindex="0" aria-label="Noodles">🍜<p>Noodles</p></div>
  <div class="food-tile" data-emoji="🍝" role="button" tabindex="0" aria-label="Pasta">🍝<p>Pasta</p></div>
  <div class="food-tile" data-emoji="🎂" role="button" tabindex="0" aria-label="Cake">🎂<p>Cake</p></div>
  <div class="food-tile" data-emoji="🍪" role="button" tabindex="0" aria-label="Cookies">🍪<p>Cookies</p></div>
  <div class="food-tile" data-emoji="🍕" role="button" tabindex="0" aria-label="Pizza">🍕<p>Pizza</p></div>
  <div class="food-tile" data-emoji="🍩" role="button" tabindex="0" aria-label="Donuts">🍩<p>Donuts</p></div>
</div>

<script>
document.querySelectorAll('.food-tile').forEach(tile => {
    const emoji = tile.getAttribute('data-emoji') || '🍽️';
    function trigger() {
        const rect = tile.getBoundingClientRect();
        for (let i = 0; i < 6; i++) {
            const x = rect.left + Math.random() * rect.width;
            spawnEmojiAt(emoji, x, -20, {
                size: 20 + Math.random() * 32,
                duration: 2.6 + Math.random() * 2.4
            });
        }
    }
    tile.addEventListener('click', trigger);
    tile.addEventListener('keydown', (e) => {
        if (e.key === 'Enter' || e.key === ' ') {
            e.preventDefault();
            trigger();
        }
    });
});
</script>

---

### Favorite Places to Visit 🌍

<div class="grid-container">
  <div class="grid-item">
    <img src="https://upload.wikimedia.org/wikipedia/commons/7/77/Paradise_Island_Bahamas.jpg" alt="Bahamas">
    <p>Bahamas 🏝️</p>
  </div>
  <div class="grid-item">
    <img src="https://upload.wikimedia.org/wikipedia/commons/4/4f/Alaska_Mountains.jpg" alt="Alaska">
    <p>Alaska ❄️</p>
  </div>
  <div class="grid-item">
    <img src="https://upload.wikimedia.org/wikipedia/commons/f/fc/Bali_rice_terraces.jpg" alt="Bali">
    <p>Bali 🌺</p>
  </div>
  <div class="grid-item">
    <img src="https://upload.wikimedia.org/wikipedia/commons/a/a8/Tour_Eiffel_Wikimedia_Commons.jpg" alt="Paris">
    <p>Paris 🗼</p>
  </div>
  <div class="grid-item">
    <img src="https://upload.wikimedia.org/wikipedia/commons/e/e3/Kheops-Pyramid.jpg" alt="Egypt">
    <p>Egypt 🏜️</p>
  </div>
</div>

---

### Hobbies 🎨✨

<div class="grid-container">
  <div class="grid-item">
    <img src="https://upload.wikimedia.org/wikipedia/commons/f/f4/Sunset_2007-1.jpg" alt="Watching the Sunset">
    <p>Watching the Sunset 🌅</p>
  </div>
  <div class="grid-item">
    <img src="https://upload.wikimedia.org/wikipedia/commons/c/c3/Crochet_yarn.jpg" alt="Crocheting">
    <p>Crocheting 🧶</p>
  </div>
  <div class="grid-item">
    <img src="https://upload.wikimedia.org/wikipedia/commons/b/b7/Pencil_drawing.jpg" alt="Drawing">
    <p>Drawing ✏️</p>
  </div>
  <div class="grid-item">
    <img src="https://upload.wikimedia.org/wikipedia/commons/3/3f/Camera_photography.jpg" alt="Photography">
    <p>Photography 📸</p>
  </div>
  <div class="grid-item">
    <img src="https://upload.wikimedia.org/wikipedia/commons/3/3a/Shopping_bags.jpg" alt="Shopping">
    <p>Shopping 🛍️</p>
  </div>
</div>

<footer style="margin-top:18px;color:#666;font-size:0.95rem">
  Made with ❤️ — try clicking the flags and food!
</footer>
