<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="./css/style.css">
    <script defer src="./js/script.js" ></script>
    <title>mario jump</title>
</head>
<body>
    <div class="game-board"> 
     <audio id = "musicaDefundo" src="mario.mp3" autoplay loop ></audio>
     <img src="./imagens/sol.png" class="sol">
     <img src="./imagens/clouds.png" class="clouds">
     <img src="./imagens/mario.webp" class="mario ">
    <img src="./imagens/turbo.png" class="turbo">
    <div class="score">Pontuação: 0</div> <!-- Aqui está o contador -->


    </div>



</body>
</html> 
const mario = document.querySelector('.mario');
const turbo = document.querySelector('.turbo');
const scoreDisplay = document.querySelector('.score');

let score = 0;
let isGameOver = false;

// Incrementar pontuação a cada 100 ms   
const scoreInterval = setInterval(() => {
    if (!isGameOver) {
        score++;
        scoreDisplay.textContent = `Pontuação: ${score}`;  // Corrigido com crases
    }
}, 100);

const jump = () => {
    mario.classList.add('jump');
    setTimeout(() => {
        mario.classList.remove('jump');
    }, 500);
};

const loop = setInterval(() => {
    const turboPosition = turbo.offsetLeft;
    const marioPosition = +window.getComputedStyle(mario).bottom.replace('px', '');

    if (turboPosition <= 120 && turboPosition > 0 && marioPosition < 80) {
        turbo.style.animation = 'none';
        turbo.style.left = `${turboPosition}px`;  // Corrigido com crases

        mario.style.animation = 'none';
        mario.style.bottom = `${marioPosition}px`;  // Corrigido com crases

        mario.src = './imagens/gameover.png';
        mario.style.width = '75px';
        mario.style.marginLeft = '50px';

        isGameOver = true;
        clearInterval(loop);
        clearInterval(scoreInterval);

        alert(`Game Over! Sua pontuação foi: ${score}`);  // Corrigido com crases
    }
}, 10);

// Evento de pulo
document.addEventListener('keydown', jump);
 * { 
     margin: 0;
     padding: 0;
     box-sizing: border-box;
 }

 .game-board {
  width: 100%;
   height: 500px;
  border-bottom: 15px solid rgb(35, 160,35);
  margin: 0 auto;
  position: relative;
  overflow: hidden;
  background: linear-gradient(#87cee8, #e0f6ff);
 }

 .turbo {
  position: absolute;
  bottom: 0;
  width: 50px;
  animation: turbo-animation 1.5s infinite linear;
 }

 .mario { 
  width: 100px;
  position: absolute;
  bottom: 0;
  
 }
 .jump {
  animation: jump 500ms  ease-out;
 }

.clouds {
 position: absolute;
  width: 500px;
   animation: clouds-animation 20s infinite linear;
}
 .sol {
   position: absolute;
   width: 100px;
  animation: sol-animation infinite linear;
 }
 .score {
  position: absolute;
  top: 20px;
  left: 20px;
  font-size: 24px;
  font-weight: bold;
  color: #fff;
  text-shadow: 2px 2px 4px #000;
}
 @keyframes turbo-animation {
   from {
    right: -80px;
   }
   to {
    right: 100%;

   }


 }


 @keyframes jump {
  0% { 
    bottom: 0;
  }
  40% {
    bottom: 180px;
  }
  50% {
    bottom: 180px;
  }
  60% {
    bottom: 180px;
  }
  100% {
    bottom: 0;
  }

 }

 @keyframes clouds-animation {
    from {
      right: -500px;
    }
   
  to{
   right: 100%;

  }

 }

 @keyframes sol-animation {
   from {
    right: -100px;
   }

  to {

    right: 100%;
  }




 }
 
