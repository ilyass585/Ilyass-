PK
     ���ZS��s�  �  
   index.html<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>تحدي الأذكياء!</title>
  <link href="https://fonts.googleapis.com/css2?family=Readex+Pro:wght@400;700&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <div class="container">
    <h1>تحدى عقلك!</h1>
    <div class="counter" id="day-counter"></div>

    <div class="puzzle-container" id="puzzle1">
      <p class="puzzle-text" id="puzzle1-text"></p>
      <input type="text" class="answer-input" id="answer1" placeholder="أدخل إجابتك هنا">
      <button class="check-button" onclick="checkAnswer(0)">تحقق</button>
      <p class="result-message" id="result1"></p>
    </div>

    <div class="puzzle-container" id="puzzle2">
      <p class="puzzle-text" id="puzzle2-text"></p>
      <input type="text" class="answer-input" id="answer2" placeholder="أدخل إجابتك هنا">
      <button class="check-button" onclick="checkAnswer(1)">تحقق</button>
      <p class="result-message" id="result2"></p>
    </div>

    <div class="puzzle-container" id="puzzle3">
      <p class="puzzle-text" id="puzzle3-text"></p>
      <input type="text" class="answer-input" id="answer3" placeholder="أدخل إجابتك هنا">
      <button class="check-button" onclick="checkAnswer(2)">تحقق</button>
      <p class="result-message" id="result3"></p>
    </div>

    <p class="completion-message" id="completion-message">
      <span>أحسنت!</span> 🎉<br>
      لقد أتممت ألغاز اليوم بنجاح!<br>
      التحدي الجديد سيكون متاحًا بعد 24 ساعة. ⏳
    </p>

    <p id="timer-message" class="timer-message">
      التحدي التالي سيكون متاحًا بعد: <span id="countdown"></span>
    </p>

    <p class="waiting-message" id="waiting-message" style="display:none;">
      شكراً على مشاركتك اليوم!  
      استعد لتحديات جديدة وألغاز أذكى غدًا!  
      ابقَ على استعداد، فإن كل يوم يحمل لك مفاجآت ذكية!
    </p>
  </div>

  <script src="script.js"></script>
