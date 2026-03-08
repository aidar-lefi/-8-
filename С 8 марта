<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>С 8 Марта! 🌷</title>
    <style>
        :root {
            --primary: #ff4da6;
            --secondary: #ff9ac6;
            --accent: #6c5ce7;
            --glass: rgba(255, 255, 255, 0.85);
        }

        body {
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', Roboto, sans-serif;
            background: linear-gradient(135deg, #fce4ec 0%, #ffebee 100%);
            background-attachment: fixed;
            text-align: center;
            color: #444;
            overflow-x: hidden;
            min-height: 100vh;
        }

        header {
            background: var(--glass);
            backdrop-filter: blur(10px);
            padding: 20px;
            box-shadow: 0 4px 20px rgba(0,0,0,0.05);
            position: sticky;
            top: 0;
            z-index: 1000;
        }

        h1 { color: #d81b60; margin: 0; font-size: 1.8rem; }

        .container { padding: 40px 20px; max-width: 600px; margin: 0 auto; }

        /* Подарок */
        .gift {
            font-size: 100px;
            cursor: pointer;
            display: inline-block;
            transition: all 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275);
            filter: drop-shadow(0 10px 15px rgba(0,0,0,0.1));
            user-select: none;
        }
        .gift:hover { transform: scale(1.1) rotate(-5deg); }
        .gift:active { transform: scale(0.9); }

        #hint { font-style: italic; color: #888; margin-top: 10px; }

        /* Карточки */
        .card {
            display: none;
            background: var(--glass);
            backdrop-filter: blur(15px);
            margin-top: 30px;
            padding: 30px;
            border-radius: 30px;
            border: 1px solid rgba(255,255,255,0.5);
            box-shadow: 0 20px 40px rgba(0,0,0,0.1);
            animation: slideUp 0.6s ease-out forwards;
        }

        @keyframes slideUp {
            from { opacity: 0; transform: translateY(50px); }
            to { opacity: 1; transform: translateY(0); }
        }

        /* Поля ввода */
        textarea, input[type="text"] {
            width: 100%;
            padding: 15px;
            margin: 10px 0;
            border-radius: 15px;
            border: 2px solid #fce4ec;
            background: rgba(255,255,255,0.9);
            font-size: 16px;
            box-sizing: border-box;
            transition: 0.3s;
        }
        textarea:focus, input:focus { border-color: var(--primary); outline: none; }

        button {
            background: var(--primary);
            color: white;
            border: none;
            padding: 15px 30px;
            border-radius: 50px;
            font-weight: bold;
            cursor: pointer;
            margin: 10px 5px;
            transition: 0.3s;
            box-shadow: 0 4px 15px rgba(255, 77, 166, 0.3);
        }
        button:hover { background: #e91e63; transform: translateY(-2px); }
        .btn-share { background: var(--accent); }

        /* Результат для получателя */
        #finalMessage { font-size: 1.25rem; line-height: 1.6; color: #333; white-space: pre-wrap; }
        #finalImage { max-width: 100%; border-radius: 20px; margin-top: 20px; box-shadow: 0 10px 25px rgba(0,0,0,0.1); display: none; }

        /* Улучшенная анимация цветов */
        .flower {
            position: fixed;
            top: -50px;
            pointer-events: none;
            z-index: 9999;
            animation: fallAndSway linear infinite;
        }

        @keyframes fallAndSway {
            0% { transform: translateY(0) translateX(0) rotate(0deg); opacity: 1; }
            25% { transform: translateY(25vh) translateX(20px) rotate(90deg); }
            50% { transform: translateY(50vh) translateX(-20px) rotate(180deg); }
            75% { transform: translateY(75vh) translateX(20px) rotate(270deg); }
            100% { transform: translateY(105vh) translateX(0) rotate(360deg); opacity: 0.3; }
        }

        footer { padding: 40px; color: #ad1457; font-size: 0.9rem; opacity: 0.7; }
    </style>
</head>
<body>

<header id="configHeader">
    <h1>🎀 Мастер Поздравлений</h1>
    <div style="margin-top: 10px;">
        Выбери стиль: 
        <select id="flowerChoice" style="padding: 5px; border-radius: 10px;">
            <option value="🌸">Лепестки Сакуры</option>
            <option value="🌹">Красные Розы</option>
            <option value="🌷">Нежные Тюльпаны</option>
            <option value="✨">Мерцание звезд</option>
        </select>
    </div>
</header>

<div class="container">
    <div id="giftBox" class="gift" onclick="handleGiftClick()">🎁</div>
    <p id="hint">Нажми на подарок 3 раза, чтобы открыть!</p>

    <div id="editorCard" class="card">
        <h3>Шаг 1: Напиши текст</h3>
        <textarea id="msgInput" placeholder="Дорогая, поздравляю тебя с 8 Марта..."></textarea>
        
        <h3>Шаг 2: Вставь ссылку на фото</h3>
        <input type="text" id="imgInput" placeholder="https://ссылка-на-твое-фото.jpg">
        <p style="font-size: 11px; color: #999;">(Загрузи фото в соцсеть и скопируй адрес изображения)</p>
        
        <button class="btn-share" onclick="generateLink()">🔗 Скопировать ссылку для неё</button>
    </div>

    <div id="receiverCard" class="card">
        <h2 style="color: var(--primary);">С праздником весны! ✨</h2>
        <div id="finalMessage"></div>
        <img id="finalImage" src="" alt="Поздравление">
    </div>
</div>

<footer>Сделано с любовью к 8 Марта ❤️</footer>

<script>
    let clickCount = 0;
    const urlParams = new URLSearchParams(window.location.search);
    const isReceiver = urlParams.has('m');

    // Если зашел получатель - сразу готовим данные
    if (isReceiver) {
        document.getElementById('configHeader').style.display = 'none';
        document.body.style.background = "linear-gradient(135deg, #fff1f2 0%, #fce4ec 100%)";
        
        // Настройка цветов из ссылки
        const fl = urlParams.get('f') || '🌸';
        startFlowers(fl);
    }

    function handleGiftClick() {
        if (clickCount >= 3) return;
        clickCount++;
        
        const gift = document.getElementById('giftBox');
        gift.style.transform = scale(${1 + clickCount * 0.15}) rotate(${clickCount * 5}deg);

        if (clickCount === 3) {
            gift.innerHTML = "🔓";
            document.getElementById('hint').innerText = "Сюрприз раскрыт!";
            
            if (isReceiver) {
                showForReceiver();
            } else {
                document.getElementById('editorCard').style.display = 'block';
            }
            
            // Плавный скролл к контенту
            setTimeout(() => {
                window.scrollTo({ top: document.body.scrollHeight, behavior: 'smooth' });
            }, 300);
        }
    }

    function showForReceiver() {
        const msg = decodeURIComponent(urlParams.get('m'));
        const img = urlParams.get('i');
        
        const card = document.getElementById('receiverCard');
        card.style.display = 'block';
        
        document.getElementById('finalMessage').innerText = msg;
        
        if (img) {
            const imgEl = document.getElementById('finalImage');
            imgEl.src = decodeURIComponent(img);
            imgEl.style.display = 'block';
        }
    }

    function generateLink() {
        const msg = document.getElementById('msgInput').value;
        const img = document.getElementById('imgInput').value;
        const fl = document.getElementById('flowerChoice').value;

        if (!msg) {
            alert("Пожалуйста, напиши хотя бы пару слов!");
            return;
        }

        const baseUrl = window.location.origin + window.location.pathname;
        const finalUrl = ${baseUrl}?m=${encodeURIComponent(msg)}&i=${encodeURIComponent(img)}&f=${encodeURIComponent(fl)};

        navigator.clipboard.writeText(finalUrl).then(() => {
            alert("Готово! Ссылка в буфере обмена. Теперь отправь её той самой девушке! 🌹");
        });
    }

    function startFlowers(emoji) {
        setInterval(() => {
            const flower = document.createElement('div');
            flower.className = 'flower';
            flower.innerText = emoji;
            flower.style.left = Math.random() * 100 + 'vw';
            flower.style.fontSize = (Math.random() * 20 + 20) + 'px';
            flower.style.animationDuration = (Math.random() * 3 + 4) + 's';
            document.body.appendChild(flower);
            
            setTimeout(() => flower.remove(), 7000);
        }, 300);
    }
</script>

</body>
</html>
