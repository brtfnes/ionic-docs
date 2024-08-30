<!DOCTYPE html>
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Box Number Oyunu</title>
    <link rel="icon" href="favicon.ico" type="image/x-icon">
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <div id="loading-screen">
        <h1>Box Number Oyunu Yükleniyor...</h1>
        <div class="loader"></div>
    </div>

    <div id="game-select" style="display: none;">
        <h1>Oyun Etabı Seçin</h1>
        <div id="stage-buttons">
            <button class="stage-button" data-size="5">5x5</button>
            <button class="stage-button" data-size="6">6x6</button>
            <button class="stage-button" data-size="7">7x7</button>
            <button class="stage-button" data-size="8">8x8</button>
            <button class="stage-button" data-size="9">9x9</button>
            <button class="stage-button" data-size="10">10x10</button>
        </div>
    </div>

    <div id="game-area" style="display: none;">
        <div id="game-menu">
            <button id="game-menu-button" class="button">Oyun Menüsü</button>
            <div id="game-menu-content" class="dropdown-content">
                <button id="reset-game" class="button">Yeniden Başlat</button>
                <button id="pause-game" class="button">Duraklat</button>
                <button id="show-rules" class="button">Kurallar</button>
                <button id="back-to-select" class="button">Etap Seçimine Dön</button>
            </div>
        </div>
        <div id="game-info">
            <div id="timer">Süre: <span>00:00</span></div>
            <div id="score">Skor: <span>0</span></div>
        </div>
        <div id="grid"></div>
        <div id="last-number">Son rakam: <span>1</span></div>
    </div>

    <div id="rules-popup" class="popup" style="display: none;">
        <div class="popup-content">
            <h2>Oyun Kuralları</h2>
            <ul>
                <li>1'den başlayarak sırayla sayıları yerleştirmelisiniz.</li>
                <li>İlk sayıyı istediğiniz yere koyabilirsiniz.</li>
                <li>Sonraki sayılar için geçerli hamleler:</li>
                <ul>
                    <li>Yatay veya dikey olarak 3 kare atlayabilirsiniz.</li>
                    <li>Çapraz olarak 2 kare atlayabilirsiniz.</li>
                </ul>
                <li>Tüm sayıları yerleştirmeye çalışın!</li>
            </ul>
            <button id="close-rules" class="button">Kapat</button>
        </div>
    </div>

    <div id="game-over-popup" class="popup" style="display: none;">
        <div class="popup-content">
            <h2>Oyun Bitti!</h2>
            <p>Süre: <span id="final-time"></span></p>
            <p>Skor: <span id="final-score"></span></p>
            <button id="play-again" class="button">Tekrar Oyna</button>
            <button id="back-to-select-end" class="button">Etap Seçimine Dön</button>
        </div>
    </div>

    <script src="script.js"></script>
</body>
</html>
body {
    font-family: Arial, sans-serif;
    margin: 0;
    padding: 0;
    text-align: center;
    background: url('background.jpg') no-repeat center center fixed;
    background-size: cover;
    color: #333;
}

#loading-screen, #game-select, #game-area {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    min-height: 100vh;
    background-color: rgba(255, 255, 255, 0.8);
}

.loader {
    border: 16px solid #f3f3f3;
    border-top: 16px solid #3498db;
    border-radius: 50%;
    width: 120px;
    height: 120px;
    animation: spin 2s linear infinite;
}

@keyframes spin {
    0% { transform: rotate(0deg); }
    100% { transform: rotate(360deg); }
}

.button, .stage-button {
    padding: 10px 20px;
    margin: 10px;
    font-size: 16px;
    cursor: pointer;
    background-color: #4CAF50;
    color: white;
    border: none;
    border-radius: 5px;
    transition: background-color 0.3s;
}

.button:hover, .stage-button:hover {
    background-color: #45a049;
}

#game-area {
    padding: 20px;
    background-color: rgba(255, 255, 255, 0.9);
    border-radius: 10px;
    margin: 20px auto;
    max-width: 95%;
    height: auto;
}

#game-menu {
    position: relative;
    margin-bottom: 20px;
}

