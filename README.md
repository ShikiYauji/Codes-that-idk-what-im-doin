<!DOCTYPE html>
<html>
<head>
  <title>Custom Order Application</title>
</head>
<body>
  <h1>Custom Order Application</h1>
  <form id="custom-order-form" onsubmit="submitForm()">
<p>   
    <label for="name">Name:</label>
    <input type="text" id="name" placeholder="John Smith" required><br>
</p>
<p>
    <label for="email">Email Address:</label>
    <input type="email" id="email" placeholder="JSmith123@example.com" required>
</p>
<script>
    const nameInput = document.getElementById('name');
    const emailInput = document.getElementById('email');
    const submitButton = document.getElementById('submit-button');

    submitButton.addEventListener('click', (event) => {
        if (!nameInput.checkValidity()) {
            alert('Please enter your name');
            event.preventDefault();
        }
        if (!emailInput.checkValidity()) {
            alert('Please enter a valid email address');
            event.preventDefault();
        }
    });
</script>

<label for="date">Completion Date:</label>
<input type="date" id="date" required min="<?php echo date('Y-m-d'); ?>" aria-describedby="date-description"><br>
<label><small id="date-description">Enter the date you'd like to see this order completed. Keep a grace period between the completion date and the actual date you need our product. If there is no rush for this order, enter the current date you are filling this form.</small></label>

<p>
  <label for="quantity">Quantity:</label>
  <small id="quantity-description"><em>Enter an estimated amount of soap.</em></small><br>
  <select id="quantity" required aria-describedby="quantity-description">
    <option value="" selected disabled>Select an option</option>
    <option value="5">5 lbs (min.)</option>
    <option value="9">5 - 9 lbs</option>
    <option value="14">10 - 14 lbs</option>
    <option value="19">15 - 19 lbs</option>
    <option value="24">20 - 24 lbs</option>
    <option value="25">25 lbs (max.)</option>
  </select><br>
</p>
<p>
  <label for="soap-type">Soap Type:</label>
  <small id="soap-type-description"><em>Select a base soap type. Each has unique properties.</em></small><br>
  <select id="soap-type" required aria-describedby="soap-type-description">
    <option value="" selected disabled>Select an option</option>
    <option value="Goat's Milk">Goat's Milk</option>
    <option value="Shea Butter">Shea Butter</option>
    <option value="Clear">Clear</option>
    <option value="Aloe Vera">Aloe Vera</option>
    <option value="Castile">Castile</option>
    <option value="Olive Oil">Olive Oil</option>
  </select><br>
</p>




<p>
  <label for="soap-shape">Soap Shape:</label>
  <small id="soap-shape-description"><em>Select the shape you'd like to see your soap as.</em></small><br>
  <select id="soap-shape" required onchange="showTextBox(this.value)" aria-describedby="soap-shape-description">
    <option value="" selected disabled>Select an option</option>
    <option value="rectangle">Rectangle</option>
    <option value="hexagon">Hexagon</option>
    <option value="rose-flowers">Rose Flowers</option>
    <option value="honeycomb">Honeycomb</option>
    <option value="large-hearts">Large Hearts</option>
    <option value="hearts">Hearts</option>
    <option value="moons">Moons</option>
    <option value="stars">Stars</option>
    <option value="10">Other</option>
  </select><br>
  <div id="shape-other" style="display:none;">
    <label for="soap-shape-other">Enter Other Shape:</label>
    <input type="text" id="soap-shape-other" name="soap-shape-other" placeholder="Enter Other Shapes" maxlength="100" required>
  </div>

  <script>
    function showTextBox(selectedValue) {
      var textboxDiv = document.getElementById("shape-other");
      if(selectedValue == "10") {
        textboxDiv.style.display = "block";
        document.getElementById("soap-shape-other").required = true;
      }
      else {
        textboxDiv.style.display = "none";
        document.getElementById("soap-shape-other").required = false;
      }
    }
  </script>

</p>
<p>
<label>Soap Color:</label>
<label><small id="soap-color-description">Select up to 4</small></label><br>
<label>
  <input type="checkbox" id="natural-base" name="soap-color[]" value="natural-base" onclick="selectColor('natural-base')">Natural Base Soap (No Color)
</label>
<br>