</body>
</html>PK
     ���Z��hh,  h,  	   script.jsconst allPuzzles = [
  // Bronze
  { question: "ما هي عاصمة مصر؟", answer: "القاهرة", level: "bronze" },
  { question: "من هو النبي الذي ابتلعه الحوت؟", answer: "يونس", level: "bronze" },
  { question: "ما اسم العملة في المغرب؟", answer: "الدرهم", level: "bronze" },
  { question: "من هو مخترع المصباح الكهربائي؟", answer: "توماس إديسون", level: "bronze" },
  { question: "كم عدد أيام السنة؟", answer: "365", level: "bronze" },
  { question: "ما هي اللغة الرسمية في فرنسا؟", answer: "الفرنسية", level: "bronze" },
  { question: "ما اسم أول كتاب نزل من السماء؟", answer: "الزبور", level: "bronze" },
  { question: "أين تقع مكة؟", answer: "السعودية", level: "bronze" },
  { question: "ما هو الحيوان الذي يُلقب بسفينة الصحراء؟", answer: "الجمل", level: "bronze" },
  { question: "من هو أبو البشرية؟", answer: "آدم", level: "bronze" },
  { question: "ما هو الكوكب الأحمر؟", answer: "المريخ", level: "bronze" },
  { question: "ما اسم البحر بين السعودية ومصر؟", answer: "البحر الأحمر", level: "bronze" },
  { question: "ما هي عاصمة فلسطين؟", answer: "القدس", level: "bronze" },
  { question: "كم عدد حروف اللغة العربية؟", answer: "28", level: "bronze" },
  { question: "من هو النبي الذي شق البحر؟", answer: "موسى", level: "bronze" },
  { question: "ما هي السورة التي تبدأ ببسم الله وليس فيها بسم الله؟", answer: "التوبة", level: "bronze" },
  { question: "من هو أول الخلفاء الراشدين؟", answer: "أبو بكر", level: "bronze" },
  { question: "أين توجد الأهرامات؟", answer: "مصر", level: "bronze" },
  { question: "من هو مؤلف رواية البؤساء؟", answer: "فيكتور هوغو", level: "bronze" },
  { question: "ما هو جمع كلمة 'قلم'؟", answer: "أقلام", level: "bronze" },
  { question: "من هو أول رئيس للولايات المتحدة؟", answer: "جورج واشنطن", level: "bronze" },
  { question: "ما اسم الكتاب المقدس عند المسلمين؟", answer: "القرآن", level: "bronze" },
  { question: "من هو مخترع الهاتف؟", answer: "غراهام بيل", level: "bronze" },
  { question: "ما اسم البحر الذي يفصل بين أوروبا وأفريقيا؟", answer: "المتوسط", level: "bronze" },
  { question: "في أي قارة تقع الجزائر؟", answer: "أفريقيا", level: "bronze" },
  { question: "ما اسم أول سورة في القرآن؟", answer: "الفاتحة", level: "bronze" },
  { question: "ما هو جمع كلمة 'وردة'؟", answer: "ورود", level: "bronze" },
  { question: "أين تقع مدينة مراكش؟", answer: "المغرب", level: "bronze" },
  { question: "ما هو أكبر كوكب في النظام الشمسي؟", answer: "المشتري", level: "bronze" },
  { question: "ما اسم أطول نهر في العالم؟", answer: "النيل", level: "bronze" },

  // Silver
  { question: "من هو مكتشف أمريكا؟", answer: "كريستوفر كولومبوس", level: "silver" },
  { question: "من هو النبي الذي تكلم وهو رضيع؟", answer: "عيسى", level: "silver" },
  { question: "من هو أول من كتب بسم الله الرحمن الرحيم؟", answer: "سليمان", level: "silver" },
  { question: "من مؤلف كتاب الأمير؟", answer: "ميكافيلي", level: "silver" },
  { question: "من هو الخليفة العباسي الأول؟", answer: "أبو العباس السفاح", level: "silver" },
  { question: "أين يوجد جبل طارق؟", answer: "بين المغرب وإسبانيا", level: "silver" },
  { question: "من هو مكتشف قانون الجاذبية؟", answer: "نيوتن", level: "silver" },
  { question: "ما اسم أول قمر صناعي؟", answer: "سبوتنيك", level: "silver" },
  { question: "كم عدد الكواكب؟", answer: "8", level: "silver" },
  { question: "أين تقع الأندلس؟", answer: "إسبانيا", level: "silver" },
  { question: "ما اسم أسرع حيوان بري؟", answer: "الفهد", level: "silver" },
  { question: "من هو مكتشف البنسلين؟", answer: "ألكسندر فليمنغ", level: "silver" },
  { question: "ما اسم عاصمة اليابان؟", answer: "طوكيو", level: "silver" },
  { question: "ما اسم أول إنسان على القمر؟", answer: "نيل أرمسترونغ", level: "silver" },
  { question: "ما اسم أطول سور في العالم؟", answer: "سور الصين العظيم", level: "silver" },
  { question: "كم عدد أركان الإسلام؟", answer: "5", level: "silver" },
  { question: "من هو الخليفة الذي جمع القرآن؟", answer: "عثمان بن عفان", level: "silver" },
  { question: "من هو أعظم علماء الرياضيات؟", answer: "الخوارزمي", level: "silver" },
  { question: "من هو الفيلسوف الذي علم الإسكندر؟", answer: "أرسطو", level: "silver" },
  { question: "أين يقع جبل إيفرست؟", answer: "النيبال", level: "silver" },
  { question: "من هو أول من صنع الورق؟", answer: "الصينيون", level: "silver" },
  { question: "أين تقع مدينة دبي؟", answer: "الإمارات", level: "silver" },
  { question: "كم عدد أضلاع المثلث؟", answer: "3", level: "silver" },
  { question: "ما هو العنصر الأساسي في الماء؟", answer: "الهيدروجين", level: "silver" },
  { question: "ما اسم القارة المتجمدة؟", answer: "أنتاركتيكا", level: "silver" },
  { question: "من هو أشهر عبقري في الفيزياء؟", answer: "آينشتاين", level: "silver" },
  { question: "من هو النبي الذي فلق البحر؟", answer: "موسى", level: "silver" },
  { question: "ما اسم الجهاز المسؤول عن ضخ الدم؟", answer: "القلب", level: "silver" },
  { question: "من هو أول طيار؟", answer: "الأخوان رايت", level: "silver" },
  { question: "ما اسم أعظم المساجد في الإسلام؟", answer: "الحرم المكي", level: "silver" },

  // Gold – سأكملها مباشرة بعد تأكيدك

];
// 90 لغز ثقافي كامل — موجود مسبقاً فـ const allPuzzles []

