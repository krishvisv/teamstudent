---
layout: base
title: Snake Game
permalink: /snake/
---

<style>
    body {
        background-color: #121212; /* Dark background */
        font-family: Arial, sans-serif;
        color: white;
    }
    .wrap {
        margin-left: auto;
        margin-right: auto;
    }
    canvas {
        display: none;
        border-style: solid;
        border-width: 10px;
        border-color: #FFFFFF;
        background-color: #1a1a1a;
        box-shadow: 0 0 20px rgba(255,255,255,0.3);
    }
    canvas:focus {
        outline: none;
    }

    /* UI overhaul */
    #gameover p, #setting p, #menu p {
        font-size: 22px;
    }
    #gameover a, #setting a, #menu a {
        font-size: 28px;
        display: block;
        margin: 10px 0;
        text-decoration: none;
        color: #ffcc00;
        transition: 0.3s;
    }
    #gameover a:hover, #setting a:hover, #menu a:hover {
        cursor: pointer;
        color: #ff66cc;
        text-shadow: 0 0 8px #fff;
    }

    #menu { display: block; }
    #gameover, #setting { display: none; }

    #setting input { display:none; }
    #setting label {
        cursor: pointer;
        border: 1px solid #fff;
        padding: 4px 8px;
        border-radius: 5px;
        margin: 3px;
    }
    #setting input:checked + label {
        background-color: #FFF;
        color: #000;
    }
</style>

<h2>Snake</h2>
<div class="container">
    <p class="fs-4">Score: <span id="score_value">0</span> | Lives: <span id="lives_value">3</span></p>

    <div class="container bg-secondary" style="text-align:center;">
        <!-- Main Menu -->
        <div id="menu" class="py-4 text-light">
            <p>Welcome to Snake, press <span style="background-color: #FFFFFF; color: #000000">space</span> to begin</p>
            <a id="new_game">New Game</a>
            <a id="setting_menu">Settings</a>
        </div>
        <!-- Game Over -->
        <div id="gameover" class="py-4 text-light">
            <p>Game Over, press <span style="background-color: #FFFFFF; color: #000000">space</span> to try again</p>
            <a id="new_game1">New Game</a>
            <a id="setting_menu1">Settings</a>
        </div>
        <!-- Play Screen -->
        <canvas id="snake" class="wrap" width="320" height="320" tabindex="1"></canvas>
        <!-- Settings Screen -->
        <div id="setting" class="py-4 text-light">
            <p>Settings (press <span style="background-color: #FFFFFF; color: #000000">space</span> to return)</p>
            <a id="new_game2">New Game</a>
            <br>
            <p>Speed:
                <input id="speed1" type="radio" name="speed" value="120" checked/>
                <label for="speed1">Slow</label>
                <input id="speed2" type="radio" name="speed" value="75"/>
                <label for="speed2">Normal</label>
                <input id="speed3" type="radio" name="speed" value="35"/>
                <label for="speed3">Fast</label>
            </p>
            <p>Wall:
                <input id="wallon" type="radio" name="wall" value="1" checked/>
                <label for="wallon">On</label>
                <input id="walloff" type="radio" name="wall" value="0"/>
                <label for="walloff">Off</label>
            </p>
        </div>
    </div>
</div>

