---
title: Snake game blog
permalink: /snake-game-blog/
---
This update to the Snake game introduces two main visual changes: the snake is now colored pink, and the food is represented by a yellow star instead of a simple square. The following explains the necessary code modifications and how these effects were achieved.

## Changing the Snake Color to Pink

The snake's color is controlled within the `drawSnakeDot` function, which draws each segment of the snake on the canvas. To change the snake's color, the fill style was updated to use the color `"pink"`.

```js
let drawSnakeDot = function(x, y){
    ctx.fillStyle = "pink";
    ctx.fillRect(x * BLOCK, y * BLOCK, BLOCK, BLOCK);
}
his modification ensures every segment of the snake appears in pink, replacing the previous color.

Drawing the Food as a Yellow Star

Replacing the default square food with a yellow star requires creating a new drawing function. The drawFoodStar function uses trigonometry to draw a 5-pointed star at the food's position.
let drawFoodStar = function(x, y){
    const cx = x * BLOCK + BLOCK/2;
    const cy = y * BLOCK + BLOCK/2;
    const spikes = 5;
    const outerRadius = BLOCK/2;
    const innerRadius = BLOCK/4;
    let rot = Math.PI/2*3;
    let step = Math.PI/spikes;

    ctx.beginPath();
    ctx.moveTo(cx, cy - outerRadius);
    for(let i = 0; i < spikes; i++){
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
In the main game loop, this function replaces the original food drawing code:
drawFoodStar(food.x, food.y);

## Summary

This update to the Snake game focused on improving the game's visual elements to create a more engaging and colorful experience. The snake's color was changed to pink by simply updating the fill style in the drawing function responsible for rendering each snake segment. This small but impactful change gives the snake a fresh, noticeable appearance.

More significantly, the food was transformed from a plain white square into a bright yellow star. This was achieved by creating a custom drawing function that uses trigonometry to plot the points of a 5-pointed star on the canvas. By setting the fill color to yellow before drawing the star, the food becomes visually distinct and more attractive.

These graphical improvements demonstrate how simple modifications in the canvas drawing code can greatly enhance the game's look and feel, making it more enjoyable for players. The changes also provide a foundation for further customization and creativity in game design.

