---
layout: post
title: About
permalink: /Anwita_about/
comments: true
---

## About me!

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
        {"img": "https://upload.wikimedia.org/wikipedia/commons/0/01/Flag_of_California.svg", "greeting": "Hey,", "description": "California - SUNNY DAYS"},
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

Most importantly, my birthday is on 05/05/09
