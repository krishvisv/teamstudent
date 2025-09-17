---
<<<<<<< HEAD:navigation/snake-blog.md
title: Snake Game Blog
=======
title: Snake Game Hack Blog
>>>>>>> c0913f49345cd0a6cfb75ce1d5db019ed494e604:_posts/Foundation/F-projects/2025-09-16-snake-blog.md
permalink: /snake-game-blog/
---

This update to the Snake game introduces two main visual changes:  
1. The snake is now colored **pink**.  
2. The food is represented by a **yellow star** instead of a simple square.  

Below, I’ll walk through the code modifications and explain how these effects were achieved.

---

## 🎨 Changing the Snake Color to Pink

The snake’s color is controlled inside the `drawSnakeDot` function, which renders each segment of the snake on the canvas.  
To make the snake pink, I updated the `fillStyle` to `"pink"`:

```js
let drawSnakeDot = function(x, y) {
    ctx.fillStyle = "pink";
    ctx.fillRect(x * BLOCK, y * BLOCK, BLOCK, BLOCK);
}
## ⭐ Drawing the Food as a Yellow Star

Instead of a plain square, the food is now drawn as a 5-pointed yellow star.
I created a custom function drawFoodStar that uses trigonometry to calculate the star’s points:

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
    ctx.fill();
}
## Finally, in the game loop, I replaced the old food drawing call with:
drawFoodStar(food.x, food.y);


## 📌 Summary

-The snake’s color was updated to pink with a simple fillStyle change.

-The food was upgraded from a plain square to a bright yellow star, using custom trigonometry-based drawing logic.

These small but impactful changes make the game look more fun, colorful, and engaging. 