
<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8">
  <title>С 8 МАРТОМ УСТИНА!</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    html, body {
      width: 100%;
      height: 100%;
      overflow: hidden;
      background: linear-gradient(135deg, #ff9a9e, #fad0c4);
      color: #fff;
      display: flex;
      justify-content: center;
      align-items: center;
      flex-direction: column;
      font-family: 'Marck Script', cursive, sans-serif;
      position: relative;
    }

    /* (1) Пульсирующее сердце (исчезает через 2.5 с) */
    .back {
      position: fixed;
      width: 100vw;
      height: 100vh;
      background: radial-gradient(circle, rgba(255,0,150,0.5) 20%, rgba(0,0,0,0) 80%);
      z-index: 9999;
      display: flex;
      justify-content: center;
      align-items: center;
      transition: opacity 1s ease;
      opacity: 1;
    }
    .heart {
      position: relative;
      width: 100px;
      height: 100px;
      background: red;
      transform: rotate(-45deg);
      animation: pulse 2s infinite ease-in-out;
    }
    .heart::before,
    .heart::after {
      content: "";
      position: absolute;
      width: 100px;
      height: 100px;
      background: red;
      border-radius: 50%;
    }
    .heart::before {
      top: -50px;
      left: 0;
    }
    .heart::after {
      top: 0;
      left: 50px;
    }
    @keyframes pulse {
      0%, 100% {
        transform: scale(1) rotate(-45deg);
      }
      50% {
        transform: scale(1.2) rotate(-45deg);
      }
    }

    /* (2) Контейнер с текстом: становится видимым после удаления .back */
    .container {
      position: relative;
      z-index: 2;
      text-align: center;
      opacity: 0;
      transition: opacity 2s ease;
    }
    body[data-loaded="true"] .container {
      opacity: 1;
    }

    /* Анимации для текста */
    @keyframes appearAndScale {
      0% {
        opacity: 0;
        transform: scale(0.5);
      }
      100% {
        opacity: 1;
        transform: scale(1);
      }
    }
    @keyframes subtleBounce {
      0%, 100% { transform: translateY(0); }
      50%      { transform: translateY(-5px); }
    }
    @keyframes gradientShift {
      0%   { background-position: 0% 50%; }
      50%  { background-position: 100% 50%; }
      100% { background-position: 0% 50%; }
    }

    /* (2a) Текст: «С 8 МАРТОМ УСТИНА!» */
    .title {
      /* УВЕЛИЧЕННЫЙ РАЗМЕР */
      font-size: 8em; 
      font-weight: bold;
      margin-top: 20px;
      background: linear-gradient(
        90deg,
        #ffffff,
        #b5e0ff,
        #ffffff,
        #b5e0ff
      );
      background-size: 400% 400%;
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;

      animation:
        appearAndScale 3s forwards,    /* плавное появление 3s */
        subtleBounce 3s infinite 3s,   /* покачивание с задержкой */
        gradientShift 6s ease infinite;/* переливающийся градиент */
      opacity: 0;
      display: inline-block;
    }

    /* Адаптация под мобильные устройства: 
       если экран шире 768px — оставляем 8em, 
       если уже — уменьшаем до 5em. */
    @media (max-width: 768px) {
      .title {
        font-size: 5em; /* Поменьше, чтобы влазило на экран телефона/планшета */
      }
    }

    /* (3) Солнце: появляется плавно через 4с */
    .sun {
      position: absolute;
      top: 10%;
      left: 50%;
      transform: translateX(-50%);
      width: 120px;
      height: 120px;
      background: radial-gradient(circle at center, #fff45c, #ffc500 80%);
      border-radius: 50%;
      box-shadow: 0 0 30px rgba(255,197,0,0.7);
      z-index: 1;
      opacity: 0;
      animation: sunFadeIn 2s forwards 4s;
    }
    @keyframes sunFadeIn {
      0%   { opacity: 0; transform: translateX(-50%) scale(0.5); }
      100% { opacity: 1; transform: translateX(-50%) scale(1); }
    }/* (4) Общее правило для облаков */
    .cloud {
      position: absolute;
      display: flex;
      align-items: center;
      justify-content: center;
      flex-wrap: nowrap;

      width: 200px;
      height: 120px;
      left: -25%;
      opacity: 0; /* спрятано до удаления .back */
    }
    body[data-loaded="true"] .cloud {
      opacity: 1;
    }

    /* Комки облака: радиальный градиент для псевдо-объёма */
    .cloud-lump {
      position: absolute;
      border-radius: 50%;
      background: radial-gradient(
        circle at 50% 35%,
        #ffffff 0%,
        #def1ff 40%,
        #b1daff 80%
      );
      box-shadow:
        0 0 10px rgba(177,218,255, 0.7),
        inset 0 0 15px rgba(177,218,255, 0.4);
    }
    .lump1 {
      width: 70px;  height: 70px;
      top: 20px;    left: 0px;
    }
    .lump2 {
      width: 90px;  height: 90px;
      top: 10px;    left: 40px;
    }
    .lump3 {
      width: 60px;  height: 60px;
      top: 30px;    left: 110px;
    }
    .lump4 {
      width: 60px;  height: 60px;
      top: 50px;    left: 20px;
    }
    .lump5 {
      width: 50px;  height: 50px;
      top: 60px;    left: 80px;
    }

    @keyframes moveCloud {
      0%   { left: -25%; }
      100% { left: 120%; }
    }

    /* Разные облака с разной скоростью/задержкой */
    .cloud1 {
      top: 20%;
      animation: moveCloud 20s linear infinite;
      animation-delay: 3s;
    }
    .cloud2 {
      top: 30%;
      animation: moveCloud 30s linear infinite;
      animation-delay: 5s;
    }
    .cloud3 {
      top: 40%;
      animation: moveCloud 25s linear infinite;
      animation-delay: 8s;
    }
    .cloud4 {
      top: 15%;
      animation: moveCloud 35s linear infinite;
      animation-delay: 2s;
    }
    .cloud5 {
      top: 50%;
      animation: moveCloud 28s linear infinite;
      animation-delay: 7s;
    }
    .cloud6 {
      top: 65%;
      animation: moveCloud 32s linear infinite;
      animation-delay: 10s;
    }

    /* (5) Искры */
    .sparkles {
      position: absolute;
      width: 100%;
      height: 100%;
      top: 0;
      left: 0;
      pointer-events: none;
    }
    .sparkle {
      position: absolute;
      width: 5px;
      height: 5px;
      background: white;
      border-radius: 50%;
      opacity: 0.8;
      animation: sparkleAnim 2s infinite ease-in-out;
    }
    @keyframes sparkleAnim {
      0%   { transform: translateY(0) scale(1);   opacity: 0.8; }
      50%  { transform: translateY(-20px) scale(1.5); opacity: 1; }
      100% { transform: translateY(-40px) scale(1);   opacity: 0; }
    }
  </style>
</head>
<body>
  <!-- (1) Сердце -->
  <div class="back">
    <div class="heart"></div>
  </div>

  <!-- (2) Текст -->
  <div class="container">
    <div class="title">С 8 МАРТОМ УСТИНА!</div>
  </div>

  <!-- (3) Солнце -->
  <div class="sun"></div>

  <!-- (4) Шесть облаков с разной скоростью и задержкой -->
  <div class="cloud cloud1">
    <div class="cloud-lump lump1"></div>
    <div class="cloud-lump lump2"></div>
    <div class="cloud-lump lump3"></div>
    <div class="cloud-lump lump4"></div>
    <div class="cloud-lump lump5"></div>
  </div>
  <div class="cloud cloud2">
    <div class="cloud-lump lump1"></div>
    <div class="cloud-lump lump2"></div>
    <div class="cloud-lump lump3"></div>
    <div class="cloud-lump lump4"></div>
    <div class="cloud-lump lump5"></div>
  </div>
  <div class="cloud cloud3">
    <div class="cloud-lump lump1"></div>
    <div class="cloud-lump lump2"></div>
    <div class="cloud-lump lump3"></div>
    <div class="cloud-lump lump4"></div>
    <div class="cloud-lump lump5"></div>
  </div>
  <div class="cloud cloud4">
    <div class="cloud-lump lump1"></div>
    <div class="cloud-lump lump2"></div>
    <div class="cloud-lump lump3"></div>
    <div class="cloud-lump lump4"></div><div class="cloud-lump lump5"></div>
</div>
<div class="cloud cloud5">
  <div class="cloud-lump lump1"></div>
  <div class="cloud-lump lump2"></div>
  <div class="cloud-lump lump3"></div>
  <div class="cloud-lump lump4"></div>
  <div class="cloud-lump lump5"></div>
</div>
<div class="cloud cloud6">
  <div class="cloud-lump lump1"></div>
  <div class="cloud-lump lump2"></div>
  <div class="cloud-lump lump3"></div>
  <div class="cloud-lump lump4"></div>
  <div class="cloud-lump lump5"></div>
</div>

<!-- (5) Искры -->
<div class="sparkles"></div>

<script>
  window.onload = function() {
    // Исчезновение сердечка .back
    const back = document.querySelector('.back');
    setTimeout(() => {
      back.style.opacity = '0';
      setTimeout(() => {
        back.remove();
        // Показываем остальное
        document.body.setAttribute('data-loaded', 'true');
      }, 1000);
    }, 2500);

    // Создаём искры
    const sparkleContainer = document.querySelector('.sparkles');
    for (let i = 0; i < 150; i++) {
      let sparkle = document.createElement('div');
      sparkle.classList.add('sparkle');
      sparkle.style.left = Math.random() * 100 + 'vw';
      sparkle.style.top = Math.random() * 100 + 'vh';
      sparkle.style.animationDelay = Math.random() * 2 + 's';
      sparkleContainer.appendChild(sparkle);
    }
  };
</script>
</body>
</html>
