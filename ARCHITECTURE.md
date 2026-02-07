<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Защита и Помощь — Ваш цифровой помощник</title>
    <style>
        :root {
            --safe-green: #2e7d32;
            --danger-red: #d32f2f;
            --warning-orange: #f57c00;
            --bg-soft: #f9fbfd;
            --text-main: #2c3e50;
        }

        body {
            font-family: Arial, sans-serif;
            margin: 0; padding: 0;
            background: var(--bg-soft);
            color: var(--text-main);
            font-size: 20px; /* Увеличенный шрифт для удобства */
        }

        /* Крупная и понятная навигация */
        nav {
            background: #fff;
            padding: 15px;
            display: flex;
            justify-content: space-around;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
            position: sticky; top: 0; z-index: 100;
        }

        .nav-link {
            text-decoration: none;
            color: var(--text-main);
            font-weight: bold;
            font-size: 18px;
            padding: 10px;
        }

        .container { 
            max-width: 700px; 
            margin: 20px auto; 
            padding: 20px; 
        }

        .card {
            background: white;
            border-radius: 20px;
            padding: 30px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.05);
            margin-bottom: 30px;
            border: 2px solid #e0e0e0;
        }

        h1 { color: var(--safe-green); font-size: 32px; }
        h2 { font-size: 26px; }

        /* Крупные кнопки */
        .btn {
            background: var(--safe-green);
            color: white;
            border: none;
            padding: 20px 30px;
            border-radius: 12px;
            font-size: 22px;
            font-weight: bold;
            cursor: pointer;
            width: 100%;
            display: block;
            margin: 10px 0;
        }

        .btn-secondary { background: #546e7a; }

        /* Поля ввода */
        textarea, input {
            width: 100%;
            padding: 15px;
            font-size: 18px;
            border: 3px solid #cfd8dc;
            border-radius: 12px;
            box-sizing: border-box;
            margin-bottom: 20px;
        }

        /* Результаты проверки */
        .result-box {
            padding: 20px;
            border-radius: 12px;
            margin-top: 20px;
            display: none;
            line-height: 1.5;
        }

        .danger-box { background: #ffebee; border: 2px solid var(--danger-red); color: #b71c1c; }
        .safe-box { background: #e8f5e9; border: 2px solid var(--safe-green); color: #1b5e20; }

        .tip {
            background: #fff9c4;
            padding: 15px;
            border-left: 5px solid #fbc02d;
            margin-top: 10px;
            font-size: 18px;
        }
    </style>
</head>
<body>

<nav>
    <a href="#home" class="nav-link">🏠 Главная</a>
    <a href="#check" class="nav-link">🛡️ Проверка</a>
    <a href="#rules" class="nav-link">📜 Советы</a>
</nav>

<div class="container">

    <section id="home" class="card">
        <h1>Здравствуйте!</h1>
        <p>Мы поможем вам распознать мошенников. Если вам пришло странное сообщение или файл — давайте проверим их вместе.</p>
        <button class="btn" onclick="location.href='#check'">Проверить сейчас</button>
    </section>

    <section id="check" class="card">
        <h2>Проверим SMS или письмо</h2>
        <p>Вставьте текст сообщения, которое вам прислали:</p>
        <textarea id="sms-input" rows="5" placeholder="Пример: Вы выиграли 1000000, перейдите по ссылке..."></textarea>
        <button class="btn" onclick="checkMessage()">Проверить текст</button>

        <div id="result" class="result-box"></div>
    </section>

    <section id="rules" class="card">
        <h2>Простые правила безопасности</h2>
        <div class="tip">🛑 <strong>Никому</strong> не говорите коды из SMS. Даже «сотрудникам банка».</div>
        <div class="tip">📞 Если звонят и пугают — просто положите трубку и сами позвоните родным.</div>
        <div class="tip">🔗 Не нажимайте на ссылки от незнакомых людей.</div>
    </section>

</div>

<script>
function checkMessage() {
    const text = document.getElementById('sms-input').value.toLowerCase();
    const resultDiv = document.getElementById('result');
    resultDiv.style.display = 'block';

    // Понятные триггеры для пожилых
    const badWords = ['выигрыш', 'счет заблокирован', 'перейдите по ссылке', 'срочно', 'акция', 'пароль', 'карта', 'цб', 'безопасный счет'];
    
    let found = [];
    badWords.forEach(word => {
        if(text.includes(word)) found.push(word);
    });

    if (text.length < 5) {
        resultDiv.className = 'result-box';
        resultDiv.innerHTML = "Пожалуйста, напишите или вставьте текст сообщения.";
        return;
    }

    if (found.length > 0) {
        resultDiv.className = 'result-box danger-box';
        resultDiv.innerHTML = `
            <h3>⚠️ Будьте осторожны!</h3>
            <p>Это сообщение очень похоже на обман. Мошенники часто используют такие слова как: <strong>${found.join(', ')}</strong>.</p>
            <p><strong>Что делать?</strong> Ничего не нажимайте и не отвечайте. Просто удалите это сообщение.</p>
        `;
    } else {
        resultDiv.className = 'result-box safe-box';
        resultDiv.innerHTML = `
            <h3>✅ Подозрительных слов не найдено</h3>
            <p>Но все равно будьте бдительны. Если сообщение просит прислать деньги или данные карты — это могут быть мошенники.</p>
        `;
    }
}
</script>

</body>
</html>
