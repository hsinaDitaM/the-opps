
<html>
<head>
  <title>Upcoming Games</title>
  <style>
    table {
      border-collapse: collapse;
      width: 100%;
    }

    th, td {
      padding: 8px;
      text-align: left;
      border-bottom: 1px solid #ddd;
    }

    th {
      background-color: #f2f2f2;
    }
  </style>
</head>
<body>
  <h1>Upcoming Games</h1>
  <table id="resultTable">
    <thead>
      <tr>
        <th>Home Team</th>
        <th>Away Team</th>
        <th>Status</th>
        <th>Date</th>
      </tr>
    </thead>
    <tbody id="resultBody"></tbody>
  </table>

  <script>
    const url = 'https://football-data1.p.rapidapi.com/tournament/fixture?tournamentId=9';
    const options = {
      method: 'GET',
      headers: {
        'X-RapidAPI-Key': 'fdcfde47b5msh587d8d1cc3ff1dap13f3e3jsnb4f74da50f3e',
        'X-RapidAPI-Host': 'football-data1.p.rapidapi.com'
      }
    };

    async function fetchData() {
      try {
        const response = await fetch(url, options);
        const data = await response.json();
        const resultBody = document.getElementById('resultBody');

        data.forEach(fixture => {
          const row = document.createElement('tr');
          const homeTeamCell = document.createElement('td');
          homeTeamCell.textContent = fixture.homeTeam.name;
          row.appendChild(homeTeamCell);

          const awayTeamCell = document.createElement('td');
          awayTeamCell.textContent = fixture.awayTeam.name;
          row.appendChild(awayTeamCell);

          const statusCell = document.createElement('td');
          statusCell.textContent = fixture.status.name;
          row.appendChild(statusCell);

          const dateCell = document.createElement('td');
          dateCell.textContent = fixture.date;
          row.appendChild(dateCell);

          resultBody.appendChild(row);
        });
      } catch (error) {
        console.error(error);
      }
    }

    fetchData();
  </script>
</body>
</html>
