<!DOCTYPE html>
<html>
<head>
	<title>Fetch API Example</title>
	<script>
		function fetchData() {
			const url = 'https://odds.p.rapidapi.com/v4/sports?all=true';
			const options = {
				method: 'GET',
				headers: {
					'X-RapidAPI-Key': '31c2c9240dmshb093261393c2f95p1ac6bajsn3bf7b947282a',
					'X-RapidAPI-Host': 'odds.p.rapidapi.com'
				}
			};
			fetch(url, options)
				.then(response => response.text())
				.then(result => {
					// Output the result to the HTML document
					document.getElementById('output').textContent = result;
				})
				.catch(error => {
					console.error(error);
				});
		}
	</script>
</head>
<body>
	<button onclick="fetchData()">Fetch Data</button>
	<div id="output"></div>
</body>
</html>
