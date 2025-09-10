---
layout: post
title: About
permalink: /about/
comments: true
---

# Hi, my name is Krishna

## Here are some of my interests .


- Music
- Painting
- Sewing
- Beadwork
- Fashion
- Taco Bell. I love taco bell.

<img src="https://upload.wikimedia.org/wikipedia/en/b/b3/Taco_Bell_2016.svg" alt="taco bell logo">

<comment>
places
<comment>

<style>
    /* Style looks pretty compact, 
       - grid-container and grid-item are referenced the code 
    */
    .grid-container {
        display: grid;
        grid-template-columns: repeat(auto-fill, minmax(150px, 1fr)); /* Dynamic columns */
        gap: 10px;
    }
    .grid-item {
        text-align: center;
    }
    .grid-item img {
        width: 100%;
        height: 100px; /* Fixed height for uniformity */
        object-fit: contain; /* Ensure the image fits within the fixed height */
    }
    .grid-item p {
        margin: 5px 0; /* Add some margin for spacing */
    }

    .image-gallery {
        display: flex;
        flex-wrap: nowrap;
        overflow-x: auto;
        gap: 10px;
        }

    .image-gallery img {
        max-height: 150px;
        object-fit: cover;
        border-radius: 5px;
    }
</style>

<!-- This grid_container class is used by CSS styling and the id is used by JavaScript connection -->
<div class="grid-container" id="grid_container">
    <!-- content will be added here by JavaScript -->
</div>

<script>
    // 1. Make a connection to the HTML container defined in the HTML div
    var container = document.getElementById("grid_container"); // This container connects to the HTML
    // 2. Define a JavaScript object for our http source and our data rows for the Living in the World grid
    var http_source = "https://upload.wikimedia.org/wikipedia/commons/";
    var living_in_the_world = [
        {"flag": "0/01/Flag_of_California.svg", "greeting": "Hey", "description": "California - forever"},
        {"flag": "/4/41/Flag_of_India.svg", "greeting": "Namaste or Namaskaram", "description": "Never lived here but my parents did till 2003"},
    ];

    // 3a. Consider how to update style count for size of container
    // The grid-template-columns has been defined as dynamic with auto-fill and minmax

    // 3b. Build grid items inside of our container for each row of data
    for (const location of living_in_the_world) {
        // Create a "div" with "class grid-item" for each row
        var gridItem = document.createElement("div");
        gridItem.className = "grid-item";  // This class name connects the gridItem to the CSS style elements
        // Add "img" HTML tag for the flag
        var img = document.createElement("img");
        img.src = http_source + location.flag; // concatenate the source and flag
        img.alt = location.flag + " Flag"; // add alt text for accessibility

        // Add "p" HTML tag for the description
        var description = document.createElement("p");
        description.textContent = location.description; // extract the description

        // Add "p" HTML tag for the greeting
        var greeting = document.createElement("p");
        greeting.textContent = location.greeting;  // extract the greeting

        // Append img and p HTML tags to the grid item DIV
        gridItem.appendChild(img);
        gridItem.appendChild(description);
        gridItem.appendChild(greeting);

        // Append the grid item DIV to the container DIV
        container.appendChild(gridItem);
    }
</script>


# Journey through Life

How I Got to Where I Am

