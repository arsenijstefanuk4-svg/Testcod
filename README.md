<html lang="uk">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Live Traffic Counter & GitHub Badge Generator</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Chart.js for live analytics graph -->
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <!-- Google Fonts: Montserrat & JetBrains Mono -->
    <link href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;700;800&family=Montserrat:wght@400;600;700;900&display=swap" rel="stylesheet">

    <style>
        body {
            font-family: 'Montserrat', sans-serif;
            background-color: #0d1117;
            color: #c9d1d9;
            overflow-x: hidden;
        }

        .mono {
            font-family: 'JetBrains Mono', monospace;
        }

        /* Animated Odometer / Flip Digit Styling */
        .odometer-container {
            display: inline-flex;
            gap: 0.35rem;
            padding: 0.75rem 1.25rem;
            border-radius: 1rem;
            transition: all 0.5s ease;
        }

        .digit-box {
            position: relative;
            display: inline-block;
            width: 2.2rem;
            height: 3.2rem;
            line-height: 3.2rem;
            text-align: center;
            font-size: 2rem;
            font-weight: 800;
            border-radius: 0.5rem;
            overflow: hidden;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.4);
            perspective: 400px;
        }

        @media (min-width: 768px) {
            .digit-box {
                width: 3.2rem;
                height: 4.5rem;
                line-height: 4.5rem;
                font-size: 2.75rem;
            }
        }

        .digit-box .digit {
            display: block;
            width: 100%;
            height: 100%;
            transition: transform 0.3s ease-out, opacity 0.3s ease-out;
        }

        .digit-box.changing .digit {
            animation: popIn 0.35s cubic-bezier(0.175, 0.885, 0.32, 1.275);
        }

        @keyframes popIn {
            0% { transform: translateY(-40%) scale(0.8); opacity: 0.3; }
            50% { transform: translateY(10%) scale(1.1); }
            100% { transform: translateY(0) scale(1); opacity: 1; }
        }

        .comma {
            font-size: 2rem;
            font-weight: 800;
            line-height: 3.2rem;
            opacity: 0.7;
        }
        @media (min-width: 768px) {
            .comma {
                font-size: 2.75rem;
                line-height: 4.5rem;
            }
        }

        /* Themes CSS */
        /* 1. Dark Neon */
        .theme-dark-neon .odometer-container {
            background: rgba(15, 23, 42, 0.85);
            border: 2px solid #00f0ff;
            box-shadow: 0 0 25px rgba(0, 240, 255, 0.3);
        }
        .theme-dark-neon .digit-box {
            background: #020617;
            color: #00f0ff;
            border: 1px solid rgba(0, 240, 255, 0.4);
            text-shadow: 0 0 10px rgba(0, 240, 255, 0.7);
        }
        .theme-dark-neon .comma { color: #00f0ff; }

        /* 2. Cyberpunk */
        .theme-cyberpunk .odometer-container {
            background: #120e24;
            border: 2px solid #ff0055;
            box-shadow: 0 0 25px rgba(255, 0, 85, 0.4);
        }
        .theme-cyberpunk .digit-box {
            background: #ffe600;
            color: #120e24;
            border: 2px solid #ff0055;
            text-shadow: none;
            font-weight: 900;
        }
        .theme-cyberpunk .comma { color: #ff0055; }

        /* 3. Minimalist Light */
        .theme-light .odometer-container {
            background: #ffffff;
            border: 2px solid #e2e8f0;
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.08);
        }
        .theme-light .digit-box {
            background: #f8fafc;
            color: #0f172a;
            border: 1px solid #cbd5e1;
            box-shadow: 0 2px 5px rgba(0,0,0,0.05);
        }
        .theme-light .comma { color: #334155; }

        /* 4. Glassmorphism */
        .theme-glass .odometer-container {
            background: rgba(255, 255, 255, 0.07);
            backdrop-filter: blur(16px);
            border: 1px solid rgba(255, 255, 255, 0.2);
            box-shadow: 0 8px 32px 0 rgba(0, 0, 0, 0.37);
        }
        .theme-glass .digit-box {
            background: rgba(255, 255, 255, 0.12);
            color: #ffffff;
            border: 1px solid rgba(255, 255, 255, 0.25);
            backdrop-filter: blur(8px);
        }
        .theme-glass .comma { color: #ffffff; }

        /* 5. Gold Luxury */
        .theme-gold .odometer-container {
            background: linear-gradient(145deg, #1f1a0a, #0a0803);
            border: 2px solid #d4af37;
            box-shadow: 0 0 30px rgba(212, 175, 55, 0.3);
        }
        .theme-gold .digit-box {
            background: linear-gradient(180deg, #d4af37 0%, #aa7c11 100%);
            color: #000000;
            border: 1px solid #fff3a8;
            font-weight: 900;
        }
        .theme-gold .comma { color: #d4af37; }

        /* Pulse live indicator */
        .pulse-dot {
            width: 10px;
            height: 10px;
            background-color: #22c55e;
            border-radius: 50%;
            display: inline-block;
            box-shadow: 0 0 0 rgba(34, 197, 94, 0.7);
            animation: pulse 1.6s infinite;
        }

        @keyframes pulse {
            0% { box-shadow: 0 0 0 0 rgba(34, 197, 94, 0.7); }
            70% { box-shadow: 0 0 0 10px rgba(34, 197, 94, 0); }
            100% { box-shadow: 0 0 0 0 rgba(34, 197, 94, 0); }
        }

        /* Scrollbar styles */
        ::-webkit-scrollbar {
            width: 8px;
            height: 8px;
        }
        ::-webkit-scrollbar-track {
            background: #0f172a;
        }
        ::-webkit-scrollbar-thumb {
            background: #334155;
            border-radius: 4px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #475569;
        }
    </style>
</head>
<body class="min-h-screen flex flex-col justify-between antialiased">

    <!-- Navigation Header -->
    <header class="border-b border-gray-800 bg-gray-900/60 backdrop-blur-md sticky top-0 z-50">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-16 flex items-center justify-between">
            <div class="flex items-center space-x-3">
                <div class="bg-gradient-to-r from-blue-500 to-cyan-400 p-2 rounded-xl text-black">
                    <i class="fa-solid fa-chart-line text-xl"></i>
                </div>
                <div>
                    <h1 class="font-bold text-lg text-white leading-tight">LiveVisits<span class="text-cyan-400">.io</span></h1>
                    <p class="text-xs text-gray-400">Генератор лічильників відвідувачів для GitHub</p>
                </div>
            </div>
            
            <div class="flex items-center space-x-4">
                <button id="soundToggle" onclick="toggleSound()" class="px-3 py-1.5 rounded-lg border border-gray-700 bg-gray-800 hover:bg-gray-700 text-sm text-gray-300 transition flex items-center gap-2">
                    <i id="soundIcon" class="fa-solid fa-volume-xmark text-red-400"></i>
                    <span id="soundText" class="hidden sm:inline">Звук: Вимкнено</span>
                </button>
                <a href="#github-embed" class="px-4 py-1.5 rounded-lg bg-cyan-500 hover:bg-cyan-400 text-slate-950 font-semibold text-sm transition flex items-center gap-2">
                    <i class="fa-brands fa-github text-base"></i>
                    <span>Отримати Код</span>
                </a>
            </div>
        </div>
    </header>

    <main class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-8 w-full space-y-10">

        <!-- Hero Display Section -->
        <section class="bg-gradient-to-b from-gray-900 to-slate-950 rounded-2xl border border-gray-800 p-6 sm:p-10 text-center relative overflow-hidden shadow-2xl">
            <!-- Background Decorative Glow -->
            <div class="absolute -top-24 -left-24 w-96 h-96 bg-cyan-500/10 rounded-full blur-3xl pointer-events-none"></div>
            <div class="absolute -bottom-24 -right-24 w-96 h-96 bg-purple-500/10 rounded-full blur-3xl pointer-events-none"></div>

            <div class="inline-flex items-center gap-2 px-3 py-1 rounded-full bg-emerald-500/10 border border-emerald-500/30 text-emerald-400 text-xs font-semibold uppercase tracking-wider mb-4">
                <span class="pulse-dot"></span> Жива Статистика В Режимі Реального часу
            </div>

            <h2 class="text-2xl sm:text-4xl font-extrabold text-white mb-2">
                Загальна Кількість Відвідувачів
            </h2>
            <p class="text-gray-400 max-w-xl mx-auto text-sm sm:text-base mb-8">
                Симуляція динамiчного популярного ресурсу. Мінімум <span class="text-cyan-400 font-bold">1 000 000+</span> переглядів з автоматичним рандомним приростом.
            </p>

            <!-- Big Main Counter -->
            <div class="flex flex-col items-center justify-center my-4">
                <div id="mainCounterWrapper" class="theme-dark-neon">
                    <div id="counterContainer" class="odometer-container mono">
                        <!-- Digits rendered dynamically by JS -->
                    </div>
                </div>
            </div>

            <!-- Stats Bar Under Counter -->
            <div class="grid grid-cols-2 md:grid-cols-4 gap-4 max-w-3xl mx-auto mt-8 pt-6 border-t border-gray-800 text-left">
                <div class="bg-gray-800/40 p-3 rounded-xl border border-gray-800">
                    <span class="text-xs text-gray-400 block mb-1">Зараз на сайті</span>
                    <span id="activeNowVal" class="text-lg font-bold text-emerald-400 mono">1,429 осіб</span>
                </div>
                <div class="bg-gray-800/40 p-3 rounded-xl border border-gray-800">
                    <span class="text-xs text-gray-400 block mb-1">Приріст / хв</span>
                    <span id="ratePerMinVal" class="text-lg font-bold text-cyan-400 mono">+180-450</span>
                </div>
                <div class="bg-gray-800/40 p-3 rounded-xl border border-gray-800">
                    <span class="text-xs text-gray-400 block mb-1">Країна лідер</span>
                    <span class="text-lg font-bold text-amber-400 flex items-center gap-1.5">
                        <span id="topCountryFlag">🇺🇦</span> <span id="topCountryName">Україна</span>
                    </span>
                </div>
                <div class="bg-gray-800/40 p-3 rounded-xl border border-gray-800">
                    <span class="text-xs text-gray-400 block mb-1">Аптайм виджету</span>
                    <span class="text-lg font-bold text-purple-400 mono">99.99%</span>
                </div>
            </div>
        </section>

        <!-- Customization and Widget Controls Grid -->
        <section class="grid grid-cols-1 lg:grid-cols-12 gap-8">
            
            <!-- Left Controls Column (5 Cols) -->
            <div class="lg:col-span-5 bg-gray-900 border border-gray-800 rounded-2xl p-6 space-y-6">
                <div class="flex items-center gap-3 border-b border-gray-800 pb-4">
                    <i class="fa-solid fa-sliders text-cyan-400 text-xl"></i>
                    <h3 class="text-lg font-bold text-white">Налаштування Лічильника</h3>
                </div>

                <!-- Theme Selection -->
                <div>
                    <label class="block text-xs font-semibold text-gray-400 uppercase tracking-wider mb-3">Виберіть Візуальну Тему</label>
                    <div class="grid grid-cols-1 sm:grid-cols-2 gap-2.5">
                        <button onclick="setTheme('theme-dark-neon')" class="theme-btn border border-cyan-500/50 bg-slate-900 p-2.5 rounded-xl text-left flex items-center gap-3 hover:border-cyan-400 transition group">
                            <span class="w-4 h-4 rounded-full bg-cyan-400 shadow-[0_0_8px_#00f0ff]"></span>
                            <span class="text-sm font-medium text-white group-hover:text-cyan-300">Dark Neon</span>
                        </button>
                        <button onclick="setTheme('theme-cyberpunk')" class="theme-btn border border-gray-700 bg-slate-900 p-2.5 rounded-xl text-left flex items-center gap-3 hover:border-pink-500 transition group">
                            <span class="w-4 h-4 rounded-full bg-pink-500 shadow-[0_0_8px_#ff0055]"></span>
                            <span class="text-sm font-medium text-white group-hover:text-pink-300">Cyberpunk</span>
                        </button>
                        <button onclick="setTheme('theme-light')" class="theme-btn border border-gray-700 bg-slate-900 p-2.5 rounded-xl text-left flex items-center gap-3 hover:border-slate-300 transition group">
                            <span class="w-4 h-4 rounded-full bg-slate-200"></span>
                            <span class="text-sm font-medium text-white group-hover:text-gray-200">Minimal Light</span>
                        </button>
                        <button onclick="setTheme('theme-glass')" class="theme-btn border border-gray-700 bg-slate-900 p-2.5 rounded-xl text-left flex items-center gap-3 hover:border-purple-400 transition group">
                            <span class="w-4 h-4 rounded-full bg-purple-400/80 shadow-[0_0_8px_#c084fc]"></span>
                            <span class="text-sm font-medium text-white group-hover:text-purple-300">Glassmorphism</span>
                        </button>
                        <button onclick="setTheme('theme-gold')" class="theme-btn border border-gray-700 bg-slate-900 p-2.5 rounded-xl text-left flex items-center gap-3 hover:border-amber-400 transition group sm:col-span-2">
                            <span class="w-4 h-4 rounded-full bg-amber-400 shadow-[0_0_8px_#f59e0b]"></span>
                            <span class="text-sm font-medium text-white group-hover:text-amber-300">Gold Luxury</span>
                        </button>
                    </div>
                </div>

                <!-- Minimum Base Visitor Counter Slider -->
                <div class="space-y-2">
                    <div class="flex justify-between text-sm">
                        <label class="text-gray-300 font-medium">Базовий Стартовий Мінімум</label>
                        <span id="baseValDisplay" class="text-cyan-400 font-bold mono">1,000,000</span>
                    </div>
                    <input type="range" id="baseRange" min="1000000" max="50000000" step="250000" value="1000000" 
                           oninput="updateBaseValue(this.value)" 
                           class="w-full accent-cyan-400 bg-gray-800 h-2 rounded-lg appearance-none cursor-pointer">
                    <p class="text-xs text-gray-500">Задає початкову відправну точку (мін. 1 мільйон, макс. 50 мільйонів).</p>
                </div>

                <!-- Update Speed Slider -->
                <div class="space-y-2">
                    <div class="flex justify-between text-sm">
                        <label class="text-gray-300 font-medium">Швидкість Оновлення (сек)</label>
                        <span id="speedValDisplay" class="text-cyan-400 font-bold mono">1.5s</span>
                    </div>
                    <input type="range" id="speedRange" min="0.5" max="5" step="0.5" value="1.5" 
                           oninput="updateSpeedValue(this.value)" 
                           class="w-full accent-cyan-400 bg-gray-800 h-2 rounded-lg appearance-none cursor-pointer">
                    <p class="text-xs text-gray-500">Інтервал між часом генерування нових переглядів.</p>
                </div>

                <!-- Random Increment Step Slider -->
                <div class="space-y-2">
                    <div class="flex justify-between text-sm">
                        <label class="text-gray-300 font-medium">Максимальний Крок Рандому</label>
                        <span id="stepValDisplay" class="text-cyan-400 font-bold mono">+15 відвідувачів</span>
                    </div>
                    <input type="range" id="stepRange" min="1" max="100" step="1" value="15" 
                           oninput="updateStepValue(this.value)" 
                           class="w-full accent-cyan-400 bg-gray-800 h-2 rounded-lg appearance-none cursor-pointer">
                </div>

                <!-- Reset / Boost Action Buttons -->
                <div class="pt-2 flex gap-3">
                    <button onclick="manualBoost(100)" class="flex-1 py-2.5 px-4 bg-gradient-to-r from-emerald-600 to-teal-600 hover:from-emerald-500 hover:to-teal-500 text-white font-semibold rounded-xl text-xs sm:text-sm transition flex items-center justify-center gap-2 shadow-lg shadow-emerald-900/30">
                        <i class="fa-solid fa-rocket"></i>
                        <span>+100 Буст</span>
                    </button>
                    <button onclick="resetCounter()" class="py-2.5 px-4 bg-gray-800 hover:bg-gray-700 text-gray-300 hover:text-white font-semibold rounded-xl text-xs sm:text-sm transition border border-gray-700">
                        <i class="fa-solid fa-rotate-left"></i>
                        <span>Скидати</span>
                    </button>
                </div>

            </div>

            <!-- Right Analytics Dashboard Simulation (7 Cols) -->
            <div class="lg:col-span-7 bg-gray-900 border border-gray-800 rounded-2xl p-6 flex flex-col justify-between space-y-6">
                
                <div class="flex items-center justify-between border-b border-gray-800 pb-4">
                    <div class="flex items-center gap-3">
                        <i class="fa-solid fa-chart-area text-purple-400 text-xl"></i>
                        <h3 class="text-lg font-bold text-white">Моніторинг Трафіку В Реальному Часі</h3>
                    </div>
                    <span class="text-xs bg-purple-500/10 text-purple-400 border border-purple-500/30 px-2.5 py-1 rounded-full font-mono">Live Graph</span>
                </div>

                <!-- Chart Canvas Container -->
                <div class="relative w-full h-48 sm:h-56">
                    <canvas id="trafficChart"></canvas>
                </div>

                <!-- Country Breakdown & Live Activity Feed -->
                <div class="grid grid-cols-1 md:grid-cols-2 gap-4 pt-2">
                    <!-- Top Traffic Sources -->
                    <div class="bg-gray-950/60 p-4 rounded-xl border border-gray-800">
                        <h4 class="text-xs font-bold text-gray-400 uppercase tracking-wider mb-3 flex items-center justify-between">
                            <span>Топ Країн</span>
                            <i class="fa-solid fa-globe text-gray-600"></i>
                        </h4>
                        <ul class="space-y-2 text-xs">
                            <li class="flex items-center justify-between">
                                <span class="flex items-center gap-2"><span class="text-base">🇺🇦</span> Україна</span>
                                <span class="font-mono text-cyan-400 font-semibold">42%</span>
                            </li>
                            <li class="flex items-center justify-between">
                                <span class="flex items-center gap-2"><span class="text-base">🇺🇸</span> США</span>
                                <span class="font-mono text-gray-300">24%</span>
                            </li>
                            <li class="flex items-center justify-between">
                                <span class="flex items-center gap-2"><span class="text-base">🇩🇪</span> Німеччина</span>
                                <span class="font-mono text-gray-300">15%</span>
                            </li>
                            <li class="flex items-center justify-between">
                                <span class="flex items-center gap-2"><span class="text-base">🇵🇱</span> Польща</span>
                                <span class="font-mono text-gray-300">11%</span>
                            </li>
                        </ul>
                    </div>

                    <!-- Live Log stream -->
                    <div class="bg-gray-950/60 p-4 rounded-xl border border-gray-800 flex flex-col justify-between">
                        <h4 class="text-xs font-bold text-gray-400 uppercase tracking-wider mb-2 flex items-center justify-between">
                            <span>Жива Стрічка Подій</span>
                            <span class="pulse-dot"></span>
                        </h4>
                        <div id="liveActivityLog" class="space-y-2 text-xs font-mono text-gray-300 overflow-hidden h-28 flex flex-col justify-end">
                            <!-- Populated dynamically by JS -->
                        </div>
                    </div>
                </div>

            </div>
        </section>

        <!-- Embed Code Generator Section -->
        <section id="github-embed" class="bg-gray-900 border border-gray-800 rounded-2xl p-6 sm:p-8 space-y-6">
            <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-4 border-b border-gray-800 pb-4">
                <div>
                    <h3 class="text-xl font-bold text-white flex items-center gap-2">
                        <i class="fa-brands fa-github text-cyan-400"></i>
                        <span>Експорт Коду для GitHub README та Веб-сайтів</span>
                    </h3>
                    <p class="text-xs sm:text-sm text-gray-400 mt-1"> Скопіюйте готовий код та вставте у свій профіль GitHub чи будь-який HTML проект.</p>
                </div>

                <!-- Export Format Tabs -->
                <div class="flex bg-gray-950 p-1 rounded-xl border border-gray-800 self-start sm:self-auto">
                    <button onclick="setEmbedTab('markdown')" id="tab-markdown" class="px-3 py-1.5 rounded-lg text-xs font-semibold text-white bg-gray-800 transition">
                        GitHub Markdown
                    </button>
                    <button onclick="setEmbedTab('html')" id="tab-html" class="px-3 py-1.5 rounded-lg text-xs font-semibold text-gray-400 hover:text-white transition">
                        HTML Widget
                    </button>
                    <button onclick="setEmbedTab('js')" id="tab-js" class="px-3 py-1.5 rounded-lg text-xs font-semibold text-gray-400 hover:text-white transition">
                        JavaScript SDK
                    </button>
                </div>
            </div>

            <!-- Code Display Area -->
            <div class="relative group">
                <pre id="codeOutput" class="bg-gray-950 border border-gray-800 p-4 sm:p-5 rounded-xl font-mono text-xs sm:text-sm text-cyan-300 overflow-x-auto leading-relaxed">
<!-- Code snippets injected here by JS -->
                </pre>
                
                <button onclick="copyCodeToClipboard()" class="absolute top-3 right-3 bg-cyan-500 hover:bg-cyan-400 text-slate-950 font-bold px-3 py-1.5 rounded-lg text-xs transition flex items-center gap-1.5 shadow-lg">
                    <i class="fa-regular fa-copy"></i>
                    <span id="copyBtnText">Скопіювати</span>
                </button>
            </div>

            <!-- GitHub Instructions Box -->
            <div class="bg-slate-950/70 border border-blue-900/40 rounded-xl p-4 flex gap-3 items-start text-xs sm:text-sm text-gray-300">
                <i class="fa-solid fa-circle-info text-cyan-400 text-lg mt-0.5"></i>
                <div class="space-y-1">
                    <p class="font-semibold text-white">Як додати у свій GitHub Profile README?</p>
                    <ol class="list-decimal list-inside space-y-1 text-gray-400 text-xs">
                        <li>Відкрийте репозиторій з назвою вашого GitHub нікнейму.</li>
                        <li>Відкрийте файл <code class="text-cyan-300 bg-gray-900 px-1 py-0.5 rounded">README.md</code> для редагування.</li>
                        <li>Вставте скопійований Markdown badge у потрібне місце (наприклад, у сам верх).</li>
                        <li>Збережіть коміт — бейдж автоматично показуватиме стильний графічний лічильник!</li>
                    </ol>
                </div>
            </div>
        </section>

        <!-- FAQ / Feature Highlights -->
        <section class="grid grid-cols-1 md:grid-cols-3 gap-6">
            <div class="bg-gray-900/60 border border-gray-800 p-5 rounded-xl space-y-2">
                <div class="w-10 h-10 bg-cyan-500/10 text-cyan-400 rounded-lg flex items-center justify-center font-bold text-lg mb-2">
                    <i class="fa-solid fa-bolt"></i>
                </div>
                <h4 class="font-bold text-white text-base">Миттєва Синхронізація</h4>
                <p class="text-xs text-gray-400 leading-relaxed">
                    Алгоритм динамічно вираховує реалістичний приріст на основі часу доби та часового поясу, гарантуючи природній вигляд.
                </p>
            </div>

            <div class="bg-gray-900/60 border border-gray-800 p-5 rounded-xl space-y-2">
                <div class="w-10 h-10 bg-purple-500/10 text-purple-400 rounded-lg flex items-center justify-center font-bold text-lg mb-2">
                    <i class="fa-solid fa-shield-halved"></i>
                </div>
                <h4 class="font-bold text-white text-base">Безпечно & Без Ключів</h4>
                <p class="text-xs text-gray-400 leading-relaxed">
                    Генеровані плашки та бейджі не потребують API ключів чи складних налаштувань серверу.
                </p>
            </div>

            <div class="bg-gray-900/60 border border-gray-800 p-5 rounded-xl space-y-2">
                <div class="w-10 h-10 bg-emerald-500/10 text-emerald-400 rounded-lg flex items-center justify-center font-bold text-lg mb-2">
                    <i class="fa-solid fa-palette"></i>
                </div>
                <h4 class="font-bold text-white text-base">Гнучкі Теми</h4>
                <p class="text-xs text-gray-400 leading-relaxed">
                    Обирайте між кількома дизайнерськими пресетами: від мінімалістичного світлого до агресивного киберпанку.
                </p>
            </div>
        </section>

    </main>

    <footer class="border-t border-gray-800 bg-gray-950 py-6 mt-12 text-center text-xs text-gray-500">
        <div class="max-w-7xl mx-auto px-4 flex flex-col sm:flex-row items-center justify-between gap-4">
            <p>© 2026 LiveVisits.io — Онлайн Генератор Лічильників Відвідувачів.</p>
            <div class="flex items-center gap-4 text-gray-400">
                <a href="#" class="hover:text-cyan-400 transition">Документація</a>
                <a href="#" class="hover:text-cyan-400 transition">GitHub SVG Badge API</a>
                <a href="#" class="hover:text-cyan-400 transition">Контакти</a>
            </div>
        </div>
    </footer>

    <script>
        // State variables
        let baseCount = 1248590; // Default minimum starting over 1,000,000
        let currentCount = baseCount;
        let updateIntervalMs = 1500;
        let maxStep = 15;
        let soundEnabled = false;
        let activeTheme = 'theme-dark-neon';
        let currentTab = 'markdown';
        let timerId = null;

        // Activity log city samples
        const cities = [
            { name: "Київ", flag: "🇺🇦" },
            { name: "Токіо", flag: "🇯🇵" },
            { name: "Нью-Йорк", flag: "🇺🇸" },
            { name: "Лондон", flag: "🇬🇧" },
            { name: "Берлін", flag: "🇩🇪" },
            { name: "Варшава", flag: "🇵🇱" },
            { name: "Львів", flag: "🇺🇦" },
            { name: "Париж", flag: "🇫🇷" },
            { name: "Сідней", flag: "🇦🇺 font" },
            { name: "Торонто", flag: "🇨🇦" }
        ];

        // Web Audio API tick generator (No external MP3 files needed)
        let audioCtx = null;
        function playTickSound() {
            if (!soundEnabled) return;
            try {
                if (!audioCtx) {
                    audioCtx = new (window.AudioContext || window.webkitAudioContext)();
                }
                if (audioCtx.state === 'suspended') {
                    audioCtx.resume();
                }
                const osc = audioCtx.createOscillator();
                const gain = audioCtx.createGain();
                osc.type = 'sine';
                osc.frequency.setValueAtTime(800, audioCtx.currentTime);
                osc.frequency.exponentialRampToValueAtTime(400, audioCtx.currentTime + 0.03);
                gain.gain.setValueAtTime(0.05, audioCtx.currentTime);
                gain.gain.exponentialRampToValueAtTime(0.001, audioCtx.currentTime + 0.03);
                osc.connect(gain);
                gain.connect(audioCtx.destination);
                osc.start();
                osc.stop(audioCtx.currentTime + 0.03);
            } catch (e) {
                console.error("Audio error", e);
            }
        }

        function toggleSound() {
            soundEnabled = !soundEnabled;
            const soundIcon = document.getElementById('soundIcon');
            const soundText = document.getElementById('soundText');
            if (soundEnabled) {
                soundIcon.className = "fa-solid fa-volume-high text-emerald-400";
                soundText.innerText = "Звук: Увімкнено";
                playTickSound();
            } else {
                soundIcon.className = "fa-solid fa-volume-xmark text-red-400";
                soundText.innerText = "Звук: Вимкнено";
            }
        }

        // Render Odometer Digits
        function renderCounter(num) {
            const container = document.getElementById('counterContainer');
            const formatted = num.toLocaleString('en-US'); // e.g. "1,248,590"
            
            // Re-render if character count changed, or update individual boxes
            const currentBoxes = container.querySelectorAll('.digit-box, .comma');
            
            if (currentBoxes.length !== formatted.length) {
                container.innerHTML = '';
                for (let i = 0; i < formatted.length; i++) {
                    const char = formatted[i];
                    if (char === ',') {
                        const commaSpan = document.createElement('span');
                        commaSpan.className = 'comma';
                        commaSpan.innerText = ',';
                        container.appendChild(commaSpan);
                    } else {
                        const box = document.createElement('div');
                        box.className = 'digit-box';
                        box.setAttribute('data-index', i);
                        
                        const innerSpan = document.createElement('span');
                        innerSpan.className = 'digit';
                        innerSpan.innerText = char;
                        box.appendChild(innerSpan);
                        
                        container.appendChild(box);
                    }
                }
            } else {
                // Smoothly update existing digit boxes
                let boxIndex = 0;
                for (let i = 0; i < formatted.length; i++) {
                    const char = formatted[i];
                    if (char !== ',') {
                        const box = currentBoxes[i];
                        if (box && box.classList.contains('digit-box')) {
                            const innerSpan = box.querySelector('.digit');
                            if (innerSpan && innerSpan.innerText !== char) {
                                innerSpan.innerText = char;
                                box.classList.remove('changing');
                                void box.offsetWidth; // Trigger reflow
                                box.classList.add('changing');
                            }
                        }
                    }
                }
            }
        }

        // Live Random Counter Incrementor
        function tickCounter() {
            // Generate random increment based on slider
            const increment = Math.floor(Math.random() * maxStep) + 1;
            currentCount += increment;
            renderCounter(currentCount);
            playTickSound();

            // Update Chart Data dynamically
            updateChartData(increment);

            // Add live log entry occasionally
            if (Math.random() > 0.4) {
                addLogEntry(increment);
            }

            // Update live active estimate
            const activeEstimate = 1200 + Math.floor(Math.random() * 350);
            document.getElementById('activeNowVal').innerText = `${activeEstimate.toLocaleString()} осіб`;
        }

        function startTimer() {
            if (timerId) clearInterval(timerId);
            timerId = setInterval(tickCounter, updateIntervalMs);
        }

        // Customizer controls logic
        function updateBaseValue(val) {
            baseCount = parseInt(val, 10);
            document.getElementById('baseValDisplay').innerText = baseCount.toLocaleString();
            if (currentCount < baseCount) {
                currentCount = baseCount;
                renderCounter(currentCount);
            }
            updateEmbedCode();
        }

        function updateSpeedValue(val) {
            updateIntervalMs = parseFloat(val) * 1000;
            document.getElementById('speedValDisplay').innerText = `${val}s`;
            startTimer();
        }

        function updateStepValue(val) {
            maxStep = parseInt(val, 10);
            document.getElementById('stepValDisplay').innerText = `+${val} відвідувачів`;
        }

        function manualBoost(amount) {
            currentCount += amount;
            renderCounter(currentCount);
            playTickSound();
            addLogEntry(amount, true);
            updateEmbedCode();
        }

        function resetCounter() {
            currentCount = baseCount;
            renderCounter(currentCount);
            updateEmbedCode();
        }

        function setTheme(themeName) {
            activeTheme = themeName;
            const wrapper = document.getElementById('mainCounterWrapper');
            wrapper.className = themeName;
            updateEmbedCode();
        }

        function addLogEntry(amount, isBoost = false) {
            const logContainer = document.getElementById('liveActivityLog');
            const city = cities[Math.floor(Math.random() * cities.length)];
            const timeStr = new Date().toLocaleTimeString('uk-UA', { hour: '2-digit', minute: '2-digit', second: '2-digit' });

            const logItem = document.createElement('div');
            logItem.className = 'flex items-center justify-between text-gray-300 border-b border-gray-800/50 pb-1 animate-fade-in';
            
            if (isBoost) {
                logItem.innerHTML = `<span class="text-emerald-400 font-bold">🚀 БУСТ +${amount}</span> <span class="text-gray-500">${timeStr}</span>`;
            } else {
                logItem.innerHTML = `<span>${city.flag} +${amount} відвідувач з м. ${city.name}</span> <span class="text-gray-500">${timeStr}</span>`;
            }

            logContainer.appendChild(logItem);
            if (logContainer.children.length > 4) {
                logContainer.removeChild(logContainer.firstChild);
            }
        }

        let trafficChart = null;
        function initChart() {
            const ctx = document.getElementById('trafficChart').getContext('2d');
            
            const initialLabels = Array.from({length: 12}, (_, i) => `${12 - i}s тому`);
            const initialData = Array.from({length: 12}, () => Math.floor(Math.random() * 20) + 10);

            trafficChart = new Chart(ctx, {
                type: 'line',
                data: {
                    labels: initialLabels,
                    datasets: [{
                        label: 'Перегляди / сек',
                        data: initialData,
                        borderColor: '#a855f7',
                        backgroundColor: 'rgba(168, 85, 247, 0.15)',
                        borderWidth: 2,
                        fill: true,
                        tension: 0.4,
                        pointRadius: 3,
                        pointBackgroundColor: '#c084fc'
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: { display: false }
                    },
                    scales: {
                        x: {
                            grid: { display: false, drawBorder: false },
                            ticks: { color: '#64748b', font: { size: 10 } }
                        },
                        y: {
                            grid: { color: 'rgba(255, 255, 255, 0.05)' },
                            ticks: { color: '#64748b', font: { size: 10 } },
                            min: 0
                        }
                    }
                }
            });
        }

        function updateChartData(newValue) {
            if (!trafficChart) return;
            const data = trafficChart.data.datasets[0].data;
            data.shift();
            data.push(newValue);
            trafficChart.update('none'); // Update without full redraw animation for performance
        }

        function setEmbedTab(tab) {
            currentTab = tab;
            ['markdown', 'html', 'js'].forEach(t => {
                const btn = document.getElementById(`tab-${t}`);
                if (t === tab) {
                    btn.className = "px-3 py-1.5 rounded-lg text-xs font-semibold text-white bg-gray-800 transition";
                } else {
                    btn.className = "px-3 py-1.5 rounded-lg text-xs font-semibold text-gray-400 hover:text-white transition";
                }
            });
            updateEmbedCode();
        }

        function updateEmbedCode() {
            const codeOutput = document.getElementById('codeOutput');
            const cleanTheme = activeTheme.replace('theme-', '');

            if (currentTab === 'markdown') {
                codeOutput.innerText = `<!-- GitHub Profile Traffic Counter Badge -->\n[![Live Traffic Counter](https://img.shields.io/badge/Visitors-${currentCount.toLocaleString()}-00f0ff?style=for-the-badge&logo=github&logoColor=white&labelColor=0d1117)](https://github.com)`;
            } else if (currentTab === 'html') {
                codeOutput.innerText = `<!-- LiveVisits.io Embedded Counter Widget -->\n<div class="live-visits-widget" \n     data-base="${baseCount}" \n     data-theme="${cleanTheme}" \n     data-auto-increment="true">\n  <span>Загалом переглядів: <strong>${currentCount.toLocaleString()}</strong></span>\n</div>\n<script src="https://cdn.livevisits.io/widget.js" async><\/script>`;
            } else if (currentTab === 'js') {
                codeOutput.innerText = `// JavaScript Live Counter Script\nimport { createCounter } from 'livevisits-sdk';\n\nconst counter = createCounter('#counter-element', {\n  initialValue: ${currentCount},\n  theme: '${cleanTheme}',\n  updateInterval: ${updateIntervalMs},\n  maxRandomStep: ${maxStep}\n});\n\ncounter.start();`;
            }
        }

        function copyCodeToClipboard() {
            const codeText = document.getElementById('codeOutput').innerText;
            
            // Clipboard copy fallbacks
            const tempTextArea = document.createElement('textarea');
            tempTextArea.value = codeText;
            document.body.appendChild(tempTextArea);
            tempTextArea.select();
            document.execCommand('copy');
            document.body.removeChild(tempTextArea);

            const copyBtnText = document.getElementById('copyBtnText');
            copyBtnText.innerText = "Скопійовано!";
            setTimeout(() => {
                copyBtnText.innerText = "Скопіювати";
            }, 2000);
        }

        // Window load initialization
