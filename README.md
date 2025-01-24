# Speed-click-
Jogue para treinar sua agilidade 
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta name="description" content="Teste sua velocidade de clique no jogo Click Speed! Clique o mais rápido possível em 30 segundos e veja sua pontuação. Divirta-se agora mesmo!">
    <meta name="keywords" content="Click Speed, velocidade de clique, jogo de clique, teste de clique, reflexos">
    <meta name="author" content="Seu Nome ou Empresa">
    <title>Click Speed - Teste Sua Velocidade de Clique</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #282c34;
            color: white;
            text-align: center;
        }
        h1 {
            margin-top: 20px;
        }
        #gameArea {
            position: relative;
            width: 90%;
            max-width: 600px;
            height: 400px;
            background-color: #444;
            margin: 20px auto;
            overflow: hidden;
            border: 2px solid white;
            border-radius: 10px;
        }
        .circle {
            position: absolute;
            width: 50px;
            height: 50px;
            background-color: #1a73e8;
            border-radius: 50%;
            cursor: pointer;
            animation: disappear 1.5s ease-out forwards;
        }
        @keyframes disappear {
            0% { opacity: 1; }
            100% { opacity: 0; }
        }
        #score, #timer {
            font-size: 24px;
            margin: 10px;
        }
        button {
            background-color: #1a73e8;
            color: white;
            padding: 10px 20px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            margin: 10px;
        }
        button:hover {
            background-color: #155db2;
        }
        @media (max-width: 600px) {
            #gameArea {
                height: 300px;
            }
            .circle {
                width: 40px;
                height: 40px;
            }
        }
    </style>
</head>
<body>
    <h1>Click Speed</h1>
    <p id="score">Pontos: 0</p>
    <p id="timer">Tempo: 30s</p>
    <div id="gameArea"></div>
    <button id="startButton" onclick="startGame()">Iniciar Jogo</button>

    <script>
        let score = 0;
        let timeLeft = 30;
        let gameInterval, timerInterval;

        function startGame() {
            score = 0;
            timeLeft = 30;
            document.getElementById('score').textContent = 'Pontos: 0';
            document.getElementById('timer').textContent = 'Tempo: 30s';
            document.getElementById('startButton').style.display = 'none'; // Esconder botão iniciar

            // Limpar área do jogo
            const gameArea = document.getElementById('gameArea');
            gameArea.innerHTML = '';

            // Iniciar jogo
            gameInterval = setInterval(spawnCircle, 1000);
            timerInterval = setInterval(updateTimer, 1000);
        }

        function spawnCircle() {
            const gameArea = document.getElementById('gameArea');
            const circle = document.createElement('div');
            circle.classList.add('circle');

            // Garantir que largura e altura da área estão disponíveis
            const gameAreaWidth = gameArea.offsetWidth || 300;
            const gameAreaHeight = gameArea.offsetHeight || 300;

            // Posição aleatória
            const x = Math.random() * (gameAreaWidth - 50);
            const y = Math.random() * (gameAreaHeight - 50);
            circle.style.left = `${x}px`;
            circle.style.top = `${y}px`;

            // Clique no círculo
            circle.onclick = () => {
                score++;
                document.getElementById('score').textContent = `Pontos: ${score}`;
                circle.remove();
            };

            // Adicionar ao jogo
            gameArea.appendChild(circle);

            // Remover círculo após 1.5s
            setTimeout(() => {
                if (circle.parentElement) {
                    circle.remove();
                }
            }, 1500);
        }

        function updateTimer() {
            timeLeft--;
            document.getElementById('timer').textContent = `Tempo: ${timeLeft}s`;
            if (timeLeft <= 0) {
                clearInterval(gameInterval);
                clearInterval(timerInterval);
                endGame();
            }
        }

        function endGame() {
            alert(`Fim de jogo! Sua pontuação: ${score}`);
            document.getElementById('startButton').textContent = 'Jogar Novamente';
            document.getElementById('startButton').style.display = 'block'; // Mostrar botão de jogar novamente
        }
    </script>
</body>
</html>
