---
toc: True
layout: post
data: tools
title: Whack-a-Mole Hack Blog
description: A Whack-a-Mole game rebuilt with OOP JavaScript — now featuring a 4×4 grid, new mole types, power-ups, scaling difficulty, and high score tracking.
permalink: /github/pages/whack_a_mole_changes
breadcrumbs: True
---

## 🔄 These are the hacks I did to the Whack a Mole Game

Here’s what’s different from the original Whack-a-Mole game:

### 🎮 Gameplay & Features
- Expanded grid from **3×3 (9 holes)** → **4×4 (16 holes)**.  
- Added **keyboard controls** (press number keys 1–16 to whack).  
- Increased **canvas size** from 400×400 → 450×450.  
- Added **difficulty scaling** (spawn speed increases with score).  
- Added **high score tracking** (saved with `localStorage`).  
- Added **multiplier system** (x2 points for 5 seconds).  

### 🐹 Mole & Power-Ups
- 🟢 **Green Mole (Normal):** +10 points. Lose 1 life if missed.  
- 🟡 **Golden Mole:** +30 points. Lose 1 life if missed.  
- 🔵 **Blue Mole (New):** +50 points but also speeds up the game.  
- 🔴 **Red Bomb:** Changed behavior → now **-1 life if hit** (instead of ending the game instantly).  
- 🌸 **Pink Power-up (Double):** Double points for 5 seconds.  
- 🔵 **Cyan Power-up (Life):** +1 life.  e

## 🔧 Code Changes in Whack-a-Mole

### 🟦 New Mole Type: Blue Mole
- Added a **blue mole** worth **+50 points**.  
- Each hit also **speeds up the game** by reducing the spawn interval.  
- Implemented in the `Mole` class (`constructor`, `draw`, `onHit`) and `spawnEntity()`.

### 🔢 Grid Expansion
- Changed grid from **3×3 (9 holes)** → **4×4 (16 holes)**.  
- Updated:
  - `gridSize` property.  
  - Hole creation loop (now generates 16 holes).  
  - Keyboard controls to map keys **1–16**.  
- Increased canvas size from **400×400 → 450×450** to fit the larger board.  

## A New Mole Type 🟦

I introduced a blue mole that shakes things up. Unlike regular moles, hitting the blue mole gives players +50 points, but there’s a catch—it also makes the game speed up. This twist forces players to think strategically: is it worth the risk of making the game harder just to rack up extra points?

## Bigger Grid 🟩

The original game used a 3×3 grid, but I expanded it to a 4×4 grid. With more holes for moles to appear in, players have to be sharper and faster to keep up. This change makes the game have more variety, and increases the difficulty in a natural way.