<label>
  <input type="checkbox" id="white" name="soap-color[]" value="white" onclick="selectColor('white')">White
</label>
<br>

<label>
  <input type="checkbox" id="red" name="soap-color[]" value="red" onclick="selectColor('red')">Red
</label>
<br>

<label>
  <input type="checkbox" id="violet" name="soap-color[]" value="violet" onclick="selectColor('violet')">Violet
</label>
<br>

<label>
  <input type="checkbox" id="jungle-green" name="soap-color[]" value="jungle-green" onclick="selectColor('jungle-green')">Jungle Green
</label>
<br>

<label>
  <input type="checkbox" id="ocean-blue" name="soap-color[]" value="ocean-blue" onclick="selectColor('ocean-blue')">Ocean Blue
</label>
<br>

<label>
  <input type="checkbox" id="lemon-yellow" name="soap-color[]" value="lemon-yellow" onclick="selectColor('lemon-yellow')">Lemon Yellow
</label>
<br>

<label>
  <input type="checkbox" id="dark-purple" name="soap-color[]" value="dark-purple" onclick="selectColor('dark-purple')">Dark Purple
</label>
<br>

<label>
  <input type="checkbox" id="chestnut-brown" name="soap-color[]" value="chestnut-brown" onclick="selectColor('chestnut-brown')">Chestnut Brown
</label>
<br>

<label>
  <input type="checkbox" id="other" name="soap-color[]" value="other" onclick="selectColor('other')">Other
</label>
<br>

<div id="other-colors" style="display:none;">
  <label for="other-colors-input">Enter up to 4 additional colors:</label>
  <br>
  <input type="text" id="other-colors-input" name="other-colors-input" maxlength="100">
</div>

<script>
function selectColor(selectedColor) {
  var selectedColors = document.getElementsByName("soap-color[]");
  var selectedColorCount = 0;
  var otherColorsDiv = document.getElementById("other-colors");

  for(var i = 0; i < selectedColors.length; i++) {
    if(selectedColors[i].checked) {
      selectedColorCount++;
    }
  }

  if(selectedColorCount > 4) {
    alert("You can only select up to 4 colors.");
    document.getElementById(selectedColor).checked = false;
    return;
  }

  if(selectedColor == "other") {
    otherColorsDiv.style.display = "block";
  }
  else {
    otherColorsDiv.style.display = "none";
  }
}
</script>
</p>
<p>
  <label>Fragrance:</label>
<label><small>Select up to 4</small></label><br>

<label>
  <input type="checkbox" name="fragrance" value="no-fragrance">No Fragrance
</label>
<br>
<label>
  <input type="checkbox" name="fragrance" value="Oatmeal-milk-honey">Oatmeal Milk & Honey
</label>
<br>
<label>
  <input type="checkbox" name="fragrance" value="Lavender">Lavender
</label>
<br>
<label>
  <input type="checkbox" name="fragrance" value="Jasmine">Jasmine
</label>
<br>
<label>
  <input type="checkbox" name="fragrance" value="Roses">Roses
</label>
<br>
<label>
  <input type="checkbox" name="fragrance" value="Rum">Rum
</label>
<br>
<label>
  <input type="checkbox" name="fragrance" value="Vanilla">Vanilla
</label>
<br>
<label>
  <input type="checkbox" name="fragrance" value="Amber">Amber
</label>
<br>
<label>
  <input type="checkbox" name="fragrance" value="Tobacco">Tobacco
</label>
<br>
<label>
  <input type="checkbox" name="fragrance" value="Linen">Linen
</label>
<br>
<label>
  <input type="checkbox" name="fragrance" value="Aloe">Aloe
</label>
<br>
<label>
  <input type="checkbox" name="fragrance" value="Lily-of-the-valley">Lily of the Valley
</label>
<br>
<label>
  <input type="checkbox" name="fragrance" value="Green-tea">Green Tea
</label>
<br>
<label>
  <input type="checkbox" name="fragrance" value="fragrance-other" onclick="showTextBox()">Other
</label>
<br>
<div id="fragrance-other" style="display:none;">
  <label for="fragrance-other-text">Enter Desired Fragrance:</label>
  <input type="text" id="fragrance-other-text" name="fragrance-other-text" placeholder="Enter Desired Fragrance" maxlength="100">
