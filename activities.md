
<html>
<head>
    <title>NFL Team Data Visualizer</title>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
</head>
<body>
    <div>
        <select id="teamSelector">
            <option value="">Select a team</option>
            <option value="NE">New England Patriots</option>
            <option value="KC">Kansas City Chiefs</option>
            <option value="TB">Tampa Bay Buccaneers</option>
            <!-- Add more teams as needed -->
        </select>
    </div>
    <div>
        <canvas id="chart"></canvas>
    </div>

  <script>
        document.addEventListener("DOMContentLoaded", function () {
            var teamSelector = document.getElementById("teamSelector");
            var chartCanvas = document.getElementById("chart");
            var ctx = chartCanvas.getContext("2d");
            var chart;

            // Define your team data
            var teamData = {
                NE: {
                    label: "New England Patriots",
                    data: [11 Wins, 12 Wins, 7 Wins, 10 Wins, 8 Wins] // Example data, replace with your own
                },
                KC: {
                    label: "Kansas City Chiefs",
                    data: [70, 80, 90, 80, 70] // Example data, replace with your own
                },
                TB: {
                    label: "Tampa Bay Buccaneers",
                    data: [80, 70, 60, 50, 40] // Example data, replace with your own
                }
                // Add more teams with their respective data
            };

            // Function to update the chart
            function updateChart(team) {
                var data = teamData[team].data;
                var label = teamData[team].label;

                if (chart) {
                    chart.destroy();
                }

                chart = new Chart(ctx, {
                    type: "bar",
                    data: {
                        labels: ["2018", "2019", "2020", "2021", "2022"],
                        datasets: [
                            {
                                label: label,
                                data: data,
                                backgroundColor: "rgba(75, 192, 192, 0.6)",
                                borderColor: "rgba(75, 192, 192, 1)",
                                borderWidth: 1
                            }
                        ]
                    },
                    options: {
                        responsive: true,
                        scales: {
                            y: {
                                beginAtZero: true
                            }
                        }
                    }
                });
            }

            // Event listener for team selection
            teamSelector.addEventListener("change", function () {
                var selectedTeam = teamSelector.value;
                if (selectedTeam) {
                    updateChart(selectedTeam);
                }
            });
        });
    </script>
</body>
</html>
