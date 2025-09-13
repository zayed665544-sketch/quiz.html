<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8">
  <title>اختبار أحكام المد</title>
  <style>
    body {
      font-family: "Tahoma", sans-serif;
      background: #f7f9fc;
      margin: 0;
      padding: 0;
      text-align: center;
    }
    .container {
      max-width: 750px;
      margin: auto;
      background: #fff;
      padding: 20px;
      margin-top: 40px;
      border-radius: 20px;
      box-shadow: 0 6px 15px rgba(0,0,0,0.1);
    }
    h1 {
      color: #0077b6;
    }
    .question {
      font-size: 20px;
      margin: 20px 0;
      font-weight: bold;
    }
    .options button {
      display: block;
      margin: 10px auto;
      padding: 12px;
      width: 85%;
      font-size: 18px;
      border: none;
      border-radius: 10px;
      background: #e9ecef;
      cursor: pointer;
      transition: 0.3s;
    }
    .options button:hover {
      background: #d0ebff;
    }
    .result {
      font-size: 22px;
      margin-top: 20px;
      color: #333;
    }
    .reward {
      margin-top: 20px;
      font-size: 20px;
      font-weight: bold;
      color: #007f5f;
    }
  </style>
</head>
<body>

<div class="container">
  <h1>اختبار أحكام المد</h1>
  <div id="quiz">
    <div id="question" class="question"></div>
    <div id="options" class="options"></div>
  </div>
  <div id="result" class="result"></div>
  <div id="reward" class="reward"></div>
</div>

<script>
const questions = [
  {question:"ما هو المد الطبيعي؟",options:["هو الذي لا تقوم ذات الحرف إلا به","هو مد زائد عن الطبيعي","هو مد لازم","هو مد عارض للسكون"],answer:0},
  {question:"مقدار المد الطبيعي:",options:["حركتان","4 حركات","6 حركات","لا يمد"],answer:0},
  {question:"متى يسمى المد مدًّا واجبًا متصلاً؟",options:["إذا جاء الهمز بعد المد في نفس الكلمة","إذا جاء الهمز بعد المد في كلمة أخرى","إذا جاء السكون بعد المد","لا شيء مما سبق"],answer:0},
  {question:"مقدار المد الواجب المتصل:",options:["حركتان","3 حركات","4-5 حركات","6 حركات"],answer:3},
  {question:"المد الجائز المنفصل يكون إذا:",options:["جاء حرف المد آخر الكلمة والهمز أول الكلمة التالية","جاء السكون بعد المد","جاءت الشدة بعد المد","لا شيء مما سبق"],answer:0},
  {question:"مقدار المد الجائز المنفصل:",options:["حركتان","4 أو 5 حركات","6 حركات","اختياري بين 2 و 6"],answer:1},
  {question:"المد اللازم يكون إذا:",options:["جاء بعد حرف المد همزة","جاء بعد حرف المد سكون أصلي","جاء بعد المد سكون عارض","لا شيء مما سبق"],answer:1},
  {question:"مقدار المد اللازم:",options:["حركتان","4 حركات","6 حركات","لا يمد"],answer:2},
  {question:"المد العارض للسكون سببه:",options:["همزة","سكون أصلي","سكون عارض عند الوقف","لا شيء"],answer:2},
  {question:"مقدار المد العارض للسكون:",options:["2 أو 4 أو 6 حركات","حركتان فقط","6 حركات فقط","لا يمد"],answer:0},
  {question:"المد اللازم الكلمي المثقل مثال:",options:["الحآقّة","الطآمة","الضآلين","الكتاب"],answer:0},
  {question:"المد اللازم الحرفي يوجد في:",options:["بداية بعض السور","آخر الآيات","وسط الكلمات","كل القرآن"],answer:0},
  {question:"المد اللازم الكلمي المخفف مثال:",options:["ءآلآن","الحاقة","الطامة","الصاخة"],answer:0},
  {question:"المد الطبيعي يسمى:",options:["مد أصلي","مد عارض","مد لازم","مد فرعي"],answer:0},
  {question:"المد الواجب المتصل حكمه:",options:["واجب مده","يجوز قصره","لا يمد","مقداره حركتان"],answer:0},
  {question:"المد الجائز المنفصل حكمه:",options:["يجوز قصره أو مده","واجب مده","لا يمد","مقداره ثابت"],answer:0},
  {question:"مقدار مد البدل:",options:["حركتان","4 حركات","6 حركات","لا شيء"],answer:0},
  {question:"سبب تسمية مد البدل:",options:["لأن حرف المد أُبدل من همزة","لأنه بدل عن مد لازم","لأنه بدل عن مد طبيعي","لا شيء مما سبق"],answer:0},
  {question:"مد الصلة الكبرى يكون:",options:["إذا وقع بعد هاء الضمير همزة","إذا وقع بعد المد سكون","إذا وقع بعد حرف المد شدة","لا شيء"],answer:0},
  {question:"مقدار مد الصلة الكبرى:",options:["حركتان","4 أو 5 حركات","6 حركات","اختياري"],answer:1},
  {question:"مد الصلة الصغرى يمد:",options:["حركتان","4 حركات","6 حركات","لا يمد"],answer:0},
  {question:"مد العوض يكون عند:",options:["الوقف على تنوين نصب","الوقف على ساكن","الوصل بين كلمتين","لا شيء"],answer:0},
  {question:"مقدار مد العوض:",options:["حركتان","4 حركات","6 حركات","لا شيء"],answer:0},
  {question:"المد اللازم الحرفي المثقل مثال:",options:["الم","يس","ن والقلم","طه"],answer:0},
  {question:"المد الطبيعي الأصلي لا يتوقف على:",options:["همز أو سكون","حركة","حرف","شدة"],answer:0},
  {question:"مقدار حركة واحدة يساوي:",options:["زمن قبض أو بسط الإصبع","ثانيتين","جزء من الثانية","حركتين"],answer:0},
  {question:"أقوى أنواع المد:",options:["المد اللازم","المد العارض","المد الطبيعي","مد العوض"],answer:0},
  {question:"أضعف أنواع المد:",options:["المد الطبيعي","المد الواجب","المد اللازم","المد العارض"],answer:0},
  {question:"مد الفرق يوجد في:",options:["ءآلآن","ءآلذكرين","ءآللَّه","لا شيء"],answer:2},
  {question:"مقدار مد الفرق:",options:["6 حركات","4 حركات","2 حركتين","اختياري"],answer:0},
  {question:"المد اللازم الحرفي المخفف مثال:",options:["حم","ق","ن","ص"],answer:1},
  {question:"مد التمكين يوجد عند:",options:["اجتماع ياءين","اجتماع واوين","اجتماع همزتين","لا شيء"],answer:0},
  {question:"مقدار مد التمكين:",options:["حركتان","4 حركات","6 حركات","لا شيء"],answer:0},
  {question:"المد الطبيعي سبب تسميته:",options:["لطبيعته بدون سبب","لأنه فرعي","لأنه واجب","لا شيء"],answer:0},
  {question:"المد الواجب المتصل يسمى:",options:["واجب متصل","طبيعي","لازم","بدل"],answer:0},
  {question:"من أمثلة المد الجائز المنفصل:",options:["في أنفسكم","الضآلين","ءآلآن","طه"],answer:0},
  {question:"مد البدل مثال:",options:["ءآمنوا","أولئك","إيمانا","كلا"],answer:0},
  {question:"مد العوض مثال:",options:["عليماً","كتاباً","كبيراً","كلها صحيحة"],answer:3},
  {question:"المد اللازم الحرفي يوجد في أوائل:",options:["السور","الكلمات","الآيات","الجمل"],answer:0},
  {question:"المد العارض للسكون يكون عند:",options:["الوقف","الوصل","كلاهما","لا شيء"],answer:0},
  {question:"المد الطبيعي يمد:",options:["حركتين","4 حركات","6 حركات","اختياري"],answer:0},
  {question:"مد الصلة الكبرى مثال:",options:["إنهُ أولى","بهمُ أولئك","لهُ أجر","لا شيء"],answer:1},
  {question:"مد الصلة الصغرى مثال:",options:["إنهُ كان","بهِ بصير","لهُ حكيم","كلها صحيحة"],answer:3},
  {question:"مد البدل سببه:",options:["همز مبدل","سكون","شدة","لا شيء"],answer:0},
  {question:"المد اللازم الكلمي المثقل يكون عند:",options:["وجود شدة بعد المد","وجود همزة","وجود سكون عارض","لا شيء"],answer:0},
  {question:"أقل مقدار للمد العارض للسكون:",options:["حركتان","4 حركات","6 حركات","لا شيء"],answer:0},
  {question:"أعلى مقدار للمد العارض للسكون:",options:["6 حركات","4 حركات","2 حركتين","لا شيء"],answer:0},
  {question:"مد التمكين سببه:",options:["اجتماع ياءين أولاهما ساكنة والثانية متحركة","اجتماع همزتين","اجتماع واوين","لا شيء"],answer:0},
  {question:"المد اللازم الحرفي المثقل يكون في:",options:["الم","الر","يس","كلها صحيحة"],answer:3},
  {question:"عدد حركات المد الطبيعي:",options:["2","4","6","8"],answer:0}
];