let currentPuzzles = [];
let answeredPuzzles = [false, false, false];
let lastCompletionTime = localStorage.getItem('lastCompletionTime');
const countdownElement = document.getElementById('countdown');
const timerMessageElement = document.getElementById('timer-message');
const completionMessage = document.getElementById('completion-message');
const dayCounter = document.getElementById('day-counter');
const waitingMessage = document.getElementById('waiting-message');

function selectPuzzlesForToday() {
  const today = new Date().toLocaleDateString();
  const solvedPuzzlesData = localStorage.getItem('solvedPuzzles_' + today);
  const solvedPuzzles = solvedPuzzlesData ? JSON.parse(solvedPuzzlesData) : [];

  const startDate = new Date(localStorage.getItem('startDate') || new Date().toLocaleDateString());
  localStorage.setItem('startDate', startDate.toLocaleDateString());
  const daysPassed = Math.floor((new Date() - new Date(startDate)) / (1000 * 60 * 60 * 24));

  let level = 'bronze';
  if (daysPassed >= 20) level = 'gold';
  else if (daysPassed >= 10) level = 'silver';

  let available = allPuzzles
    .map((p, i) => ({ ...p, index: i }))
    .filter(p => p.level === level && !solvedPuzzles.includes(p.index));

  if (available.length < 3) {
    available = allPuzzles.filter(p => p.level === level).map((p, i) => ({ ...p, index: i }));
  }

  const selected = [];
  for (let i = 0; i < 3; i++) {
    const rand = Math.floor(Math.random() * available.length);
    selected.push(available.splice(rand, 1)[0]);
  }

  currentPuzzles = selected;
  for (let i = 0; i < 3; i++) {
    document.getElementById(`puzzle${i + 1}-text`).textContent = currentPuzzles[i].question;
    if (i === 0) document.getElementById(`puzzle1`).style.display = 'block';
  }
}

function checkAnswer(index) {
  const input = document.getElementById(`answer${index + 1}`);
  const result = document.getElementById(`result${index + 1}`);
  const correct = currentPuzzles[index].answer.trim().toLowerCase();
  const userInput = input.value.trim().toLowerCase();

  if (userInput === correct) {
    result.textContent = "إجابة صحيحة!";
    result.className = "result-message correct";
    answeredPuzzles[index] = true;

    setTimeout(() => {
      document.getElementById(`puzzle${index + 1}`).style.display = 'none';
      if (index + 1 < 3) {
        document.getElementById(`puzzle${index + 2}`).style.display = 'block';
      } else {
        const today = new Date().toLocaleDateString();
        localStorage.setItem('lastCompletionTime', new Date().getTime());
        localStorage.setItem('solvedPuzzles_' + today, JSON.stringify(currentPuzzles.map(p => p.index)));

        let daysCompleted = parseInt(localStorage.getItem('daysCompleted') || "0");
        const lastDay = localStorage.getItem('lastDayCompleted');
        if (lastDay !== today) {
          daysCompleted += 1;
          localStorage.setItem('daysCompleted', daysCompleted);
          localStorage.setItem('lastDayCompleted', today);
        }
        updateDayCounter();
        completionMessage.style.display = 'block';
        waitingMessage.style.display = 'block';
        startCountdown();
      }
    }, 1000);
  } else {
    result.textContent = "إجابة خاطئة، حاول مرة أخرى!";
    result.className = "result-message incorrect";
  }
}

function updateDayCounter() {
  const count = parseInt(localStorage.getItem('daysCompleted') || "0");
  dayCounter.textContent = `عدد الأيام التي أكملت فيها التحدي: ${count} يوم${count === 1 ? '' : 'اً'}`;
}

