<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>EMI Calculator</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    }

    body {
      background-color: #f0f2f5;
      display: flex;
      justify-content: center;
      align-items: center;
      min-height: 100vh;
    }

    .container {
      background-color: #ffffff;
      padding: 30px;
      border-radius: 10px;
      box-shadow: 0 0 15px rgba(0, 0, 0, 0.1);
      width: 100%;
      max-width: 400px;
    }

    .container h2 {
      text-align: center;
      color: #333;
      margin-bottom: 20px;
    }

    .form-group {
      margin-bottom: 15px;
    }

    .form-group label {
      font-weight: 600;
      display: block;
      margin-bottom: 5px;
      color: #444;
    }

    .form-group input {
      width: 100%;
      padding: 10px;
      font-size: 16px;
      border-radius: 6px;
      border: 1px solid #ccc;
    }

    .btn {
      width: 100%;
      padding: 12px;
      background-color: #007bff;
      color: #fff;
      font-size: 16px;
      border: none;
      border-radius: 6px;
      cursor: pointer;
      margin-top: 10px;
    }

    .btn:hover {
      background-color: #0056b3;
    }

    .result {
      margin-top: 20px;
      padding: 15px;
      background-color: #e9f7ef;
      border-left: 5px solid #28a745;
      border-radius: 6px;
      display: none;
    }

    .result p {
      font-size: 16px;
      margin: 8px 0;
      color: #333;
    }
  </style>
</head>
<body>

  <div class="container">
    <h2>EMI Calculator</h2>

    <div class="form-group">
      <label for="amount">Loan Amount (₹):</label>
      <input type="number" id="amount" placeholder="Enter loan amount">
    </div>

    <div class="form-group">
      <label for="rate">Annual Interest Rate (%):</label>
      <input type="number" id="rate" placeholder="Enter interest rate">
    </div>

    <div class="form-group">
      <label for="tenure">Loan Tenure (months):</label>
      <input type="number" id="tenure" placeholder="Enter loan tenure">
    </div>

    <button class="btn" onclick="calculateEMI()">Calculate EMI</button>

    <div class="result" id="result">
      <p id="emiOutput"></p>
      <p id="interestOutput"></p>
      <p id="totalOutput"></p>
    </div>
  </div>

  <script>
    function calculateEMI() {
      const amount = parseFloat(document.getElementById("amount").value);
      const rate = parseFloat(document.getElementById("rate").value);
      const tenure = parseFloat(document.getElementById("tenure").value);

      if (isNaN(amount) || isNaN(rate) || isNaN(tenure) || amount <= 0 || rate <= 0 || tenure <= 0) {
        alert("Please enter valid, positive numbers.");
        return;
      }

      const monthlyRate = rate / 12 / 100;
      const emi = (amount * monthlyRate * Math.pow(1 + monthlyRate, tenure)) /
                  (Math.pow(1 + monthlyRate, tenure) - 1);

      const totalPayment = emi * tenure;
      const totalInterest = totalPayment - amount;

      document.getElementById("emiOutput").innerText = `Monthly EMI: ₹${emi.toFixed(2)}`;
      document.getElementById("interestOutput").innerText = `Total Interest: ₹${totalInterest.toFixed(2)}`;
      document.getElementById("totalOutput").innerText = `Total Payment: ₹${totalPayment.toFixed(2)}`;

      document.getElementById("result").style.display = "block";
    }
  </script>

</body>
</html>
