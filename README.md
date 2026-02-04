<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width,initial-scale=1.0">
  <title>Will You Be My Valentine?</title>
  <style>
    body { /* styling unchanged */ }
    .hide { display: none; }
    .emoji-row { font-size: 2.5rem; animation: pulse 1.8s infinite; text-align: center; margin-bottom: 10px;}
    @keyframes pulse {0%{transform:scale(1);}50%{transform:scale(1.1);}100%{transform:scale(1);}}
    .question { font-size: 1.5rem; color: #cc1656; margin-bottom: 28px;}
    .buttons { display: flex; gap: 30px; justify-content: center; margin-bottom: 42px;}
    .btn { padding:16px 42px; font-size:1.2rem; border-radius:40px; border:none; background:#e8505b; color:#fff; box-shadow:0 7px 20px -4px #e8505b44; transition:all .2s; position:relative; z-index:1;}
    .btn:active{background:#b51b44;}
    .btn.no {background: #fff; color:#e8505b; border:2px solid #e8505b;}
    .response {font-size:1.3rem; color:#cc1656; font-weight:bold; text-align:center; margin-top:24px;}
    .results-page {position:fixed; inset:0; z-index:100; background:linear-gradient(125deg,#fbb1b1 10%,#ffebee 90%); display:flex; flex-direction:column; align-items:center; justify-content:center; animation:fadeIn 1s; text-align:center;}
    @keyframes fadeIn{from{opacity:0;}to{opacity:1;}}
    .results-heart-bg {font-size:4rem; color:#ef476f77; filter:blur(0.5px); position:absolute; left:2vw; right:2vw; top:4vw; bottom:4vw; pointer-events:none; user-select:none;}
    .results-photo {width:120px; height:120px; border-radius:50%; object-fit:cover; border:5px solid #fff; box-shadow:0 0 32px #bf1555bb; margin-bottom:15px;}
    .declaration {font-size:1.4rem; padding:1rem 10vw 0rem 10vw; color:#ae185a; font-weight:500; margin-bottom:3vh;}
    @media (max-width: 500px) {
      .btn, .buttons {font-size:1.05rem;}
      .question {font-size:1.1rem;}
      .results-photo {width:90px; height:90px;}
      .declaration {font-size:1.08rem;}
    }
  </style>
</head>
<body>
  <audio id="valentineAudio" src="love.mp3"></audio>
  <div class="emoji-row">💕 🥰 💌 ❤️ 😍 💝 💞</div>
  <div class="question">Will you be my Valentine, Babe (Gudakumari)?</div>
  <div class="buttons">
    <button class="btn yes">Yes</button>
    <button class="btn no">No</button>
  </div>
  <div class="response"></div>
  <!-- Page 2: Hidden initially -->
  <div class="results-page hide">
    <div class="results-heart-bg">💖 💞 💓 💕 💖 💝 💖 💘 💗 💝 💖 💞 💕 💓 💟 💌 ❤️</div>
    <img class="results-photo" src="mypic.jpg" alt="Our couple photo" />
    <div class="declaration">
      Hey Gudakumari,<br><br>
      You are truly the best thing that ever happened to me.<br>
      Every day with you feels like a fairytale.<br><br>
      Thank you for being my sunshine, my partner, and my cutest everything.<br>
      Happy Valentine’s Day, my love! ❤️<br>
      <b>I just knew you'd say YES!<br>
      I love you more than all the emojis in the world! 💖😊</b>
    </div>
  </div>
  <script>
    const noBtn = document.querySelector('.btn.no');
    const yesBtn = document.querySelector('.btn.yes');
    const responseDiv = document.querySelector('.response');
    const questionDiv = document.querySelector('.question');
    const page2 = document.querySelector('.results-page');
    let clicks = 0;

    // Move "No" button on touch/click
    function moveNoButton(event) {
      let parent = noBtn.parentElement;
      let parentRect = parent.getBoundingClientRect();
      let maxX = parentRect.width - noBtn.offsetWidth;
      let maxY = parentRect.height - noBtn.offsetHeight;
      let x = Math.random() * maxX;
      let y = Math.random() * maxY;
      noBtn.style.position = 'absolute';
      noBtn.style.left = x + "px";
      noBtn.style.top = y + "px";
      clicks++;
      if(clicks>3){
        noBtn.animate([{transform:'rotate(-8deg)'},{transform:'rotate(6deg)'},{transform:'rotate(-5deg)'},{transform:'rotate(0deg)'}], {duration:200});
      }
    }
    noBtn.addEventListener('touchstart', moveNoButton);
    noBtn.addEventListener('mouseenter', moveNoButton);
    noBtn.addEventListener('mousedown', moveNoButton);

    // Yes button handler (shows page 2 and plays audio instantly, no delay)
    yesBtn.addEventListener('click', function(){
      responseDiv.textContent = "I knew you'd say YES! 🥰💖";
      // REMOVE DELAY: Instantly show page 2
      document.querySelector('.emoji-row').classList.add('hide');
      questionDiv.classList.add('hide');
      document.querySelector('.buttons').classList.add('hide');
      responseDiv.classList.add('hide');
      page2.classList.remove('hide');
      // Play audio
      document.getElementById('valentineAudio').play();
    });

    // Prevent scrolling (optional)
    document.body.addEventListener('touchmove', function (e) {
      if (!page2.classList.contains('hide')) e.preventDefault();
    }, {passive:false});
  </script>
</body>
</html>
