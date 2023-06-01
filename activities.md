
<html>
<head>
  <title>NFL Team History</title>
  <style>
    table {
      border-collapse: collapse;
      width: 100%;
    }

    th, td {
      border: 1px solid #ddd;
      padding: 8px;
      text-align: left;
    }
    
    th {
      background-color: #f2f2f2;
    }

  </style>
</head>
<body>
  <div id="output"></div>

  <script>
    document.addEventListener("DOMContentLoaded", function() {
      const url = 'https://nfl-team-stats1.p.rapidapi.com/teamStats';
      const options = {
        method: 'GET',
        headers: {
          'X-RapidAPI-Key': '31c2c9240dmshb093261393c2f95p1ac6bajsn3bf7b947282a',
          'X-RapidAPI-Host': 'nfl-team-stats1.p.rapidapi.com'
        }
      };

      const outputElement = document.getElementById('output');

      async function fetchData() {
        try {
          const response = await fetch(url, options);
          const data = await response.json();
          createTable(data);
        } catch (error) {
          console.error(error);
        }
      }

      function createTable(data) {
        const table = document.createElement('table');

        // Create table header
        const thead = document.createElement('thead');
        const headerRow = document.createElement('tr');
        for (const key in data[0]) {
          const th = document.createElement('th');
          th.textContent = key;
          headerRow.appendChild(th);
        }
        thead.appendChild(headerRow);
        table.appendChild(thead);

        // Create table body
        const tbody = document.createElement('tbody');
        data.forEach((item) => {
          const row = document.createElement('tr');
          for (const key in item) {
            const td = document.createElement('td');
            td.textContent = item[key];
            row.appendChild(td);
          }
          tbody.appendChild(row);
        });
        table.appendChild(tbody);

        outputElement.appendChild(table);
      }

      fetchData();
    });
  </script>
</body>
</html>
