<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Love Quiz</title>
<style>
body{
  margin:0;
  min-height:100vh;
  display:flex;
  align-items:center;
  justify-content:center;
  font-family: system-ui, sans-serif;
  background: radial-gradient(circle at top, #1b1b2a, #0b0b12);
  color:#fff;
}
.card{
  width:min(800px,95vw);
  background:rgba(255,255,255,0.08);
  border:1px solid rgba(255,255,255,0.14);
  border-radius:18px;
  padding:22px;
  backdrop-filter:blur(10px);
  text-align:center;
}
.progress{height:10px;background:rgba(255,255,255,0.15);border-radius:999px;margin-bottom:15px;overflow:hidden;}
.bar{height:100%;width:0;background:#ff69b4;transition:width .3s;}
.question{font-size:20px;margin-bottom:10px;}
.row{display:flex;gap:10px;justify-content:center;}
input{
  width:60%;
  padding:12px;
  border-radius:12px;
  border:1px solid rgba(255,255,255,0.2);
  background:rgba(255,255,255,0.08);
  color:#fff;
  text-align:center;
}
button{
  padding:12px 16px;
  border-radius:12px;
  border:none;
  font-weight:bold;
  cursor:pointer;
}
.primary{background:#ff69b4;color:#111;}
.feedback{margin-top:10px;font-weight:bold;color:#ff69b4;}
.hidden{display:none;}
.plan{margin-top:15px;background:rgba(255,255,255,0.07);padding:14px;border-radius:12px;}
</style>
</head>
<body>
<div class="card">
  <div class="progress"><div class="bar" id="bar"></div></div>

  <div id="quiz">
    <div class="question" id="questionText"></div>
    <div class="row">
      <input id="answerInput" placeholder="Type answer..." />
      <button class="primary" id="nextBtn">➜</button>
    </div>
    <div class="feedback" id="feedback"></div>
  </div>

  <div id="result" class="hidden">
    <h2>Weekend Vibes 💕</h2>
    <div class="plan">
      Celebrate love, make memories, and enjoy every moment together ✨<br><br>
      Saturday: Fun & laughter<br>
      Sunday: Chill & cuddles 💖
    </div>
  </div>
</div>

<script>
const questions = [
  { q: "What is your favorite color now?", a: "pink" },
  { q: "Is seafood your favorite food?", a: "seafood" },
  { q: "whats one of the spots we are going in july?", a: "jamaica" },
  { q: "Are you ready for valentines?", a: "any" }
];

let index = 0;
const bar = document.getElementById("bar");
const questionText = document.getElementById("questionText");
const input = document.getElementById("answerInput");
const nextBtn = document.getElementById("nextBtn");
const feedback = document.getElementById("feedback");
const result = document.getElementById("result");
const quiz = document.getElementById("quiz");

function updateBar(){
  bar.style.width = (index / questions.length * 100) + "%";
}

function showQuestion(){
  feedback.textContent = "";
  questionText.textContent = questions[index].q;
  input.value = "";
  input.focus();
  updateBar();
}

nextBtn.onclick = () => {
  const userAnswer = input.value.trim().toLowerCase();
  if(!userAnswer) return;

  const correctAnswer = questions[index].a;

  if(correctAnswer === "any" || userAnswer === correctAnswer){
    feedback.textContent = "CORRECT! 💖";
    setTimeout(() => {
      index++;
      if(index < questions.length){
        showQuestion();
      } else {
        bar.style.width = "100%";
        quiz.classList.add("hidden");
        result.classList.remove("hidden");
      }
    }, 800);
  } else {
    feedback.textContent = "Try again ❤️";
  }
};

showQuestion();
</script>
</body>
</html>
