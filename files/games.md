<br>
<h2><center> NFL TEAMS, RECEIVES, TOUCHDOWNS, AND YARDS</center></h2>
<br>
<html>
<head>
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
<script src="https://cdn.jsdelivr.net/npm/pandas-js@1.2.0/dist/pandas.min.js"></script>

  <div id="maxValueTable"></div>
  <br>
  <div id="maxValueTableTouchdowns"></div>
  <br>
  <div id="maxValueTableYards"></div>
  <br>
  <div id="result"></div>


  
<script>
  const url = 'https://nfl-team-stats.p.rapidapi.com/v1/nfl-stats/teams/receiving-stats/offense/2019';
  let favoriteTeams = []; 
  let sortDirection = 'asc'; 
  let sortBy = 0; 

  function setCookie(name, value, days) {
    const expires = new Date();
    expires.setTime(expires.getTime() + (days * 24 * 60 * 60 * 1000));
    document.cookie = `${name}=${value};expires=${expires.toUTCString()};path=/`;
  }

  function getCookie(name) {
    const cookies = document.cookie.split(';');
    for (let i = 0; i < cookies.length; i++) {
      const cookie = cookies[i].trim();
      if (cookie.startsWith(`${name}=`)) {
        return cookie.substring(name.length + 1);
      }
    }
    return '';
  }

  function handleCheckboxChange(checkbox, teamName) {
    if (checkbox.checked) {
      favoriteTeams.push(teamName);
    } else {
      const index = favoriteTeams.indexOf(teamName);
      if (index !== -1) {
        favoriteTeams.splice(index, 1);
      }
    }
    console.log(favoriteTeams); 

    setCookie('favoriteTeams', JSON.stringify(favoriteTeams), 30);
  }

  function initializeCheckboxStates() {
    const favoriteTeamsCookie = getCookie('favoriteTeams');
    if (favoriteTeamsCookie) {
      favoriteTeams = JSON.parse(favoriteTeamsCookie);

      const checkboxes = document.querySelectorAll('input[type="checkbox"]');
      checkboxes.forEach(checkbox => {
        const teamName = checkbox.getAttribute('data-team-name');
        checkbox.checked = favoriteTeams.includes(teamName);
      });
    }
  }

  function sortTable(columnIndex) {
    const table = document.getElementById('teamTable');
    const tbody = table.querySelector('tbody');
    const rows = Array.from(tbody.querySelectorAll('tr'));

    sortDirection = sortDirection === 'asc' ? 'desc' : 'asc';
    sortBy = columnIndex - 1;

    const arrows = table.querySelectorAll('.arrow');
    arrows.forEach(arrow => arrow.classList.remove('up', 'down'));

    const arrow = arrows[columnIndex - 1];
    arrow.classList.add(sortDirection === 'asc' ? 'up' : 'down');

    rows.sort((rowA, rowB) => {
      const cellA = rowA.cells[columnIndex].textContent;
      const cellB = rowB.cells[columnIndex].textContent;
      return sortDirection === 'asc' ? cellA.localeCompare(cellB) : cellB.localeCompare(cellA);
    });

    while (tbody.firstChild) {
      tbody.removeChild(tbody.firstChild);
    }

    rows.forEach(row => tbody.appendChild(row));
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
      table.id = 'teamTable'; 

      const thead = document.createElement('thead');
      const headerRow = document.createElement('tr');
      const headers = ['Favorites', 'Team', 'Receives', 'Touchdowns', 'Yards'];

      headers.forEach((headerText, index) => {
        const th = document.createElement('th');
        if (index > 0) {
          const arrowUp = document.createElement('span');
          arrowUp.classList.add('arrow', 'up');
          arrowUp.addEventListener('click', () => sortTable(index));
          th.appendChild(arrowUp);
        }
        th.appendChild(document.createTextNode(headerText));
        if (index > 0) {
          const arrowDown = document.createElement('span');
          arrowDown.classList.add('arrow', 'down');
          arrowDown.addEventListener('click', () => sortTable(index));
          th.appendChild(arrowDown);
        }
        headerRow.appendChild(th);
      });

      thead.appendChild(headerRow);
      table.appendChild(thead);

      const tbody = document.createElement('tbody');
      data._embedded.teamReceivingStatsList.forEach(team => {
        const row = document.createElement('tr');

        const checkboxCell = document.createElement('td');
        const checkbox = document.createElement('input');
        checkbox.type = 'checkbox';
        checkbox.setAttribute('data-team-name', team.name);