#game-menu-button {
    font-size: 24px;
    padding: 5px 10px;
}

.dropdown-content {
    display: none;
    position: absolute;
    background-color: #f9f9f9;
    min-width: 160px;
    box-shadow: 0px 8px 16px 0px rgba(0,0,0,0.2);
    z-index: 1;
}

.dropdown-content button {
    display: block;
    width: 100%;
    text-align: left;
}

#game-info {
    display: flex;
    justify-content: center;
    margin-bottom: 20px;
    width: 100%;
}

#timer, #score {
    font-size: 18px;
    font-weight: bold;
    margin: 0 10px;
}

#grid {
    display: grid;
    grid-gap: 2px;
    margin: 20px auto;
    width: max-content;
}

.cell {
    width: 35px;
    height: 35px;
    border: 1px solid #000;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 14px;
    background-color: #f0f0f0;
    transition: background-color 0.3s;
    cursor: pointer;
}

.cell:hover {
    background-color: #e0e0e0;
}

.cell.filled {
    background-color: #4CAF50;
    color: white;
}

#last-number {
    font-size: 18px;
    margin: 20px 0;
}

.popup {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 1000;
}

.popup-content {
    background-color: white;
    padding: 20px;
    border-radius: 10px;
    max-width: 500px;
    text-align: left;
}

.popup-content h2 {
    margin-top: 0;
}

.popup-content ul {
    padding-left: 20px;
}

.popup-content li {
    margin-bottom: 10px;
}

#stage-buttons {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
}

