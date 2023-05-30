<!DOCTYPE html>
<html>
<head>
	<title>NFL Team's History</title>
	<script>
		async function fetchData() {
			const url = 'https://nfl-team-stats1.p.rapidapi.com/teamStats';
			const options = {
				method: 'GET',
				headers: {
					'X-RapidAPI-Key': '31c2c9240dmshb093261393c2f95p1ac6bajsn3bf7b947282a',
					'X-RapidAPI-Host': 'nfl-team-stats1.p.rapidapi.com'
				}
			};
			try {
				const response = await fetch(url, options);
				const result = await response.json();
				console.log(result);
				// Create table
				const table = document.createElement('table');
				table.border = '1';
				// Create table header
				const headerRow = document.createElement('tr');
				for (const key in result[0]) {
					const headerCell = document.createElement('th');
					headerCell.textContent = key;
					headerRow.appendChild(headerCell);
				}
				table.appendChild(headerRow);
				// Create table rows
				for (const item of result) {
					const row = document.createElement('tr');
					for (const key in item) {
						const cell = document.createElement('td');
						cell.textContent = item[key];
						row.appendChild(cell);
					}
					table.appendChild(row);
				}
				// Append table to the HTML document
				document.getElementById('output').appendChild(table);
			} catch (error) {
				console.error(error);
			}
		}
	</script>
</head>
<body>
	<button onclick="fetchData()">Fetch Data</button>
	<div id="output"></div>
</body>
</html>
