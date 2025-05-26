async function checkBTC() {
  const address = document.getElementById('btcAddress').value.trim();
  const result = document.getElementById('btcResult');
  const txsResult = document.getElementById('btcTxs');

  if (!address) {
    result.textContent = "⚠️ Please enter a Bitcoin address.";
    return;
  }

  result.textContent = "Checking BTC balance...";
  txsResult.textContent = "";

  try {
    // Get BTC Balance
    const balRes = await fetch(`https://blockchain.info/q/addressbalance/${address}?confirmations=6`);
    const satoshis = await balRes.text();
    const btc = (parseInt(satoshis) / 1e8).toFixed(8);
    result.innerHTML = `💰 <strong>${btc} BTC</strong>`;

    // Get recent transactions
    const txRes = await fetch(`https://blockchain.info/rawaddr/${address}`);
    const txData = await txRes.json();

    const txs = txData.txs.slice(0, 5); // First 5
    let txList = `<h4 style="margin-top:20px;">Recent Transactions</h4><ul style="text-align:left;">`;

    txs.forEach(tx => {
      const date = new Date(tx.time * 1000).toLocaleString();
      const total = tx.result / 1e8;
      const direction = total >= 0 ? "Received" : "Sent";
      const amount = Math.abs(total).toFixed(8);

      txList += `<li>📅 ${date} – <strong>${direction}</strong>: ${amount} BTC</li>`;
    });

    txList += `</ul>`;
    txsResult.innerHTML = txList;

  } catch (e) {
    result.textContent = "❌ Error fetching BTC data.";
    txsResult.textContent = "";
  }
}
