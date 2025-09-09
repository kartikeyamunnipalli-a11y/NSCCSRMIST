# Tasks

## Task 1
[https://tinyurl.com/3hn5jxm4](https://tinyurl.com/3hn5jxm4)

## Task 2- save it as .html and run it through notepad.
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Interactive Quiz App</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }

        .container {
            background: white;
            border-radius: 15px;
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.1);
            padding: 40px;
            max-width: 800px;
            width: 100%;
            animation: fadeIn 0.5s ease-in;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        h1 {
            text-align: center;
            color: #333;
            margin-bottom: 30px;
            font-size: 2.5em;
            background: linear-gradient(135deg, #667eea, #764ba2);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .quiz-container {
            display: block;
        }

        .question-container {
            margin-bottom: 30px;
            padding: 25px;
            background: #f8f9fa;
            border-radius: 10px;
            border-left: 5px solid #667eea;
            transition: transform 0.2s ease;
        }

        .question-container:hover {
            transform: translateX(5px);
        }

        .question {
            font-size: 1.2em;
            font-weight: 600;
            color: #333;
            margin-bottom: 15px;
        }

        .options {
            display: grid;
            gap: 10px;
        }

        .option {
            display: flex;
            align-items: center;
            padding: 12px 15px;
            background: white;
            border: 2px solid #e9ecef;
            border-radius: 8px;
            cursor: pointer;
            transition: all 0.3s ease;
            position: relative;
        }

        .option:hover {
            border-color: #667eea;
            background: #f0f4ff;
        }

        .option input[type="radio"] {
            margin-right: 12px;
            transform: scale(1.2);
        }

        .option label {
            cursor: pointer;
            font-weight: 500;
            color: #555;
        }

        .option.selected {
            border-color: #667eea;
            background: #f0f4ff;
            box-shadow: 0 2px 10px rgba(102, 126, 234, 0.2);
        }

        .submit-btn {
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
            border: none;
            padding: 15px 40px;
            font-size: 1.1em;
            font-weight: 600;
            border-radius: 50px;
            cursor: pointer;
            display: block;
            margin: 30px auto;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(102, 126, 234, 0.3);
        }

        .submit-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(102, 126, 234, 0.4);
        }

        .submit-btn:active {
            transform: translateY(0);
        }

        .results {
            display: none;
            text-align: center;
            animation: slideIn 0.5s ease-out;
        }

        @keyframes slideIn {
            from { opacity: 0; transform: translateY(30px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .score {
            font-size: 2.5em;
            font-weight: bold;
            margin: 20px 0;
            background: linear-gradient(135deg, #667eea, #764ba2);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .score-message {
            font-size: 1.3em;
            color: #666;
            margin-bottom: 30px;
        }

        .detailed-results {
            margin-top: 30px;
            text-align: left;
        }

        .result-item {
            margin: 15px 0;
            padding: 15px;
            border-radius: 8px;
            border-left: 5px solid #ddd;
        }

        .result-item.correct {
            background: #d4edda;
            border-left-color: #28a745;
        }

        .result-item.incorrect {
            background: #f8d7da;
            border-left-color: #dc3545;
        }

        .result-question {
            font-weight: 600;
            margin-bottom: 8px;
        }

        .result-answer {
            font-size: 0.9em;
            color: #666;
        }

        .restart-btn {
            background: #6c757d;
            color: white;
            border: none;
            padding: 12px 30px;
            font-size: 1em;
            border-radius: 25px;
            cursor: pointer;
            margin-top: 20px;
            transition: all 0.3s ease;
        }

        .restart-btn:hover {
            background: #545b62;
            transform: translateY(-1px);
        }

        .progress-bar {
            width: 100%;
            height: 6px;
            background: #e9ecef;
            border-radius: 3px;
            margin-bottom: 30px;
            overflow: hidden;
        }

        .progress-fill {
            height: 100%;
            background: linear-gradient(90deg, #667eea, #764ba2);
            width: 0%;
            transition: width 0.3s ease;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Interactive Quiz App</h1>
        
        <div class="progress-bar">
            <div class="progress-fill" id="progressFill"></div>
        </div>

        <div class="quiz-container" id="quizContainer">
            <!-- Questions will be generated here -->
        </div>

        <button class="submit-btn" id="submitBtn" onclick="submitQuiz()">Submit Quiz</button>

        <div class="results" id="results">
            <div class="score" id="scoreDisplay"></div>
            <div class="score-message" id="scoreMessage"></div>
            <div class="detailed-results" id="detailedResults"></div>
            <button class="restart-btn" onclick="restartQuiz()">Take Quiz Again</button>
        </div>
    </div>

    <script>
        // Quiz data with 5 multiple choice questions
        const quizData = [
            {
                question: "What does HTML stand for?",
                options: [
                    "Hypertext Markup Language",
                    "High Tech Modern Language",
                    "Home Tool Markup Language",
                    "Hyperlink and Text Markup Language"
                ],
                correct: 0
            },
            {
                question: "Which programming language is known as the 'language of the web'?",
                options: [
                    "Python",
                    "Java",
                    "JavaScript",
                    "C++"
                ],
                correct: 2
            },
            {
                question: "What does CSS stand for?",
                options: [
                    "Computer Style Sheets",
                    "Cascading Style Sheets",
                    "Creative Style Sheets",
                    "Colorful Style Sheets"
                ],
                correct: 1
            },
            {
                question: "Which company developed JavaScript?",
                options: [
                    "Microsoft",
                    "Apple",
                    "Netscape",
                    "Google"
                ],
                correct: 2
            },
            {
                question: "What is the latest version of HTML?",
                options: [
                    "HTML4",
                    "HTML5",
                    "HTML6",
                    "XHTML"
                ],
                correct: 1
            }
        ];

        let userAnswers = [];

        // Generate quiz questions
        function generateQuiz() {
            const container = document.getElementById('quizContainer');
            container.innerHTML = '';

            quizData.forEach((item, index) => {
                const questionDiv = document.createElement('div');
                questionDiv.className = 'question-container';
                
                let optionsHTML = '';
                item.options.forEach((option, optionIndex) => {
                    optionsHTML += `
                        <div class="option" onclick="selectOption(${index}, ${optionIndex}, this)">
                            <input type="radio" name="q${index}" value="${optionIndex}" id="q${index}_${optionIndex}">
                            <label for="q${index}_${optionIndex}">${option}</label>
                        </div>
                    `;
                });

                questionDiv.innerHTML = `
                    <div class="question">${index + 1}. ${item.question}</div>
                    <div class="options">
                        ${optionsHTML}
                    </div>
                `;

                container.appendChild(questionDiv);
            });
        }

        // Handle option selection
        function selectOption(questionIndex, optionIndex, element) {
            // Remove selection from other options in the same question
            const questionContainer = element.parentElement.parentElement;
            const allOptions = questionContainer.querySelectorAll('.option');
            allOptions.forEach(opt => opt.classList.remove('selected'));

            // Add selection to clicked option
            element.classList.add('selected');
            element.querySelector('input').checked = true;

            // Store user answer
            userAnswers[questionIndex] = optionIndex;

            // Update progress bar
            updateProgress();
        }

        // Update progress bar
        function updateProgress() {
            const answeredCount = userAnswers.filter(answer => answer !== undefined).length;
            const progressPercent = (answeredCount / quizData.length) * 100;
            document.getElementById('progressFill').style.width = progressPercent + '%';
        }

        // Submit quiz and show results
        function submitQuiz() {
            // Check if all questions are answered
            if (userAnswers.length < quizData.length || userAnswers.some(answer => answer === undefined)) {
                alert('Please answer all questions before submitting!');
                return;
            }

            // Calculate score
            let correctAnswers = 0;
            const detailedResults = [];

            quizData.forEach((question, index) => {
                const userAnswer = userAnswers[index];
                const isCorrect = userAnswer === question.correct;
                
                if (isCorrect) {
                    correctAnswers++;
                }

                detailedResults.push({
                    question: question.question,
                    userAnswer: question.options[userAnswer],
                    correctAnswer: question.options[question.correct],
                    isCorrect: isCorrect
                });
            });

            // Display results
            showResults(correctAnswers, detailedResults);
        }

        // Show results
        function showResults(score, detailed) {
            document.getElementById('quizContainer').style.display = 'none';
            document.getElementById('submitBtn').style.display = 'none';
            document.getElementById('results').style.display = 'block';

            // Display score
            document.getElementById('scoreDisplay').textContent = `${score}/${quizData.length}`;
            
            // Display score message
            let message = '';
            const percentage = (score / quizData.length) * 100;
            if (percentage === 100) {
                message = 'Perfect! Outstanding work! 🎉';
            } else if (percentage >= 80) {
                message = 'Excellent! Great job! 👏';
            } else if (percentage >= 60) {
                message = 'Good work! Keep it up! 👍';
            } else {
                message = 'Keep practicing! You can do better! 💪';
            }
            document.getElementById('scoreMessage').textContent = message;

            // Display detailed results (Brownie subtask)
            const detailedContainer = document.getElementById('detailedResults');
            detailedContainer.innerHTML = '<h3 style="margin-bottom: 20px; color: #333;">Detailed Results:</h3>';

            detailed.forEach((result, index) => {
                const resultDiv = document.createElement('div');
                resultDiv.className = `result-item ${result.isCorrect ? 'correct' : 'incorrect'}`;
                
                resultDiv.innerHTML = `
                    <div class="result-question">${index + 1}. ${result.question}</div>
                    <div class="result-answer">
                        <strong>Your answer:</strong> ${result.userAnswer}<br>
                        <strong>Correct answer:</strong> ${result.correctAnswer}<br>
                        <strong>Status:</strong> ${result.isCorrect ? '✓ Correct' : '✗ Incorrect'}
                    </div>
                `;

                detailedContainer.appendChild(resultDiv);
            });
        }

        // Restart quiz
        function restartQuiz() {
            userAnswers = [];
            document.getElementById('quizContainer').style.display = 'block';
            document.getElementById('submitBtn').style.display = 'block';
            document.getElementById('results').style.display = 'none';
            document.getElementById('progressFill').style.width = '0%';
            generateQuiz();
        }

        // Initialize quiz when page loads
        document.addEventListener('DOMContentLoaded', function() {
            generateQuiz();
        });
    </script>
</body>
</html>
