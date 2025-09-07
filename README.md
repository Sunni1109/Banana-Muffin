# Banana-Muffin
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Banana Recipe Scaler</title>
  <style>
    body { font-family: Arial, sans-serif; padding: 20px; line-height: 1.6; }
    input, button { margin: 5px 0; padding: 5px; }
    ul { margin-top: 10px; }
  </style>
</head>
<body>
  <h2>Banana Recipe Scaler</h2>
  <label for="bananas">How many bananas do you have?</label><br>
  <input type="number" id="bananas" value="3" min="1" step="0.5"><br>
  <button onclick="scaleRecipe()">Recalculate</button>

  <h3>Ingredients:</h3>
  <ul id="ingredients"></ul>

  <script>
    // Base recipe (for 3 bananas)
    const baseBananas = 3;
    const baseRecipe = {
      "Bananas (large, ripe, mashed)": 3,
      "Melted unsalted butter (tablespoons)": 6,
      "Granulated sugar (cups)": 0.5,
      "Brown sugar (cups)": 0.5,
      "Eggs (large)": 1,
      "Vanilla extract (teaspoons)": 1,
      "All-purpose flour (cups)": 1.5,
      "Baking soda (teaspoons)": 0.75,
      "Baking powder (teaspoons)": 0.5,
      "Sour cream (cups)": 0.25,
      "Salt (pinch)": 1,
      "Semi-sweet chocolate chips (cups)": 0.75
    };

    function scaleRecipe() {
      const bananas = parseFloat(document.getElementById("bananas").value);
      const scaleFactor = bananas / baseBananas;
      const ingredientsList = document.getElementById("ingredients");
      ingredientsList.innerHTML = "";

      for (let item in baseRecipe) {
        let amount = baseRecipe[item] * scaleFactor;

        // Special handling for salt
        if (item.includes("Salt")) {
          ingredientsList.innerHTML += `<li>${item}: ${scaleFactor === 1 ? "Pinch" : (amount.toFixed(2) + " pinches")}</li>`;
        } else {
          ingredientsList.innerHTML += `<li>${item}: ${amount.toFixed(2)}</li>`;
        }
      }
    }

    // Run once on load
    scaleRecipe();
  </script>
</body>
</html>
