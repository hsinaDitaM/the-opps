
<html>
<head>
<<<<<<< HEAD
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
=======
  <title>NFL Team Stats</title>
>>>>>>> 969c2849ed05bfc0d47f7b31fd72e2496b7ae433
</head>
<body>
  <div id="output"></div>

  <script>
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
        const result = await response.text();
        outputElement.innerText = result;
      } catch (error) {
        console.error(error);
      }
    }

    fetchData();

  </script>
</body>
</html>
