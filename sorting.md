# PLAN
1. Data Structure: Define a data structure to store NBA statistics. For example, you can create a class called PlayerStats with attributes like name, points, rebounds, assists, etc. You can also create a list to store instances of the PlayerStats class.
 
<html>
<head>
  <title>Player Stats</title>
  <script>
    class PlayerStats {
      constructor(name, points, rebounds, assists) {
        this.name = name;
        this.points = points;
        this.rebounds = rebounds;
        this.assists = assists;
      }
    }
    var playerStatsList = [
      new PlayerStats("LeBron James", 27.4, 8.5, 7.4),
      new PlayerStats("Stephen Curry", 30.1, 5.5, 6.2),
      new PlayerStats("Kevin Durant", 29.3, 7.1, 5.6),
      new PlayerStats("Giannis Antetokounmpo", 28.1, 11.0, 6.1)
    ];
    function sortStatsByAttribute(statsList, attribute) {
      return statsList.sort(function(a, b) {
        return a[attribute] - b[attribute];
      });
    }
    function printStats(statsList) {
      var table = document.getElementById("statsTable");
      table.innerHTML = ""; 
      for (var i = 0; i < statsList.length; i++) {
        var player = statsList[i];
        var row = document.createElement("tr");
        var nameCell = document.createElement("td");
        nameCell.textContent = player.name;
        row.appendChild(nameCell);
        var pointsCell = document.createElement("td");
        pointsCell.textContent = player.points;
        row.appendChild(pointsCell);
        var reboundsCell = document.createElement("td");
        reboundsCell.textContent = player.rebounds;
        row.appendChild(reboundsCell);
        var assistsCell = document.createElement("td");
        assistsCell.textContent = player.assists;
        row.appendChild(assistsCell);
        table.appendChild(row);
      }
    }
    var sortedStats = sortStatsByAttribute(playerStatsList, 'points');
    printStats(sortedStats);
  </script>
</head>
<body>
  <h1>Player Stats</h1>
  <table id="statsTable">
    <tr>
      <th>Name</th>
      <th>Points</th>
      <th>Rebounds</th>
      <th>Assists</th>
    </tr>
  </table>
</body>
</html>


