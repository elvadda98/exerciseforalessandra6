<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vocabulary Game: Expressions & Personal Development</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #6a93cb 0%, #a4bfef 100%);
            min-height: 100vh;
            padding: 20px;
            color: #2c3e50;
        }

        .container {
            max-width: 1000px;
            margin: 0 auto;
            background: white;
            border-radius: 20px;
            box-shadow: 0 15px 35px rgba(0,0,0,0.2);
            overflow: hidden;
        }

        .header {
            background: linear-gradient(135deg, #4a6fa5, #6a93cb);
            color: white;
            padding: 30px;
            text-align: center;
            position: relative;
        }

        .header h1 {
            font-size: 2.5em;
            margin-bottom: 10px;
            position: relative;
            z-index: 1;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.2);
        }

        .header p {
            font-size: 1.2em;
            opacity: 0.9;
            position: relative;
            z-index: 1;
        }

        .nav-buttons {
            display: flex;
            justify-content: center;
            gap: 10px;
            padding: 20px;
            background: #f8f9fa;
            flex-wrap: wrap;
        }

        .nav-btn {
            padding: 12px 24px;
            border: none;
            border-radius: 25px;
            cursor: pointer;
            font-size: 16px;
            font-weight: bold;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(0,0,0,0.1);
        }

        .nav-btn.active {
            background: linear-gradient(135deg, #4a6fa5, #6a93cb);
            color: white;
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(74, 111, 165, 0.4);
        }

        .nav-btn:not(.active) {
            background: white;
            color: #666;
        }

        .nav-btn:hover:not(.active) {
            background: #e9ecef;
            transform: translateY(-1px);
        }

        .game-section {
            display: none;
            padding: 30px;
            min-height: 400px;
        }

        .game-section.active {
            display: block;
            animation: fadeIn 0.5s ease-in;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .word-bank {
            background: linear-gradient(135deg, #f5f7fa, #e8f4f2);
            padding: 25px;
            border-radius: 15px;
            margin-bottom: 25px;
            border: 2px solid #4a6fa5;
            box-shadow: 0 4px 15px rgba(74, 111, 165, 0.2);
        }

        .word-bank h3 {
            color: #4a6fa5;
            margin-bottom: 15px;
            text-align: center;
            font-size: 1.4em;
        }

        .word-options {
            display: flex;
            flex-wrap: wrap;
            gap: 12px;
            justify-content: center;
        }

        .word-option {
            background: linear-gradient(135deg, #4a6fa5, #6a93cb);
            color: white;
            padding: 10px 18px;
            border-radius: 20px;
            font-weight: bold;
            font-size: 16px;
            box-shadow: 0 3px 10px rgba(74, 111, 165, 0.3);
            transition: all 0.3s ease;
            cursor: default;
        }

        .word-option:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(74, 111, 165, 0.4);
        }

        .question {
            background: #f8f9fa;
            padding: 25px;
            border-radius: 15px;
            margin-bottom: 20px;
            border-left: 5px solid #4a6fa5;
            box-shadow: 0 4px 15px rgba(0,0,0,0.05);
        }

        .question h3 {
            color: #4a6fa5;
            margin-bottom: 15px;
            font-size: 1.3em;
        }

        .fill-blank {
            background: #fff;
            border: 2px solid #ddd;
            border-radius: 8px;
            padding: 8px 12px;
            font-size: 16px;
            margin: 0 5px;
            min-width: 120px;
            transition: border-color 0.3s ease;
        }

        .fill-blank.correct {
            border-color: #4CAF50;
            background: #e8f5e8;
        }

        .fill-blank.incorrect {
            border-color: #f44336;
            background: #ffeaea;
        }

        .options {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 15px;
            margin-top: 15px;
        }

        .option {
            padding: 15px 20px;
            border: 2px solid #ddd;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s ease;
            background: white;
            text-align: center;
            font-weight: 500;
        }

        .option:hover {
            border-color: #4a6fa5;
            transform: translateY(-2px);
            box-shadow: 0 4px 15px rgba(74, 111, 165, 0.2);
        }

        .option.selected {
            background: #4a6fa5;
            color: white;
            border-color: #4a6fa5;
        }

        .option.correct {
            background: #4CAF50;
            color: white;
            border-color: #4CAF50;
        }

        .option.incorrect {
            background: #f44336;
            color: white;
            border-color: #f44336;
        }

        .matching-container {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 30px;
            margin-top: 20px;
        }

        .match-column h4 {
            text-align: center;
            margin-bottom: 15px;
            color: #4a6fa5;
            font-size: 1.2em;
        }

        .match-item {
            padding: 15px;
            margin: 8px 0;
            border: 2px solid #ddd;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s ease;
            background: white;
            text-align: center;
            font-weight: 500;
        }

        .match-item:hover {
            border-color: #4a6fa5;
            transform: translateY(-1px);
            box-shadow: 0 4px 15px rgba(74, 111, 165, 0.2);
        }

        .match-item.selected {
            background: #e8f4f2;
            border-color: #4a6fa5;
        }

        .match-item.matched {
            background: #4CAF50;
            color: white;
            border-color: #4CAF50;
            cursor: default;
        }

        .check-btn {
            background: linear-gradient(135deg, #4a6fa5, #6a93cb);
            color: white;
            border: none;
            padding: 15px 30px;
            border-radius: 25px;
            cursor: pointer;
            font-size: 16px;
            font-weight: bold;
            margin: 20px auto;
            display: block;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(74, 111, 165, 0.3);
        }

        .check-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(74, 111, 165, 0.4);
        }

        .feedback {
            margin-top: 15px;
            padding: 15px;
            border-radius: 10px;
            font-weight: bold;
            text-align: center;
            animation: slideIn 0.3s ease;
        }

        @keyframes slideIn {
            from { transform: translateX(-20px); opacity: 0; }
            to { transform: translateX(0); opacity: 1; }
        }

        .feedback.correct {
            background: #d4edda;
            color: #155724;
            border: 1px solid #c3e6cb;
        }

        .feedback.incorrect {
            background: #f8d7da;
            color: #721c24;
            border: 1px solid #f5c6cb;
        }

        .score {
            position: fixed;
            top: 20px;
            right: 20px;
            background: linear-gradient(135deg, #4a6fa5, #6a93cb);
            color: white;
            padding: 15px 20px;
            border-radius: 25px;
            font-weight: bold;
            box-shadow: 0 4px 15px rgba(74, 111, 165, 0.3);
            z-index: 1000;
        }

        .icon {
            font-size: 24px;
            margin-right: 10px;
            vertical-align: middle;
        }

        @media (max-width: 768px) {
            .matching-container {
                grid-template-columns: 1fr;
                gap: 20px;
            }
            
            .nav-buttons {
                flex-direction: column;
                align-items: center;
            }
            
            .nav-btn {
                width: 200px;
            }
            
            .score {
                position: static;
                margin: 20px auto;
                display: block;
                width: fit-content;
            }
        }
    </style>
</head>
<body>
    <div class="score">Score: <span id="score">0</span>/18</div>
    
    <div class="container">
        <div class="header">
            <h1><i class="fas fa-book icon"></i> Vocabulary Game: Expressions & Personal Development</h1>
            <p>Test your knowledge of these useful English expressions and personal development terms!</p>
        </div>

        <div class="nav-buttons">
            <button class="nav-btn active" onclick="showSection('fill-gaps')">Fill in the Gaps</button>
            <button class="nav-btn" onclick="showSection('matching')">Match Meanings</button>
            <button class="nav-btn" onclick="showSection('multiple-choice')">Multiple Choice</button>
        </div>

        <!-- Fill in the Gaps Section -->
        <div id="fill-gaps" class="game-section active">
            <div class="word-bank">
                <h3><i class="fas fa-list-ul icon"></i> Word Bank - Choose from these words:</h3>
                <div class="word-options">
                    <span class="word-option">worried</span>
                    <span class="word-option">assignment</span>
                    <span class="word-option">to hand in</span>
                    <span class="word-option">essay</span>
                    <span class="word-option">mark</span>
                    <span class="word-option">breed</span>
                    <span class="word-option">willpower</span>
                    <span class="word-option">motivate</span>
                    <span class="word-option">relatives</span>
                    <span class="word-option">hold back</span>
                    <span class="word-option">come across</span>
                </div>
            </div>

            <div class="question">
                <h3>Question 1:</h3>
                <p>Don't let fear <input type="text" class="fill-blank" data-answer="hold back" placeholder="answer"> from pursuing your dreams.</p>
                <div class="feedback" id="feedback-1" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 2:</h3>
                <p>I need to write a 2000-word <input type="text" class="fill-blank" data-answer="essay" placeholder="answer"> on climate change for my environmental science class.</p>
                <div class="feedback" id="feedback-2" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 3:</h3>
                <p>I hope I get a good <input type="text" class="fill-blank" data-answer="mark" placeholder="answer"> on my presentation; I worked really hard on it.</p>
                <div class="feedback" id="feedback-3" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 4:</h3>
                <p>My coach knows how to <input type="text" class="fill-blank" data-answer="motivate" placeholder="answer"> the team to perform at our best.</p>
                <div class="feedback" id="feedback-4" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 5:</h3>
                <p>I'm <input type="text" class="fill-blank" data-answer="worried" placeholder="answer"> about my exam results; I don't think I did very well.</p>
                <div class="feedback" id="feedback-5" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 6:</h3>
                <p>Our history teacher gave us a new <input type="text" class="fill-blank" data-answer="assignment" placeholder="answer"> that's due next Friday.</p>
                <div class="feedback" id="feedback-6" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 7:</h3>
                <p>We're having a family reunion, and all our <input type="text" class="fill-blank" data-answer="relatives" placeholder="answer"> from across the country will be there.</p>
                <div class="feedback" id="feedback-7" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 8:</h3>
                <p>Don't forget to <input type="text" class="fill-blank" data-answer="to hand in" placeholder="answer"> your permission slips before the field trip.</p>
                <div class="feedback" id="feedback-8" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 9:</h3>
                <p>When I clean out my closet, I always <input type="text" class="fill-blank" data-answer="come across" placeholder="answer"> clothes I forgot I owned.</p>
                <div class="feedback" id="feedback-9" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 10:</h3>
                <p>Persistence and hard work <input type="text" class="fill-blank" data-answer="breed" placeholder="answer"> success in any field.</p>
                <div class="feedback" id="feedback-10" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 11:</h3>
                <p>It takes tremendous <input type="text" class="fill-blank" data-answer="willpower" placeholder="answer"> to resist eating sweets when you're on a diet.</p>
                <div class="feedback" id="feedback-11" style="display: none;"></div>
            </div>

            <button class="check-btn" onclick="checkFillBlanks()">Check Answers</button>
        </div>

        <!-- Matching Section -->
        <div id="matching" class="game-section">
            <h2 style="text-align: center; margin-bottom: 20px; color: #4a6fa5;">Match the expressions with their meanings</h2>
            <div class="matching-container">
                <div class="match-column">
                    <h4>Words</h4>
                    <div class="match-item" data-word="worried" onclick="selectMatch(this)">worried</div>
                    <div class="match-item" data-word="assignment" onclick="selectMatch(this)">assignment</div>
                    <div class="match-item" data-word="to hand in" onclick="selectMatch(this)">to hand in</div>
                    <div class="match-item" data-word="essay" onclick="selectMatch(this)">essay</div>
                    <div class="match-item" data-word="mark" onclick="selectMatch(this)">mark</div>
                    <div class="match-item" data-word="breed" onclick="selectMatch(this)">breed</div>
                    <div class="match-item" data-word="willpower" onclick="selectMatch(this)">willpower</div>
                    <div class="match-item" data-word="motivate" onclick="selectMatch(this)">motivate</div>
                    <div class="match-item" data-word="relatives" onclick="selectMatch(this)">relatives</div>
                    <div class="match-item" data-word="hold back" onclick="selectMatch(this)">hold back</div>
                    <div class="match-item" data-word="come across" onclick="selectMatch(this)">come across</div>
                </div>
                <div class="match-column">
                    <h4>Meanings</h4>
                    <div class="match-item" data-meaning="mark" onclick="selectMatch(this)">A grade or score given for academic work</div>
                    <div class="match-item" data-meaning="breed" onclick="selectMatch(this)">To cause something to happen or develop</div>
                    <div class="match-item" data-meaning="relatives" onclick="selectMatch(this)">Members of one's family</div>
                    <div class="match-item" data-meaning="to hand in" onclick="selectMatch(this)">To submit or deliver something</div>
                    <div class="match-item" data-meaning="assignment" onclick="selectMatch(this)">A task or piece of work assigned to someone</div>
                    <div class="match-item" data-meaning="hold back" onclick="selectMatch(this)">To prevent or restrain from doing something</div>
                    <div class="match-item" data-meaning="essay" onclick="selectMatch(this)">A short piece of writing on a particular subject</div>
                    <div class="match-item" data-meaning="come across" onclick="selectMatch(this)">To find or encounter something unexpectedly</div>
                    <div class="match-item" data-meaning="willpower" onclick="selectMatch(this)">The ability to control one's impulses and actions</div>
                    <div class="match-item" data-meaning="worried" onclick="selectMatch(this)">Anxious or concerned about something</div>
                    <div class="match-item" data-meaning="motivate" onclick="selectMatch(this)">To provide someone with a reason to do something</div>
                </div>
            </div>
            <div class="feedback" id="matching-feedback" style="display: none;"></div>
        </div>

        <!-- Multiple Choice Section -->
        <div id="multiple-choice" class="game-section">
            <div class="question">
                <h3>Question 1: What does "worried" mean?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Excited and enthusiastic</div>
                    <div class="option" onclick="selectOption(this, true)">Anxious or concerned about something</div>
                    <div class="option" onclick="selectOption(this, false)">Completely certain</div>
                    <div class="option" onclick="selectOption(this, false)">Indifferent or uncaring</div>
                </div>
                <div class="feedback" id="mc-feedback-1" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 2: An "assignment" is:</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">A type of vacation</div>
                    <div class="option" onclick="selectOption(this, true)">A task or piece of work assigned to someone</div>
                    <div class="option" onclick="selectOption(this, false)">A social gathering</div>
                    <div class="option" onclick="selectOption(this, false)">A form of transportation</div>
                </div>
                <div class="feedback" id="mc-feedback-2" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 3: "To hand in" means:</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">To applaud someone</div>
                    <div class="option" onclick="selectOption(this, true)">To submit or deliver something</div>
                    <div class="option" onclick="selectOption(this, false)">To reject an offer</div>
                    <div class="option" onclick="selectOption(this, false)">To physically hand something to someone</div>
                </div>
                <div class="feedback" id="mc-feedback-3" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 4: An "essay" is:</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">A type of exam</div>
                    <div class="option" onclick="selectOption(this, true)">A short piece of writing on a particular subject</div>
                    <div class="option" onclick="selectOption(this, false)">A verbal presentation</div>
                    <div class="option" onclick="selectOption(this, false)">A mathematical problem</div>
                </div>
                <div class="feedback" id="mc-feedback-4" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 5: A "mark" in academic context refers to:</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">A spot on paper</div>
                    <div class="option" onclick="selectOption(this, true)">A grade or score given for academic work</div>
                    <div class="option" onclick="selectOption(this, false)">A target to aim for</div>
                    <div class="option" onclick="selectOption(this, false)">A signature</div>
                </div>
                <div class="feedback" id="mc-feedback-5" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 6: "Breed" in this context means:</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">To raise animals</div>
                    <div class="option" onclick="selectOption(this, true)">To cause something to happen or develop</div>
                    <div class="option" onclick="selectOption(this, false)">To mix ingredients</div>
                    <div class="option" onclick="selectOption(this, false)">To create a new type of something</div>
                </div>
                <div class="feedback" id="mc-feedback-6" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 7: "Willpower" refers to:</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Physical strength</div>
                    <div class="option" onclick="selectOption(this, true)">The ability to control one's impulses and actions</div>
                    <div class="option" onclick="selectOption(this, false)">Legal authority</div>
                    <div class="option" onclick="selectOption(this, false)">Financial resources</div>
                </div>
                <div class="feedback" id="mc-feedback-7" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 8: To "motivate" someone means:</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">To criticize them</div>
                    <div class="option" onclick="selectOption(this, true)">To provide someone with a reason to do something</div>
                    <div class="option" onclick="selectOption(this, false)">To pay them money</div>
                    <div class="option" onclick="selectOption(this, false)">To give them instructions</div>
                </div>
                <div class="feedback" id="mc-feedback-8" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 9: "Relatives" are:</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Close friends</div>
                    <div class="option" onclick="selectOption(this, true)">Members of one's family</div>
                    <div class="option" onclick="selectOption(this, false)">Work colleagues</div>
                    <div class="option" onclick="selectOption(this, false)">Neighbors</div>
                </div>
                <div class="feedback" id="mc-feedback-9" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 10: To "hold back" means:</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">To support someone</div>
                    <div class="option" onclick="selectOption(this, true)">To prevent or restrain from doing something</div>
                    <div class="option" onclick="selectOption(this, false)">To remember something</div>
                    <div class="option" onclick="selectOption(this, false)">To move forward quickly</div>
                </div>
                <div class="feedback" id="mc-feedback-10" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 11: To "come across" something means:</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">To avoid something</div>
                    <div class="option" onclick="selectOption(this, true)">To find or encounter something unexpectedly</div>
                    <div class="option" onclick="selectOption(this, false)">To travel to a place</div>
                    <div class="option" onclick="selectOption(this, false)">To explain something clearly</div>
                </div>
                <div class="feedback" id="mc-feedback-11" style="display: none;"></div>
            </div>
        </div>
    </div>

    <script>
        let score = 0;
        let selectedWord = null;
        let selectedMeaning = null;
        let matchedPairs = [];

        function showSection(sectionId) {
            // Hide all sections
            document.querySelectorAll('.game-section').forEach(section => {
                section.classList.remove('active');
            });
            
            // Remove active class from all buttons
            document.querySelectorAll('.nav-btn').forEach(btn => {
                btn.classList.remove('active');
            });
            
            // Show selected section
            document.getElementById(sectionId).classList.add('active');
            
            // Add active class to clicked button
            event.target.classList.add('active');
        }

        function checkFillBlanks() {
            const blanks = document.querySelectorAll('.fill-blank');
            let correctCount = 0;
            
            blanks.forEach((blank, index) => {
                const userAnswer = blank.value.toLowerCase().trim();
                const correctAnswer = blank.dataset.answer.toLowerCase();
                
                if (userAnswer === correctAnswer) {
                    blank.classList.remove('incorrect');
                    blank.classList.add('correct');
                    correctCount++;
                } else {
                    blank.classList.remove('correct');
                    blank.classList.add('incorrect');
                }
                
                // Show feedback for each question
                const feedback = document.getElementById(`feedback-${index+1}`);
                if (userAnswer === correctAnswer) {
                    feedback.textContent = '✅ Correct!';
                    feedback.className = 'feedback correct';
                } else {
                    feedback.textContent = `❌ Incorrect. The correct answer is: "${blank.dataset.answer}"`;
                    feedback.className = 'feedback incorrect';
                }
                feedback.style.display = 'block';
            });
            
            updateScore();
        }

        function selectMatch(element) {
            if (element.classList.contains('matched')) return;
            
            if (element.dataset.word) {
                // Word selected
                if (selectedWord) selectedWord.classList.remove('selected');
                selectedWord = element;
                element.classList.add('selected');
            } else {
                // Meaning selected
                if (selectedMeaning) selectedMeaning.classList.remove('selected');
                selectedMeaning = element;
                element.classList.add('selected');
            }
            
            // Check if we have both word and meaning selected
            if (selectedWord && selectedMeaning) {
                checkMatch();
            }
        }

        function checkMatch() {
            const feedback = document.getElementById('matching-feedback');
            
            if (selectedWord.dataset.word === selectedMeaning.dataset.meaning) {
                // Correct match
                selectedWord.classList.remove('selected');
                selectedWord.classList.add('matched');
                selectedMeaning.classList.remove('selected');
                selectedMeaning.classList.add('matched');
                
                matchedPairs.push(selectedWord.dataset.word);
                
                feedback.textContent = '✅ Correct match!';
                feedback.className = 'feedback correct';
                
                // Check if all matches are complete
                if (matchedPairs.length === 11) {
                    feedback.textContent = '🎉 Congratulations! You matched all terms correctly!';
                }
            } else {
                // Incorrect match
                feedback.textContent = '❌ Incorrect match. Try again.';
                feedback.className = 'feedback incorrect';
            }
            
            feedback.style.display = 'block';
            selectedWord = null;
            selectedMeaning = null;
            
            updateScore();
        }

        function selectOption(element, isCorrect) {
            // Remove selection from all options in this question
            const options = element.parentElement.querySelectorAll('.option');
            options.forEach(opt => {
                opt.classList.remove('selected');
                opt.classList.remove('correct');
                opt.classList.remove('incorrect');
            });
            
            // Mark the selected option
            element.classList.add('selected');
            
            const questionNumber = element.closest('.question').querySelector('h3').textContent.match(/\d+/)[0];
            const feedback = document.getElementById(`mc-feedback-${questionNumber}`);
            
            if (isCorrect) {
                element.classList.add('correct');
                feedback.textContent = '✅ Correct!';
                feedback.className = 'feedback correct';
            } else {
                element.classList.add('incorrect');
                feedback.textContent = '❌ Incorrect. Try again.';
                feedback.className = 'feedback incorrect';
                
                // Show the correct answer
                options.forEach(opt => {
                    if (opt.onclick.toString().includes('true')) {
                        opt.classList.add('correct');
                    }
                });
            }
            
            feedback.style.display = 'block';
            updateScore();
        }

        function updateScore() {
            // Calculate score for fill-in-the-blank
            let fillScore = 0;
            document.querySelectorAll('.fill-blank.correct').forEach(blank => {
                if (!blank.classList.contains('counted')) {
                    fillScore++;
                    blank.classList.add('counted');
                }
            });
            
            // Calculate score for matching (each pair is 1 point)
            const matchScore = matchedPairs.length;
            
            // Calculate score for multiple choice (each correct is 1 point)
            let mcScore = 0;
            document.querySelectorAll('.option.correct.selected').forEach(opt => {
                mcScore++;
            });
            
            // Total score
            score = fillScore + matchScore + mcScore;
            document.getElementById('score').textContent = score;
        }
    </script>
</body>
</html>
