<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Quiz Apps</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    animation: {
                        'fade-in': 'fadeIn 0.5s ease-in-out',
                        'bounce-slow': 'bounce 2s infinite',
                    },
                    keyframes: {
                        fadeIn: {
                            '0%': { opacity: 0 },
                            '100%': { opacity: 1 },
                        }
                    }
                }
            }
        }
    </script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&display=swap');
        body {
            font-family: 'Poppins', sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            padding: 1rem;
        }
        .mobile-frame {
            box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.25);
            border-radius: 2rem;
            overflow: hidden;
            position: relative;
        }
        .status-bar {
            height: 24px;
            background: #1f2937;
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 0 1rem;
            font-size: 0.7rem;
            color: white;
        }
        .nav-bar {
            height: 48px;
            background: #000;
            display: flex;
            justify-content: space-around;
            align-items: center;
            color: #6b7280;
        }
        .active-option {
            animation: pulse 1s infinite;
        }
        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.02); }
            100% { transform: scale(1); }
        }
    </style>
</head>
<body>
    <div class="mobile-frame w-full max-w-sm h-[700px] bg-white overflow-hidden relative border-8 border-gray-800">
        <!-- Status Bar -->
        <div class="status-bar">
            <span>12:30</span>
            <div class="flex space-x-1">
                <span>🔋</span>
                <span>📶</span>
            </div>
        </div>
        
        <!-- Main Content Area -->
        <div id="app-container" class="h-[calc(100%-72px)] w-full overflow-hidden relative">
            <!-- Splash Screen -->
            <div id="splash-screen" class="h-full w-full bg-white flex flex-col items-center justify-center animate-fade-in">
                <div class="text-center">
                    <h1 class="text-4xl font-bold text-green-600 mb-2">QUIZ APPS 🎓</h1>
                    <div class="mt-4 animate-spin h-8 w-8 border-4 border-green-500 border-t-transparent rounded-full mx-auto"></div>
                </div>
            </div>
            
            <!-- Home Screen -->
            <div id="home-screen" class="h-full w-full bg-gray-50 flex flex-col items-center justify-center p-6 space-y-8 animate-fade-in hidden">
                <div class="text-center space-y-2">
                    <div class="bg-green-100 p-4 rounded-full inline-block mb-4">
                        <i class="fas fa-star text-green-600 text-4xl"></i>
                    </div>
                    <h1 class="text-3xl font-bold text-green-700">QUIZ APPS</h1>
                    <p class="text-gray-500">Uji pengetahuan Androidmu!</p>
                </div>

                <div class="w-full max-w-xs space-y-4">
                    <button id="leaderboard-btn" class="w-full bg-yellow-400 hover:bg-yellow-500 text-white font-bold py-4 px-6 rounded-xl shadow-md transform transition active:scale-95 flex items-center justify-center gap-2">
                        <i class="fas fa-trophy"></i> LEADERBOARD
                    </button>

                    <button id="play-btn" class="w-full bg-green-600 hover:bg-green-700 text-white font-bold py-4 px-6 rounded-xl shadow-md transform transition active:scale-95 flex items-center justify-center gap-2">
                        <i class="fas fa-play"></i> PLAY
                    </button>
                </div>
            </div>
            
            <!-- Nickname Screen -->
            <div id="nickname-screen" class="h-full w-full bg-white flex flex-col items-center justify-center p-8 animate-fade-in hidden">
                <h2 class="text-2xl font-bold text-gray-800 mb-8">Masukkan Nama</h2>
                
                <div class="w-full max-w-xs relative mb-6">
                    <i class="fas fa-user absolute left-3 top-3 text-gray-400"></i>
                    <input 
                        id="nickname-input" 
                        type="text" 
                        placeholder="Enter nickname" 
                        class="w-full border-2 border-gray-300 rounded-lg py-3 pl-10 pr-4 focus:outline-none focus:border-green-500 transition"
                    />
                </div>

                <button id="start-btn" class="w-full max-w-xs font-bold py-3 rounded-lg shadow-md transition flex items-center justify-center gap-2 bg-gray-300 text-gray-500 cursor-not-allowed">
                    START <i class="fas fa-arrow-right"></i>
                </button>
            </div>
            
            <!-- Quiz Screen -->
            <div id="quiz-screen" class="h-full w-full bg-gray-50 flex flex-col p-6 animate-fade-in hidden">
                <!-- Header / Progress -->
                <div class="mb-6 flex justify-between items-center">
                    <span class="text-sm font-bold text-gray-500">Question <span id="question-number">1</span>/<span id="total-questions">5</span></span>
                    <div class="w-24 h-2 bg-gray-200 rounded-full">
                        <div id="progress-bar" class="h-full bg-green-500 rounded-full transition-all duration-300" style="width: 20%"></div>
                    </div>
                </div>

                <!-- Question -->
                <div class="flex-grow flex flex-col justify-center">
                    <div class="bg-white p-6 rounded-2xl shadow-sm border border-gray-100 mb-6">
                        <h3 id="question-text" class="text-xl font-bold text-gray-800 text-center">Apa bahasa pemrograman resmi Android?</h3>
                    </div>

                    <!-- Options -->
                    <div id="options-container" class="space-y-3">
                        <!-- Options will be dynamically added here -->
                    </div>
                </div>

                <!-- Button Next -->
                <div class="mt-6">
                    <button id="next-btn" class="w-full py-4 rounded-xl font-bold text-lg shadow-md transition bg-gray-300 text-gray-500 cursor-not-allowed">
                        NEXT
                    </button>
                </div>
            </div>
            
            <!-- Result Screen -->
            <div id="result-screen" class="h-full w-full bg-green-600 flex flex-col items-center justify-center p-6 animate-fade-in hidden text-white">
                <i class="fas fa-check-circle text-4xl mb-4 text-green-200 animate-bounce-slow"></i>
                
                <h2 class="text-2xl font-semibold opacity-90 mb-2">Quiz Completed!</h2>
                <h1 id="final-score" class="text-8xl font-bold mb-2 tracking-tighter">0</h1>
                <p class="text-green-100 mb-10 text-lg">Your Final Score</p>

                <button id="done-btn" class="bg-white text-green-700 font-bold py-3 px-10 rounded-full shadow-lg hover:bg-gray-100 transform transition active:scale-95">
                    Done
                </button>
            </div>
            
            <!-- Leaderboard Screen -->
            <div id="leaderboard-screen" class="h-full w-full bg-white flex flex-col animate-fade-in hidden">
                <!-- Toolbar -->
                <div class="p-4 border-b flex items-center bg-green-600 text-white shadow-sm">
                    <button id="back-btn" class="p-2 -ml-2 hover:bg-green-700 rounded-full transition">
                        <i class="fas fa-arrow-right transform rotate-180"></i>
                    </button>
                    <h1 class="text-xl font-bold ml-2">Leaderboard</h1>
                </div>

                <div id="leaderboard-list" class="flex-1 overflow-y-auto p-4">
                    <!-- Leaderboard items will be added here -->
                </div>
            </div>
        </div>

        <!-- Navigation Bar -->
        <div class="nav-bar">
           <div class="w-4 h-4 border-2 border-gray-500 rotate-45 rounded-[2px]"></div>
           <div class="w-4 h-4 border-2 border-gray-500 rounded-full"></div>
           <div class="w-4 h-4 border-2 border-gray-500 rounded-[1px]"></div>
        </div>
    </div>

    <script>
        // Mock data
        const MOCK_LEADERBOARD = [
            { name: "Budi", score: 100 },
            { name: "Siti", score: 80 },
            { name: "Agus", score: 60 },
            { name: "Dewi", score: 40 },
        ];

        const QUESTIONS = [
            {
                question: "Apa bahasa pemrograman resmi Android?",
                options: ["Python", "Kotlin", "Swift", "PHP"],
                answer: 1 // Kotlin
            },
            {
                question: "File layout di Android menggunakan format?",
                options: ["XML", "JSON", "HTML", "YAML"],
                answer: 0 // XML
            },
            {
                question: "Fungsi untuk pindah activity adalah?",
                options: ["Move()", "Go()", "Intent", "Jump"],
                answer: 2 // Intent
            },
            {
                question: "Folder untuk menyimpan gambar adalah?",
                options: ["layout", "values", "drawable", "gradle"],
                answer: 2 // drawable
            },
            {
                question: "Siapa pembuat Android?",
                options: ["Andy Rubin", "Steve Jobs", "Bill Gates", "Mark Zuckerberg"],
                answer: 0 // Andy Rubin
            }
        ];

        // State management
        let currentScreen = 'splash';
        let nickname = '';
        let lastScore = 0;
        let currentQuestionIndex = 0;
        let score = 0;
        let selectedOption = null;

        // DOM Elements
        const screens = {
            splash: document.getElementById('splash-screen'),
            home: document.getElementById('home-screen'),
            nickname: document.getElementById('nickname-screen'),
            quiz: document.getElementById('quiz-screen'),
            result: document.getElementById('result-screen'),
            leaderboard: document.getElementById('leaderboard-screen')
        };

        const navButtons = {
            play: document.getElementById('play-btn'),
            leaderboard: document.getElementById('leaderboard-btn'),
            back: document.getElementById('back-btn'),
            start: document.getElementById('start-btn'),
            next: document.getElementById('next-btn'),
            done: document.getElementById('done-btn')
        };

        const inputs = {
            nickname: document.getElementById('nickname-input')
        };

        const uiElements = {
            questionNumber: document.getElementById('question-number'),
            totalQuestions: document.getElementById('total-questions'),
            progressBar: document.getElementById('progress-bar'),
            questionText: document.getElementById('question-text'),
            optionsContainer: document.getElementById('options-container'),
            finalScore: document.getElementById('final-score'),
            leaderboardList: document.getElementById('leaderboard-list')
        };

        // Navigation functions
        function showScreen(screenName) {
            // Hide all screens
            Object.values(screens).forEach(screen => screen.classList.add('hidden'));
            
            // Show current screen
            screens[screenName].classList.remove('hidden');
            currentScreen = screenName;
            
            // Update UI based on screen
            switch(screenName) {
                case 'quiz':
                    loadQuestion();
                    break;
                case 'leaderboard':
                    renderLeaderboard();
                    break;
                case 'result':
                    uiElements.finalScore.textContent = lastScore;
                    break;
            }
        }

        // Initialize app
        function initApp() {
            // Splash screen timing
            setTimeout(() => {
                showScreen('home');
            }, 2000);

            // Event listeners
            navButtons.play.addEventListener('click', () => {
                showScreen('nickname');
            });

            navButtons.leaderboard.addEventListener('click', () => {
                showScreen('leaderboard');
            });

            navButtons.back.addEventListener('click', () => {
                showScreen('home');
            });

            inputs.nickname.addEventListener('input', () => {
                const startBtn = navButtons.start;
                if (inputs.nickname.value.trim()) {
                    startBtn.className = "w-full max-w-xs font-bold py-3 rounded-lg shadow-md transition flex items-center justify-center gap-2 bg-green-600 text-white hover:bg-green-700 active:scale-95";
                    startBtn.disabled = false;
                } else {
                    startBtn.className = "w-full max-w-xs font-bold py-3 rounded-lg shadow-md transition flex items-center justify-center gap-2 bg-gray-300 text-gray-500 cursor-not-allowed";
                    startBtn.disabled = true;
                }
            });

            navButtons.start.addEventListener('click', () => {
                if (inputs.nickname.value.trim()) {
                    nickname = inputs.nickname.value;
                    showScreen('quiz');
                    currentQuestionIndex = 0;
                    score = 0;
                    selectedOption = null;
                    uiElements.totalQuestions.textContent = QUESTIONS.length;
                }
            });

            navButtons.next.addEventListener('click', handleNextQuestion);
            navButtons.done.addEventListener('click', () => {
                showScreen('home');
            });
        }

        // Quiz functionality
        function loadQuestion() {
            const currentQ = QUESTIONS[currentQuestionIndex];
            uiElements.questionText.textContent = currentQ.question;
            uiElements.questionNumber.textContent = currentQuestionIndex + 1;
            
            // Calculate progress percentage
            const progress = ((currentQuestionIndex + 1) / QUESTIONS.length) * 100;
            uiElements.progressBar.style.width = `${progress}%`;
            
            // Clear previous options
            uiElements.optionsContainer.innerHTML = '';
            
            // Add new options
            currentQ.options.forEach((option, index) => {
                const optionElement = document.createElement('button');
                optionElement.className = `w-full p-4 rounded-xl border-2 text-left transition duration-200 flex items-center ${
                    selectedOption === index 
                        ? 'border-green-500 bg-green-50 text-green-700 font-semibold shadow-sm active-option' 
                        : 'border-gray-200 bg-white text-gray-700 hover:bg-gray-50'
                }`;
                optionElement.innerHTML = `
                    <div class="w-5 h-5 rounded-full border-2 mr-3 flex items-center justify-center ${
                        selectedOption === index ? 'border-green-500' : 'border-gray-300'
                    }">
                        ${selectedOption === index ? '<div class="w-2.5 h-2.5 bg-green-500 rounded-full"></div>' : ''}
                    </div>
                    ${option}
                `;
                
                optionElement.addEventListener('click', () => {
                    selectedOption = index;
                    // Update UI highlighting
                    document.querySelectorAll('#options-container button').forEach(btn => {
                        btn.className = btn.className.replace('active-option', '').replace('border-green-500 bg-green-50 text-green-700 font-semibold shadow-sm', '');
                        btn.className += ' border-gray-200 bg-white text-gray-700 hover:bg-gray-50';
                    });
                    
                    optionElement.className = optionElement.className.replace('border-gray-200 bg-white text-gray-700 hover:bg-gray-50', 'border-green-500 bg-green-50 text-green-700 font-semibold shadow-sm active-option');
                    
                    // Enable next button
                    navButtons.next.className = "w-full py-4 rounded-xl font-bold text-lg shadow-md transition bg-green-600 text-white hover:bg-green-700 active:scale-95";
                    navButtons.next.disabled = false;
                });
                
                uiElements.optionsContainer.appendChild(optionElement);
            });
            
            // Reset next button state
            navButtons.next.className = "w-full py-4 rounded-xl font-bold text-lg shadow-md transition bg-gray-300 text-gray-500 cursor-not-allowed";
            navButtons.next.disabled = true;
        }

        function handleNextQuestion() {
            // Check if answer is correct
            if (selectedOption === QUESTIONS[currentQuestionIndex].answer) {
                score += 20;
            }

            if (currentQuestionIndex + 1 < QUESTIONS.length) {
                currentQuestionIndex++;
                selectedOption = null;
                loadQuestion();
            } else {
                lastScore = score;
                showScreen('result');
            }
        }

        // Leaderboard functionality
        function renderLeaderboard() {
            // Combine mock data with current user session if available
            const displayData = nickname 
                ? [...MOCK_LEADERBOARD, { name: nickname, score: lastScore }].sort((a, b) => b.score - a.score)
                : MOCK_LEADERBOARD;

            uiElements.leaderboardList.innerHTML = '';
            
            displayData.forEach((item, i) => {
                const itemElement = document.createElement('div');
                itemElement.className = `flex items-center justify-between p-4 mb-3 rounded-xl border shadow-sm ${
                    item.name === nickname ? 'bg-green-50 border-green-300' : 'bg-white border-gray-100'
                }`;
                
                let rankClass = '';
                if (i === 0) rankClass = 'bg-yellow-400';
                else if (i === 1) rankClass = 'bg-gray-400';
                else if (i === 2) rankClass = 'bg-orange-400';
                else rankClass = 'bg-green-600';
                
                itemElement.innerHTML = `
                    <div class="flex items-center gap-4">
                        <div class="w-8 h-8 rounded-full flex items-center justify-center font-bold text-white ${rankClass}">
                            ${i + 1}
                        </div>
                        <div>
                            <p class="font-bold text-gray-800">${item.name}</p>
                            ${item.name === nickname ? '<span class="text-xs text-green-600 font-semibold">YOU</span>' : ''}
                        </div>
                    </div>
                    <span class="font-bold text-xl text-green-600">${item.score}</span>
                `;
                
                uiElements.leaderboardList.appendChild(itemElement);
            });
        }

        // Initialize the app when DOM is loaded
        document.addEventListener('DOMContentLoaded', initApp);
    </script>
</body>
</html>
