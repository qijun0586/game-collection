<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>陈启君测试合集</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdn.jsdelivr.net/npm/font-awesome@4.7.0/css/font-awesome.min.css" rel="stylesheet">
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        primary: '#4F46E5',
                        secondary: '#EC4899',
                        accent: '#10B981',
                        dark: '#0F172A',
                        darker: '#020617',
                        'dark-accent': '#1E293B',
                        light: '#F9FAFB'
                    },
                    fontFamily: {
                        game: ['Poppins', 'sans-serif'],
                    },
                }
            }
        }
    </script>
    <style type="text/tailwindcss">
        @layer utilities {
            .content-auto {
                content-visibility: auto;
            }
            .grid-bg {
                background-size: 30px 30px;
                background-image:
                    linear-gradient(to right, rgba(255,255,255,0.07) 1px, transparent 1px),
                    linear-gradient(to bottom, rgba(255,255,255,0.07) 1px, transparent 1px);
                animation: gridShift 20s linear infinite;
            }
            .starfield-bg {
                background: radial-gradient(ellipse at bottom, #1B2735 0%, #090A0F 100%);
                position: relative;
                overflow: hidden;
            }
            .star {
                position: absolute;
                background-color: white;
                border-radius: 50%;
                animation: twinkle linear infinite;
            }
            .text-shadow {
                text-shadow: 0 2px 8px rgba(0,0,0,0.4);
            }
            .glow {
                filter: drop-shadow(0 0 8px rgba(79, 70, 229, 0.5));
            }
            .food-glow {
                filter: drop-shadow(0 0 10px rgba(255, 165, 0, 0.7));
            }
            .plane-glow {
                filter: drop-shadow(0 0 6px rgba(34, 211, 238, 0.8));
            }
            .enemy-glow {
                filter: drop-shadow(0 0 6px rgba(239, 68, 68, 0.8));
            }
            .powerup-glow {
                filter: drop-shadow(0 0 8px rgba(16, 185, 129, 0.9));
            }
            .btn-glow {
                filter: drop-shadow(0 0 5px rgba(79, 70, 229, 0.3));
            }
            .bg-game-gradient {
                background: linear-gradient(135deg, #0F172A 0%, #1E293B 100%);
            }
            .border-gradient {
                border-image: linear-gradient(45deg, #4F46E5, #EC4899) 1;
            }
            .rainbow-1 { background: linear-gradient(90deg, #FF5E5E, #FF7D5E); }
            .rainbow-2 { background: linear-gradient(90deg, #FF7D5E, #FFB347); }
            .rainbow-3 { background: linear-gradient(90deg, #FFB347, #FFF275); }
            .rainbow-4 { background: linear-gradient(90deg, #FFF275, #93FF96); }
            .rainbow-5 { background: linear-gradient(90deg, #93FF96, #42D7F5); }
            .rainbow-6 { background: linear-gradient(90deg, #42D7F5, #7D5FFF); }
            .rainbow-7 { background: linear-gradient(90deg, #7D5FFF, #C774E8); }
            .rainbow-8 { background: linear-gradient(90deg, #C774E8, #FF5E5E); }

            @keyframes gridShift {
                0% { background-position: 0 0; }
                100% { background-position: 30px 30px; }
            }
            @keyframes pulse {
                0%, 100% { transform: scale(1); }
                50% { transform: scale(1.05); }
            }
            @keyframes fadeIn {
                from { opacity: 0; transform: scale(0.9); }
                to { opacity: 1; transform: scale(1); }
            }
            @keyframes float {
                0%, 100% { transform: translateY(0); }
                50% { transform: translateY(-10px); }
            }
            @keyframes twinkle {
                0%, 100% { opacity: 1; }
                50% { opacity: 0.3; }
            }
            @keyframes slideIn {
                from { transform: translateY(20px); opacity: 0; }
                to { transform: translateY(0); opacity: 1; }
            }
            @keyframes buttonPress {
                0% { transform: scale(1); }
                50% { transform: scale(0.9); }
                100% { transform: scale(1); }
            }
            .animate-fade-in {
                animation: fadeIn 0.5s ease-out forwards;
            }
            .animate-pulse-slow {
                animation: pulse 3s infinite;
            }
            .animate-float {
                animation: float 3s ease-in-out infinite;
            }
            .animate-slide-in {
                animation: slideIn 0.5s ease-out forwards;
            }
            .animate-button-press {
                animation: buttonPress 0.2s ease-in-out;
            }
        }
    </style>
</head>
<body class="bg-game-gradient font-game text-light min-h-screen flex flex-col items-center justify-start p-4 overflow-hidden pt-4">
    <div class="max-w-3xl w-full flex flex-col h-[calc(100vh-2rem)]">
        <!-- 标题区域 -->
        <header class="mb-4 flex justify-between items-center flex-shrink-0">
            <h1 class="text-[clamp(1.2rem,4vw,2rem)] font-bold text-transparent bg-clip-text bg-gradient-to-r from-primary to-secondary text-shadow animate-pulse-slow">
                陈启君测试合集
            </h1>
            <div id="score-display" class="bg-dark/60 backdrop-blur-md px-4 py-2 rounded-lg border border-white/15 shadow-lg glow transition-all duration-300 hover:shadow-primary/20 hidden">
                <span class="text-sm font-medium text-white/70">分数:</span>
                <span id="score" class="text-xl font-bold ml-2 transition-all duration-300">0</span>
            </div>
        </header>

        <!-- 游戏选择界面 -->
        <div id="game-selection" class="bg-dark-accent/80 backdrop-blur-sm rounded-xl overflow-hidden shadow-2xl border-2 border-transparent border-gradient flex-grow mb-4 flex flex-col items-center justify-center p-6">
            <h2 class="text-[clamp(1.5rem,5vw,2.5rem)] font-bold mb-8 text-transparent bg-clip-text bg-gradient-to-r from-primary to-secondary text-shadow animate-pulse-slow">
                选择游戏
            </h2>

            <div class="grid grid-cols-1 md:grid-cols-2 gap-6 w-full max-w-md">
                <!-- 贪吃蛇游戏选择卡片 -->
                <div class="game-card bg-dark/60 backdrop-blur-md rounded-xl p-5 border border-white/10 hover:border-primary/50 transition-all duration-300 cursor-pointer transform hover:scale-105 hover:shadow-lg hover:shadow-primary/20 animate-slide-in" data-game="snake" style="animation-delay: 0.1s">
                    <div class="flex justify-center mb-4">
                        <div class="w-20 h-20 relative">
                            <div class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 w-16 h-6 rounded-full rainbow-1"></div>
                            <div class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 w-12 h-6 rounded-full rainbow-3" style="left: 35%"></div>
                            <div class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 w-8 h-6 rounded-full rainbow-5" style="left: 25%"></div>
                        </div>
                    </div>
                    <h3 class="text-xl font-bold text-center mb-2">进阶版贪吃蛇</h3>
                    <p class="text-white/60 text-sm text-center">经典贪吃蛇，带有彩虹变色和速度变化</p>
                </div>

                <!-- 飞机大战游戏选择卡片 -->
                <div class="game-card bg-dark/60 backdrop-blur-md rounded-xl p-5 border border-white/10 hover:border-secondary/50 transition-all duration-300 cursor-pointer transform hover:scale-105 hover:shadow-lg hover:shadow-secondary/20 animate-slide-in" data-game="plane" style="animation-delay: 0.2s">
                    <div class="flex justify-center mb-4">
                        <div class="w-20 h-20 relative">
                            <div class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 w-16 h-16">
                                <!-- 飞机形状 -->
                                <svg viewBox="0 0 100 100" class="plane-glow">
                                    <path d="M50,10 L90,50 L50,90 L10,50 Z" fill="#22D3EE" />
                                    <path d="M50,30 L70,50 L50,70 L30,50 Z" fill="#38BDF8" />
                                </svg>
                            </div>
                        </div>
                    </div>
                    <h3 class="text-xl font-bold text-center mb-2">太空飞机大战</h3>
                    <p class="text-white/60 text-sm text-center">击落敌机，收集道具，挑战高分</p>
                </div>
            </div>

            <button id="back-to-menu" class="mt-8 px-6 py-2 bg-dark/60 backdrop-blur-md rounded-lg border border-white/10 text-white/80 hover:text-white transition-all duration-300 hidden">
                <i class="fa fa-home mr-2"></i>返回菜单
            </button>
        </div>

        <!-- 贪吃蛇游戏区域 -->
        <div id="snake-game" class="bg-dark-accent/80 backdrop-blur-sm rounded-xl overflow-hidden shadow-2xl border-2 border-transparent border-gradient flex-grow mb-4 hidden relative">
            <canvas id="snakeCanvas" class="w-full h-full grid-bg"></canvas>

            <!-- 虚拟方向键 -->
            <div class="absolute bottom-4 right-4 flex flex-col items-center gap-2 z-10 md:hidden">
                <button id="snake-up" class="w-16 h-16 bg-dark/70 backdrop-blur-md rounded-full border border-white/20 flex items-center justify-center text-2xl text-white hover:bg-primary/30 active:animate-button-press transition-all duration-200 btn-glow">
                    <i class="fa fa-arrow-up"></i>
                </button>
                <div class="flex gap-2">
                    <button id="snake-left" class="w-16 h-16 bg-dark/70 backdrop-blur-md rounded-full border border-white/20 flex items-center justify-center text-2xl text-white hover:bg-primary/30 active:animate-button-press transition-all duration-200 btn-glow">
                        <i class="fa fa-arrow-left"></i>
                    </button>
                    <button id="snake-down" class="w-16 h-16 bg-dark/70 backdrop-blur-md rounded-full border border-white/20 flex items-center justify-center text-2xl text-white hover:bg-primary/30 active:animate-button-press transition-all duration-200 btn-glow">
                        <i class="fa fa-arrow-down"></i>
                    </button>
                    <button id="snake-right" class="w-16 h-16 bg-dark/70 backdrop-blur-md rounded-full border border-white/20 flex items-center justify-center text-2xl text-white hover:bg-primary/30 active:animate-button-press transition-all duration-200 btn-glow">
                        <i class="fa fa-arrow-right"></i>
                    </button>
                </div>
            </div>

            <div id="snake-gameOver" class="absolute inset-0 bg-dark/70 backdrop-blur-md flex flex-col items-center justify-center hidden animate-fade-in">
                <h2 class="text-[clamp(2rem,6vw,3.5rem)] font-bold mb-2 text-transparent bg-clip-text bg-gradient-to-r from-red-500 to-yellow-500 text-shadow">游戏结束!</h2>
                <p class="text-[clamp(1rem,3vw,1.5rem)] mb-6">最终分数: <span id="snake-finalScore" class="font-bold">0</span></p>
                <div class="flex flex-col sm:flex-row gap-4">
                    <button id="snake-restartButton" class="px-6 py-3 bg-gradient-to-r from-primary to-secondary rounded-full text-white font-bold shadow-lg hover:shadow-primary/30 hover:scale-105 transition-all duration-300 focus:outline-none focus:ring-2 focus:ring-primary/50">
                        <i class="fa fa-refresh mr-2"></i>重新开始
                    </button>
                    <button class="back-to-menu-btn px-6 py-3 bg-dark/60 backdrop-blur-md rounded-full text-white font-bold shadow-lg hover:shadow-white/10 hover:scale-105 transition-all duration-300 focus:outline-none">
                        <i class="fa fa-home mr-2"></i>返回菜单
                    </button>
                </div>
            </div>
        </div>

        <!-- 飞机大战游戏区域 -->
        <div id="plane-game" class="bg-dark-accent/80 backdrop-blur-sm rounded-xl overflow-hidden shadow-2xl border-2 border-transparent border-gradient flex-grow mb-4 hidden relative">
            <canvas id="planeCanvas" class="w-full h-full starfield-bg"></canvas>

            <!-- 鼠标控制提示 -->
            <div class="absolute top-4 left-4 bg-dark/50 backdrop-blur-sm px-3 py-1 rounded-lg text-xs text-white/70 hidden md:block">
                <p>鼠标移动控制方向 | 左键发射 | 右键打开菜单</p>
            </div>

            <!-- 右键菜单 -->
            <div id="plane-context-menu" class="absolute hidden bg-dark-accent/90 backdrop-blur-md rounded-lg shadow-xl border border-white/10 py-2 z-20 min-w-[150px] animate-fade-in">
                <button id="plane-restart-from-menu" class="w-full text-left px-4 py-2 text-white hover:bg-primary/20 transition-colors duration-200">
                    <i class="fa fa-refresh mr-2"></i>重新开始
                </button>
                <button id="plane-continue" class="w-full text-left px-4 py-2 text-white hover:bg-primary/20 transition-colors duration-200">
                    <i class="fa fa-play mr-2"></i>继续游戏
                </button>
                <button id="plane-back-to-menu" class="w-full text-left px-4 py-2 text-white hover:bg-primary/20 transition-colors duration-200">
                    <i class="fa fa-home mr-2"></i>返回菜单
                </button>
            </div>

            <div id="plane-gameOver" class="absolute inset-0 bg-dark/70 backdrop-blur-md flex flex-col items-center justify-center hidden animate-fade-in">
                <h2 class="text-[clamp(2rem,6vw,3.5rem)] font-bold mb-2 text-transparent bg-clip-text bg-gradient-to-r from-red-500 to-yellow-500 text-shadow">游戏结束!</h2>
                <p class="text-[clamp(1rem,3vw,1.5rem)] mb-6">最终分数: <span id="plane-finalScore" class="font-bold">0</span></p>
                <div class="flex flex-col sm:flex-row gap-4">
                    <button id="plane-restartButton" class="px-6 py-3 bg-gradient-to-r from-primary to-secondary rounded-full text-white font-bold shadow-lg hover:shadow-primary/30 hover:scale-105 transition-all duration-300 focus:outline-none focus:ring-2 focus:ring-primary/50">
                        <i class="fa fa-refresh mr-2"></i>重新开始
                    </button>
                    <button class="back-to-menu-btn px-6 py-3 bg-dark/60 backdrop-blur-md rounded-full text-white font-bold shadow-lg hover:shadow-white/10 hover:scale-105 transition-all duration-300 focus:outline-none">
                        <i class="fa fa-home mr-2"></i>返回菜单
                    </button>
                </div>
            </div>
        </div>

        <!-- 游戏说明区域 -->
        <div id="game-instructions" class="mt-2 text-center text-white/60 text-sm flex-shrink-0">
            <p class="flex flex-wrap justify-center items-center gap-x-1">使用方向键
                <i class="fa fa-arrow-up mx-1"></i>
                <i class="fa fa-arrow-down mx-1"></i>
                <i class="fa fa-arrow-left mx-1"></i>
                <i class="fa fa-arrow-right mx-1"></i>
                控制
            </p>
            <p id="snake-instructions" class="mt-1 hidden">每吃一个食物，蛇的速度会增加，颜色也会变化</p>
            <p id="plane-instructions" class="mt-1 hidden">空格键发射子弹，击落敌机获取分数和道具</p>
        </div>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', () => {
            // 游戏状态管理
            const gameState = {
                currentGame: null,
                score: 0,
                isGameOver: false,
                isPaused: false
            };

            // DOM 元素
            const gameSelection = document.getElementById('game-selection');
            const snakeGame = document.getElementById('snake-game');
            const planeGame = document.getElementById('plane-game');
            const scoreDisplay = document.getElementById('score-display');
            const scoreElement = document.getElementById('score');
            const backToMenuBtn = document.getElementById('back-to-menu');
            const gameCards = document.querySelectorAll('.game-card');
            const backToMenuBtns = document.querySelectorAll('.back-to-menu-btn');
            const snakeInstructions = document.getElementById('snake-instructions');
            const planeInstructions = document.getElementById('plane-instructions');

            // 贪吃蛇虚拟按键
            const snakeUpBtn = document.getElementById('snake-up');
            const snakeDownBtn = document.getElementById('snake-down');
            const snakeLeftBtn = document.getElementById('snake-left');
            const snakeRightBtn = document.getElementById('snake-right');

            // 飞机大战右键菜单
            const planeContextMenu = document.getElementById('plane-context-menu');
            const planeRestartFromMenu = document.getElementById('plane-restart-from-menu');
            const planeContinue = document.getElementById('plane-continue');
            const planeBackToMenu = document.getElementById('plane-back-to-menu');

            // 游戏切换函数
            function showGame(gameName) {
                gameSelection.classList.add('hidden');
                snakeGame.classList.add('hidden');
                planeGame.classList.add('hidden');
                snakeInstructions.classList.add('hidden');
                planeInstructions.classList.add('hidden');

                if (gameName === 'snake') {
                    snakeGame.classList.remove('hidden');
                    snakeInstructions.classList.remove('hidden');
                    initSnakeGame();
                } else if (gameName === 'plane') {
                    planeGame.classList.remove('hidden');
                    planeInstructions.classList.remove('hidden');
                    initPlaneGame();
                }

                scoreDisplay.classList.remove('hidden');
                backToMenuBtn.classList.remove('hidden');
                gameState.currentGame = gameName;
                gameState.isPaused = false;
                updateScore(0);
            }

            function returnToMenu() {
                if (gameState.currentGame === 'snake') {
                    stopSnakeGame();
                } else if (gameState.currentGame === 'plane') {
                    stopPlaneGame();
                }

                gameSelection.classList.remove('hidden');
                snakeGame.classList.add('hidden');
                planeGame.classList.add('hidden');
                scoreDisplay.classList.add('hidden');
                backToMenuBtn.classList.add('hidden');
                snakeInstructions.classList.add('hidden');
                planeInstructions.classList.add('hidden');
                planeContextMenu.classList.add('hidden');

                gameState.currentGame = null;
            }

            function updateScore(newScore) {
                gameState.score = newScore;
                scoreElement.textContent = newScore;

                // 分数变化动画
                scoreElement.classList.add('scale-125', 'text-secondary');
                setTimeout(() => {
                    scoreElement.classList.remove('scale-125', 'text-secondary');
                }, 300);
            }

            // 事件监听器
            gameCards.forEach(card => {
                card.addEventListener('click', () => {
                    showGame(card.dataset.game);
                });
            });

            backToMenuBtn.addEventListener('click', returnToMenu);
            backToMenuBtns.forEach(btn => {
                btn.addEventListener('click', returnToMenu);
            });

            // 贪吃蛇游戏实现
            let snakeGameInterval;
            const snakeCanvas = document.getElementById('snakeCanvas');
            const snakeCtx = snakeCanvas.getContext('2d');
            const snakeGameOverScreen = document.getElementById('snake-gameOver');
            const snakeFinalScore = document.getElementById('snake-finalScore');
            const snakeRestartButton = document.getElementById('snake-restartButton');

            // 贪吃蛇游戏变量
            let snake = [];
            let food = {};
            let snakeDirection = 'right';
            let snakeNextDirection = 'right';
            let gridSize;
            let snakeSize;
            let foodSize;
            let snakeGameSpeed = 150;
            let rainbowColors = [
                'rainbow-1', 'rainbow-2', 'rainbow-3', 'rainbow-4',
                'rainbow-5', 'rainbow-6', 'rainbow-7', 'rainbow-8'
            ];
            let currentColorIndex = 0;

            function resizeSnakeCanvas() {
                const container = snakeGame;
                snakeCanvas.width = container.clientWidth;
                snakeCanvas.height = container.clientHeight;
            }

            function initSnakeGame() {
                resizeSnakeCanvas();
                window.addEventListener('resize', resizeSnakeCanvas);

                gridSize = Math.floor(snakeCanvas.width / 25);
                snakeSize = gridSize * 0.8;
                foodSize = gridSize * 0.9;

                snake = [
                    {x: 5 * gridSize, y: 5 * gridSize},
                    {x: 4 * gridSize, y: 5 * gridSize},
                    {x: 3 * gridSize, y: 5 * gridSize}
                ];
                snakeDirection = 'right';
                snakeNextDirection = 'right';
                currentColorIndex = 0;
                snakeGameSpeed = 150;

                gameState.isGameOver = false;
                snakeGameOverScreen.classList.add('hidden');

                generateSnakeFood();
                updateScore(0);

                if (snakeGameInterval) clearInterval(snakeGameInterval);
                snakeGameInterval = setInterval(snakeGameLoop, snakeGameSpeed);
            }

            function stopSnakeGame() {
                if (snakeGameInterval) clearInterval(snakeGameInterval);
                window.removeEventListener('resize', resizeSnakeCanvas);
            }

            function generateSnakeFood() {
                const maxX = Math.floor(snakeCanvas.width / gridSize) - 1;
                const maxY = Math.floor(snakeCanvas.height / gridSize) - 1;

                let overlapping;
                do {
                    overlapping = false;
                    food = {
                        x: Math.floor(Math.random() * maxX) * gridSize,
                        y: Math.floor(Math.random() * maxY) * gridSize,
                        blink: 1,
                        blinkDir: -0.02
                    };

                    for (let segment of snake) {
                        if (segment.x === food.x && segment.y === food.y) {
                            overlapping = true;
                            break;
                        }
                    }
                } while (overlapping);
            }

            function getGradientColors(colorClass) {
                const gradients = {
                    'rainbow-1': { start: '#FF5E5E', end: '#FF7D5E' },
                    'rainbow-2': { start: '#FF7D5E', end: '#FFB347' },
                    'rainbow-3': { start: '#FFB347', end: '#FFF275' },
                    'rainbow-4': { start: '#FFF275', end: '#93FF96' },
                    'rainbow-5': { start: '#93FF96', end: '#42D7F5' },
                    'rainbow-6': { start: '#42D7F5', end: '#7D5FFF' },
                    'rainbow-7': { start: '#7D5FFF', end: '#C774E8' },
                    'rainbow-8': { start: '#C774E8', end: '#FF5E5E' }
                };

                return gradients[colorClass] || { start: '#4F46E5', end: '#EC4899' };
            }

            function drawSnake() {
                snake.forEach((segment, index) => {
                    const colorIndex = (currentColorIndex + Math.floor(index / 3)) % rainbowColors.length;
                    const colorClass = rainbowColors[colorIndex];
                    const colors = getGradientColors(colorClass);

                    const gradient = snakeCtx.createLinearGradient(
                        segment.x, segment.y,
                        segment.x + snakeSize, segment.y + snakeSize
                    );
                    gradient.addColorStop(0, colors.start);
                    gradient.addColorStop(1, colors.end);

                    // 呼吸效果
                    const scale = 1 + Math.sin(Date.now() / 300 + index * 0.5) * 0.02;

                    snakeCtx.save();
                    snakeCtx.translate(segment.x + gridSize/2, segment.y + gridSize/2);
                    snakeCtx.scale(scale, scale);
                    snakeCtx.translate(-(segment.x + gridSize/2), -(segment.y + gridSize/2));

                    // 绘制蛇身体
                    snakeCtx.fillStyle = gradient;
                    snakeCtx.beginPath();
                    snakeCtx.roundRect(
                        segment.x + (gridSize - snakeSize) / 2,
                        segment.y + (gridSize - snakeSize) / 2,
                        snakeSize, snakeSize, snakeSize / 4
                    );
                    snakeCtx.fill();

                    // 高光效果
                    snakeCtx.fillStyle = 'rgba(255, 255, 255, 0.1)';
                    snakeCtx.beginPath();
                    snakeCtx.roundRect(
                        segment.x + (gridSize - snakeSize) / 2,
                        segment.y + (gridSize - snakeSize) / 2,
                        snakeSize * 0.6, snakeSize * 0.6, snakeSize / 8
                    );
                    snakeCtx.fill();

                    snakeCtx.restore();

                    // 绘制眼睛
                    if (index === 0) {
                        drawSnakeEyes(segment);
                    }
                });
            }

            function drawSnakeEyes(segment) {
                snakeCtx.fillStyle = '#fff';

                let leftEyeX, leftEyeY, rightEyeX, rightEyeY;
                const eyeSize = snakeSize / 8;
                const eyeOffset = Math.sin(Date.now() / 300) * eyeSize * 0.3;

                switch(snakeDirection) {
                    case 'right':
                        leftEyeX = segment.x + snakeSize * 0.7 + eyeOffset;
                        leftEyeY = segment.y + snakeSize * 0.3;
                        rightEyeX = segment.x + snakeSize * 0.7 + eyeOffset;
                        rightEyeY = segment.y + snakeSize * 0.7;
                        break;
                    case 'left':
                        leftEyeX = segment.x + snakeSize * 0.3 - eyeOffset;
                        leftEyeY = segment.y + snakeSize * 0.3;
                        rightEyeX = segment.x + snakeSize * 0.3 - eyeOffset;
                        rightEyeY = segment.y + snakeSize * 0.7;
                        break;
                    case 'up':
                        leftEyeX = segment.x + snakeSize * 0.3;
                        leftEyeY = segment.y + snakeSize * 0.3 - eyeOffset;
                        rightEyeX = segment.x + snakeSize * 0.7;
                        rightEyeY = segment.y + snakeSize * 0.3 - eyeOffset;
                        break;
                    case 'down':
                        leftEyeX = segment.x + snakeSize * 0.3;
                        leftEyeY = segment.y + snakeSize * 0.7 + eyeOffset;
                        rightEyeX = segment.x + snakeSize * 0.7;
                        rightEyeY = segment.y + snakeSize * 0.7 + eyeOffset;
                        break;
                }

                // 眼睛白色部分
                snakeCtx.beginPath();
                snakeCtx.arc(leftEyeX, leftEyeY, eyeSize, 0, Math.PI * 2);
                snakeCtx.arc(rightEyeX, rightEyeY, eyeSize, 0, Math.PI * 2);
                snakeCtx.fill();

                // 瞳孔
                const pupilOffsetX = Math.sin(Date.now() / 500) * eyeSize * 0.2;
                const pupilOffsetY = Math.cos(Date.now() / 500) * eyeSize * 0.2;

                snakeCtx.fillStyle = '#000';
                snakeCtx.beginPath();
                snakeCtx.arc(leftEyeX + pupilOffsetX, leftEyeY + pupilOffsetY, eyeSize / 2, 0, Math.PI * 2);
                snakeCtx.arc(rightEyeX + pupilOffsetX, rightEyeY + pupilOffsetY, eyeSize / 2, 0, Math.PI * 2);
                snakeCtx.fill();
            }

            function drawSnakeFood() {
                // 更新闪烁状态
                food.blink += food.blinkDir;
                if (food.blink <= 0.8 || food.blink >= 1.2) {
                    food.blinkDir *= -1;
                }

                snakeCtx.save();
                snakeCtx.translate(food.x + gridSize / 2, food.y + gridSize / 2);
                snakeCtx.rotate(Date.now() / 800);
                snakeCtx.scale(food.blink, food.blink);

                // 绘制星星
                snakeCtx.beginPath();
                snakeCtx.moveTo(0, -foodSize / 2);
                for (let i = 1; i < 10; i++) {
                    const angle = (i * 2 * Math.PI / 10) - (Math.PI / 2);
                    const radius = i % 2 === 0 ? foodSize / 2 : foodSize / 5;
                    snakeCtx.lineTo(Math.cos(angle) * radius, Math.sin(angle) * radius);
                }
                snakeCtx.closePath();

                // 径向渐变
                const gradient = snakeCtx.createRadialGradient(
                    0, 0, 0,
                    0, 0, foodSize / 2
                );
                gradient.addColorStop(0, '#FFEE58');
                gradient.addColorStop(0.5, '#FFC107');
                gradient.addColorStop(1, '#FF8F00');

                snakeCtx.fillStyle = gradient;
                snakeCtx.fill();

                // 边框和发光效果
                snakeCtx.strokeStyle = 'rgba(255, 255, 255, 0.9)';
                snakeCtx.lineWidth = 2;
                snakeCtx.stroke();

                // 中心高光
                snakeCtx.fillStyle = 'rgba(255, 255, 255, 0.6)';
                snakeCtx.beginPath();
                snakeCtx.arc(0, 0, foodSize / 8, 0, Math.PI * 2);
                snakeCtx.fill();

                snakeCtx.restore();
            }

            function drawSnakeParticles(x, y) {
                for (let i = 0; i < 8; i++) {
                    const angle = (i * Math.PI / 4);
                    const distance = gridSize * 0.6;
                    const particleX = x + Math.cos(angle) * distance;
                    const particleY = y + Math.sin(angle) * distance;

                    const colorClass = rainbowColors[i % rainbowColors.length];
                    const colors = getGradientColors(colorClass);

                    snakeCtx.fillStyle = colors.start;
                    snakeCtx.beginPath();
                    snakeCtx.arc(particleX, particleY, gridSize / 8, 0, Math.PI * 2);
                    snakeCtx.fill();
                }
            }

            function checkSnakeCollision() {
                const head = {...snake[0]};

                if (
                    head.x < 0 ||
                    head.x >= snakeCanvas.width ||
                    head.y < 0 ||
                    head.y >= snakeCanvas.height
                ) {
                    return true;
                }

                for (let i = 1; i < snake.length; i++) {
                    if (head.x === snake[i].x && head.y === snake[i].y) {
                        return true;
                    }
                }

                return false;
            }

            function snakeGameLoop() {
                if (gameState.isPaused) return;

                snakeCtx.clearRect(0, 0, snakeCanvas.width, snakeCanvas.height);

                snakeDirection = snakeNextDirection;

                const head = {x: snake[0].x, y: snake[0].y};

                switch(snakeDirection) {
                    case 'up':
                        head.y -= gridSize;
                        break;
                    case 'down':
                        head.y += gridSize;
                        break;
                    case 'left':
                        head.x -= gridSize;
                        break;
                    case 'right':
                        head.x += gridSize;
                        break;
                }

                snake.unshift(head);
                let ateFood = false;

                if (head.x === food.x && head.y === food.y) {
                    updateScore(gameState.score + 10);
                    snakeGameSpeed = Math.max(50, snakeGameSpeed - 5);
                    currentColorIndex++;
                    generateSnakeFood();
                    clearInterval(snakeGameInterval);
                    snakeGameInterval = setInterval(snakeGameLoop, snakeGameSpeed);
                    ateFood = true;
                } else {
                    snake.pop();
                }

                if (checkSnakeCollision()) {
                    snakeGameOver();
                    return;
                }

                drawSnake();
                drawSnakeFood();

                if (ateFood) {
                    drawSnakeParticles(head.x + gridSize/2, head.y + gridSize/2);
                }
            }

            function snakeGameOver() {
                gameState.isGameOver = true;
                clearInterval(snakeGameInterval);
                snakeFinalScore.textContent = gameState.score;
                snakeGameOverScreen.classList.remove('hidden');
            }

            snakeRestartButton.addEventListener('click', initSnakeGame);

            // 贪吃蛇虚拟按键控制
            snakeUpBtn.addEventListener('click', () => {
                if (snakeDirection !== 'down' && !gameState.isGameOver) {
                    snakeNextDirection = 'up';
                    snakeUpBtn.classList.add('animate-button-press');
                    setTimeout(() => snakeUpBtn.classList.remove('animate-button-press'), 200);
                }
            });

            snakeDownBtn.addEventListener('click', () => {
                if (snakeDirection !== 'up' && !gameState.isGameOver) {
                    snakeNextDirection = 'down';
                    snakeDownBtn.classList.add('animate-button-press');
                    setTimeout(() => snakeDownBtn.classList.remove('animate-button-press'), 200);
                }
            });

            snakeLeftBtn.addEventListener('click', () => {
                if (snakeDirection !== 'right' && !gameState.isGameOver) {
                    snakeNextDirection = 'left';
                    snakeLeftBtn.classList.add('animate-button-press');
                    setTimeout(() => snakeLeftBtn.classList.remove('animate-button-press'), 200);
                }
            });

            snakeRightBtn.addEventListener('click', () => {
                if (snakeDirection !== 'left' && !gameState.isGameOver) {
                    snakeNextDirection = 'right';
                    snakeRightBtn.classList.add('animate-button-press');
                    setTimeout(() => snakeRightBtn.classList.remove('animate-button-press'), 200);
                }
            });

            // 飞机大战游戏实现
            let planeGameInterval;
            const planeCanvas = document.getElementById('planeCanvas');
            const planeCtx = planeCanvas.getContext('2d');
            const planeGameOverScreen = document.getElementById('plane-gameOver');
            const planeFinalScore = document.getElementById('plane-finalScore');
            const planeRestartButton = document.getElementById('plane-restartButton');

            // 飞机大战游戏变量
            let player = {
                x: 0,
                y: 0,
                width: 40,
                height: 40,
                speed: 5,
                bullets: [],
                bulletSpeed: 8,
                fireRate: 200,
                lastFired: 0,
                invincible: false,
                shield: false,
                multiShot: false,
                lives: 3
            };
            let enemies = [];
            let powerups = [];
            let explosions = [];
            let stars = [];
            let enemySpawnRate = 1500;
            let lastEnemySpawn = 0;
            let gameLevel = 1;

            function resizePlaneCanvas() {
                const container = planeGame;
                planeCanvas.width = container.clientWidth;
                planeCanvas.height = container.clientHeight;

                // 重新定位玩家
                if (player) {
                    player.x = planeCanvas.width / 2 - player.width / 2;
                    player.y = planeCanvas.height - player.height - 20;
                }

                // 重新生成星星背景
                generateStars();
            }

            function generateStars() {
                stars = [];
                const starCount = Math.floor((planeCanvas.width * planeCanvas.height) / 1500);

                for (let i = 0; i < starCount; i++) {
                    stars.push({
                        x: Math.random() * planeCanvas.width,
                        y: Math.random() * planeCanvas.height,
                        radius: Math.random() * 1.5 + 0.3,
                        opacity: Math.random() * 0.8 + 0.2,
                        speed: Math.random() * 0.5 + 0.2,
                        twinkleSpeed: Math.random() * 3 + 2
                    });
                }
            }

            function initPlaneGame() {
                resizePlaneCanvas();
                window.addEventListener('resize', resizePlaneCanvas);

                // 初始化玩家
                player = {
                    x: planeCanvas.width / 2 - 20,
                    y: planeCanvas.height - 60,
                    width: 40,
                    height: 40,
                    speed: 5,
                    bullets: [],
                    bulletSpeed: 8,
                    fireRate: 200,
                    lastFired: 0,
                    invincible: false,
                    shield: false,
                    multiShot: false,
                    lives: 3,
                    blinkState: false,
                    blinkTimer: 0
                };

                enemies = [];
                powerups = [];
                explosions = [];
                enemySpawnRate = 1500;
                lastEnemySpawn = 0;
                gameLevel = 1;

                gameState.isGameOver = false;
                gameState.isPaused = false;
                planeGameOverScreen.classList.add('hidden');
                planeContextMenu.classList.add('hidden');

                updateScore(0);

                if (planeGameInterval) clearInterval(planeGameInterval);
                planeGameInterval = setInterval(planeGameLoop, 16);
            }

            function stopPlaneGame() {
                if (planeGameInterval) clearInterval(planeGameInterval);
                window.removeEventListener('resize', resizePlaneCanvas);
            }

            function spawnEnemy() {
                if (gameState.isPaused) return;

                const enemyTypes = [
                    { width: 30, height: 30, speed: 2 + gameLevel * 0.3, health: 1, score: 10 },
                    { width: 40, height: 40, speed: 1.5 + gameLevel * 0.2, health: 2, score: 20 },
                    { width: 25, height: 25, speed: 3 + gameLevel * 0.4, health: 1, score: 15 }
                ];

                // 随关卡提升增加强敌概率
                let enemyType;
                const rand = Math.random();
                if (rand < 0.7 - gameLevel * 0.05) {
                    enemyType = enemyTypes[0];
                } else if (rand < 0.9 - gameLevel * 0.03) {
                    enemyType = enemyTypes[1];
                } else {
                    enemyType = enemyTypes[2];
                }

                const x = Math.random() * (planeCanvas.width - enemyType.width);

                enemies.push({
                    x: x,
                    y: -enemyType.height,
                    width: enemyType.width,
                    height: enemyType.height,
                    speed: enemyType.speed,
                    health: enemyType.health,
                    score: enemyType.score,
                    color: enemyType.health > 1 ? '#EF4444' : '#F87171',
                    hitFlash: false,
                    hitTimer: 0
                });
            }

            function spawnPowerup(x, y) {
                const powerupTypes = [
                    { type: 'shield', color: '#3B82F6', icon: '🛡️' },
                    { type: 'multishot', color: '#10B981', icon: '⚡' },
                    { type: 'speed', color: '#F59E0B', icon: '💨' },
                    { type: 'life', color: '#EC4899', icon: '❤️' }
                ];

                const type = powerupTypes[Math.floor(Math.random() * powerupTypes.length)];

                powerups.push({
                    x: x,
                    y: y,
                    width: 25,
                    height: 25,
                    speed: 2,
                    type: type.type,
                    color: type.color,
                    icon: type.icon,
                    blink: 1,
                    blinkDir: -0.02
                });
            }

            function createExplosion(x, y, size = 30) {
                const particles = [];
                for (let i = 0; i < 15; i++) {
                    particles.push({
                        x: x,
                        y: y,
                        radius: Math.random() * 3 + 1,
                        color: `hsl(${Math.random() * 60}, 100%, 60%)`,
                        speed: Math.random() * 3 + 1,
                        angle: Math.random() * Math.PI * 2,
                        life: Math.random() * 30 + 20,
                        maxLife: Math.random() * 30 + 20
                    });
                }

                explosions.push({
                    particles: particles,
                    active: true
                });
            }

            function drawPlayer() {
                planeCtx.save();

                // 闪烁效果（无敌状态）
                if (player.invincible) {
                    player.blinkTimer++;
                    if (player.blinkTimer % 10 === 0) {
                        player.blinkState = !player.blinkState;
                    }
                    if (!player.blinkState) {
                        planeCtx.restore();
                        return;
                    }
                }

                // 绘制飞机主体
                const centerX = player.x + player.width / 2;
                const centerY = player.y + player.height / 2;

                planeCtx.translate(centerX, centerY);

                // 轻微摇摆动画
                const wiggle = Math.sin(Date.now() / 500) * 0.03;
                planeCtx.rotate(wiggle);

                planeCtx.translate(-centerX, -centerY);

                // 飞机形状
                planeCtx.beginPath();
                planeCtx.moveTo(player.x + player.width / 2, player.y);
                planeCtx.lineTo(player.x + player.width, player.y + player.height);
                planeCtx.lineTo(player.x + player.width / 2, player.y + player.height * 0.7);
                planeCtx.lineTo(player.x, player.y + player.height);
                planeCtx.closePath();

                // 渐变填充
                const gradient = planeCtx.createLinearGradient(
                    player.x, player.y,
                    player.x + player.width, player.y + player.height
                );
                gradient.addColorStop(0, '#22D3EE');
                gradient.addColorStop(1, '#38BDF8');
                planeCtx.fillStyle = gradient;
                planeCtx.fill();

                // 高光
                planeCtx.fillStyle = 'rgba(255, 255, 255, 0.3)';
                planeCtx.beginPath();
                planeCtx.moveTo(player.x + player.width / 2, player.y + player.height * 0.1);
                planeCtx.lineTo(player.x + player.width * 0.8, player.y + player.height * 0.6);
                planeCtx.lineTo(player.x + player.width / 2, player.y + player.height * 0.5);
                planeCtx.lineTo(player.x + player.width * 0.2, player.y + player.height * 0.6);
                planeCtx.closePath();
                planeCtx.fill();

                // 护盾
                if (player.shield) {
                    planeCtx.strokeStyle = 'rgba(59, 130, 246, 0.8)';
                    planeCtx.lineWidth = 2;
                    planeCtx.beginPath();
                    planeCtx.arc(
                        centerX, centerY,
                        player.width * 0.7,
                        0, Math.PI * 2
                    );
                    planeCtx.stroke();
                }

                // 暂停状态显示
                if (gameState.isPaused) {
                    planeCtx.fillStyle = 'rgba(255, 255, 255, 0.7)';
                    planeCtx.font = '16px Arial';
                    planeCtx.textAlign = 'center';
                    planeCtx.textBaseline = 'middle';
                    planeCtx.fillText('暂停中', planeCanvas.width / 2, planeCanvas.height / 2);
                }

                planeCtx.restore();
            }

            function drawEnemies() {
                enemies.forEach(enemy => {
                    planeCtx.save();

                    // 受击闪烁效果
                    if (enemy.hitFlash) {
                        enemy.hitTimer++;
                        if (enemy.hitTimer > 5) {
                            enemy.hitFlash = false;
                            enemy.hitTimer = 0;
                        }
                        planeCtx.globalAlpha = 0.7;
                    }

                    const centerX = enemy.x + enemy.width / 2;
                    const centerY = enemy.y + enemy.height / 2;

                    // 轻微摇摆动画
                    const wiggle = Math.sin(Date.now() / 800 + enemy.x) * 0.05;
                    planeCtx.translate(centerX, centerY);
                    planeCtx.rotate(wiggle);
                    planeCtx.translate(-centerX, -centerY);

                    // 绘制敌机
                    planeCtx.fillStyle = enemy.color;

                    // 不同类型敌机不同形状
                    if (enemy.width === 30) { // 小型敌机
                        planeCtx.beginPath();
                        planeCtx.moveTo(enemy.x + enemy.width / 2, enemy.y + enemy.height);
                        planeCtx.lineTo(enemy.x + enemy.width, enemy.y);
                        planeCtx.lineTo(enemy.x, enemy.y);
                        planeCtx.closePath();
                        planeCtx.fill();
                    } else if (enemy.width === 40) { // 大型敌机
                        planeCtx.fillRect(enemy.x, enemy.y, enemy.width, enemy.height);
                        planeCtx.fillStyle = '#DC2626';
                        planeCtx.fillRect(enemy.x + 5, enemy.y - 5, enemy.width - 10, 10);
                    } else { // 快速敌机
                        planeCtx.beginPath();
                        planeCtx.ellipse(
                            enemy.x + enemy.width / 2,
                            enemy.y + enemy.height / 2,
                            enemy.width / 2,
                            enemy.height / 2,
                            0, 0, Math.PI * 2
                        );
                        planeCtx.fill();
                    }

                    planeCtx.restore();
                });
            }

            function drawBullets() {
                player.bullets.forEach(bullet => {
                    planeCtx.save();

                    planeCtx.fillStyle = bullet.color || '#FBBF24';

                    // 子弹轨迹
                    if (bullet.trail) {
                        planeCtx.globalAlpha = 0.3;
                        planeCtx.fillRect(
                            bullet.x,
                            bullet.y + bullet.speed * 2,
                            bullet.width,
                            bullet.height * 3
                        );
                        planeCtx.globalAlpha = 1;
                    }

                    planeCtx.fillRect(bullet.x, bullet.y, bullet.width, bullet.height);

                    // 子弹前端高光
                    planeCtx.fillStyle = 'rgba(255, 255, 255, 0.7)';
                    planeCtx.fillRect(
                        bullet.x,
                        bullet.y,
                        bullet.width,
                        bullet.height / 2
                    );

                    planeCtx.restore();
                });
            }

            function drawPowerups() {
                powerups.forEach(powerup => {
                    // 更新闪烁状态
                    powerup.blink += powerup.blinkDir;
                    if (powerup.blink <= 0.8 || powerup.blink >= 1.2) {
                        powerup.blinkDir *= -1;
                    }

                    planeCtx.save();

                    planeCtx.translate(
                        powerup.x + powerup.width / 2,
                        powerup.y + powerup.height / 2
                    );
                    planeCtx.scale(powerup.blink, powerup.blink);
                    planeCtx.translate(
                        -(powerup.x + powerup.width / 2),
                        -(powerup.y + powerup.height / 2)
                    );

                    // 绘制道具
                    planeCtx.fillStyle = powerup.color;
                    planeCtx.beginPath();
                    planeCtx.roundRect(
                        powerup.x, powerup.y,
                        powerup.width, powerup.height,
                        8
                    );
                    planeCtx.fill();

                    // 发光效果
                    planeCtx.strokeStyle = 'rgba(255, 255, 255, 0.8)';
                    planeCtx.lineWidth = 2;
                    planeCtx.stroke();

                    // 图标
                    planeCtx.font = '14px Arial';
                    planeCtx.textAlign = 'center';
                    planeCtx.textBaseline = 'middle';
                    planeCtx.fillStyle = 'white';
                    planeCtx.fillText(
                        powerup.icon,
                        powerup.x + powerup.width / 2,
                        powerup.y + powerup.height / 2
                    );

                    planeCtx.restore();
                });
            }

            function drawExplosions() {
                explosions.forEach(explosion => {
                    if (!explosion.active) return;

                    explosion.particles.forEach(particle => {
                        particle.life--;
                        if (particle.life <= 0) return;

                        particle.x += Math.cos(particle.angle) * particle.speed;
                        particle.y += Math.sin(particle.angle) * particle.speed;

                        const alpha = particle.life / particle.maxLife;

                        planeCtx.save();
                        planeCtx.globalAlpha = alpha;
                        planeCtx.fillStyle = particle.color;
                        planeCtx.beginPath();
                        planeCtx.arc(particle.x, particle.y, particle.radius, 0, Math.PI * 2);
                        planeCtx.fill();
                        planeCtx.restore();
                    });

                    // 检查是否所有粒子都已消失
                    const activeParticles = explosion.particles.some(p => p.life > 0);
                    if (!activeParticles) {
                        explosion.active = false;
                    }
                });

                // 清理已完成的爆炸效果
                explosions = explosions.filter(e => e.active);
            }

            function drawStars() {
                stars.forEach(star => {
                    if (gameState.isPaused) return;

                    // 移动星星模拟背景滚动
                    star.y += star.speed;
                    if (star.y > planeCanvas.height) {
                        star.y = -2;
                        star.x = Math.random() * planeCanvas.width;
                    }

                    // 闪烁效果
                    const alpha = star.opacity * (0.5 + Math.sin(Date.now() / (1000 * star.twinkleSpeed)) * 0.5);

                    planeCtx.save();
                    planeCtx.globalAlpha = alpha;
                    planeCtx.fillStyle = 'white';
                    planeCtx.beginPath();
                    planeCtx.arc(star.x, star.y, star.radius, 0, Math.PI * 2);
                    planeCtx.fill();
                    planeCtx.restore();
                });
            }

            function drawLives() {
                planeCtx.save();
                planeCtx.font = '16px Arial';
                planeCtx.fillStyle = 'white';
                planeCtx.textAlign = 'left';
                planeCtx.textBaseline = 'top';

                let livesText = '❤️'.repeat(player.lives);
                planeCtx.fillText(livesText, 10, 10);

                planeCtx.restore();
            }

            function fireBullet() {
                if (gameState.isPaused || gameState.isGameOver) return;

                const now = Date.now();
                if (now - player.lastFired < player.fireRate) return;

                player.lastFired = now;

                if (player.multiShot) {
                    // 三向射击
                    player.bullets.push({
                        x: player.x + player.width / 2 - 2,
                        y: player.y,
                        width: 4,
                        height: 12,
                        speed: player.bulletSpeed,
                        color: '#FBBF24',
                        trail: true
                    });
                    player.bullets.push({
                        x: player.x + player.width / 2 - 2,
                        y: player.y,
                        width: 4,
                        height: 12,
                        speed: player.bulletSpeed,
                        color: '#FBBF24',
                        trail: true,
                        angle: -0.2
                    });
                    player.bullets.push({
                        x: player.x + player.width / 2 - 2,
                        y: player.y,
                        width: 4,
                        height: 12,
                        speed: player.bulletSpeed,
                        color: '#FBBF24',
                        trail: true,
                        angle: 0.2
                    });
                } else {
                    // 普通射击
                    player.bullets.push({
                        x: player.x + player.width / 2 - 2,
                        y: player.y,
                        width: 4,
                        height: 12,
                        speed: player.bulletSpeed,
                        color: '#FBBF24',
                        trail: true
                    });
                }
            }

            function checkCollisions() {
                if (gameState.isPaused) return;

                // 子弹与敌机碰撞
                player.bullets = player.bullets.filter(bullet => {
                    let hit = false;

                    // 更新子弹位置（考虑角度）
                    if (bullet.angle) {
                        bullet.x += Math.sin(bullet.angle) * bullet.speed;
                        bullet.y -= Math.cos(bullet.angle) * bullet.speed;
                    } else {
                        bullet.y -= bullet.speed;
                    }

                    // 子弹出界检查
                    if (bullet.y < -bullet.height ||
                        bullet.x < -bullet.width ||
                        bullet.x > planeCanvas.width) {
                        return false;
                    }

                    // 检测与敌机的碰撞
                    enemies.forEach(enemy => {
                        if (
                            bullet.x < enemy.x + enemy.width &&
                            bullet.x + bullet.width > enemy.x &&
                            bullet.y < enemy.y + enemy.height &&
                            bullet.y + bullet.height > enemy.y
                        ) {
                            hit = true;
                            enemy.health--;
                            enemy.hitFlash = true;

                            // 敌机被摧毁
                            if (enemy.health <= 0) {
                                createExplosion(
                                    enemy.x + enemy.width / 2,
                                    enemy.y + enemy.height / 2,
                                    enemy.width
                                );

                                updateScore(gameState.score + enemy.score);

                                // 随机掉落道具
                                if (Math.random() < 0.2) {
                                    spawnPowerup(
                                        enemy.x + enemy.width / 2 - 12,
                                        enemy.y + enemy.height / 2 - 12
                                    );
                                }

                                // 移除敌机
                                enemies = enemies.filter(e => e !== enemy);
                            }
                        }
                    });

                    return !hit;
                });

                // 敌机与玩家碰撞
                if (!player.invincible) {
                    enemies.forEach(enemy => {
                        let collision = false;

                        if (player.shield) {
                            // 护盾碰撞检测（更大范围）
                            const playerCenterX = player.x + player.width / 2;
                            const playerCenterY = player.y + player.height / 2;
                            const enemyCenterX = enemy.x + enemy.width / 2;
                            const enemyCenterY = enemy.y + enemy.height / 2;
                            const distance = Math.sqrt(
                                Math.pow(enemyCenterX - playerCenterX, 2) +
                                Math.pow(enemyCenterY - playerCenterY, 2)
                            );

                            if (distance < player.width * 0.7) {
                                collision = true;
                                player.shield = false; // 护盾吸收一次伤害
                                createExplosion(enemyCenterX, enemyCenterY);
                            }
                        } else {
                            // 直接碰撞检测
                            if (
                                player.x < enemy.x + enemy.width &&
                                player.x + player.width > enemy.x &&
                                player.y < enemy.y + enemy.height &&
                                player.y + player.height > enemy.y
                            ) {
                                collision = true;
                            }
                        }

                        if (collision) {
                            createExplosion(
                                enemy.x + enemy.width / 2,
                                enemy.y + enemy.height / 2
                            );

                            enemies = enemies.filter(e => e !== enemy);

                            if (!player.shield) {
                                player.lives--;
                                player.invincible = true;
                                createExplosion(
                                    player.x + player.width / 2,
                                    player.y + player.height / 2,
                                    player.width * 1.5
                                );

                                // 3秒后取消无敌状态
                                setTimeout(() => {
                                    if (player) player.invincible = false;
                                }, 3000);

                                if (player.lives <= 0) {
                                    planeGameOver();
                                }
                            }
                        }
                    });
                }

                // 道具与玩家碰撞
                powerups = powerups.filter(powerup => {
                    powerup.y += powerup.speed;

                    // 道具出界
                    if (powerup.y > planeCanvas.height) {
                        return false;
                    }

                    // 检测碰撞
                    if (
                        player.x < powerup.x + powerup.width &&
                        player.x + player.width > powerup.x &&
                        player.y < powerup.y + powerup.height &&
                        player.y + player.height > powerup.y
                    ) {
                        createExplosion(
                            powerup.x + powerup.width / 2,
                            powerup.y + powerup.height / 2,
                            20
                        );

                        // 应用道具效果
                        switch(powerup.type) {
                            case 'shield':
                                player.shield = true;
                                break;
                            case 'multishot':
                                player.multiShot = true;
                                setTimeout(() => {
                                    if (player) player.multiShot = false;
                                }, 8000);
                                break;
                            case 'speed':
                                player.speed *= 1.5;
                                player.bulletSpeed *= 1.5;
                                setTimeout(() => {
                                    if (player) {
                                        player.speed /= 1.5;
                                        player.bulletSpeed /= 1.5;
                                    }
                                }, 5000);
                                break;
                            case 'life':
                                player.lives++;
                                break;
                        }

                        return false;
                    }

                    return true;
                });

                // 移除出界的敌机
                enemies = enemies.filter(enemy => {
                    enemy.y += enemy.speed;
                    return enemy.y < planeCanvas.height + enemy.height;
                });
            }

            function updateLevel() {
                if (gameState.isPaused) return;

                const newLevel = Math.floor(gameState.score / 100) + 1;
                if (newLevel > gameLevel) {
                    gameLevel = newLevel;
                    enemySpawnRate = Math.max(500, 1500 - (gameLevel - 1) * 100);
                }
            }

            function planeGameLoop() {
                planeCtx.clearRect(0, 0, planeCanvas.width, planeCanvas.height);

                // 绘制背景星星
                drawStars();

                // 绘制玩家
                drawPlayer();

                // 绘制敌机
                drawEnemies();

                // 绘制子弹
                drawBullets();

                // 绘制道具
                drawPowerups();

                // 绘制爆炸效果
                drawExplosions();

                // 绘制生命值
                drawLives();

                // 生成敌机
                const now = Date.now();
                if (now - lastEnemySpawn > enemySpawnRate) {
                    spawnEnemy();
                    lastEnemySpawn = now;
                }

                // 碰撞检测
                checkCollisions();

                // 更新关卡
                updateLevel();
            }

            function planeGameOver() {
                gameState.isGameOver = true;
                clearInterval(planeGameInterval);
                planeFinalScore.textContent = gameState.score;
                planeGameOverScreen.classList.remove('hidden');
                planeContextMenu.classList.add('hidden');
            }

            planeRestartButton.addEventListener('click', initPlaneGame);

            // 飞机大战右键菜单功能
            planeRestartFromMenu.addEventListener('click', () => {
                initPlaneGame();
                planeContextMenu.classList.add('hidden');
            });

            planeContinue.addEventListener('click', () => {
                gameState.isPaused = false;
                planeContextMenu.classList.add('hidden');
            });

            planeBackToMenu.addEventListener('click', () => {
                returnToMenu();
                planeContextMenu.classList.add('hidden');
            });

            // 鼠标控制飞机
            planeCanvas.addEventListener('mousemove', (e) => {
                if (gameState.currentGame !== 'plane' || gameState.isGameOver) return;

                const rect = planeCanvas.getBoundingClientRect();
                const mouseX = e.clientX - rect.left;
                const mouseY = e.clientY - rect.top;

                // 限制飞机在画布内
                player.x = Math.max(0, Math.min(planeCanvas.width - player.width, mouseX - player.width / 2));
                player.y = Math.max(0, Math.min(planeCanvas.height - player.height, mouseY - player.height / 2));
            });

            // 鼠标左键发射
            planeCanvas.addEventListener('mousedown', (e) => {
                if (gameState.currentGame !== 'plane') return;

                if (e.button === 0) { // 左键
                    fireBullet();
                } else if (e.button === 2) { // 右键
                    e.preventDefault();
                    if (gameState.isGameOver) return;

                    // 显示右键菜单
                    const rect = planeCanvas.getBoundingClientRect();
                    const menuX = e.clientX - rect.left;
                    const menuY = e.clientY - rect.top;

                    planeContextMenu.style.left = `${menuX}px`;
                    planeContextMenu.style.top = `${menuY}px`;
                    planeContextMenu.classList.remove('hidden');

                    // 如果游戏不在暂停状态，点击右键暂停游戏
                    if (!gameState.isPaused) {
                        gameState.isPaused = true;
                    }
                }
            });

            // 点击其他地方关闭右键菜单
            document.addEventListener('click', (e) => {
                if (!planeContextMenu.contains(e.target) &&
                    e.target !== planeCanvas &&
                    e.button !== 2) {
                    planeContextMenu.classList.add('hidden');
                }
            });

            // 阻止右键菜单默认行为
            planeCanvas.addEventListener('contextmenu', (e) => {
                if (gameState.currentGame === 'plane' && !gameState.isGameOver) {
                    e.preventDefault();
                }
            });

            // 通用控制
            document.addEventListener('keydown', (e) => {
                if (gameState.isGameOver) return;

                if (['ArrowUp', 'ArrowDown', 'ArrowLeft', 'ArrowRight', ' ', 'w', 'a', 's', 'd', 'p'].includes(e.key)) {
                    e.preventDefault();
                }

                // 暂停/继续游戏
                if (e.key === 'p' && gameState.currentGame === 'plane') {
                    gameState.isPaused = !gameState.isPaused;
                    if (gameState.isPaused) {
                        // 显示菜单
                        const rect = planeCanvas.getBoundingClientRect();
                        const menuX = rect.width / 2;
                        const menuY = rect.height / 2;

                        planeContextMenu.style.left = `${menuX}px`;
                        planeContextMenu.style.top = `${menuY}px`;
                        planeContextMenu.classList.remove('hidden');
                    } else {
                        planeContextMenu.classList.add('hidden');
                    }
                }

                if (gameState.currentGame === 'snake' && !gameState.isPaused) {
                    switch(e.key) {
                        case 'ArrowUp':
                        case 'w':
                            if (snakeDirection !== 'down') {
                                snakeNextDirection = 'up';
                            }
                            break;
                        case 'ArrowDown':
                        case 's':
                            if (snakeDirection !== 'up') {
                                snakeNextDirection = 'down';
                            }
                            break;
                        case 'ArrowLeft':
                        case 'a':
                            if (snakeDirection !== 'right') {
                                snakeNextDirection = 'left';
                            }
                            break;
                        case 'ArrowRight':
                        case 'd':
                            if (snakeDirection !== 'left') {
                                snakeNextDirection = 'right';
                            }
                            break;
                        case 'p':
                            gameState.isPaused = !gameState.isPaused;
                            break;
                    }
                } else if (gameState.currentGame === 'plane' && !gameState.isPaused) {
                    // 飞机控制（键盘备用）
                    switch(e.key) {
                        case 'ArrowUp':
                        case 'w':
                            player.y = Math.max(0, player.y - player.speed);
                            break;
                        case 'ArrowDown':
                        case 's':
                            player.y = Math.min(
                                planeCanvas.height - player.height,
                                player.y + player.speed
                            );
                            break;
                        case 'ArrowLeft':
                        case 'a':
                            player.x = Math.max(0, player.x - player.speed);
                            break;
                        case 'ArrowRight':
                        case 'd':
                            player.x = Math.min(
                                planeCanvas.width - player.width,
                                player.x + player.speed
                            );
                            break;
                        case ' ':
                            fireBullet();
                            break;
                    }
                }
            });

            // 持续按键检测
            const keys = {};
            document.addEventListener('keydown', (e) => {
                keys[e.key] = true;
            });

            document.addEventListener('keyup', (e) => {
                keys[e.key] = false;
            });

            // 处理持续按键
            function handleContinuousKeys() {
                if (gameState.isGameOver || !gameState.currentGame || gameState.isPaused) return;

                if (gameState.currentGame === 'plane') {
                    if (keys['ArrowUp'] || keys['w']) {
                        player.y = Math.max(0, player.y - player.speed);
                    }
                    if (keys['ArrowDown'] || keys['s']) {
                        player.y = Math.min(
                            planeCanvas.height - player.height,
                            player.y + player.speed
                        );
                    }
                    if (keys['ArrowLeft'] || keys['a']) {
                        player.x = Math.max(0, player.x - player.speed);
                    }
                    if (keys['ArrowRight'] || keys['d']) {
                        player.x = Math.min(
                            planeCanvas.width - player.width,
                            player.x + player.speed
                        );
                    }
                    if (keys[' ']) {
                        fireBullet();
                    }
                }

                requestAnimationFrame(handleContinuousKeys);
            }

            // 触摸控制
            let touchStartX = 0;
            let touchStartY = 0;
            let touchMoveX = 0;
            let touchMoveY = 0;
            let isTouching = false;

            document.addEventListener('touchstart', (e) => {
                if (gameState.isGameOver || !gameState.currentGame || gameState.isPaused) return;

                touchStartX = e.touches[0].clientX;
                touchStartY = e.touches[0].clientY;
                touchMoveX = 0;
                touchMoveY = 0;
                isTouching = true;

                // 飞机游戏触摸发射子弹
                if (gameState.currentGame === 'plane') {
                    fireBullet();
                }

                e.preventDefault();
            }, { passive: false });

            document.addEventListener('touchmove', (e) => {
                if (gameState.isGameOver || !gameState.currentGame || !isTouching || gameState.isPaused) return;

                const touchX = e.touches[0].clientX;
                const touchY = e.touches[0].clientY;
                touchMoveX = touchX - touchStartX;
                touchMoveY = touchY - touchStartY;

                // 控制飞机移动
                if (gameState.currentGame === 'plane') {
                    const newX = player.x + touchMoveX * 0.1;
                    const newY = player.y + touchMoveY * 0.1;

                    player.x = Math.max(0, Math.min(planeCanvas.width - player.width, newX));
                    player.y = Math.max(0, Math.min(planeCanvas.height - player.height, newY));

                    touchStartX = touchX;
                    touchStartY = touchY;
                }

                e.preventDefault();
            }, { passive: false });

            document.addEventListener('touchend', (e) => {
                if (gameState.isGameOver || !gameState.currentGame) return;

                isTouching = false;

                // 贪吃蛇游戏触摸控制
                if (gameState.currentGame === 'snake' && !gameState.isPaused) {
                    if (Math.abs(touchMoveX) > Math.abs(touchMoveY)) {
                        if (touchMoveX > 50 && snakeDirection !== 'left') {
                            snakeNextDirection = 'right';
                        } else if (touchMoveX < -50 && snakeDirection !== 'right') {
                            snakeNextDirection = 'left';
                        }
                    } else {
                        if (touchMoveY > 50 && snakeDirection !== 'up') {
                            snakeNextDirection = 'down';
                        } else if (touchMoveY < -50 && snakeDirection !== 'down') {
                            snakeNextDirection = 'up';
                        }
                    }
                }

                e.preventDefault();
            }, { passive: false });

            // 启动持续按键检测
            handleContinuousKeys();
        });
    </script>
</body>
</html>