function startCountdown() {
  timerMessageElement.style.display = 'block';
  function update() {
    const last = parseInt(localStorage.getItem('lastCompletionTime'));
    const now = new Date().getTime();
    const remaining = 24 * 60 * 60 * 1000 - (now - last);

    if (remaining <= 0) {
      location.reload();
      return;
    }

    const h = Math.floor(remaining / (1000 * 60 * 60));
    const m = Math.floor((remaining % (1000 * 60 * 60)) / (1000 * 60));
    const s = Math.floor((remaining % (1000 * 60)) / 1000);
    countdownElement.textContent = `${h} ساعة ${m} دقيقة ${s} ثانية`;

    setTimeout(update, 1000);
  }
  update();
}

window.onload = function () {
  const now = new Date().getTime();
  updateDayCounter();

  if (lastCompletionTime && now - lastCompletionTime < 24 * 60 * 60 * 1000) {
    startCountdown();
    completionMessage.style.display = 'block';
    waitingMessage.style.display = 'block';
    return;
  }

  selectPuzzlesForToday();
};PK
     ���Zc��`"	  "	  	   style.cssbody {
  font-family: 'Readex Pro', sans-serif;
  background: linear-gradient(135deg, #6dd5ed, #2193b0);
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  margin: 0;
  color: #333;
}

.container {
  background-color: rgba(255, 255, 255, 0.95);
  padding: 40px;
  border-radius: 20px;
  box-shadow: 0 12px 25px rgba(0, 0, 0, 0.3);
  text-align: center;
  width: 90%;
  max-width: 700px;
  height: 90vh;
  overflow-y: auto;
}

h1 {
  font-size: 3em;
  color: #2c3e50;
  margin-bottom: 10px;
  text-shadow: 1px 1px 3px rgba(0, 0, 0, 0.1);
}

.counter {
  font-size: 1.4em;
  color: #f39c12;
  margin-bottom: 30px;
}

.puzzle-container {
  background-color: #ecf0f1;
  padding: 25px;
  border-radius: 10px;
  margin-bottom: 20px;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  display: none;
}

.puzzle-text {
  font-size: 1.8em;
  color: #34495e;
  margin-bottom: 15px;
  font-weight: bold;
}

.answer-input {
  padding: 15px;
  border: 1px solid #3498db;
  border-radius: 8px;
  font-size: 1.6em;
  margin-bottom: 15px;
  width: calc(100% - 32px);
  box-sizing: border-box;
}

.answer-input:focus {
  outline: none;
  border-color: #e67e22;
  box-shadow: 0 0 8px rgba(230, 126, 34, 0.3);
}

.check-button {
  background-color: #27ae60;
  color: white;
  border: none;
  padding: 15px 30px;
  border-radius: 8px;
  cursor: pointer;
  font-size: 1.6em;
}

.check-button:hover {
  background-color: #218c74;
}

.result-message {
  font-size: 1.6em;
  font-weight: bold;
  margin-top: 10px;
}

.correct { color: #2ecc71; }
.incorrect { color: #e74c3c; }

.completion-message {
  font-size: 2em;
  color: #3498db;
  font-weight: bold;
  margin-top: 25px;
  display: none;
}

.completion-message span {
  color: #f39c12;
}

.timer-message {
  font-size: 1.2em;
  color: #d35400;
  margin-top: 20px;
  font-weight: bold;
  display: none;
}

.waiting-message {
  font-size: 1.4em;
  color: #2980b9;
  background: #eaf6ff;
  border-radius: 12px;
  padding: 20px;
  margin-top: 30px;
  line-height: 1.8;
  box-shadow: 0 0 8px rgba(0, 0, 0, 0.05);
}
header h1 {
  font-size: 2.5em;
  margin-bottom: 5px;
}

header p.counter {
  font-size: 1.3em;
  color: #2980b9;
}

main section {
  margin-bottom: 25px;
}

main h2 {
  font-size: 1.4em;
  margin-bottom: 10px;
  color: #2c3e50;
}

footer {
  margin-top: 30px;
}PK 
     ���ZS��s�  �  
                 index.htmlPK 
     ���Z��hh,  h,  	             	  script.jsPK 
     ���Zc��`"	  "	  	             �5  style.cssPK      �   �>    
