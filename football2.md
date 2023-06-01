<!DOCTYPE html>
<html>
<head>
    <title>API Fetch Example</title>
</head>
<body>
    <script>
        const url = 'https://americanfootballapi.p.rapidapi.com/api/american-football/search/brady';
        const options = {
            method: 'GET',
            headers: {
                'X-RapidAPI-Key': 'SIGN-UP-FOR-KEY',
                'X-RapidAPI-Host': 'americanfootballapi.p.rapidapi.com'
            }
        };

        async function fetchData() {
            try {
                const response = await fetch(url, options);
                const result = await response.text();
                console.log(result);
            } catch (error) {
                console.error(error);
            }
        }

        // Call the fetchData function
        fetchData();
    </script>
</body>
</html>