- 🏫 Elementary School at Stone Ranch Elementary School
- 🏫 Middle and High School in Glendale (CA), Hoover High graduated '77
- 🎓 Glendale CA Community College, UCLA Extension, LA Wilshire Computer Tech School '77 to '79
- ⛪ England, London Missionary for Church of Jesus Christ of Latter-day Saints '79 to '81
- 💼 Culver City, Glendale CA founder at Ashton-Tate, original PC's dBase 2 and 3 '82 to '87
- 🎓 Eugene Oregon Undergraduate CompSci Degree at University of Oregon (Go Ducks!) '89 to '91
- 💼 Eugene Oregon, founder and owner @ Microniche `88, Point Control CAD CAM developer '91 to '96
- 🏢 San Diego CA Qualcomm, Satellite Comm and 1st Mobile OS (BREW) '96 to '19
- 👨‍🏫 San Diego CA Teacher of Computer Science @ Del Norte High School San Diego '19 to present

### Culture, Family, and Fun

The mango is an important memento to me realizing i typed baseur1 and not baseurl and finally getting images to work..

- My friends and music are really important to me
- One of my favorite bands is a local band called Citrus Jr. I go to a lot of their concerts and I love local shows generally, as well as all music
- There are photos of my friends from across the states, a lot of whom are from the east coast. I met them at a summer program I did at Georgia Tech and I miss them every day
- Finding time for the people I love always makes me grateful for the life I live and the people I've met

<comment>
Gallery of Pics, scroll to the right for more ...
</comment>
<div class="image-gallery">
<img src="{{site.baseurl}}/images/krishna_images/mango_test.jpg" alt="pleaseeeeeeee">
  <img src="{{site.baseurl}}/images/krishna_images/2025_grad.jpg" alt="2025 grad">
  <img src="{{site.baseurl}}/images/krishna_images/belmont_park.jpg" alt="belmont park">
  <img src="{{site.baseurl}}/images/krishna_images/georgia_tech_aquarium.jpg" alt="georgia aquarium">
  <img src="{{site.baseurl}}/images/krishna_images/hoco.jpg" alt="hoco">
  <img src="{{site.baseurl}}/images/krishna_images/mcr.jpg" alt="mcr">
  <img src="{{site.baseurl}}/images/krishna_images/me_and_tanishqa.jpg" alt="driving jk parked">
  <img src="{{site.baseurl}}/images/krishna_images/us_on_christmas.jpg" alt="christmas">
  <img src="{{site.baseurl}}/images/krishna_images/prom.jpg" alt="prom">
  <img src="{{site.baseurl}}/images/krishna_images/us_at_citrus.jpg" alt="citrus jr">
</div>

# Hi, my name is Varada. 
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


# Hi I'm Anwita 

## Here's a little about me

Here is where I have lived and my ethnic homeland

<comment>
Flags are made using Wikipedia images
</comment>

<style>
    /* Style looks pretty compact, 
       - grid-container and grid-item are referenced the code 
    */
    .grid-container {
        display: grid;
        grid-template-columns: repeat(auto-fill, minmax(150px, 1fr)); /* Dynamic columns */
        gap: 10px;
    }
    .grid-item {
        text-align: center;
    }
    .grid-item img {
        width: 100%;
        height: 100px; /* Fixed height for uniformity */
        object-fit: contain; /* Ensure the image fits within the fixed height */
    }
    .grid-item p {
        margin: 5px 0; /* Add some margin for spacing */
    }

    .image-gallery {
        display: flex;
        flex-wrap: nowrap;
        overflow-x: auto;
        gap: 10px;
        }

    .image-gallery img {
        max-height: 150px;
        object-fit: cover;
        border-radius: 5px;
    }
</style>

<!-- This grid_container class is used by CSS styling and the id is used by JavaScript connection -->
<div class="grid-container" id="grid_container">
    <!-- content will be added here by JavaScript -->
</div>

<script>
    // 1. Make a connection to the HTML container defined in the HTML div
    var container = document.getElementById("grid_container"); // This container connects to the HTML div

    // 2. Define a JavaScript object for our http source and our data rows for the Living in the World grid
    var living_in_the_world = [
        {"img": "https://upload.wikimedia.org/wikipedia/commons/0/01/Flag_of_California.svg", "greeting": "Hey, like-", "description": "California - SUNNY DAYS"},
        {"img": "https://upload.wikimedia.org/wikipedia/commons/4/41/Flag_of_India.svg", "greeting": "Namaste", "description": "India - family roots"}
    ];

    // 3a. Consider how to update style count for size of container
    // The grid-template-columns has been defined as dynamic with auto-fill and minmax

    // 3b. Build grid items inside of our container for each row of data
    for (const location of living_in_the_world) {
        var gridItem = document.createElement("div");
        gridItem.className = "grid-item";
        var img = document.createElement("img");
        img.src = location.img;
        img.alt = location.description;
        var description = document.createElement("p");
        description.textContent = location.description;
        var greeting = document.createElement("p");
        greeting.textContent = location.greeting;
        gridItem.appendChild(img);
        gridItem.appendChild(description);
        gridItem.appendChild(greeting);
        container.appendChild(gridItem);
    }
</script>

### Journey through Life

Here is what I did at those places

- 🏫 I lived in San Diego since birth, going to Monterey Elementary School in 4S Ranch

- 🏫 Middle and High School in 4S Ranch (CA), Current Junior at Del Norte Highschool

- 💃I completed my Dance Arangetram in the summer of 2025 after 9 years of dance

- 🎓 Part of the Del Norte Varsity Golf Team 

- 🧫 Part of the DNHS iGEM team and work with the Yeo Lab at UCSD

- 🍵My dream job is to join own a matcha cafe and have a pet samoyed.

<style>
  .receipt-container {
    position: relative;
    margin: 20px 0;
  }

  .receipt-btn {
    background-color: #576e35ff; /* matcha green */
    color: white;
    padding: 10px 20px;
    border-radius: 8px;
    font-weight: bold;
    cursor: pointer;
    border: none;
    transition: background 0.2s ease;
  }

  .receipt-btn:hover {
    background-color: #576e35ff;
  }

  .receipt {
    max-height: 0;
    overflow: hidden;
    background: #f1eadaff;   
    font-family: monospace;
    border: 2px dashed #aba4a0ff;
    border-radius: 6px;
    margin-top: 10px;
    padding: 0 15px;
    width: 220px;
    transition: max-height 0.6s ease;
  }

  .receipt.open {
    max-height: 500px; /* enough room to expand */
    padding: 15px;
  }

  .receipt h4 {
    margin: 0 0 10px 0;
    text-align: center;
    border-bottom: 1px dashed #aaa;
    padding-bottom: 5px;
    color: #576e35ff !important;
  }

  .receipt p {
    margin: 4px 0;
    color: #6d5430ff !important;
  }

  .receipt .total {
    margin-top: 10px;
    border-top: 1px dashed #aaa;
    padding-top: 5px;
    text-align: right;
    font-weight: bold;
  }
</style>

<div class="receipt-container">
  <button class="receipt-btn" onclick="toggleReceipt()">🍵 Reveal My Matcha Order</button>
  <div class="receipt" id="receipt" style="color: #6d5430ff;">
  <h4 style="color: #6d5430ff;">Matcha Order</h4>
  <p style="color: #6d5430ff;">Drink: Iced Matcha Latte</p>
  <p style="color: #6d5430ff;">Sweetness: 50% Sugar</p>
  <p style="color: #6d5430ff;">Ice: Light Ice</p>
  <p style="color: #6d5430ff;">Size: Regular</p>
    <div class="total">Total: $5.50</div>
  </div>
</div>

<script>
  function toggleReceipt() {
    const receipt = document.getElementById("receipt");
    receipt.classList.toggle("open");
  }
</script>

### Culture, Family, and Fun

Everything for me, revolves around my friends and family. 

- I am 100% Indian but my dad is from North India and my mom is from South India

- I have an older sister named Aditi. People say we look alike, but no one in my family thinks so. 

- I have 6 cousins and I'm the youngest in my extended family. I'm also the only left handed person in my whole family. 

- My favorite show is Money Heist, but I don't watch a lot of TV. My favorite character is Tigger from Winnie the Pooh

- In my free time, I enjoy listening to music and going to local cafes with my friends!🧋☕ 

<h3>Here's some of my Favorite Music</h3>
<iframe data-testid="embed-iframe" style="border-radius:12px" src="https://open.spotify.com/embed/track/4QhWbupniDd44EDtnh2bFJ?utm_source=generator" width="100%" height="252" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture" loading="lazy"></iframe>
<iframe data-testid="embed-iframe" style="border-radius:12px" src="https://open.spotify.com/embed/track/0QyJXG36Q3Kta662XS8GhY?utm_source=generator" width="100%" height="252" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture" loading="lazy"></iframe>
<iframe data-testid="embed-iframe" style="border-radius:12px" src="https://open.spotify.com/embed/track/4S4Mfvv03M1cHgIOJcbUCL?utm_source=generator" width="100%" height="252" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture" loading="lazy"></iframe>

<comment>
I also really like food. Here's some of my favorite foods!🍝
</comment>
<div class="image-gallery">
  <img src="https://thefoodiediaries.co/wp-content/uploads/2023/03/img_2354-e1678956380440.jpg" alt="Image 1">
  <img src="https://i0.wp.com/smittenkitchen.com/wp-content/uploads/2021/02/rigatoni-alla-vodka-1-scaled.jpg?fit=1200%2C800&ssl=1" alt="Image 2">
  <img src="https://fox5sandiego.com/wp-content/uploads/sites/15/2023/04/raisingcanes-800x500-1.jpg?w=800" alt="Image 3">
  <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRGxTF-6-po8yNTZBmLaP4Wo3JPT3BQ9KJxFg&s" alt="Image 4">
  <img src="https://whatsinthepan.com/wp-content/uploads/2019/02/Chicken-Parmesan-2.jpg" alt="Image 5">
  <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSRP8TT5yrQL9VLVB84RX1BA8CGcfiV7t6MzQ&s" alt="Image 6">
  <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcR_JV1CFPpG-TVY6BN2y5Ko2_YNJSPH9RgaPg&s" alt="Image 7">
  <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSl_p-_Z2acLuScUHEEcw8nSp8GuxLFA8XS2w&s" alt="Image 8">
  <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRhG9pMi3c_TCEJr-jp2mGRfAxM4E-BSK4ulQ&s" alt="Image 9">
</div>


