<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Туалетные истории 16 · главное меню</title>
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
        <button class="menu-btn" id="startGameBtn">▶ ИГРАТЬ</button>
        <button class="menu-btn menu-btn-secondary" id="resetGameBtn">⟳ Заново</button>
        <div class="menu-footer">
            <span>🧼 16 комнат · не более 2 аномалий подряд</span>
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
                    <button id="fullscreenButton" class="fullscreen-btn">⛶</button>
                    <button id="backButton">◀</button>
                    <button id="actionButton">➡️</button>
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

        const canvas = document.getElementById('gameCanvas');
        const ctx = canvas.getContext('2d');
        const gameWrapper = document.getElementById('gameWrapper');

        const roomDisplay = document.getElementById('roomDisplay');
        const messageDisplay = document.getElementById('messageDisplay');
        const progressDisplay = document.getElementById('progressDisplay');
        const actionBtn = document.getElementById('actionButton');
        const backBtn = document.getElementById('backButton');
        const fullscreenBtn = document.getElementById('fullscreenButton');

        const MAX_ROOMS = 16;
        let currentRoom = 1;
        let hasAnomaly = false;
        let anomalyType = 0;
        let gameFinished = false;
        let isFullscreen = false;
        let animFrameId = null;
        let time = 0;

        let anomalyData = {
            offsetX: 0, offsetY: 0, rotation: 0, scale: 1,
            flicker: 0, pulse: 0, floatOffset: 0, speed: 1
        };

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
        images.windi31.src = 'https://pic.rtbcdn.ru/user/b5/87/b587ecd7a3492734866ee096fc1186c9.jpg';

        const ANOMALY_TYPES = 8;
        let roomAnomalyMap = new Array(MAX_ROOMS + 1).fill(0);
        let windiRooms = new Array(MAX_ROOMS + 1).fill(false);

        // ----- ГЕНЕРАЦИЯ АНОМАЛИЙ (не более 2 подряд, после 2 аномалий — 2 чистых) -----
        function generateAnomalies() {
            roomAnomalyMap.fill(0);
            const totalAnomalies = 6 + Math.floor(Math.random() * 3);
            let placed = 0, attempts = 0;

            while (placed < totalAnomalies && attempts < 1000) {
                attempts++;
                const room = Math.floor(Math.random() * MAX_ROOMS) + 1;
                if (roomAnomalyMap[room] !== 0) continue;

                let leftAnomaly = (room > 1 && roomAnomalyMap[room-1] !== 0);
                let rightAnomaly = (room < MAX_ROOMS && roomAnomalyMap[room+1] !== 0);
                if (leftAnomaly && room > 2 && roomAnomalyMap[room-2] !== 0) continue;
                if (rightAnomaly && room < MAX_ROOMS-1 && roomAnomalyMap[room+2] !== 0) continue;

                let leftStreak = 0, temp = room - 1;
                while (temp >= 1 && roomAnomalyMap[temp] !== 0) { leftStreak++; temp--; }
                let rightStreak = 0; temp = room + 1;
                while (temp <= MAX_ROOMS && roomAnomalyMap[temp] !== 0) { rightStreak++; temp++; }

                if (leftStreak >= 2 || rightStreak >= 2) continue;

                if (leftStreak === 1 && room > 1 && roomAnomalyMap[room-1] !== 0) {
                    let lastAnomaly = room - 1;
                    while (lastAnomaly >= 1 && roomAnomalyMap[lastAnomaly] !== 0) lastAnomaly--;
                    if (lastAnomaly >= 1 && room - lastAnomaly - 1 >= 2) {
                        let cleanAfter = 0;
                        for (let i = lastAnomaly + 1; i <= MAX_ROOMS; i++) {
                            if (roomAnomalyMap[i] === 0) cleanAfter++;
                            else break;
                        }
                        if (cleanAfter < 2) continue;
                    }
                }

                if (rightStreak === 1 && room < MAX_ROOMS && roomAnomalyMap[room+1] !== 0) {
                    let lastAnomaly = room + 1;
                    while (lastAnomaly <= MAX_ROOMS && roomAnomalyMap[lastAnomaly] !== 0) lastAnomaly++;
                    if (lastAnomaly <= MAX_ROOMS && lastAnomaly - room - 1 >= 2) {
                        let cleanAfter = 0;
                        for (let i = room + 2; i <= MAX_ROOMS; i++) {
                            if (roomAnomalyMap[i] === 0) cleanAfter++;
                            else break;
                        }
                        if (cleanAfter < 2) continue;
                    }
                }

                roomAnomalyMap[room] = Math.floor(Math.random() * ANOMALY_TYPES) + 1;
                placed++;
            }

            // Коррекция
            for (let i = 1; i <= MAX_ROOMS - 2; i++) {
                if (roomAnomalyMap[i] !== 0 && roomAnomalyMap[i+1] !== 0 && roomAnomalyMap[i+2] !== 0) {
                    roomAnomalyMap[i+1] = 0;
                }
            }
            for (let i = 1; i <= MAX_ROOMS - 3; i++) {
                if (roomAnomalyMap[i] !== 0 && roomAnomalyMap[i+1] !== 0) {
                    if (roomAnomalyMap[i+2] !== 0) roomAnomalyMap[i+2] = 0;
                    if (i+3 <= MAX_ROOMS && roomAnomalyMap[i+3] !== 0) roomAnomalyMap[i+3] = 0;
                }
            }
            let count = 0;
            for (let i = 1; i <= MAX_ROOMS; i++) if (roomAnomalyMap[i] !== 0) count++;
            if (count < 4) {
                for (let i = 1; i <= MAX_ROOMS && count < 4; i++) {
                    if (roomAnomalyMap[i] === 0) {
                        let left = (i > 1 && roomAnomalyMap[i-1] !== 0);
                        let right = (i < MAX_ROOMS && roomAnomalyMap[i+1] !== 0);
                        if (!left && !right) {
                            roomAnomalyMap[i] = Math.floor(Math.random() * ANOMALY_TYPES) + 1;
                            count++;
                        }
                    }
                }
            }
        }

        function generateWindiRooms() {
            for (let i = 1; i <= MAX_ROOMS; i++) windiRooms[i] = Math.random() < 0.4;
            let hasWindi = false;
            for (let i = 1; i <= MAX_ROOMS; i++) if (windiRooms[i]) { hasWindi = true; break; }
            if (!hasWindi) windiRooms[Math.floor(Math.random() * MAX_ROOMS) + 1] = true;
        }

        function updateUI() {
            roomDisplay.textContent = `🚽 ${currentRoom} / ${MAX_ROOMS}`;
            progressDisplay.textContent = `${currentRoom-1}/${MAX_ROOMS}`;
            if (gameFinished) {
                messageDisplay.textContent = '🏆 ПОБЕДА!';
                actionBtn.disabled = true;
                backBtn.disabled = true;
                actionBtn.textContent = '🏁';
                backBtn.textContent = '◀';
                return;
            }
            actionBtn.disabled = false;
            backBtn.disabled = false;
            actionBtn.textContent = '➡️';
            backBtn.textContent = '◀';
            if (hasAnomaly) messageDisplay.textContent = '⚠️ АНОМАЛИЯ';
            else messageDisplay.textContent = '✅ ЧИСТО';
        }

        function updateAnomalyAnimation() {
            if (!hasAnomaly || gameFinished) return;
            const speed = 0.02 + Math.random() * 0.02;
            time += speed;
            anomalyData.floatOffset = Math.sin(time * 1.2) * 15;
            anomalyData.offsetX = Math.sin(time * 0.7) * 20;
            anomalyData.offsetY = Math.sin(time * 0.9 + 1) * 15 + anomalyData.floatOffset * 0.3;
            anomalyData.rotation = Math.sin(time * 0.5) * 0.3;
            anomalyData.pulse = 0.85 + Math.sin(time * 1.8) * 0.15;
            anomalyData.scale = anomalyData.pulse;
            anomalyData.flicker = 0.5 + Math.sin(time * 3.5 + anomalyType * 2) * 0.25; // снизили базовую прозрачность
            if (anomalyType === 3) {
                anomalyData.offsetX = Math.sin(time * 1.5) * 25;
                anomalyData.offsetY = Math.sin(time * 1.3 + 0.5) * 20;
                anomalyData.rotation = Math.sin(time * 1.2) * 0.4;
            } else if (anomalyType === 4) {
                anomalyData.offsetY = Math.abs(Math.sin(time * 1.6)) * 20 - 10;
                anomalyData.rotation = Math.sin(time * 0.8) * 0.2;
            } else if (anomalyType === 1) {
                anomalyData.rotation = Math.sin(time * 0.9) * 0.5;
                anomalyData.scale = 0.9 + Math.sin(time * 1.1) * 0.1;
            } else if (anomalyType === 2) {
                anomalyData.offsetX = Math.sin(time * 0.5) * 18;
                anomalyData.rotation = Math.sin(time * 0.4 + 0.3) * 0.25;
            } else if (anomalyType === 5) {
                anomalyData.offsetY = Math.sin(time * 1.8) * 12;
                anomalyData.scale = 0.9 + Math.sin(time * 0.7) * 0.1;
            } else if (anomalyType === 6) {
                anomalyData.offsetY = Math.abs(Math.sin(time * 2.2)) * 25 - 12;
                anomalyData.rotation = Math.sin(time * 0.6) * 0.15;
            } else if (anomalyType === 7) {
                anomalyData.offsetY = Math.sin(time * 3.0) * 30;
                anomalyData.offsetX = Math.sin(time * 2.5 + 1) * 20;
                anomalyData.scale = 0.7 + Math.sin(time * 2.0) * 0.3;
            } else if (anomalyType === 8) {
                anomalyData.offsetX = Math.sin(time * 0.8) * 40;
                anomalyData.offsetY = Math.cos(time * 0.8 + 0.5) * 30;
                anomalyData.rotation = time * 0.3;
            }
        }

        function drawRoom() {
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
                let imgToDraw = null;
                let baseSize = 110;
                let size = baseSize * anomalyData.scale;
                let x = 750/2 - size/2 + anomalyData.offsetX;
                let y = 470/2 - size/2 + 10 + anomalyData.offsetY;
                switch (anomalyType) {
                    case 1: imgToDraw = images.anomaly1; break;
                    case 2: imgToDraw = images.anomaly2; break;
                    case 3: imgToDraw = images.anomaly3; break;
                    case 4: imgToDraw = images.anomaly4; break;
                    case 5: imgToDraw = images.anomaly5; break;
                    case 6: imgToDraw = images.anomaly6; break;
                    case 7: imgToDraw = images.anomaly7; break;
                    case 8: imgToDraw = images.anomaly8; break;
                    default: break;
                }
                if (anomalyType === 3) {
                    size = (130 + Math.sin(time * 0.5) * 10) * anomalyData.scale;
                    x = 750/2 - size/2 - 10 + anomalyData.offsetX;
                    y = 470/2 - size/2 - 5 + anomalyData.offsetY;
                } else if (anomalyType === 4) {
                    size = (120 + Math.sin(time * 0.7) * 8) * anomalyData.scale;
                    x = 750/2 - size/2 + 5 + anomalyData.offsetX;
                    y = 470/2 - size/2 + 5 + anomalyData.offsetY;
                } else if (anomalyType === 5) {
                    size = (140 + Math.sin(time * 0.5) * 10) * anomalyData.scale;
                    x = 750/2 - size/2 + anomalyData.offsetX;
                    y = 470/2 - size/2 + 10 + anomalyData.offsetY;
                } else if (anomalyType === 6) {
                    size = (130 + Math.sin(time * 0.3) * 5) * anomalyData.scale;
                    x = 750/2 - size/2 + anomalyData.offsetX;
                    y = 470/2 - size/2 + 15 + anomalyData.offsetY;
                } else if (anomalyType === 7) {
                    size = 40;
                    const count = 6 + Math.floor(Math.sin(time * 0.5) * 2);
                    for (let i = 0; i < count; i++) {
                        const angle = time * 2.5 + i * 1.8;
                        const dist = 60 + Math.sin(time * 0.7 + i) * 30;
                        const px = 750/2 + Math.cos(angle + time * 0.5) * dist + anomalyData.offsetX * 0.5;
                        const py = 470/2 + Math.sin(angle * 1.3 + time * 1.2) * dist * 0.6 + Math.sin(time * 3 + i) * 20 + anomalyData.offsetY * 0.5;
                        if (images.anomaly7.complete && images.anomaly7.naturalWidth > 0) {
                            const s = 25 + Math.sin(time + i) * 8;
                            ctx.globalAlpha = 0.3 + Math.sin(time * 1.5 + i) * 0.15; // полупрозрачность
                            ctx.drawImage(images.anomaly7, px - s/2, py - s/2, s, s);
                        }
                    }
                    ctx.globalAlpha = 1.0;
                    return;
                } else if (anomalyType === 8) {
                    size = (120 + Math.sin(time * 0.4) * 10) * anomalyData.scale;
                    x = 750/2 - size/2 + anomalyData.offsetX;
                    y = 470/2 - size/2 + 10 + anomalyData.offsetY;
                }
                if (imgToDraw && imgToDraw.complete && imgToDraw.naturalWidth > 0) {
                    // ПОЛУПРОЗРАЧНОСТЬ: базовая alpha 0.35–0.75, с мерцанием
                    let alpha = 0.35 + 0.4 * (0.5 + 0.5 * Math.sin(time * 2.5 + anomalyType));
                    if (anomalyType === 3 || anomalyType === 4) {
                        alpha = 0.4 + 0.3 * (0.5 + 0.5 * Math.sin(time * 2 + anomalyType));
                    }
                    ctx.globalAlpha = Math.max(0.25, Math.min(0.8, alpha));
                    
                    if (anomalyType !== 5 && anomalyType !== 6) {
                        ctx.shadowColor = 'rgba(255, 0, 0, 0.15)';
                        ctx.shadowBlur = 15 + Math.sin(time * 1.5) * 8;
                    }
                    ctx.save();
                    ctx.translate(x + size/2, y + size/2);
                    ctx.rotate(anomalyData.rotation);
                    ctx.drawImage(imgToDraw, -size/2, -size/2, size, size);
                    ctx.restore();
                    ctx.shadowBlur = 0;
                    ctx.globalAlpha = 1.0;
                    if (anomalyType === 3 || anomalyType === 4) {
                        ctx.save();
                        ctx.globalAlpha = 0.08 + Math.sin(time * 2) * 0.05;
                        const glowSize = size * 1.4;
                        const gradient = ctx.createRadialGradient(
                            750/2 + anomalyData.offsetX, 470/2 + anomalyData.offsetY, 10,
                            750/2 + anomalyData.offsetX, 470/2 + anomalyData.offsetY, glowSize
                        );
                        gradient.addColorStop(0, anomalyType === 3 ? '#ff00ff' : '#00ffaa');
                        gradient.addColorStop(1, 'transparent');
                        ctx.fillStyle = gradient;
                        ctx.beginPath();
                        ctx.arc(750/2 + anomalyData.offsetX, 470/2 + anomalyData.offsetY, glowSize, 0, Math.PI * 2);
                        ctx.fill();
                        ctx.restore();
                    }
                } else {
                    ctx.fillStyle = '#ff4d6d';
                    ctx.globalAlpha = 0.6;
                    ctx.font = 'bold 40px sans-serif';
                    ctx.fillText(`⚠️ АНОМАЛИЯ ${anomalyType}`, 250, 260);
                    ctx.globalAlpha = 1;
                }
            }
            if (gameFinished) {
                ctx.fillStyle = 'rgba(0,0,0,0.5)';
                ctx.fillRect(0, 0, 750, 470);
                ctx.fillStyle = '#fadf9e';
                ctx.font = 'bold 54px sans-serif';
                ctx.shadowColor = '#000';
                ctx.shadowBlur = 18;
                ctx.fillText('✨ ПОБЕДА ✨', 180, 240);
                ctx.shadowBlur = 0;
            }
        }

        function animate() {
            if (hasAnomaly && !gameFinished) updateAnomalyAnimation();
            drawRoom();
            animFrameId = requestAnimationFrame(animate);
        }

        function loadRoom(roomNumber) {
            if (gameFinished) return;
            if (roomNumber < 1) roomNumber = MAX_ROOMS;
            if (roomNumber > MAX_ROOMS) {
                gameFinished = true;
                hasAnomaly = false;
                anomalyType = 0;
                updateUI();
                if (animFrameId) cancelAnimationFrame(animFrameId);
                drawRoom();
                return;
            }
            const anomalyId = roomAnomalyMap[roomNumber] || 0;
            hasAnomaly = (anomalyId !== 0);
            anomalyType = anomalyId;
            if (hasAnomaly) {
                time = Math.random() * 10;
                anomalyData.speed = 0.8 + Math.random() * 0.6;
                time += Math.random() * 5;
            } else {
                anomalyData.offsetX = 0; anomalyData.offsetY = 0; anomalyData.rotation = 0;
                anomalyData.scale = 1; anomalyData.flicker = 1; anomalyData.pulse = 1;
                anomalyData.floatOffset = 0;
            }
            updateUI();
            if (animFrameId) cancelAnimationFrame(animFrameId);
            animate();
        }

        function handleNextRoom() {
            if (gameFinished) return;
            if (hasAnomaly) { messageDisplay.textContent = '⚠️ АНОМАЛИЯ'; return; }
            currentRoom++;
            if (currentRoom > MAX_ROOMS) {
                gameFinished = true;
                hasAnomaly = false;
                anomalyType = 0;
                updateUI();
                if (animFrameId) cancelAnimationFrame(animFrameId);
                drawRoom();
                return;
            }
            loadRoom(currentRoom);
        }

        function handleBackRoom() {
            if (gameFinished) return;
            if (hasAnomaly) {
                if (currentRoom < MAX_ROOMS) { currentRoom++; loadRoom(currentRoom); }
                else { gameFinished = true; hasAnomaly = false; anomalyType = 0; updateUI(); if (animFrameId) cancelAnimationFrame(animFrameId); drawRoom(); }
                return;
            }
            if (currentRoom <= 1) { currentRoom = MAX_ROOMS; loadRoom(currentRoom); return; }
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
            generateAnomalies();
            generateWindiRooms();
            currentRoom = 1;
            gameFinished = false;
            hasAnomaly = false;
            anomalyType = 0;
            actionBtn.disabled = false;
            backBtn.disabled = false;
            time = 0;
            if (animFrameId) cancelAnimationFrame(animFrameId);
            loadRoom(1);
            menuOverlay.classList.remove('hidden');
        }

        // ----- ЗАГРУЗКА -----
        let loadCounter = 0;
        const totalImages = 9;
        function imageLoaded() {
            loadCounter++;
            if (loadCounter >= totalImages) {
                menuOverlay.classList.remove('hidden');
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
            menuOverlay.classList.add('hidden');
            if (gameFinished || currentRoom > MAX_ROOMS) resetGame();
            menuOverlay.classList.add('hidden');
        });

        resetBtn.addEventListener('click', () => {
            resetGame();
            menuOverlay.classList.remove('hidden');
        });

        actionBtn.addEventListener('click', handleNextRoom);
        backBtn.addEventListener('click', handleBackRoom);
        fullscreenBtn.addEventListener('click', toggleFullscreen);

        canvas.addEventListener('dblclick', () => {
            resetGame();
            menuOverlay.classList.remove('hidden');
        });

        window.addEventListener('load', () => {
            setTimeout(() => {
                if (loadCounter >= totalImages) {
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
                generateAnomalies();
                generateWindiRooms();
                currentRoom = 1;
                gameFinished = false;
                loadRoom(1);
                menuOverlay.classList.remove('hidden');
            }
        }, 500);

        console.log('🚽 Туалетные истории 16 · полупрозрачные аномалии');
    })();
</script>
</body>
</html>