let currentQuestion = 0;
let score = 0;

function showQuestion() {
  document.getElementById("result").innerText = "";
  const q = questions[currentQuestion];
  document.getElementById("question").innerText = `س${currentQuestion+1}: ${q.question}`;
  const optionsDiv = document.getElementById("options");
  optionsDiv.innerHTML = "";
  q.options.forEach((opt, i) => {
    const btn = document.createElement("button");
    btn.innerText = opt;
    btn.onclick = () => checkAnswer(i);
    optionsDiv.appendChild(btn);
  });
}

function checkAnswer(selected) {
  const q = questions[currentQuestion];
  if (selected === q.answer) {
    score++;
  }
  currentQuestion++;
  if (currentQuestion < questions.length) {
    showQuestion();
  } else {
    endQuiz();
  }
}

function endQuiz() {
  document.getElementById("quiz").innerHTML = "";
  document.getElementById("result").innerText = `🎯 انتهى الاختبار! نتيجتك: ${score} من ${questions.length}`;
  
  let reward = "";
  if (score === 50) {
    reward = "🏆 ميدالية ذهبية! أحسنت جدًا!";
  } else if (score >= 40) {
    reward = "🥈 ميدالية فضية! ممتاز!";
  } else if (score >= 25) {
    reward = "🥉 ميدالية برونزية! جيد جدًا!";
  } else {
    reward = "🎁 حاول مرة أخرى، وستفوز بجائزة عند التحسن!";
  }
  document.getElementById("reward").innerText = reward;
}

showQuestion();
</script>

</body>
</html>
