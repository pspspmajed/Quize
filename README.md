<!DOCTYPE html>
<html>
<head>
    <title>Quiz</title>
    <style>
        body {
            font-family: Arial, sans-serif;
        }
        .quiz-container {
            width: 50%;
            margin: auto;
            padding: 20px;
            border: 1px solid #ddd;
            border-radius: 5px;
            background-color: #f9f9f9;
        }
        .question {
            margin-bottom: 20px;
        }
        .options label {
            display: block;
            margin-bottom: 10px;
        }
        .result {
            margin-top: 20px;
            font-size: 1.2em;
        }
    </style>
</head>
<body>
    <div class="quiz-container">
        <h1>Quiz</h1>
        <div id="quiz"></div>
        <button onclick="submitQuiz()">Submit</button>
        <div id="result" class="result"></div>
    </div>

    <script>
        const quizData = [
            {
                question: "What is the capital of France?",
                options: [
                    { text: "Berlin", correct: false },
                    { text: "Madrid", correct: false },
                    { text: "Paris", correct: true },
                    { text: "Rome", correct: false }
                ]
            },
            {
                question: "Which planet is known as the Red Planet?",
                options: [
                    { text: "Earth", correct: false },
                    { text: "Mars", correct: true },
                    { text: "Jupiter", correct: false },
                    { text: "Saturn", correct: false }
                ]
            },
            {
                question: "What is the largest ocean on Earth?",
                options: [
                    { text: "Atlantic Ocean", correct: false },
                    { text: "Indian Ocean", correct: false },
                    { text: "Arctic Ocean", correct: false },
                    { text: "Pacific Ocean", correct: true }
                ]
            }
        ];

        const quizContainer = document.getElementById('quiz');

        function loadQuiz() {
            quizData.forEach((item, index) => {
                const questionDiv = document.createElement('div');
                questionDiv.className = 'question';
                questionDiv.innerHTML = `<p>${item.question}</p>`;
                
                const optionsDiv = document.createElement('div');
                optionsDiv.className = 'options';
                
                item.options.forEach((option, optIndex) => {
                    const optionLabel = document.createElement('label');
                    optionLabel.innerHTML = `
                        <input type="radio" name="question${index}" value="${optIndex}">
                        ${option.text}
                    `;
                    optionsDiv.appendChild(optionLabel);
                });

                questionDiv.appendChild(optionsDiv);
                quizContainer.appendChild(questionDiv);
            });
        }

        function submitQuiz() {
            let score = 0;

            quizData.forEach((item, index) => {
                const selectedOption = document.querySelector(`input[name="question${index}"]:checked`);
                if (selectedOption) {
                    const answerIndex = parseInt(selectedOption.value);
                    if (item.options[answerIndex].correct) {
                        score++;
                    }
                }
            });

            const resultDiv = document.getElementById('result');
            resultDiv.textContent = `Your score is ${score} out of ${quizData.length}`;
        }

        // Load the quiz when the page loads
        window.onload = loadQuiz;
    </script>
</body>
</html>
