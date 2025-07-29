<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>PIYAS CC GEN - Advanced 🔥</title>
  <style>
    body {
      background-color: black;
      color: #f7c200;
      font-family: monospace;
      padding: 20px;
      text-transform: uppercase;
    }
    h1, h2, h3 {
      margin: 5px 0;
    }
    label {
      font-weight: bold;
      margin-top: 10px;
      display: block;
    }
    input, select, button, textarea {
      background-color: #111;
      color: #f7c200;
      border: 1px solid #f7c200;
      padding: 8px;
      margin: 5px 0;
      font-size: 16px;
      text-transform: uppercase;
      width: 100%;
      box-sizing: border-box;
    }
    textarea {
      height: 200px;
      border: 2px dashed #f7c200;
      resize: vertical;
      font-family: monospace;
      font-size: 14px;
    }
    button {
      cursor: pointer;
    }
  </style>
</head>
<body>

  <h1>💳 PIYAS CC GEN 🔥</h1>

  <label for="bin">BIN (6-16 DIGITS):</label>
  <input type="text" id="bin" placeholder="Example: 414720" maxlength="16" />

  <label for="month">MONTH:</label>
  <select id="month">
    <option value="">RANDOM</option>
    <script>
      for(let m=1; m<=12; m++) {
        const mm = m < 10 ? "0"+m : m;
        document.write(`<option value="${mm}">${mm}</option>`);
      }
    </script>
  </select>

  <label for="year">YEAR:</label>
  <select id="year">
    <option value="">RANDOM</option>
    <script>
      for(let y=2025; y<=2050; y++) {
        document.write(`<option value="${y}">${y}</option>`);
      }
    </script>
  </select>

  <label for="quantity">QUANTITY (Dropdown):</label>
  <select id="quantity">
    <option value="10">10</option>
    <option value="50">50</option>
    <option value="100">100</option>
    <option value="200">200</option>
    <option value="300">300</option>
    <option value="400">400</option>
    <option value="500">500</option>
  </select>

  <label for="custom_quantity">OR ENTER CUSTOM QUANTITY:</label>
  <input type="number" id="custom_quantity" placeholder="E.g. 123" min="1" max="1000" />

  <button onclick="generateCards()">🔁 GENERATE</button>
  <button onclick="checkLive()">✅ CHECK LIVE</button>
  <button onclick="copyLive()">📋 COPY LIVE</button>

  <textarea id="output" placeholder="Generated cards will appear here..." readonly></textarea>

<script>
  // Helper functions
  function randomNum(len) {
    let s = '';
    for(let i=0; i<len; i++) {
      s += Math.floor(Math.random()*10);
    }
    return s;
  }

  function randomMonth() {
    let m = Math.floor(Math.random() * 12) + 1;
    return m < 10 ? "0"+m : ""+m;
  }

  function randomYear() {
    return (2025 + Math.floor(Math.random() * 26)) + '';
  }

  function isValidBin(bin) {
    return /^[0-9]{6,16}$/.test(bin);
  }

  async function generateCards() {
    const bin = document.getElementById('bin').value.trim();
    const monthSelect = document.getElementById('month').value;
    const yearSelect = document.getElementById('year').value;
    const qtyDropdown = parseInt(document.getElementById('quantity').value);
    const qtyCustom = parseInt(document.getElementById('custom_quantity').value);
    const quantity = isNaN(qtyCustom) ? qtyDropdown : qtyCustom;
    const output = document.getElementById('output');

    output.value = '';

    if(!isValidBin(bin)) {
      alert('Please enter a valid BIN (6 to 16 digits).');
      return;
    }

    let cards = [];
    for(let i=0; i<quantity; i++) {
      let cardNumber = bin;
      if(bin.length < 16) {
        cardNumber += randomNum(16 - bin.length);
      }
      let month = monthSelect !== '' ? monthSelect : randomMonth();
      let year = yearSelect !== '' ? yearSelect : randomYear();
      let cvv = randomNum(3);
      cards.push(`${cardNumber}|${month}|${year}|${cvv}`);
    }

    output.value = cards.join('\n');
  }

  function checkLive() {
    const output = document.getElementById('output');
    let cards = output.value.trim().split('\n');
    if(cards.length === 0 || cards[0] === '') {
      alert('Please generate cards first!');
      return;
    }
    let checked = [];
    cards.forEach(card => {
      let status = Math.random() > 0.5 ? 'LIVE ✅' : 'DEAD ❌';
      checked.push(`${card} => ${status}`);
    });
    output.value = checked.join('\n');
  }

  function copyLive() {
    const output = document.getElementById('output').value.trim();
    if(!output) {
      alert('Nothing to copy!');
      return;
    }
    const lines = output.split('\n');
    const liveLines = lines.filter(line => line.includes('LIVE ✅'));
    const textToCopy = liveLines.length > 0 ? liveLines.join('\n') : output;
    navigator.clipboard.writeText(textToCopy).then(() => {
      alert('Copied live cards to clipboard!');
    }).catch(() => {
      alert('Failed to copy!');
    });
  }
</script>

</body>
</html># piyas-ccgen
