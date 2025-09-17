---
title: Snake Game Blog
permalink: /snake-game-blog/
---

https://krishvisv.github.io/teamstudent/snake

# Snake Game Update

This update to the Snake game introduces several visual and gameplay changes:  

- The snake is now colored **pink**.  
- The food is represented by a **yellow star** instead of a simple square.  
- Added **speed settings** to control the snake’s speed.  
- Added **WASD controls** in addition to arrow keys.  
- Introduced **multiple lives** (3 lives per game).  
- Added a **special pink square food** that gives bonus points and length.  
- Added **glowing effects** to the snake and food.  
- Overhauled the **menu, settings, and game over UI** for a modern look.  

Below, all code modifications and explanations are presented in Markdown.

---

## 🎨 Changing the Snake Color to Pink

The snake’s appearance is controlled inside the `drawSnakeDot` function, which draws each block of the snake on the canvas.  
To make the snake pink and add a glowing effect:

```
let drawSnakeDot = function(x, y) {
    ctx.fillStyle = "pink"; // Snake is now pink
    ctx.shadowColor = "cyan"; // Glowing effect
    ctx.shadowBlur = 10;
    ctx.fillRect(x * BLOCK, y * BLOCK, BLOCK, BLOCK);
    ctx.shadowBlur = 0;
}
```

---

## ⭐ Drawing the Food as a Yellow Star

Instead of a plain square, the food is now a **5-pointed yellow star** with glow.  
A custom function `drawFoodStar` calculates the points and draws the star:

```
let drawFoodStar = function(x, y) {
    const cx = x * BLOCK + BLOCK / 2;
    const cy = y * BLOCK + BLOCK / 2;
    const spikes = 5;
    const outerRadius = BLOCK / 2;
    const innerRadius = BLOCK / 4;
    let rot = Math.PI / 2 * 3;
    let step = Math.PI / spikes;

    ctx.beginPath();
    ctx.moveTo(cx, cy - outerRadius);
    for (let i = 0; i < spikes; i++) {
        let x1 = cx + Math.cos(rot) * outerRadius;
        let y1 = cy + Math.sin(rot) * outerRadius;
        ctx.lineTo(x1, y1);
        rot += step;

        let x2 = cx + Math.cos(rot) * innerRadius;
        let y2 = cy + Math.sin(rot) * innerRadius;
        ctx.lineTo(x2, y2);
        rot += step;
    }
    ctx.lineTo(cx, cy - outerRadius);
    ctx.closePath();
    ctx.fillStyle = "yellow";
    ctx.shadowColor = "yellow"; // Glow effect
    ctx.shadowBlur = 15;
    ctx.fill();
    ctx.shadowBlur = 0;
}
```
In the game loop, replace the old food drawing call with:

```
drawFoodStar(food.x, food.y);
```
---

## ⚡ Speed Settings

Players can now choose the snake’s speed in the settings screen: Slow, Normal, or Fast.  
This allows for more personalized gameplay:

```<p>Speed:
    <input id="speed1" type="radio" name="speed" value="120" checked/>
    <label for="speed1">Slow</label>
    <input id="speed2" type="radio" name="speed" value="75"/>
    <label for="speed2">Normal</label>
    <input id="speed3" type="radio" name="speed" value="35"/>
    <label for="speed3">Fast</label>
</p>
```

Clicking an option updates the snake’s movement interval.

---

## ⌨️ WASD Controls

The snake now responds to **WASD keys** in addition to arrow keys.  
This makes controlling the snake more flexible:

```
let changeDir = function(key){
    switch(key){
        case "ArrowUp": case "w": if(snake_dir!==2) snake_next_dir=0; break;
        case "ArrowRight": case "d": if(snake_dir!==3) snake_next_dir=1; break;
        case "ArrowDown": case "s": if(snake_dir!==0) snake_next_dir=2; break;
        case "ArrowLeft": case "a": if(snake_dir!==1) snake_next_dir=3; break;
    }
}
```

---

## ❤️ Multiple Lives

Players now start with **3 lives**, which appear on screen.  
Colliding with walls or self decreases a life instead of immediately ending the game:

```
let loseLife = function(){
    lives--;
    ele_lives.innerHTML = lives;
    if(lives <= 0){
        showScreen(SCREEN_GAME_OVER);
    } else {
        // Reset snake position
        snake = [{x:5, y:5}];
        snake_next_dir = 1;
    }
}
```

---

## 🍒 Special Pink Food

A new **pink square food** appears randomly, giving **+5 length and bonus points**:

```
let drawSpecialFood = function(x, y){
    ctx.fillStyle = "pink";
    ctx.shadowColor = "pink";
    ctx.shadowBlur = 15;
    ctx.fillRect(x*BLOCK, y*BLOCK, BLOCK, BLOCK);
    ctx.shadowBlur = 0;
}
```

---

## 🎨 UI Overhaul

The menu, settings, and game over screens were redesigned for a modern look.  
Hover effects, font sizes, and colors improve clarity and user experience:

```
#gameover a, #setting a, #menu a {
    font-size: 28px;
    margin: 10px 0;
    color: #ffcc00;
    transition: 0.3s;
}

#gameover a:hover, #setting a:hover, #menu a:hover {
    color: #ff66cc;
    text-shadow: 0 0 8px #fff;
}
```

---

## 📌 Summary

- ✅ Snake color updated to **pink** with glow.  
- ✅ Food updated to **yellow star** with glow.  
- ✅ **Speed settings** added (Slow, Normal, Fast).  
- ✅ **WASD controls** added.  
- ✅ **Multiple lives** system (3 lives).  
- ✅ **Special pink square food** with bonus growth.  
- ✅ **Glowing effects** applied to snake and food.  
- ✅ **Menu and settings UI** redesigned for modern look.