@media (max-width: 600px) {
    .cell {
        width: 30px;
        height: 30px;
        font-size: 12px;
    }
}
document.addEventListener('DOMContentLoaded', () => {
    const loadingScreen = document.getElementById('loading-screen');
    const gameSelect = document.getElementById('game-select');
    const gameArea = document.getElementById('game-area');
    const grid = document.getElementById('grid');
    const timerDisplay = document.getElementById('timer').querySelector('span');
    const scoreDisplay = document.getElementById('score').querySelector('span');
    const lastNumberDisplay = document.getElementById('last-number').querySelector('span');
    const resetGameButton = document.getElementById('reset-game');
    const pauseGameButton = document.getElementById('pause-game');
    const showRulesButton = document.getElementById('show-rules');
    const rulesPopup = document.getElementById('rules-popup');
    const closeRulesButton = document.getElementById('close-rules');
    const gameOverPopup = document.getElementById('game-over-popup');
    const finalTimeDisplay = document.getElementById('final-time');
    const finalScoreDisplay = document.getElementById('final-score');
    const playAgainButton = document.getElementById('play-again');
    const backToSelectButton = document.getElementById('back-to-select');
    const backToSelectEndButton = document.getElementById('back-to-select-end');
    const stageButtons = document.querySelectorAll('.stage-button');
    const gameMenuButton = document.getElementById('game-menu-button');
    const gameMenuContent = document.getElementById('game-menu-content');

    let numbers = [];
    let currentNumber = 1;
    let interval;
    let seconds = 0;
    let score = 0;
    let isPaused = false;
    let gridSize = 5;
    let maxNumber = 25;

    function startTimer() {
        interval = setInterval(() => {
            if (!isPaused) {
                seconds++;
                updateTimerDisplay();
            }
        }, 1000);
    }

    function updateTimerDisplay() {
        let minutes = Math.floor(seconds / 60);
        let secs = seconds % 60;
        timerDisplay.textContent = `${minutes < 10 ? '0' : ''}${minutes}:${secs < 10 ? '0' : ''}${secs}`;
    }

    function stopTimer() {
        clearInterval(interval);
    }

    function setupGame() {
        grid.innerHTML = '';
        numbers = Array(gridSize * gridSize).fill(0);
        grid.style.gridTemplateColumns = `repeat(${gridSize}, 35px)`;
        for (let i = 0; i < gridSize * gridSize; i++) {
            const cell = document.createElement('div');
            cell.classList.add('cell');
            cell.dataset.index = i;
            cell.addEventListener('click', () => makeMove(i));
            grid.appendChild(cell);
        }
    }

    function makeMove(index) {
        if (isPaused) return;
        if (numbers[index] === 0 && isValidMove(index)) {
            numbers[index] = currentNumber;
            grid.children[index].textContent = currentNumber;
            grid.children[index].classList.add('filled');
            lastNumberDisplay.textContent = currentNumber;
            currentNumber++;
            updateScore();
            checkGameEnd();
        }
    }

    function isValidMove(index) {
        if (currentNumber === 1) return true;

        const lastIndex = numbers.indexOf(currentNumber - 1);
        if (lastIndex === -1) return false;

        const row = Math.floor(index / gridSize);
        const col = index % gridSize;
        const lastRow = Math.floor(lastIndex / gridSize);
        const lastCol = lastIndex % gridSize;

        if (Math.abs(row - lastRow) === 3 && col === lastCol) return true;
        if (Math.abs(col - lastCol) === 3 && row === lastRow) return true;
        if (Math.abs(row - lastRow) === 2 && Math.abs(col - lastCol) === 2) return true;

        return false;
    }

    function updateScore() {
        score += 10;
        scoreDisplay.textContent = score;
    }

    function checkGameEnd() {
        const validMovesLeft = numbers.some((num, index) => num === 0 && isValidMove(index));
        if (currentNumber > maxNumber || !validMovesLeft) {
            stopTimer();
            showGameOverPopup();
        }
    }

    function showGameOverPopup() {
        finalTimeDisplay.textContent = timerDisplay.textContent;
        finalScoreDisplay.textContent = score;
        gameOverPopup.style.display = 'flex';
    }

    function startGame() {
        setupGame();
        currentNumber = 1;
        seconds = 0;
        score = 0;
        isPaused = false;
        updateTimerDisplay();
        scoreDisplay.textContent = '0';
        lastNumberDisplay.textContent = '1';
        startTimer();
        pauseGameButton.textContent = 'Duraklat';
    }

    function showLoadingScreen() {
        loadingScreen.style.display = 'flex';
        gameSelect.style.display = 'none';
        gameArea.style.display = 'none';
        setTimeout(() => {
            loadingScreen.style.display = 'none';
            gameSelect.style.display = 'flex';
        }, 2000);
    }

    stageButtons.forEach(button => {
        button.addEventListener('click', () => {
            gridSize = parseInt(button.dataset.size);
            maxNumber = gridSize * gridSize;
            gameSelect.style.display = 'none';
            gameArea.style.display = 'flex';
            startGame();
        });
    });

    resetGameButton.addEventListener('click', () => {
        startGame();
        gameMenuContent.style.display = 'none';
    });

    pauseGameButton.addEventListener('click', () => {
        isPaused = !isPaused;
        pauseGameButton.textContent = isPaused ? 'Devam Et' : 'Duraklat';
        gameMenuContent.style.display = 'none';
    });

    showRulesButton.addEventListener('click', () => {
        rulesPopup.style.display = 'flex';
        gameMenuContent.style.display = 'none';
    });

    closeRulesButton.addEventListener('click', () => {
        rulesPopup.style.display = 'none';
    });

    playAgainButton.addEventListener('click', () => {
        gameOverPopup.style.display = 'none';
        startGame();
    });

    backToSelectButton.addEventListener('click', () => {
        gameArea.style.display = 'none';
        gameSelect.style.display = 'flex';
        stopTimer();
        gameMenuContent.style.display = 'none';
    });

    backToSelectEndButton.addEventListener('click', () => {
        gameOverPopup.style.display = 'none';
        gameArea.style.display = 'none';
        gameSelect.style.display = 'flex';
    });

    gameMenuButton.addEventListener('click', () => {
        gameMenuContent.style.display = gameMenuContent.style.display === 'none' ? 'block' : 'none';
    });

    document.addEventListener('click', (event) => {
        if (!gameMenuButton.contains(event.target) && !gameMenuContent.contains(event.target)) {
            gameMenuContent.style.display = 'none';
        }
    });

    showLoadingScreen();
});
