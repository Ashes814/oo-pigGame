# 欧欧变小猪-js小游戏

游戏地址：[https://oo-piggame.netlify.app](https://oo-piggame.netlify.app/)

# 1. 规则介绍

<aside>
💡 小猪游戏是一个数字博弈游戏，由两名玩家进行游戏，分别扮演`猪猪1号`以及`猪猪2号`；游戏开始时由猪猪1号投骰子，投到2-5之间的数字后表示猪猪1号此次吃了相应点数的饭，猪猪1号可以选择`吃饱`或继续投骰子，如果`吃饱`，则将本轮得分加到总得分上，接下来由猪猪2号`吃饭`（投骰子），如果选择继续投骰子，则可以继续将投到的点数加到当前饭量中，直到自己选择吃饱或着投出点数1，点数1表示吃吐，本轮游戏中之前吃到的点数全部作废且交换玩家进行游戏。谁的总分率先达到`100分`即获胜。

</aside>

# 2. 文件准备与制作html

## 2.1. 要素准备

- 创建文件
    - html+css+js分别对应一个文件
    - 骰子图片6张

![Untitled](%E6%AC%A7%E6%AC%A7%E5%8F%98%E5%B0%8F%E7%8C%AA-js%E5%B0%8F%E6%B8%B8%E6%88%8F%20205916d6eed04561a929157aaf7ff95d/Untitled.png)

- 游戏区
    - 猪猪1号与猪猪2号的信息
- 按钮区
    - 新游戏
    - 投骰子
    - 吃饱
- 骰子

![Untitled](%E6%AC%A7%E6%AC%A7%E5%8F%98%E5%B0%8F%E7%8C%AA-js%E5%B0%8F%E6%B8%B8%E6%88%8F%20205916d6eed04561a929157aaf7ff95d/Untitled%201.png)

![Untitled](%E6%AC%A7%E6%AC%A7%E5%8F%98%E5%B0%8F%E7%8C%AA-js%E5%B0%8F%E6%B8%B8%E6%88%8F%20205916d6eed04561a929157aaf7ff95d/Untitled%202.png)

- 代码
    
    ```html
    <!DOCTYPE html>
    <html lang="zh">
      <head>
        <meta charset="UTF-8" />
        <meta http-equiv="X-UA-Compatible" content="IE=edge" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <link rel="stylesheet" href="style.css" />
        <title>欧欧变小猪</title>
      </head>
      <body>
        <main>
          <section class="player player--0 player--active">
            <h2 class="name" id="name--0">🐷猪猪1号</h2>
            <p class="score" id="score--0">43</p>
            <div class="current">
              <p class="current-label">这顿饭</p>
              <p class="current-score" id="current--0">0</p>
            </div>
          </section>
          <section class="player player--1">
            <h2 class="name" id="name--1">🐷猪猪2号</h2>
            <p class="score" id="score--1">24</p>
            <div class="current">
              <p class="current-label">这顿饭</p>
              <p class="current-score" id="current--1">0</p>
            </div>
          </section>
    
          <img src="img/dice-5.png" alt="游戏骰子" class="dice" />
          <button class="btn btn--new">🔄 生成新猪猪</button>
          <button class="btn btn--roll">🎲 猪猪多吃饭</button>
          <button class="btn btn--hold">📥 猪猪吃饱了</button>
        </main>
        <script src="script.js"></script>
      </body>
    </html>
    ```
    

# 3. 创建css

- flex进行主要布局
- 按钮与骰子的位置通过绝对位置布局
- 背景采用紫色渐变
- 代码

```css
@import url("https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&family=ZCOOL+KuaiLe&display=swap");

* {
  margin: 0;
  padding: 0;
  box-sizing: inherit;
}

html {
  font-size: 62.5%;
  box-sizing: border-box;
}

body {
  font-family: "ZCOOL KuaiLe", sans-serif;
  font-weight: 400;
  height: 100vh;
  color: #333;
  background-image: linear-gradient(to top left, #753682 0%, #bf2e34 100%);
  display: flex;
  align-items: center;
  justify-content: center;
}

/* LAYOUT */
main {
  position: relative;
  width: 100rem;
  height: 60rem;
  background-color: rgba(255, 255, 255, 0.35);
  backdrop-filter: blur(200px);
  filter: blur();
  box-shadow: 0 3rem 5rem rgba(0, 0, 0, 0.25);
  border-radius: 9px;
  overflow: hidden;
  display: flex;
}

.player {
  flex: 50%;
  padding: 9rem;
  display: flex;
  flex-direction: column;
  align-items: center;
  transition: all 0.75s;
}

/* ELEMENT */
.name {
  position: relative;
  font-size: 4rem;
  text-transform: uppercase;
  letter-spacing: 1px;
  word-spacing: 2px;
  font-weight: 300;
  margin-bottom: 1rem;
}

.score {
  font-size: 8rem;
  font-weight: 300;
  color: #c7365f;
  margin-bottom: auto;
}

.player--active {
  background-color: rgba(255, 255, 255, 0.4);
}

.player--active .name {
  font-weight: 700;
}

.player--active .score {
  font-weight: 400;
}

.player--active .current {
  opacity: 1;
}

.current {
  background-color: #cf365f;
  opacity: 0.8;
  border-radius: 9px;
  color: #fff;
  width: 65%;
  padding: 2rem;
  text-align: center;
  transition: all 0.75s;
}

.current-label {
  text-transform: uppercase;
  margin-bottom: 1rem;
  font-size: 1.7rem;
  color: #ddd;
}

.current-score {
  font-size: 3.5rem;
}

/* Absolute Positioned Elements */
.btn {
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
  color: #444;
  background-color: none;
  border: none;
  font-family: inherit;
  font-size: 1.8rem;
  text-transform: uppercase;
  cursor: pointer;
  font-weight: 400;
  transition: all 0.2s;

  background-color: white;
  background-color: rgba(255, 255, 255, 0.6);
  backdrop-filter: blur(10px);

  padding: 0.7rem 2.5rem;
  border-radius: 50rem;
  box-shadow: 0 1.75rem 3.5rem rgba(0, 0, 0, 0.1);
}

.btn::first-letter {
  font-size: 2.4rem;
  display: inline-block;
  margin-right: 0.7rem;
}

.btn--new {
  top: 4rem;
}

.btn--roll {
  top: 39.3rem;
}

.btn--hold {
  top: 46.1rem;
}

.btn:active {
  transform: translate(-50%, 3px);
  box-shadow: 0 1rem 2rem rgba(0, 0, 0, 0.15);
}

.btn:focus {
  outline: none;
}

.dice {
  position: absolute;
  left: 50%;
  top: 16.5rem;
  transform: translateX(-50%);
  height: 10rem;
  box-shadow: 0 2rem 5rem rgba(0, 0, 0, 0.2);
}

.player--winner {
  background-color: #2f2f2f;
}

.player--winner .name {
  font-weight: 700;
  color: #c7365f;
}

.hidden {
  display: none;
}
```

# 4. js功能

## 4.1 选择html要素

- 这里通过`querySelector`与`getElementById`选择要素

```jsx
"use strict";

// SELECTING ELEMENTS
const player0El = document.querySelector(".player--0");
const player1El = document.querySelector(".player--1");
const score0El = document.querySelector("#score--0");
const score1El = document.getElementById("score--1");
const current0El = document.getElementById("current--0");
const current1El = document.getElementById("current--1");

const diceEl = document.querySelector(".dice");
const btnNew = document.querySelector(".btn--new");
const btnRoll = document.querySelector(".btn--roll");
const btnHold = document.querySelector(".btn--hold");

let scores, currentScore, activePlayer, playing;
```

## 4.2 初始化函数

- 将两位猪猪的得分存在一个数组score 中
- 将所有的分数变量与分数显示设置为0
- 将激活的玩家设置为0
- 隐藏不需要的要素

```jsx
// Starting Conditions
const init = function () {
  scores = [0, 0];
  currentScore = 0;
  activePlayer = 0;
  playing = true;

  score0El.textContent = 0;
  score1El.textContent = 0;
  current0El.textContent = 0;
  current1El.textContent = 0;

  diceEl.classList.add("hidden");
  player0El.classList.remove("player--winner");
  player1El.classList.remove("player--winner");
  player0El.classList.add("player--active");
  player1El.classList.remove("player--active");
};
init();
```

## 4.3 游戏核心功能

- 创建交换玩家的函数
    - 将当前玩家的本顿饭设置为0
    - 若当前玩家为0则交换为1
- 创建投骰子函数
    - 若为1，则调用交换玩家函数，显示警告
    - 若为其他，则将当前分数加入本次饭中
- 创建吃饱了函数
    - 转换玩家
    - 若总分大于100，则游戏结束

## 4.4. 完整代码

```jsx
"use strict";

// SELECTING ELEMENTS
const player0El = document.querySelector(".player--0");
const player1El = document.querySelector(".player--1");
const score0El = document.querySelector("#score--0");
const score1El = document.getElementById("score--1");
const current0El = document.getElementById("current--0");
const current1El = document.getElementById("current--1");

const diceEl = document.querySelector(".dice");
const btnNew = document.querySelector(".btn--new");
const btnRoll = document.querySelector(".btn--roll");
const btnHold = document.querySelector(".btn--hold");

let scores, currentScore, activePlayer, playing;

// Starting Conditions
const init = function () {
  scores = [0, 0];
  currentScore = 0;
  activePlayer = 0;
  playing = true;

  score0El.textContent = 0;
  score1El.textContent = 0;
  current0El.textContent = 0;
  current1El.textContent = 0;

  diceEl.classList.add("hidden");
  player0El.classList.remove("player--winner");
  player1El.classList.remove("player--winner");
  player0El.classList.add("player--active");
  player1El.classList.remove("player--active");
};
init();

const switchPlayer = function () {
  document.getElementById(`current--${activePlayer}`).textContent = 0;
  currentScore = 0;
  activePlayer = activePlayer === 0 ? 1 : 0;
  player0El.classList.toggle("player--active");
  player1El.classList.toggle("player--active");
};

// Rolling dice functionality;
btnRoll.addEventListener("click", function () {
  if (playing) {
    // 1. Generating a random dice roll
    const dice = Math.trunc(Math.random() * 6) + 1;

    // 2. Display a dice
    diceEl.classList.remove("hidden");
    diceEl.src = `img/dice-${dice}.png`;

    // 3. Check for rolled 1
    if (dice !== 1) {
      // Add dice to current score
      currentScore += dice;
      document.getElementById(`current--${activePlayer}`).textContent =
        currentScore;
    } else {
      // Switch to next player
      alert(`猪猪${activePlayer + 1}号吃撑了，把之前吃的都吐了🤮`);
      switchPlayer();
    }
  }
});

btnHold.addEventListener("click", function () {
  if (playing) {
    // 1. Add current score to active player's score
    scores[activePlayer] += currentScore;
    document.getElementById(`score--${activePlayer}`).textContent =
      scores[activePlayer];

    // 2. Check if player's score is >= 100;
    if (scores[activePlayer] >= 100) {
      // Finish the game
      playing = false;
      diceEl.classList.add("hidden");

      document
        .querySelector(`.player--${activePlayer}`)
        .classList.add("player--winner");
      document
        .querySelector(`.player--${activePlayer}`)
        .classList.remove("player--active");
      alert(`猪猪${activePlayer + 1}获胜，获得大肥猪猪称号！`);
    } else {
      // Switch to the next Player
      switchPlayer();
    }
  }
});
btnNew.addEventListener("click", init);
```