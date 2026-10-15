<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>バスケットボール総合サポートツール</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- FontAwesome -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Google Fonts: Inter & Orbitron -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700;800;900&family=Orbitron:wght@700;900&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #f8fafc;
            color: #0f172a;
            -webkit-tap-highlight-color: transparent;
        }
        .digital-font {
            font-family: 'Orbitron', monospace;
            font-variant-numeric: tabular-nums;
            letter-spacing: 0.05em;
        }
        canvas {
            touch-action: none;
        }
        .court-bg {
            background-color: #e29d52;
            background-image: radial-gradient(#eca95f 3px, transparent 3px);
            background-size: 16px 16px;
        }
    </style>
</head>
<body class="min-h-screen flex flex-col justify-between bg-slate-100 text-slate-800">

    <header class="bg-white border-b border-slate-200 p-3 shadow-sm sticky top-0 z-50">
        <div class="max-w-7xl mx-auto flex flex-col sm:flex-row items-center justify-between gap-2.5">
            <div class="flex items-center gap-2.5 w-full sm:w-auto justify-between sm:justify-start">
                <div class="flex items-center gap-2">
                    <div class="bg-orange-500 text-white p-2 rounded-xl text-lg font-bold shadow-md shadow-orange-500/20">
                        <i class="fa-solid fa-basketball"></i>
                    </div>
                    <div>
                        <h1 class="text-base sm:text-lg font-extrabold text-slate-900 tracking-wide">バスケットボール総合ツール</h1>
                        <p class="text-[11px] text-slate-500 font-medium">タイマー / 24秒計 / スコア / 作戦盤</p>
                    </div>
                </div>
            </div>
            
            <!-- Mode Switch Tabs -->
            <div class="flex bg-slate-100 p-1 rounded-xl gap-1 border border-slate-200 text-xs sm:text-sm font-bold w-full sm:w-auto justify-center">
                <button onclick="switchTab('timer_score')" id="tab-timer_score" class="flex-1 sm:flex-initial px-4 py-2 rounded-lg transition-all text-orange-600 bg-white shadow-sm border border-slate-200">
                    <i class="fa-solid fa-stopwatch mr-1"></i> タイマー＆スコア
                </button>
                <button onclick="switchTab('board')" id="tab-board" class="flex-1 sm:flex-initial px-4 py-2 rounded-lg transition-all text-slate-600 hover:text-slate-900">
                    <i class="fa-solid fa-chalkboard-user mr-1"></i> 作戦盤
                </button>
            </div>
        </div>
    </header>

    <main class="flex-1 max-w-7xl w-full mx-auto p-2.5 sm:p-5 flex flex-col justify-stretch">

        <!-- SECTION 1: TIMER & SCOREBOARD -->
        <section id="sec-timer_score" class="grid grid-cols-1 lg:grid-cols-12 gap-4">

            <!-- LEFT PANEL: Game Clock & Shot Clock -->
            <div class="lg:col-span-6 bg-white border border-slate-200 rounded-3xl p-4 sm:p-6 shadow-sm flex flex-col justify-between space-y-4">
                <div>
                    <div class="flex justify-between items-center mb-2">
                        <span class="text-xs font-bold text-slate-500 uppercase tracking-wider bg-slate-100 px-3 py-1 rounded-full border border-slate-200">
                            <i class="fa-solid fa-clock mr-1 text-orange-500"></i> メインタイマー
                        </span>
                        <span id="period-display" class="text-xs font-extrabold text-orange-600 bg-orange-50 px-3 py-1 rounded-full border border-orange-200">
                            第 1 クォーター (1Q)
                        </span>
                    </div>

                    <!-- Main Game Clock -->
                    <div class="bg-slate-50 border-2 border-slate-200 rounded-2xl py-3 px-2 text-center my-2 shadow-inner">
                        <div id="game-clock-display" class="text-5xl sm:text-6xl font-black text-orange-600 digital-font tracking-wider leading-none py-1">
                            10:00
                        </div>
                    </div>

                    <!-- Quick Preset Buttons -->
                    <div class="grid grid-cols-4 gap-1.5 my-2.5">
                        <button onclick="setClockPreset(600)" class="py-2 bg-slate-100 hover:bg-slate-200 text-slate-700 rounded-xl text-xs font-bold transition-all border border-slate-200">10分</button>
                        <button onclick="setClockPreset(480)" class="py-2 bg-slate-100 hover:bg-slate-200 text-slate-700 rounded-xl text-xs font-bold transition-all border border-slate-200">8分</button>
                        <button onclick="setClockPreset(300)" class="py-2 bg-slate-100 hover:bg-slate-200 text-slate-700 rounded-xl text-xs font-bold transition-all border border-slate-200">5分</button>
                        <button onclick="setClockPreset(120)" class="py-2 bg-slate-100 hover:bg-slate-200 text-slate-700 rounded-xl text-xs font-bold transition-all border border-slate-200">2分</button>
                    </div>

                    <!-- Shot Clock Section -->
                    <div class="bg-white border border-slate-200 rounded-2xl p-3.5 my-2.5">
                        <div class="flex items-center justify-between gap-2 mb-2">
                            <span class="text-xs font-bold text-slate-500 uppercase tracking-wider">24秒ショットクロック</span>
                            <div class="flex gap-1.5">
                                <button onclick="resetShotClock(24)" class="px-2.5 py-1 bg-orange-500 hover:bg-orange-600 text-white rounded-lg text-xs font-bold shadow-sm">24秒</button>
                                <button onclick="resetShotClock(14)" class="px-2.5 py-1 bg-orange-500 hover:bg-orange-600 text-white rounded-lg text-xs font-bold shadow-sm">14秒</button>
                                <button id="btn-shotclock-toggle" onclick="toggleShotClockOnly()" class="px-2.5 py-1 bg-slate-200 hover:bg-slate-300 text-slate-700 rounded-lg text-xs font-bold">
                                    <i class="fa-solid fa-pause"></i>
                                </button>
                            </div>
                        </div>
                        <div class="bg-slate-50 border-2 border-slate-200 rounded-xl py-2 px-2 text-center shadow-inner">
                            <div id="shot-clock-display" class="text-4xl sm:text-5xl font-black text-red-600 digital-font leading-none tracking-wider">
                                24
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Main Clock Action Controls -->
                <div class="flex gap-2.5 pt-1">
                    <button id="btn-master-start" onclick="toggleMasterTimer()" class="flex-1 py-3.5 bg-orange-500 hover:bg-orange-600 text-white text-base sm:text-lg font-extrabold rounded-2xl shadow-lg shadow-orange-500/20 transition-all flex items-center justify-center gap-2">
                        <i class="fa-solid fa-play"></i> スタート
                    </button>
                    <button onclick="resetMasterTimer()" class="px-5 py-3.5 bg-slate-100 hover:bg-slate-200 text-slate-700 font-bold rounded-2xl transition-all border border-slate-200">
                        <i class="fa-solid fa-rotate-right"></i>
                    </button>
                </div>
            </div>

            <!-- RIGHT PANEL: Scoreboard -->
            <div class="lg:col-span-6 bg-white border border-slate-200 rounded-3xl p-4 sm:p-6 shadow-sm flex flex-col justify-between space-y-4">
                <div>
                    <div class="flex justify-between items-center mb-3">
                        <span class="text-xs font-bold text-slate-500 uppercase tracking-wider bg-slate-100 px-3 py-1 rounded-full border border-slate-200">
                            <i class="fa-solid fa-trophy mr-1 text-orange-500"></i> スコアボード
                        </span>
                        <button onclick="resetScores()" class="text-xs text-slate-600 hover:text-slate-900 bg-slate-100 hover:bg-slate-200 px-3 py-1 rounded-lg border border-slate-200 font-semibold">
                            <i class="fa-solid fa-rotate-right mr-1"></i> リセット
                        </button>
                    </div>

                    <!-- Score Displays Row -->
                    <div class="grid grid-cols-2 gap-3 my-2">
                        <!-- HOME TEAM -->
                        <div class="bg-slate-50 border-2 border-slate-200 rounded-2xl p-3 sm:p-4 text-center flex flex-col justify-between space-y-2.5 shadow-inner">
                            <input type="text" value="HOME" class="w-full bg-transparent text-center font-black text-slate-700 text-sm sm:text-base uppercase tracking-wider outline-none border-b border-slate-300 pb-1">
                            <div class="bg-white border-2 border-slate-200 rounded-xl py-2 shadow-inner">
                                <div id="score-home" class="text-4xl sm:text-5xl font-black text-orange-600 digital-font py-1 tracking-wider">0</div>
                            </div>
                            <div class="grid grid-cols-2 gap-1.5">
                                <button onclick="changeScore('home', 1)" class="py-2 bg-orange-500 hover:bg-orange-600 text-white font-extrabold text-xs sm:text-sm rounded-xl shadow-sm">+1</button>
                                <button onclick="changeScore('home', 2)" class="py-2 bg-orange-500 hover:bg-orange-600 text-white font-extrabold text-xs sm:text-sm rounded-xl shadow-sm">+2</button>
                                <button onclick="changeScore('home', 3)" class="py-2 bg-orange-500 hover:bg-orange-600 text-white font-extrabold text-xs sm:text-sm rounded-xl shadow-sm">+3</button>
                                <button onclick="changeScore('home', -1)" class="py-2 bg-slate-200 hover:bg-slate-300 text-slate-700 font-bold text-xs sm:text-sm rounded-xl">-1</button>
                            </div>
                        </div>

                        <!-- GUEST TEAM -->
                        <div class="bg-slate-50 border-2 border-slate-200 rounded-2xl p-3 sm:p-4 text-center flex flex-col justify-between space-y-2.5 shadow-inner">
                            <input type="text" value="GUEST" class="w-full bg-transparent text-center font-black text-slate-700 text-sm sm:text-base uppercase tracking-wider outline-none border-b border-slate-300 pb-1">
                            <div class="bg-white border-2 border-slate-200 rounded-xl py-2 shadow-inner">
                                <div id="score-guest" class="text-4xl sm:text-5xl font-black text-blue-600 digital-font py-1 tracking-wider">0</div>
                            </div>
                            <div class="grid grid-cols-2 gap-1.5">
                                <button onclick="changeScore('guest', 1)" class="py-2 bg-blue-600 hover:bg-blue-700 text-white font-extrabold text-xs sm:text-sm rounded-xl shadow-sm">+1</button>
                                <button onclick="changeScore('guest', 2)" class="py-2 bg-blue-600 hover:bg-blue-700 text-white font-extrabold text-xs sm:text-sm rounded-xl shadow-sm">+2</button>
                                <button onclick="changeScore('guest', 3)" class="py-2 bg-blue-600 hover:bg-blue-700 text-white font-extrabold text-xs sm:text-sm rounded-xl shadow-sm">+3</button>
                                <button onclick="changeScore('guest', -1)" class="py-2 bg-slate-200 hover:bg-slate-300 text-slate-700 font-bold text-xs sm:text-sm rounded-xl">-1</button>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Quarter Switch Controls -->
                <div class="pt-2 border-t border-slate-200 flex justify-between items-center gap-2">
                    <span class="text-xs text-slate-500 font-bold">Q:</span>
                    <div class="flex gap-1.5 flex-1 justify-end">
                        <button onclick="setPeriod(1)" class="px-3 py-1.5 bg-slate-100 hover:bg-slate-200 text-slate-700 text-xs font-bold rounded-lg border border-slate-200">1Q</button>
                        <button onclick="setPeriod(2)" class="px-3 py-1.5 bg-slate-100 hover:bg-slate-200 text-slate-700 text-xs font-bold rounded-lg border border-slate-200">2Q</button>
                        <button onclick="setPeriod(3)" class="px-3 py-1.5 bg-slate-100 hover:bg-slate-200 text-slate-700 text-xs font-bold rounded-lg border border-slate-200">3Q</button>
                        <button onclick="setPeriod(4)" class="px-3 py-1.5 bg-slate-100 hover:bg-slate-200 text-slate-700 text-xs font-bold rounded-lg border border-slate-200">4Q</button>
                    </div>
                </div>
            </div>
        </section>

        <!-- SECTION 2: INTERACTIVE TACTICS BOARD (HALF COURT) -->
        <section id="sec-board" class="hidden space-y-3">
            <div class="grid grid-cols-1 lg:grid-cols-4 gap-4">
                <!-- Toolbar -->
                <div class="bg-white border border-slate-200 rounded-3xl p-4 space-y-3 shadow-sm flex flex-col justify-between">
                    <div>
                        <h2 class="text-base font-extrabold text-slate-900 mb-1 flex items-center gap-2">
                            <i class="fa-solid fa-chalkboard text-orange-500"></i> ハーフコート作戦盤
                        </h2>
                        <p class="text-xs text-slate-500 mb-3">選手アイコンのドラッグ移動や、ペンによる戦術の書き込みができます。</p>
                        
                        <div class="space-y-2.5">
                            <div class="grid grid-cols-2 gap-2">
                                <button onclick="setBoardTool('select')" id="tool-select" class="py-2 px-2.5 rounded-xl text-xs font-extrabold bg-orange-50 text-orange-600 border border-orange-200 flex items-center justify-center gap-1">
                                    <i class="fa-solid fa-hand-pointer"></i> 移動
                                </button>
                                <button onclick="setBoardTool('draw')" id="tool-draw" class="py-2 px-2.5 rounded-xl text-xs font-extrabold bg-slate-100 text-slate-600 hover:text-slate-900 border border-slate-200 flex items-center justify-center gap-1">
                                    <i class="fa-solid fa-pen"></i> ペン
                                </button>
                            </div>

                            <div>
                                <label class="block text-[11px] font-bold text-slate-500 mb-1">カラー</label>
                                <div class="flex gap-2">
                                    <button onclick="setDrawColor('#2563eb')" class="w-7 h-7 rounded-full bg-blue-600 border-2 border-white shadow-sm"></button>
                                    <button onclick="setDrawColor('#dc2626')" class="w-7 h-7 rounded-full bg-red-600 border-2 border-white shadow-sm"></button>
                                    <button onclick="setDrawColor('#f97316')" class="w-7 h-7 rounded-full bg-orange-500 border-2 border-white shadow-sm"></button>
                                    <button onclick="setDrawColor('#000000')" class="w-7 h-7 rounded-full bg-black border-2 border-white shadow-sm"></button>
                                </div>
                            </div>
                        </div>
                    </div>

                    <div class="pt-3 border-t border-slate-200 flex gap-2">
                        <button onclick="resetBoardPositions()" class="flex-1 py-2 bg-slate-100 hover:bg-slate-200 text-slate-700 rounded-xl text-xs font-bold border border-slate-200">
                            <i class="fa-solid fa-rotate-right mr-1"></i>初期位置
                        </button>
                        <button onclick="clearBoardCanvas()" class="flex-1 py-2 bg-red-50 hover:bg-red-100 text-red-600 rounded-xl text-xs font-bold border border-red-200">
                            <i class="fa-solid fa-trash mr-1"></i>クリア
                        </button>
                    </div>
                </div>

                <!-- Tactics Half Court Canvas -->
                <div class="lg:col-span-3 bg-white border border-slate-200 rounded-3xl p-3 flex items-center justify-center shadow-sm">
                    <div class="relative w-full aspect-[4/3] max-h-[550px] rounded-2xl overflow-hidden court-bg border-4 border-amber-800/40 shadow-inner flex items-center justify-center">
                        <canvas id="boardCanvas" class="w-full h-full block cursor-crosshair touch-none"></canvas>
                    </div>
                </div>
            </div>
        </section>

    </main>

    <script>
        function switchTab(tab) {
            document.getElementById('sec-timer_score').classList.add('hidden');
            document.getElementById('sec-board').classList.add('hidden');

            document.getElementById('tab-timer_score').className = "flex-1 sm:flex-initial px-4 py-2 rounded-lg transition-all text-slate-600 hover:text-slate-900";
            document.getElementById('tab-board').className = "flex-1 sm:flex-initial px-4 py-2 rounded-lg transition-all text-slate-600 hover:text-slate-900";

            if (tab === 'timer_score') {
                document.getElementById('sec-timer_score').classList.remove('hidden');
                document.getElementById('tab-timer_score').className = "flex-1 sm:flex-initial px-4 py-2 rounded-lg transition-all text-orange-600 bg-white shadow-sm border border-slate-200 font-bold";
            } else if (tab === 'board') {
                document.getElementById('sec-board').classList.remove('hidden');
                document.getElementById('tab-board').className = "flex-1 sm:flex-initial px-4 py-2 rounded-lg transition-all text-orange-600 bg-white shadow-sm border border-slate-200 font-bold";
                initBoardCanvas();
            }
        }

        let masterTimerInterval = null, isMasterRunning = false, isShotClockRunning = true;
        let gameTimeLeft = 600, shotClockLeft = 24, currentPeriod = 1;

        function updateTimerDisplays() {
            const m = Math.floor(gameTimeLeft / 60), s = gameTimeLeft % 60;
            document.getElementById('game-clock-display').innerText = `${String(m).padStart(2, '0')}:${String(s).padStart(2, '0')}`;
            document.getElementById('shot-clock-display').innerText = shotClockLeft;
        }

        function toggleMasterTimer() {
            const btn = document.getElementById('btn-master-start');
            if (isMasterRunning) {
                clearInterval(masterTimerInterval);
                isMasterRunning = false;
                btn.innerHTML = `<i class="fa-solid fa-play"></i> 再開`;
                btn.className = "flex-1 py-3.5 bg-orange-500 hover:bg-orange-600 text-white text-base sm:text-lg font-extrabold rounded-2xl shadow-lg shadow-orange-500/20 transition-all flex items-center justify-center gap-2";
            } else {
                masterTimerInterval = setInterval(() => {
                    if (gameTimeLeft > 0) gameTimeLeft--;
                    if (isShotClockRunning && shotClockLeft > 0) {
                        shotClockLeft--;
                    } else if (shotClockLeft === 0) {
                        playBuzzer();
                    }
                    updateTimerDisplays();
                }, 1000);
                isMasterRunning = true;
                btn.innerHTML = `<i class="fa-solid fa-pause"></i> 一時停止`;
                btn.className = "flex-1 py-3.5 bg-slate-600 hover:bg-slate-700 text-white text-base sm:text-lg font-extrabold rounded-2xl shadow-lg transition-all flex items-center justify-center gap-2";
            }
        }

        function toggleShotClockOnly() {
            isShotClockRunning = !isShotClockRunning;
            const btn = document.getElementById('btn-shotclock-toggle');
            btn.innerHTML = isShotClockRunning ? `<i class="fa-solid fa-pause"></i>` : `<i class="fa-solid fa-play"></i>`;
        }

        function resetMasterTimer() {
            if (isMasterRunning) toggleMasterTimer();
            gameTimeLeft = 600; shotClockLeft = 24;
            updateTimerDisplays();
        }

        function setClockPreset(s) {
            if (isMasterRunning) toggleMasterTimer();
            gameTimeLeft = s; shotClockLeft = 24;
            updateTimerDisplays();
        }

        function resetShotClock(s) { shotClockLeft = s; updateTimerDisplays(); }
        function setPeriod(p) {
            currentPeriod = p;
            document.getElementById('period-display').innerText = `第 ${p} クォーター (${p}Q)`;
        }

        function playBuzzer() {
            try {
                const ctx = new (window.AudioContext || window.webkitAudioContext)();
                const osc = ctx.createOscillator();
                const gain = ctx.createGain();
                osc.type = 'sawtooth'; osc.frequency.setValueAtTime(220, ctx.currentTime);
                gain.gain.setValueAtTime(0.2, ctx.currentTime);
                osc.connect(gain); gain.connect(ctx.destination);
                osc.start(); osc.stop(ctx.currentTime + 0.6);
            } catch(e) {}
        }

        let scoreHome = 0, scoreGuest = 0;
        function changeScore(team, val) {
            if (team === 'home') {
                scoreHome = Math.max(0, scoreHome + val);
                document.getElementById('score-home').innerText = scoreHome;
            } else {
                scoreGuest = Math.max(0, scoreGuest + val);
                document.getElementById('score-guest').innerText = scoreGuest;
            }
        }
        function resetScores() {
            scoreHome = 0; scoreGuest = 0;
            document.getElementById('score-home').innerText = "0";
            document.getElementById('score-guest').innerText = "0";
        }

        // TACTICS BOARD CANVAS
        const boardCanvas = document.getElementById('boardCanvas');
        const boardCtx = boardCanvas.getContext('2d');
        let boardMode = 'select', currentDrawColor = '#2563eb', isDrawing = false, selectedToken = null, boardDrawings = [];

        let boardTokens = [
            { id: 'BALL', label: 'BALL', type: 'ball', x: 0.5, y: 0.38 },
            { id: 'O1', label: '1', type: 'offense', x: 0.5, y: 0.3 },
            { id: 'O2', label: '2', type: 'offense', x: 0.8, y: 0.45 },
            { id: 'O3', label: '3', type: 'offense', x: 0.2, y: 0.45 },
            { id: 'O4', label: '4', type: 'offense', x: 0.65, y: 0.75 },
            { id: 'O5', label: '5', type: 'offense', x: 0.35, y: 0.75 },
            { id: 'D1', label: 'D1', type: 'defense', x: 0.5, y: 0.4 },
            { id: 'D2', label: 'D2', type: 'defense', x: 0.73, y: 0.5 },
            { id: 'D3', label: 'D3', type: 'defense', x: 0.27, y: 0.5 },
            { id: 'D4', label: 'D4', type: 'defense', x: 0.6, y: 0.72 },
            { id: 'D5', label: 'D5', type: 'defense', x: 0.4, y: 0.72 }
        ];

        function initBoardCanvas() {
            const container = boardCanvas.parentElement;
            boardCanvas.width = container.clientWidth;
            boardCanvas.height = container.clientHeight;
            renderBoard();
        }

        function drawHalfCourtLines(ctx, w, h) {
            ctx.clearRect(0, 0, w, h);
            ctx.strokeStyle = "#ffffff";
            ctx.lineWidth = Math.max(2, w * 0.005);
            ctx.strokeRect(w * 0.05, h * 0.05, w * 0.9, h * 0.9);

            ctx.beginPath();
            ctx.arc(w / 2, h * 0.05, w * 0.15, 0, Math.PI, false);
            ctx.stroke();

            const kw = w * 0.32, kh = h * 0.42, kx = (w - kw) / 2, ky = h * 0.95 - kh;
            ctx.fillStyle = "rgba(180, 83, 9, 0.35)";
            ctx.fillRect(kx, ky, kw, kh);
            ctx.strokeRect(kx, ky, kw, kh);

            ctx.beginPath();
            ctx.arc(w / 2, ky, kw / 2, Math.PI, 0, false);
            ctx.stroke();

            const hoopY = h * 0.85, cornerDist = w * 0.38;
            ctx.beginPath();
            ctx.moveTo(w / 2 - cornerDist, h * 0.95);
            ctx.lineTo(w / 2 - cornerDist, hoopY);
            ctx.arc(w / 2, hoopY, cornerDist, Math.PI, 0, false);
            ctx.lineTo(w / 2 + cornerDist, h * 0.95);
            ctx.stroke();

            ctx.beginPath();
            ctx.arc(w / 2, hoopY, w * 0.022, 0, Math.PI * 2);
            ctx.strokeStyle = "#ea580c"; ctx.lineWidth = 3; ctx.stroke();
        }

        function renderBoard() {
            const w = boardCanvas.width, h = boardCanvas.height;
            drawHalfCourtLines(boardCtx, w, h);

            boardCtx.lineWidth = 3; boardCtx.lineCap = 'round'; boardCtx.lineJoin = 'round';
            boardDrawings.forEach(path => {
                if (path.points.length < 2) return;
                boardCtx.strokeStyle = path.color;
                boardCtx.beginPath();
                boardCtx.moveTo(path.points[0].x * w, path.points[0].y * h);
                for (let i = 1; i < path.points.length; i++) {
                    boardCtx.lineTo(path.points[i].x * w, path.points[i].y * h);
                }
                boardCtx.stroke();
            });

            boardTokens.forEach(t => {
                const tx = t.x * w, ty = t.y * h, radius = Math.max(15, w * 0.025);
                boardCtx.beginPath();
                boardCtx.arc(tx, ty, radius, 0, Math.PI * 2);
                boardCtx.fillStyle = t.type === 'ball' ? '#ea580c' : (t.type === 'offense' ? '#2563eb' : '#dc2626');
                boardCtx.fill();
                boardCtx.strokeStyle = '#ffffff'; boardCtx.lineWidth = 2; boardCtx.stroke();

                if (t.type !== 'ball') {
                    boardCtx.fillStyle = '#ffffff';
                    boardCtx.font = "bold 11px sans-serif";
                    boardCtx.textAlign = "center"; boardCtx.textBaseline = "middle";
                    boardCtx.fillText(t.label, tx, ty);
                }
            });
        }

        function setBoardTool(mode) {
            boardMode = mode;
            document.getElementById('tool-select').className = mode === 'select' ? "py-2 px-2.5 rounded-xl text-xs font-extrabold bg-orange-50 text-orange-600 border border-orange-200 flex items-center justify-center gap-1" : "py-2 px-2.5 rounded-xl text-xs font-extrabold bg-slate-100 text-slate-600 border border-slate-200 flex items-center justify-center gap-1";
            document.getElementById('tool-draw').className = mode === 'draw' ? "py-2 px-2.5 rounded-xl text-xs font-extrabold bg-orange-50 text-orange-600 border border-orange-200 flex items-center justify-center gap-1" : "py-2 px-2.5 rounded-xl text-xs font-extrabold bg-slate-100 text-slate-600 border border-slate-200 flex items-center justify-center gap-1";
        }
        function setDrawColor(c) { currentDrawColor = c; setBoardTool('draw'); }

        function resetBoardPositions() {
            boardTokens = [
                { id: 'BALL', label: 'BALL', type: 'ball', x: 0.5, y: 0.38 },
                { id: 'O1', label: '1', type: 'offense', x: 0.5, y: 0.3 },
                { id: 'O2', label: '2', type: 'offense', x: 0.8, y: 0.45 },
                { id: 'O3', label: '3', type: 'offense', x: 0.2, y: 0.45 },
                { id: 'O4', label: '4', type: 'offense', x: 0.65, y: 0.75 },
                { id: 'O5', label: '5', type: 'offense', x: 0.35, y: 0.75 },
                { id: 'D1', label: 'D1', type: 'defense', x: 0.5, y: 0.4 },
                { id: 'D2', label: 'D2', type: 'defense', x: 0.73, y: 0.5 },
                { id: 'D3', label: 'D3', type: 'defense', x: 0.27, y: 0.5 },
                { id: 'D4', label: 'D4', type: 'defense', x: 0.6, y: 0.72 },
                { id: 'D5', label: 'D5', type: 'defense', x: 0.4, y: 0.72 }
            ];
            renderBoard();
        }
        function clearBoardCanvas() { boardDrawings = []; renderBoard(); }

        let currentPath = null;
        boardCanvas.addEventListener('pointerdown', (e) => {
            const rect = boardCanvas.getBoundingClientRect();
            const x = (e.clientX - rect.left) / rect.width, y = (e.clientY - rect.top) / rect.height;
            if (boardMode === 'select') {
                selectedToken = boardTokens.find(t => Math.hypot(t.x - x, t.y - y) < 0.08);
            } else {
                isDrawing = true;
                currentPath = { color: currentDrawColor, points: [{ x, y }] };
                boardDrawings.push(currentPath);
            }
        });
        boardCanvas.addEventListener('pointermove', (e) => {
            const rect = boardCanvas.getBoundingClientRect();
            const x = (e.clientX - rect.left) / rect.width, y = (e.clientY - rect.top) / rect.height;
            if (boardMode === 'select' && selectedToken) {
                selectedToken.x = Math.max(0.05, Math.min(0.95, x));
                selectedToken.y = Math.max(0.05, Math.min(0.95, y));
                renderBoard();
            } else if (boardMode === 'draw' && isDrawing && currentPath) {
                currentPath.points.push({ x, y });
                renderBoard();
            }
        });
        boardCanvas.addEventListener('pointerup', () => { selectedToken = null; isDrawing = false; currentPath = null; });

        window.onload = () => { updateTimerDisplays(); };
        window.onresize = () => { if (!document.getElementById('sec-board').classList.contains('hidden')) initBoardCanvas(); };
    </script>
</body>
</html>
