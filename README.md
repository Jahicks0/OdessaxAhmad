
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
  width:min(860px,95vw);
  background:rgba(255,255,255,0.08);
  border:1px solid rgba(255,255,255,0.14);
  border-radius:18px;
  padding:22px;
  backdrop-filter:blur(10px);
  text-align:center;
}
.progress{
  height:10px;
  background:rgba(255,255,255,0.15);
  border-radius:999px;
  margin-bottom:15px;
  overflow:hidden;
}
.bar{
  height:100%;
  width:0;
  background:#ff69b4;
  transition:width .3s;
}
.question{font-size:20px;margin-bottom:10px;}
.row{
  display:flex;
  gap:10px;
  justify-content:center;
  align-items:center;
}
input{
  width:min(520px, 70%);
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
.feedback{
  margin-top:10px;
  font-weight:bold;
  color:#ff69b4;
  min-height:24px;
}
.hidden{display:none;}

.plan{
  margin-top:15px;
  background:rgba(255,255,255,0.07);
  padding:16px;
  border-radius:14px;
  border:1px solid rgba(255,255,255,0.12);
  text-align:left;
}
.plan h3{margin:0 0 8px;font-size:16px;}
.plan ul{
  margin:0 0 14px;
  padding-left:18px;
  line-height:1.5;
  color:rgba(255,255,255,0.9);
}
.tag{
  display:inline-block;
  margin:8px 0 14px;
  font-size:12px;
  border:1px solid rgba(255,255,255,0.18);
  padding:6px 10px;
  border-radius:999px;
  background:rgba(255,255,255,0.06);
}
.intro{
  margin:10px 0 16px;
  line-height:1.5;
  color:rgba(255,255,255,0.95);
}
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
    <h2>Weekend Plans 💕</h2>
    <div class="tag">Arundel Hotel • Dinner • Brunch • Paint + Movie</div>

    <div class="intro">
      Lets have a beautiful weekend, create special memories together as always,
      laugh but most importantly spend quality time with each other.
      I love you baby so here is a lil run down on how the weekend is about to go.
    </div>

    <div class="plan">
      <h3>Saturday</h3>
      <ul>
        <li>I reserved a room at <b>Arundel Hotel</b> for Saturday night.</li>
        <li>I will get you at <b>5:30 PM</b>.</li>
        <li><b>Dinner</b> is at <b>7:00 PM</b>.</li>
        <li>Arrive back at the hotel around <b>10:00 PM</b>.</li>
        <li>Card games, drinking, etc.</li>
        <li>Fun &amp; laughter 😄</li>
      </ul>

      <h3>Sunday</h3>
      <ul>
        <li><b>Brunch</b> at <b>12:00 PM</b>.</li>
        <li>Leave brunch back to my house.</li>
        <li>Paint a picture but switch off every <b>2 minutes</b> 🎨</li>
        <li>Watch a movie with snacks/popcorn 🍿</li>
      </ul>
    </div>
  </div>
</div>

<script>
const questions = [
  { q: "What is your favorite color now?", a: "pink" },
  { q: "Is seafood your favorite food?", a: "yes" }, // ✅ CHANGED HERE
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

  const correct = questions[index].a;
  if(correct === "any" || userAnswer === correct){
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