</div>
<script>
  function showTextBox() {
    var textboxDiv = document.getElementById("fragrance-other");
    var checkboxes = document.querySelectorAll('input[name="fragrance"]:checked');

    if (checkboxes.length > 4) {
      alert("You can select up to 4 options only.");
      return;
    }

    if (document.getElementsByName('fragrance').checked) {
      textboxDiv.style.display = "block";
      document.getElementById("fragrance-other-text").required = true;
    } else {
      textboxDiv.style.display = "none";
      document.getElementById("fragrance-other-text").required = false;
    }
  }
</script>
</p>
<p>
  <label>Additive:</label> Let's spice up your soap!
  <br>

<label><small>Select up to 6</small></label><br>
<br>
  <i>Salts?</i>
  <br>
  <label>
    <input type="checkbox" name="salts" value="Dead-sea">Dead Sea Salt
  </label>
  <br>
  <label>
    <input type="checkbox" name="salts" value="black-hawaiian">Black Hawaiian Sea Salt
  </label>
  <br>
  <label>
    <input type="checkbox" name="salts" value="pink-himalayan">Pink Himalayan Salt
  </label>
  <br><br>

  <i>Powder?</i>
  <br>
  <label>
    <input type="checkbox" name="powder" value="spinach">Spinach Powder
  </label>
  <br>
  <label>
    <input type="checkbox" name="powder" value="activated">Activated Charcoal
  </label>
  <br><br>

  <i>Clays?</i>
  <br>
  <label>
    <input type="checkbox" name="clays" value="Moroccan">Moroccan
  </label>
  <br>
  <label>
    <input type="checkbox" name="clays" value="White-kaolin">White Kaolin
  </label>
  <br>
  <label>
    <input type="checkbox" name="clays" value="red-kaolin">Red Kaolin
  </label>
    <br>
  <label>
    <input type="checkbox" name="clays" value="Rhassoul">Rhassoul
  </label>
  <br>
    <label>
    <input type="checkbox" name="clays" value="bentonite">Bentonite
  </label>
  <br><br>

  <i>Florals?</i>
  <br>
  <label>
    <input type="checkbox" name="florals" value="lavender">Lavender Buds
  </label>
  <br>
    <label>
    <input type="checkbox" name="florals" value="spearmint">Spearmint
  </label>
  <br>
   <label>
    <input type="checkbox" name="florals" value="peppermint">Peppermint
  </label>
  <br>
  <label>
    <input type="checkbox" name="florals" value="rose">Rose Petals
  </label>
  <br>
  <label>
    <input type="checkbox" name="florals" value="hibiscus">Hibiscus Flowers
  </label>
  <br><br>

  <i>Other?</i>
  <br>
  <input type="text" name="other" placeholder="Enter Up to 6 Non-listed Additives" maxlength="100">
</p>

<script>
  var checkboxes = document.querySelectorAll('input[type="checkbox"]');
  var otherInput = document.querySelector('input[name="other"]');

  function updateCheckedStatus() {
    var checkedCount = 0;

    checkboxes.forEach(function(checkbox) {
      if (checkbox.checked) {
        checkedCount++;
      }
    });

    if (checkedCount >= 6) {
      checkboxes.forEach(function(checkbox) {
        if (!checkbox.checked) {
          checkbox.disabled = true;
        }
      });
      otherInput.disabled = true;
    } else {
      checkboxes.forEach(function(checkbox) {
        checkbox.disabled = false;
      });
      otherInput.disabled = false;
    }
  }

  checkboxes.forEach(function(checkbox) {
    checkbox.addEventListener('change', function() {
      updateCheckedStatus();
    });
  });
</script>
<label for="decoration">Decoration:</label>
<em><small>Tell us how you want your soaps decorated and packaged!</small></em>
<br><br>
<textarea id="decoration" name="decoration" rows="8" cols="50" placeholder="Example: Custom labels, wax paper, assorted colored cardstock, windowed boxes, etc."></textarea>
<br><br>

<label for="comment-box">Have a question, comment, or concern?</label>
<br>
<textarea id="comment-box" name="comment-box" rows="8" cols="50" placeholder="Let us know here!"></textarea>

<br><br>
<button onclick="sendEmail()">Submit</button>