<script>
(function(){
    const canvas = document.getElementById("snake");
    const ctx = canvas.getContext("2d");

    const BLOCK = 10;
    const SCREEN_MENU = -1, SCREEN_SNAKE = 0, SCREEN_GAME_OVER = 1, SCREEN_SETTING = 2;

    const screen_snake = document.getElementById("snake");
    const ele_score = document.getElementById("score_value");
    const ele_lives = document.getElementById("lives_value");
    const speed_setting = document.getElementsByName("speed");
    const wall_setting = document.getElementsByName("wall");

    const screen_menu = document.getElementById("menu");
    const screen_game_over = document.getElementById("gameover");
    const screen_setting = document.getElementById("setting");

    const button_new_game = document.getElementById("new_game");
    const button_new_game1 = document.getElementById("new_game1");
    const button_new_game2 = document.getElementById("new_game2");
    const button_setting_menu = document.getElementById("setting_menu");
    const button_setting_menu1 = document.getElementById("setting_menu1");

    let SCREEN = SCREEN_MENU;
    let snake, snake_dir, snake_next_dir, snake_speed;
    let food = {x:0,y:0}, specialFood = {x:-1,y:-1}; 
    let score, wall, lives;

    function showScreen(screen_opt){
        SCREEN = screen_opt;
        screen_snake.style.display = (screen_opt===SCREEN_SNAKE)? "block":"none";
        screen_menu.style.display = (screen_opt===SCREEN_MENU)? "block":"none";
        screen_setting.style.display = (screen_opt===SCREEN_SETTING)? "block":"none";
        screen_game_over.style.display = (screen_opt===SCREEN_GAME_OVER)? "block":"none";
    }

    window.onload = function(){
        button_new_game.onclick = ()=>newGame();
        button_new_game1.onclick = ()=>newGame();
        button_new_game2.onclick = ()=>newGame();
        button_setting_menu.onclick = ()=>showScreen(SCREEN_SETTING);
        button_setting_menu1.onclick = ()=>showScreen(SCREEN_SETTING);

        setSnakeSpeed(120);
        for(let i=0;i<speed_setting.length;i++){
            speed_setting[i].addEventListener("click", ()=>{
                if(speed_setting[i].checked){ setSnakeSpeed(speed_setting[i].value); }
            });
        }

        setWall(1);
        for(let i=0;i<wall_setting.length;i++){
            wall_setting[i].addEventListener("click", ()=>{
                if(wall_setting[i].checked){ setWall(wall_setting[i].value); }
            });
        }

        window.addEventListener("keydown", function(evt) {
            if(evt.code==="Space" && SCREEN!==SCREEN_SNAKE) newGame();
        }, true);
    }

    function mainLoop(){
        let _x = snake[0].x;
        let _y = snake[0].y;
        snake_dir = snake_next_dir;
        switch(snake_dir){
            case 0:_y--;break; case 1:_x++;break; case 2:_y++;break; case 3:_x--;break;
        }

        snake.pop();
        snake.unshift({x:_x,y:_y});

        // Wall collision
        if(wall==1){
            if(_x<0||_x>=canvas.width/BLOCK||_y<0||_y>=canvas.height/BLOCK){ loseLife(); return; }
        } else {
            if(_x<0)snake[0].x+=canvas.width/BLOCK;
            if(_x>=canvas.width/BLOCK)snake[0].x-=canvas.width/BLOCK;
            if(_y<0)snake[0].y+=canvas.height/BLOCK;
            if(_y>=canvas.height/BLOCK)snake[0].y-=canvas.height/BLOCK;
        }

        // Self collision
        for(let i=1;i<snake.length;i++){
            if(snake[0].x===snake[i].x && snake[0].y===snake[i].y){ loseLife(); return; }
        }

        // Eat normal food
        if(checkBlock(snake[0].x,snake[0].y,food.x,food.y)){
            growSnake(3);
            altScore(++score);
            addFood();
            maybeAddSpecial();
        }

        // Eat special food
        if(checkBlock(snake[0].x,snake[0].y,specialFood.x,specialFood.y)){
            growSnake(5);
            score+=5;
            altScore(score);
            specialFood.x=-1;
        }

        // Draw
        ctx.fillStyle = "#222";
        ctx.fillRect(0,0,canvas.width,canvas.height);

        snake.forEach((s,i)=>drawSnakeDot(s.x,s.y,i===0));
        drawFoodStar(food.x,food.y);
        if(specialFood.x>=0) drawSpecialFood(specialFood.x,specialFood.y);

        setTimeout(mainLoop,snake_speed);
    }

    function newGame(){
        showScreen(SCREEN_SNAKE);
        screen_snake.focus();
        score=0; altScore(score);
        lives=3; ele_lives.innerHTML=lives;
        snake=[{x:5,y:5}];
        snake_next_dir=1;
        addFood();
        specialFood.x=-1;
        canvas.onkeydown=(evt)=>changeDir(evt.key);
        mainLoop();
    }

    function loseLife(){
        lives--;
        ele_lives.innerHTML=lives;
        if(lives<=0){ showScreen(SCREEN_GAME_OVER); }
        else{ snake=[{x:5,y:5}]; snake_next_dir=1; mainLoop(); }
    }

    function changeDir(key){
        switch(key){
            case "ArrowUp": case "w": if(snake_dir!==2)snake_next_dir=0; break;
            case "ArrowRight": case "d": if(snake_dir!==3)snake_next_dir=1; break;
            case "ArrowDown": case "s": if(snake_dir!==0)snake_next_dir=2; break;
            case "ArrowLeft": case "a": if(snake_dir!==1)snake_next_dir=3; break;
        }
    }

    function drawSnakeDot(x,y,isHead){
        ctx.fillStyle = isHead? "#ff66cc":"#00ffcc";
        ctx.shadowColor = "cyan";
        ctx.shadowBlur = 10;
        ctx.fillRect(x*BLOCK,y*BLOCK,BLOCK,BLOCK);
        ctx.shadowBlur=0;
    }

    function drawFoodStar(x,y){
        const cx=x*BLOCK+BLOCK/2, cy=y*BLOCK+BLOCK/2;
        const spikes=5, outer=BLOCK/2, inner=BLOCK/4;
        let rot=Math.PI/2*3, step=Math.PI/spikes;
        ctx.beginPath();
        ctx.moveTo(cx,cy-outer);
        for(let i=0;i<spikes;i++){
            ctx.lineTo(cx+Math.cos(rot)*outer,cy+Math.sin(rot)*outer);
            rot+=step;
            ctx.lineTo(cx+Math.cos(rot)*inner,cy+Math.sin(rot)*inner);
            rot+=step;
        }
        ctx.closePath();
        ctx.fillStyle="yellow";
        ctx.shadowColor="yellow";
        ctx.shadowBlur=15;
        ctx.fill();
        ctx.shadowBlur=0;
    }

    function drawSpecialFood(x,y){
        ctx.fillStyle="pink";
        ctx.shadowColor="pink";
        ctx.shadowBlur=15;
        ctx.fillRect(x*BLOCK,y*BLOCK,BLOCK,BLOCK);
        ctx.shadowBlur=0;
    }

    function addFood(){
        food.x=Math.floor(Math.random()*(canvas.width/BLOCK));
        food.y=Math.floor(Math.random()*(canvas.height/BLOCK));
    }
    function maybeAddSpecial(){
        if(Math.random()<0.3){ // 30% chance
            specialFood.x=Math.floor(Math.random()*(canvas.width/BLOCK));
            specialFood.y=Math.floor(Math.random()*(canvas.height/BLOCK));
        }
    }

    function growSnake(amount){
        for(let i=0;i<amount;i++){ snake.push({...snake[snake.length-1]}); }
    }

    function checkBlock(x,y,_x,_y){ return (x===_x&&y===_y); }
    function altScore(v){ ele_score.innerHTML=String(v); }
    function setSnakeSpeed(v){ snake_speed=v; }
    function setWall(v){ wall=v; }
})();
</script>
