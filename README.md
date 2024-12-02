<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>เกมลำดับและอนุกรม</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Sarabun:wght@400;600&display=swap');
        body {
            font-family: 'Sarabun', Arial, sans-serif;
            margin: 0;
            height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            background: linear-gradient(135deg, #89f7fe, #66a6ff);
        }
        .container {
            text-align: center;
            background: rgba(255, 255, 255, 0.8);
            padding: 20px;
            border-radius: 15px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
        }
        h1 {
            font-size: 48px;
            font-weight: 600;
            margin-bottom: 10px;
            background: linear-gradient(90deg, #FF7EB3, #FF758C, #FF65A3, #FF5680);
            -webkit-background-clip: text;
            color: transparent;
        }
        p {
            font-size: 20px;
        }
        .sequence {
            font-size: 36px;
            margin: 20px;
        }
        .input-box {
            margin: 10px;
            font-size: 20px;
            padding: 5px;
            width: 200px;
            border: 1px solid #ccc;
            border-radius: 5px;
        }
        button {
            font-size: 20px;
            padding: 10px 20px;
            border: none;
            border-radius: 5px;
            background: #4caf50;
            color: white;
            cursor: pointer;
            transition: background 0.3s;
        }
        button:hover {
            background: #45a049;
        }
        #result {
            font-size: 24px;
            margin: 20px;
        }
        #score {
            font-size: 20px;
            color: #333;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>เกมลำดับและอนุกรม</h1>
        <p>เติมตัวเลขที่หายไปลงในช่องว่างให้ถูกต้อง</p>
        <div class="sequence" id="sequence"></div>
        <input class="input-box" type="number" id="answer" placeholder="Enter your answer">
        <button onclick="checkAnswer()">Submit</button>
        <p id="result"></p>
        <p id="score">คะแนน: 0</p>
    </div>

    <script>
        const questions = [
            { sequence: "2, 4, ___, 8, 10", answer: 6 },
            { sequence: "1, 3, 5, ___, 9", answer: 7 },
            { sequence: "-2, -4, ___, -8, -10", answer: -6 },
            { sequence: "10, 20, ___, 40, 50", answer: 30 },
            { sequence: "1, 4, 9, ___, 25", answer: 16 },
            { sequence: "-1, -3, -5, ___, -9", answer: -7 },
            { sequence: "3, 6, 9, ___, 15", answer: 12 },
            { sequence: "-3, -6, ___, -12, -15", answer: -9 },
            { sequence: "2, 3, 5, ___, 12", answer: 8 },
            { sequence: "-2, -3, -5, ___, -12", answer: -8 },
            { sequence: "5, 10, 20, ___, 80", answer: 40 },
            { sequence: "-5, -10, -20, ___, -80", answer: -40 },
            { sequence: "8, 16, 24, ___, 40", answer: 32 },
            { sequence: "100, 90, ___, 70, 60", answer: 80 },
            { sequence: "-100, -90, ___, -70, -60", answer: -80 },
            { sequence: "50, 45, ___, 35, 30", answer: 40 },
            { sequence: "-50, -45, ___, -35, -30", answer: -40 },
            { sequence: "2,4,8,16,___,64", answer: 32 },
            { sequence: "-1,4,9,16,___,36", answer: 25 },
            { sequence: "100,90,81,73,___,58", answer: 66 },
            { sequence: "3,6,12,24,___,96", answer: 48 },
            { sequence: "81,27,9,3,___,1/3", answer: 1 },
            { sequence: "1,2,6,24,___,720", answer: 120 },
            { sequence: "2,4,7,11,___,22", answer: 16 },
            { sequence: "100,50,25,___,6.25,3.125", answer: 12.5 },
            { sequence: "1,4,7,10,___,16", answer: 13 },
            { sequence: "100,81,64,49,___,25", answer: 36 },
            { sequence: "3,6,11,18,___,38", answer: 27 },
            { sequence: "2,4,8,14,___,34", answer: 22 },
            { sequence: "5,10,20,40,___,160", answer: 80 )
        ];

        let currentQuestionIndex = null; // เริ่มต้นโดยไม่มีโจทย์
        let score = 0;

        function getRandomQuestion() {
            const randomIndex = Math.floor(Math.random() * questions.length);
            return questions[randomIndex];
        }

        function showQuestion() {
            const question = getRandomQuestion(); // ดึงคำถามแบบสุ่ม
            currentQuestionIndex = questions.indexOf(question); // บันทึกตำแหน่งคำถามที่ถูกสุ่ม
            document.getElementById("sequence").textContent = question.sequence;
            document.getElementById("answer").value = "";
            document.getElementById("result").textContent = "";
        }

        function checkAnswer() {
            const userAnswer = parseFloat(document.getElementById("answer").value);
            const correctAnswer = questions[currentQuestionIndex].answer;

            if (userAnswer === correctAnswer) {
                document.getElementById("result").textContent = "Correct! 🎉";
                document.getElementById("result").style.color = "green";
                score++;
                document.getElementById("score").textContent = `คะแนน: ${score}`;
                setTimeout(() => {
                    showQuestion(); // เปลี่ยนโจทย์หลังจาก 1 วินาที
                }, 1000);
            } else {
                document.getElementById("result").textContent = "ลองอีกครั้ง! ❌";
                document.getElementById("result").style.color = "red";
            }
        }

        showQuestion();

        document.getElementById("answer").addEventListener("keydown", function(event) {
            if (event.key === "Enter") {
                checkAnswer();
            }
        });
    </script>
</body>
</html>

