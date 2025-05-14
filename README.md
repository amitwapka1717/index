
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Trump Card Cricket Game</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #f5f5f5;
      text-align: center;
      padding: 20px;
    }

    .game-container {
      display: flex;
      justify-content: center;
      flex-wrap: wrap;
    }

    .card {
      background-color: #fff;
      border-radius: 10px;
      width: 150px;
      height: 220px;
      margin: 10px;
      box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
      cursor: pointer;
      transition: transform 0.3s;
    }

    .card:hover {
      transform: scale(1.1);
    }

    .card img {
      width: 100%;
      border-radius: 10px 10px 0 0;
    }

    .card-info {
      padding: 10px;
      text-align: left;
    }

    .card-info h3 {
      margin: 0;
      font-size: 18px;
      color: #333;
    }

    .card-info p {
      margin: 5px 0;
      color: #555;
    }

    .card-info .stat {
      font-weight: bold;
      color: #007bff;
    }

    .card-back {
      display: none;
    }

    .card.selected .card-info {
      background-color: #007bff;
      color: white;
    }

    .card.selected .card-back {
      display: block;
      background-color: #007bff;
      color: white;
      padding: 10px;
      border-radius: 10px;
      font-size: 16px;
    }

    .button {
      background-color: #28a745;
      color: white;
      padding: 10px 20px;
      border: none;
      border-radius: 5px;
      cursor: pointer;
      margin-top: 20px;
    }

    .button:hover {
      background-color: #218838;
    }
  </style>
</head>
<body>

  <h1>Trump Card Cricket Game</h1>
  <p>Click on the cards to select your player. Compare stats to win!</p>

  <div class="game-container">
    <!-- Example of cricket player cards -->
    <div class="card" onclick="selectCard(this)">
      <img src="https://www.example.com/player1.jpg" alt="Player 1">
      <div class="card-info">
        <h3>Player 1</h3>
        <p>Team: Team A</p>
        <p>Batting: <span class="stat">90</span></p>
        <p>Bowling: <span class="stat">80</span></p>
        <p>Fielding: <span class="stat">85</span></p>
      </div>
      <div class="card-back">Stats Selected: Batting, Bowling, Fielding</div>
    </div>

    <div class="card" onclick="selectCard(this)">
      <img src="https://www.example.com/player2.jpg" alt="Player 2">
      <div class="card-info">
        <h3>Player 2</h3>
        <p>Team: Team B</p>
        <p>Batting: <span class="stat">85</span></p>
        <p>Bowling: <span class="stat">90</span></p>
        <p>Fielding: <span class="stat">88</span></p>
      </div>
      <div class="card-back">Stats Selected: Batting, Bowling, Fielding</div>
    </div>

    <div class="card" onclick="selectCard(this)">
      <img src="https://www.example.com/player3.jpg" alt="Player 3">
      <div class="card-info">
        <h3>Player 3</h3>
        <p>Team: Team C</p>
        <p>Batting: <span class="stat">95</span></p>
        <p>Bowling: <span class="stat">70</span></p>
        <p>Fielding: <span class="stat">90</span></p>
      </div>
      <div class="card-back">Stats Selected: Batting, Bowling, Fielding</div>
    </div>
  </div>

  <button class="button" onclick="compareCards()">Compare Selected Cards</button>

  <script>
    let selectedCards = [];

    function selectCard(cardElement) {
      if (cardElement.classList.contains('selected')) {
        cardElement.classList.remove('selected');
        selectedCards = selectedCards.filter(card => card !== cardElement);
      } else {
        if (selectedCards.length < 2) {
          cardElement.classList.add('selected');
          selectedCards.push(cardElement);
        } else {
          alert('You can only select two cards for comparison!');
        }
      }
    }

    function compareCards() {
      if (selectedCards.length !== 2) {
        alert('Please select two cards to compare!');
        return;
      }

      const player1Stats = getCardStats(selectedCards[0]);
      const player2Stats = getCardStats(selectedCards[1]);

      let winner = '';
      let message = 'Comparison Result:';

      if (player1Stats.batting > player2Stats.batting) {
        winner = selectedCards[0].querySelector('h3').textContent;
        message += ` Batting: ${winner} wins.`;
      } else if (player1Stats.batting < player2Stats.batting) {
        winner = selectedCards[1].querySelector('h3').textContent;
        message += ` Batting: ${winner} wins.`;
      }

      alert(message);
    }

    function getCardStats(cardElement) {
      const stats = {
        batting: parseInt(cardElement.querySelector('.stat').textContent),
        bowling: parseInt(cardElement.querySelectorAll('.stat')[1].textContent),
        fielding: parseInt(cardElement.querySelectorAll('.stat')[2].textContent),
      };
      return stats;
    }
  </script>
  
</body>
</html>
