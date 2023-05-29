## Team Stats

<!DOCTYPE html>
<html>
<head>
  <title>Team Information</title>
</head>
<body>
  <h1>Team Information</h1>
  <label for="searchInput">Search:</label>
  <input type="text" id="searchInput" placeholder="Enter team name">
  <div id="teamContainer"></div>

  <script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
  <script>
    const apiKey = '31c2c9240dmshb093261393c2f95p1ac6bajsn3bf7b947282a';
    const apiUrl = 'https://nfl-team-stats.p.rapidapi.com/v1/nfl-stats/teams/receiving-stats/offense/2019'; // Replace with your API URL
    // Fetch team data from the API
    axios.get(apiUrl, {
      headers: {
        'Authorization': `Bearer ${apiKey}`
      }
    })
    .then(response => {
      const data = response.data;
      // Sort teams alphabetically by name
      const sortedTeams = bubbleSort(data.teams, 'name');
      // Display team information
      const teamContainer = document.getElementById('teamContainer');
      sortedTeams.forEach(team => {
        const teamElement = createTeamElement(team);
        teamContainer.appendChild(teamElement);
      });
      // Filter teams based on search input
      const searchInput = document.getElementById('searchInput');
      searchInput.addEventListener('input', () => {
        const filterValue = searchInput.value.toLowerCase();
        const filteredTeams = sortedTeams.filter(team => team.name.toLowerCase().includes(filterValue));
        teamContainer.innerHTML = '';
        filteredTeams.forEach(team => {
          const teamElement = createTeamElement(team);
          teamContainer.appendChild(teamElement);
        });
      });
    })
    .catch(error => {
      console.error('Error fetching team data:', error);
    });
    // Bubble sort algorithm
    function bubbleSort(array, key) {
      const arr = [...array];
      const length = arr.length;
      for (let i = 0; i < length - 1; i++) {
        for (let j = 0; j < length - i - 1; j++) {
          if (arr[j][key] > arr[j + 1][key]) {
            const temp = arr[j];
            arr[j] = arr[j + 1];
            arr[j + 1] = temp;
          }
        }
      }
      return arr;
    }
    // Create HTML element for displaying team information
    function createTeamElement(team) {
      const teamElement = document.createElement('div');
      teamElement.innerHTML = `
        <h2>${team.name}</h2>
        <p>Location: ${team.location}</p>
        <p>Founded: ${team.founded}</p>
        <hr>
      `;
      return teamElement;
    }
  </script>
</body>
</html>
