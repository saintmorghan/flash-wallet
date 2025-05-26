<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Live BTC Wallet Viewer</title>
  <style>
    body {
      background: #121212;
      color: #fff;
      font-family: Arial, sans-serif;
      text-align: center;
      padding: 40px;
    }
    .wallet {
      background: #1f1f1f;
      padding: 30px;
      border-radius: 10px;
      display: inline-block;
      box-shadow: 0 0 20px rgba(255,255,255,0.1);
    }
    input {
      padding: 10px;
      width: 100%;
      margin-top: 10px;
      font-size: 16px;
      border: none;
      border-radius: 5px;
    }
    button {
      padding: 10px 20px;
      margin-top: 15px;
      background: gold;
      color: #000;
      border: none;
      font-weight: bold;
      border-radius: 5px;
      cursor: pointer;
    }
    .result {
      margin-top: 20px;
      font-size: 18px;
    }
  </style>
</head>
<body>

  <div class="wallet">
    <h2>Check Bitcoin Wallet Balance</h2>
    <input type="text" id="btcAddress" placeholder="Enter BTC Address"/>
    <button onclick="checkBalance()">Check Balance</button>
    <div class="result" id="balanceResult"></div>
  </div>

  <script>
    async function checkBalance() {
      const address = document.getElementById('btcAddress').value.trim();
      const result = document.getElementById('balanceResult');

      if (!address) {
        result.textContent = "⚠️ Please enter a Bitcoin address.";
        return;
      }

      result.textContent = "Checking...";
      
      try {
        const res = await fetch(`https://blockchain.info/q/addressbalance/${address}?confirmations=6`);
        const satoshis = await res.text();
        const btc = (parseInt(satoshis) / 1e8).toFixed(8);
        result.innerHTML = `💰 Balance for <strong>${address}</strong>:<br><span style="font-size: 22px; color: lightgreen;">${btc} BTC</span>`;
      } catch (e) {
        result.textContent = "❌ Error fetching balance. Address might be invalid.";
      }
    }
  </script>

</body>
</html>
