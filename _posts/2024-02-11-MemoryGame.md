
<html lang="en"><head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Emoji Memory Game</title>
<style>
  .grid {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 10px;
    margin: 20px auto;
    max-width: 600px;
  }
  .card {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100px;
    background-color: #f0f0f0;
    font-size: 2rem;
    cursor: pointer;
  }
  .hidden {
    background-color: #9e9e9e;
  }
</style>
</head>
<body>
<div id="game" class="grid"></div>

<script>
const emojis = ['😀', '😃', '😄', '😁', '😆', '😅', '😂', '🤣', '😊', '😇', '🙂', '🙃', '😉', '😌', '😍', '🥰'];
let selectedEmojis = emojis.slice(0, 8); // Use only 8 emojis for 16 cards
selectedEmojis = [...selectedEmojis, ...selectedEmojis]; // Duplicate emojis for pairs
selectedEmojis.sort(() => 0.5 - Math.random()); // Shuffle the emojis

const game = document.getElementById('game');
let hasFlippedCard = false;
let lockBoard = false;
let firstCard, secondCard;

function createBoard() {
  for (let i = 0; i < 16; i++) {
    const card = document.createElement('div');
    card.classList.add('card', 'hidden');
    card.setAttribute('data-emoji', selectedEmojis[i]);
    card.addEventListener('click', flipCard);
    game.appendChild(card);
  }
}

function flipCard() {
  if (lockBoard) return;
  if (this === firstCard) return;

  this.classList.remove('hidden');
  this.innerHTML = this.getAttribute('data-emoji');

  if (!hasFlippedCard) {
    hasFlippedCard = true;
    firstCard = this;
    return;
  }

  secondCard = this;
  checkForMatch();
}

function checkForMatch() {
  const isMatch = firstCard.getAttribute('data-emoji') === secondCard.getAttribute('data-emoji');
  isMatch ? disableCards() : unflipCards();
}

function disableCards() {
  firstCard.removeEventListener('click', flipCard);
  secondCard.removeEventListener('click', flipCard);
  resetBoard();
}

function unflipCards() {
  lockBoard = true;

  setTimeout(() => {
    firstCard.classList.add('hidden');
    secondCard.classList.add('hidden');
    firstCard.innerHTML = '';
    secondCard.innerHTML = '';
    resetBoard();
  }, 1500);
}

function resetBoard() {
  [hasFlippedCard, lockBoard] = [false, false];
  [firstCard, secondCard] = [null, null];
}

createBoard();
</script>
</body>
</html>
