<html lang="ru" class="dark">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Majestic RP — Сбор Средств 8,000,000$</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Google Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=Montserrat:ital,wght@0,300;0,400;0,600;0,700;0,800;0,900;1,800&display=swap" rel="stylesheet">
    
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    colors: {
                        majestic: {
                            bg: '#0a0812',
                            card: '#130e24',
                            purple: '#8b5cf6',
                            purpleGlow: '#a855f7',
                            gold: '#fbbf24',
                            goldGlow: '#f59e0b',
                            accent: '#22c55e',
                            darkGlass: 'rgba(19, 14, 36, 0.75)',
                            borderGlass: 'rgba(139, 92, 246, 0.25)'
                        }
                    },
                    fontFamily: {
                        sans: ['Montserrat', 'sans-serif'],
                    },
                    animation: {
                        'pulse-glow': 'pulseGlow 2s infinite alternate',
                        'float': 'float 3s ease-in-out infinite',
                        'wave': 'wave 4s ease-in-out infinite'
                    },
                    keyframes: {
                        pulseGlow: {
                            '0%': { boxShadow: '0 0 15px rgba(139, 92, 246, 0.3)' },
                            '100%': { boxShadow: '0 0 30px rgba(168, 85, 247, 0.8), 0 0 10px rgba(251, 191, 36, 0.4)' },
                        },
                        float: {
                            '0%, 100%': { transform: 'translateY(0px)' },
                            '50%': { transform: 'translateY(-8px)' }
                        },
                        wave: {
                            '0%, 100%': { transform: 'rotate(-2deg)' },
                            '50%': { transform: 'rotate(2deg)' }
                        }
                    }
                }
            }
        }
    </script>

    <style>
        body {
            background-color: #0a0812;
            background-image: 
                radial-gradient(circle at 15% 20%, rgba(139, 92, 246, 0.15) 0%, transparent 40%),
                radial-gradient(circle at 85% 70%, rgba(245, 158, 11, 0.1) 0%, transparent 40%),
                radial-gradient(circle at 50% 50%, rgba(10, 8, 18, 0.9) 0%, #0a0812 100%);
            background-attachment: fixed;
        }

        /* Glassmorphism custom utilities */
        .glass-panel {
            background: rgba(19, 14, 36, 0.75);
            backdrop-filter: blur(16px);
            -webkit-backdrop-filter: blur(16px);
            border: 1px solid rgba(139, 92, 246, 0.2);
            box-shadow: 0 8px 32px 0 rgba(0, 0, 0, 0.5);
        }

        .glass-input {
            background: rgba(10, 8, 18, 0.7);
            border: 1px solid rgba(139, 92, 246, 0.3);
            color: #ffffff;
            transition: all 0.3s ease;
        }

        .glass-input:focus {
            border-color: #a855f7;
            box-shadow: 0 0 12px rgba(168, 85, 247, 0.4);
            outline: none;
        }

        /* Jar liquid wave styling */
        .liquid-container {
            position: relative;
            overflow: hidden;
            border-radius: 0 0 35px 35px;
        }

        .liquid-fill {
            position: absolute;
            bottom: 0;
            left: 0;
            width: 100%;
            background: linear-gradient(180deg, #a855f7 0%, #6d28d9 60%, #4c1d95 100%);
            transition: height 1s ease-in-out;
            box-shadow: 0 0 20px rgba(168, 85, 247, 0.6) inset;
        }

        .liquid-fill::before {
            content: "";
            position: absolute;
            width: 200%;
            height: 20px;
            top: -10px;
            left: -50%;
            background: rgba(251, 191, 36, 0.4);
            border-radius: 40%;
            animation: wave 3s ease-in-out infinite alternate;
        }

        /* Custom Scrollbar */
        ::-webkit-scrollbar {
            width: 6px;
        }
        ::-webkit-scrollbar-track {
            background: rgba(10, 8, 18, 0.8);
        }
        ::-webkit-scrollbar-thumb {
            background: #6d28d9;
            border-radius: 4px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #8b5cf6;
        }
    </style>
</head>
<body class="text-slate-100 min-h-screen font-sans flex flex-col justify-between selection:bg-purple-600 selection:text-white">

    <!-- Navbar Header -->
    <header class="w-full glass-panel border-b border-purple-900/40 sticky top-0 z-40">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-20 flex items-center justify-between">
            <!-- Brand Logo / Title -->
            <div class="flex items-center space-x-3">
                <div class="w-10 h-10 rounded-xl bg-gradient-to-tr from-purple-600 to-amber-500 flex items-center justify-center font-black text-xl text-black shadow-lg shadow-purple-500/30">
                    M
                </div>
                <div>
                    <h1 class="font-extrabold tracking-wider text-xl bg-clip-text text-transparent bg-gradient-to-r from-purple-400 via-pink-400 to-amber-400">
                        MAJESTIC <span class="text-white text-xs px-2 py-0.5 rounded bg-purple-900/60 border border-purple-500/30 ml-1">RP</span>
                    </h1>
                    <p class="text-xs text-slate-400 tracking-wider uppercase font-semibold">Сбор Средств / Crowdfunding</p>
                </div>
            </div>

            <!-- Action Buttons -->
            <div class="flex items-center space-x-3">
                <button onclick="toggleGithubModal()" class="px-4 py-2 rounded-xl text-xs font-semibold glass-input hover:bg-purple-900/40 text-purple-300 transition duration-300 flex items-center gap-2">
                    <i class="fa-brands fa-github text-base"></i>
                    <span class="hidden sm:inline">Как загрузить на GitHub</span>
                </button>
                <button onclick="resetDataPrompt()" title="Сбросить данные" class="p-2 rounded-xl glass-input hover:bg-red-900/40 text-slate-400 hover:text-red-400 transition duration-300">
                    <i class="fa-solid fa-rotate-right"></i>
                </button>
            </div>
        </div>
    </header>

    <!-- Main Content Grid -->
    <main class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-8 w-full flex-grow grid grid-cols-1 lg:grid-cols-12 gap-8 items-start">
        
        <!-- Left Column: Goal Summary & Visual Jar (5 Cols) -->
        <section class="lg:col-span-5 flex flex-col gap-6">
            
            <!-- Target Card -->
            <div class="glass-panel rounded-3xl p-6 relative overflow-hidden animate-pulse-glow">
                <div class="absolute -right-10 -bottom-10 w-40 h-40 bg-purple-600/10 rounded-full blur-3xl pointer-events-none"></div>
                
                <div class="flex justify-between items-start mb-4">
                    <div>
                        <span class="text-xs uppercase tracking-widest text-amber-400 font-bold flex items-center gap-1">
                            <i class="fa-solid fa-crosshairs"></i> Главная Цель
                        </span>
                        <h2 class="text-2xl font-black text-white mt-1">На Большую Мечту</h2>
                    </div>
                    <span class="px-3 py-1 rounded-full text-xs font-bold bg-amber-500/20 text-amber-300 border border-amber-500/30 shadow-sm">
                        GTA 5 RP
                    </span>
                </div>

                <!-- Numbers Display -->
                <div class="my-4">
                    <div class="flex justify-between items-baseline mb-1">
                        <span class="text-sm text-slate-400">Собрано:</span>
                        <span id="raised-text" class="text-3xl font-black text-transparent bg-clip-text bg-gradient-to-r from-amber-300 via-amber-400 to-amber-500">
                            $0
                        </span>
                    </div>
                    <div class="flex justify-between items-center text-xs text-slate-400 font-semibold">
                        <span>Цель: <strong class="text-slate-200" id="target-text">$8,000,000</strong></span>
                        <span id="percent-text" class="text-purple-400 font-bold">0%</span>
                    </div>
                </div>

                <!-- Progress Bar -->
                <div class="w-full bg-slate-900/80 h-4 rounded-full overflow-hidden p-0.5 border border-purple-900/50 relative">
                    <div id="progress-bar" class="h-full bg-gradient-to-r from-purple-600 via-pink-500 to-amber-400 rounded-full transition-all duration-1000 ease-out w-0 relative">
                        <div class="absolute inset-0 bg-white/20 animate-pulse"></div>
                    </div>
                </div>
            </div>

            <!-- The Majestic Jar / Piggy Bank Container -->
            <div class="glass-panel rounded-3xl p-6 flex flex-col items-center justify-center relative overflow-hidden">
                <h3 class="text-sm font-bold uppercase tracking-wider text-slate-300 mb-6 flex items-center gap-2">
                    <i class="fa-solid fa-jar text-amber-400 text-lg"></i> Магическая Баночка
                </h3>

                <!-- Visual Jar Element -->
                <div class="relative w-48 h-64 border-4 border-purple-400/40 rounded-b-[40px] rounded-t-[15px] bg-slate-950/60 shadow-[0_0_30px_rgba(139,92,246,0.2)] flex flex-col justify-end overflow-hidden backdrop-blur-md">
                    <!-- Glass Shine Highlight -->
                    <div class="absolute top-0 left-3 w-3 h-full bg-gradient-to-b from-white/30 via-white/10 to-transparent rounded-full z-20 pointer-events-none"></div>
                    <div class="absolute top-2 right-3 w-1.5 h-full bg-gradient-to-b from-white/20 to-transparent rounded-full z-20 pointer-events-none"></div>
                    
                    <!-- Jar Lid -->
                    <div class="absolute -top-1 left-1/2 -translate-x-1/2 w-40 h-5 bg-gradient-to-r from-amber-600 via-amber-400 to-amber-600 rounded-t-md border-b border-amber-800 z-30 shadow-md"></div>

                    <!-- Liquid Inside -->
                    <div id="jar-liquid" class="liquid-fill" style="height: 0%;">
                        <!-- Floating Gold Coins inside Liquid -->
                        <div class="absolute inset-0 opacity-40 pointer-events-none">
                            <i class="fa-solid fa-coins absolute left-4 bottom-6 text-amber-300 animate-float text-sm"></i>
                            <i class="fa-solid fa-sack-dollar absolute right-6 bottom-12 text-amber-200 animate-float text-xs" style="animation-delay: 1s;"></i>
                            <i class="fa-solid fa-gem absolute left-12 bottom-16 text-purple-200 animate-float text-xs" style="animation-delay: 1.5s;"></i>
                        </div>
                    </div>

                    <!-- Percentage Overlay inside Jar -->
                    <div class="absolute inset-0 flex items-center justify-center z-20 pointer-events-none">
                        <span id="jar-percent" class="text-3xl font-black text-white drop-shadow-[0_2px_8px_rgba(0,0,0,0.8)]">0%</span>
                    </div>
                </div>

                <p class="text-xs text-slate-400 text-center mt-4 max-w-xs">
                    Баночка наполняется в реальном времени при добавлении новых пожертвований!
                </p>
            </div>

        </section>

        <!-- Right Column: Contribution Form & Leaderboard (7 Cols) -->
        <section class="lg:col-span-7 flex flex-col gap-6">

            <!-- Donation Input Form -->
            <div class="glass-panel rounded-3xl p-6 sm:p-8 relative">
                <div class="flex items-center gap-3 mb-6">
                    <div class="p-3 bg-purple-600/20 border border-purple-500/30 rounded-2xl text-purple-400">
                        <i class="fa-solid fa-hand-holding-dollar text-xl"></i>
                    </div>
                    <div>
                        <h2 class="text-xl font-bold text-white">Внести Пожертвование</h2>
                        <p class="text-xs text-slate-400">Укажите ваш никнейм на сервере и сумму</p>
                    </div>
                </div>

                <form id="donation-form" onsubmit="handleDonate(event)" class="space-y-4">
                    <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
                        <!-- Nickname Input -->
                        <div>
                            <label class="block text-xs font-semibold text-slate-300 mb-1 tracking-wider uppercase">
                                <i class="fa-solid fa-user text-purple-400 mr-1"></i> Никнейм (Ник)
                            </label>
                            <input type="text" id="donor-nick" required placeholder="Ivan_Ivanov" 
                                class="w-full px-4 py-3 rounded-xl glass-input text-sm font-semibold placeholder:text-slate-600 focus:ring-1 focus:ring-purple-500">
                        </div>

                        <!-- Amount Input -->
                        <div>
                            <label class="block text-xs font-semibold text-slate-300 mb-1 tracking-wider uppercase">
                                <i class="fa-solid fa-dollar-sign text-amber-400 mr-1"></i> Сумма ($)
                            </label>
                            <input type="number" id="donor-amount" required min="1" step="any" placeholder="50000" 
                                class="w-full px-4 py-3 rounded-xl glass-input text-sm font-semibold placeholder:text-slate-600 focus:ring-1 focus:ring-purple-500">
                        </div>
                    </div>

                    <!-- Quick Amount Shortcuts -->
                    <div class="flex flex-wrap gap-2 pt-1">
                        <button type="button" onclick="setQuickAmount(10000)" class="px-3 py-1 rounded-lg text-xs font-semibold glass-input hover:border-amber-400/50 hover:text-amber-300 transition">+10,000$</button>
                        <button type="button" onclick="setQuickAmount(50000)" class="px-3 py-1 rounded-lg text-xs font-semibold glass-input hover:border-amber-400/50 hover:text-amber-300 transition">+50,000$</button>
                        <button type="button" onclick="setQuickAmount(100000)" class="px-3 py-1 rounded-lg text-xs font-semibold glass-input hover:border-amber-400/50 hover:text-amber-300 transition">+100,000$</button>
                        <button type="button" onclick="setQuickAmount(500000)" class="px-3 py-1 rounded-lg text-xs font-semibold glass-input hover:border-amber-400/50 hover:text-amber-300 transition">+500,000$</button>
                        <button type="button" onclick="setQuickAmount(1000000)" class="px-3 py-1 rounded-lg text-xs font-semibold glass-input hover:border-amber-400/50 hover:text-amber-300 transition">+1,000,000$</button>
                    </div>

                    <!-- Comment Input -->
                    <div>
                        <label class="block text-xs font-semibold text-slate-300 mb-1 tracking-wider uppercase">
                            <i class="fa-solid fa-comment-dots text-purple-400 mr-1"></i> Сообщение / Пожелание (Необязательно)
                        </label>
                        <input type="text" id="donor-comment" placeholder="На новый семейный дом!" 
                            class="w-full px-4 py-3 rounded-xl glass-input text-sm placeholder:text-slate-600">
                    </div>

                    <!-- Submit Button -->
                    <button type="submit" class="w-full py-4 rounded-xl bg-gradient-to-r from-purple-600 via-purple-500 to-amber-500 hover:from-purple-500 hover:to-amber-400 text-white font-extrabold uppercase tracking-wider text-sm shadow-lg shadow-purple-600/30 transition duration-300 transform active:scale-[0.99] flex items-center justify-center gap-2">
                        <i class="fa-solid fa-paper-plane"></i> Скинуть Денег
                    </button>
                </form>
            </div>

            <!-- Leaderboard / History Log -->
            <div class="glass-panel rounded-3xl p-6 flex flex-col flex-grow">
                
                <!-- Filter Tabs & Title -->
                <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-4 mb-6">
                    <div>
                        <h2 class="text-xl font-bold text-white flex items-center gap-2">
                            <i class="fa-solid fa-list-ol text-amber-400"></i> История Пополнений
                        </h2>
                        <p class="text-xs text-slate-400">Список всех участников сбора</p>
                    </div>

                    <!-- Sorting controls -->
                    <div class="flex p-1 bg-slate-950/60 rounded-xl border border-purple-900/40 text-xs self-start sm:self-auto">
                        <button id="sort-recent-btn" onclick="setSortMode('recent')" class="px-3 py-1.5 rounded-lg font-semibold text-white bg-purple-600 transition">
                            Последние
                        </button>
                        <button id="sort-top-btn" onclick="setSortMode('top')" class="px-3 py-1.5 rounded-lg font-semibold text-slate-400 hover:text-white transition">
                            Топ Топ-Скинувших
                        </button>
                    </div>
                </div>

                <!-- List Output -->
                <div id="donations-list" class="space-y-3 max-h-[380px] overflow-y-auto pr-2">
                    <!-- Dynamic Items will be rendered here -->
                </div>

            </div>

        </section>

    </main>

    <!-- Footer -->
    <footer class="w-full border-t border-purple-900/30 glass-panel py-4 mt-8">
        <div class="max-w-7xl mx-auto px-4 text-center text-xs text-slate-500">
            <p>Стилизовано под <span class="text-purple-400 font-semibold">Majestic RP</span> • Сохранение данных работает локально в вашем браузере (LocalStorage).</p>
        </div>
    </footer>

    <!-- GitHub Pages Guide Modal -->
    <div id="github-modal" class="fixed inset-0 bg-black/80 backdrop-blur-md z-50 hidden flex items-center justify-center p-4">
        <div class="glass-panel max-w-2xl w-full rounded-3xl p-6 sm:p-8 relative border border-purple-500/40 shadow-2xl">
            <button onclick="toggleGithubModal()" class="absolute top-5 right-5 text-slate-400 hover:text-white text-xl">
                <i class="fa-solid fa-xmark"></i>
            </button>

            <div class="flex items-center gap-3 mb-4">
                <div class="p-3 bg-purple-600/20 border border-purple-500/30 rounded-2xl text-purple-300">
                    <i class="fa-brands fa-github text-2xl"></i>
                </div>
                <div>
                    <h3 class="text-xl font-bold text-white">Инструкция: Публикация на GitHub Pages</h3>
                    <p class="text-xs text-purple-300">Бесплатный хостинг вашего сайта за 2 минуты</p>
                </div>
            </div>

            <div class="space-y-4 text-xs sm:text-sm text-slate-300 leading-relaxed max-h-[60vh] overflow-y-auto pr-2">
                <div class="p-3 bg-slate-900/80 rounded-xl border border-purple-900/40">
                    <strong class="text-amber-400 block mb-1">Шаг 1: Создайте файл index.html</strong>
                    <p>Скопируйте весь код этой страницы и сохраните его в файл с именем <code class="bg-black/50 px-2 py-0.5 rounded text-purple-300">index.html</code> на вашем компьютере.</p>
                </div>

                <div class="p-3 bg-slate-900/80 rounded-xl border border-purple-900/40">
                    <strong class="text-amber-400 block mb-1">Шаг 2: Создайте репозиторий на GitHub</strong>
                    <p>Зайдите на <a href="https://github.com" target="_blank" class="text-purple-400 underline">GitHub.com</a>, нажмите <strong>New Repository</strong>. Назовите его, например, <code class="bg-black/50 px-2 py-0.5 rounded text-purple-300">majestic-goal</code> и выберите <strong>Public</strong>.</p>
                </div>

                <div class="p-3 bg-slate-900/80 rounded-xl border border-purple-900/40">
                    <strong class="text-amber-400 block mb-1">Шаг 3: Загрузите index.html</strong>
                    <p>В созданном репозитории нажмите <strong>uploading an existing file</strong> и перетащите ваш файл <code class="bg-black/50 px-2 py-0.5 rounded text-purple-300">index.html</code>. Нажмите <strong>Commit changes</strong>.</p>
                </div>

                <div class="p-3 bg-slate-900/80 rounded-xl border border-purple-900/40">
                    <strong class="text-amber-400 block mb-1">Шаг 4: Включите GitHub Pages</strong>
                    <p>Перейдите в <strong>Settings</strong> вашего репозитория ➔ вкладка <strong>Pages</strong> (слева). В разделе <em>Build and deployment / Branch</em> выберите ветку <code class="bg-black/50 px-2 py-0.5 rounded text-purple-300">main</code> (или <code class="bg-black/50 px-2 py-0.5 rounded text-purple-300">master</code>) и нажмите <strong>Save</strong>.</p>
                </div>

                <div class="p-3 bg-amber-500/10 rounded-xl border border-amber-500/30 text-amber-200">
                    <i class="fa-solid fa-circle-info mr-1"></i> Готово! Через 1-2 минуты ваш сайт станет доступен по адресу: <br>
                    <code class="text-xs bg-black/40 px-2 py-1 rounded mt-1 inline-block text-amber-300">https://твой-ник.github.io/majestic-goal/</code>
                </div>
            </div>

            <button onclick="toggleGithubModal()" class="w-full mt-6 py-3 rounded-xl bg-purple-600 hover:bg-purple-500 text-white font-bold text-xs uppercase tracking-wider">
                Понятно, закрыть
            </button>
        </div>
    </div>

    <!-- Application Logic Script -->
    <script>
        // Constants
        const TARGET_AMOUNT = 8000000; // 8 Million Target
        const STORAGE_KEY = 'majestic_rp_donations_data_v2';

        // State variables
        let donations = [];
        let currentSortMode = 'recent'; // 'recent' or 'top'

        // Load Initial Data on Startup
        window.addEventListener('DOMContentLoaded', () => {
            loadStoredData();
            updateUI();
        });

        // Load from LocalStorage or initialize default sample data
        function loadStoredData() {
            const saved = localStorage.getItem(STORAGE_KEY);
            if (saved) {
                try {
                    donations = JSON.parse(saved);
                } catch (e) {
                    console.error("Ошибка чтения LocalStorage:", e);
                    donations = getInitialData();
                }
            } else {
                donations = getInitialData();
                saveToLocalStorage();
            }
        }

        // Initial default donations (Only requested entries)
        function getInitialData() {
            return [
                { id: 1, nick: 'Ева Елфи', amount: 0, comment: 'Первоначальный внос', date: new Date().toISOString() },
                { id: 2, nick: 'Дженни Китти', amount: 0, comment: 'Первоначальный внос', date: new Date().toISOString() }
            ];
        }

        // Save current donations state to LocalStorage
        function saveToLocalStorage() {
            localStorage.setItem(STORAGE_KEY, JSON.stringify(donations));
        }

        // Add New Donation
        function handleDonate(event) {
            event.preventDefault();

            const nickInput = document.getElementById('donor-nick');
            const amountInput = document.getElementById('donor-amount');
            const commentInput = document.getElementById('donor-comment');

            const nick = nickInput.value.trim();
            const amount = parseFloat(amountInput.value);
            const comment = commentInput.value.trim();

            if (!nick || isNaN(amount) || amount <= 0) {
                alert('Пожалуйста, введите корректный ник и сумму!');
                return;
            }

            const newContribution = {
                id: Date.now(),
                nick: nick,
                amount: amount,
                comment: comment || 'Без сообщения',
                date: new Date().toISOString()
            };

            donations.unshift(newContribution);
            saveToLocalStorage();
            updateUI();

            // Reset Form fields
            amountInput.value = '';
            commentInput.value = '';
        }

        // Set quick amount helper
        function setQuickAmount(val) {
            document.getElementById('donor-amount').value = val;
        }

        // Calculate total raised amount
        function getTotalRaised() {
            return donations.reduce((sum, item) => sum + Number(item.amount), 0);
        }

        // Update UI Elements
        function updateUI() {
            const total = getTotalRaised();
            const percentage = Math.min((total / TARGET_AMOUNT) * 100, 100).toFixed(1);

            // Text Updates
            document.getElementById('raised-text').innerText = formatCurrency(total);
            document.getElementById('percent-text').innerText = `${percentage}%`;
            document.getElementById('jar-percent').innerText = `${percentage}%`;

            // Progress Bar Update
            document.getElementById('progress-bar').style.width = `${Math.min(percentage, 100)}%`;

            // Jar Liquid Fill Update
            document.getElementById('jar-liquid').style.height = `${Math.min(percentage, 100)}%`;

            // Render Leaderboard
            renderLeaderboard();
        }

        // Render Leaderboard / History
        function renderLeaderboard() {
            const listContainer = document.getElementById('donations-list');
            listContainer.innerHTML = '';

            if (donations.length === 0) {
                listContainer.innerHTML = `
                    <div class="text-center py-8 text-slate-500 text-xs">
                        Пока нет пожертвований. Будьте первым!
                    </div>
                `;
                return;
            }

            // Copy array for sorting
            let sortedList = [...donations];

            if (currentSortMode === 'top') {
                sortedList.sort((a, b) => b.amount - a.amount);
            } else {
                sortedList.sort((a, b) => new Date(b.date) - new Date(a.date));
            }

            sortedList.forEach((item, index) => {
                const dateObj = new Date(item.date);
                const formattedDate = dateObj.toLocaleDateString('ru-RU', { hour: '2-digit', minute: '2-digit' });

                // Crown badge for Top 3 in 'top' mode
                let badgeHTML = '';
                if (currentSortMode === 'top') {
                    if (index === 0) badgeHTML = '<span class="text-amber-400 font-bold text-sm"><i class="fa-solid fa-crown"></i> #1</span>';
                    else if (index === 1) badgeHTML = '<span class="text-slate-300 font-bold text-sm"><i class="fa-solid fa-medal"></i> #2</span>';
                    else if (index === 2) badgeHTML = '<span class="text-amber-600 font-bold text-sm"><i class="fa-solid fa-award"></i> #3</span>';
                    else badgeHTML = `<span class="text-slate-500 text-xs font-semibold">#${index + 1}</span>`;
                }

                const card = document.createElement('div');
                card.className = 'p-3.5 rounded-2xl bg-slate-900/60 border border-purple-900/30 hover:border-purple-500/40 transition duration-300 flex items-center justify-between gap-3';

                card.innerHTML = `
                    <div class="flex items-center gap-3 overflow-hidden">
                        <div class="w-10 h-10 rounded-xl bg-purple-950/80 border border-purple-500/30 flex items-center justify-center text-purple-300 shrink-0 font-black">
                            ${item.nick.charAt(0).toUpperCase()}
                        </div>
                        <div class="truncate">
                            <div class="flex items-center gap-2">
                                <span class="font-bold text-sm text-white truncate">${escapeHTML(item.nick)}</span>
                                ${badgeHTML}
                            </div>
                            <p class="text-xs text-slate-400 truncate mt-0.5">${escapeHTML(item.comment)}</p>
                        </div>
                    </div>

                    <div class="text-right shrink-0">
                        <div class="font-extrabold text-sm text-amber-400">
                            +${formatCurrency(item.amount)}
                        </div>
                        <div class="text-[10px] text-slate-500">
                            ${formattedDate}
                        </div>
                    </div>
                `;

                listContainer.appendChild(card);
            });
        }

        // Sorting Switch
        function setSortMode(mode) {
            currentSortMode = mode;
            const recentBtn = document.getElementById('sort-recent-btn');
            const topBtn = document.getElementById('sort-top-btn');

            if (mode === 'recent') {
                recentBtn.className = 'px-3 py-1.5 rounded-lg font-semibold text-white bg-purple-600 transition';
                topBtn.className = 'px-3 py-1.5 rounded-lg font-semibold text-slate-400 hover:text-white transition';
            } else {
                topBtn.className = 'px-3 py-1.5 rounded-lg font-semibold text-white bg-purple-600 transition';
                recentBtn.className = 'px-3 py-1.5 rounded-lg font-semibold text-slate-400 hover:text-white transition';
            }

            renderLeaderboard();
        }

        // Reset Data Prompt
        function resetDataPrompt() {
            if (confirm('Вы уверены, что хотите сбросить все пожертвования и восстановить начальные данные?')) {
                donations = getInitialData();
                saveToLocalStorage();
                updateUI();
            }
        }

        // Helper: Format Number into $ Currency
        function formatCurrency(val) {
            return '$' + Number(val).toLocaleString('en-US');
        }

        // Helper: Escape HTML to prevent XSS
        function escapeHTML(str) {
            return str.replace(/[&<>'"]/g, 
                tag => ({ '&': '&amp;', '<': '&lt;', '>': '&gt;', "'": '&#39;', '"': '&quot;' }[tag] || tag)
