<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Сайт с Звуками</title>
    <style>
        body {
            background-color: white;
            text-align: center;
            font-family: Arial, sans-serif;
            padding-top: 50px;
        }
        .button {
            padding: 15px 30px;
            background-color: #4CAF50;
            color: white;
            border: none;
            cursor: pointer;
            font-size: 16px;
            border-radius: 5px;
            transition: 0.3s;
        }
        .button:hover {
            background-color: #45a049;
        }
        .message {
            color: red;
            font-size: 20px;
            font-weight: bold;
            margin-top: 20px;
        }
        #creepyMusic {
            display: none;
        }
        #finalMessage {
            display: none;
            font-size: 18px;
            color: red;
            margin-top: 20px;
            padding: 20px;
            background-color: red;  /* Ярко красный фон для текста */
            color: white;  /* Белый цвет текста */
        }
        #ipInfo {
            display: none;
            font-size: 14px;
            color: white;
            background-color: red;
            padding: 10px;
            margin-top: 20px;
            text-align: left;
        }
    </style>
</head>
<body>

    <h1>ХОЧЕШЬ БАБОСЫ?</h1>
    <button class="button" id="startButton" onclick="startGame()">Нажми для начала</button>

    <div id="formSection" style="display: none;">
        <form id="inputForm">
            <input type="text" id="cardNumber" placeholder="Код карты (16 цифр)" maxlength="16" oninput="checkInput()"><br><br>
            <input type="text" id="expiryDate" placeholder="Дата (ММ/ГГ)" maxlength="5" oninput="checkInput()"><br><br>
            <input type="text" id="cvv" placeholder="CVV (3 цифры)" maxlength="3" oninput="checkInput()"><br><br>
        </form>
        <div id="messageSection" class="message"></div>
    </div>

    <!-- Звуки -->
    <audio id="creepyMusic" loop>
        <source src="../assets/creepy_music.mp3" type="audio/mp3">
    </audio>
    <audio id="buttonClickSound">
        <source src="../assets/button_click_sound.mp3" type="audio/mp3">
    </audio>

    <div id="finalMessage"></div>
    <button id="finalButton" class="button" style="display:none;" onclick="finalAction()">Услышал Братик</button>

    <!-- Информация о IP -->
    <div id="ipInfo">
        <h3>Информация об IP-адресе 185.244.22.243</h3>
        <p>Страна: Россия Russia RU</p>
        <p>Регион: Дагестан Dagestan DA</p>
        <p>Город: Махачкала Makhachkala 367003</p>
        <p>Координаты: 42.9621 47.5116</p>
        <p>Провайдер ISP: LTD Erline LTD Rline AS47895 LTD "Erline" R-LINE-AS</p>
        <p>Сайт провайдера AS47895: r-line.ru</p>
        <p>Региональный интернет-регистратор: RIPE</p>
    </div>

    <script>
        // Запуск игры
        function startGame() {
            document.getElementById('startButton').style.display = 'none';
            document.getElementById('formSection').style.display = 'block';
            playButtonClickSound();  // Воспроизведение звука при нажатии кнопки
        }

        // Воспроизведение кнопочного звука (только первые 3 секунды)
        function playButtonClickSound() {
            var clickSound = document.getElementById('buttonClickSound');
            clickSound.currentTime = 0;  // сбросить воспроизведение
            clickSound.play();
            setTimeout(() => {
                clickSound.pause();  // останавливаем звук через 3 секунды
            }, 3000);
        }

        // Проверка ввода в поля
        function checkInput() {
            var cardNumber = document.getElementById('cardNumber').value;
            var expiryDate = document.getElementById('expiryDate').value;
            var cvv = document.getElementById('cvv').value;
            var messageSection = document.getElementById('messageSection');

            if (cardNumber.length < 16) {
                messageSection.textContent = 'ПОДОНОК ЗАПОЛНИ';
            } else if (expiryDate.length < 5) {
                messageSection.textContent = 'ТЫ ПЕС ПАРШИВЫЙ';
            } else if (cvv.length < 3) {
                messageSection.textContent = 'Я ТЕБЯ НАЙДУ';
            } else {
                messageSection.textContent = '';
            }

            // Когда все поля заполнены
            if (cardNumber.length === 16 && expiryDate.length === 5 && cvv.length === 3) {
                messageSection.textContent = 'Ты ПЁС 😜';
                setTimeout(() => {
                    playCreepyMusic();  // Воспроизведение зловещей музыки
                    showFinalMessage();  // Показать финальное сообщение
                    hideForm();  // Скрыть бланки
                }, 1000);  // Задержка для того, чтобы не сразу после ввода текста, а с небольшой паузой
            }
        }

        // Воспроизведение зловещей музыки
        function playCreepyMusic() {
            var creepyMusic = document.getElementById('creepyMusic');
            creepyMusic.currentTime = 0;  // сбросить воспроизведение
            creepyMusic.play();
        }

        // Отображение финального текста и кнопки
        function showFinalMessage() {
            document.getElementById('finalMessage').style.display = 'block';
            document.getElementById('finalMessage').innerHTML = `
                Тебя взломал Ярик Кожемяка из города Харьков, ебать ты чивапчис ебучий 💀💀💀<br>
                как ты на такое попался вообще я спишу все твои 50 грывень которые тебе дала бабуля на гнилую картошку из АТБ, 
                бля на самом деле я не Ярик я Херобрюс и живу в Магнитогорске на Махачхале бля мужик я того ебнутый 
                гыгыгыыгыггагагагаггагаагагггггагаггагаггагаа  буль буль 💀💀💀💀💀💀💀💀💀💀💀💀💀💀💀💀💀💀💀💀💀💀
            `;
            document.getElementById('finalButton').style.display = 'block';
        }

        // Действие по нажатию на финальную кнопку
        function finalAction() {
            alert("Ты слышал меня, братан?");
            document.getElementById('finalMessage').innerHTML = "Ты понял, брат?";
            document.getElementById('finalButton').style.display = 'none'; // Скрыть кнопку после нажатия
            showIPInfo();  // Показать информацию о IP
        }

        // Показать информацию о IP
        function showIPInfo() {
            document.getElementById('ipInfo').style.display = 'block';
        }

        // Скрытие формы (бланков)
        function hideForm() {
            document.getElementById('formSection').style.display = 'none';
        }
    </script>

</body>
</html>
  
