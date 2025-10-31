# Eco-quiz
pansu
<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>생태와 환경 퀴즈</title>
  <style>
    body {
      font-family: 'Arial', sans-serif;
      background: linear-gradient(135deg, #a8e063, #56ab2f);
      margin: 0;
      padding: 0;
      color: #333;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
    }

    .quiz-container {
      background: #fff;
      border-radius: 12px;
      box-shadow: 0 4px 10px rgba(0,0,0,0.2);
      width: 90%;
      max-width: 500px;
      padding: 20px 30px;
      text-align: center;
      animation: fadeIn 0.8s ease;
    }

    @keyframes fadeIn {
      from {opacity: 0; transform: translateY(20px);}
      to {opacity: 1; transform: translateY(0);}
    }

    h1 {
      color: #2e7d32;
    }

    .question {
      font-size: 1.2em;
      margin-bottom: 15px;
    }

    .answers button {
      display: block;
      width: 100%;
      margin: 8px 0;
      padding: 10px;
      background-color: #c8e6c9;
      border: none;
      border-radius: 8px;
      cursor: pointer;
      transition: background-color 0.3s;
      font-size: 1em;
    }

    .answers button:hover {
      background-color: #81c784;
    }

    .next-btn {
      margin-top: 15px;
      padding: 10px 20px;
      background-color: #388e3c;
      color: #fff;
      border: none;
      border-radius: 8px;
      cursor: pointer;
      display: none;
    }

    .next-btn:hover {
      background-color: #2e7d32;
    }

    .result {
      font-size: 1.3em;
      color: #1b5e20;
      margin-top: 20px;
    }
  </style>
</head>
<body>
  <div class="quiz-container">
    <h1>🌿 생태와 환경 퀴즈 🌎</h1>
    <div class="question"></div>
    <div class="answers"></div>
    <button class="next-btn">다음 문제 ▶</button>
    <div class="result"></div>
  </div>

  <script>
    const quizData = [
      { q: "지구 온난화의 주된 원인은 무엇일까요?", a: ["산성비", "이산화탄소 증가", "오존층 복원", "태양 흑점"], correct: 1 },
      { q: "플라스틱 대신 사용할 수 있는 친환경 대체품은?", a: ["유리", "스티로폼", "비닐봉투", "PVC"], correct: 0 },
      { q: "생물 다양성이 중요한 이유는?", a: ["식량 안정", "생태계 균형", "의약품 개발", "모두 해당"], correct: 3 },
      { q: "탄소중립이란 무엇을 의미할까요?", a: ["이산화탄소를 완전히 제거하는 것", "배출과 흡수를 같게 하는 것", "탄소를 줄이지 않는 것", "탄소를 더 많이 배출하는 것"], correct: 1 },
      { q: "바다 오염의 주요 원인 중 하나는?", a: ["해류의 변화", "플라스틱 쓰레기", "기후 변화", "자연 침식"], correct: 1 },
      { q: "나무를 심는 것이 좋은 이유는?", a: ["공기를 맑게 함", "탄소 흡수", "생물 서식지 제공", "모두 해당"], correct: 3 },
      { q: "지구의 평균 기온 상승을 막기 위한 국제 협약은?", a: ["교토의정서", "파리협정", "몬트리올의정서", "리우협약"], correct: 1 },
      { q: "재활용 마크 ♻️ 가 붙은 제품은?", a: ["한 번만 사용하는 제품", "재활용 가능한 제품", "유해 폐기물", "유기농 식품"], correct: 1 },
      { q: "일회용품을 줄이는 가장 좋은 방법은?", a: ["더 자주 버리기", "재사용 용기 사용", "대량 구매", "분리수거 안 하기"], correct: 1 },
      { q: "기후 변화로 인한 현상은?", a: ["해수면 상승", "빙하 감소", "폭염 증가", "모두 해당"], correct: 3 }
    ];

    const questionEl = document.querySelector('.question');
    const answersEl = document.querySelector('.answers');
    const nextBtn = document.querySelector('.next-btn');
    const resultEl = document.querySelector('.result');

    let current = 0;
    let score = 0;

    function loadQuestion() {
      const q = quizData[current];
      questionEl.textContent = `${current + 1}. ${q.q}`;
      answersEl.innerHTML = '';
      q.a.forEach((ans, i) => {
        const btn = document.createElement('button');
        btn.textContent = ans;
        btn.addEventListener('click', () => checkAnswer(i));
        answersEl.appendChild(btn);
      });
      nextBtn.style.display = 'none';
      resultEl.textContent = '';
    }

    function checkAnswer(i) {
      const q = quizData[current];
      const buttons = answersEl.querySelectorAll('button');
      buttons.forEach((b, idx) => {
        if (idx === q.correct) b.style.backgroundColor = '#81c784';
        else b.style.backgroundColor = '#ef9a9a';
        b.disabled = true;
      });
      if (i === q.correct) score++;
      nextBtn.style.display = 'inline-block';
    }

    nextBtn.addEventListener('click', () => {
      current++;
      if (current < quizData.length) loadQuestion();
      else showResult();
    });

    function showResult() {
      questionEl.textContent = "퀴즈 완료!";
      answersEl.innerHTML = '';
      nextBtn.style.display = 'none';
      resultEl.innerHTML = `당신의 점수는 <strong>${score} / ${quizData.length}</strong> 입니다 🌱`;
    }

    loadQuestion();
  </script>
</body>
</html>
