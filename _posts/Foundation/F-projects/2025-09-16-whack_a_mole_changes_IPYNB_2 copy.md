---
toc: True
layout: post
data: tools
title: Whack-a-Mole Hack Blog
description: A Whack-a-Mole game rebuilt with OOP JavaScript — now featuring a 4×4 grid, new mole types, power-ups, scaling difficulty, and high score tracking. Done by: Anwita, Aashika, and Krishna
permalink: /github/pages/whack_a_mole_changes
breadcrumbs: True
---

## 🔄 These are the hacks I did to the Whack a Mole Game

Here’s what’s different from the original Whack-a-Mole game:

## A New Mole Type 🟦

I introduced a blue mole that shakes things up. Unlike regular moles, hitting the blue mole gives players +50 points, but there’s a catch, it also makes the game speed up. This effect forces players to think strategically: is it worth the risk of making the game harder just to rack up extra points?

## Bigger Grid 🟩

The original game used a 3×3 grid, but I expanded it to a 4×4 grid. With more holes for moles to appear in, players have to be sharper and faster to keep up. This change makes the game have more variety, and increases the difficulty in a not so boring way.

### Code Changes to Add the Hacks

### 1. Game Instructions and Info
I first had to change the game information
- Before: "Click the moles or press number keys (1–9) to score."
- After: "Click the moles or press number keys (1–16) to score."

**Code Changes**
```diff
-Click the moles or press number keys (1–9) to score.  
+Click the moles or press number keys (1–16) to score. 
```
+ - 🔵 **Blue Mole:** +50 points and speeds up game. Lose **1 life** if missed.  

### 2. Game Board Size
- Before: this.gridSize = 3; (3x3 grid)
- After: this.gridSize = 4; (4x4 grid)

**Code Changes**
```diff
-      this.gridSize = 3;
+      this.gridSize = 4;
```

### 3. Key Press Handling
- Before: Allowed keys 1–9.
- After: Allowed keys 1–16.

**Code Changes**
```diff
-      for (const key in this.keys) {
-        if (this.keys[key] && !isNaN(key)) {
-          const num = parseInt(key);
-          const hole = this.holes.find(h => h.index === num);
-          if (hole && hole.entity) hole.entity.onHit(this);
-          this.keys[key] = false;
-        }
-      }
+      for (const key in this.keys) {
+        if (this.keys[key] && !isNaN(key)) {
+          const num = parseInt(key);
+          // Only allow keys 1-16 for 4x4 grid
+          if (num >= 1 && num <= 16) {
+            const hole = this.holes.find(h => h.index === num);
+            if (hole && hole.entity) hole.entity.onHit(this);
+          }
+          this.keys[key] = false;
+        }
+      }
```

### 4. Mole Types and Spawning 
- Before: Only "normal", "golden", and "bomb" moles.
- After: Added "blue" mole and adjusted spawn probabilities:
  - "normal": 60%
  - "golden": 15%
  - "bomb": 13%
  - "blue": 8%
  - Power-ups: (Double or Life): 4% (2% each)

**Code Changes**:
```diff
-      const r = Math.random();
-      if (r < 0.7) this.moles.push(new Mole(hole, "normal"));
-      else if (r < 0.85) this.moles.push(new Mole(hole, "golden"));
-      else if (r < 0.95) this.moles.push(new Mole(hole, "bomb"));
-      else {
-        const type = Math.random() < 0.5 ? "double" : "life";
-        this.moles.push(new PowerUp(hole, type));
-      }
+      const r = Math.random();
+      if (r < 0.6) this.moles.push(new Mole(hole, "normal"));
+      else if (r < 0.75) this.moles.push(new Mole(hole, "golden"));
+      else if (r < 0.88) this.moles.push(new Mole(hole, "bomb"));
+      else if (r < 0.96) this.moles.push(new Mole(hole, "blue"));
+      else {
+        const type = Math.random() < 0.5 ? "double" : "life";
+        this.moles.push(new PowerUp(hole, type));
+      }
```

### 5. Mole Class
- Before: No "blue" mole.
- After: Added "blue" mole with:
  - 50 points on hit
  - Speeds up the game (reduces spawn interval)


**Code Changes**
```diff
-    onHit(game){
-      if(this.type==="normal") game.addScore(10);
-      else if(this.type==="golden") game.addScore(30);
-      else if(this.type==="bomb") game.lives--;
-      this.hit = true;
-      this.hole.entity = null;
+    onHit(game){
+      if(this.type==="normal") game.addScore(10);
+      else if(this.type==="golden") game.addScore(30);
+      else if(this.type==="bomb") game.lives--;
+      else if(this.type==="blue") {
+        game.addScore(50);
+        game.spawnInterval = Math.max(300, game.spawnInterval - 200);
+      }
+      this.hit = true;
+      this.hole.entity = null;
```
```diff
-    constructor(hole, type="normal") {
-      const durations = { normal:1000, golden:800, bomb:1000 };
-      super(hole, durations[type]);
-      this.type = type;
+    constructor(hole, type="normal") {
+      const durations = { normal:1000, golden:800, bomb:1000, blue:700 };
+      super(hole, durations[type] || 1000);
+      this.type = type;
```

- Before: Mole colors: brown, gold, black.
- After: Mole colors: brown, gold, black, blue (#649dcbff). I also changed the brown mole color to make it look better but the main addition is the blue color.

```diff
-      ctx.beginPath();
-      if (this.type === "normal") ctx.fillStyle = "#8b4513"; // brown mole
-      else if (this.type === "golden") ctx.fillStyle = "gold";
-      else if (this.type === "bomb") ctx.fillStyle = "black";
-
-      // Main mole body (slight ellipse)
-      ctx.ellipse(cx, cy, r * 0.8, r, 0, 0, Math.PI * 2);
-      ctx.fill();
+      ctx.beginPath();
+      if (this.type === "normal") ctx.fillStyle = "#735a48ff"; // brown mole
+      else if (this.type === "golden") ctx.fillStyle = "gold";
+      else if (this.type === "bomb") ctx.fillStyle = "black";
+      else if (this.type === "blue") ctx.fillStyle = "#649dcbff"; // blue mole
+      ctx.ellipse(cx, cy, r * 0.8, r, 0, 0, Math.PI * 2);
+      ctx.fill();
```


## Link to Updated Game
https://anwitabandaru-gif.github.io/student/whack_a_mole/