<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Flash Bitcoin Wallet (Demo)</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #121212;
      color: #f2f2f2;
      padding: 40px;
      max-width: 500px;
      margin: auto;
    }
    .wallet {
      background-color: #1e1e1e;
      padding: 20px;
      border-radius: 10px;
      box-shadow: 0 0 20px rgba(255, 255, 255, 0.1);
    }
    .wallet h2 {
      text-align: center;
      color: #f2a900;
    }
    input, button {
      width: 100%;
      padding: 10px;
      margin: 10px 0;
      border: none;
      border-radius: 5px;
      font-size: 16px;
    }
    button {
      background-color: #f2a900;
      color: #000;
      font-weight: bold;
      cursor: pointer;
    }
    .transactions {
      margin-top: 20px;
    }
    .tx {
      border-bottom: 1px solid #333;
      padding: 10px 0;
    }
  </style>
</head>
<body>
  <div class="wallet">
    <h2>Flash BTC Wallet</h2>
    <p><strong>Fake Wallet Address:</strong> <span id="btcAddress"></span></p>
    <p><strong>Fake Balance:</strong> <span id="btcBalance">10.00000000 BTC</span></p>

    <label for="newBalance">Update Fake Balance:</label>
    <input type="number" step="0.00000001" id="newBalance" placeholder="Enter new balance"/>
    <button onclick="updateBalance()">Set Fake Balance</button>

    <div class="transactions">
      <h3>Transaction History</h3>
      <div class="tx">⬅ Received 5.00000000 BTC from 1ExAmpleAddr... [Confirmed]</div>
      <div class="tx">➡ Sent 2.00000000 BTC to 1RandomAddr... [Confirmed]</div>
      <div class="tx">⬅ Received 7.00000000 BTC from 1AnotherAddr... [Pending]</div>
    </div>
  </div>

  <script>
    function generateFakeBTCAddress() {
      const chars = '123456789ABCDEFGHJKLMNPQRSTUVWXYZabcdefghijkmnopqrstuvwxyz';
      let address = '1';
      for (let i = 0; i < 33; i++) {
        address += chars[Math.floor(Math.random() * chars.length)];
      }
      return address;
    }

    document.getElementById('btcAddress').textContent = generateFakeBTCAddress();

    function updateBalance() {
      const newBalance = document.getElementById('newBalance').value;
      if (newBalance !== '') {
        document.getElementById('btcBalance').textContent = parseFloat(newBalance).toFixed(8) + ' BTC';
        alert('✅ Fake balance updated.');
      } else {
        alert('❌ Please enter a valid number.');
      }
    }
  </script>
</body>
</html>
