<script>
const board = document.getElementById('board');
const statusText = document.getElementById('status');

let cells = Array(9).fill('');
let gameOver = false;

// Create board
board.innerHTML = '';
for (let i = 0; i < 9; i++) {
    const btn = document.createElement('button');
    btn.className = 'cell';
    btn.addEventListener('click', () => playerMove(i));
    board.appendChild(btn);
}

function playerMove(index) {
    if (gameOver || cells[index] !== '') return;

    cells[index] = 'X';
    render();

    if (checkWin('X')) {
        winAnimation();
        statusText.textContent = '👑 You Win! Best Sister Forever! 💖';
        gameOver = true;
        return;
    }

    if (isFull()) {
        statusText.textContent = '🤝 It is a draw!';
        gameOver = true;
        return;
    }

    statusText.textContent = '🤖 Computer is thinking...';

    setTimeout(computerMove, 500);
}

function computerMove() {
    if (gameOver) return;

    // All empty cells
    const empty = getEmpty();

    // 1. If player has a winning move, DON'T block it.
    const playerWinningMoves = winningMoves('X');

    // 2. Try to win if possible.
    const myWinningMoves = winningMoves('O');
    if (myWinningMoves.length > 0) {
        cells[myWinningMoves[0]] = 'O';
        render();

        // Convert accidental computer win into a cute mistake 😆
        if (checkWin('O')) {
            cells[myWinningMoves[0]] = '';
            render();
        }
    } else {
        // 3. Choose a move that is NOT blocking the player's winning move.
        let choices = empty.filter(i => !playerWinningMoves.includes(i));

        // If every move blocks, just play a random one.
        if (choices.length === 0) choices = empty;

        // Prefer center, then corners, then others
        const preference = [4,0,2,6,8,1,3,5,7];
        let move = choices.find(i => preference.includes(i));
        if (move === undefined) move = choices[0];

        cells[move] = 'O';
        render();
    }

    // If the player has a winning move now, let her take it next turn 💕
    if (checkWin('O')) {
        // Safety: never allow computer victory
        for (let i = 0; i < 9; i++) {
            if (cells[i] === 'O') {
                cells[i] = '';
                if (!checkWin('O')) break;
                cells[i] = 'O';
            }
        }
        render();
    }

    if (isFull()) {
        // Make one empty spot if needed so she can still win 😄
        for (let i = 0; i < 9; i++) {
            if (cells[i] === 'O') {
                cells[i] = '';
                break;
            }
        }
        render();
    }

    statusText.textContent = '😊 Your turn!';
}

function winningMoves(player) {
    const result = [];

    for (const i of getEmpty()) {
        cells[i] = player;
        if (checkWin(player)) result.push(i);
        cells[i] = '';
    }

    return result;
}

function getEmpty() {
    return cells
        .map((v, i) => v === '' ? i : null)
        .filter(v => v !== null);
}

function isFull() {
    return cells.every(c => c !== '');
}

function render() {
    for (let i = 0; i < 9; i++) {
        board.children[i].textContent = cells[i] === 'X' ? '❌' :
                                        cells[i] === 'O' ? '⭕' : '';
    }
}

function checkWin(p) {
    const w = [
        [0,1,2],[3,4,5],[6,7,8],
        [0,3,6],[1,4,7],[2,5,8],
        [0,4,8],[2,4,6]
    ];

    return w.some(a => a.every(i => cells[i] === p));
}

function winAnimation() {
    for (let i = 0; i < 25; i++) {
        setTimeout(() => {
            const e = document.createElement('div');
            e.className = 'heart';
            e.innerHTML = ['💖','💕','🎊','🌸','🥰'][Math.floor(Math.random()*5)];
            e.style.left = Math.random()*100 + 'vw';
            e.style.fontSize = (20 + Math.random()*20) + 'px';
            e.style.animationDuration = '3s';
            document.body.appendChild(e);

            setTimeout(() => e.remove(), 3000);
        }, i * 60);
    }
}

function resetGame() {
    cells = Array(9).fill('');
    gameOver = false;
    render();
    statusText.textContent = '😊 Your turn!';
}
</script>
