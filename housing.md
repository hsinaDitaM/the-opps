<br>
<html>
<head>
  <title>GET Method Example</title>
  <style>
    table {
      border-collapse: collapse;
      width: 100%;
      background-color: #f0f0f0;
      box-shadow: 4px 4px 8px rgba(0, 0, 0, 0.1), -4px -4px 8px rgba(255, 255, 255, 0.5);
      border-radius: 10px;
    }

    th, td {
      border: 1px solid #e0e0e0;
      padding: 8px;
      text-align: left;
    }

    th {
      background-color: #e0e0e0;
      font-weight: bold;
    }

    tbody tr:nth-child(even) {
      background-color: #f8f8f8;
    }

    tbody tr:hover {
      background-color: #e0e0e0;
    }
  </style>
</head>
<body>

  <div id="result"></div>

  <script>
    const url = 'https://nfl-team-stats.p.rapidapi.com/v1/nfl-stats/teams/receiving-stats/offense/2019';
    let favoriteTeams = []; // Array to store the user's favorite teams

    function handleCheckboxChange(checkbox, teamName) {
      if (checkbox.checked) {
        // Add the team to the favorites array
        favoriteTeams.push(teamName);
      } else {
        // Remove the team from the favorites array
        const index = favoriteTeams.indexOf(teamName);
        if (index !== -1) {
          favoriteTeams.splice(index, 1);
        }
      }
      console.log(favoriteTeams); // You can perform further actions with the favoriteTeams array
    }

    fetch(url, {
      method: 'GET',
      headers: {
        'X-RapidAPI-Key': 'fdcfde47b5msh587d8d1cc3ff1dap13f3e3jsnb4f74da50f3e',
        'X-RapidAPI-Host': 'nfl-team-stats.p.rapidapi.com'
      }
    })
      .then(response => response.json())
      .then(data => {
        const table = document.createElement('table');
        
        // Create table header
        const thead = document.createElement('thead');
        const headerRow = document.createElement('tr');
        const headers = ['Favorites', 'Team', 'Receives', 'Touchdowns', 'Yards'];
        
        headers.forEach(headerText => {
          const th = document.createElement('th');
          th.appendChild(document.createTextNode(headerText));
          headerRow.appendChild(th);
        });
        
        thead.appendChild(headerRow);
        table.appendChild(thead);
        
        // Create table body
        const tbody = document.createElement('tbody');
        data._embedded.teamReceivingStatsList.forEach(team => {
          const row = document.createElement('tr');
          
          // Create checkbox cell
          const checkboxCell = document.createElement('td');
          const checkbox = document.createElement('input');
          checkbox.type = 'checkbox';
          checkbox.addEventListener('change', () => handleCheckboxChange(checkbox, team.name));
          checkboxCell.appendChild(checkbox);
          row.appendChild(checkboxCell);
          
          const columns = [team.name, team.receives, team.touchdowns, team.yards];
          
          columns.forEach(columnText => {
            const td = document.createElement('td');
            td.appendChild(document.createTextNode(columnText));
            row.appendChild(td);
          });
          
          tbody.appendChild(row);
        });
        
        table.appendChild(tbody);
        
        // Display the table
        document.getElementById('result').appendChild(table);
      })
      .catch(error => {
        console.error(error);
      });
  </script>
</body>
</html>
