<!DOCTYPE html>
<html>
<head>
  <title>NFL Team Stats</title>
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
