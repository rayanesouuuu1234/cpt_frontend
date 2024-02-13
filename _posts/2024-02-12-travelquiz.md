<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Travel Recommendation Quiz</title>
</head>
<body>
<h1>Welcome to the Travel Recommendation Quiz!</h1>
<p>Answer the following questions to find out where you should travel.</p>

<div id="quiz">
  <div class="question">What type of climate do you prefer?
    <ul>
      <li><input type="radio" name="q1" value="Italy"> Sunny and Mediterranean</li>
      <li><input type="radio" name="q1" value="Iceland"> Cool and Nordic</li>
      <li><input type="radio" name="q1" value="Thailand"> Warm and Tropical</li>
      <li><input type="radio" name="q1" value="Switzerland"> Crisp and Alpine</li>
    </ul>
  </div>
  <div class="question">What activity sounds most appealing to you?
    <ul>
      <li><input type="radio" name="q2" value="Italy"> Exploring ancient ruins</li>
      <li><input type="radio" name="q2" value="Iceland"> Chasing Northern Lights</li>
      <li><input type="radio" name="q2" value="Thailand"> Relaxing on beautiful beaches</li>
      <li><input type="radio" name="q2" value="Switzerland"> Skiing in the mountains</li>
    </ul>
  </div>
  <div class="question">What type of cuisine are you most interested in trying?
    <ul>
      <li><input type="radio" name="q3" value="Italy"> Pasta, Pizza, Gelato</li>
      <li><input type="radio" name="q3" value="Iceland"> Fresh seafood</li>
      <li><input type="radio" name="q3" value="Thailand"> Spicy Thai dishes</li>
      <li><input type="radio" name="q3" value="Switzerland"> Swiss chocolate and cheese</li>
    </ul>
  </div>
  <div class="question">What scenery would you like to wake up to?
    <ul>
      <li><input type="radio" name="q4" value="Italy"> Views of rolling hills and vineyards</li>
      <li><input type="radio" name="q4" value="Iceland"> Vast landscapes with glaciers</li>
      <li><input type="radio" name="q4" value="Thailand"> Palm trees and turquoise waters</li>
      <li><input type="radio" name="q4" value="Switzerland"> Snow-capped mountains and pristine lakes</li>
    </ul>
  </div>
  <button onclick="calculateDestination()">Submit</button>
</div>

<script>
function calculateDestination() {
  const answers = document.querySelectorAll('input[type="radio"]:checked');
  const destinationScores = {
    "Italy": 0,
    "Iceland": 0,
    "Thailand": 0,
    "Switzerland": 0
  };

  answers.forEach(answer => {
    destinationScores[answer.value] += 1;
  });

  const recommendedDestination = Object.keys(destinationScores).reduce((a, b) => destinationScores[a] > destinationScores[b] ? a : b);
  alert("Based on your answers, we recommend you travel to " + recommendedDestination + "!");
}
</script>

</body>
</html>
