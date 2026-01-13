<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Transaction Recorder</title>
  <style>
    body { font-family: Arial, sans-serif; margin: 40px; }
    h1 { margin-bottom: 20px; }
    form { max-width: 400px; margin-bottom: 30px; }
    label { display: block; margin-top: 10px; }
    input, button { width: 100%; padding: 8px; margin-top: 5px; }
    table { border-collapse: collapse; width: 100%; }
    th, td { border: 1px solid #ccc; padding: 8px; text-align: left; }
    th { background-color: #f4f4f4; }
  </style>
</head>
<body>
  <h1>Transaction Recorder</h1>

  <form id="transactionForm">
    <label>
      Description
      <input type="text" id="description" required />
    </label>
    <label>
      Amount
      <input type="number" id="amount" required />
    </label>
    <label>
      Date
      <input type="date" id="date" required />
    </label>
    <button type="submit">Add Transaction</button>
  </form>

  <table>
    <thead>
      <tr>
        <th>Description</th>
        <th>Amount</th>
        <th>Date</th>
      </tr>
    </thead>
    <tbody id="transactionTable"></tbody>
  </table>

  <script>
    const form = document.getElementById('transactionForm');
    const tableBody = document.getElementById('transactionTable');

    function loadTransactions() {
      const transactions = JSON.parse(localStorage.getItem('transactions')) || [];
      tableBody.innerHTML = '';
      transactions.forEach(t => addRow(t));
    }

    function addRow(transaction) {
      const row = document.createElement('tr');
      row.innerHTML = `
        <td>${transaction.description}</td>
        <td>${transaction.amount}</td>
        <td>${transaction.date}</td>
      `;
      tableBody.appendChild(row);
    }

    form.addEventListener('submit', function (e) {
      e.preventDefault();
      const transaction = {
        description: description.value,
        amount: amount.value,
        date: date.value
      };
      const transactions = JSON.parse(localStorage.getItem('transactions')) || [];
      transactions.push(transaction);
      localStorage.setItem('transactions', JSON.stringify(transactions));
      addRow(transaction);
      form.reset();
    });

    loadTransactions();
  </script>
</body>
</html>
