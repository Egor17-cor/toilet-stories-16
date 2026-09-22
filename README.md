<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Туалетные истории 16 · марафон</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            user-select: none;
        }
        body {
            background: #1a1410;
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            font-family: 'Segoe UI', Roboto, system-ui, sans-serif;
            overflow: hidden;
        }
        .menu-overlay {
            position: fixed;
            inset: 0;
            z-index: 1000;
            background: #1a1410;
            display: flex;
            justify-content: center;
            align-items: center;
            transition: opacity 0.5s ease, visibility 0.5s ease;
        }
        .menu-overlay.hidden {
            opacity: 0;
            visibility: hidden;
            pointer-events: none;
        }
        .menu-bg {
            position: absolute;
            inset: 0;
            background: #1a1410;
            z-index: 0;
        }
        .menu-bg img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            opacity: 0.35;
            filter: blur(2px) brightness(0.7);
            display: block;
        }
        .menu-card {
            position: relative;
            z-index: 2;
            background: #2f241e;
            padding: 2.5rem 3rem 3rem;
            border-radius: 4rem 4rem 3rem 3rem;
            box-shadow: 0 30px 40px rgba(0,0,0,0.8), inset 0 -6px 0 #5e4b3b;
            text-align: center;
            max-width: 600px;
            width: 90%;
            transition: all 0.3s ease;
            border: 2px solid #6d5543;
            backdrop-filter: blur(4px);
            background: rgba(47, 36, 30, 0.88);
        }
        .menu-title {
            font-size: 3.2rem;
            font-weight: 800;
            color: #f5e6d3;
            text-shadow: 0 4px 0 #2d1f15, 0 8px 12px rgba(0,0,0,0.6);
            letter-spacing: 1px;
            margin-bottom: 0.5rem;
            line-height: 1.1;
        }
        .menu-sub {
            font-size: 1.2rem;
            color: #c9b09b;
            background: #3d2c1f;
            display: inline-block;
            padding: 0.2rem 2rem;
            border-radius: 40px;
            box-shadow: inset 0 -3px 0 #1e140e;
            margin-bottom: 2rem;
            letter-spacing: 2px;
        }
        .menu-emoji-row {
            font-size: 2.8rem;
            margin: 0.5rem 0 1.5rem;
            filter: drop-shadow(0 4px 6px #00000066);
        }
        .menu-btn {
            background: #c9b09b;
            border: none;
            color: #1d130e;
            font-weight: 700;
            font-size: 1.8rem;
            padding: 0.8rem 3rem;
            border-radius: 60px;
            cursor: pointer;
            box-shadow: 0 8px 0 #6d5543, 0 8px 20px rgba(0,0,0,0.5);
            transition: 0.06s linear;
            letter-spacing: 1px;
            width: 100%;
            max-width: 300px;
            margin: 0.5rem auto;
            display: block;
        }
        .menu-btn:active {
            transform: translateY(6px);
            box-shadow: 0 2px 0 #5d4533;
        }
        .menu-btn-secondary {
            background: #4d6b7a;
            color: #f2e3d0;
            box-shadow: 0 8px 0 #2d3f4a;
            font-size: 1.2rem;
            padding: 0.6rem 2rem;
            max-width: 200px;
        }
        .menu-btn-secondary:active {
            box-shadow: 0 2px 0 #2d3f4a;
        }
        .menu-btn-gold {
            background: #c9a84d;
            color: #1d130e;
            box-shadow: 0 8px 0 #8a6d2a;
            font-size: 1.5rem;
            padding: 0.7rem 2.5rem;
        }
        .menu-btn-gold:active {
            box-shadow: 0 2px 0 #8a6d2a;
        }
        .menu-btn-gold.locked {
            background: #5a4a3a;
            color: #8a7a6a;
            box-shadow: 0 8px 0 #3a2a1a;
            cursor: not-allowed;
            opacity: 0.6;
        }
        .menu-btn-gold.locked:active {
            transform: none;
            box-shadow: 0 8px 0 #3a2a1a;
        }
        .menu-footer {
            margin-top: 2rem;
            color: #8f765e;
            font-size: 0.85rem;
            border-top: 1px solid #4d3a2b;
            padding-top: 1.2rem;
        }
        .menu-footer span {
            background: #2b1f17;
            padding: 0.2rem 1rem;
            border-radius: 30px;
            display: inline-block;
        }
        .game-wrapper {
            background: #2f241e;
            padding: 1.5rem 2rem 2rem;
            border-radius: 3rem 3rem 2rem 2rem;
            box-shadow: 0 20px 30px rgba(0,0,0,0.7);
            transition: all 0.3s ease;
            width: fit-content;
            margin: 0 auto;
        }
        .game-wrapper.fullscreen {
            padding: 0.5rem;
            border-radius: 0;
            background: #1a1410;
            box-shadow: none;
            width: 100vw;
            height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
        }
        .game-wrapper.fullscreen .game-container {
            border-radius: 0;
            padding: 0.5rem;
            background: #b8a492;
            width: 100%;
            height: 100%;
            display: flex;
            flex-direction: column;
            justify-content: center;
        }
        .game-wrapper.fullscreen canvas {
            width: 100%;
            height: calc(100% - 80px);
            aspect-ratio: auto;
            border-radius: 1rem;
        }
        .game-wrapper.fullscreen .info-panel {
            margin: 0.5rem 0.2rem 0;
            font-size: 1.1rem;
        }
        .game-wrapper.fullscreen .room-badge {
            font-size: 1.1rem;
            padding: 0.2rem 1.2rem;
        }
        .game-wrapper.fullscreen .message-box {
            font-size: 1rem;
            min-width: 120px;
            padding: 0.2rem 1rem;
        }
        .game-wrapper.fullscreen button {
            font-size: 0.9rem;
            padding: 0.2rem 1rem;
        }
        .game-wrapper.fullscreen .progress-text {
            font-size: 0.85rem;
            padding: 0.1rem 0.8rem;
        }
        .game-container {
            background: #b8a492;
            padding: 1.2rem 1.2rem 1rem;
            border-radius: 2.5rem;
            box-shadow: inset 0 -6px 0 #5e4b3b;
            transition: all 0.3s ease;
        }
        canvas {
            display: block;
            width: 750px;
            height: 470px;
            border-radius: 1.8rem;
            background: #d6c3b0;
            box-shadow: 0 0 0 3px #4d3a2b, 0 10px 20px rgba(0,0,0,0.5);
            cursor: crosshair;
            transition: all 0.3s ease;
        }
        .info-panel {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin: 1rem 0.5rem 0.2rem;
            color: #f2e3d0;
            font-weight: 600;
            text-shadow: 0 2px 0 #2d1f15;
            letter-spacing: 0.3px;
            flex-wrap: wrap;
            gap: 0.5rem;
        }
        .room-badge {
            background: #3d2c1f;
            padding: 0.3rem 1.8rem;
            border-radius: 30px;
            font-size: 1.25rem;
            box-shadow: inset 0 -3px 0 #1e140e;
        }
        .message-box {
            background: #2b1f17;
            padding: 0.3rem 1.5rem;
            border-radius: 40px;
            font-size: 1.1rem;
            min-width: 150px;
            text-align: center;
            border: 1px solid #8f765e;
            color: #f5e6d3;
            box-shadow: inset 0 1px 3px #b89d84;
        }
        .button-group {
            display: flex;
            gap: 0.6rem;
            align-items: center;
        }
        button {
            background: #c9b09b;
            border: none;
            color: #1d130e;
            font-weight: 700;
            font-size: 1rem;
            padding: 0.3rem 1.2rem;
            border-radius: 40px;
            cursor: pointer;
            box-shadow: 0 5px 0 #6d5543, 0 4px 8px rgba(0,0,0,0.4);
            transition: 0.05s linear;
            letter-spacing: 0.3px;
            white-space: nowrap;
        }
        button:active {
            transform: translateY(4px);
            box-shadow: 0 1px 0 #5d4533;
        }
        button:disabled {
            opacity: 0.4;
            transform: translateY(4px);
            box-shadow: 0 1px 0 #5d4533;
            pointer-events: none;
        }
        .footer {
            display: flex;
            gap: 0.8rem;
            align-items: center;
            flex-wrap: wrap;
        }
        .progress-text {
            font-size: 0.95rem;
            background: #2b1f17;
            padding: 0.2rem 1.2rem;
            border-radius: 30px;
            border: 1px solid #7a6450;
        }
        .fullscreen-btn {
            background: #4d6b7a;
            color: #f2e3d0;
            box-shadow: 0 5px 0 #2d3f4a;
            font-size: 0.9rem;
            padding: 0.3rem 1rem;
        }
        .fullscreen-btn:active {
            box-shadow: 0 1px 0 #2d3f4a;
        }
        .search-btn {
            background: #4d7a6b;
            color: #f2e3d0;
            box-shadow: 0 5px 0 #2d4a3f;
            font-size: 0.9rem;
            padding: 0.3rem 1rem;
        }
        .search-btn:active {
            box-shadow: 0 1px 0 #2d4a3f;
        }
        .search-btn.active {
            background: #7a4d6b;
            box-shadow: 0 5px 0 #4a2d3f;
        }
        .menu-btn-exit {
            background: #6b4d4d;
            color: #f2e3d0;
            box-shadow: 0 5px 0 #3a2d2d;
            font-size: 0.9rem;
            padding: 0.3rem 1rem;
        }
        .menu-btn-exit:active {
            box-shadow: 0 1px 0 #3a2d2d;
        }
        @media (max-width: 800px) {
            .game-wrapper { padding: 0.8rem; }
            canvas { width: 100%; height: auto; aspect-ratio: 750/470; }
            .info-panel { flex-direction: column; align-items: stretch; }
            .message-box { min-width: auto; }
            .menu-title { font-size: 2.4rem; }
            .menu-card { padding: 2rem 1.5rem; }
        }
    </style>
</head>
<body>

<!-- ГЛАВНОЕ МЕНЮ (оверлей) с фоном -->
<div class="menu-overlay" id="menuOverlay">
    <div class="menu-bg">
        <img src="https://avatars.mds.yandex.net/i?id=951eebf924a7f83492136f485a193c73_l-5496696-images-thumbs&png" alt="фон меню" crossorigin="anonymous">
    </div>
    <div class="menu-card">
        <div class="menu-title">🚽 ТУАЛЕТНЫЕ<br>ИСТОРИИ 16</div>
        <div class="menu-sub">🔍 найди все аномалии</div>
        <div class="menu-emoji-row">🧻👻🚽🕵️</div>
        <button class="menu-btn" id="startGameBtn">▶ ИГРАТЬ (16)</button>
        <button class="menu-btn menu-btn-gold locked" id="marathonBtn" disabled>🔒 МАРАФОН (64)</button>
        <button class="menu-btn menu-btn-secondary" id="resetGameBtn">⟳ Заново</button>
        <div class="menu-footer">
            <span id="marathonStatus">🧼 Пройдите 16 комнат, чтобы открыть марафон</span>
        </div>
    </div>
</div>

<!-- ИГРОВОЙ КОНТЕЙНЕР -->
<div class="game-wrapper" id="gameWrapper">
    <div class="game-container">
        <canvas id="gameCanvas" width="750" height="470"></canvas>
        <div class="info-panel">
            <div class="room-badge" id="roomDisplay">🚽 1 / 16</div>
            <div class="message-box" id="messageDisplay">🔍 Осмотрись</div>
            <div class="footer">
                <span class="progress-text" id="progressDisplay">0/16</span>
                <div class="button-group">
                    <button id="searchButton" class="search-btn">🔎 Обзор</button>
                    <button id="fullscreenButton" class="fullscreen-btn">⛶</button>
                    <button id="backButton">◀</button>
                    <button id="actionButton">➡️</button>
                    <button id="exitToMenuButton" class="menu-btn-exit">🏠 Меню</button>
                </div>
            </div>
        </div>
    </div>
</div>

<script>
    (function(){
        const menuOverlay = document.getElementById('menuOverlay');
        const startBtn = document.getElementById('startGameBtn');
        const resetBtn = document.getElementById('resetGameBtn');
        const marathonBtn = document.getElementById('marathonBtn');
        const marathonStatus = document.getElementById('marathonStatus');
        const exitToMenuBtn = document.getElementById('exitToMenuButton');

        const canvas = document.getElementById('gameCanvas');
        const ctx = canvas.getContext('2d');
        const gameWrapper = document.getElementById('gameWrapper');

        const roomDisplay = document.getElementById('roomDisplay');
        const messageDisplay = document.getElementById('messageDisplay');
        const progressDisplay = document.getElementById('progressDisplay');
        const actionBtn = document.getElementById('actionButton');
        const backBtn = document.getElementById('backButton');
        const fullscreenBtn = document.getElementById('fullscreenButton');
        const searchBtn = document.getElementById('searchButton');

        let MAX_ROOMS = 16;
        let currentRoom = 1;
        let hasAnomaly = false;
        let anomalyType = 0;
        let gameFinished = false;
        let isFullscreen = false;
        let animFrameId = null;
        let time = 0;
        let isSearching = false;
        let isMarathon = false;
        let marathonUnlocked = false;
        let epicEnding = false;
        let epicTime = 0;

        let anomalyData = {
            offsetX: 0, offsetY: 0, rotation: 0, scale: 1,
            flicker: 0, pulse: 0, floatOffset: 0, speed: 1,
            alpha: 1, glowIntensity: 0
        };

        // ------ ЗВУКИ ------
        const audioCtx = new (window.AudioContext || window.webkitAudioContext)();
        let musicInterval = null;

        function playBeep(freq, duration, vol = 0.3) {
            try {
                const osc = audioCtx.createOscillator();
                const gain = audioCtx.createGain();
                osc.type = 'sawtooth';
                osc.frequency.value = freq;
                gain.gain.value = vol;
                gain.gain.exponentialRampToValueAtTime(0.001, audioCtx.currentTime + duration);
                osc.connect(gain);
                gain.connect(audioCtx.destination);
                osc.start();
                osc.stop(audioCtx.currentTime + duration);
            } catch(e) {}
        }

        function playEpicMusic() {
            if (musicInterval) {
                clearInterval(musicInterval);
                musicInterval = null;
            }
            const notes = [523, 587, 659, 784, 880, 988, 1175];
            let noteIndex = 0;
            musicInterval = setInterval(() => {
                const note = notes[noteIndex % notes.length];
                const vol = 0.15 + Math.sin(noteIndex * 0.5) * 0.05;
                playBeep(note, 0.15, vol);
                if (noteIndex % 2 === 0) {
                    setTimeout(() => playBeep(note * 1.25, 0.1, vol * 0.6), 80);
                }
                noteIndex++;
                if (noteIndex > 60) {
                    noteIndex = 0;
                }
            }, 180);
        }

        function stopEpicMusic() {
            if (musicInterval) {
                clearInterval(musicInterval);
                musicInterval = null;
            }
        }

        function playScareSound() {
            for (let i = 0; i < 3; i++) {
                setTimeout(() => playBeep(400 + i * 200, 0.15, 0.4), i * 80);
            }
            setTimeout(() => playBeep(900, 0.3, 0.5), 200);
        }

        function playAlertSound() {
            playBeep(600, 0.2, 0.25);
            setTimeout(() => playBeep(800, 0.2, 0.25), 150);
            setTimeout(() => playBeep(600, 0.3, 0.3), 300);
        }

        function playToiletPaperSound() {
            playBeep(300, 0.1, 0.2);
            setTimeout(() => playBeep(350, 0.1, 0.2), 100);
            setTimeout(() => playBeep(400, 0.15, 0.2), 200);
        }

        function playSearchSound() {
            playBeep(440, 0.1, 0.15);
            setTimeout(() => playBeep(550, 0.1, 0.15), 100);
        }

        function playUnlockSound() {
            playBeep(523, 0.15, 0.3);
            setTimeout(() => playBeep(659, 0.15, 0.3), 120);
            setTimeout(() => playBeep(784, 0.2, 0.4), 240);
        }

        // ------ ИЗОБРАЖЕНИЯ ------
        const images = {
            toilet: new Image(),
            anomaly1: new Image(),
            anomaly2: new Image(),
            anomaly3: new Image(),
            anomaly4: new Image(),
            anomaly5: new Image(),
            anomaly6: new Image(),
            anomaly7: new Image(),
            anomaly8: new Image(),
            anomaly9: new Image(),
            anomaly10: new Image(),
            anomaly11: new Image(),
            anomaly12: new Image(),
            anomaly13: new Image(),
            windi31: new Image()
        };

        images.toilet.src = 'https://static.vecteezy.com/system/resources/previews/000/519/306/original/a-clean-toilet-background-vector.jpg';
        images.anomaly1.src = 'https://image.pngaaa.com/761/4327761-middle.png';
        images.anomaly2.src = 'https://avatars.mds.yandex.net/i?id=9404987bc83ab6f267bd40078dbd57bf_l-5210109-images-thumbs&png';
        images.anomaly3.src = 'https://static.wikia.nocookie.net/fridaynightfunking/images/3/3b/TakeoverSkibidiLeft.gif/revision/latest/scale-to-width-down/115?cb=20230728024954';
        images.anomaly4.src = 'https://www.clipartmax.com/png/full/400-4004703_poocrew-your-yard-cleaned-of-poop-quick-and-easy-clip-poocrew-your.png';
        images.anomaly5.src = 'https://avatars.mds.yandex.net/i?id=f44c9f9c09ed35031f4a57ee3985f1a0_l-4825130-images-thumbs&ref=rim&n=13&w=800&png';
        images.anomaly6.src = 'https://static.vecteezy.com/system/resources/previews/040/323/643/non_2x/ai-generated-black-garbage-bag-trash-bag-on-transparent-background-free-png.png';
        images.anomaly7.src = 'https://image.pngaaa.com/761/4327761-middle.png';
        images.anomaly8.src = 'https://cdn.icon-icons.com/icons2/2070/PNG/512/toilet_icon_126466.png';
        images.anomaly9.src = 'https://i.pinimg.com/736x/8c/24/2f/8c242f29e7c25756ea2bcb78a54a3e80.jpg';
        images.anomaly10.src = 'https://image.made-in-china.com/2f0j00RSiWvjJPGBkm/Pink-Color-Embossed-Virgin-Toilet-Tissue-2ply-Pink-Toilet-Paper-Roll-Soft-Factory-Price-Wholesale-Toilet-Tissue.png';
        images.anomaly11.src = 'https://avatars.mds.yandex.net/i?id=f557b5b577e2ffcdd2919dbcfdd06ab3_l-4590062-images-thumbs&png';
        images.anomaly12.src = 'https://avatars.mds.yandex.net/i?id=b7aafbe3ae97c0c5f6b58e5ba8273a2d_l-5294324-images-thumbs&png';
        images.anomaly13.src = 'https://static.vecteezy.com/system/resources/previews/048/081/951/non_2x/red-siren-light-warning-sign-police-alarm-ambulance-alarm-cartoon-illustration-vector.jpg';
        images.windi31.src = 'https://pic.rtbcdn.ru/user/b5/87/b587ecd7a3492734866ee096fc1186c9.jpg';

        const ANOMALY_TYPES = 13;
        let roomAnomalyMap = [];
        let windiRooms = [];
        let anomalyFound = [];

        function initMaps() {
            roomAnomalyMap = new Array(MAX_ROOMS + 1).fill(0);
            windiRooms = new Array(MAX_ROOMS + 1).fill(false);
            anomalyFound = new Array(MAX_ROOMS + 1).fill(false);
        }

        // ----- ГЕНЕРАЦИЯ АНОМАЛИЙ (увеличенный рандом) -----
        function generateAnomalies() {
            initMaps();
            // Больше вариаций количества аномалий (от 25% до 55% комнат)
            const totalAnomalies = Math.floor(MAX_ROOMS * (0.25 + Math.random() * 0.3));
            let placed = 0, attempts = 0;

            while (placed < totalAnomalies && attempts < 3000) {
                attempts++;
                const room = Math.floor(Math.random() * MAX_ROOMS) + 1;
                if (roomAnomalyMap[room] !== 0) continue;

                // Случайные проверки на соседние аномалии (более гибкие)
                let leftStreak = 0, temp = room - 1;
                while (temp >= 1 && roomAnomalyMap[temp] !== 0) { leftStreak++; temp--; }
                let rightStreak = 0; temp = room + 1;
                while (temp <= MAX_ROOMS && roomAnomalyMap[temp] !== 0) { rightStreak++; temp++; }

                // Максимум 3 аномалии подряд (вместо 2)
                if (leftStreak >= 3 || rightStreak >= 3) continue;

                // Случайный шанс пропуска (добавляем больше хаоса)
                if (Math.random() < 0.15) continue;

                roomAnomalyMap[room] = Math.floor(Math.random() * ANOMALY_TYPES) + 1;
                placed++;
            }

            // Коррекция: удаляем 4+ подряд
            for (let i = 1; i <= MAX_ROOMS - 3; i++) {
                if (roomAnomalyMap[i] !== 0 && roomAnomalyMap[i+1] !== 0 && 
                    roomAnomalyMap[i+2] !== 0 && roomAnomalyMap[i+3] !== 0) {
                    roomAnomalyMap[i+1] = 0;
                    roomAnomalyMap[i+2] = 0;
                }
            }
            
            // Убеждаемся, что есть хотя бы несколько аномалий
            let count = 0;
            for (let i = 1; i <= MAX_ROOMS; i++) if (roomAnomalyMap[i] !== 0) count++;
            
            // Если аномалий слишком мало или слишком много - корректируем
            const minAnomalies = Math.floor(MAX_ROOMS * 0.15);
            const maxAnomalies = Math.floor(MAX_ROOMS * 0.55);
            
            if (count < minAnomalies) {
                const needed = minAnomalies - count;
                let added = 0;
                for (let i = 1; i <= MAX_ROOMS && added < needed; i++) {
                    if (roomAnomalyMap[i] === 0) {
                        let left = (i > 1 && roomAnomalyMap[i-1] !== 0);
                        let right = (i < MAX_ROOMS && roomAnomalyMap[i+1] !== 0);
                        // Проверяем на 3 подряд
                        let left2 = (i > 2 && roomAnomalyMap[i-2] !== 0);
                        let right2 = (i < MAX_ROOMS-1 && roomAnomalyMap[i+2] !== 0);
                        if (!left || !right || !(left && right2) || !(right && left2)) {
                            roomAnomalyMap[i] = Math.floor(Math.random() * ANOMALY_TYPES) + 1;
                            added++;
                        }
                    }
                }
            } else if (count > maxAnomalies) {
                // Удаляем лишние аномалии случайно
                const toRemove = count - maxAnomalies;
                let removed = 0;
                const rooms = [];
                for (let i = 1; i <= MAX_ROOMS; i++) {
                    if (roomAnomalyMap[i] !== 0) rooms.push(i);
                }
                // Перемешиваем и удаляем
                for (let i = rooms.length - 1; i > 0; i--) {
                    const j = Math.floor(Math.random() * (i + 1));
                    [rooms[i], rooms[j]] = [rooms[j], rooms[i]];
                }
                for (let i = 0; i < Math.min(toRemove, rooms.length); i++) {
                    roomAnomalyMap[rooms[i]] = 0;
                }
            }
        }

        function generateWindiRooms() {
            // Больше рандома для Винди
            for (let i = 1; i <= MAX_ROOMS; i++) {
                windiRooms[i] = Math.random() < (0.2 + Math.random() * 0.3);
            }
            let hasWindi = false;
            for (let i = 1; i <= MAX_ROOMS; i++) if (windiRooms[i]) { hasWindi = true; break; }
            if (!hasWindi) {
                const room = Math.floor(Math.random() * MAX_ROOMS) + 1;
                windiRooms[room] = true;
                // Может быть несколько Винди
                if (Math.random() < 0.3) {
                    const room2 = Math.floor(Math.random() * MAX_ROOMS) + 1;
                    if (room2 !== room) windiRooms[room2] = true;
                }
            }
        }

        function updateUI() {
            roomDisplay.textContent = `🚽 ${currentRoom} / ${MAX_ROOMS}`;
            progressDisplay.textContent = `${currentRoom-1}/${MAX_ROOMS}`;
            
            if (epicEnding) {
                messageDisplay.textContent = '🌟 ГИПЕР ЭПИК КОНЦОВКА! 🌟';
                actionBtn.disabled = true;
                backBtn.disabled = true;
                searchBtn.disabled = true;
                exitToMenuBtn.style.display = 'inline-block';
                return;
            }
            
            if (gameFinished) {
                messageDisplay.textContent = isMarathon ? '🏆 МАРАФОН ПРОЙДЕН!' : '🏆 ПОБЕДА!';
                actionBtn.disabled = true;
                backBtn.disabled = true;
                actionBtn.textContent = '🏁';
                backBtn.textContent = '◀';
                searchBtn.disabled = true;
                exitToMenuBtn.style.display = 'inline-block';
                return;
            }
            actionBtn.disabled = false;
            backBtn.disabled = false;
            searchBtn.disabled = false;
            exitToMenuBtn.style.display = 'none';
            actionBtn.textContent = '➡️';
            backBtn.textContent = '◀';
            
            if (hasAnomaly) {
                if (anomalyFound[currentRoom]) {
                    messageDisplay.textContent = '✅ АНОМАЛИЯ НАЙДЕНА!';
                } else {
                    messageDisplay.textContent = '🔍 ИЩИ АНОМАЛИЮ';
                }
            } else {
                messageDisplay.textContent = '✅ ЧИСТО';
            }
        }

        // ----- УЛУЧШЕННАЯ АНИМАЦИЯ АНОМАЛИЙ С БОЛЬШИМ РАНДОМОМ -----
        function updateAnomalyAnimation() {
            if (!hasAnomaly || gameFinished || epicEnding) return;
            
            // Базовая скорость с большим рандомом
            const baseSpeed = 0.015 + Math.random() * 0.035;
            time += baseSpeed;
            
            // Разные частоты для разных осей (больше рандома)
            const freqX = 0.4 + Math.random() * 1.2;
            const freqY = 0.5 + Math.random() * 1.4;
            const freqRot = 0.3 + Math.random() * 0.9;
            const freqScale = 0.6 + Math.random() * 1.6;
            const freqAlpha = 0.8 + Math.random() * 2.5;
            
            // Амплитуды с рандомом
            const ampX = 15 + Math.random() * 35;
            const ampY = 10 + Math.random() * 30;
            const ampRot = 0.15 + Math.random() * 0.5;
            const ampScale = 0.05 + Math.random() * 0.25;
            
            anomalyData.floatOffset = Math.sin(time * 1.2 + Math.random() * 0.5) * (10 + Math.random() * 15);
            anomalyData.offsetX = Math.sin(time * freqX + Math.random() * 2) * ampX;
            anomalyData.offsetY = Math.sin(time * freqY + Math.random() * 2 + 1) * ampY + anomalyData.floatOffset * (0.2 + Math.random() * 0.3);
            anomalyData.rotation = Math.sin(time * freqRot + Math.random() * 3) * ampRot;
            anomalyData.pulse = (0.8 + Math.random() * 0.2) + Math.sin(time * freqScale + Math.random() * 2) * ampScale;
            anomalyData.scale = anomalyData.pulse;
            anomalyData.flicker = 0.3 + Math.sin(time * freqAlpha + Math.random() * 4) * (0.2 + Math.random() * 0.2);
            anomalyData.alpha = 0.3 + Math.sin(time * (0.5 + Math.random() * 2) + Math.random() * 3) * 0.25;
            
            // Специфичные анимации для разных типов (с рандомом)
            if (anomalyType === 9) {
                anomalyData.offsetY = Math.sin(time * (0.8 + Math.random() * 0.6)) * (8 + Math.random() * 15);
                anomalyData.scale = 0.85 + Math.sin(time * (0.5 + Math.random() * 0.8)) * (0.05 + Math.random() * 0.15);
                anomalyData.rotation = Math.sin(time * (0.3 + Math.random() * 0.5) + Math.random() * 2) * (0.1 + Math.random() * 0.3);
            } else if (anomalyType === 10) {
                anomalyData.offsetX = Math.sin(time * (1.5 + Math.random() * 1.5)) * (20 + Math.random() * 30);
                anomalyData.rotation = Math.sin(time * (1.0 + Math.random() * 1.2) + Math.random() * 2) * (0.3 + Math.random() * 0.4);
                anomalyData.offsetY = Math.sin(time * (1.0 + Math.random() * 1.0) + Math.random() * 2) * (10 + Math.random() * 20);
            } else if (anomalyType === 11) {
                anomalyData.offsetX = Math.sin(time * (0.5 + Math.random() * 0.8)) * (30 + Math.random() * 50);
                anomalyData.offsetY = Math.sin(time * (0.7 + Math.random() * 1.0) + Math.random() * 2) * (20 + Math.random() * 30);
                anomalyData.scale = 0.7 + Math.sin(time * (0.6 + Math.random() * 0.8) + Math.random() * 2) * (0.15 + Math.random() * 0.25);
                anomalyData.rotation = Math.sin(time * (0.4 + Math.random() * 0.6) + Math.random() * 3) * (0.3 + Math.random() * 0.5);
            } else if (anomalyType === 12) {
                anomalyData.offsetX = Math.sin(time * (1.0 + Math.random() * 1.2)) * (25 + Math.random() * 40);
                anomalyData.offsetY = Math.cos(time * (1.2 + Math.random() * 1.4) + Math.random() * 2) * (15 + Math.random() * 30);
                anomalyData.rotation = Math.sin(time * (1.5 + Math.random() * 1.5) + Math.random() * 3) * (0.2 + Math.random() * 0.4);
            } else if (anomalyType === 13) {
                anomalyData.pulse = 0.5 + Math.sin(time * (3.0 + Math.random() * 2.0) + Math.random() * 3) * (0.3 + Math.random() * 0.2);
                anomalyData.scale = anomalyData.pulse;
                anomalyData.offsetX = Math.sin(time * (0.3 + Math.random() * 0.4) + Math.random() * 2) * (5 + Math.random() * 15);
                anomalyData.offsetY = Math.sin(time * (0.3 + Math.random() * 0.4) + Math.random() * 2 + 1) * (5 + Math.random() * 15);
                anomalyData.alpha = 0.4 + Math.sin(time * (3.0 + Math.random() * 3.0) + Math.random() * 4) * 0.3;
            } else if (anomalyType === 7) {
                // Для множественных аномалий - свой рандом
                anomalyData.offsetX = Math.sin(time * 0.5 + Math.random() * 2) * (10 + Math.random() * 20);
                anomalyData.offsetY = Math.sin(time * 0.6 + Math.random() * 2 + 1) * (10 + Math.random() * 20);
            } else {
                // Общая анимация для остальных типов
                anomalyData.offsetX = Math.sin(time * (0.5 + Math.random() * 0.8) + Math.random() * 2) * (15 + Math.random() * 25);
                anomalyData.offsetY = Math.sin(time * (0.6 + Math.random() * 0.9) + Math.random() * 2 + 1) * (10 + Math.random() * 20);
                anomalyData.rotation = Math.sin(time * (0.4 + Math.random() * 0.6) + Math.random() * 3) * (0.2 + Math.random() * 0.3);
                anomalyData.scale = 0.85 + Math.sin(time * (0.6 + Math.random() * 1.0) + Math.random() * 2) * (0.05 + Math.random() * 0.15);
            }
            
            // Случайные "всплески" анимации
            if (Math.random() < 0.01) {
                anomalyData.offsetX += (Math.random() - 0.5) * 40;
                anomalyData.offsetY += (Math.random() - 0.5) * 30;
            }
        }

        function drawEpicEnding() {
            epicTime += 0.02;
            
            const gradient = ctx.createLinearGradient(0, 0, 750, 470);
            const hue1 = (epicTime * 30) % 360;
            const hue2 = (epicTime * 30 + 120) % 360;
            const hue3 = (epicTime * 30 + 240) % 360;
            gradient.addColorStop(0, `hsl(${hue1}, 80%, 50%)`);
            gradient.addColorStop(0.5, `hsl(${hue2}, 80%, 50%)`);
            gradient.addColorStop(1, `hsl(${hue3}, 80%, 50%)`);
            ctx.fillStyle = gradient;
            ctx.fillRect(0, 0, 750, 470);

            const allTypes = [1,2,3,4,5,6,7,8,9,10,11,12,13];
            allTypes.forEach((type, idx) => {
                const angle = epicTime * 0.5 + idx * 2.1 + Math.sin(epicTime * 0.2 + idx) * 0.5;
                const radius = 120 + Math.sin(epicTime * 0.3 + idx * 0.7) * 60;
                const px = 375 + Math.cos(angle) * radius;
                const py = 235 + Math.sin(angle * 0.7 + epicTime * 0.2 + idx * 0.3) * radius * 0.6;
                const size = 50 + Math.sin(epicTime + idx * 0.5) * 15 + Math.random() * 5;
                const imgKey = `anomaly${type}`;
                if (images[imgKey] && images[imgKey].complete && images[imgKey].naturalWidth > 0) {
                    ctx.save();
                    ctx.globalAlpha = 0.6 + Math.sin(epicTime * 2 + idx * 0.7) * 0.3;
                    ctx.translate(px, py);
                    ctx.rotate(epicTime * 0.2 + idx * 0.3 + Math.sin(epicTime * 0.1 + idx) * 0.2);
                    ctx.shadowColor = `hsl(${epicTime * 50 + idx * 30}, 100%, 60%)`;
                    ctx.shadowBlur = 30 + Math.sin(epicTime + idx) * 10;
                    ctx.drawImage(images[imgKey], -size/2, -size/2, size, size);
                    ctx.restore();
                }
            });

            ctx.save();
            ctx.textAlign = 'center';
            ctx.shadowColor = 'rgba(0,0,0,0.8)';
            ctx.shadowBlur = 20;
            
            const glow = 0.7 + Math.sin(epicTime * 2) * 0.3;
            ctx.fillStyle = `rgba(255, 215, 0, ${glow})`;
            ctx.font = 'bold 60px sans-serif';
            ctx.fillText('🌟 ГИПЕР ЭПИК 🌟', 375, 100);
            
            ctx.fillStyle = `rgba(255, 255, 255, ${0.5 + Math.sin(epicTime * 1.5) * 0.3})`;
            ctx.font = 'bold 36px sans-serif';
            ctx.fillText('ВСЕ АНОМАЛИИ СОБРАНЫ!', 375, 170);
            
            ctx.fillStyle = `rgba(255, 200, 100, ${0.6 + Math.sin(epicTime * 1.2) * 0.2})`;
            ctx.font = 'bold 28px sans-serif';
            ctx.fillText(`🚽 ${MAX_ROOMS} КОМНАТ ПРОЙДЕНО! 🏆`, 375, 230);
            
            ctx.fillStyle = `rgba(255, 150, 255, ${0.5 + Math.sin(epicTime * 0.8) * 0.2})`;
            ctx.font = 'bold 22px sans-serif';
            ctx.fillText('✨ ТЫ ЛЕГЕНДА! ✨', 375, 300);
            
            ctx.fillStyle = `rgba(200, 255, 200, ${0.4 + Math.sin(epicTime * 0.6) * 0.2})`;
            ctx.font = '18px sans-serif';
            ctx.fillText('Нажми "Меню" чтобы выйти в главное меню', 375, 380);
            
            ctx.restore();

            for (let i = 0; i < 40; i++) {
                const sx = (i * 137 + epicTime * 20 + Math.sin(i * 0.5) * 30) % 750;
                const sy = (i * 251 + epicTime * 15 + Math.sin(i * 0.7) * 50) % 470;
                const ss = 2 + Math.sin(epicTime * 3 + i * 0.5) * 2.5;
                ctx.fillStyle = `rgba(255, 255, 255, ${0.2 + Math.sin(epicTime * 2 + i * 0.3) * 0.2})`;
                ctx.beginPath();
                ctx.arc(sx, sy, ss, 0, Math.PI * 2);
                ctx.fill();
            }
        }

        function drawRoom() {
            if (epicEnding) {
                drawEpicEnding();
                return;
            }

            ctx.clearRect(0, 0, 750, 470);
            if (images.toilet.complete && images.toilet.naturalWidth > 0) {
                ctx.drawImage(images.toilet, 0, 0, 750, 470);
            } else {
                ctx.fillStyle = '#b5a186';
                ctx.fillRect(0, 0, 750, 470);
                ctx.fillStyle = '#7f6a55';
                ctx.font = 'bold 28px sans-serif';
                ctx.fillText('🚽 ТУАЛЕТ', 280, 240);
            }
            
            if (windiRooms[currentRoom] && images.windi31.complete && images.windi31.naturalWidth > 0) {
                ctx.save();
                const picSize = 70, picX = 10, picY = 25;
                ctx.shadowColor = 'rgba(0,0,0,0.5)';
                ctx.shadowBlur = 15;
                ctx.fillStyle = '#8d6e63';
                ctx.fillRect(picX - 5, picY - 5, picSize + 10, picSize + 10);
                ctx.shadowBlur = 0;
                ctx.drawImage(images.windi31, picX, picY, picSize, picSize);
                ctx.fillStyle = '#f5e6d3';
                ctx.font = 'bold 12px sans-serif';
                ctx.textAlign = 'center';
                ctx.shadowColor = 'rgba(0,0,0,0.8)';
                ctx.shadowBlur = 8;
                ctx.fillText('ВИНДИ 31', picX + picSize/2, picY + picSize + 18);
                ctx.font = 'bold 9px sans-serif';
                ctx.fillStyle = '#ffd54f';
                ctx.shadowColor = 'rgba(0,0,0,0.9)';
                ctx.shadowBlur = 10;
                ctx.fillText('❤️ ЛЮБЛЮ СМОТРЕТЬ', picX + picSize/2, picY + picSize + 34);
                ctx.fillText('ВИНДИ 31 ❤️', picX + picSize/2, picY + picSize + 46);
                ctx.shadowBlur = 0;
                ctx.textAlign = 'start';
                ctx.restore();
            }
            
            if (hasAnomaly && !gameFinished) {
                const isFound = anomalyFound[currentRoom];
                const isRevealed = isSearching || isFound;
                
                if (isRevealed) {
                    let imgToDraw = null;
                    let baseSize = 110;
                    let size = baseSize * anomalyData.scale;
                    let x = 750/2 - size/2 + anomalyData.offsetX;
                    let y = 470/2 - size/2 + 10 + anomalyData.offsetY;
                    let extraText = '';

                    switch (anomalyType) {
                        case 1: imgToDraw = images.anomaly1; break;
                        case 2: imgToDraw = images.anomaly2; break;
                        case 3: imgToDraw = images.anomaly3; break;
                        case 4: imgToDraw = images.anomaly4; break;
                        case 5: imgToDraw = images.anomaly5; break;
                        case 6: imgToDraw = images.anomaly6; break;
                        case 7: imgToDraw = images.anomaly7; break;
                        case 8: imgToDraw = images.anomaly8; break;
                        case 9: 
                            imgToDraw = images.anomaly9; 
                            extraText = 'Это я тебе';
                            baseSize = 80;
                            size = baseSize * anomalyData.scale;
                            x = 750/2 - size/2 + anomalyData.offsetX;
                            y = 470/2 - size/2 - 10 + anomalyData.offsetY;
                            break;
                        case 10: 
                            imgToDraw = images.anomaly10; 
                            baseSize = 90;
                            size = baseSize * anomalyData.scale;
                            x = 750/2 - size/2 + anomalyData.offsetX;
                            y = 470/2 - size/2 + 10 + anomalyData.offsetY;
                            break;
                        case 11: 
                            imgToDraw = images.anomaly11; 
                            baseSize = 130;
                            size = baseSize * anomalyData.scale;
                            x = 750/2 - size/2 + anomalyData.offsetX;
                            y = 470/2 - size/2 + 10 + anomalyData.offsetY;
                            break;
                        case 12: 
                            imgToDraw = images.anomaly12; 
                            baseSize = 80;
                            size = baseSize * anomalyData.scale;
                            x = 750/2 - size/2 + anomalyData.offsetX;
                            y = 470/2 - size/2 + 10 + anomalyData.offsetY;
                            break;
                        case 13: 
                            imgToDraw = images.anomaly13; 
                            baseSize = 100;
                            size = baseSize * anomalyData.scale;
                            x = 750/2 - size/2 + anomalyData.offsetX;
                            y = 470/2 - size/2 + 10 + anomalyData.offsetY;
                            break;
                        default: break;
                    }

                    if (anomalyType === 7) {
                        size = 40;
                        const count = 6 + Math.floor(Math.sin(time * 0.5 + Math.random() * 0.2) * 3);
                        for (let i = 0; i < count; i++) {
                            const angle = time * (2.0 + Math.random() * 1.0) + i * (1.5 + Math.random() * 0.6);
                            const dist = 50 + Math.sin(time * 0.5 + i * 0.3 + Math.random() * 0.2) * 40;
                            const px = 750/2 + Math.cos(angle + time * (0.3 + Math.random() * 0.3)) * dist + anomalyData.offsetX * (0.3 + Math.random() * 0.4);
                            const py = 470/2 + Math.sin(angle * (1.1 + Math.random() * 0.3) + time * (0.8 + Math.random() * 0.4) + i * 0.2) * dist * 0.5 + Math.sin(time * 2 + i + Math.random() * 0.5) * 25 + anomalyData.offsetY * (0.3 + Math.random() * 0.4);
                            if (images.anomaly7.complete && images.anomaly7.naturalWidth > 0) {
                                const s = 20 + Math.sin(time + i * 0.5 + Math.random() * 0.2) * 12;
                                let alpha = 0.2 + Math.sin(time * 1.2 + i * 0.5 + Math.random() * 0.2) * 0.2;
                                if (!isFound && isSearching) alpha *= 0.5;
                                ctx.globalAlpha = Math.max(0.1, Math.min(0.8, alpha));
                                ctx.drawImage(images.anomaly7, px - s/2, py - s/2, s, s);
                            }
                        }
                        ctx.globalAlpha = 1.0;
                        return;
                    }

                    if (imgToDraw && imgToDraw.complete && imgToDraw.naturalWidth > 0) {
                        let alpha = 0.3 + Math.sin(time * (1.5 + Math.random() * 1.5) + anomalyType * 1.2 + Math.random() * 0.5) * 0.3;
                        if (anomalyType === 3 || anomalyType === 4) {
                            alpha = 0.35 + Math.sin(time * (1.2 + Math.random() * 0.8) + anomalyType * 1.5 + Math.random() * 0.5) * 0.25;
                        }
                        if (anomalyType === 13) {
                            alpha = 0.4 + Math.sin(time * (2.0 + Math.random() * 2.0) + Math.random() * 2) * 0.3;
                        }
                        if (!isFound && isSearching) {
                            alpha *= 0.2 + Math.random() * 0.15;
                            ctx.globalAlpha = Math.max(0.05, Math.min(0.35, alpha));
                            ctx.shadowBlur = 0;
                        } else if (isFound) {
                            ctx.globalAlpha = Math.max(0.2, Math.min(0.9, alpha));
                            if (anomalyType !== 5 && anomalyType !== 6 && anomalyType !== 10) {
                                ctx.shadowColor = `rgba(255, 0, 0, ${0.05 + Math.random() * 0.15})`;
                                ctx.shadowBlur = 10 + Math.sin(time * 1.2 + Math.random() * 0.5) * 15;
                            }
                        } else {
                            ctx.globalAlpha = 0;
                        }
                        
                        ctx.save();
                        ctx.translate(x + size/2, y + size/2);
                        ctx.rotate(anomalyData.rotation + Math.sin(time * 0.3 + Math.random() * 0.5) * 0.1);
                        ctx.drawImage(imgToDraw, -size/2, -size/2, size, size);
                        ctx.restore();
                        ctx.shadowBlur = 0;
                        ctx.globalAlpha = 1.0;

                        if (isFound && anomalyType === 9 && extraText) {
                            ctx.save();
                            const textGlow = 0.6 + Math.sin(time * 1.5 + Math.random() * 0.5) * 0.3;
                            ctx.fillStyle = `rgba(255, 215, 0, ${textGlow})`;
                            ctx.font = 'bold 24px sans-serif';
                            ctx.textAlign = 'center';
                            ctx.shadowColor = 'rgba(0,0,0,0.9)';
                            ctx.shadowBlur = 15 + Math.sin(time + Math.random() * 0.5) * 5;
                            ctx.fillText(extraText, 750/2 + anomalyData.offsetX * 0.7, y + size + 30 + Math.sin(time * 0.5 + Math.random() * 0.5) * 5);
                            ctx.restore();
                        }

                        if (isFound && (anomalyType === 3 || anomalyType === 4 || anomalyType === 11)) {
                            ctx.save();
                            const glowAlpha = 0.05 + Math.sin(time * 1.5 + Math.random() * 0.5) * 0.06;
                            ctx.globalAlpha = Math.max(0.02, Math.min(0.15, glowAlpha));
                            const glowSize = size * (1.2 + Math.sin(time * 0.5 + Math.random() * 0.5) * 0.3);
                            const gradient = ctx.createRadialGradient(
                                750/2 + anomalyData.offsetX * 0.5, 470/2 + anomalyData.offsetY * 0.5, 10,
                                750/2 + anomalyData.offsetX * 0.5, 470/2 + anomalyData.offsetY * 0.5, glowSize
                            );
                            let color = anomalyType === 3 ? '#ff00ff' : anomalyType === 4 ? '#00ffaa' : '#ff4444';
                            gradient.addColorStop(0, color);
                            gradient.addColorStop(1, 'transparent');
                            ctx.fillStyle = gradient;
                            ctx.beginPath();
                            ctx.arc(750/2 + anomalyData.offsetX * 0.5, 470/2 + anomalyData.offsetY * 0.5, glowSize, 0, Math.PI * 2);
                            ctx.fill();
                            ctx.restore();
                        }
                    }
                } else {
                    if (isSearching) {
                        ctx.fillStyle = `rgba(255, 255, 0, ${0.1 + Math.sin(time * 1.5) * 0.05})`;
                        ctx.font = 'bold 20px sans-serif';
                        ctx.textAlign = 'center';
                        ctx.fillText('🔍 ИЩИТЕ ВНИМАТЕЛЬНО...', 375, 235 + Math.sin(time * 0.8) * 5);
                        ctx.textAlign = 'start';
                    }
                }
            }
            
            if (gameFinished && !epicEnding) {
                ctx.fillStyle = 'rgba(0,0,0,0.5)';
                ctx.fillRect(0, 0, 750, 470);
                ctx.fillStyle = '#fadf9e';
                ctx.font = 'bold 54px sans-serif';
                ctx.shadowColor = '#000';
                ctx.shadowBlur = 18;
                ctx.fillText(isMarathon ? '🏆 МАРАФОН!' : '✨ ПОБЕДА ✨', 180, 240);
                ctx.shadowBlur = 0;
            }
        }

        function animate() {
            if (hasAnomaly && !gameFinished && !epicEnding) updateAnomalyAnimation();
            drawRoom();
            animFrameId = requestAnimationFrame(animate);
        }

        function unlockMarathon() {
            marathonUnlocked = true;
            marathonBtn.disabled = false;
            marathonBtn.classList.remove('locked');
            marathonBtn.textContent = '🏃 МАРАФОН (64)';
            marathonStatus.textContent = '🌟 МАРАФОН РАЗБЛОКИРОВАН! 🌟';
            playUnlockSound();
        }

        function goToMenu() {
            if (animFrameId) {
                cancelAnimationFrame(animFrameId);
                animFrameId = null;
            }
            stopEpicMusic();
            epicEnding = false;
            epicTime = 0;
            gameFinished = false;
            hasAnomaly = false;
            anomalyType = 0;
            isSearching = false;
            searchBtn.textContent = '🔎 Обзор';
            searchBtn.classList.remove('active');
            actionBtn.disabled = false;
            backBtn.disabled = false;
            searchBtn.disabled = false;
            exitToMenuBtn.style.display = 'none';
            time = 0;
            currentRoom = 1;
            generateAnomalies();
            generateWindiRooms();
            menuOverlay.classList.remove('hidden');
            if (animFrameId) cancelAnimationFrame(animFrameId);
            loadRoom(1);
        }

        function loadRoom(roomNumber) {
            if (gameFinished || epicEnding) return;
            if (roomNumber < 1) roomNumber = MAX_ROOMS;
            if (roomNumber > MAX_ROOMS) {
                let allFound = true;
                for (let i = 1; i <= MAX_ROOMS; i++) {
                    if (roomAnomalyMap[i] !== 0 && !anomalyFound[i]) {
                        allFound = false;
                        break;
                    }
                }
                if (!allFound) {
                    currentRoom = 1;
                    loadRoom(currentRoom);
                    return;
                }
                if (isMarathon) {
                    epicEnding = true;
                    epicTime = 0;
                    playEpicMusic();
                    updateUI();
                    if (animFrameId) cancelAnimationFrame(animFrameId);
                    animate();
                    return;
                }
                gameFinished = true;
                hasAnomaly = false;
                anomalyType = 0;
                updateUI();
                if (animFrameId) cancelAnimationFrame(animFrameId);
                drawRoom();
                if (!isMarathon && !marathonUnlocked) {
                    unlockMarathon();
                }
                return;
            }
            const anomalyId = roomAnomalyMap[roomNumber] || 0;
            hasAnomaly = (anomalyId !== 0);
            anomalyType = anomalyId;
            isSearching = false;
            searchBtn.textContent = '🔎 Обзор';
            searchBtn.classList.remove('active');
            
            if (hasAnomaly) {
                time = Math.random() * 20;
                anomalyData.speed = 0.6 + Math.random() * 1.2;
                time += Math.random() * 10;
                
                if (anomalyType === 3 || anomalyType === 11) {
                    playScareSound();
                } else if (anomalyType === 10) {
                    playToiletPaperSound();
                } else if (anomalyType === 13) {
                    playAlertSound();
                } else if (anomalyType === 9) {
                    playBeep(500 + Math.random() * 200, 0.2 + Math.random() * 0.2, 0.2 + Math.random() * 0.2);
                    setTimeout(() => playBeep(600 + Math.random() * 200, 0.2 + Math.random() * 0.2, 0.2 + Math.random() * 0.2), 150 + Math.random() * 100);
                }
            } else {
                anomalyData.offsetX = 0; anomalyData.offsetY = 0; anomalyData.rotation = 0;
                anomalyData.scale = 1; anomalyData.flicker = 1; anomalyData.pulse = 1;
                anomalyData.floatOffset = 0;
            }
            updateUI();
            if (animFrameId) cancelAnimationFrame(animFrameId);
            animate();
        }

        function toggleSearch() {
            if (gameFinished || epicEnding) return;
            if (!hasAnomaly) {
                messageDisplay.textContent = '✅ ЗДЕСЬ ЧИСТО';
                return;
            }
            if (anomalyFound[currentRoom]) {
                messageDisplay.textContent = '✅ АНОМАЛИЯ УЖЕ НАЙДЕНА!';
                return;
            }
            
            isSearching = !isSearching;
            if (isSearching) {
                searchBtn.textContent = '🔍 Ищу...';
                searchBtn.classList.add('active');
                playSearchSound();
                messageDisplay.textContent = '🔍 ОСМАТРИВАЮ КОМНАТУ...';
                
                const searchTime = 1200 + Math.random() * 800;
                setTimeout(() => {
                    if (isSearching && hasAnomaly && !anomalyFound[currentRoom]) {
                        anomalyFound[currentRoom] = true;
                        isSearching = false;
                        searchBtn.textContent = '🔎 Обзор';
                        searchBtn.classList.remove('active');
                        messageDisplay.textContent = '✅ АНОМАЛИЯ НАЙДЕНА!';
                        playBeep(700 + Math.random() * 300, 0.15 + Math.random() * 0.15, 0.2 + Math.random() * 0.2);
                        setTimeout(() => playBeep(900 + Math.random() * 300, 0.15 + Math.random() * 0.15, 0.2 + Math.random() * 0.2), 120 + Math.random() * 80);
                    }
                }, searchTime);
            } else {
                searchBtn.textContent = '🔎 Обзор';
                searchBtn.classList.remove('active');
                messageDisplay.textContent = hasAnomaly ? '🔍 ИЩИ АНОМАЛИЮ' : '✅ ЧИСТО';
            }
        }

        function handleNextRoom() {
            if (gameFinished || epicEnding) return;
            
            if (hasAnomaly && !anomalyFound[currentRoom]) {
                currentRoom = 1;
                loadRoom(currentRoom);
                return;
            }
            
            currentRoom++;
            loadRoom(currentRoom);
        }

        function handleBackRoom() {
            if (gameFinished || epicEnding) return;
            
            if (hasAnomaly && anomalyFound[currentRoom]) {
                currentRoom++;
                loadRoom(currentRoom);
                return;
            }
            
            if (currentRoom <= 1) {
                currentRoom = MAX_ROOMS;
                loadRoom(currentRoom);
                return;
            }
            currentRoom--;
            loadRoom(currentRoom);
        }

        function toggleFullscreen() {
            if (!document.fullscreenElement) {
                document.documentElement.requestFullscreen().then(() => {
                    gameWrapper.classList.add('fullscreen');
                    isFullscreen = true;
                    fullscreenBtn.textContent = '⛶';
                }).catch(err => console.log('Ошибка полноэкранного режима:', err));
            } else {
                document.exitFullscreen().then(() => {
                    gameWrapper.classList.remove('fullscreen');
                    isFullscreen = false;
                    fullscreenBtn.textContent = '⛶';
                });
            }
        }

        document.addEventListener('fullscreenchange', () => {
            if (!document.fullscreenElement) {
                gameWrapper.classList.remove('fullscreen');
                isFullscreen = false;
                fullscreenBtn.textContent = '⛶';
            }
        });

        function resetGame() {
            stopEpicMusic();
            epicEnding = false;
            epicTime = 0;
            gameFinished = false;
            hasAnomaly = false;
            anomalyType = 0;
            isSearching = false;
            searchBtn.textContent = '🔎 Обзор';
            searchBtn.classList.remove('active');
            actionBtn.disabled = false;
            backBtn.disabled = false;
            searchBtn.disabled = false;
            exitToMenuBtn.style.display = 'none';
            time = 0;
            currentRoom = 1;
            generateAnomalies();
            generateWindiRooms();
            if (animFrameId) cancelAnimationFrame(animFrameId);
            loadRoom(1);
            menuOverlay.classList.remove('hidden');
        }

        function fullReset() {
            marathonUnlocked = false;
            marathonBtn.disabled = true;
            marathonBtn.classList.add('locked');
            marathonBtn.textContent = '🔒 МАРАФОН (64)';
            marathonStatus.textContent = '🧼 Пройдите 16 комнат, чтобы открыть марафон';
            resetGame();
        }

        function startGame(marathon = false) {
            isMarathon = marathon;
            MAX_ROOMS = marathon ? 64 : 16;
            menuOverlay.classList.add('hidden');
            stopEpicMusic();
            epicEnding = false;
            epicTime = 0;
            gameFinished = false;
            hasAnomaly = false;
            anomalyType = 0;
            isSearching = false;
            searchBtn.textContent = '🔎 Обзор';
            searchBtn.classList.remove('active');
            actionBtn.disabled = false;
            backBtn.disabled = false;
            searchBtn.disabled = false;
            exitToMenuBtn.style.display = 'none';
            time = 0;
            currentRoom = 1;
            generateAnomalies();
            generateWindiRooms();
            if (animFrameId) cancelAnimationFrame(animFrameId);
            loadRoom(1);
        }

        // ----- ЗАГРУЗКА -----
        let loadCounter = 0;
        const totalImages = 14;
        function imageLoaded() {
            loadCounter++;
            if (loadCounter >= totalImages) {
                MAX_ROOMS = 16;
                isMarathon = false;
                generateAnomalies();
                generateWindiRooms();
                currentRoom = 1;
                gameFinished = false;
                hasAnomaly = false;
                anomalyType = 0;
                loadRoom(1);
                menuOverlay.classList.remove('hidden');
            }
        }

        for (let key in images) {
            if (images[key].src) {
                images[key].addEventListener('load', imageLoaded);
                images[key].addEventListener('error', () => { imageLoaded(); });
            }
        }

        startBtn.addEventListener('click', () => {
            startGame(false);
        });

        marathonBtn.addEventListener('click', () => {
            if (marathonUnlocked) {
                startGame(true);
            }
        });

        resetBtn.addEventListener('click', () => {
            fullReset();
        });

        exitToMenuBtn.addEventListener('click', goToMenu);

        actionBtn.addEventListener('click', handleNextRoom);
        backBtn.addEventListener('click', handleBackRoom);
        fullscreenBtn.addEventListener('click', toggleFullscreen);
        searchBtn.addEventListener('click', toggleSearch);

        canvas.addEventListener('dblclick', () => {
            fullReset();
        });

        window.addEventListener('load', () => {
            setTimeout(() => {
                if (loadCounter >= totalImages) {
                    MAX_ROOMS = 16;
                    isMarathon = false;
                    generateAnomalies();
                    generateWindiRooms();
                    currentRoom = 1;
                    gameFinished = false;
                    loadRoom(1);
                    menuOverlay.classList.remove('hidden');
                }
            }, 300);
        });

        setTimeout(() => {
            if (loadCounter >= totalImages) {
                MAX_ROOMS = 16;
                isMarathon = false;
                generateAnomalies();
                generateWindiRooms();
                currentRoom = 1;
                gameFinished = false;
                loadRoom(1);
                menuOverlay.classList.remove('hidden');
            }
        }, 500);

        console.log('🚽 Туалетные истории 16 · увеличенный рандом аномалий');
    })();
</script>
</body>
</html>
