# sum-of-sales-sales1236yxyz

## Round 2 Updates
# Error
The LLM did not include Round 2 Updates.

## Round 2 Updates
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Sales Summary cHJvZHVjdCxwcmljZSxzYWxlcwpBcHBsZSwxLjIwLDMw</title>
  <!-- Bootstrap 5.3.3 from CDN with fallback CSS -->
  <link
    href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css"
    rel="stylesheet"
    integrity="sha384-9NDjNTl5x0LJZh/BCl8poLZ1dxV23CJbVY6QBlR229Kf4kE6kRpBww626fElRS4fw"
    crossorigin="anonymous"
    onerror="loadFallbackCSS()"
  />
  <style>
    /* Fallback CSS if Bootstrap fails to load */
    @media all {
      body {
        font-family: Arial, sans-serif;
        background-color: #f8f9fa;
        padding: 1rem;
        color: #212529;
      }
      .container {
        max-width: 800px;
        margin: auto;
        background: #fff;
        padding: 1rem;
        border-radius: 0.5rem;
        box-shadow: 0 0 10px rgba(0,0,0,0.1);
      }
      h1 {
        font-size: 1.75rem;
        margin-bottom: 1rem;
      }
      .mt-3 {
        margin-top: 1rem;
      }
    }
  </style>
</head>
<body class="p-4" onload="initializeApp()">
  <div class="container">
    <h1>Sales Summary</h1>
    <div class="mt-3 d-flex flex-column gap-2 align-items-start">
      <div class="d-flex align-items-center">
        <label for="currency-picker" class="form-label me-2 mb-0">Select Currency:</label>
        <select id="currency-picker" class="form-select" aria-label="Currency picker">
          <option value="USD">USD</option>
          <option value="EUR">EUR</option>
          <option value="GBP">GBP</option>
          <option value="TH">TH</option>
        </select>
      </div>
      <div class="d-flex align-items-center">
        Total Sales: <span id="total-sales" class="mx-2">0</span>
        <span id="total-currency" class="fw-bold">USD</span>
      </div>
    </div>
  </div>
  <script>
    function loadFallbackCSS() {
      // Fallback CSS already included in <style> tag
      // Optionally, you could set a flag here if needed
    }

    function initializeApp() {
      const seed = 'cHJvZHVjdCxwcmljZSxzYWxlcwpBcHBsZSwxLjIwLDMw';
      const dataCsv = `product,price,sales
Apple,1.20,30
Orange,1.45,40`;
      const ratesJsonStr = '{"TH":1.0,"EUR":0.85,"GBP":0.75}';

      // Set document title with seed
      document.title = `Sales Summary ${seed}`;

      const rates = JSON.parse(ratesJsonStr);
      const currencyPicker = document.querySelector('#currency-picker');
      const totalElem = document.querySelector('#total-sales');
      const totalCurrencyElem = document.querySelector('#total-currency');

      // Parse CSV
      function parseCSV(csv) {
        const lines = csv.trim().split('\n');
        const headers = lines[0].split(',');
        const salesIndex = headers.indexOf('sales');
        let totalSales = 0;
        for(let i = 1; i < lines.length; i++) {
          const cols = lines[i].split(',');
          const salesValue = parseFloat(cols[salesIndex]);
          if (!isNaN(salesValue)) {
            totalSales += salesValue;
          }
        }
        return totalSales;
      }

      const totalSalesUSD = parseCSV(dataCsv);

      // Function to update total display based on selected currency
      function updateTotal() {
        const selectedCurrency = currencyPicker.value;
        const rate = rates[selectedCurrency];
        if (typeof rate !== 'number') {
          console.error(`Rate for currency ${selectedCurrency} not found.`);
          return;
        }
        const convertedTotal = totalSalesUSD * rate;
        totalElem.textContent = convertedTotal.toFixed(2);
        totalCurrencyElem.textContent = selectedCurrency;
      }

      // Verify presence of options
      if (!document.querySelector('#currency-picker option[value="USD"]')) {
        console.error('Currency option USD not found');
      }

      // Verify total currency element
      if (!document.querySelector('#total-currency')) {
        console.error('#total-currency element not found');
      }

      // Initialize total display
      updateTotal();

      // Event listener for currency change
      currencyPicker.addEventListener('change', updateTotal);
    }
  </script>
</body>
</html>
# Sales Summary Web App

This web application displays the total sales parsed from CSV data, allows users to select a currency, and converts the total sales based on preloaded exchange rates. The app uses Bootstrap 5.3.3 for styling, with a fallback CSS for basic styling if Bootstrap fails to load.

## Features

- Parses embedded CSV data to compute total sales.
- Presents a dropdown to select between USD, EUR, GBP, and TH.
- Converts total sales according to rates specified in JSON.
- Mirrors the active currency in the total display.
- Ensures accessibility and responsive design.

## Usage

Open the `index.html` file in a modern browser. Use the dropdown to select the desired currency, and see the total sales update accordingly.

## Development

The entire logic is contained within the `<script>` tag in the HTML file, ensuring a strictly client-side implementation without external dependencies beyond Bootstrap CDN.

## Future Improvements

- Load CSV and rates from external files or APIs.
- Add more currencies and error handling.
- Persist user currency preference using localStorage.

## Validations

The app performs the following checks:

- Ensures the currency select has an option with value "USD".
- Checks for the existence of the total currency display element.
- Maintains existing functionality and structure.